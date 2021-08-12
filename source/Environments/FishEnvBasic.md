# FishEnvBasic

## Introduction

FishEnvBasic, as its name suggests, is the most basic environment in fish learning. The fish has 
a target and it aims to swim to that target as fast as possible in this environment. We will use experiment `point point navigation koi.ipynb` as an example to show what this environment does and how can we use it. To keep the introduction elegant, some unimportant parts in the experiment have been skipped.

```python
gpuId = 0
control_dt = 0.2
theta = np.array([90, 90])
phi = np.array([0, 0])
radius = 2.0
max_time = 10
done_dist = 0.15
dist_distri_param = np.array([0.0, 0.0])
wc = 0.0*np.array([1.0, 0.5])
wp = 1.0*np.array([0.0, 1.0])
wa = 0.5
```

These variables will be used in the environment setting process. 

`gpuId` determines which GPU to use when training data. It is useful when the compute node has more than one GPUs. If the machine only has one GPU, set it to be zero is okay.

`control_dt` is the time interval between two control commands are released. And `max_time` is the maxium simulation time.

`theta`, `phi`, `radius` and `dist_distri_param` are variables that determines the position of fish in space. `theta` and `phi` refers to the pitch and yaw angle of fish, respectively. Each of them is represented by an array [a, b], meaning the data can be sampled from -a to b. For theta, the maxium values for a and b are both 90, and for phi, the maxium values are both 180. The data will be uniformly sampled from the range. `radius` is the distance between the fish start point and target point. `dist_distri_param` is the distance between fish start position and track start position.

`done_dist` is the maxium distance below which the fish can be seemed as reached the goal.

And two reward parameters `wp` and `wa` represent distance reward and action reward seperately.

```python
couple_mode =  fl.COUPLE_MODE.TWO_WAY
```

This line of code means that during training, there will be a two-way couple between fish and fluid, meaning that both fish and fluid can bring force to each other.

```python
env = gym.make('fish-basic-v0',
    env_json = '../assets/env_file/env_basic.json',
    gpuId = gpuId,
    couple_mode = couple_mode,
    control_dt = control_dt,
    theta = theta,
    phi = phi,
    radius = radius,
    max_time = max_time,
    wp = wp,
    wa = wa,
    done_dist = done_dist,
    dist_distri_param = dist_distri_param)

env_test = gym.make('fish-basic-v0',
    env_json = '../assets/env_file/env_basic.json',
    gpuId = gpuId,
    couple_mode = couple_mode,
    control_dt = control_dt,
    theta = theta,
    phi = phi,
    radius = radius,
    max_time = max_time,
    wp = wp,
    wa = wa,
    done_dist = done_dist,
    dist_distri_param = dist_distri_param)
```

These codes initialize two identical environments, one for training and another one for testing. The first parameter determines which environment to use. The match between name and environment file are listed in `gym-fish/gym_fish/__init.py`. The second parameter is a json file which determines the parameters of the environment, including rigid body model, fluid model and camera model. And the remaining parameters have been discribed above.

```python
timesteps = int(1e5)
step = int(1e3)
length =int(timesteps/step) 
print(timesteps,step,length)
last_best_reward = -1e5
cur_steps = 0

model = SAC("MlpPolicy", env, tensorboard_log = network_folder + algofoler, verbose = 1)

for i in range(0, length):
    model.learn(total_timesteps = step, log_interval = 1, reset_num_timesteps = False)
    cur_steps = cur_steps + step
    img_name = algo + "_steps_{0}.png".format(cur_steps)
    model.save(network_folder + algofoler + 'models/' + "_steps_{0}".format(cur_steps))
    rr = evaluate_env(env_test, model, title = img_name, traj_fig_name = network_folder + algofoler + 'imgs/trajs/' + img_name, reward_fig_name = network_folder + algofoler + 'imgs/rewards/' + img_name)
    if rr > last_best_reward:
        last_best_reward = rr
        model.save(network_folder + algofoler + 'models/best')

```

Now comes the training process. First we determine some parameters, such as training time. Then a model is built using stable-baselines3, the "SAC" refers to Soft Actor Critic, and a detailed description of it can be found in [Stable-Baselines: SAC](https://stable-baselines.readthedocs.io/en/master/modules/sac.html). Here, MLP is used as the network. Then we learn the model in iterations. Not that we use different environments for training and testing.

The training process will continue for several hours. After that, we will initialize another environment and evaluate the trained environment by loading the best model. 

## Results