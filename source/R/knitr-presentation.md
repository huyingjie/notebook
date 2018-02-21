# knitr&presentation

## general
show code: `echo`
show result: `eval`


## presentation example

### first slide exmple
```
adaptive design
========================================================
author: Yingjie Hu
date: 2017-12-18
autosize: true
transition: rotate
transition-speed: slow
```


## basic of presentation
no show title: `title: false`

float an image to the left or right: include it within a 2-column layouts

align left

```
![alt text](myimage.png)
***
```

Two Column Layouts `***`

```
Two-Column Slide
====================================
First column
***
Second column
```

By default the columns are split equally across the slide. 
`left: 70%`

## Slide Transitions
* default: linear: right-to-left animation

* `transition` style
    * none
    * linear
    * rotate
    * fade
    * zoom
    * concave

    globally: set a default transition style for the entire slide deck: include the transition field on the first slide of the deck. 
    
    a per-slide basis: set the transition on a slide-by-slide basis: include the transition field on individual slides.

* `transition-speed` (globally or on a per-slide basis)

    * default
    * slow
    * fast





```
Presentation Title
========================================
author: John Doe
date: February 15th, 2013
transition: rotate
```

## Slide Types

different slide type has different default appearance.

* section: use distinct background and font colors, have slightly larger heading text, and appear at a different indent level within the slide navigation menu.
* sub-section: use distinct background and font colors, have slightly larger heading text, and appear at a different indent level within the slide navigation menu.
* prompt: a distinct background color
* alert: a distinct background color

```
New Section
====================================
type: section

Prompt Slide
====================================
type: prompt
```



## Incremental Display `incremental: true` (global & per-slide)

```
My Slide
====================================
incremental: true
```
**Presentation: incremental not working in section and sub-section slides**

theses types of slides are only meant as 'heading' slides in between the content slides and are therefore not meant to display (incremental) content. 


* Headers
* paragraphs
* blockquotes
* code blocks
* list items 

are all shown incrementally

the first paragraph on any slide is always shown immediately

## limit navigation in `RStudio` window: `navigation: section`

* `none` — no slide navigation is possible
* `section` — users can navigate to sections only
* `slide`(default) — users can navigate to any slide

## Slide Links, i.e., hyperlinks to slides

1.  add an id field to a slide, e.g., `id: slide1`
2. add link `[Go to slide 1](#/slide1)`

```
Slide 1
====================================
id: slide1

Slide 2
====================================
[Go to slide 1](#/slide1)
```

## automatically open a source file `source`

```
My Slide
====================================
source: example.R
```

navigate to line 30 of a source file `source: example.R 30`

navigate to the first line that matches a regular expression: `source: example.R /loading data/`

## Displaying Presentations

1. Inline inside the RStudio IDE
2. In an external web browser

    `More -> View in Browser`
    
    
## Presentation Size Options

default: the maximum size they can be scaled to as well as the aspect ratio they are expected to be displayed at. 
    * a width of 960 pixels 
    * a height of 700 pixels. 

edit width and height

```
My Presentation
============================================
author: John Doe
width: 1440
height: 900
```

`autosize: true`: automatically adapts the size of the presentation to the size of the current pane it is being displayed in. This is especially helpful if you expect users to be viewing your presentation within the RStudio preview pane, which will have widely varying aspect ratios depending on the user's configuration.

## Distributing Presentations: save as a standalone web page

`More -> Save As Web Page`


MathJax for LaTeX equations: must include the files required by MathJax are copied to a folder that needs to be distributed along with the presentation HTML file. For example, if the saved presentation is named `MyPresentation.html` then the directory `MyPresentation_files` contains the MathJax supporting files.

## specify font `font-family`

default: Lato font

```
My Presentation
========================================
author: John Doe
font-family: 'Helvetica'
```
* The semantics of this are the same as for a CSS font-family (i.e. you can specify a comma separated list of alternate fonts).

* import web fonts from a custom URL: `font-import field`

    ```
    My Presentation
    ========================================
    author: John Doe
    font-import: http://fonts.googleapis.com/css?family=Risque
    font-family: 'Risque'
    ```


## Smaller Text `<small>text</small>`

## Custom CSS

* If a stylesheet within the same directory has the same name with presentation file name, stylesheet will be automatically imported. 

    `presentationFileName.css`

* external custom name of css

    ```
    My Presentation
    ===================================
    author: John Doe
    css: custom.css
    ```

* internal css in the presentation file

    place css at the top of the source above the title slide. any style tags included there will automatically be appended to the head element

## Applying Styles

* (apply a class to a filed) apply classes defined in CSS file to individual slides by adding a class field to the slide

    ```
    My Slide
    ===================================
    class: illustration
    ```
    
    ```
    My Slide
    ================================== 
    <span class="emphasized">Pay attention to this!</span>
    ```
    
* (apply a class to lots of fields) over the appearance of the (infrequently used) overstrike markdown syntax. 

    1. create a style for the `del` tag 
    2. adorn the spans of text with the `~~overstrike~~` delimiters.

    3. include some additional scopes in the CSS definition. 

    ```
    .reveal section del {
     color: red;
   }
    ```    
    
    ```
    ~~this text will be red~~
    ```
## Overriding Default Element Styles

change the default text color in paragraphs to blue you'd use:

```
.reveal section p {
  color: blue;
}

```

## Custom Slide Types

The default slide types of section, sub-section, prompt, and alert provide custom background colors and other styles on a per slide type basis. 

Slides are designated to be of a certain type using the type field. 

You can create a custom slide type by providing the appropriately scoped CSS. 

For example, here is the CSS for a custom slide type named exclaim that sets it's background to black and foreground text to white.

```
.exclaim .reveal .state-background {
  background: black;
} 

.exclaim .reveal h1,
.exclaim .reveal h2,
.exclaim .reveal p {
  color: white;
}

```

```
My Exclamation
========================================
type: exclaim
```

**the only way to customize the background color (or image) of a slide is to define a custom type.**

