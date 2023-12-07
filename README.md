# Current-Topics-in-Ecology

install.packages("sf")
install.packages("rnaturalearth")
library(sf)
library(ggplot2)
library(rnaturalearth)

# IUCN red list, pick a species, draw a map like the one we have drawn in the lecture

# Drawing the distribution map

setwd(choose.dir())
list.files()
Occurence_Data <- read.delim("C:/0102252-200613084148143.csv")
unique(Occurence_Data$year)
unique(Occurence_Data$countryCode)
pip_map <- st_read("C:/data_0.shp")
plot(pip_map, max.plot = 12)
land50 <- ne_download(scale = 50, type="land", category = "physical")

ggplot()+
  geom_polygon(data=land50, aes(x=long, y=lat,group=group),fill="grey70")+
  coord_fixed(xlim=c(-15,50),ylim=c(30,60),1.3)+geom_sf(data = pip_map, fill = "orange")+
  coord_sf(xlim=c(-15,50),ylim=c(30,60),1.3)+
  geom_point(data=Occurence_Data,aes(x=decimalLongitude, y=decimalLatitude,fill=countryCode,size=individualCount),col="black",pch=21)


ggplot()+
  geom_polygon(data=land50, aes(x=long, y=lat,group=group),fill="grey70")+
  geom_sf(data=pip_map,fill="orange3")
  geom_point(data=Occurence_Data,aes(x=decimalLongitude,y=decmaLatitude),col="red")+
  coord_sf(xlim=c(-15,50),ylim=c(30,60),1.3)
  
  
  # R color brewing --> Check that it helps you to determine the color for you!
