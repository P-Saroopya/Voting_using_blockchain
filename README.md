import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import plotly.express as px
import plotly.graph_objects as go
from plotly.subplots import make_subplots
from plotly.offline import init_notebook_mode
import seaborn as sns
import datetime as dt
import warnings
import os 
warnings.filterwarnings('ignore')
pd.set_option('display.max_columns',None)
init_notebook_mode(connected=True)
df = pd.read_csv("/kaggle/input/cryptocurrenciestoken-and-coin-platrform-support/dataset.csv")
df.head()
df.info()
df.isnull.sum()
df_list=df.columns.to_list()
for index, column in enumerate(df_list):
split_column = column.split("/")
if len(split_column) == 2:
   df_list[index] = split_column[1]
df.columns = df_list
df.iloc[:, 3:] = df.iloc[:3, 3:].notnull.astype(int)
df
counts = df.eq(!).sum()
sorted_counts = counts.sort_values(ascending=False)[:10]
ig = px.bar(sorted_counts, x=sorted_counts.index, y=sorted_counts.values)
fig.update_layout(title='Top 10 blockchain with the most Smart contract', xaxis_title='Blockchain', yaxis_title='Count')
fig.show()
df['sum'] = df.iloc[:, 3:].eq(1).sum(axis=1, numeric_only=True)
df = df.sort_values('sum', ascending=False)
top_10 = df.head(10)
#top 10 tokens with the most contract in different blockchain
top_10
fig = px.bar(top_10, x='sum', y='name', orientation='h')
# set plot title and axis labels
fig.update_layout(title='Top 10 Tokens with the most contracts in different blockchains', xaxis_title='Sum', yaxis_title='Name')
# display plot
fig.show()

​


      
        
        

