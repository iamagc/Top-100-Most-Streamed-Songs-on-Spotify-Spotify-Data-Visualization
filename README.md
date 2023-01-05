# Spotify'da En Çok Dinlenen 100 Şarkı Veri Setinin Görselleştirilmesi

Bu proje, Eskişehir Teknik Üniversitesi İstatistik Bölümü lisans programında 2022-2023 Güz döneminde yürütülen Veri Görselleştirme dersi dönem sonu projesi kapsamında yapılmıştır. Spotify tarafından dünyanın en çok dinlenen 100 şarkısı. Bu veri kümesi şarkılarla ilgili çeşitli değişkenlere sahiptir. Bu çalışmada Spotify veri seti veri görselleştirme yöntemleri ile araştırılmıştır. Veri setimizde 100 şarkı ve 14 değişken var.


## Veri Seti

Spotify tarafından 1975 ile 2021 arasında dünyada en çok dinlenen 100 şarkı. Bu veri kümesi şarkılarla ilgili çeşitli değişkenlere sahiptir. Bu çalışmada Spotify veri seti veri görselleştirme yöntemleri ile incelenmiştir. Veri setimizde 100 şarkı ve 14 değişken var.

Bu projede,

• Popülarite değişkeni, Scatterplot kullanılarak altı farklı değişkenle karşılaştırıldı.

• Popülarite, bpm ve enerji değişkenlerinin kesişimi, Upset grafiği ile karşılaştırıldı.

• Altı değişken arasındaki korelasyon ilişkisi incelenmiştir.

• En popüler 10 sanatçının popülaritesi karşılaştırılır.

• En yüksek üç tür olan popülerlik-enerji ilişkisi görselleştirildi.

• En yüksek üç türün bpm'si karşılaştırıldı.


## Paketler

```
# Gerekli paketlerin yüklenmesi ve çağırılması

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


## Şekiller

### Şekil 1: Altı değişken arasındaki korelasyon ilişkisi incelenmiştir.

```
bpm<-spotify_dataframe$beats.per.minute
year<-spotify_dataframe$year
acousticness<-spotify_dataframe$acousticness
energy<-spotify_dataframe$energy
popularity<-spotify_dataframe$popularity
loudness.dB<-spotify_dataframe$loudness.dB


#Sayısal değişkenleri yeni bir veri çerçevesine aktaralım

new_spo_dataset<-data.frame(bpm,year,acousticness,energy
                            ,popularity,loudness.dB)

#Korelasyon grafiğini çizelim

#https://cran.r-project.org/web/packages/corrplot/vignettes/corrplot-intro.html
par(mfrow = c(2, 2))

corrplott1<-corrplot(new_spo_dataset.cor, method = 'number', order = 'AOE',col=colorRampPalette(c("blue","white","red"))(200))

corrplott2<-corrplot(new_spo_dataset.cor, method = 'color', order = 'AOE')

grid.arrange( corrplott1,corrplott2,ncol=2,top="Main Title")

#Sıcaklık haritası

heatmap(new_spo_dataset.cor)
```

![](https://github.com/iamagc/Top-100-Most-Streamed-Songs-on-Spotify-Spotify-Data-Visualization/blob/main/figures/one.png)


Grafiğe baktığımızda en yüksek pozitif ilişkinin enerji ve desibel değişkenleri arasında bulunduğu görülmektedir. Enerji ve akustik değişkenleri arasında ise en yüksek negatif ilişki bulunmaktadır. Ayrıca popülarite- bpm  , yıl - enerji ve bpm - yıl değişkeni ikili olarak kendi içlerinde nötr ilişkiye sahiptir.


### Şekil 2: Popülerlik değişkeni, Scatterplot kullanılarak altı farklı değişkenle karşılaştırılmıştır.

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

#par(mfrow = c(3, 3)) olarak görülmeli

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

![](https://github.com/iamagc/Top-100-Most-Streamed-Songs-on-Spotify-Spotify-Data-Visualization/blob/main/figures/second.png)

Grafiğe baktığımızda,

Enerji arttıkça popülerliğin arttığı yüksek enerji yüksek popülerlik kısmında yoğunlaşma bulunuyor.

Akustik değerinin düşük olduğu kısımlarda popülerliğin yüksek olduğu görülmektedir.

Dans edilebilirlik değeri değişse de popülerlik değeri genellikle 80-90 arasında yoğunlaşmıştır.

Desibel değerinin-7.5 ve -2.5 olduğu yerlerde popülerlik değerlerinin yoğunlaştığı görülmektedir.

Canlılık değerinin 0-20 aralığında popülerlik değerinin 70-90 arasında yoğunlaştığı görülmektedir.

Valans değeri değişse de popülerlik genellikle belirli bir bölgede yoğunlaşmıştır.


### Şekil 3: Popülarite, bpm ve enerji değişkenlerinin kesişimi, Upset grafiğiyle karşılaştırılmıştır.

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

![](https://github.com/iamagc/Top-100-Most-Streamed-Songs-on-Spotify-Spotify-Data-Visualization/blob/main/figures/third.png)


Upset grafiği sayesinde,

Popülerlik, bpm ve enerji değişkenleri arasında kesişim değerinin 9 olduğu

Popülerlik ve enerji değişkenleri arasında kesişim değerinin 9 olduğu

Popülerlik ve bpm değişkenleri arasında kesişim değerinin 1 olduğu 

Enerji ve bpm değişkenleri arasında kesişim değerinin 2 

olduğu görülmektedir

### Şekil 4: En popüler 10 sanatçının popülaritesi karşılaştırılmıştır.

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

![](https://github.com/iamagc/Top-100-Most-Streamed-Songs-on-Spotify-Spotify-Data-Visualization/blob/main/figures/fourth.png)


Grafiğe baktığımızda en popüler 10 sanatçının popülerlik sıralamasını görmekteyiz. Aralarında çok az fark bulunsa da en düşük popülerliğe The Chainsmokers en yüksek popülerliğe ise The Weeknd sahiptir.



