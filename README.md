# 2048 Neuroevolution

## Introduction
The goal of this project is to create a bot for the game [2048](http://gabrielecirulli.github.io/2048/), using fixed topology neural network evolutionary algorithms, inspired by survival of the fittest. A trial solution, called a *creature* or *individual*, is characterised by its genetic representation, which encodes its behavior. In this project a creature is a neural network, while the genetic representation are the weight matrices of the network. The network takes as input the game's grid and outputs a suitable move. Then a collection of creatures is called a *population*. Neuroevolution can be applied as long as we have a *fitness function* that evaluates each network's performance and *evolution operations*, ways to create creatures based on others. The fitness used is the end game score.

### Model Parameters
The model used is a neural network. The input layer has one neuron for each cell of the game's grid, while the input value is the value of the cell divided by the current max value so that the input range is [0, 1]. Other methods of input handling should be studied. The output layer, consists of four neuron each representing a move (left, right, down, up) and the value represents the confidence in the specific move. Finally the topology of the hidden layers, that remains fixed, is determined by the size of the grid.    

The genetic representation used is a direct encoding scheme where the weight matrices of the network are explicitly represented, however it does not include all model parameters, such as the topology and input handling. Indirect encoding schemes allow more compact representations. As a result, a long representation results in high-dimensionality of the model space.

### Evolution Parameters 
The evolutionary algorithm first generates the initial population at random, then each creature is evaluated using the fitness function. After killing some of the least-fit creatures, offspring can be created from the best-fit creatures through evolution operations. Finally, the creatures are again evaluated and the cycle continues. Each cycle is called a *generation*, after a sufficient number of generations the algorithm converges to a maximum.

The fitness function is defined as the average game score of around 70 games due to the game's random nature. At each step the network is fed the current grid and the move played is the one with the highest confidence, as long as that move is valid the game continues. Hence, the goal of the algorithm is to improve the fitness score.

As the population size increases the chance of the algorithm converging to an optimal solution increases, as there is more genetic diversity. However, a large population size is not computationally efficient and the number of generations required to reach convergence increases. Usually sizes vary mostly between 50 and 200 creatures.

### Evolution Operations
In every generation after the creatures are evaluated the least-fit are dumped so new ones can be created, replacing them. The processes of creating offspring, based on the best-fit creatures, are the evolution operations. These operations could be based on multiple or a single parent. In this project single parent mutations are used. Specifically, the offspring has the same weights as the parent, however the is an 1-2% chance of a mutation, a slight change in the weight value, happening. Another type of mutation would be to change all the weights of a single neuron in the network.


## Results
First we try the method on a 2 by 2 board, where achieving the best strategy should be easier, aiming at extracting information that could help us tackle the 4 by 4 problem.
