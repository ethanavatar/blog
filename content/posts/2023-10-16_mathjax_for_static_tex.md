+++
title = "MathJax for Rendering TeX Statically"
draft = true
+++

Isn't it just the best when you're looking for math help online, and you find a site that renders TeX? Maybe its just me. But I got it working here anyway.

<!-- more -->

<!-- Include Polyfill to manage browser compatibility -->
<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>

<!-- Configure MathJax to look for your prefered wrapper symbols -->
<!-- Im using $ because thats what Obsidian uses -->
<script>
MathJax = {
  tex: {
    inlineMath: [['$', '$']]
  }
};
</script>

<!-- Include MathJax -->
<script type="text/javascript" id="MathJax-script" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
</script>

## Intro

I've quickly come to love TeX for displaying math symbols. A decent majority of my most used [Obsidian](https://obsidian.md/) notes are ones I made for either my high scool Calculus or Physics classes using inline TeX to display formulas and equations. I could never get into the groove of using full-on document typesetting solutions like LaTeX (through something like [Overleaf](https://www.overleaf.com)) or [typst](https://typst.app), as much as they intrigue me.

Obsidian's inline TeX strikes quite the nice balance between expressiveness and ease of use. Markdown is about as simple as it gets for writing text, and once I want to show something that I'd usually only be able to achieve in a kitchen sink editor like Word or a document typesetting solution like LaTeX, all I have to do is wrap it in some dollar signs and I'm good to go.

As far as I can assume, Obsidian uses [MathJax](https://www.mathjax.org/) for this capability. This is the same TeX rendering library that is used in tools like [Anki](https://apps.ankiweb.net/).

A cool thing about MathJax is that it can be included just like any other JavaScript library, and it will handle the typesetting for you. This is wonderful, because it means I can write blog posts just as I would write an Obsidian note, which would make it much easier to transfer my ideas to this site from where they already live.

## The Code

At the top of this very page, I have the following code:

```markdown
<!-- Include Polyfill to manage browser compatibility -->
<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>

<!-- Configure MathJax to look for your prefered wrapper symbols -->
<!-- Im using $ because thats what Obsidian uses -->
<script>
MathJax = {
  tex: {
    inlineMath: [['$', '$']]
  }
};
</script>

<!-- Include MathJax -->
<script type="text/javascript" id="MathJax-script" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
</script>
```

And just like that, I can use inline TeX on my static blog. No server-side rendering required.

```markdown
## The Kinematics Equations (Example)

1. $v_x=v_{x0}+a_xt$
2. $x=x_0+v_{x0}t+\frac{1}{2}a_x\Delta{t^2}$
3. $v_x^2=v_{x0}^2+2a_x\Delta{x}$
```

The snippet above becomes:

## The Kinematics Equations (Example)

1. $v_x=v_{x0}+a_xt$
2. $x=x_0+v_{x0}t+\frac{1}{2}a_x\Delta{t^2}$
3. $v_x^2=v_{x0}^2+2a_x\Delta{x}$

To see more examples, I made a whole nother post filled with trigonometric identities. It was pretty much copied verbatim from my Obsidian notes. You can find it and its source code in the previous post, [Trigonometric Identities](/posts/trig-identities/).

Or check out the source code for this page [here](https://github.com/ethanavatar/blog/blob/main/content/posts/2023-10-16_mathjax_for_static_tex.md).
