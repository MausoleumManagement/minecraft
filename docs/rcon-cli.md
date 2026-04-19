We can execute rcon commands via the `rcon-cli` tool. They work the same like the documented commands for minecraft, except we don't prefix them with a `/`, i.e. instead of `/gamerule abc 123` we run `rcon-cli gamerule abc 123`

```
k -n minecraft exec -it deploy/minecraft -- rcon-cli gamerule playersSleepingPercentage 50
```
