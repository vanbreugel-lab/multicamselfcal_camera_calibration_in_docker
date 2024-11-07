# Instructions for running MultiCamSelfCal inside docker container.

This is necessary because MultiCamSelfCal does not appear to work in Octave version > 4. 

If docker is not already installed on your system, please install  using the official [Docker documentation](https://docs.docker.com/engine/install/).

### 1. Clone the repository

Clone this repo onto your Desktop with the following:

```bash
git clone https://github.com/florisvb/multicamselfcal_camera_calibration_in_docker.git
```

### 2. Build the Docker image

Navigate to your local copy of the repo and build a Docker image from within the `docker_MultiCamSelfCal` folder:

```bash
sudo docker build -t multicamselfcal_image .
```

### 3. Run Interactive Container and External Mount

Run the Docker image with the following tags to start the Docker container with an interactive bash shell and live data mount:

```bash
sudo docker run --name multicamselfcal_env -it -v ~/Desktop/braid_camera_calibration/docker_mount:/home/host_mount multicamselfcal_image bash
```

The Docker container can interact with the host system through the mount, and vice-versa. Put whatever files you want to use in `~/Desktop/braid_camera_calibration/docker_mount`, and you will see it in the `/home/host_mount` directory of the docker container. Similarly, any files written to `/home/host_mount` will be visible in `~/Desktop/braid_camera_calibration/docker_mount`


### 4. Run the MultiCamSelfCal command
The Docker container should have the following structure:
```
home
|-- host_mount
`-- MultiCamSelfCal
```
Navigate inside `/home/MultiCamSelfCal/MultiCamSelfCal` and run:
```
octave gocal.m --config='full/path/to/calibration/calibration.recall/multicamselfcal.cfg' 
```

### 5. Exiting, killing, and restarting the docker container

Helpful commands:

To list all docker containers, including inactive ones: `docker ps -a`
To close a docker container: 
To restart a inactive container: `docker start container_name`
