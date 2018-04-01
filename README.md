# OpenBW_IDE
Dockerized Integrated Development Environment for OpenBW


## Prerequisites

The following setup is assumed:

 - docker installed
 
 Optionally:
 
 - linux host OS
 
 
 Note: the linux host OS is not required, since docker also runs on other operating systems. However, the IDE has been tested on Ubuntu only.
 
 
## Installation

build the docker image by entering the following command in your console:

`docker build openbw -t openbw:0.9`

that's it!

For your reference, this automatically installs a gcc 6 compiler with cmake as well as SDL2 in your docker image.
It then uses those tools to download and compile OpenBW.
Finally, it downloads and unzips the required files to run OpenBW from an external repository.

## Running OpenBW

### without graphic output

type the following command in your console to access the docker console:

`docker run -ti openbw:0.9 /bin/bash`

you are now inside the docker container.
navigate to the bin directory, where OpenBW is compiled:

`cd /home/bwapi/build/bin`

run the following command to start an OpenBW instance:

`./BWAPILauncher`

Note: This will use the example bwapi.ini as provided in the OpenBW repository to launch the BWAPI test module.

You should see the following output in the console:

```
Loaded the AI Module: ../lib/TestAIModule.so

bwapi: BWAPI 4.2.0.0 RELEASE is now live using "TestAIModule.so".

bwapi: Enabled Flag CompleteMapInformation

bwapi: Enabled Flag UserInput

A Resource_Mineral_Field [0x7f185019ae60] has been created
```

### with graphic output

Docker is able to route graphical output to the host via X11. In order to do so we must map the X-Server socket and expose the $DISPLAY environment variable to docker. Just use the following command insteaad of the one given above:

`docker run -ti -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY openbw:0.9 /bin/bash`

Troubleshooting:
For the above command to work docker must be able to access the X-Server.
This can be achieved by executing the following command in the console:
`xhost +local:docker`

Check if X11 Forwarding is enabled in /etc/ssh/ssh_config:
`grep X /etc/ssh/sshd_config`
should return `ForwardX11 yes`

