# Advanced-Project
Material for level 4 advanced project "Toxic Language Detection using Machine Learning"

# Files

## Project Diary
Tracks project progress.\
Contains a list of objectives completed and those to be completed alongside the date of the meeting the completed objective was discussed.

## Project Plan
From the beginning of the project.\
Contains:
* Project Description
* Preliminary Preparation
* Basic, Intermediate and Advanced Deliverables
* Gantt Chart
* References

## List of Ideas
Initial brainstorming of project focus.\
Contains table of ideas, feasibility, potential datasets and current research on subject.\
Lists possible research questions.

## Crowdsourcing Proposal
Outlines aims, potential dataset, questioning strategy as well as reasoning behind a crowdsourcing proposal to connect annotator demographics to the demographics mentioned in toxic comments.

## Lecture Presentation
Slides for talk given during NLP lecture on project.

## Sensitivity Results
Sensitivity results for toxicity classification and sensitivity and specificity results for gender classification over different runs with different seed values.

## Meeting Notes
Contains summaries of discussions held in supervisor meetings.\
Goes over the week's progress, results, and aims for the next week.\
Labelled by date, although some are missing due to continuing work from previous week and so having little to show/focused on coursework that week/did not make progress due to personal circumstances.

## Literature
### Literature Review
Completed literature review from first term, examining papers in subject area.

### Literature Notes
Unstructured notes taken while reading literature for literature review.

### Dataset Statistics
For both datasets intended for use in project it contains:

* Description of Dataset
* Links to where it can be found/documentation/code where used
* Research that used the dataset (contribution, findings, model, metrics)
* Schema of Dataset
* Analysis of Dataset (generated graphs and examined annotator demographics)

### Dataset Summary
For each dataset discovered in the literature it contains:

* Name
* Type of data
* References
* Notes on data and its usefulness

## Code
Below are the Notebooks written for the project in order of creation.\
The notebooks containing the most recent results that are most influential to the project are described last (Toxic_BERT_Sentiment.ipynb, Male_Toxic_BERT.ipynb, Female_Toxic_BERT.ipynb, Male_BERT_No_Offensive.ipynb, Female_BERT_No_Offensive.ipynb, Gender_BERT_No_Offensive.ipynb, Gender_BERT_No_Offensive_Just_Toxic.ipynb).

Link to dataset used: https://figshare.com/articles/dataset/Wikipedia_Talk_Labels_Toxicity/4563973

Information on dataset: https://meta.wikimedia.org/wiki/Research:Detox/Data_Release

List of offensive words used: https://www.cs.cmu.edu/~biglou/resources/

### Data Analysis.ipynb
Notebook used for preliminary analysis of datasets.

* Looks at data
* Merges related datasets into single DataFrame
* Calculates mean attack, aggression and toxicity scores per comment
* Finds overlap between related datasets
* Displays useful statistics (annotations per comment, % toxic ratings, demographic information and toxicity scores related to demographic information)
* Word clouds showing most frequent words in comments about men, women, black, and white people respectively

### Word Clouds.ipynb
Word clouds showing most frequent words in comments annotated by male and female annotators repsectively.

### Autoencoder First Attempt.ipynb
Unfinished attempt at building an autoencoder trained on only one class (very toxic data annotated by women) and then measuring the reconstruction error for other classes

### Autoencoder.ipynb
Final version of autoencoder using Keras embeddings.\
Results not as expected. Reconstruction of sentences focused on the most frequent words in the comments such as 'article' and 'page'.\
Poor results meant autoencoder not fit for intended purpose of measuring reconstruction error between classes.

### First Classifier.ipynb
Intitial application of BERT to dataset.

### BERT_Classifier.ipynb
Version 1 of the BERT classifier, trained and tested on toxic and non-toxic examples, not on a balanced dataset.\
Gives confusion matrix and F1 score per batch.

### BERT_Balanced.ipynb
Version 2 of the BERT classifier, trained on balanced data for the below groups:

* Female annotator, toxicity score -2
* Male annotator, toxicity score -2
* Female annotator, toxicity score -1
* Male annotator, toxicity score -1
* Female annotator, toxicity score 0
* Male annotator, toxicity score 0
* Female annotator, toxicity score 1
* Male annotator, toxicity score 1
* Female annotator, toxicity score 2
* Male annotator, toxicity score 2

Words "toxic"/"neutral"/"healthy" were appended to comments based on toxicity score.\
The label was the gender of the annotator and gender predictions were tested for each of the 10 groups.

### BERT_groups.ipynb
Version 3 of the BERT classifier, trained on balanced data for the same 10 groups as above.\
Same conditions as in BERT_Balanced.ipynb except the labels were the groups so the ability of the classifier to sort the comments into the groups was tested.

### BERT_distributions.ipynb
Version 4 of the BERT classifier.\
Same as BERT_Balanced.ipynb except for the addition of graphs showing the distribution of the (male,female) values predicted by the classifier for the true positive and true negative cases.

### Toxic_BERT.ipynb
Version 5 of the BERT classifier.\
Trained on balanced data for male/female annotators of toxic data.\
The label was the gender of the annotator and gender predictions were tested for just the toxic data.\
Results showed a bias towards predicting an annotator as male.

### Neutral_BERT.ipynb
Same concept as Toxic_BERT.ipynb, except for neutral data, again showing bias towards predicting an annotator as male.

### Healthy_BERT.ipynb
Same concept as Toxic_BERT.ipynb, except for healthy (positive/constructive) comments, again showing bias towards predicting an annotator as male.

### Toxic_BERT_Gradients.ipynb
Version 6 of the BERT classifier, building on Toxic_BERT.ipynb.\
Addition of Captum library, using integrated gradients to visualise the words relied on for gender classification of annotators. (First attempt at this, dubious success).

### Toxic_BERT_Sentiment.ipynb
Version 7 of the BERT classifier.\
Same goal as Toxic_BERT_Gradients.ipynb, but greater success in implementation.\
Also added colour and notes to figures.\
Includes correlation metrics and graphs for number of offensive words in comment vs gender of annotator.\
Displays results of application of integrated gradients for added explainability.\
Highlights words in text that contributed strongly to male/female annotator prediction.

### Male_Toxic_BERT.ipynb
Version 8 of the BERT classifier.\
Task to find agreeement between models trained on male/female data respectively.\
This model was trained on balanced toxic/nontoxic data annotated by men.\
The aim was to predict the toxicity of comments in different test groups.\
Added offensive word analysis of test groups including word clouds.\
Removed offensive words from comments and retested on pretrained model.

### Female_Toxic_BERT.ipynb
Female version of Male_Toxic_BERT.ipynb.\
Aimed to gather same findings using model trained on female data.

### Male_BERT_No_Offensive.ipynb
Version 9 of the BERT classifier.\
This model was trained on balanced toxic/nontoxic data annotated by men, with all offensive words removed.\
The aim was to predict the toxicity of comments in different test groups, comparing with the results from Male_Toxic_BERT.ipynb to see if offensive words are a key factor in prediction and to see which gender is better at using the context and semantics in the text now that the offensive words have been removed.

### Female_BERT_No_Offensive.ipynb
Female version of Male_BERT_No_Offensive.ipynb, comparing results with Female_Toxic_BERT.ipynb.\
Aimed to compare female and male model's adaptability to training data without offensive words.

### Gender_BERT_No_Offensive.ipynb
Version 10 of the BERT classifier, based on version 7 of the BERT classifier Toxic_BERT_Sentiment.ipynb.\
Training data changed to remove offensive words in comments.\
Predicting genders of annotators for test data with/without offensive words.

### Gender_BERT_No_Offensive_Just_Toxic.ipynb
Version of Gender_BERT_No_Offensive.ipynb using only toxic class (not very toxic class) as training data to see if affected gender predictions.

### Boxplots.ipynb
Boxplots generated to present results across all runs of the above models in the paper.