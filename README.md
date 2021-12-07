# Agriculture Articles Label Classification

[AICup hosted by AIdea](https://aidea-web.tw/topic/de144f63-cd15-40b8-81e6-82db5636d598?lang=en): "Text labeling and identification of agricultural articles"

In this competition you will be provided agriculture related documents and you are asked to develop a model to label text segments relevant to "plant epidemic".

*This is a competition hosted in Taiwan and the corresponding data and other information will be in mandarin. The details on the site do translate well in chrome if you are interested on reading what the competition is about.
## Data

## Data preprocessing

1. stage 1 data: 80% training data, 20% test data
2. stage 2 data: 80% training data, 20% test data
3. stage 1+2 data: 80% training data, 20% test data

## Fit Model - TF-IDF
### scikit-learn
###### Ref
[【資料分析概念大全｜認識文本分析】給我一段話，我告訴你重點在哪：對文本重點字詞加權的TF-IDF方法](https://medium.com/datamixcontent-lab/%E6%96%87%E6%9C%AC%E5%88%86%E6%9E%90%E5%85%A5%E9%96%80-%E6%A6%82%E5%BF%B5%E7%AF%87-%E7%B5%A6%E6%88%91%E4%B8%80%E6%AE%B5%E8%A9%B1-%E6%88%91%E5%91%8A%E8%A8%B4%E4%BD%A0%E9%87%8D%E9%BB%9E%E5%9C%A8%E5%93%AA-%E5%B0%8D%E6%96%87%E6%9C%AC%E9%87%8D%E9%BB%9E%E5%AD%97%E8%A9%9E%E5%8A%A0%E6%AC%8A%E7%9A%84tf-idf%E6%96%B9%E6%B3%95-f6a2790b4991)
### Articut
### Jieba
###### Ref
[神奇寶貝的 TF-IDF (NLP 講人話系列之一)](https://www.youtube.com/watch?v=rsImqTI51WI)

## Result
|          | scikit-learn | Articut | Jieba |
| -------- | -------- | -------- | -------- |
| stage 1 | Text     | Text     | Text     |
| stage 2 | Text     | Text     | Text     |
| stage 1+2 | Text     | Text     | Text     |
| Overall ||||

###### Ref