# hm-sna-project

# Background

H\&M is a clothing company with 53 online markets and 4,850 stores. In these markets an stores, there are over 100,000 articles of clothing. Without a recommendation system, a customer could spend hours searching for an article of clothing and could ultimately decide to leave the market or store without purchasing anything. We have used collaborative filtering to build recommendation systems for customers using purchase history of the customers. These systems will improve customer experience as it will decrease the amount of time in a market or store and reduce return rates. We found that number of neighbors did not affect the performance of the model; however, the results gave evidence that there is positive correlation between MAP@k and number of recommendations.

# Challenges

1. We had sparse data because there are over 100,000 articles of clothing in the data set
2. New user also cause an issue as our user-based recommendation system must have information about other users to make recommendations. However, new users may have purchased few items causing them to not be similar to other users

To handle the challenges, we scaled the data and decreased users and items. We used only one month of data to decrease our transactions to about 1 million from 31 million. Then, we removed customers who had made fewer than 10 purchases as this would decrease our data size as well as remove new customers. Another technique was to remove items that had been purchased fewer than 20 times because this could help decrease the data size as well as remove new items.

# Data

The data provided contains information about articles of clothing, customers, and transactions. There were 105,542 articles of clothing with descriptions about name, color, appearance, and departments. There were 1,371,980 unique customers with information about age and location. In the transactions data, there were 31,788,324 transactions from September 20, 2018 to September 22, 2022. Transaction data contained the customer, article, price, and whether the customer purchased online or in store. The data did not include ratings; therefore, we used the number of purchases by a customer of an article as a proxy for how the customer would have rated the item.

# Methods

We used two methods to create our recommendation systems: item-based and user-based collaborative filtering. We used both methods to see how both performed since both methods are nearest neighbors methods. 

## Item-based

Item-based collaborative filtering predicts similar items based on the items users have already purchased. The model recommends an item based on items that the user has previously consumed. The model then looks for the items that the user has purchased then it finds other items similar to purchased items to recommend.

![Equation](https://latex.codecogs.com/svg.image?pred(u,i)&space;=&space;\frac{\sum_{j\in&space;ratedItems(u)}^{}&space;sim(i,j)&space;*&space;(r_{uj})}{\sum_{j\in&space;ratedItems(u)}^{}&space;sim(i,j)})

## User-based

User-based collaborative filtering predicts the rating for a user on an item given how other users in the neighborhood have rated the item. In order to find the neighbors in a user's neighborhood, we used cosine similarity to sort each user's neighbors from most similar to least similar.

![Equation](https://latex.codecogs.com/svg.image?pred(u,i)&space;=&space;\overline{r}_{u}&space;&plus;&space;\frac{\sum_{n\in&space;neighbors(u)}^{}&space;sim(u,n)&space;*&space;(r_{ni}&space;-&space;\overline{r}_{n})}{\sum_{n\in&space;neighbors(u)}^{}&space;sim(u,n)})

# Results

We achieved results for both methods. The user-based collaborative filtering was easiest to implement and context independent. The notebook with the analysis and results can be found [here](https://github.com/mattflaherty97/hm-sna-project/blob/main/user-based-filtering.ipynb). However, the item-based collaborative filtering used an item-item matrix and recommends based on similar items. The results can be found [here](https://github.com/mattflaherty97/hm-sna-project/blob/main/product_based_collaborative_filtering.ipynb)
