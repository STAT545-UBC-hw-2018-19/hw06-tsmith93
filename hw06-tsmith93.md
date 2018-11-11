hw06-tsmith93
================
Thomas Smith
2018-11-05

------------------------------------------------------------------------

Outline
=======

1.  Load packages

2.  Character data

3.  Writing functions

------------------------------------------------------------------------

1. Load packages
----------------

First we will load the packages we will be using for the exercises

``` r
suppressPackageStartupMessages(library(tidyverse))
suppressPackageStartupMessages(library(stringr))
suppressPackageStartupMessages(library(stringi))
suppressPackageStartupMessages(library(testthat))
suppressPackageStartupMessages(library(knitr))
```

2. Character data
-----------------

For this section, we will be workign through the Strings exercises found [here](https://r4ds.had.co.nz/strings.html)

### String basics

1.  In code that doesn’t use stringr, you’ll often see paste() and paste0(). **(a)** What’s the difference between the two functions? **(b)** What stringr function are they equivalent to? **(c)** How do the functions differ in their handling of NA?

**(a)** Both paste() and paste0() and are used to concatenate a series of strings, but paste() sepearates strings with " ", whereas paste0() separates strings with "". In order to remove " " (space) between strings when using paste(), you must also include the sep element as sep = ""

Let's walk through this with an example.

Here we use paste() to combine "c" and "at":

``` r
paste("c", "at")
```

    ## [1] "c at"

That is not quite what we want. Though we can use the sep argument to remove the space:

``` r
#using "" in the sep argument removes a space when combining the two strings
paste("c", "at", sep = "")
```

    ## [1] "cat"

Ta da! Perfect!

Lets try with paste0() now!

``` r
paste0("c", "at")
```

    ## [1] "cat"

Look at that! Using the past0 function, there automatically is no space between the combiend strings. Saves us some time as we do not have to use the sep argument.

**(b)** The stringer function that is equivalent to paste0() is str\_c(), and the stringer function that is equivalent to paste() would be str\_c() with argument sep = " " included.

Here will will go through the answer with examples. Let's try using str\_c with the strings "c" and "at"

``` r
str_c("c", "at")
```

    ## [1] "cat"

No space! Just like paste0. Let's try adding a space with the sep argument:

``` r
#using " " in the sep argument
str_c("c", "at", sep = " ")
```

    ## [1] "c at"

Yay! It worked!

**(c)** Now we will include missing data as a string to see how this affects the functions we just went over.

First with paste:

``` r
paste("c", "at", NA)
```

    ## [1] "c at NA"

Look at that, it's included as NA

Next with paste0:

``` r
paste0("c", "at", NA)
```

    ## [1] "catNA"

Same as last, as expected.

Now let's try including missing data using str\_c():

``` r
str_c("c", "at", NA)
```

    ## [1] NA

This resulted in the combined string to read as NA! Maybe this is because NA was last? Let's try it first:

``` r
str_c(NA, "c", "at")
```

    ## [1] NA

Nope! It still combined as NA!

##### 2. In your own words, describe the difference between the sep and collapse arguments to str\_c()?

Within the str\_c function, you can include both the sep and collapse arguments. - sep seperates terms and should be specified with character strign format - collapse separates results and should be specified with character strign format

We will walk through the explained differences with an example.

First we will start with a simple paste() function:

``` r
str_c("this", "is", "file", "name")
```

    ## [1] "thisisfilename"

Next we will separate the strings with a "\_"

``` r
str_c("this", "is", "file", "name", sep = "_")
```

    ## [1] "this_is_file_name"

Now to better explain collapse, we will make a vector and add this to our str\_c():

``` r
#first make a vector 
x <- c("1", "2", "3")
str_c("this", "is", "file", "name", x, sep = "_")
```

    ## [1] "this_is_file_name_1" "this_is_file_name_2" "this_is_file_name_3"

Look what happens when we add the collapse argument:

``` r
x <- c("1", "2", "3")
str_c("this", "is", "file", "name", x, sep = "_", collapse = ", ")
```

    ## [1] "this_is_file_name_1, this_is_file_name_2, this_is_file_name_3"

1.  Use str\_length() and str\_sub() to extract the middle character from a string.

``` r
str_length("elephants")
```

    ## [1] 9

``` r
str_sub("elephants", 5, 5)
```

    ## [1] "h"

What will you do if the string has an even number of characters?

``` r
str_length("frog")
```

    ## [1] 4

``` r
str_sub("frog", 2, 3)
```

    ## [1] "ro"

Matching patterns with regular expressions
------------------------------------------

2. Write a function
-------------------

For the second part of my homework 6, I will be writing a function. As I am hoping to create a package that I can use with my thesis work looking at the relationship of stream discharge and smolt production, I will try to create a relevant function. An idea I have is to write function.

As most of the data I am using is coming the United States of America, the dishcarge unit is cubic feet per second, as opposed to cubic metres per second. Therefore, I am going to try and write a function to do the conversion for me.

**ft<sup>3</sup>/s -&gt; m<sup>3</sup>/s**

The complete formula goes as such:

**(957.5065 fl. oz./1 ft<sup>3</sup> ) X (1 L/33.814 fl. oz.) X (1 m<sup>3</sup> /1000L)**

Though a direct conversion is 1 ft<sup>3</sup> X 0.02831685 m<sup>3</sup>/1 ft

We will use this simplified conversion in the function we create.

``` r
#The input of 'ft2m' is temperature in Fahrenheit
ft2m <- function(ft) {
#F to C formula
  m <- ft*(0.02831685)

  #FtoC will return the temperature in Celsius
  return(m)
}
```

There! We have now saved the function `ft2m` to convert any ft<sup>3</sup>/s data to m<sup>3</sup>/s. Let's give this baby a test drive.

``` r
#Test the function by converting 78 cubic feet per second to cubic metres per second
ft2m(78)
```

    ## [1] 2.208714

Would you look at that! 78 ft<sup>3</sup>/s does indeed equate to 2.208714 m<sup>3</sup>/s. It looks like my *very first function* is working. But before I get too excited, I should probably use testthat to make sure!

``` r
test_that("Simple cases work", {
  expect_equal(ft2m(1), 0.02831685)
  expect_lt(ft2m(78), 3)
})
```

``` r
ft2m("three")
```

    ## Error in ft * (0.02831685): non-numeric argument to binary operator

``` r
ft2m <- function (ft) {
  if (!is.numeric(ft)) {
    stop(paste("ft must be numeric, your input was character",
               typeof(ft)))
  }
  m <- ft*(0.02831685)
}
```

``` r
ft2m("three")
```

    ## Error in ft2m("three"): ft must be numeric, your input was character character

``` r
discharge <- c(66.27845435, 53.69990518, 80.78557149, 64.10702956, 98.43554032, 72.51415782, 71.19987428, 89.39984214, 50.10705428)
discharge
```

    ## [1] 66.27845 53.69991 80.78557 64.10703 98.43554 72.51416 71.19987 89.39984
    ## [9] 50.10705

``` r
discharge_converted <- ft2m(discharge)
discharge_converted
```

    ## [1] 1.876797 1.520612 2.287593 1.815309 2.787384 2.053373 2.016156 2.531522
    ## [9] 1.418874

Look at that! I converted a vector of dicharge values in feet<sup>3</sup>/second to metres<sup>3</sup>/second.

Though as I will be importing my data as a dataframe, I wanted to practice adding a new collumn for the converted dicharge values.

``` r
ef_trask = read.csv("ef_trask.csv", header = TRUE)
ef_trask
```

    ##   year coho_spaw coho_smol chin_spaw chin_smol discharge
    ## 1 2006       152      2006        59    149661  66.27845
    ## 2 2007       181      3375       126    325791  53.69991
    ## 3 2008       205      2769         7      7293  80.78557
    ## 4 2009        71      1725        13     27896  64.10703
    ## 5 2010       281      4508        17     50414  98.43554
    ## 6 2011       245      4407        20     25020  72.51416
    ## 7 2012       304      4077        90     71947  71.19987
    ## 8 2013       572      5156        23     47670  89.39984
    ## 9 2014       196      5940        32     54120  50.10705

``` r
ef_trask$dishcharge_converted <- ft2m(ef_trask$discharge)
ef_trask %>% 
  kable(col.names = c("Year", "Coho spawners", "Coho smolts", "Chinook spawners", "Chinook smolts", "Cubic feet per second", "Cubic metres per second"))
```

|  Year|  Coho spawners|  Coho smolts|  Chinook spawners|  Chinook smolts|  Cubic feet per second|  Cubic metres per second|
|-----:|--------------:|------------:|-----------------:|---------------:|----------------------:|------------------------:|
|  2006|            152|         2006|                59|          149661|               66.27845|                 1.876797|
|  2007|            181|         3375|               126|          325791|               53.69991|                 1.520612|
|  2008|            205|         2769|                 7|            7293|               80.78557|                 2.287593|
|  2009|             71|         1725|                13|           27896|               64.10703|                 1.815309|
|  2010|            281|         4508|                17|           50414|               98.43554|                 2.787384|
|  2011|            245|         4407|                20|           25020|               72.51416|                 2.053373|
|  2012|            304|         4077|                90|           71947|               71.19987|                 2.016156|
|  2013|            572|         5156|                23|           47670|               89.39984|                 2.531522|
|  2014|            196|         5940|                32|           54120|               50.10705|                 1.418874|
