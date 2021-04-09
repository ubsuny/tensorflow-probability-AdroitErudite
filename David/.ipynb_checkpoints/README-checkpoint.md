# Homework 5

## Problem 1

Implementing the Randomwalks with Tensorflow was to replace the random number generation with tensorflow's random module. The $\sigma^2$ quantities for each dimension versus time gave a Diffusion constant (via the slope). Converting the steps back into numpy is just for matters of speed; typically numpy has been faster on my raspberry than tensorflow most likely from the numpy hardware optimization.

Each dimension has a different slope beceause each walk is now slit into different possible dimensions. So calculating D using $D = \frac{s}{2 n_{dim}}$, where $s$ is the slope. Error ranges from 5% to 10% depending on the seed chosen, given 1000 walkers and 5000 steps they that. So even though there are larger amounts of data, the convergence is slow. These values seem to not change much for larger and larger steps or walkers.

Interestingly enough, all of the diffusion constants were lower than expected.

## Problem 2

Finding a suitable replacement in Tensorflow Probability took a few steps. Trying to dive straight into the Metropolis Hastings function was not very intuitive. Also, the probablistic function for the original C++ code was not normalized, where the tensorflow distributions are normalized by default. This is what led to the mixing of the two. 

The second issue I ran into is that the random walk was not switching between the center and the right peak as frequently as expected. I suspect this might be a combination of the step size not being one and that the chances that chances from moving from one peak to another is very slim,  requiring many more steps for these jumps to occur. 

Interestingly enough, this did not affect the historgram except for the off chance that there is no jump even in my walks. The distribution of these events is still correct, but with the chance for peak jumping to be diminished. This led me to making the right peak lower in amplitude so that more of this jumping occured.

Overall, this can be improved further with a deeper understanding of Tensorflow probability.