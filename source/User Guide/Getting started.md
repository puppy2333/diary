# Getting Started

## Run the environment
Now that we will try to run a basic task environment: point to point navigation.
```shell
conda activate gym_fish
python3
```
```python
import gym
import gym_fish
# Our environment runs on GPU to accelerate simulations,ensure a cuda-supported GPU exists on your machine
gpuId = 0
env = gym.make('fish-basic-v0',gpuId =gpuId)
action = env.action_space.sample()
obs,reward,done,info = env.step(action)
```

## Render the scene
Then we can see the scene in two modes : `human` and `rgbarray`.
`human` is suitable for machines that with a display.
`rgbarray` is for headless machines.

### For machines with a display
```python
env.render(mode='human')
```

### For headless machines (server/cluster)
Run a virtual display. for more details,check [here](https://moderngl.readthedocs.io/en/latest/techniques/headless_ubuntu_18_server.html)
Run follwing commands in your shell:
```shell
export DISPLAY=:99.0
Xvfb :99 -screen 0 640x480x24 &
```
Render and outputs a numpy array
```python
# This outputs a numpy array which can be saved as image
arr = env.render(mode='rgbarray`)
# Save use Pillow
from PIL import Image
image = Image.fromarray(arr)
# Then a scene output image can be viewed in 
image.save('output.png')
```