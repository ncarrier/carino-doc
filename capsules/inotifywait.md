# inotifywait

## Why

**Inotify** is a linux kernel subsystem whose purpose is to provide userland
with some interesting events occurring on the file system. These range from file
modification to file removal. Events are handily provided via one or more file
descriptors and thus can be easily multiplexed in mono-threaded applications,
with pretty much all the other file descriptor types, like sockets for instance.

**inotifywait** is a small command line utility, allowing to use **inotify** in
shell scripts. The carino build system makes use of it for creating a
per-package list of the installed files, for the staging and for the final
directories.

## The problem

Travis-CI provides linux boxes powered by ubuntu 12.04 which is starting to turn
quite old. The **inotifywait** version packaged doesn't provide the --outfile
option, tools/build.sh relies upon.

## The solution

The solution I retained was to commit in the tools project a statically
precompiled binary of the **inotifywait** executable, which build.sh can
directly use. It is only a matter of several compilation lines to get a
functional one. Please keep in mind that this is just a handy hack, not a proper
guide for packaging it.

        # everyone should have a Trash directory, that's where all the serious
        # work occurs
        cd ~/Trash
        # clone the repository maintained by the debian project
        git clone git://anonscm.debian.org/git/collab-maint/inotify-tools.git/
        cd inotify-tools
        # retrieve the same revision as me, other can work too but aren't tested
        git checkout debian/3.14-1
        # dirty trick, run configure once to get some missing header files
        ./configure
        # remove duplicate function definitions
        sed -i 's/_niceassert/_stubbed_niceassert/g' src/common.c 
        sed -i 's/isdir/stubbed_isdir/g' src/common.c
        # do compile, all-in-one command
        gcc -static src/inotifywait.c  -I build/libinotifytools/src/.deps/ \
            -I build/src -I ./libinotifytools/src/ \
            -I ./build/libinotifytools/src/ -DHAVE_CONFIG_H \
            --std=c99 \
            src/common.c libinotifytools/src/inotifytools.c \
            libinotifytools/src/redblack.c \
            -o inotifywait
        # the inotifywait binary produced has the --outfile option
        ./inotifywait --help
