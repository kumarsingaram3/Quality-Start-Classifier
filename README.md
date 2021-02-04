# Quality-Start-Likelihood

This project was created to help predict the likelihood that an MLB pitcher will earn a Quality Start (QS) next game. More detail about the story and reasoning behind the project is located here. And the script to run the model can be found [here](https://github.com/kumarsingaram3/Quality-Start-Classifier/blob/main/qs_classifier.ipynb).

## Table of Contents
* 

## Project Description

In Major League Baseball (MLB), each team has a pitching rotation they cycle through each week. Pitchers cannot play daily because doing so, adds wear and tear to their throwing arm, so these starts are typically once a week. Of the statistics that help determine a pitcher’s success in a particular start, the QS may be the most important. This is because a pitcher has two essential jobs: to prevent runs and force enough outs to get his teams’ batters back in a position to score. To get a QS, a pitcher must allow three or less earned runs and play at least six innings. The QS is a particularly important metric in fantasy baseball because of its correlation to other pitching categories we are trying to win: ERA, WHIP, and strikeouts.

## Findings

When structuring this model, it was important to think deeply about how it would be used in production. During the fantasy baseball season, we often have difficulty in choosing who deserves to start a game between relatively unknown pitchers. Making this problem binary (1 - Pitcher gets a QS, 0 - Pitcher does not get a QS), would therefore be a mistake. This is because, when streaming pitchers off the waiver wire, many pitchers would be pushed into the 0 bucket (hence why no one owns them). **Instead, it is far more important for the model we create to be able to quantify the uncertainty, thereby helping us make an informed decision.** 

In deciding on the output of the model, we were also able to clarify the performance metric to optimize, which is the Area Under the Curve (AUC). 

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



