#                          Legal Document Identifier
#### by Amir Daley

## source data
Raw https://osf.io/w3paz/ by category <br />
preprocessed https://osf.io/8mjcy/ if you want to skip he cleaning steps<br />
map file for category names https://osf.io/khpwd/<br />
## Introduction
Hello fellow analyst, This project was meant for the purpose to assist in the identification of legal casses and hopefully provide useful information for a future recommendation system system. This research is both for prediction and exploration as we look to identify how we should target and analyze cases.

Due to size contraints and the nature of the size of the data I recommend running this code on google colab. there are many features here that run faster and no need to worry about leaving your computer turn on for extended periods.  running some of these snippits of code I created concurrently was impossible with out running into time limitations. <br />
here is the link to the modeling colab, a copy of it is also here in the colab. https://colab.research.google.com/drive/1VeGzQsAHiyzjmXbm2ynluDxUikYXtuGW?usp=sharing <br />

Copy the file structure here and you should be able to run the code straight through. The pulling of the files is however you see fit but it matches the file structure here, if you do not follow exactly it will not run with out needing to be edited.

## Analysis

So I am no Lawyer but since I am currently working at the New York State Courts, I thought of tackling a problem I thought was not known to me to be saught out by law firms. And that is a way to catagorize automatically which what a case is. Is it international law related, medical malpractice or involving real estate. I am not to familiar with specialties within law but I do know that firms normally like to funnel certain type of caseses to their attourneys based on their experience withing that topic. We all know we would not want a meldical malpractice lawyer to defend someone for crimminal charges.

This was supposed to and will incorperate a recommendation system based on the word models and the information that we learn from the data but I soon realized that we should take baby steps.
and just see if we could catagorize the data and  learn as much as we cleaning




## Modeling method and results

-Okay so note that the data was pretty large with 39,155 cases 22K taken from supreme court caseses

-quickly after stop wording, lemmanizing and tokenizing the words there seemed to be only 21k words that were relevant. but later we will see why this is a bit misleading.

-I focused on 20 out of the 38 catagories. the complexity of the data made runs time time consuming so this is the reason I am cutting it about in half.

![alt1](images\numberOfCase1.png)
![alt2](images\numberOfCase2.png)

so we can see here we can collect top words by either frequency or by relevance using TF-IDF.  

 I used various classification methods like KNN, Logistic regression, multinomial naïve bayes, etc​ and Through iterative modeling tried seeing if we can fine tune by filtering relevant terms, n-grams bot 1(base),2 and 3. For the models that needed to be weighted assigned weights per category​

 |XGboost Accuracy|
 |---------|
 |0.71% |

 These were the ecompanied parameters:
 Params were max_depth=6, learning rate of .3, and num_estimators=100, gamma= 0

This was a bit discoraging because it seemed that the adjustments to the data did not really affect it differently which was shocking but we will see why in the next section

 #### Neural Net

 So we ran a NN and I thought it would run better through an LSTM but it seemed to peak out around 60 percent  before over fitting. But what we noticed, which relates to XGboost base model doing the best. Is the more unprocessed the data is the better the NN performed. Assuming because of more words to differentiate.​

 Parameters to play around with here that drastically affected performance were. The number of words the size of the pad_sequence data and the embedding size.
