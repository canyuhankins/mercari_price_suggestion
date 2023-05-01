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

