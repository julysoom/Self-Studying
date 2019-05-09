# Recommendation-System
url : https://hackernoon.com/introduction-to-recommender-system-part-1-collaborative-filtering-singular-value-decomposition-44c9659c5e75
## Introduction
### Recommendation System
* capable of predicting future preference of a set of items for a user
* recommend top N items
* modern society have too many options due to the prevalence of internet (flood of information)
  * v. past : physical store + variety of items limited
  * due to abundance of information, people have hard time selecting the items they **actually want to see**
## Traditional (CB, CF)
### Content-based
* analyzes nature of each item 
  * recommending poets based on poem content they wrote using NLP
  * news recommendation
  * using genres or specific actors for movie recommendation
  * Word2Vec
* **pro** : doesn't require lots of user data (can be used to solve cold start), doesn't need user information
* **con** : results differ based on modeling methods, limited recommendation (only recommends items that are similar), requires complex computer operation
### Collaborative Filtering
* doesn't require any info about the items/users **themselves**
* recommend based on user's **past behaviors**
  * when user A and B have similar genre preferences, CF assumes that user B will like movies user A have liked
* **pro** : has better accuracy comparing to CB and can give out segemented recommendations based on user's behavioral pattern
* **con** : requires lots of data (not appropriate for cold start)
## Collaborative Filtering
### User-based

![image](https://user-images.githubusercontent.com/42960718/57466419-91ad1100-72bb-11e9-8f5a-3fdc0971182b.png)
* *fills in blank horizontally*
* *since user A and F don't share any movie rating in common with user E, their similarities with user E are not defined in Pearson correlation (NA)*
* *we only need to consider B, C, and D*
* measures the similarity b/t target and other **users**
  * recommending items that were liked by another user that has similary preferences
* need to  compute the similarity b/t users
* however, users' preference can change over time → precomputing based on neighboring neighbors may lead to bad performance → approach this problem using **item-based CF**
* **pro** : can make recommendations without information of item itself, simple algorithm
* **con** : requires higher computing environment when amount of user-item increases, can't find similarity b/t users for new customers
* u_{i, k} denotes similarity b/t user i and user k
* v_{i, j} denotes the rating the user i gives to item j
* v_{i, j} = ? if the user did not rate the item

![image](https://user-images.githubusercontent.com/42960718/57427965-30585400-7261-11e9-9903-83239e00d990.png)
    


#### Measuring Similarity Using Correlation (Distance v. Difference)
* Co-occurence
  * unlike the basic similarity ranges from 0 to 1 (requires complex calculation of finding numerical percentage of how item A and B are similar), co-occurence can have numbers over 0
  * using **counts** - how many times did A and B show up together
  * simplest method to measure similarity
  * however, for item A, B and C must have same appearance counts in the data
    * if B and C both appeared 20 times and B and C each co-occured with A 5, 10 times, then C is surely more associated to A than B
    * but if B appeared 10 times while C appeared 100 times, then we cannot state that C has a higher similarity than B
  * Jaccard index, Tanimato metric usually used for **implicit** data - requires complex calculation for explicit
  
  
##### Pearson v. Cosine
![image](https://user-images.githubusercontent.com/42960718/57428768-cb066200-7264-11e9-867c-86db437aa40d.png)
* Pearson

![image](https://user-images.githubusercontent.com/42960718/57427983-49f99b80-7261-11e9-9e54-1e50b18121ff.png)
  * **invariant** to adding a constant to all elements
  * ranges from -1 to 1 (1 implies highest similarity)
  * using coefficient of the correlation to prevent extreme ratings from specific users 
  
* Cosine

![image](https://user-images.githubusercontent.com/42960718/57427997-5b42a800-7261-11e9-8864-90ab9387d77d.png)
  * expressing the similarity between the two characteristic vectors using cosine
  * mainly used for **explicit** data
  * measuring correlation or change rating to vector and find cosine b/t two vectors
  * ranges from -1 to 1
    * -1 = completely opposite
    * 0 = mutually independent
    * 1= completely same
### Item-based

![image](https://user-images.githubusercontent.com/42960718/57466419-91ad1100-72bb-11e9-8f5a-3fdc0971182b.png)
* *unlike user-based CF, the blanks are filled vertically; shows similarity with "Me Before You"*
* *there is only one user that have rated "Titanic" and "Matrix" but they have a similarity of 1 → wrong result since the genre of the two movies are completely different*
* measures the similarity b/t the **items** that target user has **rated/interacted** with other items
* **similar users shares same interests → tends to like similar items**
  * recommending Sprite to users who drink Coke frequently
* **pro** : can recommend without item information, can make recommendations to new users
  * avoids problems occurred in user-based since item information is more static
* **con** : complex computing required as data increases - **scalability**, low recommendation performance at initial service due to lack of data - **sparsity**
### Utility Matrix
* how user i likes item j
* shows past behavior of users
* each cell in the matrix represents the **associated opinion** that a user holds
* where m = users, n = items (m * n matrix)
* CF is like **filling the blank** of the utility matrix that a user has **not seen/rated** before based on the similiary b/t users or items
### Explicit v. Implicit Opinion
* **Explicit** = directly shows how a user **rates** that item
  * rating an app or movie
  * straight-forward
* **Implicit** = only serves as a porxy which provides us **heuristics** about how an uesr likes an item
  * number of likes, clicks, visits
  * need to guess what each numbers imply
* Finding Music Preference
  * for instance, there is a song user really likes but he only played in once because he was busy
  * without explicit implicating (rating), it is difficult to figure out whether the user likes/dislikes the item
  * however, most of the feedbacks we collect are **implicit**
## Singular Value Decomposition (SVD)
* CF has scalability & sparsity issue → leverage a latent factor model to capture the similarity between users and items
* **recommendation → optimization** : how good we are in predicting the rating for items for the given user
* one common metric is **Root Mean Square Error (RMSE)** → the lower, the better
  * since we don't know the rating for the unseen items, we will temporarily ignore them
  * only **minimizing RMSE** on the **known** entries in the utility matrix
  * to achieve minimal RMSE, **SVD** is used
## Measuring Recommendation System Performance
* Discounted Cumulative Gain (DCG)
  * measure of ranking quality
  * measures usefulness, or gain of a document based on its position in the result list
  
  
  
   
  
  
