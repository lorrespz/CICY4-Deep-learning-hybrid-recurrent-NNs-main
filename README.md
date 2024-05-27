# CICY4: Deep learning Hodge numbers with hybrid CNN-RNN and purely recurrent LSTM-based networks

## Introduction

 In this work, I report the results of applying deep learning based on hybrid convolutional-recurrent and purely recurrent neural network architectures to the dataset of almost one million CICY4 manifolds to learn the four Hodge numbers $h^{(1,1)}, h^{(2,1)}, h^{(3,1)}, h^{(2,2)}$. In particular, I experimented 12 different neural network models, nine of which are convolutional-recurrent (CNN-RNN) hybrids with the RNN unit being either GRU (Gated Recurrent Unit) or Long Short Term Memory (LSTM). The remaining four models are purely recurrent LSTM-based networks. In total, I trained the following 12 models (the training was done fully on Kaggle using the P100 GPU unit) at 72\% training ratio. 

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
|LSTM-456 | 3.011 | 4.45 |

The top three models resulting from this first round of training were retrained at 80\% data split. 

The organization of this repo is as follows:
  - The training notebooks for the 12 models are contained in the folders 'Models_CNN-RNN-hybrid' and 'Models_LSTM-based'.
  - The trained models are saved in the folder 'Results_p2_Trained_models'.
  - Some figures from the arXiv paper are stored in the folder 'Resutls_p1_Figures'.

## Processed data 
The original data set was introduced in the paper "Topological Invariants and Fibration Structure of Complete Intersection Calabi-Yau Four-Folds", arXiv:1405.2073,
and can be downloaded in either text or Mathematic file format from:

https://www-thphys.physics.ox.ac.uk/projects/CalabiYau/Cicy4folds/index.html

A conveniently created dataset using npy file can be obtained by running the script 'create_data.py' from https://github.com/robin-schneider/cicy-fourfolds

For the ease of working with Kaggle notebooks, I created a Kaggle dataset containing the full, train, validation and test sets (among other files) for both the 72\% and 80\% data splits, which can be accessed at:

https://www.kaggle.com/datasets/lorresprz/calabi-yau-cicy-4-folds

## Training results (72% data split)
At the training ratio of 72%, our best performing individual model is CNN-LSTM-400, which obtains the accuracies of 99.74%, 98.07%, 95.19%, 81.01%, respectively, for $h^{(1,1)}, h^{(2,1)}, h^{(3,1)}, h^{(2,2)}$. 
Our second best performing individual model is LSTM-448, which obtains the accuracy of 99.74%, 97.51%, 94.24%, and 78.63%. The third best-performing model is LSTM-424, with the accuracies of 99.56%, 97.07%, 93.19%, 74.47%. 

The following ensembles of several top-performing models were formed. Some of these ensembles were found to outperform CNN-LSTM-400. In particular, Ensemble 2 attains the accuracies of of 99.8%, 98.4%, 95.8%, 83%.
|          |        |
| :-------------: |:-------------:| 
|Ens-1| LSTM-448, CNN-LSTM-400 |
|Ens-2| LSTM-448, LSTM-424, CNN-LSTM-400|
|Ens-3| LSTM-448, LSTM-424, CNN-LSTM-400, CNN-LSTM-384|
|Ens-4| LSTM-448, LSTM-424|

The performances of the 12 models plus the four ensembles, ranked in terms of the test accuracies of the four individual Hodge numbers are shown in the figure below.

<img width="800px" src="https://github.com/lorrespz/CICY4-Deep-learning-hybrid-recurrent-NNs-main/blob/main/Results_p1_Figures/Train_test_accuracies_all.png"  alt="Test accuracies" />

## Training results (80% data split)
With the enlarged 80\% dataset, only the top three models, CNN-LSTM-400, LSTM-448, LSTM-424, from the first round of training (using 72\% data split) were retrained. Several ensembles of these three models (listed below) were formed as well.

|          |        |
| :-------------: |:-------------:| 
|En-80-1| LSTM-448, LSTM-424|
|Ens-80-2| LSTM-448, CNN-LSTM-400|
|Ens-80-3| LSTM-448, LSTM-424, CNN-LSTM-400|

The accuracy rankings for all models, including the ensembles are shown in the Figure below.

<img width="800px" src="https://github.com/lorrespz/CICY4-Deep-learning-hybrid-recurrent-NNs-main/blob/main/Results_p1_Figures/Test80_accuracies_all.png"  alt="Test accuracies" />


