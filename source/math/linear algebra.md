---
title: Linear Algebra
description: Intuition
---

Reference:

* [3Blue1Brown linear algebra series](https://www.youtube.com/watch?v=kjBOesZCoqc&t=0s&index=1&list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab)


**3 distinct but related ideas about vectors**

* physics: vectors are arrows pointing in space. definition: length & direction. If length & direction of vectors are the same, even moving around vectors, they are still the same vectors
* cs: vectors are ordered lists of numbers.
* math: generalize both physics and cs


![](/figs/math/3 perspectives of vectors.png)

![](figs/math/vectors-physics.png)


transformation

* keep grid lines parallel and evenly spaced, not curve
* origion not changes


## [Toy example: 2d](https://www.youtube.com/watch?v=XkY2DOUCWMU&index=5&list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab)

* rotate 90 : $\left[ \begin{matrix} 0 & -1 \\\\ 1 & 0\end{matrix} \right]$

* sheer: $\left[ \begin{matrix} 1 & 1 \\\\ 0 & 1\end{matrix} \right]$

![](/figs/math/matrix-composition.png)

original: ![](/figs/math/transformation-original.png)

rotate 90: ![](/figs/math/transformation-rotate-90.png)

sheer: ![](/figs/math/transformation-sheer.png)


## [Toy example: 3d](https://www.youtube.com/watch?v=rHLEWRxRGiM&t=127s)

* rotate 90 degrees around y axis
$\left[ \begin{matrix} 0 & 0 & 1 \\\\ 0 & 1 & 0 \\\\ -1 & 0 & 0\end{matrix} \right]$
