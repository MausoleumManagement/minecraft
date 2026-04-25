# Ways of Messing with the Config

## Server Properties
- https://docker-minecraft-server.readthedocs.io/en/latest/configuration/server-properties/


## General Config

Configuration values in files can be overridden / templated into them via special env vars
https://docker-minecraft-server.readthedocs.io/en/latest/configuration/interpolating/#replacing-variables-inside-configs


The minecraft container image allows patching config files inside the container via JSON patches
- https://docker-minecraft-server.readthedocs.io/en/latest/configuration/interpolating/#patching-existing-files


## JVM Options

### Our image

https://docker-minecraft-server.readthedocs.io/en/latest/configuration/jvm-options/
https://docker-minecraft-server.readthedocs.io/en/latest/configuration/jvm-options/#extra-jvm-options

### G1GC

https://aikar.co/2018/07/02/tuning-the-jvm-g1gc-garbage-collector-flags-for-minecraft/
https://docs.papermc.io/paper/aikars-flags/


### Meowice
https://github.com/MeowIce/meowice-flags

### ZGC
There's some prior art on this: https://github.com/1ByteBit/ZGC-For-Minecraft