
""" loading libraries """
import numpy as np
import pandas as pd
#doing so now we can call plt.plot instead of plt.pyplot.plot
import matplotlib.pyplot as plt
#scikit learn is a huge library so we should only lead parts that we need, but for now I'm gonna leave whole
import sklearn as skl
%matplotlib inline


##if you don't have them you need to install them, I had problems with numpy, so i think the best solution is to install anaconda, there are all this packeges built-in

"""Reading CVS"""
## files need to be in the same folder as this script
train_df = pd.read_csv('train.tsv',  sep='\t')
test_df = pd.read_csv('test.tsv', sep='\t')
#droping id column
train_df = train_df.drop(["train_id"], axis = 1)
test_df = test_df.drop(["test_id"], axis = 1)
#for visualisation and better understanding
combine = [train_df, test_df]


# preview the data
train_df.head(15)

# visualisation
plt.pyplot.hist(train_df.dropna() ["price"], 100)
#smaller range
plt.pyplot.hist(train_df.dropna() ["price"], 50, range = (0,150))

#share of products with price below 200$ 
number_of_products = train_df.price.dropna().count()
number_of_products_below200 = train_df [train_df.price.dropna() <200].count() ["price"]
number_of_products_below200/number_of_products
#we need to think what number should be the maximum one, maybe there are categoties with much higher prices

#number of products with NaN as a pirce
number_of_products /train_df.price.count()
#all products have price :)

#let's see what products have higher price than 500$
train_df [train_df.price > 500].head()
#mostly luxury products, but there are over 1000 of them, maybe they should not be skipped
#I think there are no fakes, as propably those records are transactions not offers
#the most expensive product is "NEW Chanel WOC Caviar Gold Hardware"


#compering means of products with brands and without
#plt.pyplot([train_df.isnull("brand_name")["price"].mean(), train_df.notnull("brand_name")["price"].mean()])
mean_brand =[0, 0]
std_brand = [0, 0]
#mean_brand[0] and std_brand [0] - without brand
mean_brand[0] =train_df.price[pd.isnull(train_df.brand_name)].mean()
mean_brand[1] =train_df.price[pd.notnull(train_df.brand_name)].mean()
std_brand[0] = train_df.price[pd.isnull(train_df.brand_name)].std()
std_brand[1] = train_df.price[pd.notnull(train_df.brand_name)].std()
plt.pyplot.bar(np.arange(2), mean_brand, yerr = std_brand, width = 0.35)

#number of brands 
len(train_df.brand_name.unique())

#just for you to take a look how construction looks like
meanNike = train_df [train_df.brand_name == "Nike"]

meanNike.price.mean()
