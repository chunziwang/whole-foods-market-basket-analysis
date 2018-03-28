# Whole Foods: Analyzing Grocery Buying Habits to Boost Cross-Selling
----

## Business Problem

Amazon recently acquired Whole Foods for $13.7 billion. The acquisition is about two things: data and product. In particular, Amazon is interested in the treasure trove of consumer data that comes with this acquisition.

What exactly is in the Whole Foods data that Amazon would want? The answer is the grocery buying habits and patterns of its customers, and the correlations between purchases of different products and even different categories. Furthermore, groceries, compared to other e-commerce purchases, are habitual and frequent. People need groceries every week.

With massive amounts of data from Whole Foods shoppers, Amazon will ultimately be able to tailor the grocery shopping experience to the individual. Amazon has already mastered the process of cross selling, i.e. offering additional items that go with the items the consumer is looking to buy. Amazon now aims to increase cross sellingin the grocery segment.

What kind of analytical approaches could be implemented on the data to address the business problems and opportunities outlined above?

If this analytical project were approved, how might these approaches address the business problems?

![](https://github.com/chunziwang/whole-foods-market-basket-analysis/blob/master/figs/19.png)


## Dataset Overview

This dataset is comprised of 250,000 observations and 8 columns. The variables consist of:

- transaction_id
- product_id
- reorder - 1 means yes, 0 means no
- product_name
- aisle_id
- department_id
- department
- aisle

## Market Basket Analysis

### Find Bestsellers of all products

There're 23323 kinds of products in dataset. Groceries (fruits and vegetables) are the top 20.

![](https://github.com/chunziwang/whole-foods-market-basket-analysis/blob/master/figs/1.png)

### Find pattern in reordered items

There're large overlap of reordered items and bestsellers. Check the propability of each item being reordered.

Set the count threshold to 100 since we’re more interested in products that are more popular with the general public. This time, milk especially, and water, eggs, soda, coconut water, yogurt are the highest propability of reordered. Consider it beverage category. People who drink milk tend to drink it every day and refill it constantly.

![](https://github.com/chunziwang/whole-foods-market-basket-analysis/blob/master/figs/2.png)

Moreover, there’re more than 4000 kinds of products that’re 100% reordered but the total times they are bought are comparatively small. They serve niche market but the customers who bought them are extremely loyal.

![](https://github.com/chunziwang/whole-foods-market-basket-analysis/blob/master/figs/3.png)

Association between number of orders and probability of reordering, although some small countes of orders have high reordered rate, in general, there’s a upward trend that shows a high number of orders are naturally more likely ro be reordered.

![](https://github.com/chunziwang/whole-foods-market-basket-analysis/blob/master/figs/4.png)

### Visualize product porfolio

This graph shows the overall product porfolio this dataset holds.

![](https://github.com/chunziwang/whole-foods-market-basket-analysis/blob/master/figs/5.png)

How oftem are products from each department/aisle sold from the transaction data? It’s clear that produce and diary eggs are the top 2 departments of all the transactions.

![](https://github.com/chunziwang/whole-foods-market-basket-analysis/blob/master/figs/6.png)

This graph shows the count of products sold by aisle and department.

![](https://github.com/chunziwang/whole-foods-market-basket-analysis/blob/master/figs/7.png)

## Implement Association Rules

### Frequent items and itemsets

After transform the dataset into transaction object, we look at frequent items first.
Just like our exploratory analysis above, groceries are the most frequent single items here.

![](https://github.com/chunziwang/whole-foods-market-basket-analysis/blob/master/figs/8.png)

We then set the support to 0.08 (every 100 transactions, at least 8 times these items appear together) to look at the frequent itemsets. It looks like grocery items are oftem bought together, which makes sense.

![](https://github.com/chunziwang/whole-foods-market-basket-analysis/blob/master/figs/9.png)

### Use Apriori

At first, we use a low support threshold and a high confidence to generate strong rules even for items that are less frequent.

![](https://github.com/chunziwang/whole-foods-market-basket-analysis/blob/master/figs/10.png)

There’re some rules with a heavy lift indicating a strong association between the items. Further investigate those critical rules:

![](https://github.com/chunziwang/whole-foods-market-basket-analysis/blob/master/figs/11.png)

Different flavors of the same type of food have strong association between each other. Coffee creamer and pasta sauce has strong association towards chicken.

![](https://github.com/chunziwang/whole-foods-market-basket-analysis/blob/master/figs/12.png)

Now we increase the support and decrease condidence to get rules of some more frequent items but with less confidence.

![](https://github.com/chunziwang/whole-foods-market-basket-analysis/blob/master/figs/13.png)

![](https://github.com/chunziwang/whole-foods-market-basket-analysis/blob/master/figs/14.png)

It shows same type of items have high positive correlation.

![](https://github.com/chunziwang/whole-foods-market-basket-analysis/blob/master/figs/15.png)

Yogurt, fruits, and drinks are often bought together.

Finally, further increase support and decrease confidence.

![](https://github.com/chunziwang/whole-foods-market-basket-analysis/blob/master/figs/16.png)

![](https://github.com/chunziwang/whole-foods-market-basket-analysis/blob/master/figs/17.png)

Fruits and vegetables are highly correlated.

![](https://github.com/chunziwang/whole-foods-market-basket-analysis/blob/master/figs/18.png)

Lots of fruits. Banana is the most popular fruit among all.

## Cross Selling Strategies

+ Fruits + dairy + drinks could be sold together
+ Sauce + meat could be put closer in aisles
+ Different flavors of the same product have a strong association, so we could bundle two or three flavors of yougurts or crackers together and sell in large quantity and offer a deal
+ Put organic products in the prime spot on shelves since they have more margin
+ Link Amazon account and whole foods membership card together so we can track each grocery transactions to Amazon users and make customized recommendations.

