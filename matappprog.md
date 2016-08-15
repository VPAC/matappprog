# Introduction

## Foreword



## Preface

From a naive perspective, it is initially surprising to discover that there are multiple mathematical application and programming languages. "Surely", the reasoning goes, "all computation is a mathematical problem. Do we really need this multiplicity of languages?" Of course, when one comes to the realisation that there are multiple subfields of mathematics and the ways that these are structures and, in using their "quasi-empiricism" (to use the phrase perhaps first used by Imre Lakatos), they will have different ways of interacting with the actual computer system itself and with varying levels of efficiency and effectiveness. Thus, different mathematical programming languages. 

In one sense, mathematical programming is an optimisation problem; the selection of the best solution from available solutions. This is certainly a major treatment of the well-known journal "Mathematical Programming". Whilst important, it is only indirectly referred to in this publication, except perhaps in analogy with the slight change in title: 'Mathematical Applications and Programming'. In providing an introduction to three major mathematical applications and programming languages that are available as free and open-source products - R, Octave, and Maxima - as the best solution for three different types of mathematical problems - statistics, numerical computation, and symbolic computation. In addition to this there are always new developments in the field and emergent technologies such as Julia and UNUMs are explored in the final chapter.

Of course there are some similarities involved. Each of these applications and languages will have their own procedures for installation, on where to find online help. They each have their own way of handling different data types, managing variables and functions, and incorporating these into scripts and programs, as well as different ways of providing graphical visualisation. As far as broad categories are concerned, mathematical computation has at least some conceptual areas in common - and as it should be. After all, mathematics is neither just an art, a science, or a law, but as philosophy, it is the language of the universe. 

"Philosophy is written in this grand book, which stands continually open before our eyes (I say the 'Universe'), but can not be understood without first learning to comprehend the language and know the characters as it is written. It is written in mathematical language, and its characters are triangles, circles and other geometric figures, without which it is impossible to humanly understand a word; without these one is wandering in a dark labyrinth."

Galileo Galilei, Il Saggiatore (1623)

Source material this book has primarily come from the official documentation of the relevant progamming languages, that is, "An Introduction to R" (2015), "GNU Octave: A high-level interactive language for numerical computations" (2015), "Maxima 5.37.3 Manual" (2015), "The Julia Manual" (2015), along with "The End of Error: Unum Computing" by John Gustafson (2015), "Learning R" by Richrd Cotton (2013), "GNU Octave: Beginner's Guide" (2011) by Jesper Schmidt Hansen, "The Maxima Book" (2003) by Paulo Ney de Souza, Richard J. Fateman, Joel Moses, and Cliff Yapp, the frankly quite brilliant "Classical Mechanics with Maxima" (2016) by Todd Keene Timberlake, and J. Wilson Mixon.Jr., and, interestingly, "MATLAB(R) For Engineers" (2012) by Holly Moore.

Another particular feature of this book however, is that it is particularly designed from the perspective of using high-performance computing and as an educational text. This makes it a little different from the numerous similar texts that are available for the various programming environments that are covered here. This difference is, of course, contextual. Much of the material draws upon training manuals produced at the Victorian Partnership for Advanced Computing over the past several years.

One point must be emphasised however; there is a temptation to use computational systems to conduct mathematical operations without understanding the concepts behind those operations. There is some great dangers in doing this. Firstly, it means that that the user will not be able to recognise their own input errors and incorrect reasoning - garbage in and garbage out. Secondly, they will miss errors in the program, and especially those tied to some of the problems related to some inherent problems in computation (the aforementioned book by John Gustafson is a very interesting exploration in this subject).

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


# Numerical Computations with Octave

## About Octave and Setup

GNU Octave is a free and open source high-level software language for linear and non-linear numerical computations that is mostly compatiable with the commercial product MATLAB. An Octave program will usually run without modification on MATLAB, although the reverse is slightly less the case, as MATLAB has a larger collection of specialised and propertairy libraries. 

Octave provides an  interactive command line interface and may also be used as a batch-oriented language for data processing. It is written in C++ and can be used with GNU Plot or Grace for plotting.

The origins of Ocatave date back to 1988 when it was intended to be a companion to a chemical reactor course. Serious development was initiated by John W. Eaton in 1992, with an alpha release in 1993 and version 1.0 was released in 1994. Version 3.0 was released in late 2007. Ocatve is named after Octave Levenspiel, emeritus professor of chemical engineering at Oregon State University who taught Eaton.

On high performance clusters with environment modules enables, different versions of octave may be available. These can be invoked and illustrated by logging on to such an HPC system as follows:

```
bash-4.2$ ssh train12@trifid.in.vpac.org
[train12@trifid ~]$ qsub -l walltime=12:00:0,nodes=1:ppn=2 -I
[train12@trifid-35 ~]$ module avail octave
--------------------- /usr/local/Modules/modulefiles octave/3.6.3(default)
[train12@trifid035 ~]$ module avail gnuplot
----------- /usr/local/Modules/modulefiles 
gnuplot/4.6.1(default)
[train12@trifid035 ~]$ module load octave gnuplot
```

The submission of an interactive job to a cluster node is always preferred to running jobs on the login node, even low-intensity jobs such as interactive Octave.

For each of these applications only the most recent version has been installed on the cluster and they have been set as the default for that application. As a result the environment paths can be added without defining their version numbers.

Once loaded Ocatave can be started by simply typing 'octave', which awaits commands for interpretation. To see the range of options on launch use 'octave --help' or just 'octave -h'. To interrupt Octave, Cntrl-C will return the user to the Octave prompt. To exit Octave use ''quit' or 
'exit' at the prompt. If an optional integer status is provided, that value is passed to the operating system as Octave’s exit status.

```
[train12@trifid035 ~]$ octave
GNU Octave, version 3.6.3 
…
warning: X11 DISPLAY environment variable not set
octave:1>
```

## Help, Editing, and Errors

The command "doc" in Octave will provide an extensive manual.  If this is not installed it can be accessed through the URL: `http://www.gnu.org/software/octave/doc/interpreter/Getting-Help.html`. If the documentation is installed, the command `doc` followed by the function name will provide information concenrning that function, whereas `lookfor` followed by the function name will conduct a search for the the term.

In addition to this there is documentation for various functions and variables via the help command, followed by the name of the individual command or function. The request help --list  will provide a full list of the operators, keywords, bult-in and loadable functions available.

Editing the Octave command line is typically simply a case of entering text with the cursor advancing appropriately. However Octave uses the GNU Readline library which comes with various features worthy of note as follows:

| Commands		| Effect				  	  |
|:----------------------|:------------------------------------------------|
| Cntrl-b, Cntrl-f 	| Move cursor back or forward one character	  |
| Cntrl-a, Cntrl-e 	| Move cursor to the beginning or end of the line |
| Esc+b, Esc+f 		| Move cursor back or forward on word		  |
| Cntrl-l, clc(),home() | Clear the screen.				  |	
| Cntrl-/, Esc+r 	| Undo last action, undo all actions on this line |
| Cntrl-k 	 	| Clear ("kill") text from cursor to end of the line	  |
| Esc+d 		| Clear ("kill") text to the end of the current word	  |
| Cntrl-y 		| Paste ("yank") the most recently cleared text	  |
| Esc+y 		| Rotate the kill-ring, and yank the new top.	  | 
| Cntrl-t, Esc+t 	| Drag the character, or word, before the cursor forward over the character at the cursor, also moving the cursor forward |
|Cntrl-v 		| Add the next character that you type to the line in raw mode; effectivey escapes the control characters |		
| <tab> 		| Tab completion				  |
| Cntrl-p, Cntrl-n 	| Move up and down through the history list.	  |
| Esc+<, Esc+> 		| Move to first and last line of history	  |
| Cntrl-R, Cntrl-S 	| Search backward and forward through history list|


As with many other languages, comments in Octave are prefixed with the # or % symbol on a single line. Blocks of code can be commented by enclosing the code between matching ‘#{’ and ‘#}’ or ‘%{’ and ‘%}’ markers. 

Octave reports two kinds of errors for invalid programs.  A parse error occurs if Octave cannot understand something a user has typed. For example, if a mispelled keyword;

`octave:1> functon y = f (x) y = x^2; endfunction`

Octave will respond immediately with a message like this: 

`parse error:`
`  functon y = f (x) y = x^2; endfunction`
`          ^`

For most parse errors, Octave uses a caret (‘^’) to mark the point on the line where it was unable to make sense of your input. In this case, Octave generated an error message because the keyword function was misspelled. Instead of seeing `function f`, Octave saw two consecutive variable names, which is invalid in this context. It marked the error at y because the first name by itself was accepted as valid input. 

Another class of error message occurs at evaluation time. These errors are called run-time errors, or sometimes evaluation errors because they occur when the user's program is being run, or evaluated. For example, if after correcting the mistake in the previous function definition, the user typed;

`octave:3> f ()`
Octave will respond with 
`error: `x' undefined near line 1 column 24`
`error: evaluating expression near line 1, column 24`
`error: evaluating assignment expression near line 1, column 22`
`error: called from `f'`

This error message has several parts, and gives you quite a bit of information to help the user locate the source of the error. The messages are generated from the point of the innermost error, and provide a traceback of enclosing expressions and function calls. 

## Data and Argumentation Types

Octave includes a number of built-in data types, including real and complex scalars and matrices, character strings, a data structure type, and an array that can contain all data types. A numeric constant may be a scalar, a vector, or a matrix, and it may contain complex values. A scalar is a single number that can be an integer, a decimal fraction, a number in scientific notation, or a complex number. By default numeric constants are represented within Octave in double-precision floating point format. A string constant consists of a sequence of characters, of any length, enclosed in either double-quote or single-quote marks. However, as the single quotation mark is also used as the transpose operator most Ocatve users consider the double quotation marks to be preferable.

Octave includes support for two different mechanisms to contain arbitrary data types in the same variable. These are (i) Structures which are indexed with named fields, and (ii) cell arrays, where each element of the array can have a different data type and or shape. A structure contains elements, and the elements can be of any type. Structures may be copied and structure elements themselves may contain structures (which can contain structures and so forth). However Octave will not display to standard output all levels of a nested structure. In contrast, with a cell array several variables of different size and value can be stored in one variable. Cells are indexed by the { and } operators and can be inserted, retrieved, or changed from from this index.

```
octave:1> x.a = 1; 
octave:2> x.b = [1, 2; 3, 4]; 
octave:3> x.c = "string"; 
octave:4> x 
(snip)
octave:5:> y = {"a string", rand(2, 2)};
octave:5:> y{1:2}
(snip)
octave:6:> y{3} = 3;
(snip)
```

The final data container of note deserves special mention as it is so common as both an input and an output argument type; comma-separated lists. Elements of a cell array can be extracted into a comma separated list with the { and } operators and using [ and ], elements can be concatenated into an array. 

```
octave:7:> z{3} = 3;
octave:8> a = {1, [2, 3], 4, 5, 6}; 
octave:9> b = [a{1:4}] 
(snip)
```

## Numerical Data Types

Numerical data types in Octave may be a scalar, vector, or matrix, and may contain complex values. By default numeric constants are in double-precision floating-point format, with complex constants as pairs of double-precision floating point values. Various functions can conduct conversions between numeric data types, such as double(x) which will convert x to a double precision type. Likewise the function single(x) will convert x to a single precision type. Most of the functions in Octave accept single precision values and return single precision answers. 

Octave also supports integer matrices, both signed and unsigned represented by 8, 16, 32, or 64 bits. Most computations however require floating point calculations. Integers are most commonly used to store data, rather calculations. Consider the following randomnly generated matrix.

```
octave:26> float = rand (2, 2)
(snip)
octave:27> integer = int32 (float)
(snip)
```

In Octave, the size of a matrix is determined automatically. but it is up to the user to ensure that the rows and columns match.

```
octave:1> octa = [1, 2; 3, 4]
(snip)
octave:2> [octa, octa ]
octave:3>  [octa, 1 ]
error: horizontal dimensions mismatch (2x2 vs 1x1)
```

Whitespace is important - sometimes. For example, where there is no ambiguity in meaning Octave will simply consider whitespace as unimportant. However there is possibility that the whitespace could be interepreted as part of a calculation and the lack of whitespace as a value.

```
octave:3>  octa = [ 1 2
>            3 4 ]
(snip)
octave:4> [ 1 - 1 ]
ans = 0
octave:5>   [ 1 -1 ]
(snip)
```

Because the single quote character (') is used as both a transpose character and for quotating strings, this is another potential source of confusion.

```
octave:15> var = 1
var =  1
octave:16> [ 1 var' ]
(snip)
octave:17> [ 1 var ' ]
(snip)
octave:17> [ a 'var' ]
ans = var
```

## Strings

A string in Octave is an array of characters. Internally the string "ddddd" is actually a row vector of length 5 containing the value 100 in all places (because 100 is the ASCII code of "d"). Using a matrix of characters, it is possible to represent a collection of same-length strings in one variable. The convention used in Octave is that each row in a character matrix is a separate string, but letting each column represent a string is equally possible.

The escape sequences in Octave are the same used in the C programming language, so users familiar with both will readily adapt. In double-quoted strings, the backslash character is used to introduce escape sequences that represent other characters.  In single-quoted strings however, the backslash is not a special character.  Consider the application of the toascii() function which converts a value to ASCII in a matrix.

```
octave:17> toascii ("\n") 
ans =  10 
octave:18> toascii ('\n') 
ans = 
   92   110 
```

The following is a table of all the escape sequences.

| Escape Cod	| Result					|
|:--------------|:----------------------------------------------|
| \\ 		| A literal backslash, ‘\’			|	
| \" 		| A literal double-quote character, ‘"’		|
| \' 		| A literal single-quote character, ‘'’		|
| \0 		| The “nul” character, control-@, ASCII code 0	|
| \a 		| The “alert” character, control-g, ASCII code 7|
| \b 		| A backspace, control-h, ASCII code 8		|
| \f 		| A formfeed, control-l, ASCII code 12		|
| \n 		| A newline, control-j, ASCII code 10		|
| \r 		| A carriage return, control-m, ASCII code 13	|
| \t 		| A horizontal tab, control-i, ASCII code 9	|
| \v 		| A vertical tab, control-k, ASCII code 11	|

With a single-quoted string there is only one escape sequence: two single quote characters in succession with generate a literal single quote.

The easiest way to create a character matrix is to put several strings together into a matrix.

`charmat = [ "String #1" " String #2" ; "String #3" " String #4" ];`

If a character matrix is created from strings of different length (as in the above example)Octave puts blank characters at the end of strings shorter than the longest string. It isn't possible to represent strings of different lengths, although it is possible to have a cell array of strings. 
                 
Since a string is a character array, comparisons between strings work element by element. The strcmp(s1,s2) function will compare complete strings with case sensitivity. In comparison strncmp(s1,s2,N) compares only the first N characters. Case-insentive functions which are equivalent are strcmpi and strncmpi. As a search function, of sorts, validatestring(str,strarray) will validate the existence of a case insenstive string with the strotest match. 
                 
```octave:24> validatestring ("RED", {"redrum","red", "green", "blue", "black", "reddish"})
ans = red```
           
There is a variety of functions for string manipulation and conversions. Because a string is just a matrix standard operators can be used for a variety of changes.

e.g., search and replace

```octave:44> quote="The quick brown fox jumps over the lazy dog"
quote = The quick brown fox jumps over the lazy dog
octave:45> quote(quote==" ") = "_"
quote = The_quick_brown_fox_jumps_over_the_lazy_dog```

Other functions like deblank(s) removes trailing whitespaces s, strtrim(s) removes leading and trailing whitespace, strtrunc (s, n) will truncate the string s to length n. Useful conversion functions include bin2dec(s), which will convert binary to decimal or dec2bin(s) which conducts the reverse. A more elaborate version is dec2base(s,base) which will convert a string of digits in a variable base to a decimal integer, and  dec2base(d,base) which will do the reverse. The function str2double(s) will convert a string to a real or complex number.

## Simple Matrix Mathematics
 
Like the text "MATLAB 7 Getting Started Guide" (Mathworks, 2008), this guide will illustrate the features Octave using Albrecht Dürer's magic square found in detail of the print Melencolia I. This print itself has been subject to more interpetation than almost any other uin history (indeed a two-volume study was written on it). The order-4 magic square itself was noted in other cultures, but is believed to be the first time illustrated in Europen art.

To enter Dürer into Octave as a variable and matrix simply enter the following on the Octave command line. The entries represent rows in the matrix with individual values seperated with a comma and each end of row separted with a semi-colon. Note that without the semi-colons, the result would be a simple row vector. With semi-colons after each element it would be a column vector.

In this case however Octave helpfully responds with the entries as a matrix. To prevent this behaviour and just store the variable add a semicolon at the end.

```
octave:1> A = [16 3 2 13; 5 10 11 8; 9 6 7 12; 4 15 14 1]
A =
   16    3    2   13
    5   10   11    8
    9    6    7   12
    4   15   14    1
octave:2> A = [16 3 2 13; 5 10 11 8; 9 6 7 12; 4 15 14 1];
```

As with other magic squares in recreational mathematics, Dürer's has a number of features which are useful for illustrating some of the core features iof Octave. The function sum(A) for example with give the results of the sum of the columns. The column vector of the row sums can be achieved by transposing the the matrix. The apostrophe operator (e.g., A') conducts a conjugate transposition (A.' would just transpose), changing the row vectors in to column vectors, thus sum(A') producing the sum of the transpositions, and sum(A')' producing a column vector of the row sums, and sum(diag(A)) providing the sum of the main diagonal (top-left to bottom-right). The sum the bottom-left to top-right can be calculated by flipping the matrix left to right, i.e., sum(diag)(flip(A)).

```
octave:3> sum(A)
(snip)
octave:4> sum(A')
(snip)
octave:5> sum(A')'
(snip)
octave:6> sum(diag(A))
(snip)
octave:7> sum(diag(fliplr(A)))
(snip)
```

## Variables and Operations

Octave can store data in variables. Sometimes these can be very simple, like a one-by-one matrix. Variables must begin with a letter or a underscore and can be followed by letters, numbers, or underscores. However, variables that begin and end with two underscores are reserved for internal use by Octave; as a result it is usually best just to start with a letter. Variables are also case-sensitive. The maximum length for a variable can be determined by invoking the function namelengthmax (63 on trifid.vpac.org), although why one would want a variable that long is moot. Note that the built-in variable ans will always contain the result of the last computation.

Numbers in Octave are expressed in standard decimal notation optional decimal and  positive or negative signs. Scientific notation uses the standard e to representa a power of 10 notation, and imaginary numbers use i or j as a suffix. Standard notion (+, -, *, /, ^) and precedence (functions, transpose, exponent., logical not., multiply and divide., addition and subtraction., logical and and logical or., assignment) rules apply. Less typical notatiuon includes "left division" (\) for linerar algebra, ' (complex conjugate transpose), power operations (**). 

Simple arithematic, trigonomic, inverse trigonomic, natural and base 10 logarithms, and absolute values can be carried out with Octave with sin, cos, tan, asin, acos, and atan. For logorithms, use log or log10. For absolute values use abs. The following examples illustrate these functions:

```
octave:5> 6 / 2 * 3
ans =  9
octave:6> 6 / (2 * 3)
ans =  1
octave:7> A(1,4)+A(2,4)+A(3,4)+A(4,4)
ans =  34
octave:8> log10(100)/log10(10)
ans =  2
octave:9> sqrt(3^2 + 4^2)
ans =  5
octave:10> floor((1+tan(1.2)) / 1.2)
ans =  2
```

Line 7, whilst a simple example in terms of arithmatic, illustrates matrix addition of subelements, being the addition of the elements (row 1, column 4) plus (row 2, column 4) plus (row 3, column 4), and (row 4, column 4).

When there are two matrices of the same size, element by element operations can be performed on them. For example, the following divides each element of A by the corresponding element in B:

```
octave:11> A1 = [1, 6, 3; 2, 7, 4]
(snip)
octave:12> A2 = [2, 7, 2; 7, 3, 9]
(snip)
octave:13> A1 ./ A2
(snip)
```

The dot divide (./) operator is used perform element by element division. There are similar operators for addition (.+), subtraction (.-), multiplication (.*) and exponentiation (.^). In addition Octave also has a syntax for left division (\), which is equivalent of inverse(x) * y, and element-by-element left division (.\), and transpose (.'). Note that when a potentially ambigious statement is made (e.g., 1./m) Octave by default treats the dot as part of the operator, rather than the constant i.e., (1)./m, rather than (1.)/m.

Various constants are also pre-defined: pi, e (Euler's number), i and j (for the imaginary number sqrt(-1)), inf (Infinity), NaN (Not a Number - resulting from undefined operations, such as Inf/Inf). e.g.,

```octave:14> e^(i*pi)
ans = -1.0000e+00 + 1.2246e-16i```

Octave also includes standard comparison operations, less than (<), less than or equal (<=), equal (==), equal or greater than (>=), greater than (>), and not equal (~=, !=). Boolean operator are also in use for "or" (|), and (&), and not (!). These can be applied on an element-by-element listing as well. 

Increment operators increase (++) or decrease (--) the value of a variable by one. If the expression is on the left hand side of the variable (++x, --x) the value of the expression is the new value of the variable (equivalent to x = x +1 or x = x -1). If it is on the right-hand side (x++, x--), the value of the expression is the old value of x.

Automatic generation of vectors with a consistent increment takes the form of Start[:Increment]:End 

```
octave:15> rv = [1:2:11]
rv =
    1    3    5    7    9   11
octave:16> rv2 = [1:11]
rv2 =
    1    2    3    4    5    6    7    8    9   10   11
```

Note the use of the colon; this can vary in Octave. In the above case it acts as a delimiter for increments, or for an automatic inrementor. In subscript it can be used to refer to incremented portions of a matrix, for example the sum of the first four elements of column 4, or all the elements of column 4 (in this case that's the same).

```
octave:17> sum(A(1:4,4))
ans =  34
octave:18> sum(A(:,end))
ans =  34
```

Stepping outside of the major square for a moment, Octave can also carry out set operations. There are different core set operations in octave basically Octave can use vector, cell arrays or matrix as its set input operation.

Given two simple matricies, union, intersection, can be illustrated as follows:

```
octave:19> Aset=[1 2 3]
..
octave:19> Bset=[3 4 5]
..
octave:19> union(Aset,Bset)  
ans =
   1   2   3   4   5
octave:26> intersect(Aset,Bset)
ans =  3
```

The difference operation, also called as the a-b operation, returns those element of a that are not in b.

```octave:27> setdiff(Aset,Bset)
(snip)```

The Octave function ismember compared and the those elements that are present in the second set are marked as true rest are marked as false.

```octave:28> ismember(Aset,Bset)
(snip)```

Finally, the function setxor returns the elements exclusive to the sets listed in ascending order.

```octave:29> setxor(Aset,Bset)
(snip)```

## Manipulating Matrices

Matrix mathematics is the foundation of Octave. Unsurprisingly there are several ways that a matrix can be created. The function zeroes(a,b) will created matrix with zeroes assigned to all elements in cells across a,b rows and colums, the function ones(a,b) will do the same except with the value 1 assigned to the elements, rand(a,b) will do the same with uniformally distributed elements, randn(a,b) with normally distributed random elements. The range of random numbers can also have the fractional component truncuated leaving an integer. When added to a multiplier this provides a range. Martrices can, and typically are, assigned to a variable. For example to generate ten numbers from between 1 and 100;

```
octave:19> d100=fix(101*rand(1,10))
d100 =
   58   97   86   95   29   28   86   66   20   9
```

Remember that indicies begin with 0. 

Matrices can be concatenated by adding existing matricies together or by providing a mathematic operation on them. For example, starting with the initial example, another set of rows and columns may be added. e.g.,

```
octave:20> A = [16 3 2 13; 5 10 11 8; 9 6 7 12; 4 15 14 1]
(snip)
octave:21> B = [A A+32; A+48 A+16]
(snip)
```

The following is a list of some of the common functions for matrix manipulation available in Octave. 

| Function	| Result					|
|:--------------|:----------------------------------------------|
| tril(A)	| Returns the lower triangular part of A	|
| triu(A)	| Returns the upper triangular part of A	|
| eye(n)  	| Returns the n\times n identity matrix. You can also use eye(m, n) to return m\times n rectangular identity matrices	|
| ones(m, n)	| Returns an m\times n matrix filled with 1s. Similarly, ones(n) returns n\times n square matrix. |
| zeros(m, n)	| Returns an m\times n matrix filled with 0s. Similarly, zeros(n) returns n\times n square matrix. |
| rand(m, n)	| Returns an m\times n matrix filled with random elements drawn uniformly from [0, 1). Similarly, rand(n) returns n\times n square matrix.	|
| randn(m, n)	| Returns an m\times n matrix filled with normally distributed random elements.	|
| randperm(n)	| Returns a row vector containing a random permutation of the numbers 1, 2, \ldots, n.	|
| diag(x) or diag(A).	| For a vector, x, this returns a square matrix with the elements of x on the diagonal and 0s everywhere else. For a matrix, A, this returns a vector containing the diagonal elements of A.	|

## Indexing Matrices

Index expressions in Octave permit the referencing or extracting selected elements of a matrix or vector. Indices can be scalars, vectors, ranges, or the special operator ‘:’, which can be used to select entire rows or columns, or elements in order of row then column. For example, given a simple matrix, the following basic selections can be easily established.

```
octave:22> z=[4 3 ; 2 1]
(snip)
octave:25> z(1,3)
error: A(I,J): column index out of bounds; value 3 out of bound 2
octave:26> z(2,1)
ans =  2
octave:27> z(2,2)
ans =  1
octave:28> z(1)
ans =  4
```

Additional bracketing within the selection ([x, y]) provides column selections. All of the following expressions are equivalent and select the first row of the matrix. The colon operator (:) can be used to select all rows or columns from a matrix.

```
octave:29> z(1, [1, 2])  # row 1, columns 1 and 2
octave:30> z(1, 1:2)     # row 1, columns in range 1-2
octave:31> z(1, :)       # row 1, all columns
```

A range of rows or columns can also be selected from a matrix in the general form of: start:step:stop

The first number in the range is start, the second is start+step, the third, start+2*step, etc. The last number is less than or equal to stop.

Rows and columns can be deleted from an Octave matrix using square brackets [] to represent null. Applying this to specific rows and columns can be achieved by using the colon as a separator between rows and columns, and the comma to distinguish particular colums. For example to remove column 3 then row 1.

```
octave:32> X=A
(snip)
octave:33> X(:,3)=[]
(snip)
octave:34> X(1,:)=[]
(snip)
```

A single element cannot be deleted from a matrix (e.g., X(1,2)=[]), because that would mean it is no longer a matrix! 

Finally, there is the keyword `end` that can be used when indexing into a matrix or vector. It refers to the last element in the row or column (e.g., x(end-2:end)).

## Polynomials

A polynomial expressions in Octave is represented by its coefficients in descending order. Consider the vector expression p:

`octave:31> p = [-2, -1, 0, 1, 2];`

The polynominal itself can be displayed by using the function output polyout, which displays the the polynominal in the variable specified (e.g., 'x'). The function polyval returns p(x), depending on the value assigned to x. If x is a vector or matrix, the polynomial is evaluated at each of the elements of x.

```
octave:31> polyout(p, 'x')
-2*x^4 - 1*x^3 + 0*x^2 + 1*x^1 + 2
octave:34> y=polyval(p, 5)
y = -1368
```

Polynominal multiplication is carried out by vector convolutions. This can be determined by r=conv(p,q). The two variables, p and q, are vectors containing the coefficients of two polynominals, and the result r contains the coefficients of their product.

```
octave:31> q = [1, 1];
octave:37> r = conv(p, q)
(snip)
```

Division is represented by deconvolving two vectors such that where [b, r] = deconv (y, a) solves for b and r such that y = conv (a, b) + r . If y and a are polynomial coefficient vectors, b will contain the  coefficients of the polynomial quotient and R will be a remainder
polynomial of lowest order.

Addition of polynomials in Octave has the issue that they are represented by vectors of their coefficients. As a result, addition of vectors of different lengths will fail. For example, for the polynominals  p(x) = x^2 - 1 and q(x) = x + 1, addition will fail. To work around this, you have to add some leading zeroes to q, which does not change the polynomial.

```
octave:38> p = [1, 0, -1];
octave:39> q = [1, 1];
octave:40> p + q
error: operator +: nonconformant arguments (op1 is 1x3, op2 is 1x2)
error: evaluating binary operator `+' near line 22, column 3
octave:41> q = [0, 1, 1];
octave:42> p + q
(snip)
octave:43> polyout(ans, 'x')
1*x^2 + 1*x^1 + 0
```

Other simple functions include: 

roots(p), which returns a vector of all the roots of the polynomial with coefficients in p. The derivatives function; q = polyderiv(p), returns the coefficients of the derivative of the polynominal whose coefficients are given by the vector p. 

q = polyint(p), which returns the coefficients of the integral of the polynomial whose coefficients are represented by the vector p. The constant of integration is set to 0.

p = polyfit(x, y, n), which returns the coefficients of a polynomial p(x) of degree n that best fits the data (x_i, y_i) in the least squares sense. 
		
### Linear Algebra and Eigenvalues

The simple arithematic, set theories, and polynominals explored so far serves as an introduction to more serious mathematics concerning vector spaces in linear algebra. Octave has a number of functions which aid this research which can be elaborated. For example;

`A = octave:44> A = [16 3 2 13; 5 10 11 8; 9 6 7 12; 4 15 14 1];`

The function det computes the determinant, the value associated with a square matrix. For example;

```octave:45> det(A)
ans =  1.0871e-12```

The function lambda = eig(A) returns the eigenvalues for A in the lector lambda, and
[V, lambda] = eig(A) returns the eigenvectors in V but lambda is a now matrix whose diagonals contain the eigenvalues.  This relationship holds true A = V*lambda*inv(V).

```
octave:46> lambda = eig(A)
(snip)
octave:47> [V, lambda] = eig(A)
(snip)
octave:48> A1 = V*lambda*inv(V)
(snip)
```

In linear algebra an n-by-n (square) matrix A is called invertible (nonsingular or nondegenerate) if there exists an n-by-n matrix B such that AB = BA = In  

Where In denotes the n-by-n identity matrix and the multiplication used is ordinary matrix multiplication. If this is the case, then the matrix B is uniquely determined by A and is called the inverse of A, denoted by A−1. 

A square matrix that is not invertible is called singular or degenerate. A square matrix is singular if and only if its determinant is 0. Octave will give an error if inversion is attemopted on a non-square matrix. Matrix inversion is the process of finding the matrix B that satisfies the prior equation for a given invertible matrix A.    

Note that in theory A*inv(A) should return the identity matrix, but in practice, there may be some round off errors so the result may not be exact.

```octave:49> inv(A)
(snip)```
  
In this example, rcond stands for reciprocal condition estimate. The rank of a matrix is a measure of the "nondegenerateness" of the system of linear equations and linear transformation encoded by that matrix. The command rank(A) will compute the rank of A using singular value decomposition. The rank is taken to be the number of singular values of A that are greater than the specified tolerance TOL.  If the second argument is omitted, it is taken to be tol = max (size (A)) * sigma(1) * eps, where eps is machine precision and sigma(1) is the largest singular value of A.

```octave:50> rank(A)
ans =  3```

The eigenvalues of A produce the following:

```octave:51> e=eig(A)
(snip)```

Note that calculating the inverse is often 'not' necessary. See the next two operators as examples. Note that in theory A*inv(A) should return the identity matrix, but in practice, there may be some round off errors so the result may not be exact.

The largest eigenvalue is 34, the vector of all ones is an eigenvector.

```octave:52> v = ones(4,1)
(snip)```

Unsurprisingly;

```octave:53> A*v
(snip)```
 
The length of a vector x = (x1, x2, ... xn) in the n-dimensional real vector space R^n is usually calculated in Euclidean distance. This is famously inappropriate for taxi drivers in Manhattan, who calculate distance according the orthogonal or parallel lines. The class of p-norms is calculated as follows:   

```octave:54> norm(A)
ans =  34.000```

The command norm(A, p) computes the p-norm of the matrix (or vector) A. The second argument is optional with default value of p=2; the command "help norm" will give a variety of other options.
  
There is a small mountain of other built-in functions that Octave has available for linear algebra. The following is a small subset, which can be accessed in some detail from Octave by "help command". 

| Command	| Function				|
|:--------------|:--------------------------------------|
| balance	| eigenvalue balancing			|
| cond		| condition number			|
| dmult		| computes diag(x) * A efficiently	|
| dot		| dot product				|
| givens	| Givens rotation			|
| expm(A)	| computes the matrix exponential of a square matrix	|
| kron		| Kronecker product			|
| krylov	| Orthogonal basis of block Krylov subspace	|
| housh		| Householder reflections		|
| logm(A)	| computes the matrix logarithm of a square matrix	|
| null		| orthonormal basis of the null space	|
| orth		| orthonormal basis of the range space	|
| pinv		| pseudoinverse				|
| svd		| singular value decomposition		|
| sqrtm(A)	| computes the matrix square root of a square matrix	|
| syl		| solves the Sylvester equation		|
| trace(A)	| computes the trace (sum of the diagonal elements) of A	|


## Functions

The simple structure of a function in Octave is simply a function declation, name, body, and end of function declaration. The name of the function follows the same rules as a variable. The body will define what the function actually does. Normally, this will require an argument message to be parsed to the function after the name which is invoked from the function. If information is wanted from the function, as it is from most cases, the ret-var (return variable) is added. Multiple return values take the form of a bracketed list. There are also special parameters for variable length input argments (varargin) and return lists (varargout). As with other programming languages it is often considered good practise to assign default values to some input arguments.

function [ret-list] = name(arg1= val1, arg2 = val2 ...)
	body
endfunction

The following example of a function returns two values, the maximum element of a vector and the index where it first occurs.

```
     function [max, idx] = vmax (v)
       idx = 1;
       max = v (idx);
       for i = 2:length (v)
         if (v (i) > max)
           max = v (i);
           idx = i;
         endif
       endfor
     endfunction
```

As with blocks in other languages, a return statement can exit the function and return to the main program. Values must be assigned to the list of the return variables that are part of the function. This example function checks to see if any elements of a vector are nonzero:

```
     function retval = any_nonzero (v)
       retval = 0;
       for i = 1:length (v)
         if (v (i) != 0)
           retval = 1;
           return;
         endif
       endfor
       printf ("no nonzero elements found\n");
     endfunction
```

Normally an Octave user will want to save the functions that they written for later use. Such files, with a .m suffix, can be simply included in an invoked path from the Octave interpreter. When a function is called, Octave searches the current working directory and the Ocatve installation directory for the function. The path command will display this directory listing. New paths can be included with the addpath() function, the genpath() function for directories and subdirectories, and rmpath() to remove paths.

```
octave:12> path 
Octave's search path contains the following directories: 
(snip)
octave:14> addpath("~/mathsprog/octave") 
octave:12> path 
(path)
```

A function file may include functions in its own right, as subfunctions. An alternative is a function that calls another function in the path, or private functions. The advantage of the latter is that it is accessible by any number of functions, whereas a a subfunction is contained within the main function. Such private functions often take the role of "helper functions" carrying out generic tasks. With such variation there also needs to be some precedence within functions – it is possible that multiple versions of a function may be defined within a particular scope. Precedence is then assigned to subfunctions, private functions, command-line functions, autoload functions, and finally built-in functions.

Functions can also have function handles, effectively a pointer to another function. The general syntax is simply; handle = @function. As a similar variation, functions can also be anonymous using the syntax; handle = @(argumentlist) expression. A function can also be created from a string with the inline function.

```
octave:1> f = @sin; 
octave:2> quad (f, 0, pi) 
ans =  2 
octave:13> f = inline("x^2 + 2"); 
octave:14> f(6) 
ans =  38 
```

Because Octave is a programming and scripting language it is possible to turn octave scripts into commands that can be invoked from the command line rather than using the interpreter. This is conducted in a very similar manner to the scripting commands for shell scripts or even PBS. This is very useful for batch processing of data files. An algorithm that has been tested successfully in an interactive Octave session can then be saved as a script and executed  independently (although, please don't do so on the login node).

Unlike a function file, a script must not begin with the function keyword – although it is possible to work around this by calling a statement that has no effect (e.g.. 1;). Further, the variable named within are not local, but are of the same scope of any other variable from the command line.

The first line of an Octave script, following the standard '#!' prefix, will to provide the path to the particular Octave binary.  This can vary according to which version of Octave one wishes to use e.g.,

`#! /usr/local/octave/3.6.3/bin/octave -qf`

The -qf is a standard option when launching Octave not to include any initialisation files and not to print start-up messages. The file can be executed either by modifying its permissions to make it executable or by invoking 'octave filename'. There is also the built-in function source(file).

It is useful to be able to save Octave commands and rerun them later on.  These should should be saved with a .m extension. To run an existing script in Octave, the path needs to be specified unless the environment is in the  same directory as the script file.  For example, if I have a script called myscript.m in an octave directory, the following two commands will execute the script.

``octave55>chdir('~/mathsprog/octave'); % This changes to the octave directory
octave56>myscript;``


## Global Variables, Conditions, and Loops

A variable may be declared and initialised as global, meaning that it can be accessed from within a function body without having to pass it as a formal parameter. It is, however, necessary declare a variable as global within a function body in order to access it.

```
global g
function f ()
  g = 1; # does NOT set the value of the global variable g to 1.
  global g = 1; # This will however
endfunction
f ()
```

As with other programming languages, Ocatve provides the faciility for instructions that conditional branching and loops. These include the if statement, the switch statement, the while statement, the do-until statement, the for statement, the break and continue statements.

The if statement statement takes the basic form of : if (condition) then-body endif. The if statement can have additional branching with else; if (condition) then-body else else-body endif, and even more branching with elseif. The following is a fairly simple example:

```
d100=fix(101*rand(1))
if (rem (d100, 2) == 0)
	printf ("d100 is even\n");
elseif (rem (d100, 3) == 0)
	printf ("d100 is odd and divisible by 3\n");
else
	printf ("d100 is odd\n");
endif
```

Elaborate if-elseif-else statement can however become unwieldly. As a result, Octave offers the switch statement as an alternative with the basic structure of switch(expression) case condition (body) case condition (body) case condition (body) … otherwise (body) endswitch. Note that, unlike in C for example, case statements in Octave are exclusive and command bodies are not optional.

```
d100=fix(101*rand(1))
switch d100
	case (rem (d100, 2) == 0)
		printf ("d100 is even\n");
	case (rem (d100, 3) == 0)
		printf ("d100 is odd and divisible by 3\n");
	otherwise
		printf ("d100 is odd\n");
endswitch			
```

The while statement is the simplest sort of loop. It repeats a statement as long as an initial condition remains true. The general structure is: while (condition) body endwhile. If the condition is true, the body is executed. Then the condition is tested again. The following example uses the while statement for the first ten elements of the Fibonacci sequence in the variable fib.

```
fib = ones (1, 10);
	i = 3;
while (i <= 10)
	fib (i) = fib (i-1) + fib (i-2);
	i++;
endwhile
fib
(snip)
```

A variation is the do-until statement with the main difference is the conditional test occurs after an  initial execution of the body. The general structure is: do body until (condition). The Fibonacci sequence is illustrated again:

```
fib = ones (1, 10);
i = 2;
do
	i++;
	fib (i) = fib (i-1) + fib (i-2);
until (i == 10)
fib
```

The basic structure of an Octave for loop is; for (var = expression) (body) endfor. The assignment expression assigns each column of the expression to var in turn. If expression is a range, a row vector, or a scalar, the value of var will be a scalar each time the loop body is executed. If var is a column vector or a matrix, var will be a column vector each time the loop body is executed.  Again, using the Fibonacci sequence:

```
fib = ones (1, 10);
for i = 3:10
	fib (i) = fib (i-1) + fib (i-2);
endfor
```

Within Octave is it also possible to iterate over matrices or cell arrays using the for statement. 

```
# Matrix loop
for i = [1,3;2,4]
	i
endfor
(snip)
# Cell array loop
for i = {1,"two";"three",4}
	 i
endfor
(snip)
```

Loops can be escaped with the break statement, which exits the innermost loop that encloses it. Naturally enough, it can only be used within the body of a loop. The following example finds the smallest divisor of a given integer, and identifies prime numbers. It uses a break statement to escape the first while statement when the remainder equals zero, proceeding immediately to the next statement following the loop.

```
num = 103;
div = 2;
while (div*div <= num)
  if (rem (num, div) == 0)
    break;
  endif
  div++;
endwhile
if (rem (num, div) == 0)
  printf ("Smallest divisor of %d is %d\n", num, div)
  else
  printf ("%d is prime\n", num);
endif
```

The continue statement is also used only inside loops. Where a condition is met, it skips over the rest of the loop body, causing the next cycle around the loop to begin immediately. In the following example, if one of the elements of vec is an odd number, this example skips the print statement for that element, and continues back to the first statement in the loop.

```
vec = round (rand (1, 10) * 100);
for x = vec
  if (rem (x, 2) != 0)
    continue;
  endif
    printf ("%d\n", x);
endfor
```

## Graphics

Octave provides plotting capability through GNUplot or OpenGL, with the latter being a newer addition. The function call graphics_toolkit ("fltk") selects the FLTK/OpenGL system, and graphics_toolkit ("gnuplot") selects the gnuplot system. For the following graphics examples the local machine should be used for testing purposes rather than the cluster.

The plot() function is the workhorse in Octave for plotting. A simple two-dimensional plot can be built by assigning values for the x and y axes, properties and values – all of which except for the y coordinates are optional. Log axes can be built using the loglog(), semilogx(), and semilogy() functions. The functions bar(), barh(), stair(), stem(), scatter() and others provide the ability to effectively display discrete data as a bar graph, a horizontal bar graph, a stairstep plot, a stem graph, a scatter plot etc.

Similarly, the axis() function may be used to change the axis limits of an existing plot, the aspect ratio, and colour, functional plots with fplot(), ezplot(), and ezpolar(), and various mesh() and plot3() functions for three-dimension plots. Walking through the followinge examples from the GNU Octave book illustrates these functions in action. Note that will all of these examples they can run on the cluster with the gnuplot module loaded, which does a fairly good job for a two-dimensional black-and-white, text-based display. 

```
x = -10:0.1:10;
plot (x, sin (x));
hist (randn (10000, 1), 30);
h = bar (rand (5, 10));
set (h(1), "basevalue", 0.5);
x = 1:10;
y = 2*x;
stem (x, y, "r");
theta = 0:0.2:6;
stem3 (cos (theta), sin (theta), theta)
fplot (@sin, [-10, 10], 201);
ezplot (@(x, y) x.^2 - y.^2 - 1)
f = @(x,y) sqrt (abs (x .* y)) ./ (1 + x.^2 + y.^2);
ezcontour (f, [-3, 3]);
ezpolar (@(t) 1 + sin (t));
tx = ty = linspace (-8, 8, 41)';
[xx, yy] = meshgrid (tx, ty);
r = sqrt (xx .^ 2 + yy .^ 2) + eps;
tz = sin (r) ./ r;
mesh (tx, ty, tz);
z = [0:0.05:5];
plot3 (cos (2*pi*z), sin (2*pi*z), z, ";helix;");
plot3 (z, exp (2i*pi*z), ";complex sinusoid;");
```

Finally, the print() function allows the computational side of Octave to run, but the graphics exported to a file. The examples of mandelbrot.m and sierpinski.m in the Octave directory should be reviewed, run, and the output file copied to a local directory for visualisation. 


# Octave and MATLAB(R)

Much of the syntax and behaviour of Octave is similar to MATLAB(R). The core principles - such as the use of matrices as a basic data type, support for complex numbers, extension via functions - are common to both. Nevertheless, whilst Octave is very similar to MATLAB(R) it is not quite the same.

To begin with, the GNU Octave parser is more advanced than that of MATLAB's. Octave supports single and double quotes, whereas MATLAB only supposrts single. Octave supports C-style autoincrement and assignment operators such as i++; ++i; i+=1, whereas MATLAB does not. Unlike Octave, MATLAB does not extend character strings of different lengths in a matrix, instead it will produce and error. Matlab doesn't support `printf` as a command for printing to the standard output. MATLAB always requires "..." for line continuation whereas Octave will support a carriage return or backslash. MATLAB always requires the ~= syntax to represent the logical operator NOT, whereas Octave will accept both ~= and !=, the latter more familiar from those from other programming languages. 

MATLAB will execute a startup.m in the directory it was called from; Octave does not, but it does execute a .octaverc - which can include a startup.m file. Octave's version of the nargin() function (number of function input arguments) behaves differently in terms of assignment, and MATLAB's product of array elements function, prod() is only supported for floating point input. MATLAB lets you load empty files, whereas does not.

This are just some of the examples of the differences; when transferring files between MATLAB and Octave it is important to be aware of all the differences and try to write in a neutral fashion. In a slightly cheeky manner however, Octave does give a lauching option for a higher level of compatibility with MATLAB.

--braindead
    For compatibility with matlab, set initial values for user preferences to the following values

              PS1                             = ">> "
              PS2                             = ""
              allow_noninteger_range_as_index = true
              beep_on_error                   = true
              confirm_recursive_rmdir         = false
              crash_dumps_octave_core         = false
              default_save_options            = "-mat-binary"
              do_braindead_shortcircuit_evaluation = true
              fixed_point_format              = true
              history_timestamp_format_string = "%%-- %D %I:%M %p --%%"
              page_screen_output              = false
              print_empty_dimensions          = false

    and disable the following warnings

              Octave:abbreviated-property-match
              Octave:fopen-file-in-path
              Octave:function-name-clash
              Octave:load-file-in-path


# Symbolic Computation with Maxima

## About Maxima and Installation

Maxima is a computer algebra system (CAS) originally based on Macsyma that is particularly useful for symbolic operations, but can also be used numerical operations. Macsyma's core design was established in 1968, and coding began in 1969. In 1982, the project was split with a commercial arm which continued in development until 1999. 

The academic version of MIT Macsyma remained available and was distributed by the US Department of Energy (DOE), and was maintained by Bill Schelter. Under the name of Maxima, it was released under GPL license in 1999, and now remains under active maintenance and development.

Maxima is written in Common Lisp and designed to run on all POSIX systems including Linux, Mac OSX, and also with ports for MS-Windows. Whilst written in Common Lisp it is also designed that it can be extended with the use of Lisp programs. It will have one of a number of versions of Lisp as a dependency.

Like many good things in life it is free software, released under the GNU Public License. For it's own part, Macsyma was developed at MIT with the earliest work being conducted in 1966. It's chief developer from the early 1980s, William Schelter, received permission from the US Department of Energy in 1998 to release a version under the GPL; that became Maxima. For plotting and display Maxima can make use of Gnuplot. The most popular graphical user interfaces for Maxima in wxMaxima, Jupyter, and GMaxima.

Maxima (and gnuplot etc) can be installed by package managers assuming they are in the local system's repositories, or by source. A preference is given to the latter for performance and optimisation and is commonly found in a High Performance Computer environment. The following is an example of how a systems administrator may conduct such an installation on such a system.

```
mkdir -p /usr/local/src/MAXIMA
cd /usr/local/src/MAXIMA
wget http://sourceforge.net/projects/maxima/files/Maxima-source/5.36.1-source/maxima-5.36.1.tar.gz
tar xvf maxima-5.36.1.tar.gz
cd maxima-5.36.1/
mkdir -p /usr/local/maxima/5.36.1
./configure --prefix=/usr/local/maxima/5.36.1
make
make check
make install
```

Following this an environment modules file should be created so that users can dynamically change paths and versions of an application as required. An appropriate directory path will be required.

```
mkdir /usr/local/Modules/modulefiles/maxima
cd /usr/local/Modules/modulefiles/maxima
```

The .base file sets the library, libexec, binary, and manual paths. Note that in this case sbcl (Steel Bank Common Lisp) is also loaded. 

```
#%Module1.0#####################################################################
##
## $name modulefile
##
set ver [lrange [split [ module-info name ] / ] 1 1 ]
set name [lrange [split [ module-info name ] / ] 0 0 ]
set loading [module-info mode load]
set desc [join [read [ open "/usr/local/Modules/modulefiles/$name/.desc" ] ] ]
module-whatis   "$desc (v$ver)"
if { $loading && ![ is-loaded sbcl ] } {
  module load sbcl
}
prepend-path LD_LIBRARY_PATH /usr/local/$name/$ver/lib
prepend-path PATH /usr/local/$name/$ver/libexec/$name/$ver
prepend-path PATH /usr/local/$name/$ver/bin
prepend-path MANPATH /usr/local/$name/$ver/share/man
```

The variables allow for a symlink to be created to the `.base` file e.g., ln -s .base 5.36.1`.

A .version file sets the default in the modules system:

```
#%Module1.0###########################################################
##
## version file for module
##
set ModulesVersion      "5.36.1"
```

Finally, a  brief description of the application in the .desc file which associates with the command `module whatis maxima`.

```
Maxima is a system for the manipulation of symbolic and numerical expressions, including differentiation, integration, Taylor series, Laplace transforms, ordinary differential equations, systems of linear equations, polynomials, and sets, lists, vectors, matrices, and tensors.
```

## Help, Editing, and Errors

Once installed Maxima can be invoked on the command line which will put the user in a lisp-based intrepretative shell. Commands are terminated with a semicolon with notation to differentiate between user input and program output. Help is not invoked with the `help` command but rather with `describe(topic)`, `example(topic)` or `? topic`, for each function. The command `apropos` will search flags and functions with a particular string. A demonstration of functions can be invoked by the `demonstrate (topic)` command. To quit an interactive session use the `quit()` function.

The following HPC session starts off by secure forwarding of X-Windows, then submission of a 12-hour interactive job, placing the user on to a compute node and not interrupting other users of the login (head) node, and loads the environment paths for the default version of Maxima and GNUplot, and then runs Maxima. 

Note that throughout this chapter examples will be shown on the basic Maxima command-line. There are numerous alternatives (xMaxima, Emacs plugins etc), and the command-line is probably the least friendly for editing. However the purpose of high performance computing is computation not ease. Whilst extensive Maxima scripts should certainly be written with a more complete editing environment in mind, familiarity interacting with the Maxima command-line is a worthwhile for serious work.

```
[lev@cricetomys matappprog]$ ssh edward -Y
[lev@edward ~]$ qsub -l nodes=1:ppn=2,walltime=12:00:00 -I -X
[lev@edward043 ~]$ module load maxima
[lev@edward043 ~]$ module load gnuplot
[lev@edward043 ~]$ maxima
Maxima 5.36.1 http://maxima.sourceforge.net
using Lisp SBCL 1.2.12
Distributed under the GNU Public License. See the file COPYING.
Dedicated to the memory of William Schelter.
The function bug_report() provides bug reporting information.
(%i1) help;
(%o1)      type `describe(topic);' or `example(topic);' or `? topic'
(%i2) describe (integrate);
 -- Function: integrate
          integrate (<expr>, <x>)
          integrate (<expr>, <x>, <a>, <b>)

     Attempts to symbolically compute the integral of <expr> with
     respect to <x>.  'integrate (<expr>, <x>)' is an indefinite
     integral, while 'integrate (<expr>, <x>, <a>, <b>)' is a definite
     integral, with limits of integration <a> and <b>.  The limits
     should not contain <x>, although 'integrate' does not enforce this
     restriction.  <a> need not be less than <b>.  If <b> is equal to
     <a>, 'integrate' returns zero.
..
..
(%i3) example(integrate);
(%i4) test(f):=block([u],u:integrate(f,x),ratsimp(f-diff(u,x)))
(%o4) test(f) := block([u], u : integrate(f, x), ratsimp(f - diff(u, x)))
(%i5) test(sin(x))
..
..
(%i21) quit();
```

There is a test suite which can be run. By default it does not show results, but this can be forced by a function parameter. This will, by the way, generate a lot of output. An alternative input terminator to the semicolon is the dollar sign ($), which suppresses the display. The following command is for a bug_report, which provides a URL for where to report bugs to, and the Maxima build information.

```
(%i1) run_testsuite(display_all = true);
..
..
..
98/98 tests passed (not counting 11 expected errors)
No unexpected errors found out of 10,185 tests.
Evaluation took:
  248.509 seconds of real time
  248.063289 seconds of total run time (243.318010 user, 4.745279 system)
  [ Run times consist of 9.774 seconds GC time, and 238.290 seconds non-GC time. ]
  99.82% CPU
  17,386 forms interpreted
  12,597 lambdas converted
  497,056,429,309 processor cycles
  35,729,959,168 bytes consed
  
(%o0)                                done
(%i1) bug_report();
Please report bugs to:
    http://sourceforge.net/p/maxima/bugs
To report a bug, you must have a Sourceforge account.
Please include the following information with your bug report:
-------------------------------------------------------------
Maxima version: "5.36.1"
Maxima build date: "2015-06-18 12:03:16"
Host type: "x86_64-unknown-linux-gnu"
Lisp implementation type: "SBCL"
Lisp implementation version: "1.2.12"
-------------------------------------------------------------
The above information is also reported by the function 'build_info()'.
(%o1) 
```

A computation can be aborting without exiting Maxima with ^C - which is very handy if a computation is taking too long due to an input error. To repeat a user input command, place two single quotes quotes before the input line number. To refer to the output result, either use the o label or a percent symbol. 


```
(%i1) run_testsuite(display_all = true);
..
..
^CEvaluation took:
  0.201 seconds of real time
  0.198970 seconds of total run time (0.131980 user, 0.066990 system)
  99.00% CPU
  9 lambdas converted
  400,866,776 processor cycles
  23,851,536 bytes consed
  before it was aborted by a non-local transfer of control.
(%i1) plot2d(x^2-x+3,[x,-10,10]);
(%o1)                  [/home/lev/maxout.gnuplot_pipes]
(%i2) ''%i1;
(%o2)                  [/home/lev/maxout.gnuplot_pipes]
(%i3) 13^13;
(%o3)                           302875106592253
(%i4) %o3;
(%o4)                           302875106592253
(%i4) quit();
```


## Simple Numeric and Symbolic Calculations

Whilst Maxima is primarily designed for symbolic computation it can also do numeric computations with arbitrary precision and size determined by the computers hardware. The usual operations can be conducted with `+` (addition), `\` (division), `*` (multiplication), `^` (exponent), and `!` (factorials). Maxima uses the standard order of operations, with primacy given to equations in parantheses. 

```
(%i1) 1+1+2*3;
(%o1)                                  8
(%i2) (1+1+2)*3;
(%o2)                                 12
(%i3) (1+1)*2^3;
(%o3)                                 16
```

Maxima also allows the user to refer to the latest result through the % character, or to any previous input or output by its respective prompted %i (input) or %o (output) value. 

```
(%i4) %^5;
(%o4)                               1048576
(%i5) %o1+%o2+%o3;
(%o5)                                 74
```

In order to assign a value to a variable, Maxima uses the colon (:), not the equal sign. The equal sign is used for representing equations.  Functions are assigned through ‘:=’. Plots of functions, like any other plot, assigns the variable, the function, and the minimum and maximum range.

```
(%i6) ses:7$ ok:8$ nau:9$
(%i9) sqrt(ses^2+ok^2+nau^2);
(%o9)                              sqrt(194)
(%i10) float(sqrt(ses^2+ok^2+nau^2));
(%o10)                         13.92838827718412
(%i11) f(x) := sqrt(x);
(%o11)                          f(x) := sqrt(x)
(%i12) f(4);
(%o12)                                 2
(%i13) f(25);
(%o13)                                 5
(%i14) plot2d(sqrt(x),[x,0,1000]);
(%o14)                 [/home/lev/maxout.gnuplot_pipes]
(%i15) plot3d(x^2-y^2,[x,-4,4],[y,-4,4],[grid,16,16]);
```

Maxima will tend to give symbolic results (i.e., results including fractions, square roots, unevaluated trigonometric, exponential, or logarithmic functions) rather than floating-point (or numerical) results. Use function float, as in the examples above, to get floating-point solutions.

The percentage (%) symbol represents the most recent result. The expand function 

```
(%i16) sin(20) + cos(20) + 1;float(%);
(%o16)                       sin(20) + cos(20) + 1
(%o17)                         2.32102731254102
(%i17)
```

The following are reserved words in Maxima and cannot be used as variable names;

```and at diff do else  elseif for from if in integrate limit next or product step sum then thru unless while```

Some common constants and functions in Maxima include the following: 

| Value			| Maxima Representation	|
|:----------------------|:----------------------|
| Natural log		| %e			|
| Square root of -1	| %i			|
| Pi 			| %pi			|
| Phi, the Golden Mean	| %phi			|
| Positive real infinity| %inf			|
| Negative real infinity| %minf			|
| Euler's constant	| %gamma		|
| Boolean values	| true, false		|
| Squart root		| sqrt			|
| tangent		| tan			|
| sine			| sin			|
| cosine		| cos			|
| exponential		| exp			|
| change to float value	| float			|
| absolute value	| abs			|


Maxima only offers the natural logarithm function log. log10 is not available by default but can be defined as a function:

```
(%i16) log10(x):= log(x)/log(10);
                                          log(x)
(%o16)                        log10(x) := -------
                                          log(10)

(%i17) log10(10);
(%o17)                                 1
(%i18) log10(1000);
                                   log(1000)
(%o18)                             ---------
                                    log(10)
(%i19) 
```




