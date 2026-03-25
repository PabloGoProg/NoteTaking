**Whats** docker?__ Tool to create, manage and publish containers.

### Diff between VMs, Containers

1. __Isolating:__ complete isolating in VMs (Complete OS independent of host) - Light isolating in Containers (==Share Kernel with host OS==).
2. __Resource Efficiency:__  VMs needs all required resources to run the OS - ==Containers just include libs and dependencies==.
3. __Faster booting:__ The containers boots faster since they do not run an isolated OS.

### Docker Flow

`1. Dockerfile -- build --> 2. Docker Image -- run --> 3. Docker Container`

#### 1. Dockerfile to Image

To create a `Dockerfile` we need to create a file with this name on the root of the project:

```
/my-project
	/src
	/tests
	/docs
	...
	Dockerfile
	README.md
```

``` SHell
FROM base_image:required_tag

WORKDIR /app # Python way

COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt

COPY . .

CMD ['python', '-m', 'flask', 'run', '--host=0.0.0.0']
```

Once we have our Dockerfile finished we should run the next command to transform the file into an image

``` Shell
docker build -t img_name:img_tag docker_file_path
docker biuld -t web_site:latest .
```

#### 2. Image to Container

``` Shell
$ docker run parameters --name container_name image_name
$ docker run -it --rm -d -p 8080:80 --name my_container web_site

# -it = container logs shown
# --rm = removes previous containers with that image
# -d = runs container in scnd pane -- awaiting user interaction
# -p = ports communication with image : image communication with app
```

### Volumes

mechanisms used for storing data outside the container. All volumes are managed by docker and stored in a dedicated directory in the host.

### Container Layers

