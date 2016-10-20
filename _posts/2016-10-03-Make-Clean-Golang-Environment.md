---
layout: post
title: "Make Clean Golang Environment"
---

While working with Golang sometime I found the need to make a new GOPATH
that did not have all the binaries and files to test a build for a project.

This seem to be a quick and easy way to create a new GOPATH and set a 
new GOBIN as well.

# Operations

``` bash
export MYGODIR=goofygo
cd ~
export GOPATH=$HOME/$MYGODIR
export GOBIN=$GOPATH/bin
export PATH=$HOME/bin:$HOME/bin:/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games:/usr/local/go/bin:$GOBIN
rm -rf $GOPATH
```
