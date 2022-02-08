#                          Legal Document Identifier
#### by Amir Daley

## source data
Raw https://osf.io/w3paz/ by category <br />
preprocessed https://osf.io/8mjcy/ if you want to skip he cleaning steps<br />
map file for category names https://osf.io/khpwd/<br />
## Introduction
Hello fellow analyst, This project was meant for the purpose to assist in the identification of legal cases and hopefully provide useful information for a future recommendation system. This research is both for prediction and exploration as we look to identify how we should target and analyze cases.

Due to size constraints and the nature of the size of the data I recommend running this code on google colab. there are many features here that run faster there and you do not need to worry about leaving your computer turned on for extended periods.  Running some of these snippets of code We created and ran concurrently was impossible with out running into time limitations or hardware restraints. <br />
here is the link to the modeling colab, a copy of it is also here in the colab. https://colab.research.google.com/drive/1VeGzQsAHiyzjmXbm2ynluDxUikYXtuGW?usp=sharing <br />

Copy the file structure here and you should be able to run the code straight through. The pulling of the files is however you see fit but it matches the file structure here, if you do not follow it exactly, it will need to be edited.

## Analysis

So I am no Lawyer but since I am currently working at the New York State Courts, I thought of tackling a problem I thought was not known to me to be sought out by law firms. That is a way to automatically categorize legal cases . Is it international law related, medical malpractice or involving real estate? I am not to familiar with specialties within law but I do know that firms normally like to funnel certain type of cases to their attorney's based on their experience within that specialty. We all know we would not want a medical malpractice lawyer to defend someone for criminal charges.

In the future this will incorporate a recommendation system based on the word models and the information that we learned from the data but I soon realized that we should take baby steps
and just see if we could categorize the data and  learn as much as we can about the nature of the corpora.

## Modeling method and results

-Okay so note that the data was pretty large with 39,155 cases 22K taken from supreme court cases

-Quickly after stop wording, lemmatizing and tokenizing the words, there seemed to be only 21k words that were relevant. but later we will see why this is a bit misleading.

-I focused on 20 out of the 38 categories. The complexity of the data made runs time consuming so this is the reason I am cutting he categories to 20.

![alt1 set1](https://github.com/criolloprimero/Legal-Document-Identifier-/blob/main/images/numberOfCase1.png)

![alt2 set2](https://github.com/criolloprimero/Legal-Document-Identifier-/blob/main/images/numberOfCase2.png)

So we can see here we can collect top words by either frequency or by relevance using TF-IDF. you can see the full list of relevant terms in note book 2.  

 We used various classification methods like KNN, Logistic regression, multinomial naïve bayes, etc.​ Through iterative modeling tried seeing if we can fine tune by filtering relevant terms, n-grams bot 1(base),2 and 3. For the models that needed to be weighted assigned weights per category​

 |XGboost Accuracy|
 |---------|
 |0.71% |
 
 so not bad, but not what i was expecting, with random probability you and 20 categorical values, if you just choose randomly you would have a rate of about 5%. 

 These were the accompanied parameters for the model:
 Params were max_depth=6, learning rate of .3, and num_estimators=100, gamma= 0

This was a bit discouraging because it seemed that the adjustments to the data did not really affect it differently which was shocking but we will see why in the next section.

 #### Neural Net

 So we ran a NN and I thought it would run better through an LSTM but it seemed to peak out around 60 percent before over fitting. But what we noticed is, and this relates to the XGboost base model running well the less manipulated the data was. The less manipulated(but still preprocessed with lemma and stopwords) the data is the better the NN performed. Assuming because of pattern matching and shifting tf-idf values.

 Parameters to play around with here that drastically affected performance were. The number of words, the size of the pad_sequence data and the embedding size.

# post Analysis

We were able to make some supplementary models and charts to gain a bit more insight into how out model is working and which features are important for each case.

first we have a word to vec model, that is calculating the distance of common terms in the greater list of words. We can use this to see which words are related and those that are not.
![alt2 ](https://github.com/criolloprimero/Legal-Document-Identifier-/blob/main/images/for%20lawcat.png)

Next is just a chart representation of the distance of words. In the future I think it will be better to just have a chart representation of just two classes the function has that capability.

![alt2 ](https://github.com/criolloprimero/Legal-Document-Identifier-/blob/main/images/for%20lawcat2.png)

Last is a lime model; with this we can get a visual representation of which words are more powerful in determining what the class is. Then we can also see the context to which the words are used in the data. I will have to test out more ngram feature, but since it did not really benefit in the original model or any one after there did not seem to a point.

Another benefit we can see what words also misclassify the model when it gets it wrong. which is an added benefit.
![alt2 ](https://github.com/criolloprimero/Legal-Document-Identifier-/blob/main/images/for%20lawcat3.png)
