# Gym-Fish Docker
We provide a docker image on [Docker Hub](https://hub.docker.com/repository/docker/fnelai/gym-fish) where everything is configured and you can train your fish immediately.

## 1. Nvidia Docker Setup
To utilize CUDA in fluid simulation, the docker environment requires the [Nvidia Container Toolkit](https://github.com/NVIDIA/nvidia-docker) which is available on a variety of Linux distributions. 

Please refer to [Official Installation Guide](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html) for detailed information.

## 2. Play with Docker

### Pull Docker Image
Once the Nvidia Container Toolkit is installed, you can pull the docker image from Docker Hub with  

```
docker pull fnelai/gym-fish
```

You might need to wait for a while.

### Create Container
To create a container from pulled docker image, run the following commands.

```
docker run -it --gpus all -p 8888:8888 --name my-gym-fish fnelai/gym-fish /bin/bash
```

The `-p` parameters forward 8888 port for jupyter notebook.

### Use Jupyter Notebook
You can start the jupyter notebook with

```
start-jupyter-notebook.sh
```

After the jupyter notebook is started, you can browse http://localhost:8888 on your computer to access the notebook demos. It is recommended to set a password at the first time with displayed token so that you can after that call

```
set-autostart-jupyter.sh
```

which starts the jupyter notebook automatically when the container starts.

### Extra Requirements
Some notebook demos have extra requirements, you can install them by calling

```
install-recommends.sh
```

### Start & Stop Docker
```
docker start my-gym-fish 
# start jupyter automatically 
# if you have called set-autostart-jupyter.sh
```
```
docker start -i my-gym-fish
# start the docker with interactive stdin
```
```
docker stop my-gym-fish
```

### Docker Tips
We have provided many other scripts in docker to make your life easier. You can explore all helper scripts in `/root/util`. The installation scripts are also available in `/root/util/installed/install.sh`. Do whatever you want in your container and have fun!


# Installation

Alternatively, you can install the whole environment yourself instead of using the docker image. 

## Framework Setup
The framework depends on [DART](https://github.com/dartsim/dart) and [CUDA](https://developer.nvidia.com/cuda-toolkit). The gym is based on python 3.6.9.

### 1. DART Installation

It is recommended to install DART using Ubuntu packages with Personal Package Archives
```
sudo apt-add-repository ppa:dartsim/ppa
sudo apt-get update # not necessary since Bionic
sudo apt-get install libdart6-dev
```
Please refer to [Official DART Installation Guide](http://dartsim.github.io/install_dart_on_ubuntu.html) for detailed information.

### 2. CUDA Installation
Cuda 10.2 is recommended to run the framework, which can be downloaded from the [NVIDIA website](https://developer.nvidia.com/cuda-10.2-download-archive?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1804&target_type=runfilelocal)

Please also remember to [disable nouveau](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#runfile-nouveau) if you want to also install the driver. Refer to [Official CUDA Installation Guide](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html) more detailed information

### 3. Conda Installation
Install either [Anaconda](https://www.anaconda.com/products/individual#Anaconda%20Installers) or [Miniconda](https://docs.conda.io/en/latest/miniconda.html) or use your favorite python virtual enviroment. The framework is based on python 3.6.9.

### 4. Python Environment Setup
```shell
conda create -n gym_fish python=3.6.9
conda activate gym_fish
conda install -c conda-forge moderngl
```

### 5. Install Fish Gym
```shell
git clone https://github.com/dongfangliu/gym-fish.git
cd gym-fish
pip3 install -e .
```

### 6. To test the learning compability, you may consider install stable-baselines3
```shell
conda activate gym_fish
pip3 install 'stable-baselines3[extra]'
```

### 7. (for headless machines) Virtual Display
If you are using a headless machine (server/cluster). Please either connect to a remote display or running a local virtual display. Otherwise you might meet an *XOpenDisplay* error when you render. Details can be found in [Moderngl: Headless on Ubuntu 18 Server](https://moderngl.readthedocs.io/en/latest/techniques/headless_ubuntu_18_server.html)


<!-- ## Install dependencies

The only necessary dependency is [DART](https://github.com/dartsim/dart) and [CUDA](https://developer.nvidia.com/cuda-toolkit).
For DART installation, please refer to [Here](https://dartsim.github.io/install_dart_on_ubuntu.html).
We highly recommend to use latest version of DART and CUDA, specifically, DART 6.10.1 and CUDA 11.0 .

*Note for headless machines (server/cluster), please install dependencies for running a virtual display for scene rendering*
```shell
sudo apt install python3-pip mesa-utils libegl1-mesa xvfb
```

## Python Environment Setup
```shell
conda create -n gym_fish python=3.6.9
conda activate gym_fish
conda install -c conda-forge moderngl
```

## Install Fish Gym
```shell
git clone https://github.com/dongfangliu/gym-fish.git
cd gym-fish
pip3 install -e .
```

## Install stable-baselines3
To test the learning compability, you may consider install stable-baselines3
```shell
conda activate gym_fish
pip3 install 'stable-baselines3[extra]'
``` -->