
# Web and Social Media Analytics

## Problem Statement:
### Business Understanding

With a growing trend towards digitisation and prevalence of mobile phones and internet access, more consumers have an online presence and their opinions hold a good value for any product-based company, especially so for the B2C businesses. The industries are trying to fine-tune their strategies to suit the consumer needs, as the consumers leave some hints of their choices during their online presence. 

 

In this capstone project, we will be solving a problem in the mobile phone industry of the US, one of the major smartphones markets in the world. 

Suppose your customer is a mobile manufacturer based in the US, which entered the market three years ago. As they are a new entrant in the sector, they want to understand their competitors and preferences of their users so that they can design their strategies accordingly. They want to tweak the marketing strategies to add more value to their brand, provide features to customers that add the most value, and close the demand-supply gap. Their objective is to increase the market share as well as the brand value.

 





## Data Background

I've already provided with the Google drive link in the repository.
Here we will understand the features of the dataset.

1. **Phone data as the .csv file**: Contains the consumer activity information:

**overall**:  Overall rating for the particular product given by the user

**verified**: Whether the user is a verified reviewer or not

**reviewerID**: ID of the reviewer, e.g. A2SUAM1J3GNN3B

**asin**:  ID of the product, e.g. 0000013714.

**ASIN** stands for Amazon Standard Identification Number. It is a 10-character alphanumeric unique identifier that is assigned by Amazon.com and its partners. It is primarily used for product-identification within their product catalogue

**style**: Information about physical features like colour

**reviewerName**: Name of the reviewer

**reviewText**: Review provided by the reviewer

**summary**: Summary of the review

**unixReviewTime**: Time of the review (Unix time)

**vote**: Upvotes or Downvotes of the review. A review with more upvotes can hold a higher significance

**image**: Image of type .png or .jpg, etc provided by the reviewer

**review_sentiment**: Pre-labelled sentiment of the review which can be either positive or negative. The labels will not be available for the real-time data, and a model needs to be built for such classification

2. **Phone metadata as zipped.json file**: This data contains the product information and is independent of the consumer/reviewer activity and includes description, price, sales-rank, brand info, and co-purchasing links etc.

**Category**:  List of categories the product belongs to, e.g., ['Cell Phones & Accessories', 'Cell Phones']

**tech1**:  The specifications and technology of the product, e.g., Phablet ( a hybrid of phone and a tablet)

**tech2**:  Contains data similar to that of tech1

**description**: A short description of the product

**fit**: A column which has no values for a mobile phone dataset 

**title**: Name of the product

**also_buy**: Product IDs of the products that are generally bought along with the particular product

**image**: Image of the product by the supplier

**brand**: Brand of the product

**feature**: Features of the product including specifications such as the 4G/3G, language, apps supported etc.

**rank**: Ranking of the product as given by Amazon based on various parameters in different segments. It is a metric that explains the relationship among products within a category based on their sales performance. Sales rank is updated hourly, it can range from 1 to over 1 million, and is influenced by seasonality, and its algorithm remains unrevealed.

**also_view**: Products which are also viewed while searching for this product.

**details**: Contains details from a delivery point of view such as product dimension, shipping weight etc.

**main_cat**: The main category to which the product belongs, e.g., “All Electronics”

**similar_item**: Related products.

**price**: Price of the product.

**asin**: ID of the product, e.g., 0000031852

3. **pos_words.txt** : This is a text file that contains a corpus of positive words. This file can help you in extracting some features out of the review text. There are multiple sources available online that gives you a corpus of positive negative words. You can also customise it based on your application.

4. **neg_words.txt** : Similar to the corpus of positive words, this text file contains a list of words that can be a part of the negative reviews of the users.

5. **Stop_words_long.txt**: In the previous modules, you had learnt to remove stopwords using the NLTK library. One drawback of it is, the negation words like nor, not, never are considered as stopwords. Remove those words may not affect a spam/ham classification, but it will definitely affect the sentiment classification. Hence, we have provided you with a customised list of stop words which you can use it for the analysis.
## Solution Pipeline

The final solution can be looked to be divided into two parts:

1. **Part 1**: Deriving the business insights that are useful for product development and marketing.
2. **Part 2**: Creating a sentiment classification engine.


### Step:1 Data Pre-Processing
- You are provided with two data files - Data and phone metadata. You need to look at a few entries of the data and the columns present. This will give you an idea of the attributes present in the data set and the kind of analysis that can be done with it. 

- Exploratory Data Analysis - To be able to proceed towards analysing the data, you will have to source, clean and understand the data both quantitatively and qualitatively. This involves the following steps:

- Sourcing the data - Since you have been already provided with the data files, this step only involves arranging the data into a proper format. You have the data as a .csv file, which can be directly read into a pandas data frame. But, the metadata is a zipped json file. You will need to unzip the data and load it into a dataframe.

- Cleaning the data by handling the missing values, removing duplicates, standardising, filtering, etc. It is possible that the data may have some missing values, or they can be in the wrong format. 
    - For example, Asins are a unique identification number for each product in Amazon. Metadata contains duplicate Asins, so you will have to remove the duplicates, review text columns that cannot have blank entries, etc.

- 'Category' column of the metadata contains a list for each entry. The second element of the list tells you whether the entry is a Cell Phone or an accessory. You can extract only the entries for the Cell Phones and work with it for this project.

- Deriving new features that can be helpful for the analysis. For example, you can make use of the column ‘also viewed’ to extract some features and get an idea of the competitor brands for each of the mobile phone brands. Converting the unixReview time to normal time stamp is another example.

- Choosing the columns that can be useful to the analysis from phone data and metadata, and merging them together based on some primary key value will open up more possibilities for the insights.

### Step 2: Text analytics

This step involves the following:

- Cleaning the review text using the lexical processing methods and creating some useful word corpus that will be useful for the analysis. For example, you can create the most talked-about phone features in positive and negative reviews, visualise it and make it part of your tableau dashboard. You can further explore the insights which you can extract from this cleaned text.

- Using stemming/lemmatization is not compulsory but a good to have text pre-processing step. It will improve model performance in the latter part of the solution.

- Converting the cleaned text into a numeric format (bag-of-words or tf-idf) so that it can be fed into the machine learning models.

- You can make use of the positive and negative words corpuses provided to extract some features out of the review text and use it for visualisation.

### Step 3: Visualisation and storytelling

1. In this step, you use the features that you had extracted from step 1 and step 2, identify the right KPIs and use them to create a Tableau dashboard and build a story around it.  One assumption here is, the popularity of the brand is proportional to the number of reviews. While building the story, remember the end-objective of this exercise is that the company should be able to make crisp and relevant decisions for developing the product and marketing strategies. Some of the relevant visualisations that were mentioned in the video are,
     - Market share of competitors.
     - Brand loyalty by comparing the alternate brands the consumers are considering before buying a particular brand.
     - Important phone characteristics that resulted in positive or negative sentiments. You may find this link useful for this visualisation.

### Step 4: Building a sentiment classification engine

Currently, you are provided with positive and negative labels for each review. In reality, such labels are generated manually, and then a model is trained. Once the base model is ready, it can be used for the real-time analysis of the reviews and helps in faster decision making. Naive Bayes is one of the widely used text classification algorithms which is used for sentiment analysis. You already have the textual data converted to numeric features from step 2, or you can do the same in this step and proceed with model building. 