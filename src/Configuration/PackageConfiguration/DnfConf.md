# Dnf Conf

Dnf is slow out of the box, You need to setup mirrors and max parallel downloads in order to get high speeds and more parallel downloads.

Out of the box dnf has max_parallel_downloads=3 which just downloads 3 packages at a time. The mirror by default is set according to your location.

go to `/etc/dnf/dnf.conf` and edit it with your text editor.

```conf
see `man dnf.conf` for defaults and possible options

[main]
fastestmirror=True
max_parallel_downloads=10
```

I personally choose 10 as max_parallel_downloads but you can choose that according to your needs.

After editing the config file you need to refresh dnf to setup the fastestmirror. This process may take a while.

```bash
sudo dnf clean all
sudo dnf update -n
```
