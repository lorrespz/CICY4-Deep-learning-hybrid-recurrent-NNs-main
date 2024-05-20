# CICY4: Deep learning Hodge numbers with hybrid CNN-RNN and purely recurrent LSTM-based networks

## Introduction

 In this work, I report the results of applying deep learning based on hybrid convolutional-recurrent and purely recurrent neural network architectures to the dataset of almost one million CICY4 manifolds to learn the four Hodge numbers $h^{(1,1)}, h^{(2,1)}, h^{(3,1)}, h^{(2,2)}$. In particular, we explored 12 different neural network models, nine of which are convolutional-recurrent (CNN-RNN) hybrids with the RNN unit being either GRU (Gated Recurrent Unit) or Long Short Term Memory (LSTM). The remaining four models are LSTM-based networks. In total, I trained the following 12 models (the training was done fully on Kaggle using the P100 GPU unit). 

| Models       | # params ($\times 10^6$) | Total training time (hours)|
| ------------- |:-------------:| :-------------:| 
| CNN-GRU-384 |  2.222  |4.16|
| CNN-GRU-416 | 2.488 |  4.66|
| ResNet-GRU-256 |1.329 | 3.42|
|ResNet-GRU-400| 2.337 | 5.86 |
|CNN-LSTM-256| 1.547  | 4.00|
|CNN-LSTM-384 |  2.674 | 4.77
|CNN-LSTM-400| 2.842  | 6.37|
|CNN-LSTM-416| 3.017  |  8.82|
|LSTM-400 |  2.373 |  3.77|
|LSTM-424 |   2.637 | 4.17 |
|LSTM-448|  2.915| 4.83|
|LSTM-455 | 3.011 | 4.45 |

The organization of this repo is as follows:
  - The training notebooks for the 12 models are contained in the folders 'Models_CNN-RNN-hybrid' and 'Models_LSTM-based'.
  - The trained models are saved in the folder 'Results_p2_Trained_models'.
  - Some figures from the arXiv paper are stored in the folder 'Resutls_p1_Figures'.

## Data
The data used for the training of all models were prepared in the following Kaggle notebook:
 [url here]
 
The train, validation and test sets can be downloaded from the ouptut of the above notebook. 

## Training results
At the training ratio of 72%, our best performing individual model is CNN-LSTM-400, which obtains the accuracies of 99.74%, 98.07%, 95.19%, 81.01%, respectively, for $h^{(1,1)}, h^{(2,1)}, h^{(3,1)}, h^{(2,2)}$. 
Our second best performing individual model is LSTM-448, which obtains the accuracy of 99.74%, 97.51%, 94.24%, and 78.63%. The third best-performing model is LSTM-424, with the accuracies of 99.56%, 97.07%, 93.19%, 74.47%. 

The following ensembles of several top-performing models were formed 
|          |        |
| :-------------: |:-------------:| 
|Ensemble 1| LSTM-448, CNN-LSTM-400 |
|Ensemble 2| LSTM-448, LSTM-424, CNN-LSTM-400|
|Ensemble 3| LSTM-448, LSTM-424, CNN-LSTM-400, CNN-LSTM-384|
|Ensemble 4| LSTM-448, LSTM-424|

The performances of the 12 models plus the four ensembles, ranked in terms of the test accuracies of the four individual Hodge numbers are shown in the figure below.

<img width="1000px" src="https://github.com/lorrespz/CICY4-Deep-learning-hybrid-recurrent-NNs-main/blob/main/Results_p1_Figures/Train_test_accuracies_all.png"  alt="Test accuracies" />

The performances of the 12 models plus the four ensembles in terms of train and test accuracies can be seen the figure below. 

<img width="500px" src="https://github.com/lorrespz/CICY4-Deep-learning-hybrid-recurrent-NNs-main/blob/main/Results_p1_Figures/Train_test_4x_accuracies_all.png" alt="Train and test accuracies of the 12 models considered in this work"/>

## Inference
The saved models, stored in 'Results_p2_Trained_models', can be downloaded and used for inference on the test dataset. The example notebook ' ' demonstrates how to load and use a saved model for inference. 

