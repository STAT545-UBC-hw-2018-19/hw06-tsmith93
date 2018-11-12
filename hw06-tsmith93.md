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
#then create the string you want to attach to your vector values, using sep
str_c("this", "is", "file", "name", x, sep = "_")
```

    ## [1] "this_is_file_name_1" "this_is_file_name_2" "this_is_file_name_3"

Look what happens when we add the collapse argument:

``` r
x <- c("1", "2", "3")
#collapse will then combine together the newly created strings, separting by a comma
str_c("this", "is", "file", "name", x, sep = "_", collapse = ", ")
```

    ## [1] "this_is_file_name_1, this_is_file_name_2, this_is_file_name_3"

1.  Use str\_length() and str\_sub() to extract the middle character from a string.

``` r
str_length("elephants")
```

    ## [1] 9

``` r
#the latter two values dictate which characters in the string you want to retrieve
str_sub("elephants", 5, 5)
```

    ## [1] "h"

Lets try usign another word.

``` r
str_length("frog")
```

    ## [1] 4

Uh oh. What will you do if the string has an even number of characters

``` r
str_sub("frog", 2, 3)
```

    ## [1] "ro"

Wow, I sure feel like I have mastered a couple functions to create and investigate strings.

Matching patterns with regular expressions
------------------------------------------

As this seems to be something else foundational to workign with strings, I am goign to investigate these exercises as well. Specifically, I am going to focus on character classes and alternatives.

### Using `str_view_all()`

Create regular expressions to find all words that:

Start with a vowel.

``` r
#first call upon words
words %>% 
#the ^ symbol indiciates you are searching for words starting with specified characters. Within the square brackets what you are searching for, and match dictate whether results are what you searched or the opposite
  str_view_all("^[aeouiy]", match = TRUE)
```

<!--html_preserve-->

<script type="application/json" data-for="htmlwidget-6692f50635f64d8263c0">{"x":{"html":"<ul>\n  <li><span class='match'>a<\/span><\/li>\n  <li><span class='match'>a<\/span>ble<\/li>\n  <li><span class='match'>a<\/span>bout<\/li>\n  <li><span class='match'>a<\/span>bsolute<\/li>\n  <li><span class='match'>a<\/span>ccept<\/li>\n  <li><span class='match'>a<\/span>ccount<\/li>\n  <li><span class='match'>a<\/span>chieve<\/li>\n  <li><span class='match'>a<\/span>cross<\/li>\n  <li><span class='match'>a<\/span>ct<\/li>\n  <li><span class='match'>a<\/span>ctive<\/li>\n  <li><span class='match'>a<\/span>ctual<\/li>\n  <li><span class='match'>a<\/span>dd<\/li>\n  <li><span class='match'>a<\/span>ddress<\/li>\n  <li><span class='match'>a<\/span>dmit<\/li>\n  <li><span class='match'>a<\/span>dvertise<\/li>\n  <li><span class='match'>a<\/span>ffect<\/li>\n  <li><span class='match'>a<\/span>fford<\/li>\n  <li><span class='match'>a<\/span>fter<\/li>\n  <li><span class='match'>a<\/span>fternoon<\/li>\n  <li><span class='match'>a<\/span>gain<\/li>\n  <li><span class='match'>a<\/span>gainst<\/li>\n  <li><span class='match'>a<\/span>ge<\/li>\n  <li><span class='match'>a<\/span>gent<\/li>\n  <li><span class='match'>a<\/span>go<\/li>\n  <li><span class='match'>a<\/span>gree<\/li>\n  <li><span class='match'>a<\/span>ir<\/li>\n  <li><span class='match'>a<\/span>ll<\/li>\n  <li><span class='match'>a<\/span>llow<\/li>\n  <li><span class='match'>a<\/span>lmost<\/li>\n  <li><span class='match'>a<\/span>long<\/li>\n  <li><span class='match'>a<\/span>lready<\/li>\n  <li><span class='match'>a<\/span>lright<\/li>\n  <li><span class='match'>a<\/span>lso<\/li>\n  <li><span class='match'>a<\/span>lthough<\/li>\n  <li><span class='match'>a<\/span>lways<\/li>\n  <li><span class='match'>a<\/span>merica<\/li>\n  <li><span class='match'>a<\/span>mount<\/li>\n  <li><span class='match'>a<\/span>nd<\/li>\n  <li><span class='match'>a<\/span>nother<\/li>\n  <li><span class='match'>a<\/span>nswer<\/li>\n  <li><span class='match'>a<\/span>ny<\/li>\n  <li><span class='match'>a<\/span>part<\/li>\n  <li><span class='match'>a<\/span>pparent<\/li>\n  <li><span class='match'>a<\/span>ppear<\/li>\n  <li><span class='match'>a<\/span>pply<\/li>\n  <li><span class='match'>a<\/span>ppoint<\/li>\n  <li><span class='match'>a<\/span>pproach<\/li>\n  <li><span class='match'>a<\/span>ppropriate<\/li>\n  <li><span class='match'>a<\/span>rea<\/li>\n  <li><span class='match'>a<\/span>rgue<\/li>\n  <li><span class='match'>a<\/span>rm<\/li>\n  <li><span class='match'>a<\/span>round<\/li>\n  <li><span class='match'>a<\/span>rrange<\/li>\n  <li><span class='match'>a<\/span>rt<\/li>\n  <li><span class='match'>a<\/span>s<\/li>\n  <li><span class='match'>a<\/span>sk<\/li>\n  <li><span class='match'>a<\/span>ssociate<\/li>\n  <li><span class='match'>a<\/span>ssume<\/li>\n  <li><span class='match'>a<\/span>t<\/li>\n  <li><span class='match'>a<\/span>ttend<\/li>\n  <li><span class='match'>a<\/span>uthority<\/li>\n  <li><span class='match'>a<\/span>vailable<\/li>\n  <li><span class='match'>a<\/span>ware<\/li>\n  <li><span class='match'>a<\/span>way<\/li>\n  <li><span class='match'>a<\/span>wful<\/li>\n  <li><span class='match'>e<\/span>ach<\/li>\n  <li><span class='match'>e<\/span>arly<\/li>\n  <li><span class='match'>e<\/span>ast<\/li>\n  <li><span class='match'>e<\/span>asy<\/li>\n  <li><span class='match'>e<\/span>at<\/li>\n  <li><span class='match'>e<\/span>conomy<\/li>\n  <li><span class='match'>e<\/span>ducate<\/li>\n  <li><span class='match'>e<\/span>ffect<\/li>\n  <li><span class='match'>e<\/span>gg<\/li>\n  <li><span class='match'>e<\/span>ight<\/li>\n  <li><span class='match'>e<\/span>ither<\/li>\n  <li><span class='match'>e<\/span>lect<\/li>\n  <li><span class='match'>e<\/span>lectric<\/li>\n  <li><span class='match'>e<\/span>leven<\/li>\n  <li><span class='match'>e<\/span>lse<\/li>\n  <li><span class='match'>e<\/span>mploy<\/li>\n  <li><span class='match'>e<\/span>ncourage<\/li>\n  <li><span class='match'>e<\/span>nd<\/li>\n  <li><span class='match'>e<\/span>ngine<\/li>\n  <li><span class='match'>e<\/span>nglish<\/li>\n  <li><span class='match'>e<\/span>njoy<\/li>\n  <li><span class='match'>e<\/span>nough<\/li>\n  <li><span class='match'>e<\/span>nter<\/li>\n  <li><span class='match'>e<\/span>nvironment<\/li>\n  <li><span class='match'>e<\/span>qual<\/li>\n  <li><span class='match'>e<\/span>special<\/li>\n  <li><span class='match'>e<\/span>urope<\/li>\n  <li><span class='match'>e<\/span>ven<\/li>\n  <li><span class='match'>e<\/span>vening<\/li>\n  <li><span class='match'>e<\/span>ver<\/li>\n  <li><span class='match'>e<\/span>very<\/li>\n  <li><span class='match'>e<\/span>vidence<\/li>\n  <li><span class='match'>e<\/span>xact<\/li>\n  <li><span class='match'>e<\/span>xample<\/li>\n  <li><span class='match'>e<\/span>xcept<\/li>\n  <li><span class='match'>e<\/span>xcuse<\/li>\n  <li><span class='match'>e<\/span>xercise<\/li>\n  <li><span class='match'>e<\/span>xist<\/li>\n  <li><span class='match'>e<\/span>xpect<\/li>\n  <li><span class='match'>e<\/span>xpense<\/li>\n  <li><span class='match'>e<\/span>xperience<\/li>\n  <li><span class='match'>e<\/span>xplain<\/li>\n  <li><span class='match'>e<\/span>xpress<\/li>\n  <li><span class='match'>e<\/span>xtra<\/li>\n  <li><span class='match'>e<\/span>ye<\/li>\n  <li><span class='match'>i<\/span>dea<\/li>\n  <li><span class='match'>i<\/span>dentify<\/li>\n  <li><span class='match'>i<\/span>f<\/li>\n  <li><span class='match'>i<\/span>magine<\/li>\n  <li><span class='match'>i<\/span>mportant<\/li>\n  <li><span class='match'>i<\/span>mprove<\/li>\n  <li><span class='match'>i<\/span>n<\/li>\n  <li><span class='match'>i<\/span>nclude<\/li>\n  <li><span class='match'>i<\/span>ncome<\/li>\n  <li><span class='match'>i<\/span>ncrease<\/li>\n  <li><span class='match'>i<\/span>ndeed<\/li>\n  <li><span class='match'>i<\/span>ndividual<\/li>\n  <li><span class='match'>i<\/span>ndustry<\/li>\n  <li><span class='match'>i<\/span>nform<\/li>\n  <li><span class='match'>i<\/span>nside<\/li>\n  <li><span class='match'>i<\/span>nstead<\/li>\n  <li><span class='match'>i<\/span>nsure<\/li>\n  <li><span class='match'>i<\/span>nterest<\/li>\n  <li><span class='match'>i<\/span>nto<\/li>\n  <li><span class='match'>i<\/span>ntroduce<\/li>\n  <li><span class='match'>i<\/span>nvest<\/li>\n  <li><span class='match'>i<\/span>nvolve<\/li>\n  <li><span class='match'>i<\/span>ssue<\/li>\n  <li><span class='match'>i<\/span>t<\/li>\n  <li><span class='match'>i<\/span>tem<\/li>\n  <li><span class='match'>o<\/span>bvious<\/li>\n  <li><span class='match'>o<\/span>ccasion<\/li>\n  <li><span class='match'>o<\/span>dd<\/li>\n  <li><span class='match'>o<\/span>f<\/li>\n  <li><span class='match'>o<\/span>ff<\/li>\n  <li><span class='match'>o<\/span>ffer<\/li>\n  <li><span class='match'>o<\/span>ffice<\/li>\n  <li><span class='match'>o<\/span>ften<\/li>\n  <li><span class='match'>o<\/span>kay<\/li>\n  <li><span class='match'>o<\/span>ld<\/li>\n  <li><span class='match'>o<\/span>n<\/li>\n  <li><span class='match'>o<\/span>nce<\/li>\n  <li><span class='match'>o<\/span>ne<\/li>\n  <li><span class='match'>o<\/span>nly<\/li>\n  <li><span class='match'>o<\/span>pen<\/li>\n  <li><span class='match'>o<\/span>perate<\/li>\n  <li><span class='match'>o<\/span>pportunity<\/li>\n  <li><span class='match'>o<\/span>ppose<\/li>\n  <li><span class='match'>o<\/span>r<\/li>\n  <li><span class='match'>o<\/span>rder<\/li>\n  <li><span class='match'>o<\/span>rganize<\/li>\n  <li><span class='match'>o<\/span>riginal<\/li>\n  <li><span class='match'>o<\/span>ther<\/li>\n  <li><span class='match'>o<\/span>therwise<\/li>\n  <li><span class='match'>o<\/span>ught<\/li>\n  <li><span class='match'>o<\/span>ut<\/li>\n  <li><span class='match'>o<\/span>ver<\/li>\n  <li><span class='match'>o<\/span>wn<\/li>\n  <li><span class='match'>u<\/span>nder<\/li>\n  <li><span class='match'>u<\/span>nderstand<\/li>\n  <li><span class='match'>u<\/span>nion<\/li>\n  <li><span class='match'>u<\/span>nit<\/li>\n  <li><span class='match'>u<\/span>nite<\/li>\n  <li><span class='match'>u<\/span>niversity<\/li>\n  <li><span class='match'>u<\/span>nless<\/li>\n  <li><span class='match'>u<\/span>ntil<\/li>\n  <li><span class='match'>u<\/span>p<\/li>\n  <li><span class='match'>u<\/span>pon<\/li>\n  <li><span class='match'>u<\/span>se<\/li>\n  <li><span class='match'>u<\/span>sual<\/li>\n  <li><span class='match'>y<\/span>ear<\/li>\n  <li><span class='match'>y<\/span>es<\/li>\n  <li><span class='match'>y<\/span>esterday<\/li>\n  <li><span class='match'>y<\/span>et<\/li>\n  <li><span class='match'>y<\/span>ou<\/li>\n  <li><span class='match'>y<\/span>oung<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script>
<!--/html_preserve-->
All those words sure start with a vowel. Success!

That only contain consonants.

``` r
words %>% 
#by placing ^ infront of the letters within the square brackets, you are stating you want words not starting with specified letters.
  str_view_all("^[^aeouiy]", match = TRUE)
```

<!--html_preserve-->

<script type="application/json" data-for="htmlwidget-79d50aeb5eee5b8c2bcc">{"x":{"html":"<ul>\n  <li><span class='match'>b<\/span>aby<\/li>\n  <li><span class='match'>b<\/span>ack<\/li>\n  <li><span class='match'>b<\/span>ad<\/li>\n  <li><span class='match'>b<\/span>ag<\/li>\n  <li><span class='match'>b<\/span>alance<\/li>\n  <li><span class='match'>b<\/span>all<\/li>\n  <li><span class='match'>b<\/span>ank<\/li>\n  <li><span class='match'>b<\/span>ar<\/li>\n  <li><span class='match'>b<\/span>ase<\/li>\n  <li><span class='match'>b<\/span>asis<\/li>\n  <li><span class='match'>b<\/span>e<\/li>\n  <li><span class='match'>b<\/span>ear<\/li>\n  <li><span class='match'>b<\/span>eat<\/li>\n  <li><span class='match'>b<\/span>eauty<\/li>\n  <li><span class='match'>b<\/span>ecause<\/li>\n  <li><span class='match'>b<\/span>ecome<\/li>\n  <li><span class='match'>b<\/span>ed<\/li>\n  <li><span class='match'>b<\/span>efore<\/li>\n  <li><span class='match'>b<\/span>egin<\/li>\n  <li><span class='match'>b<\/span>ehind<\/li>\n  <li><span class='match'>b<\/span>elieve<\/li>\n  <li><span class='match'>b<\/span>enefit<\/li>\n  <li><span class='match'>b<\/span>est<\/li>\n  <li><span class='match'>b<\/span>et<\/li>\n  <li><span class='match'>b<\/span>etween<\/li>\n  <li><span class='match'>b<\/span>ig<\/li>\n  <li><span class='match'>b<\/span>ill<\/li>\n  <li><span class='match'>b<\/span>irth<\/li>\n  <li><span class='match'>b<\/span>it<\/li>\n  <li><span class='match'>b<\/span>lack<\/li>\n  <li><span class='match'>b<\/span>loke<\/li>\n  <li><span class='match'>b<\/span>lood<\/li>\n  <li><span class='match'>b<\/span>low<\/li>\n  <li><span class='match'>b<\/span>lue<\/li>\n  <li><span class='match'>b<\/span>oard<\/li>\n  <li><span class='match'>b<\/span>oat<\/li>\n  <li><span class='match'>b<\/span>ody<\/li>\n  <li><span class='match'>b<\/span>ook<\/li>\n  <li><span class='match'>b<\/span>oth<\/li>\n  <li><span class='match'>b<\/span>other<\/li>\n  <li><span class='match'>b<\/span>ottle<\/li>\n  <li><span class='match'>b<\/span>ottom<\/li>\n  <li><span class='match'>b<\/span>ox<\/li>\n  <li><span class='match'>b<\/span>oy<\/li>\n  <li><span class='match'>b<\/span>reak<\/li>\n  <li><span class='match'>b<\/span>rief<\/li>\n  <li><span class='match'>b<\/span>rilliant<\/li>\n  <li><span class='match'>b<\/span>ring<\/li>\n  <li><span class='match'>b<\/span>ritain<\/li>\n  <li><span class='match'>b<\/span>rother<\/li>\n  <li><span class='match'>b<\/span>udget<\/li>\n  <li><span class='match'>b<\/span>uild<\/li>\n  <li><span class='match'>b<\/span>us<\/li>\n  <li><span class='match'>b<\/span>usiness<\/li>\n  <li><span class='match'>b<\/span>usy<\/li>\n  <li><span class='match'>b<\/span>ut<\/li>\n  <li><span class='match'>b<\/span>uy<\/li>\n  <li><span class='match'>b<\/span>y<\/li>\n  <li><span class='match'>c<\/span>ake<\/li>\n  <li><span class='match'>c<\/span>all<\/li>\n  <li><span class='match'>c<\/span>an<\/li>\n  <li><span class='match'>c<\/span>ar<\/li>\n  <li><span class='match'>c<\/span>ard<\/li>\n  <li><span class='match'>c<\/span>are<\/li>\n  <li><span class='match'>c<\/span>arry<\/li>\n  <li><span class='match'>c<\/span>ase<\/li>\n  <li><span class='match'>c<\/span>at<\/li>\n  <li><span class='match'>c<\/span>atch<\/li>\n  <li><span class='match'>c<\/span>ause<\/li>\n  <li><span class='match'>c<\/span>ent<\/li>\n  <li><span class='match'>c<\/span>entre<\/li>\n  <li><span class='match'>c<\/span>ertain<\/li>\n  <li><span class='match'>c<\/span>hair<\/li>\n  <li><span class='match'>c<\/span>hairman<\/li>\n  <li><span class='match'>c<\/span>hance<\/li>\n  <li><span class='match'>c<\/span>hange<\/li>\n  <li><span class='match'>c<\/span>hap<\/li>\n  <li><span class='match'>c<\/span>haracter<\/li>\n  <li><span class='match'>c<\/span>harge<\/li>\n  <li><span class='match'>c<\/span>heap<\/li>\n  <li><span class='match'>c<\/span>heck<\/li>\n  <li><span class='match'>c<\/span>hild<\/li>\n  <li><span class='match'>c<\/span>hoice<\/li>\n  <li><span class='match'>c<\/span>hoose<\/li>\n  <li><span class='match'>C<\/span>hrist<\/li>\n  <li><span class='match'>C<\/span>hristmas<\/li>\n  <li><span class='match'>c<\/span>hurch<\/li>\n  <li><span class='match'>c<\/span>ity<\/li>\n  <li><span class='match'>c<\/span>laim<\/li>\n  <li><span class='match'>c<\/span>lass<\/li>\n  <li><span class='match'>c<\/span>lean<\/li>\n  <li><span class='match'>c<\/span>lear<\/li>\n  <li><span class='match'>c<\/span>lient<\/li>\n  <li><span class='match'>c<\/span>lock<\/li>\n  <li><span class='match'>c<\/span>lose<\/li>\n  <li><span class='match'>c<\/span>loses<\/li>\n  <li><span class='match'>c<\/span>lothe<\/li>\n  <li><span class='match'>c<\/span>lub<\/li>\n  <li><span class='match'>c<\/span>offee<\/li>\n  <li><span class='match'>c<\/span>old<\/li>\n  <li><span class='match'>c<\/span>olleague<\/li>\n  <li><span class='match'>c<\/span>ollect<\/li>\n  <li><span class='match'>c<\/span>ollege<\/li>\n  <li><span class='match'>c<\/span>olour<\/li>\n  <li><span class='match'>c<\/span>ome<\/li>\n  <li><span class='match'>c<\/span>omment<\/li>\n  <li><span class='match'>c<\/span>ommit<\/li>\n  <li><span class='match'>c<\/span>ommittee<\/li>\n  <li><span class='match'>c<\/span>ommon<\/li>\n  <li><span class='match'>c<\/span>ommunity<\/li>\n  <li><span class='match'>c<\/span>ompany<\/li>\n  <li><span class='match'>c<\/span>ompare<\/li>\n  <li><span class='match'>c<\/span>omplete<\/li>\n  <li><span class='match'>c<\/span>ompute<\/li>\n  <li><span class='match'>c<\/span>oncern<\/li>\n  <li><span class='match'>c<\/span>ondition<\/li>\n  <li><span class='match'>c<\/span>onfer<\/li>\n  <li><span class='match'>c<\/span>onsider<\/li>\n  <li><span class='match'>c<\/span>onsult<\/li>\n  <li><span class='match'>c<\/span>ontact<\/li>\n  <li><span class='match'>c<\/span>ontinue<\/li>\n  <li><span class='match'>c<\/span>ontract<\/li>\n  <li><span class='match'>c<\/span>ontrol<\/li>\n  <li><span class='match'>c<\/span>onverse<\/li>\n  <li><span class='match'>c<\/span>ook<\/li>\n  <li><span class='match'>c<\/span>opy<\/li>\n  <li><span class='match'>c<\/span>orner<\/li>\n  <li><span class='match'>c<\/span>orrect<\/li>\n  <li><span class='match'>c<\/span>ost<\/li>\n  <li><span class='match'>c<\/span>ould<\/li>\n  <li><span class='match'>c<\/span>ouncil<\/li>\n  <li><span class='match'>c<\/span>ount<\/li>\n  <li><span class='match'>c<\/span>ountry<\/li>\n  <li><span class='match'>c<\/span>ounty<\/li>\n  <li><span class='match'>c<\/span>ouple<\/li>\n  <li><span class='match'>c<\/span>ourse<\/li>\n  <li><span class='match'>c<\/span>ourt<\/li>\n  <li><span class='match'>c<\/span>over<\/li>\n  <li><span class='match'>c<\/span>reate<\/li>\n  <li><span class='match'>c<\/span>ross<\/li>\n  <li><span class='match'>c<\/span>up<\/li>\n  <li><span class='match'>c<\/span>urrent<\/li>\n  <li><span class='match'>c<\/span>ut<\/li>\n  <li><span class='match'>d<\/span>ad<\/li>\n  <li><span class='match'>d<\/span>anger<\/li>\n  <li><span class='match'>d<\/span>ate<\/li>\n  <li><span class='match'>d<\/span>ay<\/li>\n  <li><span class='match'>d<\/span>ead<\/li>\n  <li><span class='match'>d<\/span>eal<\/li>\n  <li><span class='match'>d<\/span>ear<\/li>\n  <li><span class='match'>d<\/span>ebate<\/li>\n  <li><span class='match'>d<\/span>ecide<\/li>\n  <li><span class='match'>d<\/span>ecision<\/li>\n  <li><span class='match'>d<\/span>eep<\/li>\n  <li><span class='match'>d<\/span>efinite<\/li>\n  <li><span class='match'>d<\/span>egree<\/li>\n  <li><span class='match'>d<\/span>epartment<\/li>\n  <li><span class='match'>d<\/span>epend<\/li>\n  <li><span class='match'>d<\/span>escribe<\/li>\n  <li><span class='match'>d<\/span>esign<\/li>\n  <li><span class='match'>d<\/span>etail<\/li>\n  <li><span class='match'>d<\/span>evelop<\/li>\n  <li><span class='match'>d<\/span>ie<\/li>\n  <li><span class='match'>d<\/span>ifference<\/li>\n  <li><span class='match'>d<\/span>ifficult<\/li>\n  <li><span class='match'>d<\/span>inner<\/li>\n  <li><span class='match'>d<\/span>irect<\/li>\n  <li><span class='match'>d<\/span>iscuss<\/li>\n  <li><span class='match'>d<\/span>istrict<\/li>\n  <li><span class='match'>d<\/span>ivide<\/li>\n  <li><span class='match'>d<\/span>o<\/li>\n  <li><span class='match'>d<\/span>octor<\/li>\n  <li><span class='match'>d<\/span>ocument<\/li>\n  <li><span class='match'>d<\/span>og<\/li>\n  <li><span class='match'>d<\/span>oor<\/li>\n  <li><span class='match'>d<\/span>ouble<\/li>\n  <li><span class='match'>d<\/span>oubt<\/li>\n  <li><span class='match'>d<\/span>own<\/li>\n  <li><span class='match'>d<\/span>raw<\/li>\n  <li><span class='match'>d<\/span>ress<\/li>\n  <li><span class='match'>d<\/span>rink<\/li>\n  <li><span class='match'>d<\/span>rive<\/li>\n  <li><span class='match'>d<\/span>rop<\/li>\n  <li><span class='match'>d<\/span>ry<\/li>\n  <li><span class='match'>d<\/span>ue<\/li>\n  <li><span class='match'>d<\/span>uring<\/li>\n  <li><span class='match'>f<\/span>ace<\/li>\n  <li><span class='match'>f<\/span>act<\/li>\n  <li><span class='match'>f<\/span>air<\/li>\n  <li><span class='match'>f<\/span>all<\/li>\n  <li><span class='match'>f<\/span>amily<\/li>\n  <li><span class='match'>f<\/span>ar<\/li>\n  <li><span class='match'>f<\/span>arm<\/li>\n  <li><span class='match'>f<\/span>ast<\/li>\n  <li><span class='match'>f<\/span>ather<\/li>\n  <li><span class='match'>f<\/span>avour<\/li>\n  <li><span class='match'>f<\/span>eed<\/li>\n  <li><span class='match'>f<\/span>eel<\/li>\n  <li><span class='match'>f<\/span>ew<\/li>\n  <li><span class='match'>f<\/span>ield<\/li>\n  <li><span class='match'>f<\/span>ight<\/li>\n  <li><span class='match'>f<\/span>igure<\/li>\n  <li><span class='match'>f<\/span>ile<\/li>\n  <li><span class='match'>f<\/span>ill<\/li>\n  <li><span class='match'>f<\/span>ilm<\/li>\n  <li><span class='match'>f<\/span>inal<\/li>\n  <li><span class='match'>f<\/span>inance<\/li>\n  <li><span class='match'>f<\/span>ind<\/li>\n  <li><span class='match'>f<\/span>ine<\/li>\n  <li><span class='match'>f<\/span>inish<\/li>\n  <li><span class='match'>f<\/span>ire<\/li>\n  <li><span class='match'>f<\/span>irst<\/li>\n  <li><span class='match'>f<\/span>ish<\/li>\n  <li><span class='match'>f<\/span>it<\/li>\n  <li><span class='match'>f<\/span>ive<\/li>\n  <li><span class='match'>f<\/span>lat<\/li>\n  <li><span class='match'>f<\/span>loor<\/li>\n  <li><span class='match'>f<\/span>ly<\/li>\n  <li><span class='match'>f<\/span>ollow<\/li>\n  <li><span class='match'>f<\/span>ood<\/li>\n  <li><span class='match'>f<\/span>oot<\/li>\n  <li><span class='match'>f<\/span>or<\/li>\n  <li><span class='match'>f<\/span>orce<\/li>\n  <li><span class='match'>f<\/span>orget<\/li>\n  <li><span class='match'>f<\/span>orm<\/li>\n  <li><span class='match'>f<\/span>ortune<\/li>\n  <li><span class='match'>f<\/span>orward<\/li>\n  <li><span class='match'>f<\/span>our<\/li>\n  <li><span class='match'>f<\/span>rance<\/li>\n  <li><span class='match'>f<\/span>ree<\/li>\n  <li><span class='match'>f<\/span>riday<\/li>\n  <li><span class='match'>f<\/span>riend<\/li>\n  <li><span class='match'>f<\/span>rom<\/li>\n  <li><span class='match'>f<\/span>ront<\/li>\n  <li><span class='match'>f<\/span>ull<\/li>\n  <li><span class='match'>f<\/span>un<\/li>\n  <li><span class='match'>f<\/span>unction<\/li>\n  <li><span class='match'>f<\/span>und<\/li>\n  <li><span class='match'>f<\/span>urther<\/li>\n  <li><span class='match'>f<\/span>uture<\/li>\n  <li><span class='match'>g<\/span>ame<\/li>\n  <li><span class='match'>g<\/span>arden<\/li>\n  <li><span class='match'>g<\/span>as<\/li>\n  <li><span class='match'>g<\/span>eneral<\/li>\n  <li><span class='match'>g<\/span>ermany<\/li>\n  <li><span class='match'>g<\/span>et<\/li>\n  <li><span class='match'>g<\/span>irl<\/li>\n  <li><span class='match'>g<\/span>ive<\/li>\n  <li><span class='match'>g<\/span>lass<\/li>\n  <li><span class='match'>g<\/span>o<\/li>\n  <li><span class='match'>g<\/span>od<\/li>\n  <li><span class='match'>g<\/span>ood<\/li>\n  <li><span class='match'>g<\/span>oodbye<\/li>\n  <li><span class='match'>g<\/span>overn<\/li>\n  <li><span class='match'>g<\/span>rand<\/li>\n  <li><span class='match'>g<\/span>rant<\/li>\n  <li><span class='match'>g<\/span>reat<\/li>\n  <li><span class='match'>g<\/span>reen<\/li>\n  <li><span class='match'>g<\/span>round<\/li>\n  <li><span class='match'>g<\/span>roup<\/li>\n  <li><span class='match'>g<\/span>row<\/li>\n  <li><span class='match'>g<\/span>uess<\/li>\n  <li><span class='match'>g<\/span>uy<\/li>\n  <li><span class='match'>h<\/span>air<\/li>\n  <li><span class='match'>h<\/span>alf<\/li>\n  <li><span class='match'>h<\/span>all<\/li>\n  <li><span class='match'>h<\/span>and<\/li>\n  <li><span class='match'>h<\/span>ang<\/li>\n  <li><span class='match'>h<\/span>appen<\/li>\n  <li><span class='match'>h<\/span>appy<\/li>\n  <li><span class='match'>h<\/span>ard<\/li>\n  <li><span class='match'>h<\/span>ate<\/li>\n  <li><span class='match'>h<\/span>ave<\/li>\n  <li><span class='match'>h<\/span>e<\/li>\n  <li><span class='match'>h<\/span>ead<\/li>\n  <li><span class='match'>h<\/span>ealth<\/li>\n  <li><span class='match'>h<\/span>ear<\/li>\n  <li><span class='match'>h<\/span>eart<\/li>\n  <li><span class='match'>h<\/span>eat<\/li>\n  <li><span class='match'>h<\/span>eavy<\/li>\n  <li><span class='match'>h<\/span>ell<\/li>\n  <li><span class='match'>h<\/span>elp<\/li>\n  <li><span class='match'>h<\/span>ere<\/li>\n  <li><span class='match'>h<\/span>igh<\/li>\n  <li><span class='match'>h<\/span>istory<\/li>\n  <li><span class='match'>h<\/span>it<\/li>\n  <li><span class='match'>h<\/span>old<\/li>\n  <li><span class='match'>h<\/span>oliday<\/li>\n  <li><span class='match'>h<\/span>ome<\/li>\n  <li><span class='match'>h<\/span>onest<\/li>\n  <li><span class='match'>h<\/span>ope<\/li>\n  <li><span class='match'>h<\/span>orse<\/li>\n  <li><span class='match'>h<\/span>ospital<\/li>\n  <li><span class='match'>h<\/span>ot<\/li>\n  <li><span class='match'>h<\/span>our<\/li>\n  <li><span class='match'>h<\/span>ouse<\/li>\n  <li><span class='match'>h<\/span>ow<\/li>\n  <li><span class='match'>h<\/span>owever<\/li>\n  <li><span class='match'>h<\/span>ullo<\/li>\n  <li><span class='match'>h<\/span>undred<\/li>\n  <li><span class='match'>h<\/span>usband<\/li>\n  <li><span class='match'>j<\/span>esus<\/li>\n  <li><span class='match'>j<\/span>ob<\/li>\n  <li><span class='match'>j<\/span>oin<\/li>\n  <li><span class='match'>j<\/span>udge<\/li>\n  <li><span class='match'>j<\/span>ump<\/li>\n  <li><span class='match'>j<\/span>ust<\/li>\n  <li><span class='match'>k<\/span>eep<\/li>\n  <li><span class='match'>k<\/span>ey<\/li>\n  <li><span class='match'>k<\/span>id<\/li>\n  <li><span class='match'>k<\/span>ill<\/li>\n  <li><span class='match'>k<\/span>ind<\/li>\n  <li><span class='match'>k<\/span>ing<\/li>\n  <li><span class='match'>k<\/span>itchen<\/li>\n  <li><span class='match'>k<\/span>nock<\/li>\n  <li><span class='match'>k<\/span>now<\/li>\n  <li><span class='match'>l<\/span>abour<\/li>\n  <li><span class='match'>l<\/span>ad<\/li>\n  <li><span class='match'>l<\/span>ady<\/li>\n  <li><span class='match'>l<\/span>and<\/li>\n  <li><span class='match'>l<\/span>anguage<\/li>\n  <li><span class='match'>l<\/span>arge<\/li>\n  <li><span class='match'>l<\/span>ast<\/li>\n  <li><span class='match'>l<\/span>ate<\/li>\n  <li><span class='match'>l<\/span>augh<\/li>\n  <li><span class='match'>l<\/span>aw<\/li>\n  <li><span class='match'>l<\/span>ay<\/li>\n  <li><span class='match'>l<\/span>ead<\/li>\n  <li><span class='match'>l<\/span>earn<\/li>\n  <li><span class='match'>l<\/span>eave<\/li>\n  <li><span class='match'>l<\/span>eft<\/li>\n  <li><span class='match'>l<\/span>eg<\/li>\n  <li><span class='match'>l<\/span>ess<\/li>\n  <li><span class='match'>l<\/span>et<\/li>\n  <li><span class='match'>l<\/span>etter<\/li>\n  <li><span class='match'>l<\/span>evel<\/li>\n  <li><span class='match'>l<\/span>ie<\/li>\n  <li><span class='match'>l<\/span>ife<\/li>\n  <li><span class='match'>l<\/span>ight<\/li>\n  <li><span class='match'>l<\/span>ike<\/li>\n  <li><span class='match'>l<\/span>ikely<\/li>\n  <li><span class='match'>l<\/span>imit<\/li>\n  <li><span class='match'>l<\/span>ine<\/li>\n  <li><span class='match'>l<\/span>ink<\/li>\n  <li><span class='match'>l<\/span>ist<\/li>\n  <li><span class='match'>l<\/span>isten<\/li>\n  <li><span class='match'>l<\/span>ittle<\/li>\n  <li><span class='match'>l<\/span>ive<\/li>\n  <li><span class='match'>l<\/span>oad<\/li>\n  <li><span class='match'>l<\/span>ocal<\/li>\n  <li><span class='match'>l<\/span>ock<\/li>\n  <li><span class='match'>l<\/span>ondon<\/li>\n  <li><span class='match'>l<\/span>ong<\/li>\n  <li><span class='match'>l<\/span>ook<\/li>\n  <li><span class='match'>l<\/span>ord<\/li>\n  <li><span class='match'>l<\/span>ose<\/li>\n  <li><span class='match'>l<\/span>ot<\/li>\n  <li><span class='match'>l<\/span>ove<\/li>\n  <li><span class='match'>l<\/span>ow<\/li>\n  <li><span class='match'>l<\/span>uck<\/li>\n  <li><span class='match'>l<\/span>unch<\/li>\n  <li><span class='match'>m<\/span>achine<\/li>\n  <li><span class='match'>m<\/span>ain<\/li>\n  <li><span class='match'>m<\/span>ajor<\/li>\n  <li><span class='match'>m<\/span>ake<\/li>\n  <li><span class='match'>m<\/span>an<\/li>\n  <li><span class='match'>m<\/span>anage<\/li>\n  <li><span class='match'>m<\/span>any<\/li>\n  <li><span class='match'>m<\/span>ark<\/li>\n  <li><span class='match'>m<\/span>arket<\/li>\n  <li><span class='match'>m<\/span>arry<\/li>\n  <li><span class='match'>m<\/span>atch<\/li>\n  <li><span class='match'>m<\/span>atter<\/li>\n  <li><span class='match'>m<\/span>ay<\/li>\n  <li><span class='match'>m<\/span>aybe<\/li>\n  <li><span class='match'>m<\/span>ean<\/li>\n  <li><span class='match'>m<\/span>eaning<\/li>\n  <li><span class='match'>m<\/span>easure<\/li>\n  <li><span class='match'>m<\/span>eet<\/li>\n  <li><span class='match'>m<\/span>ember<\/li>\n  <li><span class='match'>m<\/span>ention<\/li>\n  <li><span class='match'>m<\/span>iddle<\/li>\n  <li><span class='match'>m<\/span>ight<\/li>\n  <li><span class='match'>m<\/span>ile<\/li>\n  <li><span class='match'>m<\/span>ilk<\/li>\n  <li><span class='match'>m<\/span>illion<\/li>\n  <li><span class='match'>m<\/span>ind<\/li>\n  <li><span class='match'>m<\/span>inister<\/li>\n  <li><span class='match'>m<\/span>inus<\/li>\n  <li><span class='match'>m<\/span>inute<\/li>\n  <li><span class='match'>m<\/span>iss<\/li>\n  <li><span class='match'>m<\/span>ister<\/li>\n  <li><span class='match'>m<\/span>oment<\/li>\n  <li><span class='match'>m<\/span>onday<\/li>\n  <li><span class='match'>m<\/span>oney<\/li>\n  <li><span class='match'>m<\/span>onth<\/li>\n  <li><span class='match'>m<\/span>ore<\/li>\n  <li><span class='match'>m<\/span>orning<\/li>\n  <li><span class='match'>m<\/span>ost<\/li>\n  <li><span class='match'>m<\/span>other<\/li>\n  <li><span class='match'>m<\/span>otion<\/li>\n  <li><span class='match'>m<\/span>ove<\/li>\n  <li><span class='match'>m<\/span>rs<\/li>\n  <li><span class='match'>m<\/span>uch<\/li>\n  <li><span class='match'>m<\/span>usic<\/li>\n  <li><span class='match'>m<\/span>ust<\/li>\n  <li><span class='match'>n<\/span>ame<\/li>\n  <li><span class='match'>n<\/span>ation<\/li>\n  <li><span class='match'>n<\/span>ature<\/li>\n  <li><span class='match'>n<\/span>ear<\/li>\n  <li><span class='match'>n<\/span>ecessary<\/li>\n  <li><span class='match'>n<\/span>eed<\/li>\n  <li><span class='match'>n<\/span>ever<\/li>\n  <li><span class='match'>n<\/span>ew<\/li>\n  <li><span class='match'>n<\/span>ews<\/li>\n  <li><span class='match'>n<\/span>ext<\/li>\n  <li><span class='match'>n<\/span>ice<\/li>\n  <li><span class='match'>n<\/span>ight<\/li>\n  <li><span class='match'>n<\/span>ine<\/li>\n  <li><span class='match'>n<\/span>o<\/li>\n  <li><span class='match'>n<\/span>on<\/li>\n  <li><span class='match'>n<\/span>one<\/li>\n  <li><span class='match'>n<\/span>ormal<\/li>\n  <li><span class='match'>n<\/span>orth<\/li>\n  <li><span class='match'>n<\/span>ot<\/li>\n  <li><span class='match'>n<\/span>ote<\/li>\n  <li><span class='match'>n<\/span>otice<\/li>\n  <li><span class='match'>n<\/span>ow<\/li>\n  <li><span class='match'>n<\/span>umber<\/li>\n  <li><span class='match'>p<\/span>ack<\/li>\n  <li><span class='match'>p<\/span>age<\/li>\n  <li><span class='match'>p<\/span>aint<\/li>\n  <li><span class='match'>p<\/span>air<\/li>\n  <li><span class='match'>p<\/span>aper<\/li>\n  <li><span class='match'>p<\/span>aragraph<\/li>\n  <li><span class='match'>p<\/span>ardon<\/li>\n  <li><span class='match'>p<\/span>arent<\/li>\n  <li><span class='match'>p<\/span>ark<\/li>\n  <li><span class='match'>p<\/span>art<\/li>\n  <li><span class='match'>p<\/span>articular<\/li>\n  <li><span class='match'>p<\/span>arty<\/li>\n  <li><span class='match'>p<\/span>ass<\/li>\n  <li><span class='match'>p<\/span>ast<\/li>\n  <li><span class='match'>p<\/span>ay<\/li>\n  <li><span class='match'>p<\/span>ence<\/li>\n  <li><span class='match'>p<\/span>ension<\/li>\n  <li><span class='match'>p<\/span>eople<\/li>\n  <li><span class='match'>p<\/span>er<\/li>\n  <li><span class='match'>p<\/span>ercent<\/li>\n  <li><span class='match'>p<\/span>erfect<\/li>\n  <li><span class='match'>p<\/span>erhaps<\/li>\n  <li><span class='match'>p<\/span>eriod<\/li>\n  <li><span class='match'>p<\/span>erson<\/li>\n  <li><span class='match'>p<\/span>hotograph<\/li>\n  <li><span class='match'>p<\/span>ick<\/li>\n  <li><span class='match'>p<\/span>icture<\/li>\n  <li><span class='match'>p<\/span>iece<\/li>\n  <li><span class='match'>p<\/span>lace<\/li>\n  <li><span class='match'>p<\/span>lan<\/li>\n  <li><span class='match'>p<\/span>lay<\/li>\n  <li><span class='match'>p<\/span>lease<\/li>\n  <li><span class='match'>p<\/span>lus<\/li>\n  <li><span class='match'>p<\/span>oint<\/li>\n  <li><span class='match'>p<\/span>olice<\/li>\n  <li><span class='match'>p<\/span>olicy<\/li>\n  <li><span class='match'>p<\/span>olitic<\/li>\n  <li><span class='match'>p<\/span>oor<\/li>\n  <li><span class='match'>p<\/span>osition<\/li>\n  <li><span class='match'>p<\/span>ositive<\/li>\n  <li><span class='match'>p<\/span>ossible<\/li>\n  <li><span class='match'>p<\/span>ost<\/li>\n  <li><span class='match'>p<\/span>ound<\/li>\n  <li><span class='match'>p<\/span>ower<\/li>\n  <li><span class='match'>p<\/span>ractise<\/li>\n  <li><span class='match'>p<\/span>repare<\/li>\n  <li><span class='match'>p<\/span>resent<\/li>\n  <li><span class='match'>p<\/span>ress<\/li>\n  <li><span class='match'>p<\/span>ressure<\/li>\n  <li><span class='match'>p<\/span>resume<\/li>\n  <li><span class='match'>p<\/span>retty<\/li>\n  <li><span class='match'>p<\/span>revious<\/li>\n  <li><span class='match'>p<\/span>rice<\/li>\n  <li><span class='match'>p<\/span>rint<\/li>\n  <li><span class='match'>p<\/span>rivate<\/li>\n  <li><span class='match'>p<\/span>robable<\/li>\n  <li><span class='match'>p<\/span>roblem<\/li>\n  <li><span class='match'>p<\/span>roceed<\/li>\n  <li><span class='match'>p<\/span>rocess<\/li>\n  <li><span class='match'>p<\/span>roduce<\/li>\n  <li><span class='match'>p<\/span>roduct<\/li>\n  <li><span class='match'>p<\/span>rogramme<\/li>\n  <li><span class='match'>p<\/span>roject<\/li>\n  <li><span class='match'>p<\/span>roper<\/li>\n  <li><span class='match'>p<\/span>ropose<\/li>\n  <li><span class='match'>p<\/span>rotect<\/li>\n  <li><span class='match'>p<\/span>rovide<\/li>\n  <li><span class='match'>p<\/span>ublic<\/li>\n  <li><span class='match'>p<\/span>ull<\/li>\n  <li><span class='match'>p<\/span>urpose<\/li>\n  <li><span class='match'>p<\/span>ush<\/li>\n  <li><span class='match'>p<\/span>ut<\/li>\n  <li><span class='match'>q<\/span>uality<\/li>\n  <li><span class='match'>q<\/span>uarter<\/li>\n  <li><span class='match'>q<\/span>uestion<\/li>\n  <li><span class='match'>q<\/span>uick<\/li>\n  <li><span class='match'>q<\/span>uid<\/li>\n  <li><span class='match'>q<\/span>uiet<\/li>\n  <li><span class='match'>q<\/span>uite<\/li>\n  <li><span class='match'>r<\/span>adio<\/li>\n  <li><span class='match'>r<\/span>ail<\/li>\n  <li><span class='match'>r<\/span>aise<\/li>\n  <li><span class='match'>r<\/span>ange<\/li>\n  <li><span class='match'>r<\/span>ate<\/li>\n  <li><span class='match'>r<\/span>ather<\/li>\n  <li><span class='match'>r<\/span>ead<\/li>\n  <li><span class='match'>r<\/span>eady<\/li>\n  <li><span class='match'>r<\/span>eal<\/li>\n  <li><span class='match'>r<\/span>ealise<\/li>\n  <li><span class='match'>r<\/span>eally<\/li>\n  <li><span class='match'>r<\/span>eason<\/li>\n  <li><span class='match'>r<\/span>eceive<\/li>\n  <li><span class='match'>r<\/span>ecent<\/li>\n  <li><span class='match'>r<\/span>eckon<\/li>\n  <li><span class='match'>r<\/span>ecognize<\/li>\n  <li><span class='match'>r<\/span>ecommend<\/li>\n  <li><span class='match'>r<\/span>ecord<\/li>\n  <li><span class='match'>r<\/span>ed<\/li>\n  <li><span class='match'>r<\/span>educe<\/li>\n  <li><span class='match'>r<\/span>efer<\/li>\n  <li><span class='match'>r<\/span>egard<\/li>\n  <li><span class='match'>r<\/span>egion<\/li>\n  <li><span class='match'>r<\/span>elation<\/li>\n  <li><span class='match'>r<\/span>emember<\/li>\n  <li><span class='match'>r<\/span>eport<\/li>\n  <li><span class='match'>r<\/span>epresent<\/li>\n  <li><span class='match'>r<\/span>equire<\/li>\n  <li><span class='match'>r<\/span>esearch<\/li>\n  <li><span class='match'>r<\/span>esource<\/li>\n  <li><span class='match'>r<\/span>espect<\/li>\n  <li><span class='match'>r<\/span>esponsible<\/li>\n  <li><span class='match'>r<\/span>est<\/li>\n  <li><span class='match'>r<\/span>esult<\/li>\n  <li><span class='match'>r<\/span>eturn<\/li>\n  <li><span class='match'>r<\/span>id<\/li>\n  <li><span class='match'>r<\/span>ight<\/li>\n  <li><span class='match'>r<\/span>ing<\/li>\n  <li><span class='match'>r<\/span>ise<\/li>\n  <li><span class='match'>r<\/span>oad<\/li>\n  <li><span class='match'>r<\/span>ole<\/li>\n  <li><span class='match'>r<\/span>oll<\/li>\n  <li><span class='match'>r<\/span>oom<\/li>\n  <li><span class='match'>r<\/span>ound<\/li>\n  <li><span class='match'>r<\/span>ule<\/li>\n  <li><span class='match'>r<\/span>un<\/li>\n  <li><span class='match'>s<\/span>afe<\/li>\n  <li><span class='match'>s<\/span>ale<\/li>\n  <li><span class='match'>s<\/span>ame<\/li>\n  <li><span class='match'>s<\/span>aturday<\/li>\n  <li><span class='match'>s<\/span>ave<\/li>\n  <li><span class='match'>s<\/span>ay<\/li>\n  <li><span class='match'>s<\/span>cheme<\/li>\n  <li><span class='match'>s<\/span>chool<\/li>\n  <li><span class='match'>s<\/span>cience<\/li>\n  <li><span class='match'>s<\/span>core<\/li>\n  <li><span class='match'>s<\/span>cotland<\/li>\n  <li><span class='match'>s<\/span>eat<\/li>\n  <li><span class='match'>s<\/span>econd<\/li>\n  <li><span class='match'>s<\/span>ecretary<\/li>\n  <li><span class='match'>s<\/span>ection<\/li>\n  <li><span class='match'>s<\/span>ecure<\/li>\n  <li><span class='match'>s<\/span>ee<\/li>\n  <li><span class='match'>s<\/span>eem<\/li>\n  <li><span class='match'>s<\/span>elf<\/li>\n  <li><span class='match'>s<\/span>ell<\/li>\n  <li><span class='match'>s<\/span>end<\/li>\n  <li><span class='match'>s<\/span>ense<\/li>\n  <li><span class='match'>s<\/span>eparate<\/li>\n  <li><span class='match'>s<\/span>erious<\/li>\n  <li><span class='match'>s<\/span>erve<\/li>\n  <li><span class='match'>s<\/span>ervice<\/li>\n  <li><span class='match'>s<\/span>et<\/li>\n  <li><span class='match'>s<\/span>ettle<\/li>\n  <li><span class='match'>s<\/span>even<\/li>\n  <li><span class='match'>s<\/span>ex<\/li>\n  <li><span class='match'>s<\/span>hall<\/li>\n  <li><span class='match'>s<\/span>hare<\/li>\n  <li><span class='match'>s<\/span>he<\/li>\n  <li><span class='match'>s<\/span>heet<\/li>\n  <li><span class='match'>s<\/span>hoe<\/li>\n  <li><span class='match'>s<\/span>hoot<\/li>\n  <li><span class='match'>s<\/span>hop<\/li>\n  <li><span class='match'>s<\/span>hort<\/li>\n  <li><span class='match'>s<\/span>hould<\/li>\n  <li><span class='match'>s<\/span>how<\/li>\n  <li><span class='match'>s<\/span>hut<\/li>\n  <li><span class='match'>s<\/span>ick<\/li>\n  <li><span class='match'>s<\/span>ide<\/li>\n  <li><span class='match'>s<\/span>ign<\/li>\n  <li><span class='match'>s<\/span>imilar<\/li>\n  <li><span class='match'>s<\/span>imple<\/li>\n  <li><span class='match'>s<\/span>ince<\/li>\n  <li><span class='match'>s<\/span>ing<\/li>\n  <li><span class='match'>s<\/span>ingle<\/li>\n  <li><span class='match'>s<\/span>ir<\/li>\n  <li><span class='match'>s<\/span>ister<\/li>\n  <li><span class='match'>s<\/span>it<\/li>\n  <li><span class='match'>s<\/span>ite<\/li>\n  <li><span class='match'>s<\/span>ituate<\/li>\n  <li><span class='match'>s<\/span>ix<\/li>\n  <li><span class='match'>s<\/span>ize<\/li>\n  <li><span class='match'>s<\/span>leep<\/li>\n  <li><span class='match'>s<\/span>light<\/li>\n  <li><span class='match'>s<\/span>low<\/li>\n  <li><span class='match'>s<\/span>mall<\/li>\n  <li><span class='match'>s<\/span>moke<\/li>\n  <li><span class='match'>s<\/span>o<\/li>\n  <li><span class='match'>s<\/span>ocial<\/li>\n  <li><span class='match'>s<\/span>ociety<\/li>\n  <li><span class='match'>s<\/span>ome<\/li>\n  <li><span class='match'>s<\/span>on<\/li>\n  <li><span class='match'>s<\/span>oon<\/li>\n  <li><span class='match'>s<\/span>orry<\/li>\n  <li><span class='match'>s<\/span>ort<\/li>\n  <li><span class='match'>s<\/span>ound<\/li>\n  <li><span class='match'>s<\/span>outh<\/li>\n  <li><span class='match'>s<\/span>pace<\/li>\n  <li><span class='match'>s<\/span>peak<\/li>\n  <li><span class='match'>s<\/span>pecial<\/li>\n  <li><span class='match'>s<\/span>pecific<\/li>\n  <li><span class='match'>s<\/span>peed<\/li>\n  <li><span class='match'>s<\/span>pell<\/li>\n  <li><span class='match'>s<\/span>pend<\/li>\n  <li><span class='match'>s<\/span>quare<\/li>\n  <li><span class='match'>s<\/span>taff<\/li>\n  <li><span class='match'>s<\/span>tage<\/li>\n  <li><span class='match'>s<\/span>tairs<\/li>\n  <li><span class='match'>s<\/span>tand<\/li>\n  <li><span class='match'>s<\/span>tandard<\/li>\n  <li><span class='match'>s<\/span>tart<\/li>\n  <li><span class='match'>s<\/span>tate<\/li>\n  <li><span class='match'>s<\/span>tation<\/li>\n  <li><span class='match'>s<\/span>tay<\/li>\n  <li><span class='match'>s<\/span>tep<\/li>\n  <li><span class='match'>s<\/span>tick<\/li>\n  <li><span class='match'>s<\/span>till<\/li>\n  <li><span class='match'>s<\/span>top<\/li>\n  <li><span class='match'>s<\/span>tory<\/li>\n  <li><span class='match'>s<\/span>traight<\/li>\n  <li><span class='match'>s<\/span>trategy<\/li>\n  <li><span class='match'>s<\/span>treet<\/li>\n  <li><span class='match'>s<\/span>trike<\/li>\n  <li><span class='match'>s<\/span>trong<\/li>\n  <li><span class='match'>s<\/span>tructure<\/li>\n  <li><span class='match'>s<\/span>tudent<\/li>\n  <li><span class='match'>s<\/span>tudy<\/li>\n  <li><span class='match'>s<\/span>tuff<\/li>\n  <li><span class='match'>s<\/span>tupid<\/li>\n  <li><span class='match'>s<\/span>ubject<\/li>\n  <li><span class='match'>s<\/span>ucceed<\/li>\n  <li><span class='match'>s<\/span>uch<\/li>\n  <li><span class='match'>s<\/span>udden<\/li>\n  <li><span class='match'>s<\/span>uggest<\/li>\n  <li><span class='match'>s<\/span>uit<\/li>\n  <li><span class='match'>s<\/span>ummer<\/li>\n  <li><span class='match'>s<\/span>un<\/li>\n  <li><span class='match'>s<\/span>unday<\/li>\n  <li><span class='match'>s<\/span>upply<\/li>\n  <li><span class='match'>s<\/span>upport<\/li>\n  <li><span class='match'>s<\/span>uppose<\/li>\n  <li><span class='match'>s<\/span>ure<\/li>\n  <li><span class='match'>s<\/span>urprise<\/li>\n  <li><span class='match'>s<\/span>witch<\/li>\n  <li><span class='match'>s<\/span>ystem<\/li>\n  <li><span class='match'>t<\/span>able<\/li>\n  <li><span class='match'>t<\/span>ake<\/li>\n  <li><span class='match'>t<\/span>alk<\/li>\n  <li><span class='match'>t<\/span>ape<\/li>\n  <li><span class='match'>t<\/span>ax<\/li>\n  <li><span class='match'>t<\/span>ea<\/li>\n  <li><span class='match'>t<\/span>each<\/li>\n  <li><span class='match'>t<\/span>eam<\/li>\n  <li><span class='match'>t<\/span>elephone<\/li>\n  <li><span class='match'>t<\/span>elevision<\/li>\n  <li><span class='match'>t<\/span>ell<\/li>\n  <li><span class='match'>t<\/span>en<\/li>\n  <li><span class='match'>t<\/span>end<\/li>\n  <li><span class='match'>t<\/span>erm<\/li>\n  <li><span class='match'>t<\/span>errible<\/li>\n  <li><span class='match'>t<\/span>est<\/li>\n  <li><span class='match'>t<\/span>han<\/li>\n  <li><span class='match'>t<\/span>hank<\/li>\n  <li><span class='match'>t<\/span>he<\/li>\n  <li><span class='match'>t<\/span>hen<\/li>\n  <li><span class='match'>t<\/span>here<\/li>\n  <li><span class='match'>t<\/span>herefore<\/li>\n  <li><span class='match'>t<\/span>hey<\/li>\n  <li><span class='match'>t<\/span>hing<\/li>\n  <li><span class='match'>t<\/span>hink<\/li>\n  <li><span class='match'>t<\/span>hirteen<\/li>\n  <li><span class='match'>t<\/span>hirty<\/li>\n  <li><span class='match'>t<\/span>his<\/li>\n  <li><span class='match'>t<\/span>hou<\/li>\n  <li><span class='match'>t<\/span>hough<\/li>\n  <li><span class='match'>t<\/span>housand<\/li>\n  <li><span class='match'>t<\/span>hree<\/li>\n  <li><span class='match'>t<\/span>hrough<\/li>\n  <li><span class='match'>t<\/span>hrow<\/li>\n  <li><span class='match'>t<\/span>hursday<\/li>\n  <li><span class='match'>t<\/span>ie<\/li>\n  <li><span class='match'>t<\/span>ime<\/li>\n  <li><span class='match'>t<\/span>o<\/li>\n  <li><span class='match'>t<\/span>oday<\/li>\n  <li><span class='match'>t<\/span>ogether<\/li>\n  <li><span class='match'>t<\/span>omorrow<\/li>\n  <li><span class='match'>t<\/span>onight<\/li>\n  <li><span class='match'>t<\/span>oo<\/li>\n  <li><span class='match'>t<\/span>op<\/li>\n  <li><span class='match'>t<\/span>otal<\/li>\n  <li><span class='match'>t<\/span>ouch<\/li>\n  <li><span class='match'>t<\/span>oward<\/li>\n  <li><span class='match'>t<\/span>own<\/li>\n  <li><span class='match'>t<\/span>rade<\/li>\n  <li><span class='match'>t<\/span>raffic<\/li>\n  <li><span class='match'>t<\/span>rain<\/li>\n  <li><span class='match'>t<\/span>ransport<\/li>\n  <li><span class='match'>t<\/span>ravel<\/li>\n  <li><span class='match'>t<\/span>reat<\/li>\n  <li><span class='match'>t<\/span>ree<\/li>\n  <li><span class='match'>t<\/span>rouble<\/li>\n  <li><span class='match'>t<\/span>rue<\/li>\n  <li><span class='match'>t<\/span>rust<\/li>\n  <li><span class='match'>t<\/span>ry<\/li>\n  <li><span class='match'>t<\/span>uesday<\/li>\n  <li><span class='match'>t<\/span>urn<\/li>\n  <li><span class='match'>t<\/span>welve<\/li>\n  <li><span class='match'>t<\/span>wenty<\/li>\n  <li><span class='match'>t<\/span>wo<\/li>\n  <li><span class='match'>t<\/span>ype<\/li>\n  <li><span class='match'>v<\/span>alue<\/li>\n  <li><span class='match'>v<\/span>arious<\/li>\n  <li><span class='match'>v<\/span>ery<\/li>\n  <li><span class='match'>v<\/span>ideo<\/li>\n  <li><span class='match'>v<\/span>iew<\/li>\n  <li><span class='match'>v<\/span>illage<\/li>\n  <li><span class='match'>v<\/span>isit<\/li>\n  <li><span class='match'>v<\/span>ote<\/li>\n  <li><span class='match'>w<\/span>age<\/li>\n  <li><span class='match'>w<\/span>ait<\/li>\n  <li><span class='match'>w<\/span>alk<\/li>\n  <li><span class='match'>w<\/span>all<\/li>\n  <li><span class='match'>w<\/span>ant<\/li>\n  <li><span class='match'>w<\/span>ar<\/li>\n  <li><span class='match'>w<\/span>arm<\/li>\n  <li><span class='match'>w<\/span>ash<\/li>\n  <li><span class='match'>w<\/span>aste<\/li>\n  <li><span class='match'>w<\/span>atch<\/li>\n  <li><span class='match'>w<\/span>ater<\/li>\n  <li><span class='match'>w<\/span>ay<\/li>\n  <li><span class='match'>w<\/span>e<\/li>\n  <li><span class='match'>w<\/span>ear<\/li>\n  <li><span class='match'>w<\/span>ednesday<\/li>\n  <li><span class='match'>w<\/span>ee<\/li>\n  <li><span class='match'>w<\/span>eek<\/li>\n  <li><span class='match'>w<\/span>eigh<\/li>\n  <li><span class='match'>w<\/span>elcome<\/li>\n  <li><span class='match'>w<\/span>ell<\/li>\n  <li><span class='match'>w<\/span>est<\/li>\n  <li><span class='match'>w<\/span>hat<\/li>\n  <li><span class='match'>w<\/span>hen<\/li>\n  <li><span class='match'>w<\/span>here<\/li>\n  <li><span class='match'>w<\/span>hether<\/li>\n  <li><span class='match'>w<\/span>hich<\/li>\n  <li><span class='match'>w<\/span>hile<\/li>\n  <li><span class='match'>w<\/span>hite<\/li>\n  <li><span class='match'>w<\/span>ho<\/li>\n  <li><span class='match'>w<\/span>hole<\/li>\n  <li><span class='match'>w<\/span>hy<\/li>\n  <li><span class='match'>w<\/span>ide<\/li>\n  <li><span class='match'>w<\/span>ife<\/li>\n  <li><span class='match'>w<\/span>ill<\/li>\n  <li><span class='match'>w<\/span>in<\/li>\n  <li><span class='match'>w<\/span>ind<\/li>\n  <li><span class='match'>w<\/span>indow<\/li>\n  <li><span class='match'>w<\/span>ish<\/li>\n  <li><span class='match'>w<\/span>ith<\/li>\n  <li><span class='match'>w<\/span>ithin<\/li>\n  <li><span class='match'>w<\/span>ithout<\/li>\n  <li><span class='match'>w<\/span>oman<\/li>\n  <li><span class='match'>w<\/span>onder<\/li>\n  <li><span class='match'>w<\/span>ood<\/li>\n  <li><span class='match'>w<\/span>ord<\/li>\n  <li><span class='match'>w<\/span>ork<\/li>\n  <li><span class='match'>w<\/span>orld<\/li>\n  <li><span class='match'>w<\/span>orry<\/li>\n  <li><span class='match'>w<\/span>orse<\/li>\n  <li><span class='match'>w<\/span>orth<\/li>\n  <li><span class='match'>w<\/span>ould<\/li>\n  <li><span class='match'>w<\/span>rite<\/li>\n  <li><span class='match'>w<\/span>rong<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script>
<!--/html_preserve-->
There we go! All the words starting with consonants.

Alternatively, you can use match argument to call upon these results

``` r
words %>% 
#no need to include ^ in front of the specified letters!
  str_view_all("^[aeouiy]", match = FALSE)
```

<!--html_preserve-->

<script type="application/json" data-for="htmlwidget-ea6e2a60123ce1eed850">{"x":{"html":"<ul>\n  <li>baby<\/li>\n  <li>back<\/li>\n  <li>bad<\/li>\n  <li>bag<\/li>\n  <li>balance<\/li>\n  <li>ball<\/li>\n  <li>bank<\/li>\n  <li>bar<\/li>\n  <li>base<\/li>\n  <li>basis<\/li>\n  <li>be<\/li>\n  <li>bear<\/li>\n  <li>beat<\/li>\n  <li>beauty<\/li>\n  <li>because<\/li>\n  <li>become<\/li>\n  <li>bed<\/li>\n  <li>before<\/li>\n  <li>begin<\/li>\n  <li>behind<\/li>\n  <li>believe<\/li>\n  <li>benefit<\/li>\n  <li>best<\/li>\n  <li>bet<\/li>\n  <li>between<\/li>\n  <li>big<\/li>\n  <li>bill<\/li>\n  <li>birth<\/li>\n  <li>bit<\/li>\n  <li>black<\/li>\n  <li>bloke<\/li>\n  <li>blood<\/li>\n  <li>blow<\/li>\n  <li>blue<\/li>\n  <li>board<\/li>\n  <li>boat<\/li>\n  <li>body<\/li>\n  <li>book<\/li>\n  <li>both<\/li>\n  <li>bother<\/li>\n  <li>bottle<\/li>\n  <li>bottom<\/li>\n  <li>box<\/li>\n  <li>boy<\/li>\n  <li>break<\/li>\n  <li>brief<\/li>\n  <li>brilliant<\/li>\n  <li>bring<\/li>\n  <li>britain<\/li>\n  <li>brother<\/li>\n  <li>budget<\/li>\n  <li>build<\/li>\n  <li>bus<\/li>\n  <li>business<\/li>\n  <li>busy<\/li>\n  <li>but<\/li>\n  <li>buy<\/li>\n  <li>by<\/li>\n  <li>cake<\/li>\n  <li>call<\/li>\n  <li>can<\/li>\n  <li>car<\/li>\n  <li>card<\/li>\n  <li>care<\/li>\n  <li>carry<\/li>\n  <li>case<\/li>\n  <li>cat<\/li>\n  <li>catch<\/li>\n  <li>cause<\/li>\n  <li>cent<\/li>\n  <li>centre<\/li>\n  <li>certain<\/li>\n  <li>chair<\/li>\n  <li>chairman<\/li>\n  <li>chance<\/li>\n  <li>change<\/li>\n  <li>chap<\/li>\n  <li>character<\/li>\n  <li>charge<\/li>\n  <li>cheap<\/li>\n  <li>check<\/li>\n  <li>child<\/li>\n  <li>choice<\/li>\n  <li>choose<\/li>\n  <li>Christ<\/li>\n  <li>Christmas<\/li>\n  <li>church<\/li>\n  <li>city<\/li>\n  <li>claim<\/li>\n  <li>class<\/li>\n  <li>clean<\/li>\n  <li>clear<\/li>\n  <li>client<\/li>\n  <li>clock<\/li>\n  <li>close<\/li>\n  <li>closes<\/li>\n  <li>clothe<\/li>\n  <li>club<\/li>\n  <li>coffee<\/li>\n  <li>cold<\/li>\n  <li>colleague<\/li>\n  <li>collect<\/li>\n  <li>college<\/li>\n  <li>colour<\/li>\n  <li>come<\/li>\n  <li>comment<\/li>\n  <li>commit<\/li>\n  <li>committee<\/li>\n  <li>common<\/li>\n  <li>community<\/li>\n  <li>company<\/li>\n  <li>compare<\/li>\n  <li>complete<\/li>\n  <li>compute<\/li>\n  <li>concern<\/li>\n  <li>condition<\/li>\n  <li>confer<\/li>\n  <li>consider<\/li>\n  <li>consult<\/li>\n  <li>contact<\/li>\n  <li>continue<\/li>\n  <li>contract<\/li>\n  <li>control<\/li>\n  <li>converse<\/li>\n  <li>cook<\/li>\n  <li>copy<\/li>\n  <li>corner<\/li>\n  <li>correct<\/li>\n  <li>cost<\/li>\n  <li>could<\/li>\n  <li>council<\/li>\n  <li>count<\/li>\n  <li>country<\/li>\n  <li>county<\/li>\n  <li>couple<\/li>\n  <li>course<\/li>\n  <li>court<\/li>\n  <li>cover<\/li>\n  <li>create<\/li>\n  <li>cross<\/li>\n  <li>cup<\/li>\n  <li>current<\/li>\n  <li>cut<\/li>\n  <li>dad<\/li>\n  <li>danger<\/li>\n  <li>date<\/li>\n  <li>day<\/li>\n  <li>dead<\/li>\n  <li>deal<\/li>\n  <li>dear<\/li>\n  <li>debate<\/li>\n  <li>decide<\/li>\n  <li>decision<\/li>\n  <li>deep<\/li>\n  <li>definite<\/li>\n  <li>degree<\/li>\n  <li>department<\/li>\n  <li>depend<\/li>\n  <li>describe<\/li>\n  <li>design<\/li>\n  <li>detail<\/li>\n  <li>develop<\/li>\n  <li>die<\/li>\n  <li>difference<\/li>\n  <li>difficult<\/li>\n  <li>dinner<\/li>\n  <li>direct<\/li>\n  <li>discuss<\/li>\n  <li>district<\/li>\n  <li>divide<\/li>\n  <li>do<\/li>\n  <li>doctor<\/li>\n  <li>document<\/li>\n  <li>dog<\/li>\n  <li>door<\/li>\n  <li>double<\/li>\n  <li>doubt<\/li>\n  <li>down<\/li>\n  <li>draw<\/li>\n  <li>dress<\/li>\n  <li>drink<\/li>\n  <li>drive<\/li>\n  <li>drop<\/li>\n  <li>dry<\/li>\n  <li>due<\/li>\n  <li>during<\/li>\n  <li>face<\/li>\n  <li>fact<\/li>\n  <li>fair<\/li>\n  <li>fall<\/li>\n  <li>family<\/li>\n  <li>far<\/li>\n  <li>farm<\/li>\n  <li>fast<\/li>\n  <li>father<\/li>\n  <li>favour<\/li>\n  <li>feed<\/li>\n  <li>feel<\/li>\n  <li>few<\/li>\n  <li>field<\/li>\n  <li>fight<\/li>\n  <li>figure<\/li>\n  <li>file<\/li>\n  <li>fill<\/li>\n  <li>film<\/li>\n  <li>final<\/li>\n  <li>finance<\/li>\n  <li>find<\/li>\n  <li>fine<\/li>\n  <li>finish<\/li>\n  <li>fire<\/li>\n  <li>first<\/li>\n  <li>fish<\/li>\n  <li>fit<\/li>\n  <li>five<\/li>\n  <li>flat<\/li>\n  <li>floor<\/li>\n  <li>fly<\/li>\n  <li>follow<\/li>\n  <li>food<\/li>\n  <li>foot<\/li>\n  <li>for<\/li>\n  <li>force<\/li>\n  <li>forget<\/li>\n  <li>form<\/li>\n  <li>fortune<\/li>\n  <li>forward<\/li>\n  <li>four<\/li>\n  <li>france<\/li>\n  <li>free<\/li>\n  <li>friday<\/li>\n  <li>friend<\/li>\n  <li>from<\/li>\n  <li>front<\/li>\n  <li>full<\/li>\n  <li>fun<\/li>\n  <li>function<\/li>\n  <li>fund<\/li>\n  <li>further<\/li>\n  <li>future<\/li>\n  <li>game<\/li>\n  <li>garden<\/li>\n  <li>gas<\/li>\n  <li>general<\/li>\n  <li>germany<\/li>\n  <li>get<\/li>\n  <li>girl<\/li>\n  <li>give<\/li>\n  <li>glass<\/li>\n  <li>go<\/li>\n  <li>god<\/li>\n  <li>good<\/li>\n  <li>goodbye<\/li>\n  <li>govern<\/li>\n  <li>grand<\/li>\n  <li>grant<\/li>\n  <li>great<\/li>\n  <li>green<\/li>\n  <li>ground<\/li>\n  <li>group<\/li>\n  <li>grow<\/li>\n  <li>guess<\/li>\n  <li>guy<\/li>\n  <li>hair<\/li>\n  <li>half<\/li>\n  <li>hall<\/li>\n  <li>hand<\/li>\n  <li>hang<\/li>\n  <li>happen<\/li>\n  <li>happy<\/li>\n  <li>hard<\/li>\n  <li>hate<\/li>\n  <li>have<\/li>\n  <li>he<\/li>\n  <li>head<\/li>\n  <li>health<\/li>\n  <li>hear<\/li>\n  <li>heart<\/li>\n  <li>heat<\/li>\n  <li>heavy<\/li>\n  <li>hell<\/li>\n  <li>help<\/li>\n  <li>here<\/li>\n  <li>high<\/li>\n  <li>history<\/li>\n  <li>hit<\/li>\n  <li>hold<\/li>\n  <li>holiday<\/li>\n  <li>home<\/li>\n  <li>honest<\/li>\n  <li>hope<\/li>\n  <li>horse<\/li>\n  <li>hospital<\/li>\n  <li>hot<\/li>\n  <li>hour<\/li>\n  <li>house<\/li>\n  <li>how<\/li>\n  <li>however<\/li>\n  <li>hullo<\/li>\n  <li>hundred<\/li>\n  <li>husband<\/li>\n  <li>jesus<\/li>\n  <li>job<\/li>\n  <li>join<\/li>\n  <li>judge<\/li>\n  <li>jump<\/li>\n  <li>just<\/li>\n  <li>keep<\/li>\n  <li>key<\/li>\n  <li>kid<\/li>\n  <li>kill<\/li>\n  <li>kind<\/li>\n  <li>king<\/li>\n  <li>kitchen<\/li>\n  <li>knock<\/li>\n  <li>know<\/li>\n  <li>labour<\/li>\n  <li>lad<\/li>\n  <li>lady<\/li>\n  <li>land<\/li>\n  <li>language<\/li>\n  <li>large<\/li>\n  <li>last<\/li>\n  <li>late<\/li>\n  <li>laugh<\/li>\n  <li>law<\/li>\n  <li>lay<\/li>\n  <li>lead<\/li>\n  <li>learn<\/li>\n  <li>leave<\/li>\n  <li>left<\/li>\n  <li>leg<\/li>\n  <li>less<\/li>\n  <li>let<\/li>\n  <li>letter<\/li>\n  <li>level<\/li>\n  <li>lie<\/li>\n  <li>life<\/li>\n  <li>light<\/li>\n  <li>like<\/li>\n  <li>likely<\/li>\n  <li>limit<\/li>\n  <li>line<\/li>\n  <li>link<\/li>\n  <li>list<\/li>\n  <li>listen<\/li>\n  <li>little<\/li>\n  <li>live<\/li>\n  <li>load<\/li>\n  <li>local<\/li>\n  <li>lock<\/li>\n  <li>london<\/li>\n  <li>long<\/li>\n  <li>look<\/li>\n  <li>lord<\/li>\n  <li>lose<\/li>\n  <li>lot<\/li>\n  <li>love<\/li>\n  <li>low<\/li>\n  <li>luck<\/li>\n  <li>lunch<\/li>\n  <li>machine<\/li>\n  <li>main<\/li>\n  <li>major<\/li>\n  <li>make<\/li>\n  <li>man<\/li>\n  <li>manage<\/li>\n  <li>many<\/li>\n  <li>mark<\/li>\n  <li>market<\/li>\n  <li>marry<\/li>\n  <li>match<\/li>\n  <li>matter<\/li>\n  <li>may<\/li>\n  <li>maybe<\/li>\n  <li>mean<\/li>\n  <li>meaning<\/li>\n  <li>measure<\/li>\n  <li>meet<\/li>\n  <li>member<\/li>\n  <li>mention<\/li>\n  <li>middle<\/li>\n  <li>might<\/li>\n  <li>mile<\/li>\n  <li>milk<\/li>\n  <li>million<\/li>\n  <li>mind<\/li>\n  <li>minister<\/li>\n  <li>minus<\/li>\n  <li>minute<\/li>\n  <li>miss<\/li>\n  <li>mister<\/li>\n  <li>moment<\/li>\n  <li>monday<\/li>\n  <li>money<\/li>\n  <li>month<\/li>\n  <li>more<\/li>\n  <li>morning<\/li>\n  <li>most<\/li>\n  <li>mother<\/li>\n  <li>motion<\/li>\n  <li>move<\/li>\n  <li>mrs<\/li>\n  <li>much<\/li>\n  <li>music<\/li>\n  <li>must<\/li>\n  <li>name<\/li>\n  <li>nation<\/li>\n  <li>nature<\/li>\n  <li>near<\/li>\n  <li>necessary<\/li>\n  <li>need<\/li>\n  <li>never<\/li>\n  <li>new<\/li>\n  <li>news<\/li>\n  <li>next<\/li>\n  <li>nice<\/li>\n  <li>night<\/li>\n  <li>nine<\/li>\n  <li>no<\/li>\n  <li>non<\/li>\n  <li>none<\/li>\n  <li>normal<\/li>\n  <li>north<\/li>\n  <li>not<\/li>\n  <li>note<\/li>\n  <li>notice<\/li>\n  <li>now<\/li>\n  <li>number<\/li>\n  <li>pack<\/li>\n  <li>page<\/li>\n  <li>paint<\/li>\n  <li>pair<\/li>\n  <li>paper<\/li>\n  <li>paragraph<\/li>\n  <li>pardon<\/li>\n  <li>parent<\/li>\n  <li>park<\/li>\n  <li>part<\/li>\n  <li>particular<\/li>\n  <li>party<\/li>\n  <li>pass<\/li>\n  <li>past<\/li>\n  <li>pay<\/li>\n  <li>pence<\/li>\n  <li>pension<\/li>\n  <li>people<\/li>\n  <li>per<\/li>\n  <li>percent<\/li>\n  <li>perfect<\/li>\n  <li>perhaps<\/li>\n  <li>period<\/li>\n  <li>person<\/li>\n  <li>photograph<\/li>\n  <li>pick<\/li>\n  <li>picture<\/li>\n  <li>piece<\/li>\n  <li>place<\/li>\n  <li>plan<\/li>\n  <li>play<\/li>\n  <li>please<\/li>\n  <li>plus<\/li>\n  <li>point<\/li>\n  <li>police<\/li>\n  <li>policy<\/li>\n  <li>politic<\/li>\n  <li>poor<\/li>\n  <li>position<\/li>\n  <li>positive<\/li>\n  <li>possible<\/li>\n  <li>post<\/li>\n  <li>pound<\/li>\n  <li>power<\/li>\n  <li>practise<\/li>\n  <li>prepare<\/li>\n  <li>present<\/li>\n  <li>press<\/li>\n  <li>pressure<\/li>\n  <li>presume<\/li>\n  <li>pretty<\/li>\n  <li>previous<\/li>\n  <li>price<\/li>\n  <li>print<\/li>\n  <li>private<\/li>\n  <li>probable<\/li>\n  <li>problem<\/li>\n  <li>proceed<\/li>\n  <li>process<\/li>\n  <li>produce<\/li>\n  <li>product<\/li>\n  <li>programme<\/li>\n  <li>project<\/li>\n  <li>proper<\/li>\n  <li>propose<\/li>\n  <li>protect<\/li>\n  <li>provide<\/li>\n  <li>public<\/li>\n  <li>pull<\/li>\n  <li>purpose<\/li>\n  <li>push<\/li>\n  <li>put<\/li>\n  <li>quality<\/li>\n  <li>quarter<\/li>\n  <li>question<\/li>\n  <li>quick<\/li>\n  <li>quid<\/li>\n  <li>quiet<\/li>\n  <li>quite<\/li>\n  <li>radio<\/li>\n  <li>rail<\/li>\n  <li>raise<\/li>\n  <li>range<\/li>\n  <li>rate<\/li>\n  <li>rather<\/li>\n  <li>read<\/li>\n  <li>ready<\/li>\n  <li>real<\/li>\n  <li>realise<\/li>\n  <li>really<\/li>\n  <li>reason<\/li>\n  <li>receive<\/li>\n  <li>recent<\/li>\n  <li>reckon<\/li>\n  <li>recognize<\/li>\n  <li>recommend<\/li>\n  <li>record<\/li>\n  <li>red<\/li>\n  <li>reduce<\/li>\n  <li>refer<\/li>\n  <li>regard<\/li>\n  <li>region<\/li>\n  <li>relation<\/li>\n  <li>remember<\/li>\n  <li>report<\/li>\n  <li>represent<\/li>\n  <li>require<\/li>\n  <li>research<\/li>\n  <li>resource<\/li>\n  <li>respect<\/li>\n  <li>responsible<\/li>\n  <li>rest<\/li>\n  <li>result<\/li>\n  <li>return<\/li>\n  <li>rid<\/li>\n  <li>right<\/li>\n  <li>ring<\/li>\n  <li>rise<\/li>\n  <li>road<\/li>\n  <li>role<\/li>\n  <li>roll<\/li>\n  <li>room<\/li>\n  <li>round<\/li>\n  <li>rule<\/li>\n  <li>run<\/li>\n  <li>safe<\/li>\n  <li>sale<\/li>\n  <li>same<\/li>\n  <li>saturday<\/li>\n  <li>save<\/li>\n  <li>say<\/li>\n  <li>scheme<\/li>\n  <li>school<\/li>\n  <li>science<\/li>\n  <li>score<\/li>\n  <li>scotland<\/li>\n  <li>seat<\/li>\n  <li>second<\/li>\n  <li>secretary<\/li>\n  <li>section<\/li>\n  <li>secure<\/li>\n  <li>see<\/li>\n  <li>seem<\/li>\n  <li>self<\/li>\n  <li>sell<\/li>\n  <li>send<\/li>\n  <li>sense<\/li>\n  <li>separate<\/li>\n  <li>serious<\/li>\n  <li>serve<\/li>\n  <li>service<\/li>\n  <li>set<\/li>\n  <li>settle<\/li>\n  <li>seven<\/li>\n  <li>sex<\/li>\n  <li>shall<\/li>\n  <li>share<\/li>\n  <li>she<\/li>\n  <li>sheet<\/li>\n  <li>shoe<\/li>\n  <li>shoot<\/li>\n  <li>shop<\/li>\n  <li>short<\/li>\n  <li>should<\/li>\n  <li>show<\/li>\n  <li>shut<\/li>\n  <li>sick<\/li>\n  <li>side<\/li>\n  <li>sign<\/li>\n  <li>similar<\/li>\n  <li>simple<\/li>\n  <li>since<\/li>\n  <li>sing<\/li>\n  <li>single<\/li>\n  <li>sir<\/li>\n  <li>sister<\/li>\n  <li>sit<\/li>\n  <li>site<\/li>\n  <li>situate<\/li>\n  <li>six<\/li>\n  <li>size<\/li>\n  <li>sleep<\/li>\n  <li>slight<\/li>\n  <li>slow<\/li>\n  <li>small<\/li>\n  <li>smoke<\/li>\n  <li>so<\/li>\n  <li>social<\/li>\n  <li>society<\/li>\n  <li>some<\/li>\n  <li>son<\/li>\n  <li>soon<\/li>\n  <li>sorry<\/li>\n  <li>sort<\/li>\n  <li>sound<\/li>\n  <li>south<\/li>\n  <li>space<\/li>\n  <li>speak<\/li>\n  <li>special<\/li>\n  <li>specific<\/li>\n  <li>speed<\/li>\n  <li>spell<\/li>\n  <li>spend<\/li>\n  <li>square<\/li>\n  <li>staff<\/li>\n  <li>stage<\/li>\n  <li>stairs<\/li>\n  <li>stand<\/li>\n  <li>standard<\/li>\n  <li>start<\/li>\n  <li>state<\/li>\n  <li>station<\/li>\n  <li>stay<\/li>\n  <li>step<\/li>\n  <li>stick<\/li>\n  <li>still<\/li>\n  <li>stop<\/li>\n  <li>story<\/li>\n  <li>straight<\/li>\n  <li>strategy<\/li>\n  <li>street<\/li>\n  <li>strike<\/li>\n  <li>strong<\/li>\n  <li>structure<\/li>\n  <li>student<\/li>\n  <li>study<\/li>\n  <li>stuff<\/li>\n  <li>stupid<\/li>\n  <li>subject<\/li>\n  <li>succeed<\/li>\n  <li>such<\/li>\n  <li>sudden<\/li>\n  <li>suggest<\/li>\n  <li>suit<\/li>\n  <li>summer<\/li>\n  <li>sun<\/li>\n  <li>sunday<\/li>\n  <li>supply<\/li>\n  <li>support<\/li>\n  <li>suppose<\/li>\n  <li>sure<\/li>\n  <li>surprise<\/li>\n  <li>switch<\/li>\n  <li>system<\/li>\n  <li>table<\/li>\n  <li>take<\/li>\n  <li>talk<\/li>\n  <li>tape<\/li>\n  <li>tax<\/li>\n  <li>tea<\/li>\n  <li>teach<\/li>\n  <li>team<\/li>\n  <li>telephone<\/li>\n  <li>television<\/li>\n  <li>tell<\/li>\n  <li>ten<\/li>\n  <li>tend<\/li>\n  <li>term<\/li>\n  <li>terrible<\/li>\n  <li>test<\/li>\n  <li>than<\/li>\n  <li>thank<\/li>\n  <li>the<\/li>\n  <li>then<\/li>\n  <li>there<\/li>\n  <li>therefore<\/li>\n  <li>they<\/li>\n  <li>thing<\/li>\n  <li>think<\/li>\n  <li>thirteen<\/li>\n  <li>thirty<\/li>\n  <li>this<\/li>\n  <li>thou<\/li>\n  <li>though<\/li>\n  <li>thousand<\/li>\n  <li>three<\/li>\n  <li>through<\/li>\n  <li>throw<\/li>\n  <li>thursday<\/li>\n  <li>tie<\/li>\n  <li>time<\/li>\n  <li>to<\/li>\n  <li>today<\/li>\n  <li>together<\/li>\n  <li>tomorrow<\/li>\n  <li>tonight<\/li>\n  <li>too<\/li>\n  <li>top<\/li>\n  <li>total<\/li>\n  <li>touch<\/li>\n  <li>toward<\/li>\n  <li>town<\/li>\n  <li>trade<\/li>\n  <li>traffic<\/li>\n  <li>train<\/li>\n  <li>transport<\/li>\n  <li>travel<\/li>\n  <li>treat<\/li>\n  <li>tree<\/li>\n  <li>trouble<\/li>\n  <li>true<\/li>\n  <li>trust<\/li>\n  <li>try<\/li>\n  <li>tuesday<\/li>\n  <li>turn<\/li>\n  <li>twelve<\/li>\n  <li>twenty<\/li>\n  <li>two<\/li>\n  <li>type<\/li>\n  <li>value<\/li>\n  <li>various<\/li>\n  <li>very<\/li>\n  <li>video<\/li>\n  <li>view<\/li>\n  <li>village<\/li>\n  <li>visit<\/li>\n  <li>vote<\/li>\n  <li>wage<\/li>\n  <li>wait<\/li>\n  <li>walk<\/li>\n  <li>wall<\/li>\n  <li>want<\/li>\n  <li>war<\/li>\n  <li>warm<\/li>\n  <li>wash<\/li>\n  <li>waste<\/li>\n  <li>watch<\/li>\n  <li>water<\/li>\n  <li>way<\/li>\n  <li>we<\/li>\n  <li>wear<\/li>\n  <li>wednesday<\/li>\n  <li>wee<\/li>\n  <li>week<\/li>\n  <li>weigh<\/li>\n  <li>welcome<\/li>\n  <li>well<\/li>\n  <li>west<\/li>\n  <li>what<\/li>\n  <li>when<\/li>\n  <li>where<\/li>\n  <li>whether<\/li>\n  <li>which<\/li>\n  <li>while<\/li>\n  <li>white<\/li>\n  <li>who<\/li>\n  <li>whole<\/li>\n  <li>why<\/li>\n  <li>wide<\/li>\n  <li>wife<\/li>\n  <li>will<\/li>\n  <li>win<\/li>\n  <li>wind<\/li>\n  <li>window<\/li>\n  <li>wish<\/li>\n  <li>with<\/li>\n  <li>within<\/li>\n  <li>without<\/li>\n  <li>woman<\/li>\n  <li>wonder<\/li>\n  <li>wood<\/li>\n  <li>word<\/li>\n  <li>work<\/li>\n  <li>world<\/li>\n  <li>worry<\/li>\n  <li>worse<\/li>\n  <li>worth<\/li>\n  <li>would<\/li>\n  <li>write<\/li>\n  <li>wrong<\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script>
<!--/html_preserve-->
End with *ed*, but not with *eed*.

``` r
words %>% 
#here w specify ending with ed using $, but not eed by using ^
str_view_all("[^e]ed$", match = TRUE)
```

<!--html_preserve-->

<script type="application/json" data-for="htmlwidget-08be8767d5dae785c8ee">{"x":{"html":"<ul>\n  <li><span class='match'>bed<\/span><\/li>\n  <li>hund<span class='match'>red<\/span><\/li>\n  <li><span class='match'>red<\/span><\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script>
<!--/html_preserve-->
End with *ing* or *ise*.

``` r
words %>% 
#using | we can indicate we want either ng or se proceding i
str_view_all("i(ng|se)$", match = TRUE) 
```

<!--html_preserve-->

<script type="application/json" data-for="htmlwidget-098703c6ca7fe3f4fb41">{"x":{"html":"<ul>\n  <li>advert<span class='match'>ise<\/span><\/li>\n  <li>br<span class='match'>ing<\/span><\/li>\n  <li>dur<span class='match'>ing<\/span><\/li>\n  <li>even<span class='match'>ing<\/span><\/li>\n  <li>exerc<span class='match'>ise<\/span><\/li>\n  <li>k<span class='match'>ing<\/span><\/li>\n  <li>mean<span class='match'>ing<\/span><\/li>\n  <li>morn<span class='match'>ing<\/span><\/li>\n  <li>otherw<span class='match'>ise<\/span><\/li>\n  <li>pract<span class='match'>ise<\/span><\/li>\n  <li>ra<span class='match'>ise<\/span><\/li>\n  <li>real<span class='match'>ise<\/span><\/li>\n  <li>r<span class='match'>ing<\/span><\/li>\n  <li>r<span class='match'>ise<\/span><\/li>\n  <li>s<span class='match'>ing<\/span><\/li>\n  <li>surpr<span class='match'>ise<\/span><\/li>\n  <li>th<span class='match'>ing<\/span><\/li>\n<\/ul>"},"evals":[],"jsHooks":[]}</script>
<!--/html_preserve-->
2. Write a function
-------------------

For the second part of my homework 6, I will be writing functions. As I am hoping to create a package that I can use with my thesis work looking at the relationship of stream discharge and smolt production, I will try to create relevant functions. As most of my environmental covariates coming from the US Geological survey website, I will have to be converting several variables from imprial to metric units.

### Discharge

First I will make a function to convert discharge in cubic feet per second to cubic metres per second:

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

    ##   year coho_spaw coho_smol chin_spaw chin_smol discharge sediment
    ## 1 2006       152      2006        59    149661  66.27845     20.3
    ## 2 2007       181      3375       126    325791  53.69991     15.7
    ## 3 2008       205      2769         7      7293  80.78557     16.0
    ## 4 2009        71      1725        13     27896  64.10703     23.0
    ## 5 2010       281      4508        17     50414  98.43554     13.2
    ## 6 2011       245      4407        20     25020  72.51416      8.5
    ## 7 2012       304      4077        90     71947  71.19987      9.9
    ## 8 2013       572      5156        23     47670  89.39984     12.4
    ## 9 2014       196      5940        32     54120  50.10705     13.6

``` r
#let's use the function to convert all of our discharge values 
ef_trask$dishcharge_converted <- ft2m(ef_trask$discharge)
ef_trask %>% 
  kable(col.names = c("Year", "Coho spawners", "Coho smolts", "Chinook spawners", "Chinook smolts", "Cubic feet per second", "Cubic metres per second", "Sediment tonnes per day"))
```

|  Year|  Coho spawners|  Coho smolts|  Chinook spawners|  Chinook smolts|  Cubic feet per second|  Cubic metres per second|  Sediment tonnes per day|
|-----:|--------------:|------------:|-----------------:|---------------:|----------------------:|------------------------:|------------------------:|
|  2006|            152|         2006|                59|          149661|               66.27845|                     20.3|                 1.876797|
|  2007|            181|         3375|               126|          325791|               53.69991|                     15.7|                 1.520612|
|  2008|            205|         2769|                 7|            7293|               80.78557|                     16.0|                 2.287593|
|  2009|             71|         1725|                13|           27896|               64.10703|                     23.0|                 1.815309|
|  2010|            281|         4508|                17|           50414|               98.43554|                     13.2|                 2.787384|
|  2011|            245|         4407|                20|           25020|               72.51416|                      8.5|                 2.053373|
|  2012|            304|         4077|                90|           71947|               71.19987|                      9.9|                 2.016156|
|  2013|            572|         5156|                23|           47670|               89.39984|                     12.4|                 2.531522|
|  2014|            196|         5940|                32|           54120|               50.10705|                     13.6|                 1.418874|

Yay, look how beautifully that worked! Now for the next function...

### Sediment

As my discharge measurements coming the United States Geological Survey website is giving me sediment output in units of tonnes/day, and will want to convert these values to kg/day. The conversion for this goes as such:

**1 tonne/day = 907.185 kg/day**

Therefore, writing a function for this will be quite simple.

``` r
#The input of 'ft2m' is temperature in Fahrenheit
t2kg <- function(t) {
#F to C formula
  kg <- t*(907.185)

  #FtoC will return the temperature in Celsius
  return(kg)
}
```

There we go, the function has been written! Let's give this baby a test drive!

``` r
t2kg(1)
```

    ## [1] 907.185

Wahoo! It worked! At least that's what it seems at this point... Time to put it through some tests:

``` r
test_that("Simple cases work", {
  expect_equal(t2kg(1), 907.185)
#this time we will use greater than. This will test to make the converted value is larger than the specified value (4000 in this case) 
  expect_gt(t2kg(5), 4000)
})
```

Look at that, my second function passed the tests with flying colours :) I am a proud papa!

Time to convert all of the discharge values in my dataset.

``` r
#let's use the fnction to convert all our sediment values
ef_trask$sediment_converted <- t2kg(ef_trask$sediment)
ef_trask %>% 
#let's give out table fancy titles  
  kable(col.names = c("Year", "Coho spawners", "Coho smolts", "Chinook spawners", "Chinook smolts", "Cubic feet per second", "Cubic metres per second", "Sediment tonnes per day", "Sediment kg per day"))
```

|  Year|  Coho spawners|  Coho smolts|  Chinook spawners|  Chinook smolts|  Cubic feet per second|  Cubic metres per second|  Sediment tonnes per day|  Sediment kg per day|
|-----:|--------------:|------------:|-----------------:|---------------:|----------------------:|------------------------:|------------------------:|--------------------:|
|  2006|            152|         2006|                59|          149661|               66.27845|                     20.3|                 1.876797|            18415.856|
|  2007|            181|         3375|               126|          325791|               53.69991|                     15.7|                 1.520612|            14242.805|
|  2008|            205|         2769|                 7|            7293|               80.78557|                     16.0|                 2.287593|            14514.960|
|  2009|             71|         1725|                13|           27896|               64.10703|                     23.0|                 1.815309|            20865.255|
|  2010|            281|         4508|                17|           50414|               98.43554|                     13.2|                 2.787384|            11974.842|
|  2011|            245|         4407|                20|           25020|               72.51416|                      8.5|                 2.053373|             7711.073|
|  2012|            304|         4077|                90|           71947|               71.19987|                      9.9|                 2.016156|             8981.131|
|  2013|            572|         5156|                23|           47670|               89.39984|                     12.4|                 2.531522|            11249.094|
|  2014|            196|         5940|                32|           54120|               50.10705|                     13.6|                 1.418874|            12337.716|

Wow look at that, all of my conversions doen so easily with the easy creation of a couple functions. I sure am looking forward to creating more functions, maybe even a whole package to deal with my dataset.
