# statswithR
library(pacman)
library(rio)
library(tidyverse)
install.packages("wesanderson")
library(wesanderson)

install.packages("viridis")
library(viridis)
data <- import("figure.csv")

head(data)

library(ggplot2)
library(janitor)
install.packages("plyr")
library(plyr)

View(data)


image <- ggplot(data, aes(x=as.factor(category), y=percent, fill=type )) + 
  geom_bar(stat = "identity") +
             theme(axis.title.y=element_blank(),
                           axis.text.y=element_blank(),
                           axis.ticks.y=element_blank())

##customize order of columns
positions <- c("Low income","Lower middle income","Upper middle income","High income","World")

##use scale function to change order in graph
image +
  scale_x_discrete(limits = positions)


##change labels

image +
  scale_x_discrete(limits = positions) +
  labs(title="Percentage of countries with generally available cancer diagnosis and 
treatment services in public sector by World Bank income groups", y="", x="By World Bank income groups", caption="Source of data: canceratlas.cancer.org") +
  scale_fill_viridis(name="", 
                     labels = c("Cancer centre or cancer 
department at tertiary level", 
                                "Cancer surgery", 
                                "Subsidized chemotherapy", 
                                "Pathology services", 
                                "Radiotherapy") , discrete= TRUE) +
  geom_text(aes(label = percent), size = 2.5, hjust = 0.8, vjust = 1.34, position =     "stack")

                       

