Podman is an Open Container Initiative compatible container runtime that provides functionality similar to [[Docker]] on the desktop. Podman was developed by Red Hat and provides more permissive utilities for running containers on virtual machines on Mac OS.

- https://0to1.nl/post/minikube-m1-pro-issues/
	- ```shell
	  brew install podman # install podman itself
	  podman machine init --cpus 2 --cpus=4 --memory=4096 -v $HOME:$HOME # download and init linux VM using qemu
	  podman machine start
	  
	  # add this to .bash_profile or .zshrc
	  export DOCKER_HOST=unix://`podman machine inspect --format '{{.ConnectionInfo.PodmanSocket.Path}}'`  
	  
	  brew install docker docker-compose
	  
	  
	  ```
- https://dhwaneetbhatt.com/blog/run-docker-without-docker-desktop-on-macos/
> To allow volume mounts on MacOS, podman machine needs to be created 
  with access to the folder from which you are going to attempt to mount 
  sub-folders, so it would have access to it.
  > Is likely that most MacOS users would only want to mount from within 
  their home directory, so machine should be created like below:
- https://stackoverflow.com/questions/70971713/mounting-volumes-between-host-macos-bigsur-and-podman-vm
