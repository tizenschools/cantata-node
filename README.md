Evented I/O for V8 javascript.
===

This is a guide how to compile node.js (v0.8.16-release) for arm architecture and create the node executable to be able to be linked dynamically.

### Prerequisites (Unix only):

    * Python 2.6 or 2.7
    * GNU Make 3.81 or newer
    * libexecinfo (FreeBSD and OpenBSD only)

### Build using build script (Ubuntu only):
   
    $ mkdir output
    $ ./build --dest-cpu=arm --with-pie --prefix=./output
    $ file ./output/node
    out/Release/node: ELF 32-bit LSB shared object, Intel 80386, version 1 (SYSV), dynamically linked 
    (uses shared libs), for GNU/Linux 2.6.15, not stripped

### Build own your own:

Get node Source code:

    $ git clone git://github.com/joyent/node.git
    $ cd node
    $ git checkout v0.8.16-release

Set some envirnments for cross compile:

    $ export AR=arm-linux-gnueabi-ar
    $ export CC=arm-linux-gnueabi-gcc
    $ export CXX=arm-linux-gnueabi-g++
    $ export LINK=arm-linux-gnueabi-g++

Set patch for making node pie executable

    $ patch -p0 < ../patch-for-making-pie-executable.patch

Build node

    $ ./configure --without-snapshot --dest-cpu=arm --dest-os=linux
    $ make --jobs=8

Resources for Newcomers
---
  - [n8.io] (http://n8.io/cross-compiling-nodejs-v0.8/)
  - [The Wiki](https://github.com/joyent/node/wiki)
  - [nodejs.org](http://nodejs.org/)
  - [how to install node.js and npm (node package manager)](http://joyeur.com/2010/12/10/installing-node-and-npm/)
  - [list of modules](https://github.com/joyent/node/wiki/modules)
  - [searching the npm registry](http://search.npmjs.org/)
  - [list of companies and projects using node](https://github.com/joyent/node/wiki/Projects,-Applications,-and-Companies-Using-Node)
  - [node.js mailing list](http://groups.google.com/group/nodejs)
  - irc chatroom, [#node.js on freenode.net](http://webchat.freenode.net?channels=node.js&uio=d4)
  - [community](https://github.com/joyent/node/wiki/Community)
  - [contributing](https://github.com/joyent/node/wiki/Contributing)
  - [big list of all the helpful wiki pages](https://github.com/joyent/node/wiki/_pages)
