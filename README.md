This project page gives a general overview of the research done in the 2-month working period regarding dexterous manipulation with a visuo-tactile multi-finger hand at Aalto University - School of Electrical Engineering. The project builds the tools to conduct further research among closely related topics and will see further use in the future.

# Simulation

## Overview
- [TACTO](https://github.com/facebookresearch/tacto) serves as the simulation platform. Refer to the documentation for installation and instructions.
- [Stable-Baselines3](https://stable-baselines3.readthedocs.io/en/master/) provides implementations of reinforcement learning algorithms in PyTorch.
- [Gymnasium](https://github.com/Farama-Foundation/Gymnasium) is the base gym environment for agent training.

---

The purpose of the simulation is to explore the possibilities of the robot hand by training RL agents to complete suitable hand manipulation tasks before replicating them in real life. The simulation platform allows for sim-to-real transfer by pre-training agents in a simulation before training them in real-world environments.

## Using TACTO to Simulate & Train Agents

### 1. Valve Agent
The first step of the project is to train a simple valve-turning agent to rotate a valve handle by 180 degrees.

![Project Demo](gifs/latest-ezgif.com-crop.gif)
---
### 2. Bottle Cap Rotating Agent
This agent is designed to better utilize the capabilities of the framework. Here, we apply PCA to extract key components of the tactile images, allowing the agent to learn from the entire observation while drastically reducing the observation space. The PCA is applied to a set of 500 depth images to choose 15 principal components:

![Depth:](imgs/depth_000000.png) ![Color:](imgs/color_000000.png) ![Depth:](imgs/depth_000005.png) ![Color:](imgs/color_000005.png)
![Plot:](imgs/image.png)

PCA image reconstruction:
![Example:](imgs/output0.png) ![Example:](imgs/output5.png) ![Example:](imgs/output4.png)![Example:](imgs/output2.png)![Example:](imgs/output7.png)

Cases to keep an eye on - first image: no contact & second image: full contact (both relatively common in the simulation)
![Example:](imgs/output1.png) ![Example:](imgs/output3.png)

Initial training results:

![Project Demo](gifs/latest1-ezgif.com-speed.gif)
---
## Physical Testing

### Overview
The University offers the multi-finger hand as a testing tool to try out trained policies in the real world. However, sim2real transfers are yet to be made in this project as they will expectedly increase the scope of the research. If you're interested in this,  a paper by Entong Su et al. may be interesting: [Sim2Real Manipulation on Unknown Objects with Tactile-based Reinforcement Learning](https://arxiv.org/abs/2403.12170)

![Project Demo](gifs/MicrosoftTeams-video(2).gif)

### Sim-to-Real
To bridge sim to real, TACTO provides an ability to change the background of the simulated sensor, so both simulated and real tactile images can be used with PCA's or VAE's

![sim2real](imgs/image_copy_3.png)

![sim2real](imgs/image_copy_2.png)

This is achived by simply adding an image background to the digit sensor when creating it:
```python
bg = cv2.imread("path/to/image.jpg")
digits = tacto.Sensor(**cfg.tacto, background=bg)
```

### Discussion
Currently, the project is not being pursued further but serves as a tentative foundation for a future Master's thesis. The exact topic of the thesis has yet to be decided.

## Links
- [Project Repository](https://github.com/trannguyenle95/multifingered-tactile)
---
