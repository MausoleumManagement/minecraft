
## Delete Erroring Entities

We can nuke any (block) entity throwing errors in their update / tick methods instead of crashing the server. This is obviously destructive, but may help in a pinch. Remember to turn it off again after fixing something. The settings are in `./config/neoforge-server.toml`.

```
removeErroringBlockEntities = true
removeErroringEntities = true
```

