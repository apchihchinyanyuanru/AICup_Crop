# Team-14 - Agriculture Articles Label Classification

## Team Members
- 109078501 Riley Kao 高靖雅 
- 109078510 YuanRu Deng 鄧媛如 
- 109078511 Linda Yeh 葉芝均 
- 109078513 YanYu Fu 傅嬿羽 
- 109062423 Apoorv Saxena 

[![Dataset and all information si Published in Mandarin.](AICup hosted by AIdea)](https://aidea-web.tw/topic/de144f63-cd15-40b8-81e6-82db5636d598)
## A Brief Description
The Data is provided by the open data platform of the Agricultural Committee of the Executive Yuan which was hosted on AIdea Artificial Intelligence Collaboration Platform the main of this project is to aims to supply industrial themes and data, mediate the analyzing potential of industries and academics, and produce the industrial value of AI applications via collaboration between industries, academia, and research.
The project expect us that the data will be labelled and a text recognition analysis would be provided which will tell about the similaritiy.
## Technologies
 - Operating system: Windows
 - Platforms - Anaconda jupyter & Google Colab
 - Programming language: Python 3.8.10
 - Package (library):
    pandas1.2.4 , numpy1.20.2 , jieba0.42.1 , wget3.2 , gensim4.1.2 , collections2.1.0 , nltk3.6.2 , requests 2.25.1 , xgboost1.5.1 , sklearn0.23.2
- Pre-training model:  XgBoost & LightGBM


##  About Training Dataset
The training set data includes:

- rain.zip: A compressed file of txt files with numbers as numbers.
- Keyword.zip: Keyword files of crops, pests and diseases, and control agents, respectively 02crop.list.xlsx, 02pest.list.xlsx and 02chem.list.xlsx.
- TrainLabel.csv: List the Test and Reference article combinations marked as yes.
- submission_example.csv:  as an example for the submission file 
The same criteria where followed by Private Dataset

## Evalutation Criteria 
The text data of the training set are calculated for the results of related annotations, and the accuracy of annotation recognition.

The evaluation method adopts F1-measure (also known as F1-score), and its formula is as follows:
Precision=TP/TP+FP
Recall=TP/TP+FN
F1-measure = 2*(Precision * Recall / (Precision+Recall)
Where:- 
TP: The program calculation judgment is related, and it is correct related
FP: The program calculation judgment is related, but not correct
FN: The program calculation is judged to be okay, but it is really relevant
## Labelling

In the Labelling Combine the keywords from the dictionary of crops, pests, and control agents which were provided by the Agriculure commitee in dataset into 764 features,then  mark them as 1 or 0 according to there occurence, and compute each feature based on whether the features appear in the article provided. For determining similarity, the number of occurrences is employed as the keyword standard. As a result, when the label is removed, an item will have two essential characteristics: a one-dimensional array with a length of 764 that counts the occurrences of keywords (tion: Find compound words (binary words, ternary words)

## Similarity Coutning
- ## AU Score (keywords) {test and reference/ test}


Self Defined Feature it extracts keywords and compare the intersection between the two article, first it's label in binary as per the apperance of the keyword and then the number of time each feature is carried out by using two variablle Fa and Fb where Fa presents - The number of times that Features appear in article A and Fb Presents -  The number of times Features appear in article B. On this a total of 560 combinations among 1383 in the Train Label File provided to us.

- ## Jaccard Similarity

The number of observations in both sets is divided by the number of observations in each set to determine Jaccard similarity. In other words, the size of the intersection divided by the size of the union of two sets yields the Jaccard similarity. Using the intersection(A ∩ B) and unions (A U B)two sets. Here and be can be statae as  the number of occurence of feature in an article and the cumulative number of occurence in that of that keyword.

- ## SimHash Similarity 

It seperate the text of the document filter one each world , then these words are converted into a hash value. then after performing  weighting and dimensionality reduction, the similarity between the articles is calculated. 
It is totally didived into 5 steps:
1. Word segmentation, and determine the keywords in each segment.
2. turn each word into a hash value and mark it with a 64-bit Bit value
3. Weighting, the hash generation result that needs to be weighted according to the frequency of the keyword appearance as  weight
4. Combine, the values of step 3 in the order of appearance and a  sequence string will be formed for each one.
5. the dimensionality reduction of the result calculated in step 4 forms a SimHash sequence value, greater than 0 is recorded as 1, and less than 0 is recorded as 0.

- ## MinHash Algorithm

Minhash Algorithm is somewhat similar to Jaccard Algorithm but it also reduces the dimensionality of the original set this is represented by a hash value  it rearranges the order in each article and finds the similarity set of keyword and thus  reducing the occurrence of Overfitting. 

- ## TF-IDF Cosine Similarity

It uses the SKlearn package TfidfTransformer() and  cosine_similarity() here tf calculate the number of time feature article appear 764 feature article appear and  The IDF of a particular word is obtained by dividing the total number of files by the number of files containing the word and then taking the base quotient to the  base 10 log and Cosine Similarity calculate the similarity of (TF*IDF) between documents. The closer to 1 the higher the similarity of the article, and the closer to -1 the lower the similarity of the article. By doing this in single occurence and cumulative occurence.r.


## Feature Extracting：
- T	- Times of keywords
- A	= Appearance of keywords
- S - 	AU-score
- CTT- 	Cosine Similarity of TF from Times keywords
- CTDT - Cosine Similarity of TF-IDF from Times keywords
- CTA -  Cosine Similarity of TF from Appearance keywords
- CTDA -  Cosine Similarity of TF-IDF from Appearance keywords
- JT -  Jaccard Similarity of Times keywords
- JA -  Jaccard Similarity of Appearance keywords
- SH -  SimHash
- MH -  MinHash
## Classifier
- ## XGBOOST

"Extreme Gradient Boosting" is what XGBoost stands for. XGBoost is a distributed gradient boosting toolkit that has been tuned for efficiency, flexibility, and portability. It uses the Gradient Boosting framework to create Machine Learning algorithms.
Here we have tried four different combination withour adjusting any paramenter and seed set to one and putting sample_weight directly.
 Number | TA | A | S | CTT | CTDT | CTA | CTDA | JT | JA | SH | MH | accuracy | f1-score | 
  :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |  :---: |
 1 | V |  |V  |V  | V | V | V | V |V  |  | V | 0.9984 | 0.8349
2 |  | V |  V| V | V |  V|  V|V  | V |  |V  | 0.9983 | 0.8286
3 | V |  |  V| V |V  |  |  |  |  | V |  V| 0.9982 |0.8218
4 |  |V  |  V|  |  |  V|  V|V  |  |V  |V  |0.9982 | 0.8232

The precision in XGboost where obtained as 0.66872 which is lower when compared to model described below however it's recall rate was high which was 0.84196 when compared with the LighGBM Model.
- ## Light GBM

LightGBM is a tree-based learning algorithm-based gradient boosting framework. It is intended to be dispersed and efficient, and it offers the following benefits: Faster training speed and higher efficiency. , Lower memory usage. , Better accuracy. LightGBM extends the gradient boosting algorithm by adding a type of automatic feature selection as well as focusing on boosting examples with larger gradients. This can result in a dramatic speedup of training and improved predictive performance.

This had been used for  trying six different feature combinations and this all are  using the parameters num_leaves=31, learning_rate=0.05, n_estimators=40.
 Number | TA | A | S | CTT | CTDT | CTA | CTDA | JT | JA | SH | MH | accuracy | f1-score | 
  :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |  :---: |
 1 | V |  |V  |V  | V | V | V | V |V  |  | V | 0.9984 | 0.8168
2 |  | V |  V| V | V |  V|  V|V  | V |  |V  | 0.9984 | 0.8201
3 | V |  |  V| V |V  |  |  |  |  | V |  V| 0.9985 |0.8309
4 |  |V  |  V|  |  |  V|  V|V  |  |V  |V  |0.9983 | 0.8131
5 |  |V  |  V|  |  |  V|  V|V  |  |V  |V  |0.9984 | 0.8180
6 |  |V  |  V|  |  |  V|  V|V  |  |V  |V  |0.9984 | 0.8194



## XGBoost has a tendency of high recall and low precision, while LightGBM has a tendency of high precision and low recall. 

We have decided to combine both models for the above observation to get a better f1-score. Thus both XGBoost(Model 2) and Light GBM(Train 6 Light GBM Model) are trained on models and then for predicting for XGBoost on Model 2 and No. 6 LightGBM model for LightGBM. The dataset then the overlapped record are removed from LightGBM and with XGboost extract some 972 features and then use those to predict from Light GBM. This will increase Recall and precision.

# Final Result
The final result obtained by combining the methodology for LightGBM and XGboost gives the below result in the leaderboard.

| Score | precision | recall|
| :---: | :---: | :---: |
| 0.7770935 | 0.74061 | 0.81735 |