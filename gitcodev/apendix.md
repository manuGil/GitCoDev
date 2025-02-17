# Appendix: Formatting conventions

This website uses the [Jupyterbook Theme](https://jupyterbook.org/en/stable/basics/organize.html) for rendering content. The following conventions are used to organise and format content.

```{margin} An optional title
My margin content
```

## Lessons


### Instructor's Notes
Lessons may include explanations or instructions for the instructor. Use the following admonition for including *instructor's notes*:

```
:::{admonition} Instructor's Note 
:class: tip
*The content*
:::
```
Rendered as:

:::{admonition} Instructor's Note 
:class: tip
*The content*
:::

### Figures

Figures shall include a caption. The size of the can be controled by adjusting the value for `height`.

````
```{figure} ../img/teaching-approach.png
---
height: 400px
name: approach-fig
---
A visual representation of the teaching approach used to build self-reliance across the lessons.
```
````

```{figure} ../img/teaching-approach.png
---
height: 400px
name: approach-fig
---
A visual representation of the teaching approach used to build self-reliance across the lessons.
```

## Exercises




