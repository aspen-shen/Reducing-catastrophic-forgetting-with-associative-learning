# Reducing-catastrophic-forgetting-with-associative-learning
All methods we tested share the same network architecture: a three-layer network with an input layer (analog to PNs in fruit flies), a single hidden layer (analog to KCs) and an output layer (analog to the MBONs). For the \mnist dataset, the network contains 84 nodes in the input layer, 3200 nodes in the hidden layer, and 20 nodes in the output layer. For CIFAR-100, these three numbers are 512, 20000, and 100 respectively. The size of the hidden layer was selected to be approximately 40x larger than the input layer, as per the fly circuit.

For all models except the FlyModel, the three layers make all-to-all connections. For fly model, the PN and KC layer are connected via a sparse random matrix ($$\Theta$$); each KC sums over 10 randomly selected PNs for MNIST-20, and 64 randomy PNs for CIFAR-100.\\

**Implemenations of other methods** GEM and EWC implementations are adapted from: \url{https://github.com/facebookresearch/GradientEpisodicMemory} under the Creative Commons Attribution-NonCommercial 4.0 International Public
License. The BI-R implementation is adapted from: \url{https://github.com/GMvandeVen/brain-inspired-replay}.

**Parameters** Parameters for each model and dataset were independently selected using grid search to maximize accuracy.

- FlyModel: learning rate: 0.01 (\mnist), 0.2 (CIFAR-100); $l = m/k$, where $k=20$, the number of classes for \mnist and $k=100$ for CIFAR-100; and $m=3200$, the number of Kenyon cells for \mnist, and $m=20000$ for CIFAR-100.
- GEM: learning rate: 0.001, memory strength: 0.5, n memories: 256, batch size: 64, for both datasets.
- EWC: learning rate: 0.1 (\mnist), 0.001 (CIFAR-100); memory strength: 1000, n memories: 1000, batch size: 64, for both datasets.
- BI-R: learning rate: 0.001, batch size: 64 for both datasets. The BI-R architecture and other parameters are default to the original implementation~\cite{Ven2020}.
- Vanilla: learning rate: 0.001, batch size: 64, for both datasets.
- Offline: learning rate: 0.001, batch size: 64, for both datasets.

For Offline, Vanilla, EWC, and GEM, a softmax activation is used for the output layer, and optimization is done using stochastic gradient descent (SGD). For BI-R, no activation function is applied to the output layer, and optimization is performed using Adam with $$\beta_1 = 0.900$$, $$\beta_2=0.999$$.
