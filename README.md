# Vagrantized development environment (based on Ubuntu)

1-2-3 instructions:

1) Setup
2) Start
3) Use and modify based on your personal needs

## Purpose

To have virtualized "basic ubuntu development box", which can be used as a starting point for learning new techs or building development environments.

The goal is really not to include everything you might ever need, as this is your work to do, but just to set the basics and help you quickstart developing.

It creates virtualized development environment, which uses ubuntu. It shares folder between host and guest, creates port forwarding, installs Git, node and npm and makes sure OS is up-to-date.

Based on this article: https://medium.com/@JohnFoderaro/how-to-set-up-a-local-linux-environment-with-vagrant-163f0ba4da77

## How to setup

1) [Setup Vagrant prerequisities](https://www.vagrantup.com/docs/installation/)
2) Clone this repository
3) Modify `Vagrantfile` and follow instructions written in it

[More help with Vagrantfile](https://www.vagrantup.com/docs/vagrantfile/)

## How to start

`vagrant up`

[More help with vagrant basic commands](https://www.vagrantup.com/docs/cli/)

## How to use

Okay, now you have new shiny Vagrant environment. How to use it?

1) When you modify source code, it is wiser to use your own computer instead of modifying it inside vagrant box. That is because you probably have your favourite editors already set-up on your own computer and Vagrant environment doesn't have them. Also your own computer's I/O is faster. Fear not, Vagrant syncs the folder so your changes are instantly shown inside Vagrant.

2) Everything else happens inside Vagrant box.

```
vagrant ssh
cd ~/<name-of-your-project>
```
and you are ready to do your magic.

## But wait, this box doesn't have Typescript/React/Angular/etc installed? What to do

This is your work. You have now clean and empty development env with the bare basic setup. To make it work with your unique needs, just follow the your-technology-here instructions.

You can either do everything inside the vagrant box or if you want to share this environment with other developers, then it is wiser to setup things in provision part of the Vagrantfile.

[More help with provision](https://www.vagrantup.com/docs/cli/provision.html)

# Examples how to setup different environments

## Typescript

1) `vagrant up`
2) `vagrant ssh`
3) [Continue from Typescript instructions](https://www.typescriptlang.org/index.html)

## React with create-react-app

1) `vagrant up`
2) `vagrant ssh`
3) [Continue from create-react-app instructions](https://github.com/facebookincubator/create-react-app) and [React instructions](https://facebook.github.io/react/docs/hello-world.html)

Notices:
- Uses yarn instead of npm
- Instead of localhost:3000 use the port you set in Vagrantfile
- To enable live reloading, which means that the browser reloads when you modify source files, go to your react application folder (if you used create-react-app myapp, then go to folder myapp) and create `.env` file with content `CHOKIDAR_USEPOLLING=true`, save it and restart the react environment

# Known issues

## Has been tested to work with at least following versions

Host:
- Mac OS X El Capitan
- Vagrant 1.7.4
- VirtualBox 5.0.10

Guest:
- Nodejs 6.10.2
- npm 4.5.0
- yarn 0.23.2

## Not fixed

N/A

## Not fixed, but there is a workaround

N/A

## Fixed in a way that you don't have to worry about it

### npm global package folder permissions in vagrant

Problem: npm global package installation fails with permission issues
Solution: [Option 2 in these instructions](https://docs.npmjs.com/getting-started/fixing-npm-permissions)
Fixed: In a Vagrantfile, so you don't have to worry about it

### create-react-app installation or start fails with error coming from random npm packages

Problem: create-react-app fails to install because ENOENT error coming from random package. If run multiple times, it might eventually install. However it won't start, as another error is thrown from one of the packages
Solution: npm 4.5.0 seems to be buggy. Installed yarn
Fixed: In a Vagrantfile, so you don't have to worry about it
