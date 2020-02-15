---
title: The Julia Set
subtitle: Complex Areas
comments: true
---

This is an example of a graphical representation of the Julia set. Click for a higher resolution version.

<a href="/brotfoo/img/julia-Spectral_r1.png">
    <img src="/brotfoo/img/tm/julia-Spectral_r1.png" />
</a>

Here is some Python code to create it.

```Python
import numpy as np
import matplotlib.pyplot as plt
from os import system
from numba import jit
from numpy import random as nr
import sys

@jit
def julia():
    c = complex(-0.8,  0.156)
    s, rx, ry, t, it = 2, 3.5, 2.5, 1000, 150
    imx, imy = int(2650 * s), int(1600 * s)
    julia = np.zeros((imy, imx))
    for ix in range(imx):
        for iy in range(imy):
            z = complex(ix * rx/imx - rx/2, iy * ry/imy - ry/2)
            i = 0
            while abs(z) <= t and i < it:
                a = abs(z)
                z = z**2 + c
                i += 1
                julia[iy, ix] += 1
            julia[iy, ix] -= a/t * (1 - nr.rand())
    return julia

if __name__ == '__main__':
    cm = sys.argv[1]
    im = julia()
    plt.imsave(f'julia-{cm}.png', im, cmap=cm)
```