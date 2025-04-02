```shell
sudo nano /var/lib/flatpak/exports/share/applications/com.spotify.Client.desktop
```

on exec line go to end append `-no-zygote`

Check if it works:

```shell
ps aux | grep -i spot | grep -i zy
# /usr/bin/bwrap --args 41 -- spotify -no-zygote
```