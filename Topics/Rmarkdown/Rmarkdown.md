Rmarkdown
================

Rmarkdown? You are looking at it!
---------------------------------

This very document you are reading right now is written using Rmarkdown, it's super easy and a very effective way to document and to present things. Basically, Rmarkdown is a R package that allows you to write files (.html, .doc, .pdf) from R straight away and embed R codes and analysis in them.

A major advantage over conventional writing tools such as Microsoft Doc is that Rmarkdown embeds R codes exactly the way they are, so that if you are to copy codes from a Rmarkdown file and run them in R, you don't have to make any change!

Another reason to use Rmarkdown is that it offers you the chance to run analysis inside a document, so that it basically allows you to print out your workflow from start to finish. This is good for both making your analysis reproducible and for illustrating to others (e.g. your supervisors) exactly what you did in R (and potentially what problems you ran into).

Installing and using Rmarkdown
------------------------------

Rmarkdown is superbly easy to learn and use, which cannot be said for most R-related things. To install Rmarkdown, simply install the package 'Rmarkdown' from your Rstudio:

``` r
install.packages("rmarkdown")
```

After the package is installed, you will be able to create new Rmarkdown files (typically with the suffix .rmd) and start writing them on your own. I found the easiest way to learn syntax and codes of Rmarkdown is by constantly referring to the cheatsheet <https://www.rstudio.com/wp-content/uploads/2016/03/rmarkdown-cheatsheet-2.0.pdf>, you will find everything you need there. If you have Rmarkdown package installed, you will even be able to call up this cheatsheet from Rstudio, by going to Help &gt; cheatsheets &gt; Rmarkdown Cheat Sheet.

I will not introduce the syntax of Rmarkdown further myself, the cheatsheet does it much better than me. The best way of learning Rmarkdown is just by using it, and it is really easy to use!

If you want more information on Rmarkdown, you could visit their [official website](http://rmarkdown.rstudio.com/) or search up "Rmarkdown" on the internet, there are plenty of helpful materials.

Demonstrating code chunks in Rmarkdown
--------------------------------------

For the rest of this topic, I'm going to demonstrate what embedded code chunks look like and what you could do with them in Rmarkdown. Since this is a Rmarkdown file, I could embed a code chunk straightaway:

``` r
###for demonstration, let's call the iris data again
iris <- iris
#let's tell R to print the first few values of iris
head(iris)
```

    ##   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
    ## 1          5.1         3.5          1.4         0.2  setosa
    ## 2          4.9         3.0          1.4         0.2  setosa
    ## 3          4.7         3.2          1.3         0.2  setosa
    ## 4          4.6         3.1          1.5         0.2  setosa
    ## 5          5.0         3.6          1.4         0.2  setosa
    ## 6          5.4         3.9          1.7         0.4  setosa
