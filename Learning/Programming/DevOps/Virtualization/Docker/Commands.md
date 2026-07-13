```shell
# Commonly used commands
$ docker info     # Get info about the hardware used by docker

# images

# Builds an image from a docker file
$ docker build -t img_name:img_tag docker_file_path

# Show all images
# Syntax: docker images [OPTIONS]
$ docker images
$ docker images (name) # List images based on names
$ docker images -q # List images IDs

# SHow images based on filter ex. '*:1.0'
$ docker images --filter=reference='name:tag'

# Show images with full id
$ docker images --no-trunc

# Update a image tag
$ docker image tag current_name:current_tag new_nmae:new_tag

# Remove an image
$ docker rmi (name:tag|img_id)

# Download an Image from a registery
# Syntax: docker pull [OPTIONS] IMAGE:[TAG|@DIGEST]
# `tag` = version - Not using `tag` gets latest version of image
$ docker pull (image_mame:tag)

# Containers

# List locally installed containers
# Syntax: docker ps [OPTIONS]
$ docker ps # List only running containers
$ docker ps -a # List all containers (independent of status)
$ docker ps --size # Shows container size
$ docker ps -x # Background services
$ docker ps -u # Show owner

# Create a new container
# Syntax: docker create [OPTIONS] IMAGE [COMMAND] [ARG...]
$ dokcer create --name (container_name) (image_name):(image_tag)

# Remove a Container
# Syntax: docker rm [OPTIONS] CONTAINER
$ docker rm (container_name|conatiner_id)

# Run a container
# Syntax: docker start [OPTIONS] CONTAINER [CONATINER...]
$ docker start (container_name|container_id, ...more containers)

# Stop a container "gracefully" -> It gives a certaing window of time to
# the container to stop (not inmediately). If the container isn't rdy after 
# that time, it will stop no matter what.
# Syntax: docker stop [OPTIONS] CONTAINER [CONTAINER...]
$ docker stop (container_name|cont_id) # 10 secs until shutdown
$ docker stop -t 30 (container_name|cont_id) # 30 secs until shutdown

# Looks locally for a container -> If not found then install from Dokcer hub
# Creates the container
# Run the container
$ docker run --name container_name image_name
$ docker run -it --rm -d -p 8080:80 --name (cont_name) (image_name)

# Shows cont consummed resources stats
$ docker stats

# Follow logs from a container
$ docker --follow container_name 

# Execute a command insede a running container
# Syntax: docker exec [OPTIONS] CONTAINER COMMAND [ARG...]
$ docker exec (container_name) ls /usr/src/app
$ docker exec -t (container_name) ls /usr/src/app # Allocates a terminal (tty)                                                       to run interactive commands
$ $ docker exec -i (container_name) sudo ls /usr/src/app # Keeps stdin open
$ $ docker exec -it (container_name) sudo ls /usr/src/app # input and output
```