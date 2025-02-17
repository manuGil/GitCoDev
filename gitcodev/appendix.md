# Appendix: Formatting conventions

This website uses the [Jupyterbook Theme](https://jupyterbook.org/en/stable/basics/organize.html) for rendering content. The following conventions are used to organise and format content.


## Lessons


### Learning Objective

Use a `card` at the begining of each lesson to state the learning objectives:


````md
:::{card} Learning Objectives:

* Ojbective 1
* Objective 2

+++
Materilas:

* A list of additional materials related to the lesson for the instructor. 
* For example: slides.

:::
````

Rendered as:

:::{card} Learning Objectives:

* Ojbective 1
* Objective 2

+++
Materials:
* *[Collaborative software development](https://docs.google.com/presentation/d/1yBy_4r9aHhsUH9AH1s7zLWIQ_h20xNKVYM1somPnz1Q/edit?usp=sharing)*
:::



### Instructor's Notes
Lessons may include explanations or instructions for the instructor. Use the following admonition for including *instructor's notes*:

```md
:::{admonition} Instructor's Note 
:class: tip
*The content in italics*
:::
```
Rendered as:

:::{admonition} Instructor's Note 
:class: tip
*The content in italics*
:::

### Figures

Figures will be numbered and shall include a caption. The size of the can be controled by adjusting the value for `height`.

````md
```{figure} ../img/teaching-approach.png
---
height: 400px
name: approach-fig
---
Caption
```
````
Example:

```{figure} ../img/teaching-approach.png
---
height: 400px
name: approach-fig
---
Caption
```

### Lesson's Ecercises

Exercises within a lesson are shown using a `card`, as follows:

````md
:::{card} 
Exercise 1 
^^^    

```
{include} exercises/L3-ex01.md
```
:::
````

Exercises are numbered for each lesson, starting at one. The header of the lesson includes the word *Exercise* and the number of the exercise. The body of the card contains a reference to the file that describes the exercise.  


## Exercises

Excercises are organize in files, each file  contains the following parts:

* A title mentioning the lesson and the episode. 
* The time required to complete the exercise.
* A list of tasks or instructions 
* Admonistions, figures, etc. (optional)
* The answers to the exercise. If the exercise has no answers, that is stated by writting `No answers are provided for this exercise` 


Example:

````md
# Lesson 3 Episode 1 --- Clone a reposiory and make a contribution 

**Time: 10 min**

Please perform the following tasks individually.

1. Clone the Check-in repository via SSH: https://github.com/manuGil/check-in
1. Make a copy of the file `check-in/template.md` in the same directory; 
1. Open your copy of `template.md` and add something to the lists in the file.
1. Commit your changes, and push them to the remote repository. 
1. Reflect on the difficulties you faced, and how we might avoid them.

```{admonition} Instructor's Note
While completing this exercise, many participants will be warned by Git that they have to pull changes before pushing their contribution. 
This situation should be used as a pre-amble to [branching](branching).
```

```{dropdown} Answers

    No answers are provided for this exercise.

```
````



