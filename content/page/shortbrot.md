---
title: Numpy Python Magic
comments: true
---

It's exciting how compact one can write generation of the mandelbrot in Python with NumPy.

```Python
import numpy as n
import matplotlib.pyplot as p
import functools as f
x,y=n.ogrid[-1:1:1000j,-1.5:1.5:1000j]
t=x-1j*y
p.imshow(n.angle(f.reduce(lambda z,_:z**2+t,[0]*1000,t)), cmap='twilight')
p.show()
```

## Pastel

Your reward, another Mandelbrot image.

![Folded Mandelbrot](/brotfoo/img/mandelbrot.png)