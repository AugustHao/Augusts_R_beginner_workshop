Loops
================

'for', 'if', and 'while'
------------------------

When I first encountered 'for's and 'if's followed by a whole lot of lines in brackets, I thought to myself that I will never be smarter enough to write something like that. Turns out I was only half right: I'm still as dumb as I thought I was, but these 'if's and 'for's aren't that difficult themselves. If I can do it, so can you!

### What are they for?

The `if` statement, and `for` and `while` loops are essentially built-in R functions intended for simplifying your codes. They allow you to implement 'logic' to your codes which often spares you from writing out repeating codes yourself, thus reducing the time you spend coding tremendously (this [R-blogger article](https://www.r-bloggers.com/how-to-write-the-first-for-loop-in-r/) has a good example of it). I also find statements (technically people more often refer to `if` and `while` as 'loops' but here I will use them interchangeably) helpful in habituating me to a 'programming-friendly' way of logic. By which I mean it forces me to break down my task into logical questions that can be represented by statements: **what** action do I want to apply to **which** objects? Are these actions repeats of each other? Do I need to branch out into **either** one situation **or** the other? Is there some condition I want to fulfill before I execute an action? and so on.

### Are they worth learning?

I often find myself asking these two questions about new R skills: how likely is it I will use it? Is it worth the time and effort put into learning it? With statements, I think the answer is: there is no guarantee that you will use it and often there are other ways to get around a problem without using loops (which are typically better than loops), BUT they are very easy to learn and master. Personally I think they are a good skill to learn, just so that you know in the back of your mind that you have them at your disposal if you ever come across a problem that you can use loops for (again goes back to thinking habit, it helps me to understand a problem by just thinking that "oh I can use loops for this").

In the following sections I will briefly introduce the `if`, `for`, and `while`, and demonstrate superficially how you can use them. Again there are much better and more detailed resources out there; if you would like to read up more on statements one particular resource I found very helpful is again in the [SpuR textbook, Chapt3](https://www-taylorfrancis-com.ezp.lib.unimelb.edu.au/books/9781420068740) which contains very detailed explanation of loops and some good exercises too. For copyright reasons I will not attach that here but it's available online through the link above if you have a Unimelb account.

IF statements
-------------

`if` statements are self-explanatory: **IF** one thing happens, do this, **otherwise**, do that. It's very easy to implement this 'logical branching' in R, one just have to write:

``` r
if (logical expression){
    expression#1
    expression#2
    ...
}
```

To break down the codes above: `if` is the name of the function so that R knows you are writing a `if` statement. Following `if` in brackets `()` is `(logical expression)`, which is a R expression that evaluates to a result of the type *logical* (also called *boolean*, if you are unfamiliar with data type check out Topic 4 *Basic data cleaning and preparation*). What this means is that `(logical expression)` is either `TRUE` or `FALSE`. Following the `(logical expression)` we have more expressions in braces `{}`. This is where you tell R what to do if `(logical expression)` turned out to be `TRUE`. A minor note: if you are only writing one expression after `(logical expression)` you don't need the braces, but I recommend always putting it in so that your code is easier to read.

As an extension, you can also tell R what to do when the logical expression is FALSE by including a second ground of expressions following `else`:

``` r
if (logical expression){
    expression#1
    expression#2
    ...
}else{
    expression#3
    expression#4
    ...
}
```

In the codes above, R will execute the second group of expressions if the logical expression turned out to be wrong. You can naturally see from here that the logical branching can go on and on by including more and more `if` statements inside one another, which is called "nesting" and we will talk about it later.

One warning though, when you write `else` you must make sure it is on the same line as the closing brace `}`. This is because if you start `else` on a new line R will think your `if` statement has already finished and it won't know what to do with your `else` part. For example the code below will give you an error:

``` r
if (logical expression){
    expression#1
    expression#2
    ...
}
else{
    expression#3
    expression#4
    ...
}
```

Feeling lost? Don't worry! `if` is hard to explain with words, so let's check out an example:

Suppose one of you is very kind and decide to surprise me with a kitten as a birthday gift (totally not hinting here). You told me there is a kitten waiting for me at home and the kitten is either calico or tabby. Now being the nerd I am I decide to guess the colour of the kitten by flipping a coin, essentially assigning 50/50 chance of the kitten being of either colour. We can represent my guess using a `if` statement:

``` r
#to "guess" the colour of the kitten I need to first flip a coin, I can "flip a coin" in R by generating randomly 1s and 0s, here I will use a uniform distribution for it

if (runif(1) <0.5){#runif(1) has 50% chance of being below 0.5, just like getting a tail on a coin toss. The statement runif(1) <0.5 is logical because I am asking R "is it true that runif(1) is less than 0.5?". You can verify if the statement is logcial by copying and running it in your console, and you should get either "TRUE" or "FALSE"
    cat("the kitten is","calico","\n")#here I am asking R to print the words "the kitten is calico " if my random number runif(1) is less than 0.5
}else{
    cat("the kitten is","tabby","\n")
}
```

    ## the kitten is tabby

There are several things in the codes above you might have not seen before, don't worry, they are not relevant to statement writing: `runif` (stands for "R-uniform distribution", not "run if") is a function that generates a random number from a uniform distribution (by default from 0 to 1). Here I used `runif(1)` to give me 1 random number. The `cat` function is just for printing out the texts in console window, I swear I didn't make up this entire scenario just because the function is called `cat`. Remember if you are unfamiliar with R functions you can always look it up by typing `?functionname` in the console window.

I hope this is sufficient in helping you understand `if` statements, once again if you would like more detailed resources check out the book I linked above!

FOR loops
---------

Now that you have seen the `if` structure, `for` and `while` should be relatively easy to follow. Let's start with the more frequently used `for` loop. `for` loops are most often used to repeat an action to a number of different objects. `for` loops follow the basic structure of:

``` r
for (x in vector){ #note that it doesn't have to be x, it can be a variable with any legitimate name
    expression#1
    expression#2
    ...
}
```

When a `for` loop is run, it executes the expressions in braces once for each element in the vector. Let's see an example of it:

Let's suppose I want to express my love for all cats by declaring "ginger/calico/tortoiseshell/etc. cats are awesome" but I can't be bothered to write out that declaration so many times, here is what I can do:

``` r
#first we make a vector of cat coat colours with a length of 5
cat_colour <- c("calico","ginger","tabby","tortoiseshell","all")


for (x in 1:5){ #the cat colour vector has length of 5 so we are counting from 1 to 5 (1:5 generates a string of numbers 1,2,3,4,5)
    cat(cat_colour[x],"cats are awesome","\n")#im asking R to print a concatenation of the x-th words in the cat_colour vector, and the words "cats are awesome"
}
```

    ## calico cats are awesome 
    ## ginger cats are awesome 
    ## tabby cats are awesome 
    ## tortoiseshell cats are awesome 
    ## all cats are awesome

As seen above by using `for` loop I easily repeated the declaration 5 times without having to type it out myself. For this case `for` loop didn't seem to have helped a lot, but when you have hundreds and thousands of things to run through, you'll easily see why for loops can be useful.

WHILE loop
----------

`while` loops are not used as often as `for` loops, but they can come in handy in certain situations. Basically `while` loops express the situation of "while this condition is met, do these things" or "do these things until this condition is no longer true". In practice they look like:

``` r
while (logical expression){
    expression#1
    expression#2
    ...
}
```

The `(logical expression)` is the condition to meet and when it is met R will execute the expressions in braces. Note that because the condition could potentially be TRUE all the time `while` loops can run indefinitely, so you want to plan out your loop carefully.

As an example, suppose I have a male cat and I love my cat so much I'm overfeeding him. As such my cat is gaining weight exponentially and quickly growing to be a ferocious beast. At weight of 200kg it will evolve into a tiger and eat me, so I need to figure out how long I get to survive. Let's suppose his weight grows by 110% every months, we can work out my survival using a while loop:

``` r
#we set the initial values for cat weight and time
look_at_this_fat_cat <- 4 #let's suppose the starting weight is 4kg
months_of_survival <- 0 #start counting at 0


while (look_at_this_fat_cat <= 200){
    look_at_this_fat_cat <- look_at_this_fat_cat*1.1
    months_of_survival <- months_of_survival + 1
}

cat("I will survive for",months_of_survival,"months","\n")
```

    ## I will survive for 42 months

So yeah, totally realistic scenario and useful application of `while` loops.

Nesting loops
-------------

I have touched on nesting before, which is basically putting one statement inside another, be it `if` `for` or `while`. Nested loops can get complex and hard to interpret but they are still just loops and there is nothing particularly fancy about them. I will just give a quick example here:

Suppose I became a crazy cat person and I have 4 pairs of cats, a male and a female each with coat colour "calico","ginger","tabby", or "tortoiseshell". I can quickly write out my cat colour/sex combination using a if loop nested in a for loop.

``` r
cat_colours <- c("calico","calico","ginger","ginger","tabby","tabby","tortoiseshell","tortoiseshell")

for (i in 1:8){
    if (i %% 2 == 0){#%% is R operator for 'mod', which is the remainder of the number before %% divided by the number after. In this case I am dividing i by 2, and checking if the remainder is 0, thus checking if i is even or odd
        cat("I have a female",cat_colours[i],"cat","\n")
    }else{
        cat("I have a male",cat_colours[i],"cat","\n")
    }
}
```

    ## I have a male calico cat 
    ## I have a female calico cat 
    ## I have a male ginger cat 
    ## I have a female ginger cat 
    ## I have a male tabby cat 
    ## I have a female tabby cat 
    ## I have a male tortoiseshell cat 
    ## I have a female tortoiseshell cat

Again this example is superficial and doesn't have practical, but I hope you've learnt something!
