# Harbour: An agent for containers

## What is Harbour
Harbour is a container node agent, which runs on the host machine, works as a proxy for containers to eliminate the differences of containers. For example, harbour takes over docker local socket and network port to provides services for clients.

## Try it out

### Build

Installation is simple as:

	go get github.com/huawei-openlab/harbour
	
## Usage

```
$  ./harbour
Usage: harbour [OPTIONS] [arg...]

Options:

  -D, --debug=false                          Enable debug mode
  -d, --daemon=false                         Enable daemon mode
  --docker-sock=/var/run/docker-real.sock    Path to docker sock file
  -G, --group=docker                         Group for the unix socket
  -H, --host=[]                              Daemon socket(s) to connect to
  -h, --help=false                           Print usage
  -v, --version=false                        Print version information and quit

Commands:

Run 'harbour COMMAND --help' for more information on a command.

```
### Default mode
Make sure docker located in PATH, run docker daemon, and do things as below:
- If binary used, run docker daemon with `-H unix:///var/run/docker-real.sock`
- If ubuntu lxc-docker used, open `/etc/default/docker`, add `-H unix:///var/run/docker-real.sock` in `DOCKER_OPTS`, save and restart docker.
- If systemd used to manage docker service, open the service file corresponding to docker, add `-H unix:///var/run/docker-real.sock`, save and `systemctl restart docker`.

Then run `harbour -d D` using root(Listen to `/var/run/docker.sock` and forward it to `/var/run/docker-real.sock` by default)

### User-defined mode
`harbour -d -D --docker-sock=/var/run/dockerxxx.sock`(specified sock for docker) `-H unix:///a/b/c.sock`(specified sock for harbour)  `-H tcp://:4567`(specified tcp port for harbour)

## Certificate of Origin
By contributing to this project you agree to the Developer Certificate of
Origin (DCO). This document was created by the Linux Kernel community and is a
simple statement that you, as a contributor, have the legal right to make the
contribution. 

```
Developer Certificate of Origin
Version 1.1

Copyright (C) 2004, 2006 The Linux Foundation and its contributors.
660 York Street, Suite 102,
San Francisco, CA 94110 USA

Everyone is permitted to copy and distribute verbatim copies of this
license document, but changing it is not allowed.

Developer's Certificate of Origin 1.1

By making a contribution to this project, I certify that:

(a) The contribution was created in whole or in part by me and I
    have the right to submit it under the open source license
    indicated in the file; or

(b) The contribution is based upon previous work that, to the best
    of my knowledge, is covered under an appropriate open source
    license and I have the right under that license to submit that
    work with modifications, whether created in whole or in part
    by me, under the same open source license (unless I am
    permitted to submit under a different license), as indicated
    in the file; or

(c) The contribution was provided directly to me by some other
    person who certified (a), (b) or (c) and I have not modified
    it.

(d) I understand and agree that this project and the contribution
    are public and that a record of the contribution (including all
    personal information I submit with it, including my sign-off) is
    maintained indefinitely and may be redistributed consistent with
    this project or the open source license(s) involved.
```

## Format of the Commit Message

You just add a line to every git commit message, like this:

    Signed-off-by: Meaglith Ma <maquanyi@huawei.com>

Use your real name (sorry, no pseudonyms or anonymous contributions.)

If you set your `user.name` and `user.email` git configs, you can sign your
commit automatically with `git commit -s`.
