## How to deploy Flutter app with Docker?

# First of all, what is Docker?

Docker takes away repetitive, mundane configuration tasks and is used throughout the development lifecycle for fast, easy and portable application development - desktop and cloud. Docker’s comprehensive end to end platform includes UIs, CLIs, APIs and security that are engineered to work together across the entire application delivery lifecycle.

# Why are we deploying a Flutter web app with Docker?

Well, docker is like OS Virtualization which makes it easier for installing modules and if you ever get stuck, docker helps you by creating a new container with your required settings. 

Flutter requires different types of heavy package management which makes it complex for updating and deploying the app in the first step especially when you are ought to testing the app in a production cloned environment.

# Getting started

We will begin the process by creating a fresh `Dockerfile`, with your required settings. A sample `Dockerfile` is given below:

```dockerfile
FROM ubuntu:20.10 as builder
RUN apt update && apt install -y curl git unzip xz-utils zip libglu1-mesa openjdk-8-jdk wget
RUN useradd -ms /bin/bash user
USER user
WORKDIR /home/user

#Installing Android SDK
RUN mkdir -p Android/sdk
ENV ANDROID_SDK_ROOT /home/user/Android/sdk
RUN mkdir -p .android && touch .android/repositories.cfg
RUN wget -O sdk-tools.zip https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip
RUN unzip sdk-tools.zip && rm sdk-tools.zip
RUN mv tools Android/sdk/tools
RUN cd Android/sdk/tools/bin && yes | ./sdkmanager --licenses
RUN cd Android/sdk/tools/bin && ./sdkmanager "build-tools;29.0.2" "patcher;v4" "platform-tools" "platforms;android-29" "sources;android-29"
ENV PATH "$PATH:/home/user/Android/sdk/platform-tools"

#Installing Flutter SDK
RUN git clone https://github.com/flutter/flutter.git
ENV PATH "$PATH:/home/user/flutter/bin"
RUN flutter channel dev
RUN flutter upgrade
RUN flutter doctor
```

***Note: Please change it as your needs as we have taken latest ubuntu images, you should always use your OS specified image for Docker containers to prevent unwanted errors***

## Building the base image

To build this base image, make sure you are in the same directory as the `Dockerfile`,
We'll build the base image by:
```sh
$ docker build -t {anyNameHere}
```
You can replace `{anyNameHere}` with your required name like `dockerflutter`.

Now this was the base for how to build a docker image, now we will look onto further development and deployment:

### Building with a Git repository

Now, go ahead and push your changes to a git repository and make sure you add SSH keys in the repository settings so that we can pull the repo without conflicts.

After pushing the changes, we will slightly edit the `Dockerfile` by adding these lines at the end:
```Dockerfile
RUN git clone {gitRepo}
RUN cd {repoFolder} && flutter test
```
Replace `{gitRepo}` with your Flutter github repository and `{repoFolder}` with the folder your git repository was cloned, by default it's the name of the git repository.

## Running the app

Now we will run the flutter image by:
```sh
$ docker run -d {yourDockerImage}
```
Replace `{yourDockerImage}` with the image you built.
Here, flag `-d` refers to the *Detached Mode* which is optional when you don't want to get stuck inside the container.

Thank you! 👋