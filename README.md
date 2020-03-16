# Style-Conditioned Music Generation
 Code repo to reproduce the main experiments presented in ICME 2020 paper "Style-Conditioned Music Generation".

## Description
This work presents a modification to the vanilla formulation of a Variational Auto-Encoder (VAE) that allows user to condition on the compositional style of the music generated by the model. In our experiments, we trained our model on Bach chorales (JSB) and western folk tunes (NMD). At generation time, the user can specify the model to generate music in the style of Bach or folk tunes. The datasets used in the experiment can be downloaded at [JSB](http://kern.humdrum.org/search?s=t&keyword=Bach%20Johann&fbclid=IwAR39fsc8gUWjN6eYAUkewldNkeV499lX0Ew6VP8Nrrd_T1T7plaIIIb5nFQ) and [NMD](http://www-etud.iro.umontreal.ca/~boulanni/icml2012).


## Dependencies
- Python 3.6.8
- tensorflow(gpu) 1.15.0
- tensorflow-probability 0.8.0
- pretty-midi 0.2.8  

Tested on Ubuntu 16.04.

## Running the code
### Setup
Check _dataset.py_ in the dataset folder and put in the correct folder path for the MIDI files. Change the train/test split ratio as you desire. The output should be train/test pickle files for each style, i.e. with 2 styles, you should have 4 pickle files, train/test for style 1 and train/test for style 2.

### Training
Check _train.sh_ to tune the hyperparameters. For hyperparameters not in _train.sh_, please look into _model.py_. Those hyperparameters that are not in _train.sh_ are found to be have little impact on model's learning.

Description for hyperparameters (and the values used in the paper) and options in _train.sh_:
```
save_path=vae_model                       # model save path
train_set="jsb_train.pkl nmd_train.pkl"   # training dataset path, separate style with space
test_set="jsb_test.pkl nmd_test.pkl"      # testing dataset path, make sure style sequence is same as above
epoch=400                                 # training epoch
enc_rnn=hyperlstm                         # encoder RNN: lstm, hyperlstm
enc_rnn_dim=512                           # encoder RNN dimension
enc_rnn_layer=1                           # number of encoder RNN layers
enc_hyper_unit=256                        # number of hyper units if hyperlstm is chosen
enc_dropout=0.5                           # encoder RNN dropout rate
dec_rnn=hyperlstm                         # decoder RNN: lstm, hyperlstm
dec_rnn_dim=512                           # decoder RNN dimension
dec_hyper_unit=256                        # number of hyper units if hyperlstm is chosen
dec_dropout=0.2                           # decoder RNN dropout rate
dec_rnn_layer=1                           # number of decoder RNN layers
attention=0                               # dimension for attention units for decoder self-attention (0: disable)
cont_dim=120                              # latent space size for z_c 
cat_dim=2                                 # number of styles (categorical dimension)
gumbel=0.02                               # Gumbel softmax temperature
style_embed_dim=80                        # dimension for each style embeddings in z_s
mu_force=1.3                              # beta in [mu_forcing](https://arxiv.org/abs/1905.10072)
batch_size=64                             # batch size
```

### Generating music
Run _generate.sh_ to generate music. Options are described as follows.
```

```
