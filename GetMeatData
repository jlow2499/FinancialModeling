# -*- coding: utf-8 -*-
"""
Created on Wed May  8 08:06:39 2019

@author: jlowh001
"""
import pandas as pd
import re
import numpy as np
import matplotlib as plt

file = 'https://www.ers.usda.gov/webdocs/DataFiles/51875/WholesalePrices.xlsx?v=6727.3'

dat = pd.read_excel(file,'historical')
headers = dat.iloc[0:3]

#col name routine to impute and clean
head = []
for i in range(headers.shape[1]):
    z=re.match('Unnamed',str(headers.columns.values[i]))
    if z: 
        val = np.NaN
    else:
        val = headers.columns.values[i].strip()
    head.append(val) 

df = pd.DataFrame({"A":head})   
df = df.ffill(axis = 0) 
head  = df.A.tolist()

#row two routine for imputation and cleaning
row1 = []
for i in range(headers.shape[1]):
    z=re.match('nan',str(headers.iloc[0,i]))
    if z: 
        val = np.NaN
    else:
        val = headers.iloc[0,i].strip()
    row1.append(val) 

df = pd.DataFrame({"A":row1})   
df = df.ffill(axis = 0) 
row1  = df.A.tolist()

#row three routine for imputation and cleaning
row2 = []
for i in range(headers.shape[1]):
    z=re.match('nan',str(headers.iloc[1,i]))
    if z: 
        val = np.NaN
    else:
        val = headers.iloc[1,i].strip()
    row2.append(val) 

df = pd.DataFrame({"A":row2})   
df = df.ffill(axis = 0) 
row2  = df.A.tolist()

#row three routine for imputation and cleaning
row3 = []
for i in range(headers.shape[1]):
    z=re.match('nan',str(headers.iloc[2,i]))
    if z: 
        val = np.NaN
    else:
        val = headers.iloc[2,i].strip()
    row3.append(val) 

df = pd.DataFrame({"A":row3})   
df = df.ffill(axis = 0) 
row3  = df.A.tolist()



newheaders = []

for i in range(headers.shape[1]):
    newheaders.append(head[i] + '; ' + row1[i] + '; ' + row2[i] + '; ' + row3[i])

dat.columns = newheaders

dat = dat.drop(dat.index[0:3])

columns = list(dat.columns.values) 
for col in columns:
    dat[col] = pd.to_numeric(dat[col], downcast='float',errors ='coerce')
    
dat[columns] = dat[columns].replace(0,None)


for col in columns:
    dat[col].fillna(dat[col].rolling(4,min_periods=1).mean())
    
    
plt.pyplot.plot(dat.index,dat.iloc[:,3])
