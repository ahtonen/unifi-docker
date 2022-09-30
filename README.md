# Unifi-in-Balena

This repo is a fork of [Jacob Alberty's Unifi-in-Docker](https://github.com/jacobalberty/unifi-docker), but with modifications needed to make it deployable to a [Balena](https://www.balena.io) fleet's device.

## Motivation

I have played a lot with Ubiquity's excellent network hardware. Especially the Cloud Key, which
is running [Ubiqiti Network's](https://www.ubnt.com/) Unifi Controller, is a handy tool for
network management.

However, I didn't want to buy it, but found the Dockerized version that Jacob had nicely made
available. I could have simply run that on e.g. Raspberry Pi, in Docker Engine, but I wanted
more robustness and being able to access my Pi from anywhere in the World.

[Balena](https://www.balena.io) is a IoT fleet service in the cloud and provides free licence
up to 10 devices. It supports multitude of IoT devices and is build upon Docker technology.

## End result

Tuning Jacob's Dockerization suitable for Balena was a small trial-and-error project, but finally
these major changes made it a success:

- switch to run container as root (because of Balena)
- do not use initrd
- apply a bunch of Balena specific labels to enable needed features

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

## Using Unifi Controller

Once the application is deployed you should be able to access it from
a browser, restore the network config backup, and finally keep it running
in your IoT device, 24/7.