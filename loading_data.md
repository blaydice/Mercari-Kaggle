
# Loading data

# loading libraries 
import numpy as np
import pandas as pd
import matplotlib as plt
%matplotlib inline
###if you don't have them you need to install them, I had problems with numpy, so i think the best solution is to install anaconda, there are all this packeges built-in

# Reading CVS
##files need to be in the same folder as this script
train_df = pd.read_csv('train.tsv',  sep='\t')
test_df = pd.read_csv('test.tsv', sep='\t')
#droping id column
train_df = train_df.drop(["train_id"], axis = 1)
test_df = test_df.drop(["test_id"], axis = 1)
#for visualisation and better understanding (but we wil see :p)
combine = [train_df, test_df]

# preview the data
train_df.head(10)

# visualisation
plt.pyplot.hist(train_df.dropna() ["price"])
#smaller range
plt.pyplot.hist(train_df.dropna() ["price"], range = (0,100))
