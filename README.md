# Fork of [bdwinanto/sonarr_yt-dlp](https://github.com/bdwinanto/sonarr_yt-dlp) by [@bdwinanto](https://github.com/bdwinanto)
## Plan to keep this updated with latest yt-dlp (since yt downloads don't work with older versions) and experiment with sonarr integration


[brymck/sonarr_yt-dlp](https://github.com/brymck/sonarr_yt-dlp) is a [Sonarr](https://sonarr.tv/) companion script to allow the automatic downloading of web series normally not available for Sonarr to search for. Using [yt-dlp](https://github.com/yt-dlp/yt-dlp) it allows you to download your webseries from the list of [supported sites](https://github.com/yt-dlp/yt-dlp/blob/master/supportedsites.md).

## Features

* Downloading **Web Series** hosted on sites normally unavailable to Sonarr/not normally posted to usenet/torrent sites
* Ability to specify the downloaded video format globally or per series
* Downloads new episodes automatically once available
* Imports directly to Sonarr
* Allows setting time offsets to handle prerelease series
* Can pass cookies.txt to handle site logins

## How do I use it

Firstly you need a series that is available online in the supported sites that YouTube-DL can grab from.
Secondly you need to add this to Sonarr and monitor the episodes that you want.
Thirdly edit your config.yml accordingly so that this knows where your Sonarr is, which series you are after and where to grab it from.
Lastly be aware that this requires the TVDB to match exactly what the episodes titles are in the scan, generally this is ok but as its an openly editable site sometime there can be differences.

## Supported Architectures

The architectures supported by this image are:

| Architecture | Tag |
| :----: | --- |
| arm64 | latest |
| armhf | latest |
| amd64 | latest |

## Version Tags

| Tag | Description |
| :----: | --- |
| latest | Current release code |
| {yt-dlp release version} | Pre-release code for testing issues |

## Great how do I get started

Obviously its a docker image so you need docker, if you don't know what that is you need to look into that first.

### docker

```bash
docker create \
  --name=sonarr_yt-dlp \
  -v /path/to/data:/config \
  -v /path/to/sonarrmedia:/sonarr_root \
  -v /path/to/logs:/logs \
  --restart unless-stopped \
  bdwinanto/sonarr_yt-dlp:latest
```

### docker-compose

```yaml
---
version: '3.4'
services:
  sonarr_yt-dlp:
    image: bdwinanto/sonarr_yt-dlp:latest
    container_name: sonarr_yt-dlp
    volumes:
      - /path/to/data:/config
      - /path/to/sonarrmedia:/sonarr_root
      - /path/to/logs:/logs
```

### Docker volumes

| Parameter | Function |
| :----: | --- |
| `-v /config` | sonarr_yt-dlp configs |
| `-v /sonarr_root` | Root library location from Sonarr container |
| `-v /logs` | log location |

**Clarification on sonarr_root**

A couple of people are not sure what is meant by the sonarr root. As this downloads directly to where you media is stored I mean the root folder where sonarr will place the files. So in sonarr you have your files moving to `/mnt/sda1/media/tv/Smarter Every Day/` as an example, in sonarr you will see that it saves this series to `/tv/Smarter Every Day/` meaning the sonarr root is `/mnt/sda1/media/` as this is the root folder sonarr is working from.

## Configuration file

On first run the docker will create a template file in the config folder. Example [config.yml.template](./app/config.yml.template)

Copy the `config.yml.template` to a new file called `config.yml` and edit accordingly.



### Note

If you find yt-dlp able to download series but this docker is not able to, probably yt-dlp need to be updated to latest version. Please check yt-dlp=={version} in requirements.txt and update accordingly.
