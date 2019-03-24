# Report

## Preprocessing

All words have been converted into lower case and punctuations are removed.

### Timesteps

This defines for how many timesteps the RNN is run on any input. <br/>
Since the input sentence is of variable length, so batch training would not be possible on raw data. <br/>
And single sentence "for loop" training would take a lot of time. <br/>

So, I have divided input sentences into fixed window length input based on timestep. <br/>
For example, suppose input is w1 w2 w3 w4 w5 w6 and timestep = 4, so new input would be <br>
X = w1 w2 w3 w4 &nbsp;&nbsp; y = w5 <br/>
X = w2 w3 w4 w5 &nbsp;&nbsp; y = w6 <br/>
X = w3 w4 w5 w6 &nbsp;&nbsp; y = EOS <br/>

In "15CS30039_Ass04.ipynb" timesteps taken is 3. <br/>

## GRU 

A GRU with update gate has been written from scratch. <br/>
A point to note is that both <b>forward propagation</b> and <b>back propagation</b> <br/>
have been written <b>manually from scratch</b>, thus giving a nice implementation of GRU.<br/>

SGD has been used as optimizer.

## Network

The Network is basically a FC layer stacked upon the GRU Unit and a softmax activation applied to the output.
Its forward and back propagation have also been written manually.

## Task 1

### One Hot

A network with hidden layer of 256 units in GRU and it is trained using input batches of batch_size 128 <br/>
and input length = 6683 ( length of vocabulary ).

### Fast Text

A network with hidden layer of 256 units in GRU and it is trained using input batches of batch_size 128 <br/>
and input length = 100 ( Fast Text generated Embeddings).

During the training phase I had to tweak the lr between 1, 0.5, 0.1 and 0.01 at different timesteps to ensure learning.<br/>
Yet the accuracy achieved is not so good. Maybe more epochs would do the trick or using a good optimizer like Adam, <br/>
but the hyperparameter tuning took a looooottt of time.

## Task 2

For both the cases, sentences have been provided in the required format (one_hot or fast_text) till n/2 length <br/>
and then the cell state and next output has been used to further predict the next output. <br/>
This loop continues till further n/2 length sentence has been predicted.

## Accuracy

For both the tasks Accuracy has been calculated over a window of length 5, i.e. even if the actual output matches <br/>
with top 5 predicted words by the model, we are good to go. 
