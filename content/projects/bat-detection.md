---
title: 'Bat Detection'
date: 2024-01-07T22:22:15-05:00
draft: false
summary: "Biointerphase Team A - Fall 2023 AI Studio Project from Break Through Tech AI program at MIT."
tags: ["project","machine learning","bat","MIT","Break Through Tech AI"]
cover:
  image: /img/projects/bat-detection/conf_mtx_wordcloud.png
  alt: Bat Detection Model Prediction Confusion Matrix Word Cloud
  hidden: false
author: ["Fall 2023"]
hideMeta: false
---
Team A: Anders Freeman, Anusha Bandaru, Iris Yang, Linda Dominguez, Yuhan Wang

[^1]: Wellesley College
[^2]: Northeastern University
[^3]: Tufts University
[^4]: Smith College

---
## Introduction
White Nose Syndrome (WNS) is a fungal disease that infects skin of the muzzle, ears, wings of hibernating bats and has ravaged North American bat populations. This project aimed to understand the outlook for bat population decline in North America due to WNS, use machine Learning models to predict what features signal population decline, and so to provide insight to guide efficient bioengineered solutions to combat WNS for Biointerphase. 

Here is an overview of our approach:
{{< figure width="750" alt="Approach Overview" src=/img/projects/bat-detection/approach.png >}}

---

## Data
Our project combines 3 datasets: Skin mycobiomes of Easter North American bats, west_master_table, and white_nose_county_status. The first 2 datasets contain information about bat population, fungi detected[^5], collection date, collection location, host group, CFU, etc. The 3rd dataset contains information about time, location, and WNS presence. We merged 3 datasets by time, location, and species overlap, and then one-hot-encoded the data for model training. Our label is WNS present or not, and we aimed to explore what freatures best predict the presence of WNS.

Final dataset has 800 entries and includes columns as follow:
* Location
* Complete biological classification
* Concentration of fungi
* Time of sample collection
* If WNS had been present in the population at that time
For the final model training, Modeling(1).csv is used for the NLP model, and one_hot_model_data_without_county_and_state.csv is used for the Random Forest model.

[^5]: Specifically, information about fungal classification on differnet levels: Phylum, Class,	Order, Family, Genus, and Species

---

## Model and Results
We built 2 models in the project: a NLP(natural language processing) and a Random Forest. We started with the NLP because as the fungi classification on differnet levels are essentially arbitrary words, we wanted the model to find its own pattern. Then we chose to build a seconde model -- a random forest for a more explananble model.

### NLP Model 
{{< gist yuhanwww d567bd987edadfae5b2fca7bcdfc8615 >}}
- Took all features and put them as a natural text “sentence” and fed that data into a natural
language processing pipeline.
- Created the actual neural network with the keras library, while training it on the features in
the set
- Finally, we plotted the training and validation loss and accuracy.

Here is a table that concludes the accuracy results of different combinations of features:
|                  Data   Included                             |  Accuracy  |
|:------------------------------------------------------------:| :---------:|
| State, County, Date, Host Group, CFU, Fungal Classification  |    98.26%  |
|                    Date                                      |    95.95%  |
|                    State, County                             |    100.00% |
|            Fungus Classifications                            |    71.01%  |
|            CFU                                               |    83.24%  |
|           Host Group, CFU, Fungus Classification             |    86.13%  |

The last column is our final choice.

We conclude our model's predictions in the following 2 confusion matrix that visualizes the prediction result. We can see that the model is pretty good at predicting the presence of WNS, and tended to predict a not WNS present case to be WNS present. The second wordcloud shows in the TP, TN, FP, FN squares from the confusion matrix, what words the model rely on the most to make its prediction.
{{< figure width="800" alt="NLP model training overview" src=/img/projects/bat-detection/NLP_conf.png >}}
{{< figure width="800" alt="NLP model training overview" src=/img/projects/bat-detection/conf_mtx_wordcloud.png >}}

The main insights of the NLP model is that:
- The presence of WNS fungus in the population is not directly linked with WNS itself
- Species of fungus are associated with populations that have had WNS in the past

---

### Random Forest Model
{{< gist yuhanwww 2b452f82c8ca874dbff9418cfa30ad90 >}}
- Is more interpretable than a NLP model
- Splits the data into training and testing sets, as well as a random state to ensure
reproducibility
- Has a max_depth of 32 and a maximum number of estimators at 300.
- After the model is fitted and predictions are made, we use the root mean squared error
(RMSE) and the R2 score to get our results. The RMSE measures the difference between a model's predicted values and the actual values, while the R2 score is the accuracy.

Here is a table showing the overall results.
|                  Data   Included                             |  Accuracy  |
|:------------------------------------------------------------:| :---------:|
| Base accuracy                                                |    92.1%  |
| Removing Sample Collection Date                              |    86.7%  |
|                    Removing Resistant                        |    97.3%  |
|            Removing Unnamed: 0                               |    90.4%  |
| Removing both Sample Collection Date and Resistant           |    94.9%  |
| Removing both Sample Collection Date and Unnamed: 0          |    33.6%  |

Some key findings from the Random Forest Model:
- After performing a grid search with cross-validation to tune the hyperparameters, we found that the best-performing combination was a max depth of 30 and n-estimators of 100.
- We also found that the features that were most correlated with the data were the date and how resistant the population was.
- Sample Collection Date, and to a lesser extent, Unnamed: 0, is crucial to the accuracy of the Random Forest Model. Without it, the accuracy drops by a lot.

---
### 2 Model Comparison
{{< figure width="800" alt="NLP model training overview" src=/img/projects/bat-detection/2model_comparison.png >}}

---

## Conclusion
Combined with visualizations of the prediction results, our project indicates new directions in the research of WNS and also foundational models for future application of machine learning in the study of similar diseases. We helped inform Biointerphase of the most efficient action to combat WNS, and provided a basis for future work on combating WNS, including the availability of public datasets on WNS, 2 preliminary ML models on WNS-related data, and possible research directions.

On top of the technical aspect, we also realized the importance of having a clear outline of our research question. As dataset is really the foundation of a successful machine learning model, we hope to prioritize data exploration, analysis, and experiment in the future. Last but not least, communication, even over communication, is very essetial for a team project that scoped 3 months.

[Check out the Github Repo for full record!](https://github.com/Yuhanwww/Bat-Detection-Model)