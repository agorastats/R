# Sample document



## Iris data set


```r
## Look famous iris data set with  ==> ?iris

## make descriptive
summary(iris)
```

```
##   Sepal.Length    Sepal.Width     Petal.Length    Petal.Width   
##  Min.   :4.300   Min.   :2.000   Min.   :1.000   Min.   :0.100  
##  1st Qu.:5.100   1st Qu.:2.800   1st Qu.:1.600   1st Qu.:0.300  
##  Median :5.800   Median :3.000   Median :4.350   Median :1.300  
##  Mean   :5.843   Mean   :3.057   Mean   :3.758   Mean   :1.199  
##  3rd Qu.:6.400   3rd Qu.:3.300   3rd Qu.:5.100   3rd Qu.:1.800  
##  Max.   :7.900   Max.   :4.400   Max.   :6.900   Max.   :2.500  
##        Species  
##  setosa    :50  
##  versicolor:50  
##  virginica :50  
##                 
##                 
## 
```

```r
#using dplyr()
library(dplyr)

## mean of sepal information
iris %>% select(contains("Sepal")) %>% summarise_if(is.numeric,funs(mean=mean)) %>%
round(3) %>% DT::datatable(options = list(dom='t')) 
```

<!--html_preserve--><div id="htmlwidget-4cedd51353f58021129b" style="width:100%;height:auto;" class="datatables html-widget"></div>
<script type="application/json" data-for="htmlwidget-4cedd51353f58021129b">{"x":{"filter":"none","data":[["1"],[5.843],[3.057]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th> <\/th>\n      <th>Sepal.Length_mean<\/th>\n      <th>Sepal.Width_mean<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"dom":"t","columnDefs":[{"className":"dt-right","targets":[1,2]},{"orderable":false,"targets":0}],"order":[],"autoWidth":false,"orderClasses":false}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

```r
# mean of Sepal information by Species
iris %>%   group_by(Species) %>% select(contains("Sepal"))  %>%   summarise_if(is.numeric,funs(mean = mean)) %>%
DT::datatable(options = list(dom='t')) 
```

<!--html_preserve--><div id="htmlwidget-d98a8954e9867c609d3b" style="width:100%;height:auto;" class="datatables html-widget"></div>
<script type="application/json" data-for="htmlwidget-d98a8954e9867c609d3b">{"x":{"filter":"none","data":[["1","2","3"],["setosa","versicolor","virginica"],[5.006,5.936,6.588],[3.428,2.77,2.974]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th> <\/th>\n      <th>Species<\/th>\n      <th>Sepal.Length_mean<\/th>\n      <th>Sepal.Width_mean<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"dom":"t","columnDefs":[{"className":"dt-right","targets":[2,3]},{"orderable":false,"targets":0}],"order":[],"autoWidth":false,"orderClasses":false}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

## K-Means Clustering

```r
## make kmeans with petal information
km=kmeans(x=iris[,c("Petal.Length","Petal.Width")],centers = 3,nstart = 10)
```

## Profile of 3 clusters


```r
table(iris$Species,km$cluster)
```

```
##             
##               1  2  3
##   setosa     50  0  0
##   versicolor  0 48  2
##   virginica   0  4 46
```



## Plot kmeans

```r
library(ggplot2)
library(dplyr)

attach(iris)
iris %>% ggplot(aes(x=Petal.Length, y=Petal.Width, color=km$cluster )) + 
 geom_point(show.legend = FALSE)
```

![](iris_markdown_files/figure-html/unnamed-chunk-2-1.png)<!-- -->

