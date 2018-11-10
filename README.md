# Weights-and-Unit-Neuron-Pruning

In this project, my aim is to train a large neural network and then prune it to understand how the accuracy of the NN is
affected as more and more of it pruned. Pruning here effectively referes to increasing sparsity in the network, and given a
neural network layer, pruning can be performed in 2 ways:

1. Weight pruning: set individual weights in the weight matrix to zero. This corresponds to deleting connections between the
neurons of consecutive layers. Here, to achieve sparsity of k% we rank the individual weights in weight matrix W according
to their magnitude (absolute value) |w(i,j)|, and then set to zero the smallest k%.

2. Unit/Neuron pruning: set entire columns in the weight matrix to zero, in effect deleting the corresponding output neuron.
Here to achieve sparsity of k% we rank the the columns of a weight matrix according to their L2-norm & delete the neurons with  smallest k% norms.

Naturally, as we increase the sparsity and delete more of the network, the task performance will progressively degrade.

In this project, I plotted the accuracy vs sparsity plots for both weight pruning and neuron pruning.

To run the files and reproduce the results, run clone and download the reposirory. Keep all the files in the same folder. Each
jupyter file is a standlone file and does not depend on other files, so you can run the 4 Jupyter files in any order.

The details about the 4 Jupyter notebooks are as follows:

1. NN Weights and neuron pruning
In this notebook, a neural network with 4 hidden layers (1000, 1000, 500, 200 neurons respectively) is trained over the MNIST
dataset. After training, it is weight and neuron pruned for the following sparsity values (0,25,50,60,70,80,80,
95,97 and 99) and accuracy versus sparsity curves are plotted for both types of pruning.

2. NN Recovery analysis  - Weight pruning
Here, the weight pruned network is trained again for 500 iterations over the training data. The goal is to observe whether
the weight pruned network is able to recover the original accuracy.
Plots of original accuracy, weight pruned accuracy and weight pruned accuracy with retraining vs sparsity are plotted.

3. NN Recovery analysis  - Neuron pruning
Here, the neuron pruned network is trained again for 1000 iterations over the training data. The goal is to observe whether
the neuron pruned network is able to recover the original accuracy.
Plots of original accuracy, neuron pruned accuracy and neuron pruned accuracy with retraining vs sparsity are plotted.

4. NN Increasing the test time efficiency via Unit or Neuron Pruning

In this notebook, an attempt is made to increase the test time execution speed by using sparsity results obtained above.
All those neurons which were rendered passive (by making their corresponding weights 0) in the neuron pruned network are 
now deleted, thus decreasing the size of each hidden layer(except the last layer). This gives a neural network which has lesser number of neurons than the original network.

The test execution time is calculated in 2 ways:

i) The smaller network is used to calculate accuracy on the test set and execution time is noted. Here, the network suffers decrease in accuracy as k% neurons in each hidden layer(ewxcept the last hidden layer) have been deleted.

ii) The smaller network is forst retrained and then the accuracy and execution and test time accuracy are noted. Here, the network recovers the accuracy while maintaining the same execution time as in part (i).
The test execution time decreases by a factor of 6-7 while the accuracy over the test same remains the same.

Thus, we conclude that a neural network has a very large number of excess neurons which can be deleted once the network has been trained. After deleting these excess neurons, we retrain the smaller network and in this way, the test time execution speed can be increases substantially.

These codes have been run on MacBook Pro (13-inch, 2017) with 2.3 GHz Intel Core i5 processor.
