# Quality-Start-Likelihood

This project was created to help predict the likelihood that an MLB pitcher will earn a Quality Start (QS) next game. A more detailed background about the project can be found [here](https://github.com/kumarsingaram3/Quality-Start-Likelihood/blob/main/QS%20Likelihood%20Background.docx). And the script to run the model can be found [here](https://github.com/kumarsingaram3/Quality-Start-Classifier/blob/main/qs_classifier.ipynb).

## Table of Contents

- [Project Description](#project-description)
- [Findings](#findings)
- [Technologies](#technologies)
- [Methods](#methods)
- [Installation](#installation)

## Project Description

In Major League Baseball (MLB), each team has a pitching rotation they cycle through each week. Pitchers cannot play daily because doing so, adds wear and tear to their throwing arm, so these starts are typically once a week. Of the statistics that help determine a pitcher’s success in a particular start, the QS may be the most important. This is because a pitcher has two essential jobs: to prevent runs and force enough outs to get his teams’ batters back in a position to score. To get a QS, a pitcher must allow three or less earned runs and play at least six innings. The QS is a particularly important metric in fantasy baseball because of its correlation to other pitching categories we are trying to win: ERA, WHIP, and strikeouts.

## Findings

When structuring this model, it was important to think about how it would be used in production. During the fantasy baseball season, we often have difficulty in choosing who deserves to start a game between relatively unknown pitchers. Making this problem binary (1 - Pitcher gets a QS, 0 - Pitcher does not get a QS), would therefore be a mistake. This is because, when streaming pitchers off the waiver wire, many pitchers would be pushed into the 0 bucket (hence why no one owns them). **Instead, it is far more important for the model we create to be able to quantify uncertainty and help us make an informed decision.** 

In deciding on the output of the model, we could clarify the performance metric we should try to optimize, which we decided should be Area Under the Curve (AUC). In optimizing for AUC, we are not making an implicit decision on whether a certain kind of classification is more costly. Instead, we are measuring the performance of the model at every classification threshold.

After scraping 32K+ samples of pitcher game log data, we feature engineered many types of variables that we thought would be meaningful. The most interesting insight from the the feature set was found in the correlation matrix below:

![strikes_qs](https://user-images.githubusercontent.com/75543007/106826315-aff09e00-6654-11eb-9ad7-be9355b18ad8.PNG)

The matrix above displays the relationship between many variations of strike/strikeout features (strikes over the last 2 games, strikeouts over last 12 games, strikeout to walk ratio, etc). Despite not being an input of the Quality Start (runs and innings pitched), the strikeouts a pitcher threw showed a stronger relationship than almost any other variable (although no feature showed a correlation with the target above 25%). While this is somewhat surprising, what is even more surprising was that the relationship between *strikes* and a quality start is even stronger. This was also the case when we used mutual information classification to find the most important features. Another takeaway from the EDA process was how low the correlation strength for any of our features were. This brought to light some of the challenges of predicting a single game sample, which is why allowing the model to quantify its uncertainty instead, is valuable. 

Finally, we tested three different models to predicted the likelihood of a Quality Start. A decision tree, random forest, and a support vector machine. Each model performed very similarly, with the random forest and support vector machine performing equally:

![svm_auc](https://user-images.githubusercontent.com/75543007/106827022-0f9b7900-6656-11eb-8443-f0c42cb63348.PNG)

After viewing some of the probability predictions for both models by ranking pitchers, we finalized the support vector machine. Although the models built showed quite a bit of underfitting, there were many insights that we were able to take away, such as the importance of strikes & how runs are not as important as we thought. Also, the flexibility of having a probability for every pitcher in the MLB in their very next start will be a major competitive advantage through the fantasy season even though the model may not get it right all the time. In future iterations of this model, it would be interesting to include even more granular data into the model. For example, can we understand the influence of catchers on a pitcher's performance? How about the influence of different ball parks? The reality is that the outcome of a single game can be influenced by millions of variables and also be highly random. Figuring out ways to increase the information we have and maybe even broaden the scope of the model a bit, could help in the future. We will deploy this model into use during the 2021 season as a next step and see how it performs. 

## Technologies

* Python
* Pandas
* Numpy
* Jupyter
* Sklearn
* Beautiful Soup

## Methods

* Web Scraping
* Feature Selection
* Data Visualization
* Machine Learning Techniques

## Installation

* Clone this repo to your computer
* Save [Pitcher List](https://github.com/kumarsingaram3/Quality-Start-Classifier/blob/main/pitcher_list.xlsx) to your computer (into 'data' folder)



