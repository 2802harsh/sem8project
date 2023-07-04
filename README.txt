DISCLAIMER
==========
Our code is extended on Kothari et al.'s work and code and the folders are still named according to their work.
Any reference to a paper/github was originally in their work and does not belong to us. We have properly cited them in our paper as well.
Our Dataset is present in trajnetplusplusbaselines/DATA_BLOCK/orcadata

HOW TO TRAIN THE MODELS
===================================
$ cd scripts
$ bash setup.sh

NON-BIMODAL ==> (main branch)
________________
Before running the train command ensure to run these:

- For Non-Channelwise Attention Model
cd trajnetplusplusbaselines/
cp trajnetbaselines/lstm_files/lstm_orig.py trajnetbaselines/lstm/lstm.py

- For Channelwise Attention Model
cd trajnetplusplusbaselines/
cp trajnetbaselines/lstm_files/lstm_ca.py trajnetbaselines/lstm/lstm.py

To train, run the following command while in trajnetbaselines/ directory:
$ python -m trajnetbaselines.lstm.trainer --type directional --augment

There are flags for residual LSTM, intent and curvature loss as --residual , --intent and --curvature_loss respectively

So, for example, to train non-channelwise attention model with intent encoding and curvature loss, run the following commands:
$ cd trajnetplusplusbaselines/
$ cp trajnetbaselines/lstm_files/lstm_orig.py trajnetbaselines/lstm/lstm.py
$ python -m trajnetbaselines.lstm.trainer --type directional --augment --intent --curvature_loss

BIMODAL ==> (bimodal branch)
________________

Simply run the train command with optional intent and curvature loss flags.
There is a new flag called --mirror_train which takes an int argument. Imagine total epochs are 25 and mirror_train is set to 10:
In this case 15 epochs will be run on original dataset, 5 on dataset mirrored around X Axis and 5 on dataset mirrored around Y Axis.

For example, to train bimodal model with intent and curvature loss with 10 mirror_train, run the following command:
$ cd trajnetplusplusbaselines/
$ python -m trajnetbaselines.lstm.trainer --type directional --augment --intent --curvature_loss --mirror_train 10

HOW TO GENERATE RESULTS FOR MODELS
==================================
For now, in OUTPUT_BLOCK for all models files are created with the same name.
TO generate predictions and results use the following:

Example for Kothari et al dataset:
$ python -m trajnetbaselines.lstm.trajnet_evaluator --output OUTPUT_BLOCK/trajdata/lstm_directional_None.pkl.epoch25 --path trajdata
