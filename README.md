# News-classfication-using-LSTM-
Real or fake news classification with the use of different techniques under NLP

## Introduction:

> In todays world of digital era, information of news is spreading from one corner of world to another at faster pace like never before and that too from various sources. The authenticity of the news becomes sometimes doubtful in such a huge inflow of information.

> Social media companies have hired thousand of employees to prevent spread of fake news however when spread is happening at such a high scale, its almost not practical to verify and correct each and every news manually and there comes a use of AI. Researchers have started training AI application to automatically detect fake news.

## Problem Statement:

> It seems AI is better at creating fake news than identifying it. However lets assume that one of the social media companies want to build AI model to pro-actively detect the fake news and they have already have a dataset of such fake and real newspapers. Although mainly fake news is linked to specific sources, there are chances that fake news are the ones which are simulated or crowdsourced by humans.

> The objective here is that if we have a dataset of approx 45000 news classified into real and fake, can we build AI model that will help us to identify any possible fake news  coming on the way. The target feature of the data set has two labels as below:
      Class Labels: true fake
      
## Data Descriptions:

> Dataset has 44898 observations and 4 input features: title, text, subject and date. Target variable is ‘target’ and two values: true and fake.

> PoliticsNews and WorldNews are the subject classes having all fake news, rest subjects looks to have all True news

  ![image](https://user-images.githubusercontent.com/49444353/127814560-73e4f932-9ff4-4387-bee0-f2fdc4a7d433.png)
  
> No NaN or missing value found in all dataset 

> Both True and Fake classes of Target variable appears to have mostly equal data points 

![image](https://user-images.githubusercontent.com/49444353/127814717-43754981-39d6-415f-8da2-6aeb477e9eca.png)

> After label encoding, 'fake' and 'true' labels are converted to '0' and '1' values respectively.


## Data pre-processing:

> We will keep only 'text' column as input variable for building RNN/LSTM model. 
> Text column will be pre-processed as:

    > Removing all numbers, special characters and only keep alphabets, then converting the words into lower case.  
  	
    > Removing all stopwords like a, an, the, haven’t, couldn’t etc.  
  	
    > One-hot encoding is then applied to convert words into numbers  
  	
    > Further, padding is applied to one-hot encoded data with max length as 500.  

> After padding, the size of input variable becomes 44898, 500
> From this data, only 30K rows will be used for training, 10K for validation and rest to be used for testing purpose 


## Model Architecture:

> We will use sequential model and train embedding layer through model training. Embedding size will be 50 and it will be first layer of Sequential model. So dimension of embedding layer – 10000, 50, 500 (10000 being vocab size or max number, 500 being timestep size) <br> 

> RNN or LSTM layer of 128 will process output of embedding layer output (200, 500, 50) and output further to give 200 vectors of 128 units. <br> 

> Output of SimpleRRN or LSTM will further undergo dropout layer of 0.5 for overfitting if any and then final dense layer with activation function as ‘sigmoid’.<br>

> Model further will be compiled with optimizer as ‘Adam’ and loss as ‘binary_crossentropy’ <br>

> We tried both SimpleRRN and LSTM networks for model building keeping batch size as 200 and epochs as 5 for training.<br>

> While training, model will take an input of 200, 500 in each epoch multiple times i.e. 150 and final output will be 1 unit with a probability value from 0 to 1 for binary classification purpose. Validation accuracy resulted around 98% in both networks <br>

## Model Evaluation:

![image](https://user-images.githubusercontent.com/49444353/127815605-56a3c2ae-1b23-4710-9394-bbc80e6c7018.png)

> Training and validation accuracy both are increasing with every epoch and resulting around 98%. <br>
> Although models are not much complex, reason of increased accuracy might be because data is too simple for model to train. As we could see earlier, its only two news subjects for which fake news observations are present. 

## Model Predictions:

> Model is further tested on the test data test and predictions are sent to CSV file ‘submission.csv’ file <br> 
> Here are the predictions for first few rows of the test dataset. Value of ‘1’ means True News. The same is found in original test data set. <br>

![image](https://user-images.githubusercontent.com/49444353/127823029-750c619d-db9e-404b-9682-b0868227797a.png)




  






 



