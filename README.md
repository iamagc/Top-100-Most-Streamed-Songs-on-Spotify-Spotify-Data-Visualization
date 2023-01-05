# Top-100-Most-Streamed-Songs-on-Spotify-Spotify-Data-Visualization


## Data

The 100 most streamed songs in the world between 1975 and 2021 by Spotify. This dataset has several variables related to songs. In this study, the Spotify dataset was examined with data visualization methods. Our dataset has 100 songs and 14 variables.

In this project,

• The popularity variable was compared with six different variables using Scatterplot.

• The intersection of popularity, bpm and energy variables was compared with the Upset plot.

• The correlation relationship between six variables was examined.

• The popularity of the 10 most popular artists is compared.

• The three highest types, the popularity-energy relationship, were visualized.

• The bpm of the three highest species were compared.


## Packages 

```
# Install Packages 

install.packages("readr")
install.packages("MASS")
install.packages("dplyr")
install.packages("ggplot2")
install.packages("hrbrthemes")
install.packages("corrplot")
install.packages("gridExtra")


library(readr)
library(MASS)
library(dplyr)
library(ggplot2)
library(hrbrthemes)
library(corrplot)
library(gridExtra)

spotify <- read.csv("C:/Users/ahmet/Desktop/spotify.csv",sep=",")

spotify_dataframe<-data.frame(spotify)
head(spotify_dataframe)
```


## Figures

### Figure 1: The correlation relationship between six variables was examined.

```
bpm<-spotify_dataframe$beats.per.minute
year<-spotify_dataframe$year
acousticness<-spotify_dataframe$acousticness
energy<-spotify_dataframe$energy
popularity<-spotify_dataframe$popularity
loudness.dB<-spotify_dataframe$loudness.dB


#Let's import numeric variables into a new dataframe

new_spo_dataset<-data.frame(bpm,year,acousticness,energy
                            ,popularity,loudness.dB)

#Let's plot correlation plot

#https://cran.r-project.org/web/packages/corrplot/vignettes/corrplot-intro.html
par(mfrow = c(2, 2))

corrplott1<-corrplot(new_spo_dataset.cor, method = 'number', order = 'AOE',col=colorRampPalette(c("blue","white","red"))(200))

corrplott2<-corrplot(new_spo_dataset.cor, method = 'color', order = 'AOE')

grid.arrange( corrplott1,corrplott2,ncol=2,top="Main Title")

#Heatmap

heatmap(new_spo_dataset.cor)
```

![](https://github.com/iamagc/Top-100-Most-Streamed-Songs-on-Spotify-Spotify-Data-Visualization/blob/main/plots/1.png)


### Figure 2: The popularity variable was compared with six different variables using Scatterplot.

```
bpm<-spotify_dataframe$beats.per.minute
year<-spotify_dataframe$year
acousticness<-spotify_dataframe$acousticness
energy<-spotify_dataframe$energy
popularity<-spotify_dataframe$popularity
loudness.dB<-spotify_dataframe$loudness.dB
danceability<-spotify_dataframe$danceability
liveness<-spotify_dataframe$liveness
valance<-spotify_dataframe$valance
speechiness<-spotify_dataframe$speechiness

#Should be seen as par(mfrow = c(3, 3))

par(mfrow = c(2, 3))

plott1<-ggplot(spotify_dataframe, aes(x=energy, y=popularity))  + 
  geom_point(shape=18, color="royalblue4")+
  geom_smooth(method=lm, se=FALSE, fullrange=TRUE)

plott2<-ggplot(spotify_dataframe, aes(x=acousticness, y=popularity))  + 
  geom_point(shape=18, color="royalblue4")+
  geom_smooth(method=lm, se=FALSE, fullrange=TRUE)

plott3<-ggplot(spotify_dataframe, aes(x=danceability, y=popularity))  + 
  geom_point(shape=18, color="royalblue4")+
  geom_smooth(method=lm, se=FALSE, fullrange=TRUE)

plott4<-ggplot(spotify_dataframe, aes(x=loudness.dB , y=popularity))  + 
  geom_point(shape=18, color="royalblue4")+
  geom_smooth(method=lm, se=FALSE, fullrange=TRUE)

plott5<-ggplot(spotify_dataframe, aes(x=liveness, y=popularity ))  + 
  geom_point(shape=18, color="royalblue4")+
  geom_smooth(method=lm, se=FALSE, fullrange=TRUE)

plott6<-ggplot(spotify_dataframe, aes(x=valance, y=popularity))  + 
  geom_point(shape=18, color="royalblue4")+
  geom_smooth(method=lm, se=FALSE, fullrange=TRUE)

grid.arrange( plott1, plott2, plott3,plott4, plott5, plott6,ncol=3,top="Popularity vs Another Variables")

plott7<-ggplot(spotify_dataframe, aes(x=energy, y=popularity))  + 
  geom_point(shape=18,color="royalblue4")+
  geom_smooth(method=lm, se=FALSE, fullrange=TRUE)

plott8<-ggplot(spotify_dataframe, aes(x=acousticness, y=popularity))  + 
  geom_point(shape=18, color="royalblue4")+
  geom_smooth(method=lm, se=FALSE, fullrange=TRUE)

plott9<-ggplot(spotify_dataframe, aes(x=speechiness, y=popularity))  + 
  geom_point(shape=18, color="royalblue4")+
  geom_smooth(method=lm, se=FALSE, fullrange=TRUE)
  
```

![](https://github.com/iamagc/Top-100-Most-Streamed-Songs-on-Spotify-Spotify-Data-Visualization/blob/main/plots/2.png)


### Figure 3: The intersection of popularity, bpm and energy variables was compared with the Upset plot.

```
install.packages("UpsetR")
library(UpSetR)

energy<-spotify_dataframe$energy
popularity<-spotify_dataframe$popularity
loudness.dB<-spotify_dataframe$loudness.dB
top.genre<-spotify_dataframe$top.genre
bpm<-spotify_dataframe$beats.per.minute
listInput <- list(one = energy, two = popularity, three = bpm)
names(listInput) = c("energy", " popularity", " bpm")

upset(fromList(listInput), order.by = "freq",sets.bar.color=c("maroon","blue","orange"), matrix.color="blue")

```

![](https://github.com/iamagc/Top-100-Most-Streamed-Songs-on-Spotify-Spotify-Data-Visualization/blob/main/plots/3.png)

### Figure 4: The popularity of the 10 most popular artists is compared.

```
ggplot(selecteddata1, aes(x = reorder(artist, -popularity), y = popularity)) +
  geom_segment(aes(x = reorder(artist, -popularity),
                   xend = reorder(artist, -popularity),
                   y = 0, yend = popularity),
               color = "gray", lwd = 1) +
  geom_point(size = 4, pch = 21, bg = 4, col = 1) +
  xlab("Artist") +
  ylab("Popularity") +
  coord_flip() +
  theme_minimal()+
  labs(title="The Most Popular 10 Artists", 
       subtitle="", 
       caption="Source: Spotify Dataset") + 
  theme(axis.text.x = element_text(angle=65, vjust=0.6))

```

![](https://github.com/iamagc/Top-100-Most-Streamed-Songs-on-Spotify-Spotify-Data-Visualization/blob/main/plots/4.png)




