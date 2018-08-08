---
layout: post
title:  "Welcome"
date:   2018-05-07 15:19:37 -0400
categories: jupyter-notebook
---


```python
import torch
```

## this is the title 


```python
torch.rand(3,3)
```




    
     0.6722  0.4777  0.8250
     0.7353  0.7902  0.5744
     0.7334  0.1035  0.6565
    [torch.FloatTensor of size 3x3]




```python
import matplotlib.pyplot as plt
%matplotlib inline

import numpy as np

x = np.linspace(-5,5,1000)

sigmoid = lambda x:  np.exp(x) / ( 1 + np.exp(x))
tanh = lambda x: 2*sigmoid(2*x) - 1


plt.plot(x,sigmoid(x),label='sigmoid')
plt.plot(x,tanh(x),label="tanh")
plt.plot(x,tanh(x) * sigmoid(x),label="s * t")
plt.legend();
```


![png](output_4_0.png)
