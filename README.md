# Mercari Price Suggestion

This repository holds an attempt to provide price suggestion based on the user inputted text descriptions of their products. https://www.kaggle.com/competitions/mercari-price-suggestion-challenge/overview

## Overview
The task is to build an algorithm that automatically suggests the right product prices, mainly based on the user-inputted text descriptions of their products, along with the product details like brand name, category name, item condition and more. The evaluation metric is based on the Root Mean Squared Logarithmic Error (RMSLE).

## Data
* Data:
  * Type: 
    * Input: The dataset comes in zip file. After unzip, the train and test file is in tab separated values (tsv) format.
    * Size: zip - 430.52 MB. Unzip - ~1.2 GB
    * The instances include about around 1.5M data points for training data set, and around 700K data points for testing data set. There is also a stage 2 data set which will contain about 3.5M rows

#### Data Preprocessing / Clean-up

* Dealing with missing values/NaN
  * The category_name variable have 6327 missing values.
  * The brand_name variable have 632682 missing values.
  * The item_description have 4 missing values.
  * Instead of dropping the missing values or fill in them with mean/median/mode, I fill in "none" and hoping there will be some useful information in the item_description where I can fill in the gap. 

#### Data visualization
* Dealing with category_name variable column
  * create sub-categories for different category
  * ![image](https://user-images.githubusercontent.com/89665013/226462934-0b9660bc-1b38-48d5-99e1-6c93055594e4.png)
  * According to the plot, items in the "Women" categort is the No.1 category which contains about 45% of the whole data set.
  * sub-category 1 
  *![image](https://user-images.githubusercontent.com/89665013/227037527-e9a8a3a9-ebc4-4bf3-bd00-40402bc77df8.png)

* Dealing with item_description column
  * text mining task
  * Convert uppercase into lowercase because uppercase != lowercase
  * Remove punctuation by using the string library.
  * Remove filling/stop words in the column.

* Price distribution
   ![image](https://user-images.githubusercontent.com/89665013/235506074-4a51dcf7-7183-469d-8d66-34022fb5432b.png)
  
* item condition distribution
  ![image](https://user-images.githubusercontent.com/89665013/235507825-1e096d39-a1fd-4e94-9517-8a941ac61dbf.png)

* Word cloud

![image](https://user-images.githubusercontent.com/89665013/235523903-f15b3128-54f4-4be6-be62-e5b3367f2fe8.png)

### Problem Formulation
- Input: different features for the item for sale, the most importand variable is the item descrition, because it provides information about the item.
- Output: predicting sales prive based on the input
- Model used:
  - Ridge
  - LGBM
  
### Training
  - The data preprocessing/data cleaning part pretty time consuming and need lots of careful consideration before fit into the model, also the model selection needs some fitting and playing around.
  - Used LDA as the model
  
### Performance Comparison
- The metric to evaluate the model is Root Mean Squared Logarithmic Error (RMSLE):
![image](https://user-images.githubusercontent.com/89665013/235526587-25cfa00d-cb9a-41d8-a404-4b8037e5b303.png)

- Ridge: 0.60
- LGBM: 0.48
- The r-square score for ridge regression is higher, meaning the it is a better model to fit for the dataset, therefore I'll use ridge regression as the final prediction model.

## Conclusions
* The ridge regression model is a better model to use out of the 2, since the r-square score is higher then LGBM model. Below is the prediction for the test dataset based off the train dataset:
* ![image](https://user-images.githubusercontent.com/89665013/236702724-28868faf-53ed-436b-b7ef-d58dac2d644d.png)
* I spent about 60~70% of my work doing data cleaning/preprocessing, because over half of the variables are not numeric value, they are more of the text data, so convert these text data into useful information took me some time. Overall, it was a interesting project to work on, it really gives me some good exposure dealing with text data, and I used some NLP such as the natural language tool kit (nltk) package to clean the text, and also learned about tokenization, stemming, lemmazation which is essential for text data. 


### Future Work

* I would like to sure different model such as other regression model like lasso regression, and XGboosting. I also would like do perform different data cleaning techniques on these text data, especially the 'item description' column, so see if the resule is going to be better than what I currently got.
* Althought this project covered some basics about NLP, this project didn't really touch too much about NLP, so I would like to find other project that is more relevant in using NLP, maybe sentimental analysis would be a good next step for me.
  
## How to reproduce results

* Set up the enviroment and install nesscessary packages: numpy, pandas, matplotlib, sklearn, nltk, ridge, lightgbm, CountVectorizer, TfidfVectorizer, LabelBinarizer, vstack, hstack, csr_matrix, LatentDirichletAllocation
* Data cleaning:
 * Basic cleaning: 
   - excluding filling/stop words in the description column
   - lower case everything
   - remove punctuation, digits
 * Prepare the text in these steps before put it into the model:
   - tokenization - splitting text into words
   - stemming - removing the ending of the word (getting the root word)
   - lemmazation - similar to stemming, but instead of cutting the ending of the word, this consider the original word meaning, more expensive
   - Use CountVectorizer to count word frequency.
   - Use Label Binarizer to encode different labels into numeric values.
   - Combine everything into sparse matrix.
 * Model selection:
   - Use the r-sqaured value to determine which model fits better
 * Apply the model.
 
## Citations

 * https://www.kaggle.com/competitions/mercari-price-suggestion-challenge/overview
 * https://www.kaggle.com/code/thykhuely/mercari-interactive-eda-topic-modelling
 * https://www.kaggle.com/code/dogdriip/mercari-vectorizer-labelbinarizer-lgbmregressor#Target's-distribution

 
 
 
