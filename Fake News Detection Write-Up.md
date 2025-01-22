Angela Zhuang | [zhuanga@usc.edu](mailto:zhuanga@usc.edu)

Fake News Detection

Our digital age not only allows for the easy dissemination of important news, but also for the rapid spread of fake news, with misinformation deepening conflicts and divisions in society. To address this, I created a natural language processing (NLP) model that uses article titles to classify articles as either “fake news” or “real news.”

**DATASET**  
I used the “ISOT Fake News Dataset” ([https://www.kaggle.com/datasets/emineyetm/fake-news-detection-datasets/data](https://www.kaggle.com/datasets/emineyetm/fake-news-detection-datasets/data)), which contains 21,417 real news and 23,481 fake news entries, each with a title, text, subject, and publication date. For the preprocessing, I labeled the real news entries with a ‘1’ and the fake news entries with a ‘0’ for binary classification, combined the real and fake article datasets, shuffled the entries of this combined dataset, and extracted the title and label values. To improve generalizability, the other features were excluded since they had dataset-specific patterns: most real news texts included “(Reuters),” the set of real news subjects and fake news subjects differed, and most fake news publication dates were near the end of 2017. Additionally, since I planned to use a pre-trained BERT model, I tokenized the titles of the dataset using the “Bert-base-uncased” tokenizer.

**MODEL DEVELOPMENT AND TRAINING**  
Due to computational limitations, I used a subset of 10,000 samples from the dataset, with an 80-10-10 train-validation-test split. For the model, I used BertForSequenceClassification from the pre-trained uncased BERT model because it is suitable for natural language classification tasks. Furthermore, the pre-trained weights from the BERT model allow quicker learning of this task.  
I tested various combinations of the recommended hyperparameters for fine-tuning and used the best-performing set as a result: a batch size of 32, 2 epochs, and a learning rate of 2e-5 for the Adam optimizer. These hyperparameters achieved low training and validation loss, demonstrating strong performance.

**MODEL EVALUATION/RESULTS**  
I visualized the results using a confusion matrix. The model performed well on the test dataset, with 99% precision, 99% recall, and 98% accuracy. It was slightly better at identifying real news, with 99% accuracy, compared to identifying fake news, with 98% accuracy. However, overall, the model achieved strong performance.  

**DISCUSSION**  
***Suitability for Task***  
Although the dataset of fake and real news articles is large and very relevant to the task of classifying fake and real news, it isn’t perfect due to existing dataset-specific patterns. However, the model architecture and training procedures are effective for the task since BertForSequenceClassification is designed for classification tasks on natural language. Finally, the confusion matrix also suits the task because it provides detailed information about the accuracy of the model.  
***Wider Implications and Limitations***  
Though it is general practice to only use trusted websites and organizations as sources for news, when browsing articles on an unknown website, NLP models can be used as a starting point to determine whether the news article is fake or not. This raises awareness of misinformation, reducing the speed at which fake news spreads in our increasingly polarized world. However, one potential limitation is that the model only uses titles to determine whether an article is fake or real news, which may not provide enough context for accurate predictions.  
***Next Steps***  
It is important to expand the dataset to include more recent news articles, in order to train the model on topics and contexts that are more relevant today. In addition, training the model on both texts and titles may provide more comprehensive information for the model, and result in more accurate classification. One way to implement this is to remove “(Reuters)” from all the real news text in the dataset during preprocessing, so that the model cannot use this ungeneralizable method to differentiate between real and fake news during training.