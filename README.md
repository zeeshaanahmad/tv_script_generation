# TV Script Generation

This project builds an deep learning model to generate a [Seinfeld](https://en.wikipedia.org/wiki/Seinfeld) TV script using RNNs.  It is trained on part of the [Seinfeld dataset](https://www.kaggle.com/thec03u5/seinfeld-chronicles#scripts.csv) of scripts from 9 seasons.  The Neural Network generates a new, "fake" TV script, based on patterns it recognizes in this training data.

## Get the Data

The data is already provided in `./data/Seinfeld_Scripts.txt` and you're encouraged to open that file and look at the text. 

First we load the data and preprocess it. Please refer to `dlnd_tv_script_generation.ipynb` in thr project root for more information.

# Generated Script
    jerry: throwing me up.

    jerry:(to george) you know, i don't know. i don't want to hear that. i think i am quitting.

    kramer: yeah! i don't know. i mean, i don't think i should bid on that.

    jerry:(to jerry) you see what?

    george: oh, i was in charge to root tissue...

    george: oh, yeah.

    jerry:(to elaine) i don't know. i don't think we should just come out and get out of here.(jerry presses his hand to leave.) what do you mean?

    elaine: you don't want to go.

    george: i think i got that mustard stain in the lobby drawer.

    jerry:(to jerry) hey, hey. you got any matches?! i thought i saw you.

    elaine: you mean?!

    elaine: i got a lot more responsibility to me!!

    jerry: what do you mean?

    elaine: what do you think? i didn't hear it.

    newman: i don't want it.

    jerry:(pointing) oh, you know, the faster landed in, it was a 5th avenue patient, and i got a memo- a memo- finish amsterdam and queen suffered construction sites.

    jerry: what are you doing here?

    george: i am. i defy you to get a better meal than you? i got the goods on the coffee table book?

    elaine: i was just gonna tell ya, i don't know.

    jerry: well, you know what, i urge a little girl. i could be ostracized.

    jerry: i think you may be trusted.

    jerry: i think i am going to be honest with you.

    jerry: i know.

    kramer:(to george) you know, i really don't have to get a better meal.

    george: i don't think so.

    jerry: what do you mean," scent of"

# Hyper parameters

### sequence_length
Since average number of words per dialog in the training data is around 6, I chose 12 just to double the average length of sequences model sees.

### batch_size
I started with batch_size 200 so that the model sees enough examples in each epoch.

### num_epochs
I chose to start with 20 iterations. After the training I found that first 5 epochs were good enough to bring the loss lower than 3.5. In next 15 epochs although it went down to 2.7 at some points but the learning was quite slow. I think trying to train with different hyper parameters might reveal the exact number of epochs that are sufficient for training.

### learning_rate
First I tried with 0.01 but the loss decreased to only 4.0 in 20 epochs and remained oscillating in numbers higher than 4.0. Then I decided to lower it to 0.001 which significantly improved the learning and loss started dropping quickly in the first few epochs.

### embedding_dim
Initially I tried with 300 but couldn't find good results. I increased it to 400 which showed good results.

### hidden_dim
I just wanted to experiment to see what happens if both embedding dimension and hidden dimesions are same. It resulted in a good decrease in loss so I went ahead with it. In my previous iterations, I tried numbers like 128 and 256.

### n_layers
I kept the 2 layers for LSTM for all the training iterations since 2-3 layers has been recommended to be a good start.

Overall the model took 2 hrs to train. 