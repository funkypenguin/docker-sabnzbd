A fork of [linuxserver/sabnzbd](https://github.com/linuxserver/docker-sabnzbd) to include the mp4_automator package.

__Update__ : 30 May 2017 : for Radarr support in mp4_automator. See [here](https://www.funkypenguin.co.nz/note/docker-container-for-sabnzbd-with-sickbeard-mp4-automater-released/) for details

---

[linuxserverurl]: https://linuxserver.io
[forumurl]: https://forum.linuxserver.io
[ircurl]: https://www.linuxserver.io/irc/
[podcasturl]: https://www.linuxserver.io/podcast/

[![linuxserver.io](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/linuxserver_medium.png)][linuxserverurl]

The [LinuxServer.io][linuxserverurl] team brings you another container release featuring easy user mapping and community support. Find us for support at:
* [forum.linuxserver.io][forumurl]
* [IRC][ircurl] on freenode at `#linuxserver.io`
* [Podcast][podcasturl] covers everything to do with getting the most from your Linux Server plus a focus on all things Docker and containerisation!

# linuxserver/sabnzbd
[![](https://images.microbadger.com/badges/image/linuxserver/sabnzbd.svg)](http://microbadger.com/images/linuxserver/sabnzbd "Get your own image badge on microbadger.com")[![Docker Pulls](https://img.shields.io/docker/pulls/linuxserver/sabnzbd.svg)][hub][![Docker Stars](https://img.shields.io/docker/stars/linuxserver/sabnzbd.svg)][hub][![Build Status](http://jenkins.linuxserver.io:8080/buildStatus/icon?job=Dockers/LinuxServer.io-hub-built/linuxserver-sabnzbd)](http://jenkins.linuxserver.io:8080/job/Dockers/job/LinuxServer.io-hub-built/job/linuxserver-sabnzbd/)
[hub]: https://hub.docker.com/r/linuxserver/sabnzbd/

SABnzbd makes Usenet as simple and streamlined as possible by automating everything we can. All you have to do is add an .nzb. SABnzbd takes over from there, where it will be automatically downloaded, verified, repaired, extracted and filed away with zero human interaction.

[![sabnzbd](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/sabnzbd-banner.png)][saburl]
[saburl]: http://sabnzbd.org/

## Usage

```
docker create --name=sabnzbd \
-v <path to data>:/config \
-v <path to downloads>:/downloads \
-v <path to incomplete downloads>:/incomplete-downloads \
-e PGID=<gid> -e PUID=<uid> \
-e TZ=<timezone> \
-p 8080:8080 -p 9090:9090 \
linuxserver/sabnzbd
```

## Parameters

`The parameters are split into two halves, separated by a colon, the left hand side representing the host and the right the container side.
For example with a port -p external:internal - what this shows is the port mapping from internal to external of the container.
So -p 8080:80 would expose port 80 from inside the container to be accessible from the host's IP on port 8080
http://192.168.x.x:8080 would show you what's running INSIDE the container on port 80.`


* `-p 8080` - http port for the webui
* `-p 9090` - https port for the webui *see note below*
* `-v /config` - local path for sabnzbd config files
* `-v /downloads` local path for finished downloads
* `-v /incomplete-downloads` local path for incomplete-downloads - *optional*
* `-e PGID` for GroupID - see below for explanation
* `-e PUID` for UserID - see below for explanation
* `-e TZ` for setting timezone information, eg Europe/London

It is based on ubuntu xenial with s6 overlay, for shell access whilst the container is running do `docker exec -it sabnzbd /bin/bash`.

### User / Group Identifiers

Sometimes when using data volumes (`-v` flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user `PUID` and group `PGID`. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" ™.

In this instance `PUID=1001` and `PGID=1001`. To find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

## Setting up the application
Initial setup is done from the http port.
Https access for sabnzbd needs to be enabled in either the intial setup wizard or in the configure settings of the webui, be sure to use 9090 as port for https.
See here for info on some of the switch settings for sabnzbd http://wiki.sabnzbd.org/configure-switches


## Info

* Shell access whilst the container is running: `docker exec -it sabnzbd /bin/bash`
* To monitor the logs of the container in realtime: `docker logs -f sabnzbd`


## Versions

+ **15.09.16:** Compile par2 multicore as per latest info sabnzbd git [readme](https://github.com/sabnzbd/sabnzbd#resolving-dependencies)
+ **11.09.16:** Bump to release of 1.10
+ **09.09.16:** Rebase back to xenial,
issues with alpine version of python and 1.10 branch of sab.
+ **28.08.16:** Rebase to alpine, using git version of sab.
+ **17.03.16:** Bump to install 1.0 final at startup
+ **14.03.16:** Refresh image to pick up latest RC
+ **23.01.15:** Refresh image.
+ **14.12.15:** Refresh image to pick up latest beta
+ **21.08.15:** Intial Release.
