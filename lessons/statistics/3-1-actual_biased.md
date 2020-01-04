[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)
# Exercise  3.1  
---
Something  like  the  class  size  paradox  appears  if  you  survey children and ask how many children are in their family.  Families with many children are more likely to appear in your sample, and families with no children have no chance to be in the sample. Use the NSFG respondent variable **NUMKDHH** to construct the actual distribution for the number of children under 18 in the household. Now compute the biased distribution we would see if we surveyed the children and asked them how many children under 18 (including themselves) are in their household. Plot  the  actual  and  biased  distributions,  and  compute  their  means.   As  a starting place, you can use **chap03ex.ipynb**

# Setup
```python
import numpy as np
import pandas as pd
import thinkstats2
import nsfg
import thinkplot
import probability
```
# Import data
```python
resp = nsfg.ReadFemResp()
```

# Define bias function
```python
def BiasPmf(pmf, label):
    new_pmf = pmf.Copy(label=label)
    
    for x, p in pmf.Items():
        new_pmf.Mult(x, x)
    new_pmf.Normalize()
    return new_pmf
```

# Plot PMFs
```python
#Create histogram for numkdhh response frequencies
numkdhh_hist = thinkstats2.Hist(resp.numkdhh)

#PMF the histogram and make sure total probability == 1.0
numkdhh_pmf = thinkstats2.Pmf(numkdhh_hist, label='unbiased')
assert numkdhh_pmf.Total() == 1.0

#Compute the biased pmf you would get from asking kids
numkdhh_biased_pmf = BiasPmf(numkdhh_pmf,label='biased')
assert numkdhh_pmf.Total() == 1.0

#Set up two plots colors, generate and show plot
thinkplot.PrePlot(2)
thinkplot.Pmfs([numkdhh_pmf,numkdhh_biased_pmf])
thinkplot.Show(xlabel='kids', ylabel='PMF',width=1)
```
![alt text](https://github.com/ericbassett/dsp/blob/master/img/numkdhh_pmf.png "NUMKDHH PMF")

# Calculate Means
```python
#Calculate means
print(f'Unbiased mean: {numkdhh_pmf.Mean():.2f}')
print(f'Biased mean: {numkdhh_biased_pmf.Mean():.2f}')
```
Unbiased mean: 1.02  
Biased mean: 2.40


