# Unifi-in-Balena

This repo is a fork of [Jacob Alberty's Unifi-in-Docker](https://github.com/jacobalberty/unifi-docker), but with modifications needed to make it deployable to a [Balena fleet](https://www.balena.io).

## Motivation

I have played a lot with Ubiquity's excellent network hardware. Especially the Cloud Key, which
is running [Ubiquiti Network's](https://www.ubnt.com/) Unifi Controller, is a handy tool for
network management.

However, I didn't want to buy it, but found a Dockerized version of its software that Jacob had nicely made available. I could have simply run that on e.g. Raspberry Pi, in Docker Engine, but I wanted more robustness and being able to access my Pi anywhere in the World.

[Balena](https://www.balena.io) is an IoT fleet service in the cloud and provides free license
for up to 10 devices. It supports multitude of diffrent IoT boards and is build upon the Docker technology.

## End result

Tuning Jacob's Dockerization suitable for Balena was a small trial-and-error project, but finally
these major changes made it a success:

- switch to run container as root since Balena only supports that
- apply a bunch of Balena specific labels to enable needed features
- avoid using initrd

## Building instructions

In Balena cloud you need to setup first a fleet with at least one
device for the application. Of course you need to install command line tools,
login, etc. A good place to start is [Balena's Getting Started](https://www.balena.io/docs/learn/getting-started/).


After that you can use Balena's Cloud build
for deploying the application. For example, if your organization
name is `myorg` and fleet's name `unifi`, in the project directory say:

```
balena push myorg/unifi
```

Alternatively you can try to deploy by clicking this button:

[![deploy button](https://balena.io/deploy.svg)](https://dashboard.balena-cloud.com/deploy?repoUrl=https://github.com/ahtonen/unifi-docker&defaultDeviceType=raspberry-pi)

## Using Unifi Controller

Once the application is deployed you should be able to access it from
a browser, restore the network config backup, and finally keep it running
in your IoT device, 24/7.
