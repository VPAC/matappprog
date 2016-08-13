# Introduction

## Foreword



## Preface

From a naive perspective, it is initially surprising to discover that there are multiple mathematical application and programming languages. "Surely", the reasoning goes, "all computation is a mathematical problem. Do we really need this multiplicity of languages?" Of course, when one comes to the realisation that there are multiple subfields of mathematics and the ways that these are structures and, in using their "quasi-empiricism" (to use the phrase perhaps first used by Imre Lakatos), they will have different ways of interacting with the actual computer system itself and with varying levels of efficiency and effectiveness. Thus, different mathematical programming languages. 

In one sense, mathematical programming is an optimisation problem; the selection of the best solution from available solutions. This is certainly a major treatment of the well-known journal "Mathematical Programming". Whilst important, it is only indirectly referred to in this publication, except perhaps in analogy with the slight change in title: 'Mathematical Applications and Programming'. In providing an introduction to three major mathematical applications and programming languages that are available as free and open-source products - R, Octave, and Maxima - as the best solution for three different types of mathematical problems - statistics, numerical computation, and symbolic computation. In addition to this there are always new developments in the field and emergent technologies such as Julia and UNUMs are explored in the final chapter.

Of course there are some similarities involved. Each of these applications and languages will have their own procedures for installation, on where to find online help. They each have their own way of handling different data types, managing variables and functions, and incorporating these into scripts and programs, as well as different ways of providing graphical visualisation. As far as broad categories are concerned, mathematical computation has at least some conceptual areas in common - and as it should be. After all, mathematics is neither just an art, a science, or a law, but as philosophy, it is the language of the universe. 

"Philosophy is written in this grand book, which stands continually open before our eyes (I say the 'Universe'), but can not be understood without first learning to comprehend the language and know the characters as it is written. It is written in mathematical language, and its characters are triangles, circles and other geometric figures, without which it is impossible to humanly understand a word; without these one is wandering in a dark labyrinth."

Galileo Galilei, Il Saggiatore (1623)

Source material this book has primarily come from the official documentation of the relevant progamming languages, that is, "An Introduction to R" (2015), "GNU Octave: A high-level interactive language for numerical computations" (2015), "Maxima 5.37.3 Manual" (2015), "The Julia Manual" (2015), along with "The End of Error: Unum Computing" by John Gustafson (2015), "Learning R" by Richrd Cotton (2013), "GNU Octave: Beginner's Guide" (2011) by Jesper Schmidt Hansen, and the frankly quite brilliant "Classical Mechanics with Maxima" (2016) by Todd Keene Timberlake, and J. Wilson Mixon.Jr., and, interestingly, "MATLAB(R) For Engineers" (2012) by Holly Moore.

Another particular feature of this book however, is that it is particularly designed from the perspective of using high-performance computing and as an educational text. This makes it a little different from the numerous similar texts that are available for the various programming environments that are covered here. This difference is, of course, contextual. Much of the material draws upon training manuals produced at the Victorian Partnership for Advanced Computing over the past several years.

I also wish to thank several other contributors who assisted in this manuscript, including Chelton Evans from the Royal Melbourne Institute of Technology, and  Mark Greenaway of the University of Sydney. All errors and omissions are my own.

This book is part of a series designed to assist researchers, systems administrators, and managers in a variety of advanced computational tasks. Other books that will be published in this series include: Supercomputing with Linux, Sequential and Parallel Programming., Data Management Tools for eResearchers., Building HPC Clusters and Clouds., Teaching Research Computing to Advanced Learners., Quality Assurance in Technical Organisations., Technical Project Management, and A History of the Victorian Partnership of Advanced Computing.

Thanks are given to the Victorian Partnership of Advanced Computing for the time and resources necessary for the publication of this book, and especially Bill Yeadon, manager of research and development, and Ann Borda, Chief Executive Officer, who both authorised its publication.


Lev Lafayette, 2016
 



# Statistical Computation with R


## About R and Setup

R originated as an open-source implementaion of the S language mainly for statistical compution with an initial point release in 1997, and version 1.0 in 2000. It was originally developed by Ross Ihaka and Robert Gentleman of the University of Aukland and is free and open source software, licensed under the GPL. In addition to the base environment, R is extended by numerous packages produced my members of a particularly enthusiastic community.

Documentation and packages is available at 

`http://cran.r-project.org`

"CRAN" stands for "Comprehensive R Archive Network"

To install R on a local Linux machine either use a prefereed package manager or download a source code version from a local respository (e.g., `http://cran.ms.unimelb.edu.au/`). Be aware that for source-code installations may require additional optimisations but are also computationally faster when these optimisations are put into place.

A simple installation process would be as follows:

`cd /usr/local/src/R`
`wget http://cran.r-project.org/src/base/R-3/R-3.0.2.tar.gz`
`tar xvf R-3.0.2.tar.gz`
`cd R-3.0.2`
`./configure`
`make`
`make install`

A very small sample simple dataset that is used throughout this chapter is `auspop.txt`. Whilst it is part of the github repository that the latest version of this book is stored in, it is also replicated here. It is 

It shows the population of Australia, including states and major territories, measured in thousands of people every ten years - a fairly simple table.

Year NSW Vic. Qld SA WA Tas. NT ACT Aust.
1917 1904 1409 683 440 306 193 5 3 4941
1927 2402 1727 873 565 392 211 4 8 6182
1937 2693 1853 993 589 457 233 6 11 6836
1947 2985 2055 1106 646 502 257 11 17 7579
1957 3625 2656 1413 873 688 326 21 38 9640
1967 4295 3274 1700 1110 879 375 62 103 11799
1977 5002 3837 2130 1286 1204 415 104 214 14192
1987 5617 4210 2675 1393 1496 449 158 265 16264
1997 6274 4605 3401 1480 1798 474 187 310 18532
2007 6927 5246 4228 1592 2131 496 218 341 21181 

## Invoking, Help, and Quitting

To start R on the cluster bring the environment module to your path. A local and unique installation will do this autonomatically. If the system has multiple versions of the same software application installed they environment paths will probably be invoked by a modules system (setting them by hand each time is painful, setting them as part of a .bash_profile or similar is less painful, using modules is easiest). The following example is from the Trifid high performance computing system at the Victorian Partnership for Advanced Computing. An interactive job is launched, placing the user, `train12` on to a compute node for 12 hours, to minimise resource utilisation on the login node.

Once R is loaded into the user's PATH it is a simple of case of invoking the command-line enviroment, by simply typing "R". The prompt indicates that R is waiting for input.  For example, imagine that one has reached the certainty that the great philosophers of mathematics, Betrand Russell and Alfred North Whitehead, did in their Principia Mathmatica... "From this proposition it will follow, when arithmetical addition has been defined, that 1+1=2." (Volume I, 1st edition, page 379)

bash-4.2$ ssh train12@trifid.in.vpac.org
[train12@trifid ~]$ qsub -l walltime=12:00:0,nodes=1:ppn=2 -I
[train12@trifid-35 ~]$ module avail R
-------------------------- /usr/local/Modules/modulefiles--------------------------
R/2.15.1-gcc         R/2.15.3-gcc         R/3.0.1-gcc
R/2.15.2-gcc         R/3.0.0-gcc(default) R/3.0.2-gcc
[train12@trifid035 ~]$ module load R
$ R
WARNING: ignoring environment value of R_HOME
R version 3.0.0 (2013-04-03) -- "Masked Marvel"
Copyright (C) 2013 The R Foundation for Statistical Computing
Platform: x86_64-unknown-linux-gnu (64-bit)
..
> 1+1
[1] 2
>
```

The result is 2, the bracketed [1] meaning the first requested element. The command line now eagerly awaits new commands, all of which shall be explored in detail.  In Volume Two, p86, when discussing cardinal arithmetic, Russell and Whitehead noted that "The above proposition is occasionally useful". It is hoped that R too, can be occasionally useful. 

R commands or expressions are typed following this prompt. There is also a continuation prompt, "+". Anything that follows a # on the command line is taken as comment and ignored by R. Commands are separated either by a semi-colon or by a newline. Commands can be grouped together into by braces e.g., {commands}. The vertical arrow keys on the keyboard can be used to scroll forward and backward through a command history. 

To get help type:

`> help("command")`

The search function help.search() can be a huge help in finding what one wants. Examples of their use are:

`> help.search("correlation")`

This will often include the helpful information:

`Type 'vignette("FOO", package="PKG")' to inspect entries 'PKG::FOO'.`

Often HPC systems are deliberately designed not have a pre-installed x-windows environment, for a number of resource and security reasons. TO view binary documents they should be copied to a local machines (e.g., by using scp, Filezilla etc) for viewing.

```
> vignette("sandwich", package="sandwich")
> /usr/bin/xdg-open: line 402: htmlview: command not found
/usr/bin/xdg-open: line 402: firefox: command not found
/usr/bin/xdg-open: line 402: mozilla: command not found
/usr/bin/xdg-open: line 402: netscape: command not found
/usr/bin/xdg-open: line 402: links: command not found
/usr/bin/xdg-open: line 402: lynx: command not found 
xdg-open: no method available for opening '/usr/local/R/3.0.0-gcc/lib64/R/library/sandwich/doc/sandwich.pdf'
```

e.g.,
```
bash-4.2$ scp train12@trifid.vpac.org:/usr/local/R/3.0.0-gcc/lib64/R/library/sandwich/doc/sandwich.pdf .
sandwich.pdf                                    100%  206KB 206.4KB/s   00:00`    
bash-4.2$ evince sandwich.pdf` 
```

There are also a number of variations to the help sequence of which the following are examples. The `help(start)` is a web-based introduction which is best run a local machine.

```
> help.start() 
starting httpd help server ... done 
If the browser launched by '/usr/bin/firefox' is already running, it is
    *not* restarted, and you must switch to its window.
Otherwise, be patient ... 
> help(sqrt) # Launches help for the function in man page format.
> example(sqrt) # Run locally; works best with graphics.
> help.search("sqrt")
```


These help requests are an example of a function in R. All R functions are invoked by calling the name of the function followed by parentheses which may include arguments. One of the most used functions is the c(), or combine function which takes the arguments into a vector.

To quit R enter the exit function without arguments. It will ask the user if they wish to save your workspace image, which means any user-defined objects (vectors, matricies, data frames, lists, functions, etc) created in the session. If the user answers in the affirmative these will be automatically loaded next time they enter the R environment on the same system.

`> q()`

Typing q on its own, without the parentheses, will display the text of the function.

All R entities, including functions and data structures, exist as objects and can be viewed with an `ls()` or `objects()` function call.

## Calculations and Assignment

A number of simple calculator functions are built in with R.  The application will evaluate and print the result of expressions typed on the R command line with the result on subsequent lines. The basic arithmetic syntax for addition, subtraction, multiplication, division, powers, and brackets is familiar enough. The order of operations is  brackets, powers, division, multiplication, subtraction, addition, conducted left-to-right.

```
> 1+1 
[1] 2 	
> 2+2
[1] 4 
> 2-2 
[1] 0 
> 2*2 
[1] 4 
> 2/2 
[1] 1 
> 2^2 
[1] 4 
> (2+2)-2*2/2^2
[1] 3 
```

As with most calculators there are a number of common, built-in, functions.

```
> log(100) # natural logarithm, Euler's number e,  c2.71828.
[1] 4.60517
> log(10)+log(10) # log(a)+log(b) = log(a*b)
[1] 4.60517 
> log10(100) # The "base ten" logarithm.
[1] 2 
> log10(10)+log10(10) # To multiply powers of a number add together the exponents.
[1] 2 
> log2(256) # R can do binary logarithms as well.
[1] 8 
>  logb(100, 10) # Calculate logarithms from base (x,base).
[1] 2 
> exp(10) # exponential
[1] 22026.47 
> log(22026.47) 
[1] 10 
> sqrt(10) # An approximation; square roots, except perfect squares, are irrational.
[1] 3.162278
> sqrt(169) 
[1] 13 
> pi # R knows about pi!
[1] 3.141593
> 2*pi*6378 # Circumference of Earth at Equator, in km; radius is 6378 km.
[1] 40074.16
> sin(c(30,60,90)*pi/180) # Convert angles to radians, then take sin()
[1] 0.5000000 0.8660254 1.00000
```

As with other calculators, R has its own way of dealing with some special results. R understands infinity and negative infinity, it refers to undefined results (NaN, not a number; strictly speaking any number, x=0/0, x*0 = 0), and complex (imaginary) numbers.

```
> 1/0 
[1] Inf 
> -1/0 
[1] -Inf 
> 0/0 
[1] NaN 
> Inf/Inf 
[1] NaN 
> Inf+(-Inf) 
[1] NaN 
> (0i-9)^(1/2) 
[1] 0+3i 
> sqrt(-17) 
[1] NaN 
Warning message: 
In sqrt(-17) : NaNs produced 
> sqrt(-17+0i) 
[1] 0+4.123106i
```
Values can be assigned to variables in R with a "<-"  or a "->" combination of characters, depending on the redirection of the data to the variable. Assignment can also be made with the assign() function and, in most cases, the equals sign, but only on as a left-hand assignment. If a command is not assigned to a variable, the result is printed without being saved.

R commands and variables are case sensitive, like most things in the *nix world. Variable names are best with alphanumerics, and can be combined with fullstops and underscores, along as the character following a fullstop is an alphanumeric. 

Variables can be combined with functions. The variables can then be manipulated as expected.

```
> maxlog07<-log(max(6927,5246,4228,1592,2131,496,218,341)) 
> maxlog 07
[1] 8.843182 
> assign("maxlog07)", log(max(6927,5246,4228,1592,2131,496,218,341)) )
> maxlog07 # The same result.
[1] 8.843182 
> log(max(6274,4605,3401,1480,1798,474,187,310))->maxlog97 
> maxlog97 
[1] 8.744169
> maxlog97=log(max(6274,4605,3401,1480,1798,474,187,310)) 
> maxlog97 
[1] 8.744169
> maxlog07+maxlog97 
[1] 17.58735 
> maxlogadd=maxlog07+maxlog97 
> maxlogadd 
[1] 17.58735 
```

As an another interactive example of R acting as an interactive calculator with assignment consider Fahrenheit temperatures that correspond to Celsius temperatures 25, 26, ..., 30

```
> celsius <- 25:30
> fahrenheit <- 9/5*celsius+32
> conversion <- data.frame(Celsius=celsius, Fahrenheit=fahrenheit)
> print(conversion)
Celsius Fahrenheit
1      25       77.0
2      26       78.8
3      27       80.6
4      28       82.4
5      29       84.2
6      30       86.0
```

It is also possible to save individual objects, or collections of objects into a named image file.

```
> save.image()
> # Save contents of workspace, into the file .RData
> save.image(file="archive.RData")
> # Save into the file archive.RData
> save(celsius, fahrenheit, file="tempscales.RData")
```

## Data Types

As implied in the previous section, R has a number of different data types, or mode in R-speak, which are commonly used, including numeric, integer, complex, logical, and character. Variable types can be determined by use of the class() function.

The numeric datatype is effectively the set of real numbers expressed in decimal notation and is the default computational type. Unless specified an integer with the as.integer() function, for example, a variable will be assigned to the datatype numeric. The same function can be used to truncate real numbers to integers, although this will not work for character strings etc, that cannot be converted.
 
``` 
> realpop17 <- (4816.9) 
> realpop17
[1] 4816.9
> class(realpop17)
[1] "numeric"
> realpop17 <- (4940.9)
> realpop17
[1] 4940.9
> class(realpop17)
[1] "numeric"
> intpop17(4941)
Error: could not find function "intpop17"
> intpop17 <- 4941
> intpop17
[1] 4941
> class(intpop17)
[1] "numeric"
> is.integer(intpop17)
[1] FALSE
> intpop17 <- as.integer(4941)
> intpop17
[1] 4941
> is.integer(intpop17)
[1] TRUE
> as.integer(4816.9)
[1] 4816
> as.inter("Auspop17")
Error: could not find function "as.inter"
> as.interger("Auspop17")
Error: could not find function "as.interger"
> as.integer("Auspop17")
[1] NA
Warning message:
NAs introduced by coercion 
```

Complex data types in R are defined via the imaginary number i. Unless assigned correctly, attempts to invoke imaginary numbers will create a NaN error. Or, a value can be converted into an imaginary type.

```
> sqrt(-1)
[1] NaN
Warning message:
In sqrt(-1) : NaNs produced
> sqrt(-1+0i)
[1] 0+1i
> sqrt(as.complex(-1)) 
[1] 0+1i
```

Standard logical operations - and (&), or (|), not (!), and xor - are available in R and are often used for comparisons. 

```
> sapop87 <- (1393)
> wapop87 <- (1496)
> compare87 <- sapop87 < wapop87
> compare87
[1] TRUE
> class(compare87)
[1] "logical"
```

String values make use of the character datatype. Other values can be converted into character values with the as.character() function, and can be concatenated with the paste() function. Further, the sprintf() function makes use of a C-language syntax.

```
> pie <- as.character(3.141593)
> class(pie)
[1] "character"
> prenom <- "Lev" ; surnom <- "Lafayette"
> jemappele <- paste(prenom,surnom)
> jemappele
[1] "Lev Lafayette"
> sprintf("In 2007 %s had a population of %d thousand people", "NSW", 6927) 
[1] "In 2007 NSW had a population of 6927 thousand people"
```

Parts of a character string can be extracted by the substr() function with start and stop arguments. A search and replace can be performed with the sub function.

```
> substr("The quick brown fox jumps over the lazy dog", start=10, stop=19) 
[1] " brown fox"
sub ("fox", "wolf". "The quick brown fox")
```

## Numerical Vectors

R operates on data structures, of which the most simple are vectors, a single entity of an ordered collection and a consistent data type, or mode. Examples thus far have been a vector of a single element. 

Consider the vector population2007, using the concatenation function to generate an vector from end-to-end. This vector can be subject to a variety of arithmetic modifications as well as special R functions.

```
> population2007 <- c(6927,5246,4228,1592,2131,496,218,341) 
> population2007 
[1] 6927 5246 4228 1592 2131  496  218  341
> growth=population2007*1.03 
> growth 
[1] 7134.81 5403.38 4354.84 1639.76 2194.93  510.88  224.54  351.23
> mean(population2007)
[1] 2647.375 
> sum(population2007) 
[1] 21179 
```

A simple vector sequences can also generated by R with arithematic priority assigned to the colon separator.  A more general function is seq(), which takes arguments for the beginning ("from") and end ("to") of the sequence and, optionally, the increment ("by") or the desired length ("length") of the sequence. The order may be varied by making use of the parameter names, but length must be named.

```
> 1:30 # c(1,2 .. 30). 
 [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 
[26] 26 27 28 29 30 
> 2*1:30. 
 [1]  2  4  6  8 10 12 14 16 18 20 22 24 26 28 30 32 34 36 38 40 42 44 46 48 50 
[26] 52 54 56 58 60 	
> 2*30:1 
 [1] 30 29 28 27 26 25 24 23 22 21 20 19 18 17 16 15 14 13 12 11 10  9  8  7  6 
[26]  5  4  3  2  1 
> seq(1,30,2) 
 [1]  1  3  5  7  9 11 13 15 17 19 21 23 25 27 29 
> seq(from=1,to=30,by=2.125) 
 [1]  1.000  3.125  5.250  7.375  9.500 11.625 13.750 15.875 18.000 20.125 
[11] 22.250 24.375 26.500 28.625 
> seq(0, 30, length=8) 
[1]  0.000000  4.285714  8.571429 12.857143 17.142857 21.428571 25.714286 
[8] 30.000000 
> seq(from=1,to=30,by=pi) 
 [1]  1.000000  4.141593  7.283185 10.424778 13.566371 16.707963 19.849556 
 [8] 22.991149 26.132741 29.274334 
```

## Logical Vectors

In addition to numerical values, R also allows for logical vectors which can have the values TRUE, FALSE, or NA (not available). Logical vectors are created by establishing conditional statements where values in the vector are true or false depending on the statement. Logical operators include  <, <=, >, >=, == for exact equality and != for inequality. The which() function can be used to determine the vector elements that are true, useful if the vector is large.

```
> pop77 <- c(5002,3837,2130,1286,1204,415,104,214)
> pop87 <- c(5617,4210,2675,1393,1496,449,158,265)
> pop77 > 1250
[1]  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE
> pop87 > 1250
[1]  TRUE  TRUE  TRUE  TRUE  TRUE FALSE FALSE FALSE
> which(pop77 > 1250)
[1] 1 2 3 4
> which(pop87 > 1250)
[1] 1 2 3 4 5
```

In addition the intersection of logical vectors is expressed with the "and" character, (& or &&), and the union with the "or" character, (| or ||), along with exclusive or (xor), not (!)but only if c1 and c2 are logical expressions.

```
> pop77 & pop87 # All statements count as "true"
[1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
> pop77 | pop87 # Ditto
[1] TRUE TRUE TRUE TRUE TRUE TRUE TRUE TRUE
> x <- c(TRUE,FALSE,TRUE,FALSE,TRUE)
> y <- c(FALSE,TRUE,FALSE,TRUE,TRUE)
> x & y
[1] FALSE FALSE FALSE FALSE  TRUE
> x && y
[1] FALSE
> x | y
[1] TRUE TRUE TRUE TRUE TRUE
> x || y
[1] TRUE
> xor(x,y)
[1]  TRUE  TRUE  TRUE  TRUE FALSE
> x && !y
[1] TRUE
```

Logical vectors may sometimes be used in ordinary arithmetic, in which case they are converted into numeric vectors (1 for TRUE, 0 for FALSE). If the value of a vector is not available, a placeholder may be reserved with the value NA. Operations typically performed on a NA value become a NA. This is different to the numerical vector NaN.

```
> z <- c(1:3,NA);  ind <- is.na(z)
> z
[1]  1  2  3 NA
> ind
[1] FALSE FALSE FALSE  TRUE
```

## Character and Index Vectors

Character elements and vectors are also available in R, typically used for plotting labels. These are entered as single or double-quoted strings, with C-style escape sequences (e.g., \n, \t etc). Character vectors may be concatenated into a vector by the c() function. The paste() function takes an arbitrary number of arguments and concatenates them one by one into character strings. The arguments are by default separated in the result by a single blank character, but this can be changed by the named parameter, sep=string

```
> labs <- paste(c("X","Y"), 1:10, sep="")
> labs
 [1] "X1"  "Y2"  "X3"  "Y4"  "X5"  "Y6"  "X7"  "Y8"  "X9"  "Y10"
```

Subsets of elements of a vector may be selected. With logical vectors the index vector must be of the same length as the vector from which elements are to be selected. The negative calls for all elements except that specified. An out-of-range creates an NA.

```
> pop77[c(1,2,3,4,5)]
[1] 5002 3837 2130 1286 1204
If the value of a vector is not available, a placeholder may be reserved with the value NA. Operations typically performed on a NA value become a NA. This is different to the numerical vector NaN.
> z <- c(1:3,NA);  ind <- is.na(z)
> z
[1]  1  2  3 NA
> ind
[1] FALSE FALSE FALSE  TRUE
```

Vectors can also be named and retrived by their name.

```
> names(pop77) <- c("NSW","Vic","Qld","SA","WA","Tas","NT","ACT")
> pop77[c("NSW","Vic","Tas","ACT")]
 NSW  Vic  Tas  ACT 
5002 3837  415  214
```

Subsets of elements of a vector may be selected. With logical vectors the index vector must be of the same length as the vector from which elements are to be selected. The negative calls for all elements except that specified. An out-of-range creates an NA.

```
> pop77[c(1,2,3,4,5)]
[1] 500
> pop77[c(1:8)] 
[1] 5002 3837 2130 1286 1204  415  104  2142 3837 2130 1286 1204
> pop77[c(5,3,5,1) ] 
[1] 1204 2130 1204 5002 
> pop77[c(-3)]
[1] 5002 3837 1286 1204  415  104  214
> pop77[c(9)]
[1] NA
```

## Objects, Modes, and Class

The vector examples provided are a type of object in R. All elements in a vector must have the same data type, or mode - although NA may seem as an exception there are, in a sense, different types of NA. In comparison to vectors, R can also have operations performed on objects called lists, which are of their own mode (list). Lists can have objects included in their sequence which individually can be of any mode. Because they are an object that includes objects they are known as a recursive object in R as opposed to an atomic object. Other recursive structures are those of mode function and expression.  Expressions as objects form an advanced part of R which will not be discussed in this guide, except indirectly when we discuss formulae used with modeling in R.

The mode of an object is one of its fundamental properties. Others include the length(object) and others still can be determined by the attributes() function and the function attr(object, name) can be used to select a specific attribute. An object may have new elements may be added by indexing a value outside its existing range, although missing elements will be extended with NA, or truncated by re-assigning the element range. 

R objects have a class, indicated by the function class(), of which the datatype is typical for simple vectors, but can also be "list", "matrix", "array", "factor", "data.frame". The class of an object can allow for object-orientated programming.

```
> mode(wapop87)
[1] "numeric"
> length(wapop87)
[1] 1
> wapop87[3] <- 1497
> wapop87
[1] 1496   NA 1497
> wapop87 <- wapop87[1]
> wapop87
[1] 1496
> length(wapop87) <- 3
> wapop87
[1] 1496   NA
> length(wapop87) <- 1
> wapop87
[1] 1496
> class(wapop87)
[1] "numeric"
```

The function attributes(object) lists the non-intrinsic attributes defined for the object. The function attr(object, name) can be used to select a specific attribute. By assignment a new attribute with object or a change an existing one can be introduced. For example, a vector could be turned into a matrix.

```
> attr(wapop87, "dim") <- c(1,1) 
> wapop87 
     [,1] 
[1,] 1496 
>  wapop87 <- wapop87[1] 
> wapop87 
[1] 1496 
```

## Factors

Factors can be understood as variables which take on a limited number of different values, referred to as "categorical variables". They are analogous to enumerated types in other programming languages. Factors in R are stored as a vector of integer values with a corresponding set of character values to use when the factor is displayed. When using the factor function on the vector of values which will be returned as a vector of factor values both numeric and character variables can be used, although the factor's levels will always be character values.  To change the order in which the levels will be displayed from their default sorted order, the levels= argument can be used. If the ordering should also be used when performing comparisons, use the optional ordered=TRUE argument, creating an ordered factor.

Factors are a efficient way to store character values, because each unique character value is stored only once, and the data itself is stored as a vector of integers. Because of this, read.table will automatically convert character variables to factors unless the as.is= argument is specified.

To take an Australian demographic example for the R manual, suppose a sample of 30 tax accountants the states and territories of Australia1 with their state of origin identified by a character vecto as follows:

```
> state <- c("tas", "sa",  "qld", "nsw", "nsw", "nt",  "wa",  "wa", "qld", "vic", "nsw", "vic", "qld", "qld", "sa",  "tas", "sa",  "nt",  "wa",  "vic", "qld", "nsw", "nsw", "wa", "sa",  "act", "nsw", "vic", "vic", "act")
```

A factor created using the factor() function:

```
> statef <- factor(state)
> statef
```

To find out the levels of a factor the function levels() can be used.

```
> levels(statef)
[1] "act" "nsw" "nt"  "qld" "sa"  "tas" "vic" "wa"
```

The levels of factors are stored in alphabetical order, or in the order they were specified to factor if they were specified explicitly. Levels may have a natural ordering desired by the user; the ordered() function creates such ordered factors but is otherwise identical to factor.

Also suppose the incomes of the same tax accountants in another vector, measured in thousands of dollars. These are obviously recent graduates.

```
> incomes <- c(60, 49, 40, 61, 64, 60, 59, 54, 62, 69, 70, 42, 56, 61, 61, 61, 58, 51, 48, 65, 49, 49, 41, 48, 52, 46,
59, 46, 58, 43)
```

The mean income can now be calculated using tapply():

```
> incmeans <- tapply(incomes, statef, mean)
> incmeans
     act      nsw       nt      qld       sa      tas      vic       wa 
44.50000 57.33333 55.50000 53.60000 55.00000 60.50000 56.00000 52.25000 
> 
```

The function tapply() is used to apply a function, here mean(), to each group of components of the first argument, here incomes, defined by the levels of the second component, here statef, as if they were separate vector structures. Likewise the standard errors of the state income means can also be calculated, using the builtin function var() to calculate the sample variance:

`> stderr <- function(x) sqrt(var(x)/length(x))`

(Actually R also has a builtin function sd(), but it serves for illustration). The standard errors are calculated by

```
> incster <- tapply(incomes, statef, stderr)
> incster
     act      nsw       nt      qld       sa      tas      vic       wa 
1.500000 4.310195 4.500000 4.106093 2.738613 0.500000 5.244044 2.657536 
> incster <- tapply(incomes, statef, stderr)
```

## Simple Arrays and Matrices

A vector has been defined as single entity of an ordered collection and a consistent data type, or mode. This compares to an array, which consists of collection of subscripted data entries, of which a matrix is one type - an array of two-dimensions. A vector can be used as an array if it has the attribute dim(), and an array can be one-dimenional, in which case it is treated like a vector. Array ordering is according to column order. For example, an array a of dimensions 3,4,2 would be ordered with the individual elements a[1,1,1], a[2,1,1], .... a[2,4,2], a[3,4,2]. The notation a[,,] stands for the entire array, which is the same as omitting the subscripts entirely and just using a. For any array,the dimension vector may be referenced explicitly as dim(a) on either side of an assignment.

The function matrix creates matrices with the arguments data, nrow, ncol, by row. The data argument is typically list of the elements that will fill the matrix. The nrow and ncol arguments specify the dimension of the matrix. The byrow argument specifies how the matrix is to be filled. The default value for byrow is FALSE which means that by default the matrix will be filled column by column.

```
> seq1 <- seq(1:6)
> mat1 <- matrix(seq1, 2)
> mat1
     [,1] [,2] [,3]
[1,]    1    3    5
[2,]    2    4    6
> mat2 <- matrix(seq1, 2, byrow = T)
> mat2
     [,1] [,2] [,3]
[1,]    1    2    3
[2,]    4    5    6
> mat3 <- matrix(seq1, ncol = 2)
> mat3
     [,1] [,2]
[1,]    1    4
[2,]    2    5
[3,]    3    6
> mat4 <- matrix(seq1, 3, 2)
> mat4
     [,1] [,2]
[1,]    1    4
[2,]    2    5
[3,]    3    6
> #creating a matrix of 20 numbers from a standard normal dist.
> mat5 <- matrix(rnorm(20), 4)
> mat5
(snip)
```

Some useful matrix functions include dim, cbind, rbind, dimnames. The dim function lists the dimensions of a matrix, whereas cbind and rbind append matrices together via column and row. The dimnames function is used to manipulates row and column names. 

```
#appending v1 to mat5
> v1 <- c(1, 1, 2, 2)
> mat6 <- cbind(mat5, v1)
> mat6
(snip)
> v2 <- c(1:6)
> mat7 <- rbind(mat6, v2)
> mat7
(snip)
> dim(mat7)
[1] 5 6
> dimnames(mat7) <- list(NULL, NULL)
> mat7
(snip)
```

Matrix operations use the same symbols as the math operations.

```
> #Creating mat8 and mat9
> mat8 <- matrix(1:6, 2)
> mat9 <- matrix(c(rep(1, 3), rep(2, 3)), 2, byrow = T)
> mat8
(snip)
> mat9
(snip)
> mat8 - mat9
(snip)
> mat8 + mat9
(snip)
> mat8 / mat9
(snip)
> mat8 * mat9
(snip)
> #inverse
> solve(mat8[, 2:3])
> #transpose
> t(mat9)
```

A matrix may be used with a single index matrix in order to (a) assign a vector of quantities to an irregular collection of elements in the array, or (b) to extract an irregular collection as a vector. For example, elements can be extracted as a vector structure and replaced. Negative indices are not allowed in index matrices.

```
> mat10 <- array(1:20, dim=c(4,5))   # Generate a 4 by 5 array.
> mat10
(snip)
> i <- array(c(1:3,3:1), dim=c(3,2))
> i                             # i is a 3 by 2 index array.
(snip)
> mat10 [i]                          # Extract those elements
[1] 9 6 3
> mat10[i] <- 0                     # Replace those elements by zeros.
> mat10
(snip)
```

Arrays can be constructed from vectors by the array function which specify the data vector and the dimension vector as arguments. Elements in the vector will be recycled to fill up all the elements of the array. To create an array of zero values include this as the data vector. Arrays may be used in arithmetic expressions and the result is an array formed by element-by-element operations on the data vector.

```
> v <- c(1, 2, 3, 4, 5, 6)
> A <- array(v, dim=c(3,4,2))
> A
(snip)
> Z <- array(0, c(3,4,2))
> Z
(snip)
```

The outer product may be calculated on numeric arrays with the dimension vectors concatenated and the data vector formed from  possible products of elements of the data vectors. The outer product is formed by the special operator %o%, or ab <- outer(a, b, "*")

```
> a <- array(1:20, dim=c(4,5))
> b <- array(21:40, dim=c(4,5))
> a
(snip)
> b
(snip)
> ab <- a %o% b
> ab
(snip)
```

## Linear Equations, Eigenvalues, and Decomposition

The operator %*% is used for matrix multiplication. If A and B are square matrices of the same size (n,b), then the matrix of element products is determined by multiplication of the variables and %*% is the matrix product.

```
> a <- array (1:4, dim=c(2,2))
> a
(snip)
> b <- array (1:4, dim=c(2,2))
> b
(snip)
> a * b
(snip)
> a %*% b
```

The function crossprod() forms "crossproducts", where crossprod(X, y) is the same as t(X) %*% y , but achieved more efficiently. For diag() its meaning depends on its argument. diag(v), where v is a vector, gives a diagonal matrix with elements of the vector as the diagonal entries. On the other hand diag(M), where M is a matrix, gives the vector of main diagonal entries of M.

The function solve(a,b,..) is a generic function solves the linear equation a %*% x = b for x, where b can be either a vector or a matrix. The function eigen(A) calculates the eigenvalues and eigenvectors of a symmetric matrix Sm. The result of this function is a list of two components named values and vectors. The assignment eigen(a) calculates the eigenvalues and eigenvectors of a symmetric matrix A. Then ev$val is the vector of eigenvalues of Sm and ev$vec is the matrix of corresponding eigenvectors.  If just the eigenvalues are required then the assigment could use evals <- eigen(a)$values

```
> ev <- eigen(a)
> ev$val
> ev$vec
> eigen(a)
```

Single value composition is represented by the function svd(M), which takes a matrix as an argument (M), and calculates its singular value decomposition. This consists of matrix of columns of the same length as M, a second matrix who column space is the row space of M, and a diagonal matrix of D, such that M = U %*% D %*% t(V). D is actually returned as a vector of the diagonal elements. The result of svd(M) is actually a list of three components named d, u and v, with evident meanings. If M is a square matrix, absdetM calculates the absolute value of the determinant of M as illustrated. R also has a builtin function, det, to calculate a determinant, including the sign, and another, determinant, to give the sign and modulus 
 
```
> svd(a)
(snip)
> absdetA <- prod(svd(A)$d)
(snip)
> det(A)
(snip)
```

The function lsfit() returns a list giving results of a least squares fitting procedure, where the first argument represents the design matrix, and the second the vector of observations, whereas the function ls.diag(), provides regression diagnostics. A preferred function is, however, lm() to fit linear models, which can also be used to carry out regression, single stratum analysis of variance and analysis of covariance. This will be reviewed later in this chapter.

A closely related function is qr() which generates a matrix M into a product M - QR with an orthogonal matrix R and an upper triangular matrix R. QR decomposition is often used to solve the linear least squares problem, and is the basis for a particular eigenvalue algorithm, the QR algorithm.

## Matrix Creation, Concatenation, and Frequency

Matrices can be created by the functions cbind() and rbind(). As the name indicates the former binds vectors according to column and the latter according to row. When calling the cbind function the arguments must be vectors (of any length, with values cyclically repeated as necessary) or matrices of the same number of rows. The returned value will be a matrix with the arguments concatenated to form the columns. The same applies for rows with rbind(). Because the result of rbind() or cbind() always has matrix status their use is the simplest ways explicitly to allow a vector to be treated as a column or row matrix. 

```
> colarg1 <- c(1, 2, 3, 4, 5, 6)
> colarg2 <- c(7, 8, 9, 10, 11, 12)
> colarg3 <- c(13, 14, 15, 16)
> columned <- cbind(colarg1, colarg2, colarg3)
> columned
(snip)
> rowarg1 <- c(1, 2, 3, 4, 5, 6)
> rowarg2 <- c(7, 8, 9, 10, 11, 12)
> rowarg3 <- c(13, 14, 15, 16)
> rowed <- rbind(rowarg1, rowarg2, rowarg3)
> rowed
(snip)
```

Whilst the cbind() and rbind() are concatenation functions that respect dim attributes, the basic c() function does not, but rather clears numeric objects of all dim and dimnames attributes. This can also be useful at times. The preferred method of converting an array back to a vector is to use the as.vector() function.

```
> newveccol <- as.vector(columned)
> newvecrow <- c(rowed)
> newveccol
 [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 13 14
> newvecrow
 [1]  1  7 13  2  8 14  3  9 15  4 10 16  5 11 13  6 12 14
```

A factor defines a partition into groups. Similarly a pair of factors defines a two way cross classification, and so on. The function table() allows frequency tables to be calculated from equal length factors. If there are k factor arguments, the result is a k-way array of frequencies. Continuing the example (see 1.9) of the tax accountants distributed by state, a table of frequencies can be ordered and labelled by the levels attribute.

```
> statefr <- table(statef)
> statefr <- tapply(statef, statef, length)
```

Making use of the incomes, a incomef can be created as a factor giving a suitably defined income class for each entry in the data vector with the cut() function:

```
> factor(cut(incomes, breaks = 35+10*(0:7))) -> incomef
> table(incomef,statef)
(snip)
```

## Lists and Data Frames

A list in R list is an object consisting of an ordered collection of components. These components can be of different modes or types. For example, a list could consist of a numeric vector, a logical value, a matrix, a complex vector, a character array, a function, and so on. Here is a simple example of how to make a list:

`> WAlist <- list(name="WA", capital="Perth", no.mhr=15, no.senate=12)`

Components are always numbered and may always be referred to as such. Thus if WAlist is the name of a list with four components, these may be individually referred to as WAlist[[1]], WAlist[[2]], etc. The function length(WAlist) gives the number of (top level) components it has.

Components of lists may also be named, and in this case the component may be referred to either by giving the component name as a character string in place of the number in double square brackets, or by the component name. The names of components may be abbreviated down to the minimum number of letters needed to identify them uniquely (e.g.,  List$coefficients may be minimally specified as List$coe).


```
> WAlist[[1]]
> WAlist$name
```

The names of the list components in double square brackets, i.e., WAlist[["name"]] is the same as WAlist$name. This can be useful when the name of the component to be extracted is stored in another variable. The vector of names is in fact simply an attribute of the list like any other and may be handled as such. Other structures besides lists may, of course, similarly be given a names attribute also.

`> x <- "name"; Lst[[x]]`

New lists may be formed from existing objects by the function list() (e.g., Newlist <- list(name_1=object_1, ... name_n=object_n)). If these names are omitted, the components are numbered.  Lists, like any subscripted object, can be extended by specifying additional components. For example;

`> List[5] <- list(matrix=Mat)`

When the concatenation function c() is given list arguments, the result is an object of mode list also, whose components are those of the argument lists joined together in sequence.

`> list.ABC <- c(list.A, list.B, list.C)`

A data frame is a list with the class "data.frame". A data frame may be regarded as a matrix with columns possibly of differing modes and attributes. It may be displayed in matrix form, and its rows and columns extracted using matrix indexing conventions. Objects satisfying the restrictions placed on the columns (components) of a data frame may be used to form one using the function data.frame. Referring back to our Australian accountants:

`> accountants <- data.frame(home=statef, loot=incomes, shot=incomef)`

A list may be coerced into a data frame using the function as.data.frame(). However, the simplest way to construct a data frame from scratch is to use the read.table() function to read an entire data frame from an external file (discussed further on).

Image files can be attached, thus making objects in the file available on request. The attach() function makes the components of a list or data frame temporarily visible as variables under their component name, without the need to quote the list name explicitly each time. After being attached, assignments do not actually replace the components of the data frame, unless explicitly stated through the $ notation. To detach a data frame, use the function detach().

```
> attach(accountants)
> newloot <- loot * 1.5 # will not actually change the value in accountants but will create a new assignment.
> accountants$loot <- loot * 1.5 # will actually change the value in accountants
> detach(accountants)
> newloot
(snip)
> accountants
(snip)
```
Data frames are considered very useful if one is working with different problems in the same working directory as they allow for many temporary modifications.

## Files, Data, and Editing

When dealing with datasets of any size beyond the trivial, it is almost certain that these will exist as external files. These can be typically read in as a data frame by using the read.table() function which, as the name indicates, reads data in a table format. The external file will normally have a name for each variable in the data frame and each additional line of the file has as its first item a row label and the values for each variable. If the header is already in the data file, it can be optionally omitted.

```
> read.table("~/mathsprog/R/austpop.txt")
> austpop <- read.table("~/mathsprog/R/austpop.txt")
> austpop
(snip)
> austpop <- read.table("~/mathsprog/R/austpop.txt", header=TRUE)
> austpop
(snip)
```

An alternative is the very flexible scan() function, which can also read data from input streams (e.g., entered data or a file), and can be used to read almost any data type and in fixed or free file format. As part of scan() the 'what' option to specify the field type; with what=character() or what=" " then all the fields will be read as strings. If the data is a mix of numeric, string or complex data then a list can be used.  The default separator for the scan function is any white space (single space, tab, or new line), although this can be changed with the sep option. Unlike the read.table function which returns a data frame, the scan function returns a list or a vector. 

```
> scanpop <- scan("~/mathsprog/R/austpop.txt", skip=1)
Read 100 items
> scanpop
(snip)
> scanpop <- scan("~/mathsprog/R/austpop.txt", skip=1, what= list("","","","","","","","","",""))
Read 10 records
> scanpop
(snip)
```

In addition to these methods of reading data, there are also datasets built into the R, through the dataset package, and in some other packages. These can be listed with the data() function and can either be called directly by name or by the data(package) call.

```
> data()
..
austres                 Quarterly Time Series of the Number of
                        Australian Residents
(snip)
> austres
(snip)
```

To access data from a particular package, use the package argument. To determine which packages are already installed, use the library() command. 

```
> library()
(snip)
rpart                   Recursive Partitioning
> data(package="rpart")
> car90
(snip)
```

When called on a data frame or matrix, the edit() function brings an spreadsheet-like environment for data modification. It is common to call 'save' changes under a different name which can be done by reassignment. If the user wishes to modify original file then the fix() function can be used or assignment can be done itself. Note that this must be conducted on a local machine with the X-windows capabilities; not on the cluster.

`> auspopnew <- edit(auspop)`

## Probability

Unsurprisingly, R contains a great number of functions for probability. Qualitative or categorical data is where values belong to known, defined, and non-overlapping classes. This are the most common collection of data samples, and can include temperature measurements in locations, grades of work, economic growth by census collection districts, and so forth.

Using the library MASS, a data-frame of some fifty-four classical European painters can be loaded an analysed. One of the qualitative values is the school that they belong to, which is described in the help file. The absolute and relative distribution of the painters to the school can be simply and represented in column format if desired, as can (for example) the mean composition of a school, using the tapply() function.
  
```
> library(MASS)  
> school = painters$School 
> school.freq = table(school)
> school.freq 
(snip)
> help(painters)
> cbind(school.freq) 
(snip)
> school.relfreq = school.freq / nrow(painters) 
> school.relfreq 
(snip)
> cbind(school.relfreq) 
(snip)
> tapply(painters$Composition, painters$School, mean) 
(snip)
```

As another example, is the mean income, in thousands, for accountants in Australia can determined by the incomes vector established previously:

```
> mean(incomes)
[1] 54.73333
> sd (incomes)
[1] 8.349823
```

The probability of an income being 70 or less can be given by the normal distribution function. 

```
> pnorm(70, mean=54.73333, sd=8.349823)
[1] 0.9662539
>  pnorm(70, mean=54.73333, sd=8.349823, lower.tail=FALSE)
[1] 0.03374609
```

Another example is Poisson distribution, the probability distribution of independent event occurrences in an interval. In R Poisson, density, distribution function, quantile function and random generation for the Poisson distribution with parameter lambda. The following functions can be used, where x is the vector of non-negative quantiles, q is the vector of quatiles, p is the vector of probabilities, n is the number of random numbers to return, and lambda is the vector of non-negative means.

```
dpois(x, lambda, log = FALSE)
ppois(q, lambda, lower.tail = TRUE)
qpois(p, lambda, lower.tail = TRUE)
rpois(n, lambda)
```

Consider a fairly simple example where twelve new accountants enter a continiously growing firm in an average year, find the probability of having seventeen or more accountants joining in a particular year.

```
> ppois(16, lambda=12)   # lower tail 
[1] 0.89871 
> ppois(16, lambda=12, lower=FALSE)   # upper tail 
[1] 0.10129 
```

The following is a list of the available probability functions, their R name, and their arguments. As a short text that covers three mathematical languages a full elaboration does not occur here. However by this stage the implementation should be evident.

| Distribution	    | R name	        | Additional arguments  |
|:------------------|:------------------|:----------------------|
| beta		    | beta		| shape1, shape2, ncp   |
| binomial	    | binom		| size, prob	        |
| Cauchy	    | cauchy	        | location, scale	|
| chi-squared	    | chisq		| df, ncp		|
| exponential	    | exp		| rate			|
| F		    | f		        | df1, df2, ncp		|
| gamma		    | gamma		| shape, scale		|
| geometric	    | geom		| prob			|
| hypergeometric    | hyper		| m, n, k		|
| log-normal	    | lnorm		| meanlog, sdlog	|
| logistic	    | logis		| location, scale	|
| negative binomial | nbinom		| size, prob		|
| normal	    | norm		| mean, sd		|			      
| Poisson	    | pois		| lambda		|
| signed rank       | signrank		| n			|
| Student's t	    | t			| df, ncp		|
| uniform	    | unif		| min, max		|
| Weibull	    | weibull		| shape, scale		|	
| Wilcoxon	    | wilcox		| m, n			|
	

From an univariate data set its distribution can be examined in many ways. Two such examples summaries are given by summary and fivenum and a display of the numbers by stem, and by histogram. A plot the empirical cumulative distribution function by using the function ecdf. The latter examples requires some graphical capability so it should be conducted on a local display, not the cluster. The example uses the built-in dataset faithful, based on a set of observations of the famous Old Faithful geyser in Yellowstone National Park in the U.S.A.

```
> attach(faithful)
> summary(eruptions)
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max.
  1.600   2.163   4.000   3.488   4.454   5.100
> fivenum(eruptions)
[1] 1.6000 2.1585 4.0000 4.4585 5.1000
> stem(eruptions)
(snip)
> hist(eruptions)
## make the bins smaller, make a plot of density
> hist(eruptions, seq(1.6, 5.2, 0.2), prob=TRUE)
> plot(ecdf(eruptions), do.points=FALSE, verticals=TRUE)
> detach(faithful)
```

A common operation is to compare aspects of two samples. Consider the following sets of data on the latent heat of the fusion of ice (cal/gm) from Rice (1995, p.490) Boxplots provide a simple graphical comparison of the two samples.

```
> A <- scan()
1: 79.98 80.04 80.02 80.04 80.03 80.03 80.04 79.97
9: 80.05 80.03 80.02 80.00 80.02
14: 
Read 13 items
> B <- scan()
1: 80.02 79.94 79.98 79.97 79.97 80.03 79.95 79.97
9: 
Read 8 items
> boxplot(A, B)
> t.test(A, B)
        Welch Two Sample t-test
data:  A and B
t = 3.2499, df = 12.027, p-value = 0.006939
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 0.01385526 0.07018320
sample estimates:
mean of x mean of y 
 80.02077  79.97875 
```

## Basic Statistical Models

R provides a suite of functions and facilities that make statistical models relatively simple a number of which are illustrated here. Basic statistical numerical measures, such as mean, median, quartile, range, interquartile, variance, standard deviation, etc, are all built in as functions.

```
> head(faithful)
(snip)
> duration = faithful$eruptions 
> mean(duration)  
 [1] 3.487783
> median(duration)
[1] 4 
> quantile(duration) 
     0%     25%     50%     75%    100% 
1.60000 2.16275 4.00000 4.45425 5.10000 
> quantile(duration, c(.22, .58, .87)) 
    22%     58%     87% 
2.05408 4.15000 4.63300 
> range <- max(duration) - min(duration)
> range
[1] 3.5
> IQR(duration)
[1] 2.2915
> var(duration) 
[1] 1.302728
> sd(duration)
[1] 1.141371
```

Covariance, a positive resulting indicating the presence of a linear relationship between two variables in sample, also has its own function. A simple example is the duration of eruptions of the aforementioned Old Faithful geyser and the duration between eruptions. From a covariance it is possible to derive a correlation coefficient by dividing the covariance of two variables by the product of their individual standard deviations to derive a normalised measurement. This also has its own function.

```
> waiting = faithful$waiting   
> cov(duration, waiting)       
[1] 13.978 
>  cor(duration, waiting)
[1] 0.9008112
```

R also provides various tools for interval estimations, to estimate population parameters based on simple random sample data. Using the MASS library, a survey of University of Adelaide students can provide a point estimation mean, and accuracy levels when the standard deviation is known and unknown.

```
> library(MASS)
> help(survey)
> head(survey) 
(snip)
>mean(height.survey)
[1] NA
> mean(height.survey, na.rm=TRUE) # Not everyone answered
(snip)
> height.response = na.omit(survey$Height) # filter out non-responses
> n = length(height.response) 
> sigma = 9.48                   # population standard deviation 
> sem = sigma/sqrt(n); sem       # known standard error of the mean 
[1] 0.65575
> E = qnorm(.975)∗sem; E         # margin of error 
[1] 1.2852 
> xbar = mean(height.response)   # sample mean 
> xbar + c(-E, E) 
[1] 171.10 173.67 # 95% confidence
> t.test(height.response) # unknown standard deviation with 95% confidence
(snip)
```

R also provides functions for hypothesis testing from a population. For example, consider the claim that a vehicle only requires a service every 10,000 kilometers, but after thirty tests, a service was required every 9,900 kilometers. From this test population the standard deviation is 120 hours. With a .05 significance level, the claim can be rejected with the following:

```
> required <- 9900 
> claimed <- 10000 
> testsd <- 120            # population standard deviation 
> n <- 30                 # sample size 
> test <- (required-claimed)/(sigma/sqrt(n)) 
> test
[1] -4.5644 
> alpha <- .05 
> z.alpha <- qnorm(1-alpha) 
> -z.alpha  # critical value 
[1] −1.6449 
> # test greater than -z.alpha, therefore claim rejected
> # test against type II error 
> alpha = .05 # significance level 
> sem = testsd/sqrt(n); sem # standard error
> q = qnorm(alpha, mean=claimed, sd=sem); q 
[1] 9964
> # So long as the sample mean is greater than 9964 in a hypothesis test, the null hypothesis will not be rejected.
> # Lies, damned lies, and statistics!
```

## Conditions, Loops, and Functions 

As R has variables, arrays, and assignments it is perhaps not surprising to discover that it has programming functionality as well which is only introduced here. Specifically examples are given here for loops (for, repeat, while) and condition statements (if else). Knowledge of R programming is useful for writing one's own R function. 

The repeat loop it will execute a block of commands until (repeat-until) it reaches a conditional break 

```
> for (celsius in 25:30)
+  print(c(celsius, 9/5*celsius + 32))
(snip)
```

A while() loop will execute a block of commands (do-while) until the condition is no longer satisfied, and takes the general form of while(cond) expr. A next statement can skip part of the loop, and a break will end it. 

```
> i <- 0 
> while(i < 5) {i <- i+1; if (i == 3) next; print(i);} 
(snip) 
```

The for loop of the R language is written in the form  for (i in vector) {expr1; expr2 ...}. A break statement can be used to terminate the loop abruptly. 

```
> vector <- c(1:10)) 
> vector 
 [1]  1  2  3  4  5  6  7  8  9 10 
> for (element in vector) 
+ { 
# +    if (element == 3) break #stop at three 
# +    if (element %% 2 == 0) next # ignore even elements 
+    str <- paste(element,"is current element",sep=" ") 
+    print(str) 
+} 
(snip) 
```

The if condition has already been encountered in the loops above as conditional tests. It can be expanded into a general form as if (condition) {exp} else {exp}  and can be nested. 

```
>vector <- c(1:10) 
>vector 
 [1]  1  2  3  4  5  6  7  8  9 10 
>for (element in vector) 
+{ 
+    if (element %% 2 != 0) next 
+    else print(element) 
+} 
```

Loops and conditions can be used in the writing of user-defined functions in R, whose general form is as follows: 

```
functionname <- function(arg1, arg2, ... ){ 
statements 
return(object) 
} 
```

The following is an example of approximately converting miles to kilometers.

`> miles.to.km <- function(miles)miles*8/5`

The return value is the value of the final (and in this instance only) expression that appears in the function body. Use the function thus

```> miles.to.km(175)  # Approximate distance to Sydney, in miles
[1] 280```

The function will do the conversion for several distances all at once. To convert a vector of the three distances 100, 200 and 300 miles to distances in kilometers, specify:

```> miles.to.km(c(100,200,300))
[1] 160 320 480```

The very short but complex function below computes Fibonacci numbers recursively. 

```
> fib <- function(n) if (n>2) c(fib(n-1),sum(tail(fib(n-1),2))) else if (n>=0) rep(1,n) 
> fib(17) 
(snip)
```

## Graphics

Most of this course has concentrated on providing the computational side to R, designed for use on the cluster. However there are also a number of graphical functions, some of which are described here. These should be tested against a local installed, not the cluster installation. Some examples include the functions plot(), points(), lines(), text(), mtext(), axis(), identify() etc. form a suite that plots points, lines and text. To see some of the possibilities that R offers, enter 

`> demo(graphics)`

The plot() function is perhaps the most typically used. The plot it produces depends on the type or class of the arguments. For example, in the expression plot(x, y), if x and y are vectors then a scatterplot is produced (obviously x and y must be same length), or as the expression plot(xy) when x is a list containing two elements x and y or a two-column matrix. If x is a time series however, plot (x) will produce a time-series plot. If it is a numeric vector, it will produce a plot of the vector values against the index. In all cases, titles, axes, points, lines, and text may be added to a plot with the appropriate functions. The default settings of parameters can be changed with the parameter function, par() function. 

```
> plot((0:20)*pi/10, sin((0:20)*pi/10)) 
> plot(cos, -pi,  3*pi) 
> plot(qlogis, main = "The Inverse Logit : qlogis()") 
> austpop <- read.table("austpop.txt", header=TRUE) 
> plot(ACT ~ Year, data=austpop, type="l") 
> par(cex=1.25)  # character expanions; increases the text and plot symbol size 25% above the default. 
> plot(ACT ~ Year, data=austpop, type="b", xlab="Timeline", ylab="Thousands of People", label="ACT Population") 
```

There is quite a range of potential plot functions, including the following:

```
splom( ~ data.frame)
# Scatterplot matrix
bwplot(factor ~ numeric , . .)
# Box and whisker plot
qqnorm(numeric , . .)
# normal probability plots
dotplot(factor ~ numeric , . .)
# 1-dim. Display
stripplot(factor ~ numeric , . .)
# 1-dim. Display
barchart(character ~ numeric , . .)
histogram( ~ numeric , . .)
densityplot( ~ numeric , . .)
# Smoothed version of histogram
qqmath(numeric ~ numeric , . .)
# QQ plot
splom( ~ dataframe, . .)
# Scatterplot matrix
parallel( ~ dataframe, . .)
# Parallel coordinate plots
cloud(numeric ~ numeric * numeric, . .)
# 3-D plot
contourplot(numeric ~ numeric * numeric, . .)
# Contour plot
levelplot(numeric ~ numeric * numeric, . .)
# Variation on a contour plot
```

The following is a complete example of how to create a PNG file, which can be done either on the cluster or the local machine.

```
> png("myplot.png", bg="transparent", width=700, height=500)
> data(volcano)
> x <- 10 * (1:nrow(volcano))
> y <- 10 * (1:ncol(volcano))
> contour(x, y, volcano, levels = seq(90, 200, by = 5))
> axis(1, at = seq(100, 800, by = 100))
> axis(2, at = seq(100, 600, by = 100))
> box()
> title(main = "Maunga Whau Volcano", font.main = 4)
> dev.off()
```

![Image of ](https://github.com/VPAC/matappprog/blob/master/chapter01/MaungaWhau.png)

