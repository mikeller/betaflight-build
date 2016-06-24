# Docker Betaflight build
[![Docker Pulls](https://img.shields.io/docker/pulls/mikeller/betaflight-build.svg)](https://hub.docker.com/r/betaflight-build/) [![Docker Stars](https://img.shields.io/docker/stars/betaflight-build.svg)](https://hub.docker.com/r/betaflight-build/) [![License](https://img.shields.io/badge/license-MIT-blue.svg?style=flat)](https://github.com/betaflight-build/blob/master/LICENSE)

Clone and edit [Betaflight](https://github.com/betaflight/betaflight) locally on your platform. This image will take it from there and turn your code into a binary which you then can flash to your flight controller with the [Betaflight Configurator](https://chrome.google.com/webstore/detail/betaflight-configurator/kdaghagfopacdngbohiknlhcocjccjao).

## Usage
### Install Docker
Follow the instructions at [https://docs.docker.com/](https://docs.docker.com/) → 'Get Started' (orange button top right).

### Clone the Betaflight repository
Docker runs on a VirtualBox VM which by default only shares the user directory from the underlying guest OS. On Windows that is `c:/Users/<user>` and on Mac it's `/Users/<user>`. Hence, you need to clone the  [Betaflight](https://github.com/betaflight/betaflight) repository to your *user directory*. If you want to place it outside the user directory you need to adjust the [VirtualBox VM sharing settings](http://stackoverflow.com/q/33934776/131929) accordingly.

`git clone https://github.com/betaflight/betaflight.git`

### Run this image with Docker
Start Docker and change to the NodeMCU firmware directory (in the Docker console). Then run:

``docker run --rm -ti -v `pwd`:/opt/betaflight mikeller/betaflight-build``

Depending on the performance of your system it takes 1-3min until the compilation finishes. The first time you run this it takes longer because Docker needs to download the image and create a container.

**Note for Windows users**

(Docker on) Windows handles paths slightly differently. You need to specify the full path to the Betaflight directory in the command and you need to add an extra forward slash (`/`) to the Windows path. The command thus becomes (`c` equals C drive i.e. `c:`):

`docker run --rm -it -v //c/Users/<user>/<betaflight>:/opt/betaflight mikeller/betaflight-build`

If the Windows path contains spaces it would have to be wrapped in quotes as usual on Windows.

`docker run --rm -it -v "//c/Users/joe blogs/<betaflight>":/opt/betaflight mikeller/betaflight-build`

#### Output
The firmware file (`.bin` or `.hex`) is created in the `obj` subfolder of your betaflight source directory.

#### Options
You can pass the following optional parameters to the Docker build like so `docker run -e "<parameter>=value" -e ...`. 

- `TARGET` The platform to build for. `NAZE` is default.

### Flashing the built binary
Use the [Betaflight Configurator](https://chrome.google.com/webstore/detail/betaflight-configurator/kdaghagfopacdngbohiknlhcocjccjao) Chrome app to flash and configure your firmware.

## Support
Don't leave comments on Docker Hub that are intended to be support requests. Firstly, Docker Hub doesn't notify me when you write them, secondly I can't properly reply. Instead create an issue on [GitHub](https://github.com/mikeller/docker-betaflight-build/issues).

## Credits
Thanks to [Marcel Stoer](http://frightanic.com/) for creating [docker-nodemcu-build](https://github.com/mikeller/docker-nodemcu-build), which I used as the template for this.

## Author
Michael Keller
