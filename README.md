## Learning to Control DC Motor for Micromobility in Real Time with Reinforcement Learning

Related: [paper](10.1109/ITSC55140.2022.9921919), [Arxiv](https://arxiv.org/abs/2108.00138), [Video](https://www.youtube.com/watch?v=TgZS54wQ3ss)


<p align="center">
  <img src="https://github.com/poudel-bibek/NFQ_Golf_Cart/blob/main/site_assets/oscillate_small.gif?raw=true" alt="Alt Text">
  <br>
  <i>Steering wheel oscillating between extreme left and extreme right</i>
</p>

<p align="center">
  <img src="https://github.com/poudel-bibek/NFQ_Golf_Cart/blob/main/site_assets/various_states.png?raw=true" width="650" height="150" alt="Alt Text">
  <br>
  <i>Green= Goal states, Blue= Initial states, Red= Forbidden states</i>
</p>

------
## 1. Installation and Code Dependencies

Built on `Python 3.9.16`, Install NVIDIA Drivers + CUDA if you want to use GPU.

Intstall requirements:

```
pip install -r requirements.txt 
```

------
## 2. Understanding the Code:

`NFQ_main`: Central file integrating all components.

`NFQ_Env`: Simulates environment; hardware execution separate from `XXX`.

`NFQ_model`: Defines the neural network (Q-function approximator).

`NFQ_Agent`: Manages NFQ algorithm functions, supervised data generation, and model training.

`Steerbox_Env`: Handles position initialization strategies and environment interaction.

`Steerbox_NFQ`: Covers additional NFQ functions, goal (hint-to-goal) pattern sets, experience collection, and reward definition.

`Utils folder`: Provides utilities for generating plots and exploration strategies.

`Hardware_Data/ Simulation_Data folders`: Stores session data for runs.

`Hardware_Code folder`: Code to interface with the Arduino hardware and train hardware controller.   

------
## 3. Running the Code:

```
# run on default arguments
python NFQ_main.py 

# run on experiment related arguments
python NFQ_main.py --num_params [AAA] --hint_size [BBB] --exploration [CCC] --reset_freq [DDD] --pos_init [EEE]

# To save the files of the run
python NFQ_main.py --save_to_file
```

------
## 4. Experiments:

Five experiments are performed: 

| # | Experiment                        | Options                                                           |
|---|-----------------------------------|-------------------------------------------------------------------|
| 1 | Parameter count of neural network | 39, 61, 91, 121, 171                                              |
|   |                                   |                                                                   |
| 2 | Size of Hint-to-goal transitions  | 1%, 2%, 5%, 10%, 20%                                              |
|   |                                   |                                                                   |
| 3 | Exploration strategy              | No exploration,                                                   |
|   |                                   | ε-greedy constant 2%,                                            |
|   |                                   | ε-greedy constant 10%,                                            |
|   |                                   | Linearly decaying ε-greedy,                                       |
|   |                                   | Exponentially decaying ε-greedy                                   |
|   |                                   |                                                                   |
| 4 | Neural network reset frequency    | No reset, reset every: 1, 10, 50, 100 episodes                    |
|   |                                   |                                                                   |
| 5 | Steering wheel position           | Gaussian: mean=0, variance=0.02,                                  |
|   | initialization                    | Gaussian: mean=0, variance=0.09,                                  |
|   |                                   | Uniform: range [-0.5, 0.5],                                       |
|   |                                   | Linearly expanding range,                                         |
|   |                                   | Exponentially expanding range                                     |

Choose experiments from the arguments in `NFQ_main.py`

<p align="center">
  <img src="https://github.com/poudel-bibek/NFQ_Golf_Cart/blob/main/site_assets/experiments.png?raw=true" alt="Alt Text">
  <br>
  <i>Results of experiments (each averaged over 5 simulation runs)</i>
</p>

-------
## Cite

```
@inproceedings{poudel2022learning,
  title={Learning to Control DC Motor for Micromobility in Real Time with Reinforcement Learning},
  author={Poudel, Bibek and Watson, Thomas and Li, Weizi},
  booktitle={2022 IEEE 25th International Conference on Intelligent Transportation Systems (ITSC)},
  pages={1248--1254},
  year={2022},
  organization={IEEE}
}
```

*The repo is inclusive of hardware and code contributions from: [tpwrules](https://github.com/tpwrules)
