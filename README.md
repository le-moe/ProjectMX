# Presentation

This is a toy project to help me understand how to deploy a STM32 project using moderns tools and beeing cross-platform.
The first solution to work on STM32 is to use STM32CubeIDE. However this restrict the user by using a specific IDE to develop the firmware and many things are difficult to automate.
In this project I'm learning how to create makefile, integrate cmake and create docker file so virtually anyone can start contributing on the project rapidly.


### How to use docker

Docker solve the issue that your system may not be compatible with all the tools needed for compilation and flashing of the code to the micro-controller. The docker container provide all tools needed for this project and can be used on any platform with docker installed.

First build the docker images and give it the tag toolbox.
From docker-toolbox execute
```bash
docker build -t toolbox .
```

In order to enter the docker with a bash session you can use docker run like so:

```bash
docker run -it --entrypoint bash toolbox
```

For the moment gcc-arm-none-eabi is install in the docker, the tool is necessary to compile the project.
It is recommanded to add this alias to your ~/.bashrc or ~/.zshrc so you can call the docker tools from your terminal easier.

```
alias toolbox='docker run --env LINES=27 --env COLUMNS=128 -ti --rm --mount type=bind,source="$(pwd)",target=/mnt/bind-root toolbox'
```

To compile the project simply type this command from the root directory of the project.

```bash
toolbox make
```

These st-link tools are installed and available: st-flash, st-info, st-trace, st-util.
For example you can use this command to make sure everything is working:

```bash
toolbox st-flash --version
```
