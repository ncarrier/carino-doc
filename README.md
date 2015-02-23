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

        # apt-get install curl git

2. Get repo from the [Android Open Source project][aosp-repo] :  

        $ mkdir -p ~/bin
        $ PATH=~/bin:$PATH
        $ curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
        $ chmod a+x ~/bin/repo

3. Create and initialize your workspace:  

        $ mkdir carino
        $ cd carino
        $ repo init -u https://github.com/ncarrier/carino-manifest

4. Get the source (and a cup of coffee):  

        $ repo sync

Repo will dowload for you, the whole carino project, that is all the code, the
build system, the documentation (from which this README is extracted), the
schematics, 3D resources modelling the mechanical parts, prototypes lego
plans...  
From now on, each command will assume the working directory to be that of your
carino workspace. ~/bin is assumed to be in your PATH environment too.

## Hack the code

1. Add the needed repositories you will need to add the following lines to your
   /etc/apt/sources.list file:

> \# cross compilation toolchain  
  deb http://www.emdebian.org/debian/ sid main  
  deb http://www.emdebian.org/debian/ wheezy main  
>  
> \# for adb  
  deb http://http.debian.net/debian wheezy-backports main  

2. Install the needed tool for building the software:

        # apt-get update
        # apt-get install colormake \
            sudo \
            kpartx \
            dosfstools \
            realpath \
            inotify-tools \
            ccache \
            dcfldd \
            u-boot-tools \
            android-tools-adb \
            pkg-config \
            gettext \
            emdebian-archive-keyring \
            binutils-arm-linux-gnueabihf \
            cpp-4.7-arm-linux-gnueabihf \
            g++-4.7-arm-linux-gnueabihf \
            gcc-4.7-arm-linux-gnueabihf \
            gcc-4.7-arm-linux-gnueabihf-base \
            gcc-4.7-base-armhf-cross \
            libc-bin-armhf-cross \
            libc-dev-bin-armhf-cross \
            libc6-armhf-cross \
            libc6-dev-armhf-cross \
            libgcc1-armhf-cross \
            libgomp1-armhf-cross \
            libstdc++6-4.7-dev-armhf-cross \
            libstdc++6-armhf-cross \
            linux-libc-dev-armhf-cross
        # useradd -G sudo USERNAME

3. Create the needed links, with standard names, to use the toolchain elements:

        $ ln -sf /usr/bin/arm-linux-gnueabihf-cpp-4.7 ~/bin/arm-linux-gnueabihf-cpp
        $ ln -sf /usr/bin/arm-linux-gnueabihf-g++-4.7 ~/bin/arm-linux-gnueabihf-g++
        $ ln -sf /usr/bin/arm-linux-gnueabihf-gcc-4.7 ~/bin/arm-linux-gnueabihf-gcc
        $ ln -sf /usr/bin/arm-linux-gnueabihf-gcc-ar-4.7 ~/bin/arm-linux-gnueabihf-gcc-ar
        $ ln -sf /usr/bin/arm-linux-gnueabihf-gcc-nm-4.7 ~/bin/arm-linux-gnueabihf-gcc-nm
        $ ln -sf /usr/bin/arm-linux-gnueabihf-gcc-ranlib-4.7 ~/bin/arm-linux-gnueabihf-gcc-ranlib
        $ ln -sf /usr/bin/arm-linux-gnueabihf-gcov-4.7 ~/bin/arm-linux-gnueabihf-gcov
        $ ln -sf $(realpath tools/arm-linux-gnueabihf-pkg-config) ~/bin/arm-linux-gnueabihf-pkg-config

4. Configure nice aliases and automatic completion:

        $ . tools/setenv

5. Do build (and find something funny to do in the meantime):

        $ bb

6. Once everything is built, you can generate the SD card image, your password
   will be asked since it requires root privileges :

        $ sd

7. Write the vewly created SD card image to your SD card. **_WARNING_**, erases
   all your SD card's data, assuming your SD card appears as /dev/sdc:

        # dcfldd if=out/carino.img of=/dev/sdc

Then you just have to insert your SD card in your pcduino nano 3, boot the card
and voilà ! Now you can hack the code and update it on target. More information
on the build system and the other useful commands, can be found in the
documentation for the
[carino-tools](https://github.com/ncarrier/carino-build_scripts) and the
[carino-build_scripts](https://github.com/ncarrier/carino-tools) projects. For
example, you'll be able to compile only one project and automatically update the
needed files on target, when it's running.

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
