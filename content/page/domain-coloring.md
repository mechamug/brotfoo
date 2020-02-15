---
title: Domain Coloring
comments: true
---

A really simple way to do domain coloring in Python.

![Domain Coloring](/brotfoo/img/domain-coloring1.png)
Domain coloring of the function $f(x) = \frac{sinc(z+i)}{tan(z-i)}$:

```Python
import numpy as np
import matplotlib.pyplot as plt

x,y = np.ogrid[-10:6:2560j, -10:10:1600j]
f = lambda z: np.sinc(z+i) / np.tan(z-i)
plt.imsave('graph.png', np.angle(f((x - 1j*y).T)), cmap='twilight')
```

## Another Example

![Domain Coloring](/brotfoo/img/domain-coloring2.png)