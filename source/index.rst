Fish Gym
=====================================

(Main purpose)

Fish Gym is a physics-based simulation framework for physical articulated underwater agent 
interaction with fluid. This is the first physics-based environment that support coupled 
interation between agents and fluid in semi-realtime. Fish Gym is integrated into the OpenAI Gym 
interface, enabling the use of existing reinforcement learning and control algorithms to control 
underwater agents to accomplish specific underwater exploration task.

.. warning:: Note this environment is now tested on Ubuntu18.04 and later, not tested on Mac, definitely not work on Windows due to dependency issues.

Github repository: https://github.com/dongfangliu/gym-fish

.. toctree::
   :maxdepth: 2
   :caption: User Guide:

   User Guide/Installation
   User Guide/Getting started
   User Guide/Load and run a trained policy
   User Guide/Train your own policy
   User Guide/Evaluate your policy
   User Guide/Tips for usage

.. toctree::
   :maxdepth: 2
   :caption: Environments:

   Environments/Introduction
   Environments/FishEnvBasic

.. toctree::
   :maxdepth: 2
   :caption: Env Customization:

   Env Customization/Robot creation
   Env Customization/Robot visual editing
   Env Customization/Rigid world setup
   Env Customization/Fluid setup
   Env Customization/Compose env file
   Env Customization/Write your env

.. toctree::
   :maxdepth: 2
   :caption: API list:

   API list/API-1