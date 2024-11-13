# Section 3 - Building Images

## Images and Containers

Image - an image is a file that contains everything an application needs to run. Example: OS, third-party libraries, application files, environment variables and so on.

Container - is like a virtual machine that provides an isolated environment for executing an application. Can be stopped and restarted,
Is just a process.

## Sample Web Application

Having the react app inside this section, we have a react application. Without using docker, if we wanted to setup the react app, we should have to do these steps:

- Install node in our machine
- run `npm install` to install the application dependencies and third party libraries
- run `npm start` to start the project

## Docker file tips

1- FROM: Sets the base image for the Docker image, defining the starting point (e.g., FROM ubuntu:latest).

2- WORKDIR: Sets the working directory within the container where commands will be run (e.g., WORKDIR /app).

3- COPY: Copies files or directories from the host system to the container (e.g., COPY . /app).

4- ADD: Similar to COPY but with additional features like automatically extracting archives and supporting URLs.

5- RUN: Executes a command in the container at build time, typically used for installing dependencies (e.g., RUN apt-get update).

6- ENV: Sets environment variables in the container (e.g., ENV NODE_ENV production).

7- EXPOSE: Informs Docker that the container listens on a specific port, useful for networking (e.g., EXPOSE 8080).

8- USER: Specifies the user under which the container’s commands should be run, enhancing security (e.g., USER node).

9- CMD: Sets the default command to run when the container starts, but it can be overridden (e.g., CMD ["npm", "start"]).

10- ENTRYPOINT: Defines a command that will always run as the container’s entry point, often combined with CMD for additional arguments (e.g., ENTRYPOINT ["python", "script.py"]).

## Choosing the right base image

alpine version - this version is a very lightweight image, so it's size is smaller compared to the regular image.

To build an image, we can do something like this in the cmd: `docker build -t react-app .`. `-t` is to tag the image and `.` is where docker can find a docker file, in this case is in the current directory

NOTE: We can run `docker image ls` to check all of the images we have.

To run a docker image we can run this command: `docker run -it image_name`. The `-it` is for the interactive mode, we do not need to use it, but if we use it it let's us use the environment as we want.

For the alpine version, the bash is not installed in the image, because it's a really small image of linux. So we can use shell instead, like this: `docker run -it image_name sh`

## Copying files and directories

When we build the docker image, in the command we specify the path to the application directory. For this, docker send this to the docker engine, where the path that wee specified being passed to the image so it can use it in the COPY command, for example. This is the build context.

O docker file won't have access to anything outside the directory that we passed to it.

NOTE: If we update a docker image file, we need to build it again.
