Baby-Names
================
Fanyi Zeng
4/23/2022

Data source: <http://hadley.github.io/babynames/>

Data description: year: double, Year of birth sex: character, Binary sex
of the baby name: character, Name of the baby n: integer, Raw count
prop: double, Proportion of total births for that year

``` r
babynames <- readr::read_csv('https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2022/2022-03-22/babynames.csv')
```

    ## Rows: 1924665 Columns: 5

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr (2): sex, name
    ## dbl (3): year, n, prop

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
library(tidyverse)
```

Let’s see the top names of 1880.

For girls, top 10 names were Mary, Anna, Emma, Elizabeth, Minnie,
Margaret, Ida, Alice, Bertha, and Sarah.

For boys, top 10 names were John, William, James, Charles, George,
Frank, Joseph, Thomas, Henry, and Robert.

The most enduring girls’ name from 1880 to 2017 seems to be Emma. Boys’
names are William and James.

``` r
babynames %>%
  filter(year == "1880" & sex == "F") %>%
  arrange(desc(n))
```

    ## # A tibble: 942 x 5
    ##     year sex   name          n   prop
    ##    <dbl> <chr> <chr>     <dbl>  <dbl>
    ##  1  1880 F     Mary       7065 0.0724
    ##  2  1880 F     Anna       2604 0.0267
    ##  3  1880 F     Emma       2003 0.0205
    ##  4  1880 F     Elizabeth  1939 0.0199
    ##  5  1880 F     Minnie     1746 0.0179
    ##  6  1880 F     Margaret   1578 0.0162
    ##  7  1880 F     Ida        1472 0.0151
    ##  8  1880 F     Alice      1414 0.0145
    ##  9  1880 F     Bertha     1320 0.0135
    ## 10  1880 F     Sarah      1288 0.0132
    ## # ... with 932 more rows

``` r
babynames %>%
  filter(year == "1880" & sex == "M") %>%
  arrange(desc(n))
```

    ## # A tibble: 1,058 x 5
    ##     year sex   name        n   prop
    ##    <dbl> <chr> <chr>   <dbl>  <dbl>
    ##  1  1880 M     John     9655 0.0815
    ##  2  1880 M     William  9532 0.0805
    ##  3  1880 M     James    5927 0.0501
    ##  4  1880 M     Charles  5348 0.0452
    ##  5  1880 M     George   5126 0.0433
    ##  6  1880 M     Frank    3242 0.0274
    ##  7  1880 M     Joseph   2632 0.0222
    ##  8  1880 M     Thomas   2534 0.0214
    ##  9  1880 M     Henry    2444 0.0206
    ## 10  1880 M     Robert   2415 0.0204
    ## # ... with 1,048 more rows

Let’s see the top names of 2017.

For girls, top 10 names were Emma, Olivia, Ava, Isabella, Sophia, Mia,
Charlotte, Amelia, Evelyn, and Abigail.

For boys, top 10 names were Liam, Noah, William, James, Logan, Benjamin,
Mason, Elijah, Oliver, and Jacob.

``` r
babynames %>%
  filter(year == "2017" & sex == "F") %>%
  arrange(desc(n))
```

    ## # A tibble: 18,309 x 5
    ##     year sex   name          n    prop
    ##    <dbl> <chr> <chr>     <dbl>   <dbl>
    ##  1  2017 F     Emma      19738 0.0105 
    ##  2  2017 F     Olivia    18632 0.00994
    ##  3  2017 F     Ava       15902 0.00848
    ##  4  2017 F     Isabella  15100 0.00805
    ##  5  2017 F     Sophia    14831 0.00791
    ##  6  2017 F     Mia       13437 0.00717
    ##  7  2017 F     Charlotte 12893 0.00688
    ##  8  2017 F     Amelia    11800 0.00629
    ##  9  2017 F     Evelyn    10675 0.00569
    ## 10  2017 F     Abigail   10551 0.00563
    ## # ... with 18,299 more rows

``` r
babynames %>%
  filter(year == "2017" & sex == "M") %>%
  arrange(desc(n))
```

    ## # A tibble: 14,160 x 5
    ##     year sex   name         n    prop
    ##    <dbl> <chr> <chr>    <dbl>   <dbl>
    ##  1  2017 M     Liam     18728 0.00954
    ##  2  2017 M     Noah     18326 0.00933
    ##  3  2017 M     William  14904 0.00759
    ##  4  2017 M     James    14232 0.00725
    ##  5  2017 M     Logan    13974 0.00712
    ##  6  2017 M     Benjamin 13733 0.00699
    ##  7  2017 M     Mason    13502 0.00688
    ##  8  2017 M     Elijah   13268 0.00676
    ##  9  2017 M     Oliver   13141 0.00669
    ## 10  2017 M     Jacob    13106 0.00668
    ## # ... with 14,150 more rows

The most popular names in 1800, Mary and Anna, largely decreased in
popularity over the years. Emma being an enduring name, was both popular
in 1800 and in 2017; it has experienced a gradual decline since 1800 and
a revival since 2000. Olivia has also gained popularity around the same
time since 2000.

``` r
babynames %>%  
  filter(name == "Mary"|name == "Anna") %>%
  ggplot(aes(x=year, y=prop, color = name)) +
  geom_point() +
  geom_line()
```

![](Baby-Names_files/figure-gfm/girl%20trend-1.png)<!-- -->

``` r
babynames %>%  
  filter(name == "Emma"|name == "Olivia") %>%
  ggplot(aes(x=year, y=prop, color=name)) +
  geom_point() +
  geom_line()
```

![](Baby-Names_files/figure-gfm/girl%20trend-2.png)<!-- -->

Similarly, John and William became less favorable over the years. Liam
became more prevalent around 2000, followed by Noah.

``` r
babynames %>%  
  filter(name == "John"|name == "William") %>%
  ggplot(aes(x=year, y=prop, color = name)) +
  geom_point() +
  geom_line()
```

![](Baby-Names_files/figure-gfm/boy%20trend-1.png)<!-- -->

``` r
babynames %>%  
  filter(name == "Liam"|name == "Noah") %>%
  ggplot(aes(x=year, y=prop, color=name)) +
  geom_point() +
  geom_line()
```

![](Baby-Names_files/figure-gfm/boy%20trend-2.png)<!-- -->

A general trend is that, names that very extremely common (representing
a large %) in 1800 were much less dominant in 2017, perhaps because the
population has grown more and more diverse in terms of national origin,
race/ethnicity, religious belief, etc., which are factors that might
potentially affect how people choose to name their babies.
