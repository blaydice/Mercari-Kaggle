"""
Loading data
"""
#loading libraries 
import numpy as np
import pandas as pd
##if you don't have them you need to install them, I had problems with numpy, so i think the best solution is to install anaconda, there are all this packeges built-in

#Reading CVS
## files need to be in the same folder as this script
train_df = pd.read_csv('train.tsv',  sep='\t')
test_df = pd.read_csv('test.tsv', sep='\t')
#for visualisation and better understanding
combine = [train_df, test_df]

# preview the data
train_df.head(10)
