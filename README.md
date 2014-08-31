dockr
=====

A [Docker CLI] wrapper for lazy people

  [Docker CLI]: https://docker.readthedocs.org/en/docs/commandline/cli/


Installation
------------

Put `dockr` somewhere in your path. I keep a `bin` directory in my home for
things like this.

```bash
mkdir -p ~/bin
cd ~/bin
wget https://raw.github.com/crccheck/dockr/master/dockr && chmod u+x dockr
```

TODO add a line exporting ~/bin to bash profile for reference. It will
probably look something like this:

```bash
echo -e "# added for dockr\nexport PATH=$PATH:$HOME/bin/ >> ~/.bashrc"
```

The Good Stuff
--------------
![](http://deadhomersociety.files.wordpress.com/2010/05/luckycharms.png)

The commands I use the most are: `dockr b` - which builds an imaged and names
it according to the directory, and `docker bash` - which lets me shell in
quickly.

Many of these commands were written for older versions of the docker cli. They
have since done a better job of cleaning up intermediate containers and getting
meta out.


Full Reference
--------------

### b

Build a tagged container image based on a *path*.

To build an image called `redis` where the Dockerfile is located at ./redis:

```bash
dockr b redis/
```

You can also use relative paths, or leave it blank to use the current working
directory. It also always tries to namespace the image. By default, it will use
your username (your username has to be more then 3 characters long), but you
can override it with a `DOCKER_NAMESPACE` environment variable:

```bash
$ pwd
/home/crccheck/dockerfiles/redis
dockr b
# ... stuff happens
dockr images
# crccheck/redis appears
# OOPS, that docker image was supposed to be under another namespace
export DOCKER_NAMESPACE=lollipop
dockr b
# ... stuff happens
dockr images
# lolliop/redis appears
```

*Alternative to: `docker build -t redis redis/`*

### bash

Log into a container/image

```bash
dockr bash ubuntu:precise
dockr bash c4f3
dockr bash -v ~/tmp/data:/mnt/data c4f3
```

If you pass in arguments, make sure the name is the last thing.

*Alternative to: `docker run -i -t -v ~/tmp/data:/mnt/data c4f3 /bin/bash`*

### clean

Delete all untagged containers

```bash
dockr clean
```

*Alternative to: `docker rm $(some grep magic)`*

### cleani

Delete all untagged images

```bash
dockr cleani
```

*Alternative to: `docker rmi $(some grep magic)`*

### images

List images, filtering out untagged images

```bash
docker images
```

*Alternative to: `docker images | grep blahblahblah`*

### ip

Get the IP address of a running container

```bash
dockr ip c4f3
```

*Alternative to: `docker inspect c4f3 | python -c 'import antigravity'`*

### oops

Delete the most recent container

### smite

Stop and remove a running container

```bash
dockr smite 5029fc
```

### stopall

Stop all running containers

```bash
dockr stopall
```

*Alternative to: `docker stop $(docker ps -q)`*

### (and the rest)

Anything else you try gets passed directly to `docker`
