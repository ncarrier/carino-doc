# The carino project documentation

Carino is a platform for building vehicles, remotely controlled via wifi.  

## Goals

* provide completely finished products, with an industry level quality
* be an educative platform, with a documentation on how to build and hack a
  vehicle from the ground up, with various levels of reading so that the target
  audience can be as large as possible
* tend to be as open as possible, from the the software to the hardware (but
  see note 1.)
* bring tons of fun to everyone, starting with me :)

## Prerequisites

This README assumes you have an up to date [Debian][debian] Wheezy distribution
installed. Procedures for others debian-based distributions should be fairly
similar.  
Some work should be necessary to adapt for other linux distributions or unix
flavors.  
On other exotic platforms, like windows, the best option should be to set up a
virtual machine running Debian, VirtualBox can be used for this purpose and is
free as in free speech and free beer. Please note that compilation times will
increase, in that case.

## Get the code and all the resource

The carino project uses repo from google, for gathering the different
sub-projects it is made of:

1. Be sure to have the needed tools:  
   `# apt-get install curl git`
2. Get repo from the [Android Open Source project][aosp-repo] :  
   `$ mkdir -p ~/bin`  
   `$ PATH=~/bin:$PATH`  
   `$ curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo`  
   `$ chmod a+x ~/bin/repo`
3. Create and initialize your workspace:  
   `$ mkdir carino`  
   `$ cd carino`  
   `$ repo init -u https://github.com/ncarrier/carino-manifest`
4. Get the source (and a cup of coffee):  
   `$ repo sync`

Repo will dowload for you, the whole carino project, that is all the code, the
build system, the documentation (from which this README is extracted), the
schematics, 3D resources modelling the mechanical parts, prototypes lego
plans...  
From now on, each command will assume the working directory to be that of your
carino workspace.

## Hack the code

TODO explain how to get the tools and explain basically the build process

## Hack the schematics

TODO schematics are not ready yet, this section will be completed soon

## Hack the hardware

TODO hardware plans are not ready yet, this section will be completed soon

Notes:
1. all the ressources produced will come with an open licence, mainly (L)GPL for
source code, creative commons BY SA for documentation, "artistic" and other
material. For external bits used (e.g. hardware), an effort will be made to use
the most open solutions possible, but while keeping some pragmatism. For
example, if the pcduino3 platform will prove to fit our needs and / or be the
cheapest solution available, we will stick to it even if it's not the most open
platform. If a realist candidate for replacement emerges, we will evaluate the
possibility of changing.


[aosp-repo]: https://source.android.com/source/downloading.html#installing-repo
[debian]: https://www.debian.org/
