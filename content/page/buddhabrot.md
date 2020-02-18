---
title: The Buddhabrot
comments: true
---

This is a variation of what now is commonly called the Buddhabrot. As complex numbers are being iterated on through the Mandelbrot's recurrence relation, coordinates of intermediate complex numbers are marked, as opposed to only coloring points corresponding to their corresponding complex number's iteration count.

Someone had corrected me on Reddit, who I believe to have been the author of the great web site [Softology](https://softologyblog.wordpress.com/2011/06/26/buddhabrot-fractals/), that this is not the usual way the Buddhabrot is drawn, because I am including orbits of the proper Mandelbrot set, i.e. the interior. I will accordingly call this the "Anti-Buddhabrot" going forward.

> That is the "anti-buddhabrot". You want to skip orbits that start within the mandelbrot set to create a true buddhabrot.
>
> I have some tips here that may help https://softologyblog.wordpress.com/2011/06/26/buddhabrot-fractals/

<a href="/brotfoo/img/bb-nipy_spectral.png">
    <img src="/brotfoo/img/tm/bb-nipy_spectral.png" />
</a>

Here is some source code in Python to create it.

```Python
from numba import jit
from matplotlib.pyplot import imsave
from numpy import log, ones
from numpy.random import rand
from sys import argv

@jit
def bb(xl, xr, yl, yr, iw, ih, it=100, oc=4):
    '''
    Buddhabrot
    it: iterations
    oc: orbit coount per complex coordinate
    '''
    xd, yd = xr-xl, yr-yl
    xw, yh = iw/xd, ih/yd
    xo, yo = xd/iw/oc, yd/ih/oc
    im = ones((ih+1, iw+1))
    for xi in range(int(iw*oc)):
        for yi in range(int(ih*oc)):
            z = c = complex(xl + xi*xo, yl + yi*yo)
            for _ in range(it):
                if (abs(z) > 40): break
                z = z*z + c
                if z.real < xr and z.real > xl and z.imag < yr and z.imag > yl:
                    x = int((z.real - xl) * xw + rand())
                    y = int((z.imag - yl) * yh + rand())
                    if x >= 0 and x < iw and y >= 0 and y < ih:
                        im[y, x] += 1            
    return log(im)

if __name__ == '__main__':
    cm, sc = argv[1], 2
    im = bb(-1.5, 0.75, -1.25, 1.25, int(2650*sc), int(1600*sc))
    imsave(f'bb-{cm}.png', im, cmap=cm)
```

# Gallery

More examples. All examples are linked to higher resolution versions (around 5300×3200 in most cases).

## Twilight
<a href="/brotfoo/img/bb-twilight_r.png">
    <img src="/brotfoo/img/tm/bb-twilight_r.png" />
</a>

## Hot
<a href="/brotfoo/img/bb-afmhot.png">
    <img src="/brotfoo/img/tm/bb-afmhot.png" />
</a>

## Spectral
<a href="/brotfoo/img/bb-nipy_spectral.png">
    <img src="/brotfoo/img/tm/bb-nipy_spectral.png" />
</a>

## Cool & Warm
<a href="/brotfoo/img/bb-coolwarm.png">
    <img src="/brotfoo/img/tm/bb-coolwarm.png" />
</a>

## PuBu
<a href="/brotfoo/img/bb-PuBu.png">
    <img src="/brotfoo/img/tm/bb-PuBu.png" />
</a>

## Winter
<a href="/brotfoo/img/bb-winter.png">
    <img src="/brotfoo/img/tm/bb-winter.png" />
</a>

## Earth
<a href="/brotfoo/img/bb-gist_earth.png">
    <img src="/brotfoo/img/tm/bb-gist_earth.png" />
</a>

## HSV
<a href="/brotfoo/img/bb-hsv.png">
    <img src="/brotfoo/img/tm/bb-hsv.png" />
</a>

## Bone
<a href="/brotfoo/img/bb-bone.png">
    <img src="/brotfoo/img/tm/bb-bone.png" />
</a>
