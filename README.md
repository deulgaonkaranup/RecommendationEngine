<p align="center"><b>Natural Language Processing - Project<b></p>

Vivek Pabani
Illinois Institute of Technology
vpabani@hawk.iit.edu

Anup Deulgaonkar
Illinois Institute of Technology
adeulgao@hawk.iit.edu

Idea:

We have implemented a recommendation system for news articles. Nowadays all the online
news service providers use one or other kind of recommendation system. The basic
concept is the same - if we have history of user’s previously read articles, we can use that
information and decide if any new article will be of his interest or not. Based on this decisions, we
can recommend new articles to the user. Our application is rather simple. We provide n article
titles to the user, and based on his choice, we recommend m new articles, where n and m are user
selected. The original n articles are picked from test dataset, where topics are unknown at the
moment, and m recommendations are given from entire dataset. User can select the articles based
on title, and can read the text by further options.

Experimentatl Dataset:
We have used BBC news dataset for these experiments. the dataset consists of 2225 documents
from the BBC news website corresponding to stories in five topical areas from 2004-2005. The
topics are business, entertainment, politics, sport and tech. Each document has a title and article
text. All three classifiers are trained and tested on the same training and testing dataset. The data
is divided in 10 folds, where one part is used for testing and rest is used for training.
