# Instructions for running MultiCamSelfCal inside docker container.

This is necessary because MultiCamSelfCal does not appear to work in Octave version > 4. 

If docker is not already installed on your system, please install  using the official [Docker documentation](https://docs.docker.com/engine/install/).

### 1. Clone the repository

In the terminal, navigate to where you plan to install this repository. Clone this repo onto your Desktop with the following:

```bash
git clone https://github.com/florisvb/multicamselfcal_camera_calibration_in_docker.git
```

### 2. Build the Docker image

1. Enter the repository directory:
`cd multicamselfcal_camera_calibration_in_docker`

2. For convenience, save the full path of the repository location as an environment variable in your .bashrc: 
`echo 'export MCSC_PATH=~/multicamselfcal_camera_calibration_in_docker' >> ~/.bashrc`

3. Navigate to the `docker_MultiCamSelfCal` folder:
`cd $MCSC_PATH/docker_MultiCamSelfCal`

4. Build a Docker image from within the `docker_MultiCamSelfCal` folder:

```bash
sudo docker build -t multicamselfcal_image .
```

### 3. Run Interactive Container and External Mount

Run the Docker image with the following tags to start the Docker container with an interactive bash shell and live data mount:

```bash
sudo docker run --name multicamselfcal_env -it -v ~/Desktop/braid_camera_calibration/docker_mount:/home/host_mount multicamselfcal_image bash
```

You should see the command prompt change to something like this:
`root@bf2fb5040035:/home#`

This command puts the shared directory in `~/Desktop/braid_camera_calibration/docker_mount`. You can change that if you want it somewhere else. The Docker container can interact with the host system through that mount, and vice-versa. Put whatever files you want to use in `~/Desktop/braid_camera_calibration/docker_mount`, and you will see it in the `/home/host_mount` directory of the docker container. Similarly, any files written to `/home/host_mount` will be visible in `~/Desktop/braid_camera_calibration/docker_mount`

### 4. Test with sample data

In a different terminal (not the one running the docker):

Copy the sample data into the docker_mount:
`sudo cp -r $MCSC_PATH/example_data/sample_calibration_data.braidz.h5.recal ~/Desktop/braid_camera_calibration/docker_mount`

Now the sample data will be accessible to  the docker container. 


### 5. Run the MultiCamSelfCal command

In the docker container:

The Docker container should have the following structure:
```
home
|-- host_mount
`-- MultiCamSelfCal
```
Navigate to: `cd /home/MultiCamSelfCal/MultiCamSelfCal` and run:
```
octave gocal.m --config='/home/host_mount/sample_calibration_data.braidz.h5.recal/multicamselfcal.cfg' 
```

This will take a while, but it should converge. 

### Exiting, killing, and restarting the docker container

Helpful commands:

* From inside the docker container, `ctrl-d` will exit, but leave the container in an inactive state.
* To list all docker containers, including inactive ones: `sudo docker ps -a`
* To close a docker container: `sudo docker rm CONTAINER_ID` where CONTAINER_ID is the ID you see when you run the command above. 
* To restart a inactive container: `docker start container_name`

