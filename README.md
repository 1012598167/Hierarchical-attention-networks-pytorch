# Profile

Hierarchical Attention Networks for Document Classification

## Datasets

I use AG's News. Here are statistics of datasets I used for experiments . These datasets could be download from [link](https://drive.google.com/drive/u/0/folders/0Bz8a_Dbh9Qhbfll6bVpmNUtUcFdjYmF2SEpmZUZUcVNiMUw1TWN6RDV3a0JHT3kxLVhVR2M)

| Dataset   | Classes | Train samples | Test samples |
| --------- | ------- | ------------- | ------------ |
| AG’s News | 4       | 120 000       | 7 600        |

| Classes  | Train samples |
| -------- | ------------- |
| World    | 30000         |
| Sports   | 30000         |
| Business | 30000         |
| Sci/Tech | 30000         |

I also use [yelp](http://www.yelp.com/dataset_challenge).

| Dataset      | Classes | Train samples | Test samples |
| ------------ | ------- | ------------- | ------------ |
| Yelp reviews | 2       | 560 000       | 38 000       |

| Classes  | Train samples |
| -------- | ------------- |
| Positive | 280000        |
| Negative | 280000        |

## Initialization for embedding layer

In my implementation, **Pytorch** is used to reappear HAN, and most of the HAN repo used a default embedding layer,so I try to load pre-trained work2vec model to enhance the score of the result, which is taken from GLOVE (you could download from [link](https://nlp.stanford.edu/projects/glove/)).

I run experiments with all 4 word2vec files (50d, 100d, 200d and 300d)(d for demension of the work2vec) in AG's News. The 4 embedding methods do almost same good to the classification of AG’s News, which refer to 96%,97%,98%,98% on test set.



# Training and Result

We debug our model on local pycharm and train our model on UAI Train(use terminal because easy to handle conda environment).

The method to attach my code is to visit https://github.com/1012598167/Hierarchical-attention-networks-pytorch (I can't upload big files like models and datasets, so please visit by Ucloud), or if you are the manager of UAI train, you can visit train,test and flask template for app,app design ,our model and so on on the road below. 

(environment: python 3.6.9,conda 4.8.0,pytorch 1.1.0

run: python train/text.py)

![image-20200112213947833](README.assets/image-20200112213947833.png)

![image-20200112213934445](README.assets/image-20200112213934445.png)

![image-20200112213211360](README.assets/image-20200112213211360.png)

The final accuracy on test set is 96%.

![image-20200112221909544](README.assets/image-20200112221909544.png)

The model is in "cloud computing\Hierarchical-attention-networks-pytorch\trained_models\whole_model_han".

It does no good to introduce the basic concept of the model, you can read it on https://www.cs.cmu.edu/~./hovy/papers/16HLT-hierarchical-attention-networks.pdf.

You can download the app demo to try to get your result on your data. See releases on https://github.com/1012598167/Hierarchical-attention-networks-pytorch/releases.

# Detach the payload

I can't arrange my model successfully on UAI Inference because of "Cannot load user model".

![image-20200112215647135](README.assets/image-20200112215647135.png)

So I arrange it on my Aliyun lightweight application server and my friends' for detaching payload. 



47.101.151.73->detach paylaod

![image-20200112220314761](README.assets/image-20200112220314761.png)

It will be useful when we visit the doname or ip, it 301 jumps to the default location of flask.

47.101.151.73 →https://47.101.151.73:5000/api

![image-20200112220414429](README.assets/image-20200112220414429.png)



We use a domain to mask our ip for safety.

noname.asia → 47.101.151.73

![image-20200112220652693](README.assets/image-20200112220652693.png)



We use postman to debug our interface on model.

![image-20200112220736355](README.assets/image-20200112220736355.png)

# App demo

We upload our model on the server, and app gets the model result by http request to flask.

![image-20200112220120788](README.assets/image-20200112220120788.png)

We use android studio to make our app.

###### Workflow

1. create a simulator
2. build UI controls (word and picture)

3. realize click  button
4. Front: Nested Layout——A linear frame is nested within a constrained frame.

(For realization, we call sdk, and use Retrofit2 to realize network communication.)

![image-20200112222802562](README.assets/image-20200112222802562.png)

###### Guide

1. Download app on my github https://github.com/1012598167/Hierarchical-attention-networks-pytorch/releases
2. open the app
3. Input your text (by enter message or choose file)
4. Click button to submit
5. Get the result of the classification prediction

# Innovation Point

We use 4 embedding layer to compare which layer is better.

We use reverse proxy NGINX to detach the payload.

We register a domain for further design, which currently helps hide ip to protect ip privacy and do convenient to connect app.

We design an app demo for user to easily apply our model.

# Pity

As for Yelp, I met cuda runtime error and when we try to use Tensorflow, multiple threads will go failure. So I guess Yelp is so huge for the engine to handle.

![image-20200112211938075](README.assets/image-20200112211938075.png)

![image-20200112212120159](README.assets/image-20200112212120159.png)

I'm not familiar with the visualization method “attentionmap” on pytorch, but on Tensorflow I can make it done. Unfortunately, I can't go through correctly on Tensorflow.

For app design, I will add some dynamic effects further.



# Resource

Program github link : https://github.com/1012598167/Hierarchical-attention-networks-pytorch

In cloud computing.zip:

README.md for readme

model in Hierarchical-attention-networks-pytorch\trained_models

AndroidProjects.zip for Android

the other for model

