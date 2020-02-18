---
title: The Folded Mandelbrot
comments: true
---

A variation on the Mandelbrot set, the folded Mandelbrot.

![Folded Mandelbrot](/brotfoo/img/foldedbrot1.png)

Try out this [Mandelbrot Viewer](https://asfdfsaf.github.io/mv/viewer.html). My gratitude goes to the original authors of the viewer and libraries.

```javascript
function countIterations(x, y) {
    var count = 0;
    var t = x;
    x=-y;
    y=t;
    var zx = x;
    var zy = y;
    var n = 100;
    var p = 200;
    while (count < maxIterations && zx*zx + zy*zy < 20) {
        if (0==(count+1)%n) {
            x += zx*count/p;
            y += zy*count/p;
            n--;
            p++;
        }
        var new_zx = zx*zx - zy*zy + x;
        zy = 2*zx*zy + y;
        zx = new_zx;
        count++;
    }
    var angle = Math.floor((Math.atan(zy/zx)+Math.PI/2)/Math.PI*count);
    return count < maxIterations ? count : angle;
}
```

## Spectral
![Folded Mandelbrot](/brotfoo/img/foldedbrot6.png)

## Alternative Coloration
![Folded Mandelbrot](/brotfoo/img/foldedbrot2.png)

## Red & Blue
![Folded Mandelbrot](/brotfoo/img/foldedbrot3.png)

## Burning
![Folded Mandelbrot](/brotfoo/img/foldedbrot4.png)

## Hot & Cold
![Folded Mandelbrot](/brotfoo/img/foldedbrot5.png)
