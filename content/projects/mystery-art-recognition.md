---
title: 'Mystery Art Object'
# date: 2023-12-22T22:22:29-05:00
draft: false
summary: "Final Project for MTH 353 Deep Learning Seminar & ARH 212 Ancient Cities and Sanctuaries"
description: "Final Project for MTH 353 Deep Learning Seminar + ARH 212 Ancient Cities & Sanctuaries"
tags: ["machine learning","art history","image recognition","interdisciplinary"]
cover:
  image: /img/projects/mystery-art-recognition/model_snippet.png
  alt: Mystery Art Object Recognition Models Snippet
  hidden: false
author: ["Fall 2023"]
hideMeta: false
weight: 10
---

## Brief Abstract
Convolutional Neural Network (CNN) is a subtype of Neural Networks that is mainly used for applications in image recognition. For the final project, I trained a CNN that recognizes artworks from ancient Near Eastern, Egyptian, Greek, and Roman styles that were introduced in the ARH 212 course. The training data of this CNN are pictures of artworks from those cultures. The label for the training data is the culture origin of the artworks in the images. The trained neural network was used to predict what culture a collection of mystery objects was from. The model's performance was highly dependent on the data distribution on different categories, and the final results indicated Greek styled artworks' high resemblance to both Egyptian and Roman styles.

---
## Data
Data used for this project comes from WikiArt, the MET collection, and several directly from Google search engine. WikiArt images were used for prototype testing, which is the "Final-Project-Prototype" file. It yields good accuracy, but the dataset is poorly balanced with poor resolution.

The final training dataset uses images from the MET collection, and has the categories as follows: Near East[^1] 150 images, Egyptian 250 images, Greek 200 images, and Roman[^2] 50 images. Images only have one category in the MET collection, and has at least 72*72 resolution. 

To balance the data distribution, I also tested:
* Near East 150 images, Egyptian 300 images, Greek 250 images[^3]
* Egyptian 250 images, Greek+Roman 250+50=300 images[^4]. 


[^1]: The Near East category is a discrete set of artworks in the following categories: Phrygian, Assyrian, Iran, Achaemenid, Urartian, Israelite, Scythian, Babylonian, Parthian, Cypriot, Hillite, and Xiong Nu.
[^2]: Roman contains several artworks from Etruscan.
[^3]: This combination is to offset the really small Roman category.
[^4]: This combination is to have a binary classification with equal number of artworks. However, as indicated by the final result, Greek has a similar level of resemblance to both Egyptian and Roman, meaning that adding Roman to Egyptian might makes the model more difficult to recognize, even thought the two category has equal number of data. 

For testing, or the "Mystery Art Object Reconition", I tested out with the images in "Mixed_Categories", which are images that have multiple styles as labels or don't have a settled style from the MET collection.

Here's a snippet of the image data here: 
{{< figure width="450" alt="Image Data Snippet" src=/img/projects/mystery-art-recognition/Sample_from_Data.png >}}
Some Image augenmentation is applied to prevent overfitting as follows:
{{< figure width="450" alt="Image Augmentation Visualization" src=/img/projects/mystery-art-recognition/Image_Augmentation.png >}}

---
## Model
The models I used are CNNs, one Keras and one Tensorflow. (Keras is model 1, Tensorflow is model 2) Essentially they are the same thing, but the Keras one is more nuanced with multiple layers, while the Tensorflow one is really a high-level, basic CNN, with 3 hidden layers.

{{< gist yuhanwww 1ae0dcfd17641c8330489c477d4a6aa1 >}}

---
## Evaluation & Results
Here is a table showing the overall results.

The model overall reached an accuracy around 60%, which is not as ideal. Because the training takes much time, and the artwroks from ancient cultures indeed have many similar features, it is hard to know whether this is a good stopping point, or there are some potential places to work on to improve the model. The model's performance at this stage seems to really be dependent on the data available for one category.

Results of 2 models on the original dataset:
{{< figure width="800" alt="2 model accuracy bar plot" src=/img/projects/mystery-art-recognition/2model_vis_bar.png >}}
{{< figure width="800" alt="2 model accuracy confusino matrix" src=/img/projects/mystery-art-recognition/2model_vis_conf.png >}}

Then coming to different categorizations, it definitely helps to improve the model's performance. Deleting Roman yields an 80% accuracy for Greek; and building a balanced dataset yields a 67% overall accuracy rate.I think it will be more interesting to dig deeper into the model and find out what features of the images lead to its prediction at this moment.

Results of Tensorflow model on 3 different categorizations:
{{< figure width="800" alt="2 model accuracy bar plot" src=/img/projects/mystery-art-recognition/3cate_vis_bar.png >}}
Then coming to the prediction, the model definitely is more confident to (or prefer to) predicting Greek and Egyptian, as it never predicts the artwork to be Roman even though it is trained on 4 categories.
{{< figure width="450" alt="2 model accuracy bar plot" src=/img/projects/mystery-art-recognition/mystery_pred.png >}}

Greek and Egyptian are the two that are predicted the most, while Roman is never predicted as the highest probable culture origin. To officially implement the model in real art recognition, more work is needed to decipher how the model predicts, which will more effectively provide insights about what features link to what prediction.

---
## Final Thoughts
This project concludes my study of art of ancient cities and of machine learning in general. The prolonged data collection phase allowed me to go over a huge number of artworks in different cultures, and the overall digging of data also provides insights about the number of artworks we have in record for different cultures– Egyptian being the most abundant. Moreover, the model is an innovative foundation for future application of ML to analyze artworks of ancient cities. It is transferable to similar research and will be more informative if fed with abundant high-quality data. Lastly, the models’ performance indicates the fact that artworks of ancient cities are highly related and share similarities in many aspects– material, pattern, subject matter, and so on. Greek being the culture in between Egyptian and Roman has equal resemblance to both styles in the model’s eyes, but the fact that the model performs well in predicting Greek also points out some unique features of Greek artworks in the model’s perception. Also, when concluding the model’s prediction, I only looked at the class with the highest probability, but it will be interesting to examine the probability distribution and analyze the artwork as a collection of styles. Overall, the project intersects art history with computer science and effectively utilizes modern technology to scientifically analyze artworks in their contexts, and I am excited to continue similar approaches for creative exploration of art through the computer’s perception.

[You can view more in the Github Repo here :>](https://github.com/Yuhan-Wang-yw/Mystery-Art-Object-Recognizer)
