# docker-coreos-toolbox-ubuntu

[CoreOS](https://coreos.com) is a minimal linux distribution with Docker as package manager. Because of this it lacks of tools like tmux. Fortunatelly you can use CoreOS toolbox to install any distribution and tools into a container. This way you can use your default distro under CoreOS. Toolbox uses systemd-nspawn to start container, but you don't need to bootstrap, because it uses Docker images as a base. More information: https://coreos.com/os/docs/latest/install-debugging-tools.html .

This is an Ubuntu Linux based toolbox for CoreOS. With this you can install any tool you found in Ubuntu's apt package manager. It is configured to be able to use the most important tools in the container and you see similar environment.

## Install

- Toolbox configuration on our kubectl instances is done via terraform by copying .toolboxrc file to /home/core directory. You can find latest .toolboxrc configuration here: https://github.com/circleci/infrastructure/blob/master/terraform/cci/modules/kubernetes-kubectl-v2/files/.toolboxrc

## Deploying new version

To deploy new version, after succesful build, ssh into relevant kubectl instance and run the following command which will remove currently cached version (replace 0.1 if necessary with the value of TOOLBOX_DOCKER_TAG used in .toolboxrc configuration):

```
sudo rm -rf /var/lib/toolbox/core-circleci_docker-coreos-toolbox-ubuntu-0.1
```

### How to use tmux on CoreOS

With this toolbox, you can just run:
```
toolbox tmux
```
If you detach it, it is running in the background, so you can reattach it again with:
```
toolbox tmux attach -t 0
```

## Features

- Full Ubuntu server, with all of its tools
- Similar environment as base CoreOS
- Using the core user as default with it's home directory mounted
- CoreOS root directory is mounted under /media/root
- CoreOS tools are usable: etcdctl, docker
- Apt package manager to install any deb packages
- tmux, Midnight Commander, etc.