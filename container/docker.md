## Container can be considered as virtual "develop" environment where all necessay system set-up is equipped

## Image is packaged container that can be share to others, one can establish a container based on the image
### It's better install docker engin on linux
* permission denied:
```
sudo groupadd -f docker
sudo usermod -aG docker $USER
newgrp docker
groups
```

* **Load** a existing images, use:
 command `load IMAGE_NAME` differ from the command `import IMAGE_NAME`
* **Check** the imported/loaded images:
 command `docker images`
* **Run** the loaded image:
command `docker run ...` (to be completed)
e.g:
`docker run -ti -v MOUNTED_DIRECTORY:/MOUNTED_POINT:rw IMAGE_NAME /bin/bash`
* **Run** a image with mounting a path/repository (folder), the folder should be extract wiht same ownership and groupe as it is:
 command `tar -same-owner -xvf TAR_NAME.tar.gz`
* Check existing container:
command `docker ps -option`
without option, showing the running container
option `-a` showing all the containers
* start a existing container:
  command `start CONTAINER_NAME`
* Run existing container:
  `docker attach/exec -option CONTAINER_NAME`
  ** if you want to run the same container within another terminal use:
  `docker exec -ti CONTAINER_ID bash`

## Common building container environment variable
* update container:

`export DOCKER_IMAGE=XXX:XXX`

`alias update_ext_container='docker stop $CONTAINER_NAME; docker container rm $BRANCH_NAME; docker login -u pull-token -p TOKEN_NUMBER && docker pull $DOCKER_IMAGE && docker container create $USER:grp -v "REPO_PATH" -v "BUILD_PATH" --name "$Build_name" -it $DOCKER_IMAGE`

remark: command `it`: interactive STDIN and attach a pseudo TTY (terminaml)
* buidling from scratch in container:

`alias regen='docker start $CONTAINER_NAME && docker exec -i -t $CONTAINER_NAME bash -c "source ~/.bashrc && XXXbashrc command to build`

remark: start a new bash session in which we go to build repo and build product line
* open docker and attach a bash session:

`alias docker_swu=docker start $CONTAINER_NAME && docker exec -u own:grp -it $CONTAINER_NAME bash`
