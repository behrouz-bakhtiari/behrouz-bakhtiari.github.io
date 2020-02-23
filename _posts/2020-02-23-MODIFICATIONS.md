If you have ever looked at messy data you probably know already that it could be very frustrating to try to clean it if you do not have the right tools at your disposal. Some people even try to do it **gasps** manually.

Here I would like to introduce two very useful functions in the `tidyr` package used in `R`. These two functions are `tidyr::gather()` and `tidyr::spread`. The `gather()` function will help you convert a wide dataset to a long one and `spread()` does the opposite. They are both very useful and depending on your purpose you may use one or the other, or both!

### The Dataset

Consider the following dataset, which is presented as a *time series* monitoring average sales at a mid-size retail store (measured in $1,000s) collected monthly for 12 months, grouped based on three categories; sales from the *produce* section, sales from the *meat* section, and sales from the *deli* section.

    ##   Category April August December February January July June March May November
    ## 1     meat    28     29       31       31      28   32   32    26  33       30
    ## 2  produce    49     57       48       52      45   55   54    51  52       49
    ## 3     deli    15     16       15       17      16   18   16    17  16       17
    ##   October September
    ## 1      27        28
    ## 2      53        55
    ## 3      17        16

You may want to *clean* in different ways. However, two ideas may immediately jump at you as the most obvious ways you may want to change (or clean) this dataset. You may either want to make it longer by combining (or *gathering*) the values from different months into one variable (`month` maybe), or you may want to make it wider by *spreading* the contents of the `category` variable into two new variables. Let's start with the first idea.

### Wide to Long

You already have an idea in mind about what your new variable should look like. Let's call it `Month`. This variable would contain the name of the month, for which we have collected sales volumes. We already know there will be some repetition here since we are looking at sales numbers for three different department.

``` r
sales2 <- tidyr::gather(sales, "Month", "Sales", -Category)
```

You might have noticed that we excluded the variable Category, using `-Category`. This is because we did not want Category to be gathered (combined) along with the months. Also notice, since the content of the variables in the original dataset was sales volumes, after combining those variables into a new variable (Month) we should also house the sales volumes somewhere. That is why we are including `"Sales"` in the code, indicating that the content of the original variables should now be included under this new variable `Sales`.

Let's look at the new dataset `Sales2` below.

    ##    Category     Month Sales
    ## 1      meat     April    28
    ## 2   produce     April    49
    ## 3      deli     April    15
    ## 4      meat    August    29
    ## 5   produce    August    57
    ## 6      deli    August    16
    ## 7      meat  December    31
    ## 8   produce  December    48
    ## 9      deli  December    15
    ## 10     meat  February    31
    ## 11  produce  February    52
    ## 12     deli  February    17
    ## 13     meat   January    28
    ## 14  produce   January    45
    ## 15     deli   January    16
    ## 16     meat      July    32
    ## 17  produce      July    55
    ## 18     deli      July    18
    ## 19     meat      June    32
    ## 20  produce      June    54
    ## 21     deli      June    16
    ## 22     meat     March    26
    ## 23  produce     March    51
    ## 24     deli     March    17
    ## 25     meat       May    33
    ## 26  produce       May    52
    ## 27     deli       May    16
    ## 28     meat  November    30
    ## 29  produce  November    49
    ## 30     deli  November    17
    ## 31     meat   October    27
    ## 32  produce   October    53
    ## 33     deli   October    17
    ## 34     meat September    28
    ## 35  produce September    55
    ## 36     deli September    16

As you can see here the new variable `Month` now hosts the name of the months and the new variable `Sales` has the sales volumes corresponding to each month and category. As the result of this code, the dataset became a little longer.

Notice how the new variable `Month` has the content sorted alphabetically. We will change this later.

Also notice that each month name is repeated three times in the Month variable to account for sales volumes for each department. However, you may prefer to have a *clean* variable `Month`, where each month name is mentioned only once. In order to achieve this, you should break the category variable into three new categories so that for each observation *Month* you will see the sales volume for `meat`, `produce` and `deli` under three different variables. Obviously you will not need the `Sales` variable after that. Next we will work with another function to achieve this.

### Long to Wide

Assume you want to make the dataset a little wider by breaking the first variable into two new variables; `Produce` and `Meat`. Also, for the content of the two new variables, we will be using the content of variable `Sales`. Therefore, `Sales` will also be obsolete and should be eliminated. We are going to use the function `spread()` from the `tidyr` package. Here is the code to do that.

``` r
sales3 <- tidyr::spread(sales2, "Category", "Sales")
sales3
```

    ##        Month deli meat produce
    ## 1      April   15   28      49
    ## 2     August   16   29      57
    ## 3   December   15   31      48
    ## 4   February   17   31      52
    ## 5    January   16   28      45
    ## 6       July   18   32      55
    ## 7       June   16   32      54
    ## 8      March   17   26      51
    ## 9        May   16   33      52
    ## 10  November   17   30      49
    ## 11   October   17   27      53
    ## 12 September   16   28      55

Notice how sales volumes are now stated separately under the three new variables `Produce`, `Meat` and `deli`. Both variables `Category` and `Sales` have been dropped. Now each month name is a separate observation for this dataset. As a result of this, the dataset became a little wider.

Since each month name is an observation, and this was a time-series to begin with, we would like to sort the dataset based on the month name so that it starts with January and ends with December. Also, let's re-order the columns so that `produce` is first, followed by `meat` and `deli`. Below see the sorted dataset.

    ##        Month produce meat deli
    ## 1    January      45   28   16
    ## 2   February      52   31   17
    ## 3      March      51   26   17
    ## 4      April      49   28   15
    ## 5        May      52   33   16
    ## 6       June      54   32   16
    ## 7       July      55   32   18
    ## 8     August      57   29   16
    ## 9  September      55   28   16
    ## 10   October      53   27   17
    ## 11  November      49   30   17
    ## 12  December      48   31   15

There is much more to cleaning data and the `tidyr` package in particular. For an overview check out this [link](https://www.rdocumentation.org/packages/tidyr/versions/0.8.3)!

Happy Sunday everyone :)
