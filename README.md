# Named-Entity-Recognition
Named entity recognition using bidirectional LSTM layers

This project aims to develop multilingual named entity recognition that can deal with text that is written in english, french, german and Italian. 

In these days, named entity recognition (NER) is widely used around in our daily life. NER is a sub-task of information extraction in Natural Language Processing (NLP) that classifies named entities into predefined categories such as person names, organizations and locations. 

 
In European region, there are lots of different languages that are used. Therefore, multilingual NER is useful in the sense that it can deal with text that is written in diverse languages. In this project, I selected four different languages, English, German, French and Italian, which are the top four most widely used language in Europe. According to European Union, in 2018, more than 306 million people use these languages, which is approximately 41% of the total European population. So this multilingual Named Entity Recognition opens the door to understanding entities across languages in Europe, making our system more adaptable.

 
For this model, I used the Polyglot-NER dataset from hugging-face, which is a basic Wikipedia based training data for the task of named entity recognition. Due to the vast amount of data, only 3% of the total data is used, which consists of (approx. 12 thousand) 12,719 sentences for English, 11,350 for Italian, 12,552 for French, and 16,427 for German. There are four different NER tags : ‘O’,’PER’,’LOC’ and ‘ORG’. ‘O’ tag is for entities with no meaning. ‘PER ’ is for people or person, ‘LOC’ is for city, town, country, region and continent and ORG indicates the words for sports, sports team, book, newspaper, and organization. For each sentences, corresponding NER tags were used as target value. To ensure fair evaluation, the 80% of the data was used as training and 20% for testing.

 
Since text data cannot be directly used in neural network, preprocessing was necessary. For this dataset I used tokenization and padding. The model includes an embedding layer, two bidirectional LSTM layers, and a time distributed layer to configure the LSTM layers. The bidirectional LSTM lauers process the input sequence in both forward and backward directions, providing a comprehensive view of the context around each word. This bidirectional approach is crucial for capturing nuanced information in each sentences. 

 
To increase the reliability of the evaluation result, 5-fold cross-validation was implemented to derive the accuracy of the model. The average validation accuracy was over 98% for all the folds. For the test set, the confusion matrix, accuracy, and F1 score, were used as an evaluation metrics to provide an insight about the model’s performance in unseen data. For the test set the model performed with an accuracy of 98.72 and F1 score of 98.63%. As you can see from  yellow underlined numbers in the confusion matrix in the code, most of the errors are occurred by predicting words with no meaning as words that has meaning, and vice versa. Also, we can see that high accuracy of the model came from the fact that majority of the words has O tags as the true label. However, the model was able to capture the difference between the words with PER, LOC, and ORG tags. 


Moreover, the model can visualize the prediction outputs by assigning different colors to different NER tags. I have randomly picked 10 different sentences from the test set. The LOC tag is colored in orange, PER tag with grey and ORG tag with blue. This NER visualization can be useful for a variety of applications. It can help analysts and researchers to understand the distribution and relationships of named entities in a text and to identify patterns or anomalies in the data. Also, it will be possible to gain insights from text data and to develop more accurate and effective MER models.

 
Because the model had high accuracy due to large number of “O” tags, to improve the model, we can consider applying sentence level resampling to have more tags that contains meaning. Moreover, we can adapt the model to use different tags by training the model on data with different tagging format, such as IOB tags (inside-outside-beginning), which is one of the common tagging formats in NER. Moreover, we can explore extending our model to even more languages, enhancing its adaptability. In conclusion, this projected paved the way for more inclusive and versatile multilingual named entity recognition.
