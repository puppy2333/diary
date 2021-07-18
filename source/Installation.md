# Installation

## Install dependencies

The only necessary dependency is [DART](https://github.com/dartsim/dart) and [CUDA](https://developer.nvidia.com/cuda-toolkit).
For DART installation, please refer to [Here](https://dartsim.github.io/install_dart_on_ubuntu.html).
We highly recommend to use latest version of DART and CUDA, specifically, DART 6.10.1 and CUDA 11.0 .

*Note for headless machines (server/cluster), please install dependencies for running a virtual display for scene rendering*
```shell
sudo apt-install python3-pip mesa-utils libegl1-mesa xvfb
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