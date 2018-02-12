---
title: Differential
description: 
---

## definition

* $c$: constant
* $f, g$: function
* $x$: a variable
## rules

* Linear

	$(cf)' = cf'$
	
	$(f + g)' = f' + g'$
	
* product: $(fg)' = f'g + fg'$
* $\frac{1}{f} = \frac{-f'}{f^2}$
* $\left (\frac{f}{g} \right)' = \frac{f'g - fg'}{g^2}, g \neq 0$
* $(f o g)' = (f' o g)g'$
* $(f^{-1})' = \frac{1}{f' o f^{-1}}$
* $(f^g)' = f^g \left ( g' \mathrm{ln}f+\frac{g}{f} f' \right )$

## basic function

* $c' = 0$
* $x' = 1$
* $(cx)' = c$
* $|x|' = \frac{x}{|x|} = \mathrm{sgn}x, x \neq 0$
* $(x^c)' = cx^{c-1}$
* $\left ( \frac{1}{x} \right )' = \left ( x^{-1} \right)' = -x^{-2} = -\frac{1}{x^2}$
* $\left ( \frac{1}{x^c}\right)' = \left ( x^{-c} \right)' = \frac{1}{2}x^{-\frac{1}{2}} = \frac{1}{2\sqrt{x}}, x>0$ 

## logarithm and exponentials

* $(c^x)'=c^x \mathrm{ln}c, c>0$
* $(e^x)'=e^x$
* $(log_c x)' = \frac{1}{x\mathrm{ln}c}, c>0, c \neq 1$
* $(\mathrm{ln}x)' = \frac{1}{x}, x>0$
* $(\mathrm{ln}|x|)' = \frac{1}{x}$
* $(x^x)' = x^x(1+\mathrm{ln}x)$

## triangle function

$(\sin x)'=\cos x$|$(\arcsin x)' = \frac{1}{\sqrt{1-x^2}}$
---|---
$(\cos x)'=-\sin x$|$(\arccos x)' = -\frac{1}{\sqrt{1-x^2}}$
$(\tan x)' = \sec ^2x=\frac{1}{\cos ^2 x}$|$(\arctan x)' = \frac{1}{1+x^2}$
$(\sec x)' = \sec x \tan x$| $(\mathrm{arcsec} x)' = \frac{1}{\vert x \vert \sqrt{x^2-1}}$
$(\csc x)' = -\csc x \cot x$| $(\mathrm{arccsc} x)' = -\frac{1}{\vert x \vert \sqrt{x^2-1}}$
$(\cot x)' = - \csc^2 x = - \frac{1}{\sin ^2 x}$|$(\mathrm{arccot} x )'= - \frac{1}{1+x^2}$


$(\sinh x)' = \cosh x = \frac{ex^x+e^{-x}}{2}$| $(\mathrm{arsinh} x)' = \frac{1}{\sqrt{x^2+1}}$
---|---
$(\cosh x)' = \sinh x = \frac{e^x - e^{-x}}{2}$|$(\mathrm{arcosh} x)' = \frac{1}{\sqrt{x^2-1}} (x>1)$
$(\tanh x)' = \mathrm{sech}^2 x $|$(\mathrm{artanh}x)' = \frac{1}{1-x^2} (\vert x \vert <1)$
$(\mathrm{sech} x)' = - \mathrm{tanhx} \ \mathrm{sech} x$|$(\mathrm{arsech} x)' = -\frac{1}{x\sqrt{1-x^2}}$
$(\mathrm{csch} x)' = - \mathrm{coth} x \ \mathrm{csch} x$|$(\mathrm{arcsh} x)' = -\frac{1}{x\sqrt{1+x^2}}$
$(\coth x)' = -\mathrm{csch} ^2 x$|$(\mathrm{arcoth}x)' = \frac{1}{1-x^2}(\vert x \vert > 1)$


