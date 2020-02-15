---
title: Cellular Automata
comments: true
---

<video controls autoplay width="100%" controls>
  <source src="/brotfoo/img/cellular.mp4" type="video/mp4">
</video>

```Python
import numpy as np
import matplotlib.pyplot as plt
from matplotlib.animation import FuncAnimation
from numpy import random as nr
import itertools as it
from numba import jit

fig, ax = plt.subplots()
xdata, ydata = [], []
S, N = 50, 100
im = nr.randint(0,N,(S,S))
ip = plt.imshow(im, interpolation='gaussian', cmap='hsv')

def cn(im, x, y):
    ni = 0
    for i,j in it.product(*([[-1,0,1]]*2)):
        if abs(im[(x+i)%S, (y+j)%S] - (im[x,y])) < 7:
            ni += 1
    return ni

def update(_):
    for x in range(S):
        for y in range(S):
            ni = cn(im, x, y)
            if ni >= 3:
                im[x,y] = (im[x,y] + 1)%N
    ip.set_data(im)
    return ip,

ani = FuncAnimation(fig, update, blit=True)
plt.show()
```