# Docker Installation

If docker is not already installed on your system, please install  using the official [Docker documentation](https://docs.docker.com/engine/install/).

### 1. Clone the repository

Clone this repo onto your Desktop with the following:

```bash
git clone https://github.com/nehalsinghmangat/braid_camera_calibration.git
```

### 2. Build the Docker image

Navigate to your local copy of the repo and build a Docker image from within the `docker_flydra_and_strand-braid` folder:

```bash
sudo docker build -t flydra_and_strand-braid_image .
```

### 3. Run Interactive Container and External Mount

Run the Docker image with the following tags to start the Docker container with an interactive bash shell and live data mount:

```bash
sudo docker run --name flydra_and_strand-braid_env -it -v ~/Desktop/braid_camera_calibration/docker_mount:/home/host_mount flydra_and_strand-braid_image 
```

The Docker container can interact with the host system through the mount, and vice-versa. Put whatever files you want to use in `docker_mount`, and you will see it in the `/home/host_mount` directory of the docker container. Similarly, any files written to `/home/host_mount` will be visible in `docker_mount`

### 4. Run the Calibration

The calibration commands are the same as listed in the offical [calibration guide](https://strawlab.github.io/strand-braid/braid_calibration.html), with one minor difference. The Docker container should have the following structure:

```
home
|-- host_mount
|-- flydra
`-- strand-braid
```

Consequently, the first command should be sourced as :

```bash
python3 /home/strand-braid/strand-braid-user/scripts/convert_braidz_to_flydra_h5.py --no-delete 20190924_161153.braidz
```

The rest of the procedure is followed normally. 
