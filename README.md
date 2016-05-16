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

1.<b>K-Means</b>

K-means is a method of vector quantization, which is popular for clustering analysis. K-means
clustering aims to partition N observations into K clusters in which each observation belongs to the
cluster with the nearest mean, serving as a prototype of the cluster. This results is a partitioning
of the data space into Voronoi cells.

K-means algorithm originally is a NP hard problem but using some intelligent heuristics
can converge to a local optimum if we are working in non-convex curving function. K-means
clustering uses Expectation Maximization approach which is an iterative approach to converge
to local Minimum. K-means algorithm is implemented with cluster centroids with comparable
special extent and we use hard clustering i.e. documents do not overlap into multiple clusters.

<b>Algorithm Pseudocode</b>:
- Pick K mean vectors using labeled data
- Calculate initial mean and allow documents to assign to different cluster contradicting the label tags. We do this step to   not over fit the data
- Iterate until  ![equation](https://latex.codecogs.com/gif.latex?%7C%5Cmu%5E%7Bnew%7D_j-%5Cmu%5E%7Bold%7D_j%7C)
      - Assign each document x<sub>i</sub> to its closest mean vector μ<sub>j</sub>.
      - Update each mean vector μ<sub>j</sub> to be the mean of the x<sub>i</sub>’s assigned to it.

Distance between documents and mean are calculated using Cosine Similarity (since the documents are normalized according to their length). An error function is used as Gradient descent and the objective is to minimize this error function. It is the sum of the distance between the documents to their assigned clusters.

Error Function :

![equation](https://latex.codecogs.com/gif.latex?E%28D%2CM%29%20%3D%20%5Csum_%7Bi%3D1%7D%5E%7BN%7D%5Csum_%7Bj%3D1%7D%5E%7BN%7Dr_%7Bij%7D%20.%20d%28x_i%2C%5Cmu_j%29)

2. <b>Naive Bayes</b>:

![equation](https://latex.codecogs.com/gif.latex?P%28c_i%7C%5Coverrightarrow%7Bd_j%7D%29%20%3D%20%5Cfrac%7BP%28%5Coverrightarrow%7Bd_j%7D%7Cc_i%29%20.%20p%28c_i%29%7D%7BP%28%5Coverrightarrow%7Bd_j%7D%29%7D)

The key is how to compute the posterior probability ![equation](https://latex.codecogs.com/gif.latex?P%28c_i%7C%5Coverrightarrow%7Bd_j%7D%29) that document d<sub>j</sub> belongs to category c<sub>i</sub>. According to Bayes formula, the posterior probability ![equation](https://latex.codecogs.com/gif.latex?P%28c_i%7C%5Coverrightarrow%7Bd_j%7D%29) is translated to compute the prior probability ![equation](https://latex.codecogs.com/gif.latex?P%28%5Coverrightarrow%7Bd_j%7D%7Cc_i%29). Then, the categories that have the most prior probability are judged into the final categories of document d<sub>j</sub>.

Here P(c<sub>i</sub>) denotes the probability of category csub>i</sub> in the training set and P(dsub>j</sub>) denotes document dsub>j</sub> in the training set. Because P(dsub>j</sub>) is invariant for a given document dsub>j</sub> in all categories. The final category is decided by following formula :


![equation](https://latex.codecogs.com/gif.latex?argmax_%7Bc_i%7D%20P%28c_i%7Cd_j%29%20%3D%20argmax_%7Bc_i%7D%20P%28%5Coverrightarrow%7Bd_j%7D%7Cc_i%29%20.%20P%28c_i%29)


We have used Multinomial Naive Bayes, in which we take into account the term frequency in the class, the term count of the class and vocabulary of the dataset. If   ![equation](https://latex.codecogs.com/gif.latex?%5Coverrightarrow%7Bd_j%7D%20%3D%20%28%7Bw_1%2Cw_2........w_n%7D%29), then the probability of a token wsub>j</sub> given class c<sub>i</sub> is calculated by


![equation](https://latex.codecogs.com/gif.latex?P%28%5Coverrightarrow%7Bw_j%7D%7Cc_i%29%20%3D%20%5Cfrac%7Bcount%28w_j%2Cc_i%29%20&plus;%201%7D%7Bcount%28c%29%20&plus;%20%7CV%7C%7D)

Using this, the probability of a document given the class is given by


![equation](https://latex.codecogs.com/gif.latex?P%28%5Coverrightarrow%7Bd_j%7D%7Cc_i%29%20%3D%20P%28c_i%29%20.%20P%28w_1%7Cc_i%29%20.%20P%28w_2%7Cc_i%29.......P%28w_n%7Cc_i%29)

<b>Experimentatl Dataset</b>:

We have used BBC news dataset for these experiments. the dataset consists of 2225 documents
from the BBC news website corresponding to stories in five topical areas from 2004-2005. The
topics are business, entertainment, politics, sport and tech. Each document has a title and article
text. All three classifiers are trained and tested on the same training and testing dataset. The data
is divided in 10 folds, where one part is used for testing and rest is used for training.
