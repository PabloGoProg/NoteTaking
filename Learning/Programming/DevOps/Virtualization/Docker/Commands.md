``` Shell
# Commonly used commands
$ docker info     # Get info about the hardware used by docker
,

# images

# Builds an image from a docker file
$ docker build -t img_name:img_tag docker_file_path
# Show all images
$ docker images
# Show images based on names
$ docker images image_name
# SHow images based on filter ex. '*:1.0'
$ docker images --filter=reference='name:tag'
# Show images with full id
$ docker images --no-trunc
# Update a image tag
$ docker image tag current_name:current_tag new_nmae:new_tag
# Remove an image
$ docker rmi name:tag | img_id
# Download an Image from a registery
$ docker pull image_mame:tag

# Containers

# List locally installed containers
$ docker ps
# List all containers (independent of status)
$ docker ps -a
$ docker ps --size # Shows cont size
# Create a new container
$ dokcer create container_name image_name
# Run a container
$ dokcer start container_name
# Stop a container
$ dokcer stop container_name | cont_id
# Looks locally for a container -> If not found then install from Dokcer hub
# Creates the container
# Run the container
$ docker run --name container_name image_name
$ docker run -it --rm -d -p 8080:80 --name cont_name image_name
# Shows cont consummed resources stats
$ docker stats
# Follow logs from a container
$ docker --follow container_name 

$ docer exec      # Executes a command in a running container
```