# CICY4: Deep learning Hodge numbers with hybrid CNN-RNN and purely recurrent LSTM-based networks

## Introduction

In this work, we explored hybrid CNN-RNN and LSTM-based architectures for learning the Hodge numbers of CICY4. In total, we trained the following 12 models (the training was done fully on Kaggle using the P100 GPU unit). 

The organization of this repo is as follows:
  - The training notebooks for the 12 models are contained in the folders 'Models_CNN-RNN-hybrid' and 'Models_LSTM-based'.
  - The trained models are saved in the folder 'Results_p2_Trained_models'.
  - Some figures from the arXiv paper are stored in the folder 'Resutls_p1_Figures'.

## Data
The data used for the training of all models were prepared in the following Kaggle notebook:
 [url here]
 
The train, validation and test sets can be downloaded from the ouptut of the above notebook. 

## Training results

The performances of the 12 models can be seen the figure below. 

<img width="500px" src="https://github.com/lorrespz/CICY4-Deep-learning-hybrid-recurrent-NNs-main/blob/main/Results_p1_Figures/Train_test_4x_accuracies_all.png" alt="Train and test accuracies of the 12 models considered in this work"/>

## Inference
The saved models, stored in 'Results_p2_Trained_models', can be downloaded and used for inference on the test dataset. The example notebook ' ' demonstrates how to load and use a saved model for inference. 

