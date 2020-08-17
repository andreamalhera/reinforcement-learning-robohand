# Project: Training a robot hand to throw a ball
## LMU Reinforcement Learning Praktikum 2019

## Abstract:
You can teach an old robot new tricks:
As a university project, I was able to spend the last weeks learning more about
Reinforcement Learning and implement a project. Reinforcement Learning is a technique
to allow an agent, e.g. a robot to take actions and interact with its environment so as
to maximise the total rewards. If this reminds you of training a dog, you are correct.
So far this approach has also been quite successful for autonomous systems, robotics and gaming. If you would like to know how a human can teach a robot to learn on its own and reach a given goal, please feel welcome to join this talk.

## Presentation Slides:
* [Project Final Presentation at LMU Munich](https://github.com/andreamalhera/reinforcement-learning-robohand/blob/master/presentation_slides/Robby_robot_hand_uni.pdf) [edit](https://docs.google.com/presentation/d/1oRmDDGKMB_C7ISJgBT3auB_IZWQQS9eyBsHfChOiap8/edit)
* [PyConDe 2019 Lightning Talk (5 min)](https://github.com/andreamalhera/reinforcement-learning-robohand/blob/master/presentation_slides/robby_2_5min_lightningtalk.pdf) [edit](https://docs.google.com/presentation/d/11uKLWPDoD_YKr--j9TG3pPIvMzhpDtq16oPdWPUVLnY/edit)
* [Research Presentation at LMU Munich 2020 (10-15 min)](https://github.com/andreamalhera/reinforcement-learning-robohand/blob/master/presentation_slides/robby_10_15_min_future_research.pdf) [edit](https://docs.google.com/presentation/d/15yNk10FULY389fQZD6AdsOLlAP-UqpZKCokKtPMFLa4/edit)
* [Python Pizza Conf 2020 Lightning Talk (2 min)](https://github.com/andreamalhera/reinforcement-learning-robohand/blob/master/presentation_slides/robby_2_5min_lightningtalk.pdf) [edit](https://docs.google.com/presentation/d/11uKLWPDoD_YKr--j9TG3pPIvMzhpDtq16oPdWPUVLnY/edit)

# Important Documentations

[MuJoCo Python API](https://openai.github.io/mujoco-py/build/html/index.html)

[MuJoCo XML Reference](https://www.mujoco.org/book/XMLreference.html)

[Gym Wrappers](https://github.com/openai/gym/tree/master/gym/wrappers)

# Installation
## Prerequisite

Since gym can only run mujoco on Linux and macOS, this guide **does not work for windows!**

1. Get your mujoco license here by following the listed steps: https://www.roboti.us/license.html

2. Download mujoco200 binaries for your system(linux or macos!) from: https://www.roboti.us/index.html

3. Unzip the content of ``mujoco200_<os_name>`` to your home directory at``.mujoco/mujoco200/``

4. Add your key text file as described in the email from mujoco under ``.mujoco/``

For OS specific install instructions go to the suiting subsection

## Installation for Macbook
```
conda create --name reinforcement-learning-robohand_venv python=3.6
conda activate reinforcement-learning-robohand_venv

Before installing the custom env, make sure gym has been uninstalled.
Install custom environment via: 

pip install git+git://github.com/rl-praktikum-2019/gym.git@throw-ball-environment
pip install -r requirements.txt``

brew install cmake boost boost-python sdl2 swig wget

brew install gcc
ls zu gcc-x in '/usr/local/Cellar/gcc'
export CC=/usr/local/Cellar/gcc/9.1.0/bin/gcc-9

pip install -U 'mujoco-py<2.1,>=2.0'
```
### Environment variables for conda env
```
cd $CONDA_PREFIX
mkdir -p ./etc/conda/activate.d
mkdir -p ./etc/conda/deactivate.d
touch ./etc/conda/activate.d/env_vars.sh
touch ./etc/conda/deactivate.d/env_vars.sh
````
Add following exports to $CONDA_PREFIX/etc/conda/activate.d/env_vars.sh:
```
export LD_LIBRARY_PATH=/Users/<username>//.mujoco
export PYTHONPATH="$PYTHONPATH:/Users/<username>/git_tree/reinforcement-learning-robohand"
````


## Installation on Ubuntu

As mentioned above make sure that mujoco binaries are in``$HOME/.mujoco/mujoco200/`` and your key is in ``$HOME/.mujoco/``

Add your mujoco bin path to to end of your .bashrc via:

``
nano ~/.bashrc
``

then add the followng line to the end of bashrc:

``export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$HOME/.mujoco/mujocoXXX/bin``

close and save your changes in nano and persist via:

``
source ~/.bashrc
``

Run the following command to install mujoco-py

**Hint:**

If your are using PyCharm you may encounter an error where the mujoco-py package is not found.
Run the command from the linux os terminal targeting the python.exe from your desired (conda) environment:

``<path to your conda python.exe>/python.exe pip install mujoco-py``

Install mujoco-py and [our custom environment](#custom-environment-for-ball-throwing)


```
pip install requirements.txt
pip install git+git://github.com/rl-praktikum-2019/gym.git@throw-ball-environment
```

## Dependencies

All dependencies are included in the ``requirements.txt``

# Run

## Ubuntu with PyCharm
Add ``LD_LIBRARY_PATH`` with value ``$HOME/.mujoco/mujoco200/bin`` as a environment variable to your run configuration of the main execution .py file.

## Run from terminal with commands

- E.g.: For ddpg: ``python experiment_main.py --render-env --env=ThrowBall-v0 --algo='ddpg'``

# Custom environment for ball throwing

Github Repository: https://github.com/rl-praktikum-2019/gym

Before installing the custom env, make sure gym has been uninstalled.
Install custom environment via: 

``pip install git+git://github.com/rl-praktikum-2019/gym.git@throw-ball-environment``

Extends the given HandEnv for gym by:

- Removing the visible target goal/ball which was floating above the hand and obstructed a good view on hand and ball
- Reduced mass of robot joints to allow for more speed in finger movement
- Added a visible ground plane to give more depth to the scene
- Changed reward in order to encourage ball throwing in vertical direction.
