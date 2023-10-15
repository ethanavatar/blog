+++
title = "MathJax Example"
draft = true
+++

This is an example post showing the use of MathJax for inline TeX rendering

<!-- more -->

<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script>
MathJax = {
  tex: {
    inlineMath: [['$', '$']]
  }
};
</script>
<script type="text/javascript" id="MathJax-script" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
</script>

## Functions and Inverses

$\sin(\theta) = \frac{opposite}{hypotenuse}$ : $\csc(\theta) = \frac{hypotenuse}{opposite}$

$\cos(\theta) = \frac{adjacent}{hypotenuse}$ : $\sec(\theta) = \frac{hypotenuse}{adjacent}$

$\tan(\theta) = \frac{opposite}{adjacent}$ : $\cot(\theta) = \frac{adjacent}{opposite}$

## Periodicity

$\sin(\theta \pm 2 \pi) = \sin(\theta)$ : $\csc(\theta \pm 2 \pi) = \csc(\theta)$

$\cos(\theta \pm 2 \pi) = \cos(\theta)$ : $\sec(\theta \pm 2 \pi) = \sec(\theta)$

$\tan(\theta \pm \pi) = \tan(\theta)$ : $\tan(\theta \pm 2 \pi) = \tan(\theta)$

## Negations

$\sin(- \theta) = -\sin(\theta)$ : $\csc(-\theta) = -\csc(\theta)$

$\cos(- \theta) = \cos(\theta)$ : $\sec(- \theta) = \sec(\theta)$

$\tan(- \theta) = -\tan(\theta)$ : $\cot(- \theta) = -\cot(\theta)$

## Complements

$\cos(\theta) = \sin(\theta \pm \frac{\pi}{2})$ : $\sin(\theta) = \sin(\frac{\pi}{2} \pm \theta)$

$\cot(\theta) = \tan(\theta - \frac{\pi}{2})$ : $\tan(\theta) = \cot(\frac{\pi}{2} - \theta)$

$\csc(\theta) = \sec(\theta - \frac{\pi}{2})$ : $\sec(\theta) = \csc(\frac{\pi}{2} - \theta)$

## Supplements

$\sin(\pi - \theta) = \sin(\theta)$ : $\csc(\pi - \theta) = csc(\theta)$

$\cos(\pi - \theta) = -\cos(\theta)$ : $\sec(\pi - \theta) = -\sec(\theta)$

$\tan(\pi - \theta) = -\tan(\theta)$ : $\cot(\pi - \theta) = -\cot(\theta)$

## Pythagorean Identities

$$\cos^2(\theta) + \sin^2(\theta) = 1$$

This is essentially just the pythagorean theorem for a unit circle (vector magnitude of 1 unit):
$$x^2 + y^2 = 1$$

This is often used for the purpose of substitution. Ex:
$$\frac{1}{1 - \sin(\theta)} = \frac{1}{\cos(\theta)} = \sec(\theta)$$

These are also derived from the pythagorean theorem, but are a bit harder to remember.
$$\sec^2(\theta) = 1 + \tan^2(\theta)$$

$$1 + \cot^2(\theta) = \csc^2(\theta)$$

## Ptolemey's Identities (Angle Sum Formulas)

$\sin(\alpha + \beta) = \sin(\alpha) \cos(\beta) + \cos(\alpha) \sin(\beta)$
- This one can be thought of like $\sin = y_1 x_2 + x_1 y_2$ (separate like-components)
- Note: The addition symbol is preserved

$\cos(\alpha + \beta) = \cos(\alpha) \cos(\beta) - \sin(\alpha) \sin(\beta)$
- This one can be thought of like $\cos = x_1 x_2 - y_1 y_2$ (group like-components)
- Note: The addition symbol becomes subtraction
- Note: $\cos* - \sin*$; $x$ comes first

$\tan(\alpha + \beta) = \frac{\tan(\alpha) + \tan(\beta)}{1 - \tan(\alpha)\tan(\beta)}$
- Note: The top operator is the same
- Note: The bottom operator is flipped
- Note: $\cos* - \sin*$; $x$ comes first


$\sin(\alpha - \beta) = \sin(\alpha) \cos(\beta) - \cos(\alpha) \sin(\beta)$
- This one can be thought of like $\sin = y_1 x_2 - x_1 y_2$ (separate like-components)
- Note: The subtraction symbol is preserved

$\cos(\alpha - \beta) = \cos(\alpha) \cos(\beta) - \sin(\alpha) \sin(\beta)$
- This one can be thought of like $\cos = x_1 x_2 + y_1 y_2$ (group like-components)
- Note: The subtraction symbol becomes addition
- Note: $\cos* - \sin*$; $x$ comes first

$\tan(\alpha - \beta) = \frac{\tan(\alpha) - \tan(\beta)}{1 + \tan(\alpha)\tan(\beta)}$
- Note: The top operator is the same
- Note: The bottom operator is flipped
- Note: $\cos* - \sin*$; $x$ comes first

## Double Angle Formulas

$\sin(2 \theta) = 2 \sin(\theta) cos(\theta)$

$cos(2 \theta) = \cos^2(\theta) - \sin^2(\theta)$

&emsp;&emsp;&emsp;&emsp; $= 2 \cos^2(\theta) - 1$

&emsp;&emsp;&emsp;&emsp; $= 1 - 2 \sin^2(\theta)$

$\tan(2 \theta) = \frac{2 \tan(\theta)}{1-tan^2(\theta)}$

## Half Angle Formulas

$\sin(\frac{\theta}{2}) = \pm \sqrt{\frac{1 - \cos(\theta)}{2}}$

$cos(\frac{\theta}{2}) = \pm \sqrt{\frac{1 + \cos(\theta)}{2}}$
	  
$\tan(\frac{\theta}{2}) = \frac{\sin(\theta)}{1 + cos(\theta)}$

&emsp;&emsp;&emsp;&emsp; $= \frac{1 - cos(\theta)}{\sin(\theta)}$
  
