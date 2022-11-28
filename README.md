# Feedback Price - English Language Learning
Evaluating language knowledge of ELL students from grades 8-12

## Team Members: 
Yanzhen Shen yanzhen4@illinois.edu 

Yilun Chen yilunc3@illinois.edu

Yue Chen yuec12@illinois.edu

## Goal: 
our model aims to evaluate students' essays in the following aspects: cohesion,syntax,vocabulary,phraseology,grammar,conventions. The model will output a score will range from 1.0 to 5.0 in increments of 0.5. 

## Dataset: 
We are given a [dataset](./data/train.csv) in which each row contain an essay written by students and also its cohesion,syntax,vocabulary,phraseology,grammar,conventions scores. Our training data  

## Model:
We used DeBERTa(Decoding-enhanced BERT with disentangled attention) as our pretrained model and then fine-tune it. We chose to use Adam as our optimization algorithm given the large number of parameters in DeBERTa. For sentence embedding, we chose the technique of mean pooling, which averages all the token embeddings in the sentence. To improve accuracy, we also implement pseudo-Labeling. We first train our model on labeled data, and then we use it to proedct the label on the unlabled dataset, then we combine the original train set and the predicted set and retrain the model on this new dataset. 
We use a old dataset of students' essays in previous competition as the dataset for pesudo-Labeling. This dataset is divided into 5 subsets, which means we will repeat above steps for 5 times. 

## Result:
The score is calculated using MCRMSE, mean columnwise root mean squared Error.
Our best score is around 0.47.

## Running Instruction:
You first need to organize our data into test.csv, which contain two columns: text_id and text.
You will use DeBERTa-pseudoLabel_train.ipynb to train our model and obtain parametes. After that, you will use DeBERTa-pseudoLabel_inference.ipynb to make inference, which will store the result in submission.csv. 