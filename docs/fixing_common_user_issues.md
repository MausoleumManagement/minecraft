
Teleport a player to another player's location
```bash
k -n minecraft exec -it deploy/minecraft -- rcon-cli teleport PatrisioSeFuerte 5500PowerLiches
```

Using `F3`, you can determine your current position and use that for the teleport command.

```bash
k -n minecraft exec -it deploy/minecraft -- rcon-cli teleport PatrisioSeFuerte 1472 69 1161
```
