
## Restic Backups
Usually, when using restic interactively, the s3-bucket needs to be initialised with 

 ```bash
 restic -r s3:BUCKET-URL init
 ```
 
 In our case, the sidecar container takes care of that. Restic always encrypts backups, and a password needs to be provided for reading and writing them. Refer to our Password Storage for that. see [here](https://restic.readthedocs.io/en/latest/030_preparing_a_new_repo.html#amazon-s3)

Once some backups have been written to the bucket, we can access them via restic directly. Since restic encrypts the files and does all kinds of voodoo to them, accessing the bucket via e.g. `rclone` is not very useful.

```bash
bao login
bao kv get -mount=kv nekropolis/minecraft/minecraft-restic

export AWS_ACCESS_KEY_ID=ayyy
export AWS_SECRET_ACCESS_KEY=lmaoo
```

To see what restic is storing in the bucket, run the following command. Restic will ask us for the encryption password; that should be displayed by the openbao command above as well.
```bash
restic -r  s3:http://garage.irminsul:3900/minecraft-backups/restic snapshots
```

We can then restore one of our backups to the local disk, for example
```bash
restic -r  s3:http://garage.irminsul:3900/minecraft-backups/restic restore latest --target /tmp/restore
```
