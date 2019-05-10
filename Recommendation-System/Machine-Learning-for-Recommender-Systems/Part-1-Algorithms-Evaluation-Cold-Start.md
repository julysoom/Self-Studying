# Machine Learning for Recommender Systems Part 1 (Algorithms, Evaluation, Cold Start)
url
* https://medium.com/recombee-blog/machine-learning-for-recommender-systems-part-1-algorithms-evaluation-and-cold-start-6f696683d0ed
* https://datascienceschool.net/view-notebook/fcd3550f11ac4537acec8d18136f2066/
## Algorithms
* **Recommendation System** = software systems providing **suggestions** for users utilizing **historical interactions** and **attributes** of items/users
* modern recommenders combine both approaches (CB, CF)
### CB v. CF
* Content-based
   * using attributes of items/users
   * recommending itmes similar to those **liked by the user in the past**
* Collaborative Filtering
   * recommending items liked by **similar users**
   * allows diverse recommendation → how can we enable users to discover **new** content that is **dissimilar** to items viewd in the past?
### Recommendation Task
* set of users **U**, set of items **I** that will be recommended to users
* **learn** a function based on the **past data that predicts utility of each item** to **each user**
   * i(∈I): predicting utility of each item
   * u(∈U): to each user
* CF uses interaction matrix (rating matrix) → rare case where users provide **explict** rating of items
   * matrix is usually huge, very **sparse**, and most of the values are missing (NA)
### Baseline Model
* use user id *u*, item id *i*, *rui* (rating using *u*,*i*) → predict *hat rui* (predicted *rui*) by using a simple **regression** model → sum of average rating given out by users based on the charteristics of item

![image](https://user-images.githubusercontent.com/42960718/57523143-1e5cdb00-735f-11e9-9453-8b5d8bfa6c45.png)
* *M* = mean of total ratings
* *bu* = a conditioned rating based on a user (based on user A)
* *bi* = a conditioned rating based on a item (based on item A)


### User-based k-Nearest Neighbors
* compute similarity of users by finding **k** most similar users to user a
* recommend item that user a has **not** seen
* uses cosine similarity

![image](https://user-images.githubusercontent.com/42960718/57515108-d7fe8080-734c-11e9-9ff9-6b7f8ef18fd5.png)
## Matrix Factorization

![image](https://user-images.githubusercontent.com/42960718/57515156-f1073180-734c-11e9-8fc9-1c46ec23d90f.png)
* reducing dimensionality of the interaction matrix and approximate it by two or more small matrices with **k latent components**

![image](https://user-images.githubusercontent.com/42960718/57515236-1b58ef00-734d-11e9-9117-887cd1fee450.png)
* multiply corresponding row and column to predict the rating of item by the user
* training error can be obtained by **comparing with non-empty ratings to predicted ratings**
* also can **regularize** training loss by adding a **penalty term** to keep values of latent vectors low
### SGD v. ALS
#### Stochastic Gradient Descent (SGD)
* most popluar training algorithm that **minimizes** loss by gradient updates of both columns and rows of *p* and *q* matrices
* updates each parameter independently
* derive the loss fuction with respect to each parameter
