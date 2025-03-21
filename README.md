# CICY4: Deep learning Hodge numbers with hybrid CNN-RNN and purely recurrent LSTM-based networks

This is the GitHub repo for: https://arxiv.org/abs/2405.17406 (also for the published work 
https://doi.org/10.1016/j.nuclphysb.2025.11683)

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

The following ensembles of several top-performing models were formed and listed below. 
|          |        |
| :-------------: |:-------------:| 
|Ens-1| LSTM-448, CNN-LSTM-400 |
|Ens-2| LSTM-448, LSTM-424, CNN-LSTM-400|
|Ens-3| LSTM-448, LSTM-424, CNN-LSTM-400, CNN-LSTM-384|
|Ens-4| LSTM-448, LSTM-424|

The best ensemble is Ens-2 with the achieved accuracies of 99.80%, 98.40%, 95.80%, 83.02%.

The performances of the 12 models plus the four ensembles, ranked in terms of the test accuracies of the four individual Hodge numbers are shown in the figure below.

<img width="800px" src="https://github.com/lorrespz/CICY4-Deep-learning-hybrid-recurrent-NNs-main/blob/main/Results_p1_Figures/Train_test_accuracies_all.png"  alt="Test accuracies" />

## Training results (5-fold CV)
This is an experiment in which a single model (LSTM-448) was chosen to undergo the 5-fold cross validation (CV) training (resulting in 5 new models named LSTM-448-f0, LSTM-448-f1, LSTM-448-f2, LSTM-448-f3, LSTM-448-f4). Out of the 5 models,  a new top-performing model, LSTM-448-f1, yielding high accuracies when evaluated on both the test sets of the 72% and 80% datasets was found. The following ensembles were formed using these 5 LSTM-448 models and the models CNN-LSTM-400, LSTM-448 trained on the 72% dataset. 

|          |        |
| :-------------: |:-------------:| 
|LSTM-448-5f| LSTM-448-f0, LSTM-448-f1, LSTM-448-f2, LSTM-448-f3, LSTM-448-f4|
|LSTM-448-f0f1f4| LSTM-448-f0, LSTM-448-f1, LSTM-448-f4|
|LSTM-448-f1f4|  LSTM-448-f1, LSTM-448-f4|
|Ens-f1f4-CL400|STM-448-f1, LSTM-448-f4, CNN-LSTM-400 |
|Ens-0f1f4-CL400|LSTM-448-f1, LSTM-448-f4, LSTM-448, CNN-LSTM-400|

The performances (evaluated on the test set of the 72% dataset) of the 5 LSTM-448 models from the 5-fold CV training, the ensembles in the Table above, and 4 top performing models (CNN-LSTM-400, Ens-1, Ens-2, Ens-3) from the first round of training are shown in the figure below. The best performing model is LSTM-448-f1 (99.81%, 98.29%, 95.35%, 81.98%), and the best ensemble is Ens-0f1f4-CL400 (99.84%, 98.71%, 96.26%, 85.03%).

<img width="800px" src="https://github.com/lorrespz/CICY4-Deep-learning-hybrid-recurrent-NNs-main/blob/main/Results_p1_Figures/Test_CV_accuracies_all.png"  alt="TestCV accuracies" />

## Training results (80% data split)
With the enlarged 80\% dataset, only the top three models, CNN-LSTM-400, LSTM-448, LSTM-424, from the first round of training (using 72\% data split) were retrained. Several ensembles of these three models (listed below) were formed as well. 

|          |        |
| :-------------: |:-------------:| 
|En-80-1| LSTM-448, LSTM-424|
|Ens-80-2| LSTM-448, CNN-LSTM-400|
|Ens-80-3| LSTM-448, LSTM-424, CNN-LSTM-400|
|Ens-80-4|LSTM-424, LSTM-448, LSTM-448-f1, CNN-LSTM-400|
|Ens-80-5|LSTM-424, LSTM-448, LSTM-448-f1|

The best performing model is LSTM-448 (99.85%, 98.66%, 96.26%, 84.77%), and the best ensemble is Ens-80-4 (99.90%, 99.03%, 97.07%87.34%).

The accuracy rankings for all models, including the ensembles are shown in the Figure below.
<img width="750px" src="https://github.com/lorrespz/CICY4-Deep-learning-hybrid-recurrent-NNs-main/blob/main/Results_p1_Figures/Test80_accuracies_all.png"  alt="Test 80pc accuracies" />

## Structure of the repository

The organization of this repo is as follows:
  - The training notebooks for the 12 models are contained in the folders 'Models_CNN-RNN-hybrid' and 'Models_LSTM-based'.
  - The trained models are saved in the folder 'Results_p2_Trained_models'.
  - Some figures from the arXiv paper are stored in the folder 'Resutls_p1_Figures'.
  - The folder 'data-results-processing' contains the inference notebook ('cicy4-training-results-all-models.ipynb') as well as the notebook (cicy4-data-training-curves-processing.ipynb) for plotting the training curves in the paper. The notebook 'cicy4-training-results-all-models.ipynb' is also available on Kaggle (https://www.kaggle.com/code/lorresprz/cicy4-training-results-inference-all-models) and linked to the Kaggle dataset (https://www.kaggle.com/datasets/lorresprz/calabi-yau-cicy-4-folds).


