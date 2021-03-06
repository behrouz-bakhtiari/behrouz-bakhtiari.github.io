---
layout: post
title: Creating Github Markdowns in RStudio
subtitle: a "very" short introduction
tags: [blogging, R, RStudio]
---

You can create markdown documents (.md files) using RStudio. RStudio generally produces R Markdown documents (.Rmd files). However, with a simple modification, you can create your .md file with RStudio before pushing that into your Github Pages. For more details on using R Markdown see [rmarkdown](http://rmarkdown.rstudio.com).

All you need to do is include in the **front-matter** of your document that the variant of markdown you will be using is &gt;markdown\_github.

Then you would create your markdown document as usual. When you click the **Knit** button a document will be generated that includes both content as well as the output of any embedded R code chunks within the document. If there are any plots generated with your markdown document, make sure you upload that into the corresponding folder within your repository before publishing the new page.

In the markdown document, you can embed an R code chunk like this:

``` r
summary(mtcars)
```

    ##       mpg             cyl             disp             hp       
    ##  Min.   :10.40   Min.   :4.000   Min.   : 71.1   Min.   : 52.0  
    ##  1st Qu.:15.43   1st Qu.:4.000   1st Qu.:120.8   1st Qu.: 96.5  
    ##  Median :19.20   Median :6.000   Median :196.3   Median :123.0  
    ##  Mean   :20.09   Mean   :6.188   Mean   :230.7   Mean   :146.7  
    ##  3rd Qu.:22.80   3rd Qu.:8.000   3rd Qu.:326.0   3rd Qu.:180.0  
    ##  Max.   :33.90   Max.   :8.000   Max.   :472.0   Max.   :335.0  
    ##       drat             wt             qsec             vs        
    ##  Min.   :2.760   Min.   :1.513   Min.   :14.50   Min.   :0.0000  
    ##  1st Qu.:3.080   1st Qu.:2.581   1st Qu.:16.89   1st Qu.:0.0000  
    ##  Median :3.695   Median :3.325   Median :17.71   Median :0.0000  
    ##  Mean   :3.597   Mean   :3.217   Mean   :17.85   Mean   :0.4375  
    ##  3rd Qu.:3.920   3rd Qu.:3.610   3rd Qu.:18.90   3rd Qu.:1.0000  
    ##  Max.   :4.930   Max.   :5.424   Max.   :22.90   Max.   :1.0000  
    ##        am              gear            carb      
    ##  Min.   :0.0000   Min.   :3.000   Min.   :1.000  
    ##  1st Qu.:0.0000   1st Qu.:3.000   1st Qu.:2.000  
    ##  Median :0.0000   Median :4.000   Median :2.000  
    ##  Mean   :0.4062   Mean   :3.688   Mean   :2.812  
    ##  3rd Qu.:1.0000   3rd Qu.:4.000   3rd Qu.:4.000  
    ##  Max.   :1.0000   Max.   :5.000   Max.   :8.000

In addition to that, you can also include plots, where you have the option to include or exclude the code. For example,

#### Including the code

``` r
plot(pressure)
```

![plot](/img/pressure-1.png)

#### Excluding the code

![plot](/img/unnamed-chunk-1-1.png)

Remember, if you use RStudio you need to change the front matter of your document to include `variant: markdown_github` and then knit, to produce an `.md` file.
Once you are done knitting the document and have the `.md` file, you need to,

-   upload your .md file into your Github repository (new post).
-   upload any figure that's created by RStudio into the corresponding folder in your repository. **Note** the figures will be created in a separate folder once you knit your document!
-   make sure that the path to the plots in your markdown will be changed to the location, where your images are stored within your respository.
-   add a new front matter in the Github editor of your post (this includes indicating that it is a post, a title, tags, etc.).
-   finally watch for any errors or inconsistencies regarding the **title** of your post. I do not have a reason for this, but editing the filename will result in the title you use in the front matter to be used as the title of your post, instead of the filename!

Happy knitting!
