We have an S3-bucket in garage, that gets publicised as a website (see our wiki on how that works):


Here's the relevant `rclone` config
```
[minecraft-modpacks-s3-bucket]
type = s3
provider = Other
access_key_id = ...
secret_access_key = ...
endpoint = http://garage.irminsul:3900
acl = public-read
```

To upload new modpacks, run
```
rclone copy ~/Downloads/All_the_Mods_10-6.4.zip minecraft-modpacks-s3-bucket:minecraft-modpacks
```

The publicised "website" is a subdomain of the garage server name (handled via pihole), which is equivalent to the bucket name. Note, that the HTTP API is reachable on `3902`, not the port of the S3-API `3900`
```
wget http://minecraft-modpacks.garage.irminsul:3902/All_the_Mods_10-6.4.zip
```

The garage devs are working on allowing anonymous S3-access but for now, this should work.
