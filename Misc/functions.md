Functions
================

Why functions and when to use functions
---------------------------------------

Functions in R are the building blocks of complex programming problems. Functions are essentially a whole chunk of code that you can reuse for different variables (or *arguments* to a function). Naturally, functions are most often used when you face a very complex problem, but they can be a bit redundant for smaller analysis. In my experience I rarely use functions, but when I do, they are irreplaceable. There is definitely a lot of value in learning to write functions, even when you don't use them on a day-to-day basis.

The basics of functions
-----------------------

All functions in R are defined in this form:

``` r
name <- function(argument1, argument2,...){
    expression1,
    expression2,
...
return(output)
}
```

Here, `name` is naturally the name of your function which you will use to call up later on. `argument1`, `argument2` etc are the names of variables which you *pass* to the function to be used in the `expressions` in the braces. You can see how it almost works just like loops/statements, with the exception that it has `arguments`. One important aspect/advantage of functions is that they come with their own *environment*, which means any variables you have defined **inside** the braces will not be present in your global environment, thus keeping your global environment tidy. The `return(output)` bit at the bottom tells R what you want out of your function. There are a few caveats about it: if you do not define return R will return the result of your last expression in the braces, and if you run a function without assigning it to a variable, the returned result will only be printed in your console, so remember to assign the output of a function! If you are interested on reading more about it check out [SpuR textbook, Chapt5](https://www-taylorfrancis-com.ezp.lib.unimelb.edu.au/books/9781420068740).

Example function: comparing predictor importance between a linear model and a Random Forest
-------------------------------------------------------------------------------------------

At this point you probably feel bamboozled, none of which I've said probably makes sense or feels useful. Don't worry, that's just my horrible teaching style, I promise functions tend to be more awesome than what I've described. To redeem functions to you, let's look at an example.

Suppose you have a data set at hand and you want to know if it contains any NAs and where these NAs are. You could do so by writing this simple function:

``` r
#we will load the library raster since I used some of its functions
library(raster)
```

    ## Loading required package: sp

``` r
#first we define our function: 
#the only argument is the dataset we put in
NA.detector <- function(dataset){
    #first we check if the input data is indeed in a dataframe, if not we will terminate the function
    if(is.data.frame(dataset) != T){return(cat("ERROR: your data is not in a data frame!"))}
    #second we build a vector to tally all the NAs and their row number
    NAs <- c() #define the vector
    for (n in 1:nrow(dataset)){
        if (any(is.na(dataset[n,]) == T)){NAs <- c(NAs,n)} 
        #if a row contains any NA, we note the row number in vector NAs
    }
    total.NAs <- length(NAs) #denote the total number of rows containing NAs
    #now we ask the function to return the result
    if (is.null(NAs) == T){
        return(cat("congrats your data is NA free!"))
    }else{
        return(cat("oops your data has ",total.NAs,"rows containing NAs! They are located at row numbers: ",NAs,"\n"))
    }
} #done!

#let's test this:

#first we make a matrix containing NAs to see if the function recognise that it is not in a dataframe

test.matrix <- matrix(data = c(rnorm(10),NA,1:9,NA,NA,runif(3)),nrow = 5, ncol = 5)

#we run it through the function

NA.detector(test.matrix)
```

    ## ERROR: your data is not in a data frame!

``` r
#as expected, this did not work
#now we convert the matrix to a data frame, and check again

test.df <- as.data.frame(test.matrix)
#check our dataframe
test.df
```

    ##           V1          V2 V3 V4        V5
    ## 1  0.5792589 -0.16521579 NA  5        NA
    ## 2  0.5480710 -0.30282053  1  6        NA
    ## 3  1.4943424 -0.48227939  2  7 0.9190268
    ## 4 -0.2215238  2.17026511  3  8 0.2024637
    ## 5  0.2589710  0.01963002  4  9 0.5776992

``` r
#run it through our function
NA.detector(test.df)
```

    ## oops your data has  2 rows containing NAs! They are located at row numbers:  1 2

``` r
#now it's working properly!

#let's test it on a bigger, more real-life like dataset. we will use airquality which is provided in R

#let's take a peek at airquality

head(airquality)
```

    ##   Ozone Solar.R Wind Temp Month Day
    ## 1    41     190  7.4   67     5   1
    ## 2    36     118  8.0   72     5   2
    ## 3    12     149 12.6   74     5   3
    ## 4    18     313 11.5   62     5   4
    ## 5    NA      NA 14.3   56     5   5
    ## 6    28      NA 14.9   66     5   6

``` r
#run it through the function
NA.detector(airquality)
```

    ## oops your data has  42 rows containing NAs! They are located at row numbers:  5 6 10 11 25 26 27 32 33 34 35 36 37 39 42 43 45 46 52 53 54 55 56 57 58 59 60 61 65 72 75 83 84 96 97 98 102 103 107 115 119 150

``` r
#you can quickly see why functions are useful: 
#I did not have to repeatedly write out two chunks of codes for testing two datasets
#instead, using the function I only had to switch the argument: 
#in this way the function is much more efficient


#now that we have identified the NAs, let's write another function to remove them:

NA.removal <- function(dataset){
    #make a vector to record the rows that contain NAs just as before
    NAs <- c()
    for (i in 1:nrow(dataset)){
        if (any(is.na(dataset[i,]) == T)){
            NAs <- c(NAs,i)
        }
    }
    #take out all of these rows
    dataset <- dataset[-NAs,]
    return(dataset)
}

#we test it on airquality

airquality.noNAs <- NA.removal(airquality) 
#note I am assigning the output of the function to a new variable under the name airquality.noNAs

#now we test again if the new dataset has NAs

NA.detector(airquality.noNAs)
```

    ## congrats your data is NA free!

``` r
#our second function worked!
```

Hope that was enough to demonstrate how to use functions in R!
