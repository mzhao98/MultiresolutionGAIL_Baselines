# MultiresolutionGAIL_Baselines
Hierarchical Multiscale Recurrent Neural Network and Clockwork RNN implementations as baselines for comparison to a Multiresolution GAIL algorithm.

## Investigation/Implementation of Baselines

## A.	Hierarchical Multiscale Recurrent Neural Networks (HMRNN) – Chung 2017
### Summary of Algorithm:

HMRNN does not assign fixed update rates, but adaptively determines proper update times corresponding to different abstraction levels of the layers. This model tends to learn fine timescales for low-level layers and coarse timescales for high-level layers. There is a binary boundary detector at each layer. The boundary detector is turned on only at the time steps where a segment of the corresponding abstraction level is completely processed. Based on the binary boundary detector, at each time step, we implement one of three operations: UPDATE, COPY, FLUSH. UPDATE updates the state following the usual update rule of LSTMs. The COPY operation simply copies the cell and hidden states, doing no update. FLUSH is executed when a boundary is detected, informing us that we’ve hit  boundary between abstraction levels. The HMRNN learns to select a proper operation at each time step and to detect the boundaries, the HMM discovers a latent hierarchical structure of the sequences. 

## B. Clockwork Recurrent Neural Networks (CRNN) – Koutnik 2014
### Summary of Algorithm:

In the CRNN, the hidden layer is partitioned into separate modules, each processing inputs at its own temporal granularity, making computations only at its prescribed clock rate. The CRNN has different parts (modules) of the RNN hidden layer running at different clock speeds, timing their computation with different, discrete clock periods. CRNNs consist of input, hidden, and output layers. There are forward connections from the input to hidden layer, and from the hidden to output layer. The neurons in the hidden layer are partitioned into g-modules of size k. Each of the modules is assigned a clock period Tn. Each module is internally fully interconnected, but the recurrent connections from module j to module I exists only if the period Ti is smaller than the period Tj. Sorting the modules by increasing period, the connections between modules propagate the hidden state right-to-left, from slower modules to faster modules. What this allows for is, the low-clock-rate modules process, retain, and output the long-term information obtained from the input sequences, whereas the high-speed modules focus on the local, high-frequency information. For error propagation, the error propagates only from modules that were executed at time step t. 
