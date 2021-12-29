# Neural_Network_Charity_Analysis

## Overview
From Alphabet Soup’s business team, Beks received a CSV containing more than 34,000 organizations that have received funding from Alphabet Soup over the years. Within this dataset are a number of columns that capture metadata about each organization, such as the following:

- EIN and NAME—Identification columns
- APPLICATION_TYPE—Alphabet Soup application type
- AFFILIATION—Affiliated sector of industry
- CLASSIFICATION—Government organization classification
- USE_CASE—Use case for funding
- ORGANIZATION—Organization type
- STATUS—Active status
- INCOME_AMT—Income classification
- SPECIAL_CONSIDERATIONS—Special consideration for application
- ASK_AMT—Funding amount requested
- IS_SUCCESSFUL—Was the money used effectively
  
With our module 19 content, covering machine learning and neural networks, we use the features in the provided dataset to help Beks create a binary classifier that is capable of predicting whether applicants will be successful if funded by Alphabet Soup.

## Results

#### Deliverable 1
Using your knowledge of Pandas and the Scikit-Learn’s StandardScaler(), you’ll need to preprocess the dataset in order to compile, train, and evaluate the neural network model later in Deliverable 2.

##### Data Preprocessing

  -What variable(s) are considered the target(s) for your model?
    IS_SUCCESSFUL is the target variable field.  The goal is to predict whether applicants will be successful if funded by Alphabet Soup.
    
  -What variable(s) are considered to be the features for your model?
  
  -What variable(s) are neither targets nor features, and should be removed from the input data?
  
    EIN and NAME are both identification columns, which are neither target or feature elements of the model.  We remove both columns from our dataframe prior fitting, transforming, or scaling with the below code. 
    
   ![D4Q3](https://user-images.githubusercontent.com/88443672/147592000-3c51e1b4-1674-4867-a04f-b8daf7205061.png)

#### Deliverable 2 & 3
Using your knowledge of TensorFlow, you’ll design a neural network, or deep learning model, to create a binary classification model that can predict if an Alphabet Soup–funded organization will be successful based on the features in the dataset. You’ll need to think about how many inputs there are before determining the number of neurons and layers in your model. Once you’ve completed that step, you’ll compile, train, and evaluate your binary classification model to calculate the model’s loss and accuracy.

Using your knowledge of TensorFlow, optimize your model in order to achieve a target predictive accuracy higher than 75%. If you can't achieve an accuracy higher than 75%, you'll need to make at least three attempts to do so.

##### Compiling, Training, and Evaluating the Model

  -How many neurons, layers, and activation functions did you select for your neural network model, and why?
  
  -Were you able to achieve the target model performance?
  
    No.  
    
  -What steps did you take to try and increase model performance?
    
##### Trial Stage 1
    - After the initial model was compiled and trained, we had an accuracy of 72.43% with loss of 0.5576
    - After creating a callback and rerunning the model, we had an accuracy of 72.63% with loss of 0.5591
    - After running kerastuner for 138 trials, the best accuracy achieved was 72.93% with loss of 0.5507
    
##### Trial Stage 2
    - After reducing the Organization field to 3 identifiers from 4, and after dropping the Status column, we refit, retransformed, and rescaled our dataframe, before adding 4 additional layers and 1000 nodes per layer.  We alternated between the tanh and relu functions between layers before using sigmoid as the output layer, with adamax as the optimizer.  The model results were 72.62% accuracy and 0.5565 loss.
    - After running the kerastuner on the new dataframe for 2 hours and 26 minutes with 812 trials, the best accuracy achielved was 73.01% with loss of 0.5507.
    - After setting the activation functions to relu, relu, tanh, relu, relu, tanh and rerunning the model on the reformulated/rescaled data, we achieved an accuracy of 72.62% with loss of 0.5565.
    - After running the kerastuner 504 trials over nearly 10 hours on the new model with the reformulated/rescaled data, and altering the kerastuner options to include 9 different activator choices, and 1-1000 nodes, the best accuracy achieved was 72.99%.
    
##### Trial Stage 3
    - We then took the initial application_df and dropped both the STATUS and SPECIAL_CONSIDERATIONS columns and then refit, retransformed, and rescaled our dataframe.  From there we ran a model with 4 layers of 500 nodes with relu and tahn alternating, and with sigmoid as the output layer.  We ran several optimizers against the same base for analysis.
      - Adamax: 72.618% accuracy, 0.5598 loss
      - SGD: 72.606% accuracy, 0.5521 loss
      - Adam: 72.68% accuracy, 0.5589 loss
      - Rmsprop: 72.58% accuracy, 0.5614 loss
      - Nadam: 72.37% accuracy, 0.5598 loss
      - Ftrl: 53.32% accuracy, 0.6911 loss
      
    
## Summary
