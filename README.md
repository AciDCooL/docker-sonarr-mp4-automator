# arontx/sonarr || Clone! ||

Clone of arontx config, but with ffmpeg 4.x instead of 3.1 to support all functions and files.

Problem started with that I had files that where stuck with the mp4automator and with an updated ffmpeg I got rid of this problem. Instead of the workaround (kill -9 PID) every time something got stuck.


## Usage
````
docker create \
    --name sonarr \
    --restart unless-stopped \
    -p 8989:8989 \
    -e PUID=1001 -e PGID=1001 \
    -e TZ="America/Chicago"  \
    -v <path to data>:/config \
    -v <path to data>/mp4_automator:/config_mp4_automator \
    -v <path to data>:/movies \
    -v <path to data>:/downloads \
    aront/sonarr
    
mkdir <path to data>/mp4_automator && \
wget https://raw.githubusercontent.com/mdhiggins/sickbeard_mp4_automator/master/autoProcess.ini.sample -O <path to data>/mp4_automator/autoProcess.ini
````

## Parameters
See [https://hub.docker.com/r/linuxserver/sonarr/](https://hub.docker.com/r/linuxserver/sonarr/) for details.

## mkdir
Makes a symlink from sickbeard_mp4_automator to a config directory that is a volume for the container. If the host has a config file (autoProcess.ini) in the mounted volume, then sickbeard_mp4_automator will be able to use that. This is useful if you are running multiple containers but want to share the mp4 automation configuration between them. It also has the benefit of being able to modify the config from the host OS.
