# Goal
  
A single file that builds two notebooks, one with R code chunks, one with python code chunks. Probably will eventually want the doc with R chunks as .qmd and with Python chunks as .ipynb
  
## Idea

Use `.qmd` along with conditional code chunks using profile variable to build two `.ipynb`s, then convert the R one to `.qmd`


```{.bash filename="Terminal"}
# get R version in `_r/master.ipynb`
quarto render
quarto convert _r/master.ipynb

# get Python version
quarto render --profile python
quarto convert _python/master.ipynb 
```

### Doesn't quite work

Python looks fine:

````
---
title: Example
jupyter: python3
---


## Python


```{python}
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

mpg = sns.load_dataset('mpg')
sns.scatterplot(data=mpg, x='displacement', y='mpg')
plt.show()
```
````

R has a `jupyter` engine set, and uses the wrong language for the code chunks:

````
---
title: Example
jupyter: python3
---


## R


```{python}
library(ggplot2)
ggplot(mpg, aes(displ, cty)) +
  geom_point()
```

````
