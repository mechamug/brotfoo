---
title: Conjugate Julia Set
comments: true
---

<a href="/brotfoo/img/conjugate-julia.png">
    <img src="/brotfoo/img/tm/conjugate-julia.png" />
</a>


A very simple idea, rendering the Julia set of a point and its complex conjugate in the same picture, overlayed.

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

            z = complex(ix * rx/imx - rx/2, iy * ry/imy - ry/2)
            i = 0
            while abs(z) <= t and i < it:
                a = abs(z)
                z = z**2 + np.conj(c)
                i += 1
                julia[iy, ix] -= 1
            julia[iy, ix] -= a/t * (1 - nr.rand())
    return julia

cm = sys.argv[1]
plt.imsave(f'julia-{cm}.png', julia(), cmap=cm)
```