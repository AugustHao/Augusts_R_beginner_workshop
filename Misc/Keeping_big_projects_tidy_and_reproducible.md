Keeping big projects tidy and reproducible
================

I'm doing this topic early because it deals with habits and tips that are most useful if you start your project with them (in other words they are a pain to implement retroactively and it's not worth the trouble).

Why do I want to be tidy?
-------------------------

Cause your mum told you so.

In a seriousness tidiness will come in very handy when your project bloats in size and complexity (which often happens without you noticing it). You may often find yourself starting a new script because the old one had something bugged, then starting an even newer one cause the new one had something bugged and so on... What's more, you may often have chunks of your code that work and chunks that don't, and although you think you had been rather smart in keeping notes to yourself uisng the `#` key, over time you forget what bits work and what don't. Adding on to even that, you may sometimes find yourself highlighting and running different parts of a script to produce a particular analysis, and then forgetting which parts you have to run to do it at a later date. These are all problems that big and long-running projects tend to suffer.

While they are more or less issues of version control, neat and coherent code-writing habits will get you to start on the right foot. Remember, at the end of the day you want to have one or several bug-free scripts in your project folder, and you want to be able to reproduce your entire analysis by simply running them in the correct order (the package 'remake' is a fancy way to achieve absolute coding reproducibility but it has a rather steep learning curve so I won't cover it here). In the process of getting there, you may have written many scripts which only partly does the job or contains bugs. Keeping your project tidy and organised will help to minimise the logistic troubles of merging all the trying scripts into one final script (or if you don't have the habit of working in seperate scripts it will be a matter of deleting bad/useless lines in your script).

Write sourceable and freestanding scripts
-----------------------------------------

I found it always helpful to have a script that can be run from start to finish wihtout having to do anything to it myself. Such scripts do not require me to only run some bits and skip others, or to select and run seperate bits in a particular order. The benefits of this is that if I come back to the scripts from a hiatus, I don't need to rely or memeory or annotation to know what to do.

To check if your script is "freestanding", it is a good habit to just run it from start to finish with an empty environment after you finish writing it, and check if there is any error. It's often the small things that tend to be missed, such as loading a package or designating a working directory.

To run an entire script is also called 'source', which you can quickly do by clicking the "source" button next to "run" on your script window in Rstudio (if you are struggling with Rstudio interface check out the tutorial from Research Bazaar that I linked to in the homepage of this repository). If you want to be extra and do everything by code, just use the function `source(script.R)`.

Another benefit of having sourceable scripts is that you can directly import the result of one script into another by using the `source` function. Let's have an example:

Suppose that I have just written a script to crop and stack some raster file in a script called `help me idk how to GIS.R` (raster objects in R CANNOT be saved in .RData files as they only exist in temporary storage, so you cannot simply save the result raster stack in a .RData file), and now I want to use this raster stack for some other analysis in a script called `pretending i can model.R`, you can do so by using `source` in `pretending i can model.R`:

``` r
source("your project directory/scripts/help me idk how to GIS.R")
```

And then you should have your raster stack ready in your environment! Note that the directory is important because `source` will try to load the script from where it is saved so you need to get it right.

As a bonus, running a script using source will not clog up your console window as by default it will not copy codes you've run into the console window. However you can change with the parameter `echo` in `source`, e.g. `source("your script.R", echo = TRUE)`.

Keeping utility and function scripts
------------------------------------

Once you are used to working with different scripts, it is often a good idea to have a "utility" script containing some commands you may need or use in other scripts, such as loading a particular data directory, loading a set of packages, or some functions to keep your workspace tidy. You can find a very superficial example of a utility script (which I use often) in the same folder as this document.

Your own functions are another group of things that are neat to keep in a seperate script. I know I haven't touched on function writing but I will get to it soon. Why is it good to keep functions in a seperate script? Because the codes used for defining functions tend to be very long and confusing to look at, so you may not want to define the function everytime you need it in a new script. Therefore, I recommend defining functions in a script that contains just the function definition, and load the functions by sourcing the scripts.

More on reproducibility
-----------------------

Reproducibility is like protected sex, everyone says they are all for it but we never know how many people actually puts it to practice. And frankly it makes sense as making an entire analysis reproducible does require considerable planning and foresight, and making something reproducible after completing it in a non-reproducible way is sometimes close to impossible. If you are ever concerned about someone actually trying to run your codes again, here are some tips that may help:

### RNG

Random Number Generator is regularly used in coding as it is in Dungeons and Dragons (if only I had friends I would play it), fortunately we can actually reproduce many instances of randomness in R. How? Because as good as computers are they can't actually roll a dice, they are machines with fixed rules and algorithms, which prevents generation of actual randomness. Because of this most modern computers actually can only generate numbers that have property of randomness (being independent from the previous number in the sequence) but are actualy deterministic. This means we can actually 'control' random numbers in R by designating a 'starting point' for RNG. This is known as a 'seed' and its associated R function is `set.seed()`, which you can put above a line that has some elements of randomness.

As an example, here I will set the seed to be 1 then ask R to give me a random number generated by a standard normal distribution:

``` r
set.seed(1)

rnorm(1)
```

    ## [1] -0.6264538

try running the same code in your R, you should get exactly the same number.

### One script to source them all

Suppose that you have finally completed all your coding and now have a number of scripts that are sourceable and bug-free, you could tidy it up even further by having a 'master script' in which you source them all in the right order, for example:

``` r
#run this script to fully reproduce analysis
setwd("working directory")
source("data prep.R")
source("modelling.R")
source("evaluation.R")
source("predictions.R")
```

Having a master script like this reduces the effort of re-running the analysis and makes it easier for someone else to reproduce your project. Most of all, after your ego and confidence are thoroughly destroyed by the purgatory that is a R project, it helps to to provide a sense of pride and accomplishment for sourcing different scripts.
