# Vagrantized development environment (based on Ubuntu)

1-2-3 instructions:

1) Setup
2) Start
3) Use and modify based on your personal needs

## Purpose

"Okay, today I will start learning/develop with Typescript/React/Angular/etc.", you said, googled for installation instructions and then installed a bunch of stuff to your computer. Probably something fails, as it often does, so you install something more to fix that.

That is okay if you are planning to use this tech for good for ages. But when you just want to test something out or compare different techs, it might be intimidating to install everything to your own computer.

The purpose of this project is to give you:
- Instructions how to set up generic virtualized development environment, which is good starting point for almost any tech which runs on Ubuntu Linux
- Pre-made Vagrantfile, which automatically sets your development environment...
- And fixes the most common errors you will face when using virtual environments
- You can have as many virtual environments you like, for example, one per tech you are trying out. Also if you manage to create horrible mess, just nuke the environment and create new one to start again

The goal is not to instruct "how to install tech x", but just tell whether it has been tested out to work with this environment and then link to tech's own instructions. Also, the goal is not to pre-install everything, but just the basics you need.

Based on this article: https://medium.com/@JohnFoderaro/how-to-set-up-a-local-linux-environment-with-vagrant-163f0ba4da77

## How to setup

1) [Setup Vagrant prerequisities](https://www.vagrantup.com/docs/installation/)
2) Clone this repository
3) Modify `Vagrantfile` and follow instructions written in it

How to understand Vagrantfile?
- [More help with Vagrantfile](https://www.vagrantup.com/docs/vagrantfile/)

## How to start using your new development environment

```
vagrant up
vagrant ssh
cd ~/<name-of-your-project>
```

Notice: vagrant up takes some time when you run it the first time. It also does lots of downloading, so make sure you are on wifi.

How to start or stop development environment? How to destroy or recreate?
- [More help with vagrant basic commands](https://www.vagrantup.com/docs/cli/)

and you are ready to do your magic.

## But wait, this environment doesn't have Typescript/React/Angular/etc installed? What to do

This is your work. You have now clean and empty development environment with the bare basic setup. To make it work with your unique needs, just follow the your-technology-here instructions.

You can either do everything inside the vagrant box or if you want to share this environment with other developers, then it is wiser to set up things in provision part of the Vagrantfile.

What is pre-installed to development environment when I run vagrant up the first time?
- [More help with provision](https://www.vagrantup.com/docs/cli/provision.html)

## Okay, what now?

Okay, now you have the new shiny virtual development environment made using Vagrant. How to use it?

1) Use it as you would use any environment. Follow your tech choice's instructions for setup and usage. Do everything inside the virtual environment, except...

2) Modify source code and use a browser from your own computer, not inside the virtual environment. Why? Because virtual environment doesn't have mega-awesome browsers and IDEs installed. The virtual environment is automatically setup to both share project folder between your computer (host) and the virtual environment (guest) and forward ports between host and guest so you can use a browser on your own computer.

How to sync files between your computer and development environment?
- [More help with synced folders](https://www.vagrantup.com/docs/synced-folders/)

How to access development environment via browser?
- [More help with port forwarding](https://www.vagrantup.com/docs/networking/forwarded_ports.html)
- [More help with dhcp](https://www.vagrantup.com/docs/networking/private_network.html)

# Proven examples how to setup different environments

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

## Other technologies

Please try it out and let me know if you found any problems that need fixing.

# Known issues

## Has been tested to work with at least following versions

Host:
- Mac OS X El Capitan
- Vagrant 1.7.4
- VirtualBox 5.0.10

Guest:
- Ubuntu 14.04.5 LTS
- Nodejs 6.10.2 LTS
- npm 4.5.0
- yarn 0.23.2

## Not fixed

N/A

## Not fixed, but there is a workaround

N/A

## Fixed in a way that you don't have to worry about it

npm global package folder permissions in vagrant
- Problem: npm global package installation fails with permission issues
- Solution: [Option 2 in these instructions](https://docs.npmjs.com/getting-started/fixing-npm-permissions)
- Fixed: In a Vagrantfile, so you don't have to worry about it

create-react-app installation or start fails with error coming from random npm packages
- Problem: create-react-app fails to install because ENOENT error coming from a random package. If run multiple times, it might eventually install. However, it won't start, as another error is thrown from one of the packages
- Solution: npm 4.5.0 seems to be buggy. Installed yarn. create-react-app automatically uses yarn if it is installed.
- Fixed: In a Vagrantfile, so you don't have to worry about it
