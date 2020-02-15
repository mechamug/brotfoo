---
title: Cellular Automata
comments: true
---

<video controls autoplay width="100%" controls>
  <source src="/brotfoo/img/cellular.mp4" type="video/mp4">
</video>

I am using a variation of a cellular automaton rule I found on [Softology's blog post on cellular automata](https://softologyblog.wordpress.com/2020/01/24/alternating-neighborhoods-cyclic-cellular-automata/). He uses the neighboring states and increments a cell's state if they exceed a configured threshold.

I was trying to use his update rule for automata with more states, but it would just stall out, because not enough states would match the rule. So, instead I thought I just use a larger range of differences for the surrounding states, but I am still only looking at surrounding cells. What also made a huge difference is that I let the rule wrap around, by using modulo, or else the pattern would just sweep up against the sides and dissipate. This way I can use way more states.

The colormap is being applied by pyplot automatically. I only pick the map and by default it will nicely spread out the colormap over the range of minimum and maximum values. If the maximum values are far, far higher than the rest, as with the Buddhabrot I had recently made (see same website), taking the logarithm or square of all values is a huge visibility improvement. The smooth transitions from spot to spot is due to the gaussian interpolation that PyPlot, too, can do for you. Turn it off and you will have a pixel grid. On top of that, numpy has vectorized versions of all those operations, so it's a breeze to use them and prototype new algorithms.

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
