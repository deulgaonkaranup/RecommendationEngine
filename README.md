<p align="center"><b>Natural Language Processing - Project</b></p>

<p align="center">Vivek Pabani
Illinois Institute of Technology
vpabani@hawk.iit.edu</p>

<p align="center">Anup Deulgaonkar
Illinois Institute of Technology
adeulgao@hawk.iit.edu</p>

<b>Idea</b>:

We have implemented a recommendation system for news articles. Nowadays all the online
news service providers use one or other kind of recommendation system. The basic
concept is the same - if we have history of user’s previously read articles, we can use that
information and decide if any new article will be of his interest or not. Based on this decisions, we
can recommend new articles to the user. Our application is rather simple. We provide n article
titles to the user, and based on his choice, we recommend m new articles, where n and m are user
selected. The original n articles are picked from test dataset, where topics are unknown at the
moment, and m recommendations are given from entire dataset. User can select the articles based
on title, and can read the text by further options.

<b>Algorithms Implemented</b>:

<b><u>1. K-Means</u></b>

   <i>Algorithm Pseudocode</i>:
   - Pick K mean vectors using labeled data
   - Calculate initial mean and allow documents to assign to different cluster contradicting the label tags. We do this step   to       not over fit the data
   - Iterate until  ![equation](https://latex.codecogs.com/gif.latex?%7C%5Cmu%5E%7Bnew%7D_j-%5Cmu%5E%7Bold%7D_j%7C)
      - Assign each document x<sub>i</sub> to its closest mean vector μ<sub>j</sub>.
      - Update each mean vector μ<sub>j</sub> to be the mean of the x<sub>i</sub>’s assigned to it.

Distance between documents and mean are calculated using Cosine Similarity (since the documents are normalized according to their length). An error function is used as Gradient descent and the objective is to minimize this error function. It is the sum of the distance between the documents to their assigned clusters.

<u>Error Function</u>:

![equation](https://latex.codecogs.com/gif.latex?E%28D%2CM%29%20%3D%20%5Csum_%7Bi%3D1%7D%5E%7BN%7D%5Csum_%7Bj%3D1%7D%5E%7BN%7Dr_%7Bij%7D%20.%20d%28x_i%2C%5Cmu_j%29)

<b><u>2. Naive Bayes</u></b>:

![equation](https://latex.codecogs.com/gif.latex?P%28c_i%7C%5Coverrightarrow%7Bd_j%7D%29%20%3D%20%5Cfrac%7BP%28%5Coverrightarrow%7Bd_j%7D%7Cc_i%29%20.%20p%28c_i%29%7D%7BP%28%5Coverrightarrow%7Bd_j%7D%29%7D)

The key is how to compute the posterior probability ![equation](https://latex.codecogs.com/gif.latex?P%28c_i%7C%5Coverrightarrow%7Bd_j%7D%29) that document d<sub>j</sub> belongs to category c<sub>i</sub>. According to Bayes formula, the posterior probability ![equation](https://latex.codecogs.com/gif.latex?P%28c_i%7C%5Coverrightarrow%7Bd_j%7D%29) is translated to compute the prior probability ![equation](https://latex.codecogs.com/gif.latex?P%28%5Coverrightarrow%7Bd_j%7D%7Cc_i%29). Then, the categories that have the most prior probability are judged into the final categories of document d<sub>j</sub>.

Here P(c<sub>i</sub>) denotes the probability of category csub>i</sub> in the training set and P(dsub>j</sub>) denotes document dsub>j</sub> in the training set. Because P(dsub>j</sub>) is invariant for a given document dsub>j</sub> in all categories. The final category is decided by following formula :


![equation](https://latex.codecogs.com/gif.latex?argmax_%7Bc_i%7D%20P%28c_i%7Cd_j%29%20%3D%20argmax_%7Bc_i%7D%20P%28%5Coverrightarrow%7Bd_j%7D%7Cc_i%29%20.%20P%28c_i%29)


We have used Multinomial Naive Bayes, in which we take into account the term frequency in the class, the term count of the class and vocabulary of the dataset. If   ![equation](https://latex.codecogs.com/gif.latex?%5Coverrightarrow%7Bd_j%7D%20%3D%20%28%7Bw_1%2Cw_2........w_n%7D%29), then the probability of a token wsub>j</sub> given class c<sub>i</sub> is calculated by


![equation](https://latex.codecogs.com/gif.latex?P%28%5Coverrightarrow%7Bw_j%7D%7Cc_i%29%20%3D%20%5Cfrac%7Bcount%28w_j%2Cc_i%29%20&plus;%201%7D%7Bcount%28c%29%20&plus;%20%7CV%7C%7D)

Using this, the probability of a document given the class is given by


![equation](https://latex.codecogs.com/gif.latex?P%28%5Coverrightarrow%7Bd_j%7D%7Cc_i%29%20%3D%20P%28c_i%29%20.%20P%28w_1%7Cc_i%29%20.%20P%28w_2%7Cc_i%29.......P%28w_n%7Cc_i%29)

<b><u>3. Rank Classifier</u></b>: 

We also use Rank Classifier mentioned in paper by Qirui Zhang in the paper ‘Machine Learning Methods for Medical Text Categorization’.


<b><u>4. K-Nearest Neighbour</u></b>:

The model for kNN is the entire training dataset. When a prediction is required for a unseen data instance, the kNN algorithm will search through the training dataset for the k-most similar instances. The prediction attribute of the most similar instances is summarized and returned as the prediction for the unseen instance. The decision rule in kNN can be written as:


![equation](https://latex.codecogs.com/gif.latex?y%28x%2Cc_i%29%20%3D%20%5Csum%20sim%28x%2Cd_j%29%20.%20y%28d_j%2Cc_i%29)


Here, sim(x, d<sub>j</sub>) is cosine similarity between two documents based on their vector representation. y(x, c<sub>i</sub>) returns the value 1 or 0 based on the category prediction for i<sup>th</sup> category. We have used K-Nearest Neighbor in the final stage of recommendation system in order to find the k closest articles from the source document. This is done after the other algorithms have correctly classified the document first.

<b><u>Experimentatl Dataset</u></b>:

We have used BBC news dataset for these experiments. the dataset consists of 2225 documents
from the BBC news website corresponding to stories in five topical areas from 2004-2005. The
topics are business, entertainment, politics, sport and tech. Each document has a title and article
text. All three classifiers are trained and tested on the same training and testing dataset. The data
is divided in 10 folds, where one part is used for testing and rest is used for training.
