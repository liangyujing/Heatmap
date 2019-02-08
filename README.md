
rm(list=ls())

# Set your working dir as the current dir
setwd(dirname(rstudioapi::getSourceEditorContext()$path))
my_data <- read.csv(file ="R code/regression-assignments 1+ 2/ExperienceSampling_Group7.csv", head=T,sep=";") 



## 1. scale: standardizing the data to make variables comparable.
#scale: a character indicating if the values should be centered and scaled in either the row direction or the column direction, or none. 
#Allowed values are in c(“row”, “column”, “none”). Default is “row”.

df <- scale(my_data)


## 2.basic heatmap
heatmap(df, scale = "row")

# Default plot
heatmap(df, scale = "none")
##In the plot above, high values are in red and low values are in yellow.


## 3.Pretty heat maps: pheatmap()
library("pheatmap")
pheatmap(df, cutree_rows = 4)
##The pheatmap() function, creates pretty heatmaps, 
##where ones has better control over some graphical parameters such as cell size.


## 4.Interactive heat maps: d3heatmap()
library("d3heatmap")
d3heatmap(scale(my_data), colors = "RdYlBu",
          k_row = 4, # Number of groups in rows
          k_col = 2 # Number of groups in columns
)
##放鼠标上去可以显示具体


## 5.重要：density! Visualizing the distribution of columns in matrix
## 2density plot: the color represents distribution of the points in the plane

require(MASS)
dens<-kde2d(x=my_data$beepnum, y=my_data$PA, h=75, n=50)
filled.contour(dens)

##h is the bandwidth which controls the smoothness of the plot - you don't have to specify it, but I did. 
##Play with it to see its effect. n is the number of grid points for the output, a large number gives a higher resolution for the contour plot.

