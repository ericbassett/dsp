[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)

# Exercise 5.1  
---
In the BRFSS (see Section 5.4), the distribution of heights is roughly normal with parameters μ= 178 cm and σ= 7.7 cm for men, and μ= 163 cm and σ= 7.3 cm for women.  
  
In order to join Blue Man Group, you have to be male between 5’10” and 6’1” (seehttp://bluemancasting.com).  What percentage of the U.S. male population is in this range?  Hint:  use **scipy.stats.norm.cdf**.\

# Imports
```python
import numpy as np
import pandas as pd
import thinkstats2
import nsfg
import thinkplot
from scipy.stats import norm
```
# Generate model, get answer, double-check model
```python
# Generate normal distribution model
male_height_norm = norm(loc=178,scale=7.7)

# Calculate blue man group upper/lower limits in cm
male_height_ll_cm = round((5*12+10)*2.54,1)
male_height_ul_cm = round((6*12+1)*2.54,1)

# Calculate percentile at or below lower limit
pct_blw_ll = male_height_norm.cdf(male_height_ll_cm)*100

# Calculate percentile at or below upper limit
pct_blw_ul = male_height_norm.cdf(male_height_ul_cm)*100

# Calculate percent in range
pct_blw_ul - pct_blw_ll

print(f'Percent of US males in height range for '+ 
          f'blueman group: {pct_blw_ul-pct_blw_ll:.3f} %')
print(f'Mean height: {male_height_norm.mean()}')
print(f'Std dev of height: {male_height_norm.std()}')
```
Percent of US males in height range for blueman group: **34.209 %**  
Mean height: 178.0  
Std dev of height: 7.7  
