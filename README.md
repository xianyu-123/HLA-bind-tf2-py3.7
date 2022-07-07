HLA-CNN and HLA-Vec
=========================

__Ourwork__:Make the program run in the environment of tensorflow2.2 and python3.7, modify the incompatible API interface, and change the necessary environment parameters.

if you use tensorflow2.2,you need to modify keras.optimizer.py line 1, change import tensorflow as tf to import tensorflow.compat.v1 as tf and add tf.disable_v2_behavior(); if notes scipy error, you may need install scipy==1.2.0; if notes tensorflow_contrib not found in tensorboard, you need change tensorflow_contrib to from tensorboard.plugins import projector. etc

recommend:use tensorflow==1.14

__ourcompany__: [neoantigen](https://www.neoantigen.cn/)

__Author__: ysvang@uci.edu

__Usage:__ python main.py config.ini 

__Overview:__ HLA-CNN tool can be used to make binding prediction on HLA Class I peptides
based on convolutional neural networks and a distributed representation of amino acids, HLA-Vec. 
At a high level, the tool consists of (a) an unsupervised, distributed vector representation learner for
raw peptide sequence, (b) a training mode to learn weights to the classifier, (c) an evaluation mode 
to calculate Spearman's rank correlation coefficient (SRCC) and are under the receiver operating characteristic
curve (AUC), (d) an inference mode to make prediction new peptides.

__Pipeline__: The pipeline is specified in the config.ini file. A config file is required to specify the 
parameters used in the various learning algorithm as well as files and directories.
- _HLA-Vec_: learns an unsupervised, distributed vector representation based on raw peptide sequence
- _train_: The classifier is trained from a set of labeled data (reference Supplementary Information from doi:10.1038/srep32115)
- _evaluate_: Using a labeled test set, the trained models are evaluated in terms of SRCC and AUC.
- _inference_: Given a set of new peptides, predictions are inferred and scores are written out to a result file.

__Notes:__
- Test files are obtained from and currently in the format given by IEDB. http://tools.iedb.org/auto_bench/mhci/weekly/
- Although all columns in the test files are not required, the minimum ones required by the code are Allele, Measurement_type, Peptide_seq,
and Measurement_value (not required if performing inference mode).

__License:__ This project is licensed under the MIT License - see the LICENSE.md file for details.

__Requirements__:

- gensim==2.3.0
- Keras==2.0.6
- numpy==1.21.6
- pandas==1.3.5
- scikit_learn==1.1.1
- scipy==1.4.1
- tensorflow==2.2

__Reference__:
Vang, Y. S. and Xie, X. (2017) HLA class I binding prediction via convolutional neural networks. https://doi.org/10.1093/bioinformatics/btx264
