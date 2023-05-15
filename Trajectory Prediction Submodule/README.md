# Deep Learning Based Trajectory Prediction Submodule

In this part we have designed a deep learning based trajectory prediction submodule.

## Data Preprocess

As this method is a data driven slef-supervised method, the first step for this submodule is generating corresponding representative trajectory data and feed this data to the model. There are mainly two types data source as follows:

* The data generated by human
* The data generated from the result of MPC controller

For the first source please refer to the file \utils\referenceGenerator.py, the output for this py file should many paris [3, 80] data segment which represent the preformance of [x, y, v] states in the 80 steps. We can change some specfic parameters to modify the content of this dataset.

For the second source, we can directly read the generated target vehicles' trajectories and input these trajectories to the model to get more specfic performance.

In \utils\process_data we will split the data into desired format. In this project we will use batch trainting which means we will train the neural network with 32 pairs data in the same time. Besides, we also need the functions in this file to split the batch dataset [3, 32, 80] into [3, 32, 30] and [3, 32, 50]. The former part is the input of this model and the second part works as groundtruth.

## Neural Network

* Model is coded in Model.py where we have useded RNN and CNN.
* We adopt MSE as our loss function and the function is defined in \utils\neural_network.py
* In file Training.py we designed the training process and we can change the epoch value to evalute the training performance.
* The file visualization helps to intuitive visualize the training performance. 