# BU8-Growth-Rate


###

#BU8 Growth Rate plot
#Date: 12-2-22

library(tidyverse)
library(ggplot2)
library(dplyr)
library(tidyr)
library(hrbrthemes)



table <- read.table("BU8CSV.csv", h=T, sep=",")

table3 <- table %>% group_by(Isolate, Media) %>% 
  summarise_at(vars(X0, X24, X48, X72, X96, X120, X144), list(mean)) %>%
  tidyr::gather (Time, "Diameter", 3:9)
table3$Time <- gsub("X","",as.character(table3$Time))%>% as.numeric(table3$Time)
ggplot (table3, aes(x=Time, y=Diameter, colour=Isolate, shape=Media)) + geom_line() + geom_point(size=3.5)+ 
  ylab('Diameter (mm)') + ylim(0,90)+ xlab('Time (h)') + xlim(0,144) +
  theme(text = element_text(size = 20), axis.text.x = element_text(size=15))

#add linetype= Media to change pattern of lines (eg dotted)

###
