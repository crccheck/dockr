dockr
=====

A [Docker CLI] wrapper for lazy people

  [Docker CLI]: https://docker.readthedocs.org/en/docs/commandline/cli/


Installation
------------

Put `dockerfile` somewhere in your path. I keep a `bin` directory in my home for
things like this.

```bash
mkdir -p ~/bin
cd ~/bin
wget https://raw.github.com/crccheck/dockr/master/dockr && chmod o+x dockr
```

TODO add a line exporting ~/bin to bash profile for reference. It will
probably look something like this:

```bash
echo -e "# added for dockr\nexport PATH=$PATH:$HOME/bin/ >> ~/.bashrc"
```

The Good Stuff
--------------
![](http://deadhomersociety.files.wordpress.com/2010/05/luckycharms.png)

### b

Build a tagged container imaged based on a *path*

```bash
$ dockr b redis/
```

You can also use relative paths, or leave it blank to use the current working
directory.

### bash

Log into a container/image

```bash
$ dockr bash ubuntu:precise
$ dockr bash c4f3
$ dockr bash -v ~/tmp/data:/mnt/data c4f3
```

If you pass in arguments, make sure the name is the last thing.

### clean

Delete all untagged containers

```bash
dockr clean
```

### images

List images, filtering out untagged images

```bash
docker images
```

### ip

Get the IP address of a running container

```bash
dockr ip c4f3
```

### stopall

Stop all running containers

```bash
dockr stopall
```

### (and the rest)

Anything else you try gets passed directly to `docker`
