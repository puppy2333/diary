# Native Install

Alternatively, you can install the whole environment yourself instead of using the docker image. 

## Framework Setup

The framework depends on [DART](https://github.com/dartsim/dart) and [CUDA](https://developer.nvidia.com/cuda-toolkit). The gym is based on python 3.6.9.

### 1. DART Installation

It is recommended to install DART using Ubuntu packages with Personal Package Archives

```shell
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