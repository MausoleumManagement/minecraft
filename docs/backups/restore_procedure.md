## Restoring Restic Backups

If we want to perform any steps inside the server pod, or the backup sidecar itself, here's the commands:
```bash
k -n minecraft exec -it deploy/minecraft -c minecraft -- bash
k -n minecraft exec -it deploy/minecraft -c minecraft-mc-backup -- bash
```

Either of these pods can run `rcon-cli` commands.

Turn on Server whitelist so that we can work in quiet
```bash
rcon-cli whitelist list
rcon-cli whitelist on
```

Kick any connected players
```bash
rcon-cli list
rcon-cli kick Bob 'Server going down for maintenance; expected outage: 30m'
```

Save server state to disk, then turn off autosave
```bash
rcon-cli save-all flush
rcon-cli save-off
```

Run backup from sidecar container (has all the required env vars set), so we don't destroy anything we don't want to destroy
```bash
restic backup --tag mc_backups --tag "$BACKUP_NAME" --host "$RESTIC_HOSTNAME" "$SRC_DIR"
```

The sidecar can only read, because the datadir volume is mounted as read-only...
Likewise the server container can only read but not write on tbe backup volume
This makes stuff too fiddly, so we use a temporary debug container instead


```bash
k -n minecraft scale deploy minecraft --replicas 0
k -n minecraft apply -f docs/backups/restore-pod.yaml
k -n minecraft exec -it minecraft-restore -- bash
```

List snapshots and select an applicable one
```bash
restic snapshots
```

Restore snapshot and replace the necessary files (in this example, we just replace the `world` subdirectory, i.e. the minecraft world state). Since we took a snapshot before, we do not bother with storing the old world state.

```bash
restic restore ed888d6b --target /backups/restore20260406
rm -rf /data/world/
mv /backups/restore20260406/data/world/ /data/
rm -rf /backups/*
```


Now we can get rid of the restore-pod and start our server again 
```bash
k -n minecraft delete pod minecraft-restore
k -n minecraft scale deploy minecraft --replicas 1
```

Test connecting to the server and, if everything looks like it should, we're done.