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
    - After the initial model was compiled and trained, we had an accuracy of 72.65% with loss of 0.5564
    - After creating a callback and rerunning the model, we had an accuracy of 72.56% with loss of 0.5635
    - I then ran kerastuner using 2-4 layers with 100-200 neurons per layer, with relu, tanh, elu, softsign, softplus, elu, and selu as activation options.  Adam was used as the optimizer, with max epochs set to 100.
        - After running 1231 trials had run over the course of just under 4 hours, the best accuracy achieved was 73.01% with 0.5524 loss using elu as the activator.
    ![KST1](https://user-images.githubusercontent.com/88443672/147682342-2ef42892-53d3-49b2-b665-f686a978cc6e.png)

##### Trial Stage 2
    - After reducing the Organization field to 3 identifiers from 4, and after dropping the Status column, we refit, retransformed, and rescaled our dataframe, before adding 4 additional layers and 200 nodes per layer.  We alternated between the softsign and elu activators in one trial, alongside using a combo of relu and elu for another. The softsign/elu trial produced an accuracy of 72.58% with loss of 0.5577, while the reul/elu trial produced an accuracy of 72.54% with loss of 0.5783.
    - I then ran the kerastuner on the new dataframe for ~4.5 hours across 928 trials.  Relu, softsign, and elu were set as activators, with 3-4 hidden layers, adam as the optimizer, and neurons ranging from 100-200 (increments of 20).  Max epochs was set to 150.
        - The highest accuracy achieved was via using relu as the activator with 4 layers: Accuracy 73.0% with loss of 0.5599
    - Before trying to alter the data one more time, I ran another trial with 8 layers of 300 nodes for 100 epochs with relu as the activator and adam as the optimizer.  The accuracy result was 72.50% with loss of 0.5808.  
              
##### Trial Stage 3
    - With every trial failing to yield 75% accuracy, I then took the initial application_df and dropped both the STATUS and SPECIAL_CONSIDERATIONS columns and then refit, retransformed, and rescaled our dataframe.  From there we ran a model with 4 layers of 500 nodes across 100 epochs.  We tried several different optimizers against the same base model for analysis.
      - Adamax: 72.57% accuracy, 0.5886 loss
      - SGD: 72.65% accuracy, 0.5540 loss
      - Adam: 72.42% accuracy, 0.5863 loss
      - Rmsprop: 71.51% accuracy, 0.6621 loss
      - Nadam: 72.61% accuracy, 0.6159 loss
      - Ftrl: 53.32% accuracy, 0.6911 loss
      
    
## Summary
