[linuxserverurl]: https://linuxserver.io
[forumurl]: https://forum.linuxserver.io
[ircurl]: https://www.linuxserver.io/irc/
[podcasturl]: https://www.linuxserver.io/podcast/
[appurl]: https://couchpota.to/
[hub]: https://hub.docker.com/r/lsioarmhf/couchpotato-aarch64/

THIS IMAGE IS DEPRECATED. PLEASE USE THE MULTI-ARCH IMAGES AT `linuxserver/couchpotato`

[![linuxserver.io](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/linuxserver_medium.png)][linuxserverurl]

The [LinuxServer.io][linuxserverurl] team brings you another container release featuring easy user mapping and community support. Find us for support at:
* [forum.linuxserver.io][forumurl]
* [IRC][ircurl] on freenode at `#linuxserver.io`
* [Podcast][podcasturl] covers everything to do with getting the most from your Linux Server plus a focus on all things Docker and containerisation!

# lsioarmhf/couchpotato-aarch64
[![](https://images.microbadger.com/badges/version/lsioarmhf/couchpotato-aarch64.svg)](https://microbadger.com/images/lsioarmhf/couchpotato-aarch64 "Get your own version badge on microbadger.com")[![](https://images.microbadger.com/badges/image/lsioarmhf/couchpotato-aarch64.svg)](http://microbadger.com/images/lsioarmhf/couchpotato-aarch64 "Get your own image badge on microbadger.com")[![Docker Pulls](https://img.shields.io/docker/pulls/lsioarmhf/couchpotato-aarch64.svg)][hub][![Docker Stars](https://img.shields.io/docker/stars/lsioarmhf/couchpotato-aarch64.svg)][hub][![Build Status](https://ci.linuxserver.io/buildStatus/icon?job=Docker-Builders/arm64/arm64-couchpotato)](https://ci.linuxserver.io/job/Docker-Builders/job/arm64/job/arm64-couchpotato/)

[CouchPotato](https://couchpota.to) is an automatic NZB and torrent downloader. You can keep a "movies I want" list and it will search for NZBs/torrents of these movies every X hours. Once a movie is found, it will send it to SABnzbd or download the torrent to a specified directory.

[![couchpotato](https://couchpota.to/media/images/full.png)][appurl]

## Usage

```
docker create \
	--name=couchpotato \
	-v <path to data>:/config \
	-v <path to data>:/downloads \
	-v <path to data>:/movies \
	-e PGID=<gid> -e PUID=<uid>  \
	-e TZ=<timezone> \
	-e UMASK_SET=<022> \
	-p 5050:5050 \
	lsioarmhf/couchpotato-aarch64
```

## Parameters

`The parameters are split into two halves, separated by a colon, the left hand side representing the host and the right the container side. 
For example with a port -p external:internal - what this shows is the port mapping from internal to external of the container.
So -p 8080:80 would expose port 80 from inside the container to be accessible from the host's IP on port 8080
http://192.168.x.x:8080 would show you what's running INSIDE the container on port 80.`


* `-p 5050` - the port(s)
* `-v /config` - Couchpotato Application Data
* `-v /downloads` - Downloads Folder
* `-v /movies` - Movie Share
* `-e PGID` for for GroupID - see below for explanation
* `-e PUID` for for UserID - see below for explanation
* `-e UMASK_SET` for umask setting of couchpotato, *optional* , default if left unset is 022.
* `-e TZ` for timezone information, eg Europe/London

It is based on alpine-linux with S6 overlay, for shell access whilst the container is running do `docker exec -it couchpotato /bin/bash`.

### User / Group Identifiers

Sometimes when using data volumes (`-v` flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user `PUID` and group `PGID`. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" ™.

In this instance `PUID=1001` and `PGID=1001`. To find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

## Info
`IMPORTANT... THIS IS THE ARM64 VERSION`

* To monitor the logs of the container in realtime `docker logs -f couchpotato`.

* container version number 

`docker inspect -f '{{ index .Config.Labels "build_version" }}' couchpotato`

* image version number

`docker inspect -f '{{ index .Config.Labels "build_version" }}' lsioarmhf/couchpotato-aarch64`

## Versions

+ **14.01.19:** This image is deprecated. Please use the multi-arch images at linuxserver/couchpotato
+ **16.08.18:** Bump to alpine 3.8.
+ **10.01.18:** Bump to alpine 3.7.
+ **20.07.17:** Internal git pull instead of at runtime, add UMASK_SET variable.
+ **30.05.17:** Bump to alpine 3.6.
+ **10.12.16:** Initial Release.
