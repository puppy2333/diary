# Docker Install

We provide a docker image on [Docker Hub](https://hub.docker.com/repository/docker/fnelai/gym-fish) where everything is configured and you can train your fish immediately.

## 1. Nvidia Docker Setup

To utilize CUDA in fluid simulation, the docker environment requires the [Nvidia Container Toolkit](https://github.com/NVIDIA/nvidia-docker) which is available on a variety of Linux distributions.

Please refer to [Official Installation Guide](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html) for detailed information.

## 2. Play with Docker

### Pull Docker Image

Once the Nvidia Container Toolkit is installed, you can pull the docker image from Docker Hub with  

```shell
docker pull fnelai/gym-fish
```

You might need to wait for a while.

### Create Container

To create a container from pulled docker image, run the following commands.

```shell
docker run -it --gpus all -p 8888:8888 --name my-gym-fish fnelai/gym-fish /bin/shell
```

The `-p` parameters forward 8888 port for jupyter notebook.

### Use Jupyter Notebook

You can start the jupyter notebook with

```shell
start-jupyter-notebook.sh
```

After the jupyter notebook is started, you can browse [http://localhost:8888](http://localhost:8888) on your computer to access the notebook demos. It is recommended to set a password at the first time with displayed token so that you can after that call

```shell
set-autostart-jupyter.sh
```

which starts the jupyter notebook automatically when the container starts.

### Extra Requirements

Some notebook demos have extra requirements, you can install them by calling

```shell
install-recommends.sh
```

### Start & Stop Docker

```shell
docker start my-gym-fish 
# start jupyter automatically 
# if you have called set-autostart-jupyter.sh
```

```shell
docker start -i my-gym-fish
# start the docker with interactive stdin
```

```shell
docker stop my-gym-fish
```

### Docker Tips

We have provided many other scripts in docker to make your life easier. You can explore all helper scripts in `/root/util`. The installation scripts are also available in `/root/util/installed/install.sh`. Do whatever you want in your container and have fun!
