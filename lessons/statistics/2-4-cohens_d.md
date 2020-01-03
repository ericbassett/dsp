[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

# Exercise 2.4
---
Using the variable **totalwgt_lb**, investigate whether first babies are lighter or heavier than others.  Compute *Cohen’s d* to quantify the difference  between  the  groups.   How  does  it  compare  to  the  difference  in pregnancy length?  

## Notes
---
Pregnancy length difference (**wks**):  
    38.601 *first* - 38.523 *other* = 0.078

Pregnancy length difference (**Cohen's d**):  
    0.029 *standard deviations*
    
```python
import numpy as np
import pandas as pd
import thinkstats2
import nsfg

#Read data file into 'preg' dataframe
preg = nsfg.ReadFemPreg()

#Get all live births
live = preg[preg.outcome == 1]

#Get all (not just full term) first and other live births 
first = live[live.pregordr == 1]
other = live[live.pregordr != 1]

#Print the difference in weight between first/other live births
print('Mean Weight')
print(f'First: {first.totalwgt_lb.mean():.2f} lbs')
print(f'Other: {other.totalwgt_lb.mean():.2f} lbs')
```

Mean Weight  
First: 7.20 lbs  
Other: 7.30 lbs  

```python
def CohenEffectSize(group1, group2):
    """Computes Cohen's effect size for two groups.

    group1: Series or DataFrame
    group2: Series or DataFrame

    returns: float if the arguments are Series;
             Series if the arguments are DataFrames
    """
    diff = group1.mean() - group2.mean()

    var1 = group1.var()
    var2 = group2.var()
    n1, n2 = len(group1), len(group2)

    pooled_var = (n1 * var1 + n2 * var2) / (n1 + n2)
    d = diff / np.sqrt(pooled_var)
    return d

#Compute Cohen Effect
cohen_d = CohenEffectSize(first.totalwgt_lb,other.totalwgt_lb)
print(f'Cohen effect size: {cohen_d:.3f}')
```
Cohen effect size: -0.069

# Conclusion
The difference in mean weight between first and other babies is -0.1 lbs, so first babies are lighter than other babies. Cohen's d is -0.069, so it is a small variation (0.069 standard deviations). Being born first has a small effect on weight, but it is still greater than the effect on pregnancy length.
