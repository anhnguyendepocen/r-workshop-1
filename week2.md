---
title: "Week 2 (February 11, 2016)"

---

This week is a continuation of our introduction to R. You will review some key function concepts, alongside being introduced to basic calculations, simulation, and graphing. 

****

# 1. Introduction to R programming (Week 2)



## 1.1a Review , c() and vectors.

Let's review the concatenate function. Remember what it does?


{% highlight r %}
x <- c(1,6,2)

x
{% endhighlight %}



{% highlight text %}
## [1] 1 6 2
{% endhighlight %}



{% highlight r %}
y <- c(1,4,3)

y 
{% endhighlight %}



{% highlight text %}
## [1] 1 4 3
{% endhighlight %}

We use c() here to create two numeric vectors. I assume that you remember the logic behind vectors, but remember that they hold different types of data. Say we have a vector that is large, or unknown to us. R allows us to describe vector attributes as well as manipulate them in higher order operations. Try typing the code below:


{% highlight r %}
length(x)
{% endhighlight %}



{% highlight text %}
## [1] 3
{% endhighlight %}



{% highlight r %}
length(y)
{% endhighlight %}



{% highlight text %}
## [1] 3
{% endhighlight %}

The length() function tells us the long-wise dimension of our vector! Let's try something new with vectors...try typing the code below.


{% highlight r %}
x + y
{% endhighlight %}



{% highlight text %}
## [1]  2 10  5
{% endhighlight %}



{% highlight r %}
z = x + y

d = x / y

s = x - y

m = x * y
{% endhighlight %}

Go ahead and print (implicitly or explcitly) your new vectors! Do you understand what each line of code did? 

## 1.1b Workspace cleanup using code.

While one can utilize R Studio to make clean up easier, lets try cleaning up our workspace through the R console. Type the code below.


{% highlight r %}
ls()
{% endhighlight %}



{% highlight text %}
## [1] "d"            "KnitPost"     "m"            "myjekyllsite"
## [5] "s"            "x"            "y"            "z"
{% endhighlight %}

The list objects "ls()" function displays all objects that are currently in working memory. As I showed you before, it is easy to get rid of these with the environment tab in R Studio, but how can we do it without using that method? Lets try removing just the x and y vector objects


{% highlight r %}
rm(x, y)

ls()
{% endhighlight %}



{% highlight text %}
## [1] "d"            "KnitPost"     "m"            "myjekyllsite"
## [5] "s"            "z"
{% endhighlight %}

The remove objects "rm()" function simply removed x and y in this case. We can see that they are missing in both the R Studio environment window and by using the ls() function. What if we want to quickly remove all objects in memory?


{% highlight r %}
rm(list=ls())

ls()
{% endhighlight %}



{% highlight text %}
## character(0)
{% endhighlight %}

Woah! We can see that everything is gone. Do you understand the logic of the code that was used? If not, that is okay. Remember that when you typed out ls(), it printed out what appeared to be a character vector of each object in working memory. Like any operation we have performed before, there is no reason why we couldn't place this output into its own vector object! The code list = ls() does this nicely. The object called list is told to house the names of all objects in current working memory. If we apply the rm() function to this newly created object, it will read all current objects in working memory and remove them, including your newly created list vector. 


## 2 matrix(), or how I learned to love matrix algebra...

Remember before that I mentioned the idea of vectors as objects. Additionally, it was communicated that vectors are not the only type of object that R recognizes, but that vectors were essentially the simplest type of object one can work with. A slightly more complex object is the matrix object. What do you think separtes a matrix object from a vector? Lets try creating one. 


{% highlight r %}
x = matrix(data = c(1,2,3,4), nrow=2, ncol=2)

x
{% endhighlight %}



{% highlight text %}
##      [,1] [,2]
## [1,]    1    3
## [2,]    2    4
{% endhighlight %}

The result is probably what you suspected all along. Matrices are simply two vectors that are combined into columns and rows (think of spreadsheets!). There are a few new arguments introduced to us when creating the matrix "x". The data argument tells the matrix() function what numeric data to use, while the nrow argument indicates the number of rows and the ncol argument indicates the number of columns. Matrices in R utilize standard matrix algebra rules, so be mindful when combining different types of vectors. 

Like vectors, one can use mathematical operations to manipulate the values inside matrices. Lets introduce you to some additional mathematical operations in R. 


{% highlight r %}
sqrt(x)
{% endhighlight %}



{% highlight text %}
##          [,1]     [,2]
## [1,] 1.000000 1.732051
## [2,] 1.414214 2.000000
{% endhighlight %}



{% highlight r %}
x^2
{% endhighlight %}



{% highlight text %}
##      [,1] [,2]
## [1,]    1    9
## [2,]    4   16
{% endhighlight %}


The first line of code uses the sqrt() function to apply the square root to each matrix value. Many simple mathematical operations, or transformations, have built in R functions. The second line of code applies the square exponent to the matrix values. As you can see this is more in line with the addition/subtraction code used above. We can use the ^ operator to exponate a number to any power value.


{% highlight r %}
x^3
{% endhighlight %}



{% highlight text %}
##      [,1] [,2]
## [1,]    1   27
## [2,]    8   64
{% endhighlight %}



{% highlight r %}
x^5
{% endhighlight %}



{% highlight text %}
##      [,1] [,2]
## [1,]    1  243
## [2,]   32 1024
{% endhighlight %}



{% highlight r %}
x^10
{% endhighlight %}



{% highlight text %}
##      [,1]    [,2]
## [1,]    1   59049
## [2,] 1024 1048576
{% endhighlight %}



{% highlight r %}
x^100
{% endhighlight %}



{% highlight text %}
##              [,1]         [,2]
## [1,] 1.000000e+00 5.153775e+47
## [2,] 1.267651e+30 1.606938e+60
{% endhighlight %}

## 3. Introduction to simulation.

This next series of code is a bit more complicated, yet it demonstrates the power of R. Type the code out below.


{% highlight r %}
x = rnorm(50)


x
{% endhighlight %}



{% highlight text %}
##  [1]  0.88577884 -1.04731762  0.40895325 -1.38100700 -0.21100056
##  [6] -0.49076807  0.45243846  0.56942429  0.72048080  0.64281157
## [11] -0.02380024  1.44924683 -0.78991145  0.52500121  1.42471973
## [16] -0.88212773 -1.08711687  0.77359238  0.56173197 -1.03299116
## [21]  0.30693759 -1.32150828 -0.90692772 -1.77046991  0.40390191
## [26] -1.36557447  1.40391796 -0.01040675 -0.06720384  0.76992515
## [31]  1.06547933  0.34161790  1.36796975  2.37495458  0.52903207
## [36]  1.63879967 -1.70918571 -0.34133041  1.30260725  0.56743424
## [41]  0.34344573 -0.64487008  1.04846989 -1.72393499  0.25564522
## [46] -0.48699145  3.02233685 -0.46060760  0.29905146 -0.73921306
{% endhighlight %}

Judging by the printed output it is clear that we have created a numeric vector of length 50, but how did we do this? The rnorm() function is a tool that randomly samples vector values from a normal distribution. The 50 value in the function parentheses indicates that we wanted fifty random samples in our new vector. Remember that the standard normal distribution requires a mean of 0 and a standard deviation of 1, or simply $N(\mu = 0,\sigma = 1)$.

When we type the code above, it automatically gives us $N(0, 1)$, but it is possible to specify alternative values for $\mu$ and $\sigma$. Lets try simulating a vector with $\mu = 50$ and $\sigma = .1$. 


{% highlight r %}
y = rnorm(50, mean = 50, sd = .1)


y
{% endhighlight %}



{% highlight text %}
##  [1] 50.10316 50.07089 50.02992 50.11243 50.10436 49.93043 49.77676
##  [8] 49.94012 50.04509 50.08203 49.93660 50.04527 50.29320 50.04081
## [15] 49.98607 49.95281 50.15376 50.02378 50.10955 49.97942 49.88235
## [22] 49.98627 50.04849 49.90599 49.95582 49.78602 50.01050 49.86338
## [29] 49.84571 49.93797 49.92142 49.78694 50.05561 49.81547 50.02676
## [36] 49.99390 49.91211 49.85872 50.15037 49.89877 50.11025 50.01133
## [43] 49.95152 49.99650 50.04034 50.19083 50.17509 50.07507 49.94737
## [50] 49.95479
{% endhighlight %}

We have created a new random vector that displays a minimal spread around an average value of 50. Let's try diving into more familiar statistical analysis for a moment. Let's try and find the Pearson correlation coefficient for these two randomly simulated vectors.


{% highlight r %}
cor(x, y)
{% endhighlight %}



{% highlight text %}
## [1] 0.04670164
{% endhighlight %}

I found a correlation coefficient of 0.03847774, which is not very high! Do you notice something odd though? Your calculated correlation coefficient is probably not the same. Go back and run the code to create x and y again. If you pay attention, you will probaby notice that your values are bit different each time. Why do you think that is? The rnorm() function, or any simulation/samplng function, works with a psuedo random sampling system.[^1] What if we want to replicate our own work, or allow others to do so? We can achieve replication for random sampling by using a seed value. The random seed value tells the program to perform the calculations/sampling on a specific random selection value that will produce the same results everytime the seed value is used. Let's create a random seed value.


{% highlight r %}
set.seed(1452)

x = rnorm(50)

mean(x)
{% endhighlight %}



{% highlight text %}
## [1] 0.05073796
{% endhighlight %}



{% highlight r %}
y = rnorm(50, mean = 50, sd = .1)

mean(y)
{% endhighlight %}



{% highlight text %}
## [1] 49.99886
{% endhighlight %}



{% highlight r %}
cor(x, y)
{% endhighlight %}



{% highlight text %}
## [1] 0.1493827
{% endhighlight %}

By specifying the random seed, you should see that you produce the same results as the example above. The set.seed() function can take any numeric value as its random seed value. You should always use a random seed when working with random or simulated quantities in your work. Finally, we used only the rnorm() function to specify simulated vectors from the normal distribution. You are not restricted to only the normal distribution as R has built in function for almost every statistical distribution of interest to a data analyst. Go try and find other types of distribution sample functions.

## 4. Quantities of interest and R functions.

You may of noticed that we utilized a function called mean() in the code above. You probably suspected that this was a simple way of extracting the mean value for a numeric vector, this is correct! Here you will learn how to extract three important quantities of interest, namely mean, variance, and standard deviation. 


{% highlight r %}
set.seed(3)

y = rnorm(1000)

mean(y)
{% endhighlight %}



{% highlight text %}
## [1] 0.006396535
{% endhighlight %}



{% highlight r %}
var(y)
{% endhighlight %}



{% highlight text %}
## [1] 0.9961545
{% endhighlight %}



{% highlight r %}
sqrt(var(y))
{% endhighlight %}



{% highlight text %}
## [1] 0.9980754
{% endhighlight %}

Here we quickly created a random vector of 1000 values from a standard normal distribution. The first line of code produces the mean, the second the variance, and the third the standard deviation. Remember that standard deviation ($\sigma$) is the square root of variance ($\sigma^{2}$), or $\sqrt{\sigma^{2}}$. Fortunately, programmers are lazy and have built in a function that performs this calculation for you. 


{% highlight r %}
sd(y)
{% endhighlight %}



{% highlight text %}
## [1] 0.9980754
{% endhighlight %}

This is a good example of the usefullness of functions. Often we get bogged down in writing .do files or R scripts for complex calculations. One can easily write a function that includes these calculations. This saves time and space, while allowing us to share our own methods in a useful and condenced format.

## 4. Introduction to graphing in R

R is well-known for its ability to produce high quality graphics. The downside is that graphing in R has its own considerable learning curve. This section is to quickly introduce you to basic graph production in R. We will go over more complex and interesting graph creation later in the semester. 

Lets start by using the basic plot() function.


{% highlight r %}
set.seed(856)

x = rnorm(100)
y = rnorm(100)

plot(x,y)
{% endhighlight %}

![image](https://cbesaw.github.io/assets/unnamed-chunk-16-1.png) 

First you created two numeric vectors (variables here) that are to be used in a scatterplot. The plot() function analyzes the type of datat that is submitted to it and plots it accordingly. Because we have two interval level vectors here, it produces a scatter plot. The plot is displayed in the bottom right panel in R Studio (remember the plots tab?). Here we see a pretty random spread within the scatter plot. The resulting output is pretty non-descript, lets change that.


{% highlight r %}
plot(x, y, xlab = "This is the x-axis", ylab = "This is the y-axis",
     main = "Plot of X vs Y", col = "green")
{% endhighlight %}

![image](https://cbesaw.github.io/assets/unnamed-chunk-17-1.png) 

The plot is much more informative than before! The above code introduced some new arguments to the plot() function. the xlab argument names the x-axis label, ylab names the y-axis label, and main names the plot title. The col argument allows us to specify a specific color for the plot observations, in this case green. 

Finally, if we want to export our plot it is easy to do so in R Studio. Simply use the export button in the Plots tab to export it as an image or pdf, or to copy the plot into memory. 


****

[^1]: Anything made by a computer algorithim is never truly random. There are both mathematical and philosphical reasons for this. This is okay though, because it is good enough. Besides, is anything ever truly random? Think about it. 



