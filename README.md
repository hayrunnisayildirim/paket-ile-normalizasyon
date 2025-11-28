# paket-ile-normalizasyon
#5. hafta veri madenciligi paket kullanarak normalizasyon

#veri setinde bulunan ve numerik deger alan nitelikler normalize edilir.
#Normallestirme teknikleri, degiskenlerin olcegini kucultmemizi saglar 
#boylece verilerin istatistiksel dagilimini olumlu yonde etkiler.
#caret paketi preProcess() 

#R da Kutuphane Paketlerini Kullanarak Normalizasyon

#clusterSim ve caret paketi
#fonksiyon olarak scale

install.packages("clusterSim")
library(clusterSim)
install.packages("caret")
library(caret)

#oncelikle veri setini cagiralim
verisetim=read.table(file.choose(),header=T,sep=";")
str(verisetim)
summary(verisetim)


#clustersim ile min-maks normalizasyon 
# data.Normalization 
# min-maks normalizasyonu icin n4
yasnormalize= data.Normalization (verisetim$yas,type="n4",normalization="column")
tecrubenormalize = data.Normalization (verisetim$tecrube,type="n4",normalization="column")
maasnormalize =data.Normalization (verisetim$maas,type="n4",normalization="column")

#clusterSim ile zscore normalizasyon

yaszscore <- data.Normalization (verisetim$yas,type="n1",normalization="column")
tecrubezscore <- data.Normalization (verisetim$tecrube,type="n1",normalization="column")
maaszscore <- data.Normalization (verisetim$maas,type="n1",normalization="column")

data.frame(verisetim$yas, yasnormalize, yaszscore)


install.packages("caret")
library(caret)
#caret paketinde preProcess fonksiyonu kullanilir
# preProcess min maks icin, scale zscore icin


#min-maks
caretegoreminmaksyas <- preProcess(as.data.frame(verisetim$yas), method = c("range"))
#ayri bir basliga atiyalim normalize yas olarak
normalizeyas <- predict(caretegoreminmaksyas,as.data.frame(verisetim$yas))

#zscore icin scale fonksiyonu kullanimi

yaszscorenormalize <- as.data.frame(scale(verisetim$yas)) 
yaszscorenormalize

tecrubenormalize <- as.data.frame(scale(verisetim$tecrube))
tecrubenormalize

maasnormalize <- as.data.frame(scale(verisetim$maas))
maasnormalize

data("Orange")
str(Orange)
summary(Orange)

#age ve circumference

#min-maks n4
minmaks_age <- data.Normalization (Orange$age,type="n4",normalization="column")
minmaks_circumference <- data.Normalization (Orange$circumference,type="n4",normalization="column")


#zscore n1
zscore_age <- data.Normalization (Orange$age,type="n1",normalization="column")
zscore_circumference <- data.Normalization (Orange$circumference,type="n1",normalization="column")



#sutun kaldirmak icin
Orange$Tree <- NULL
# sutun kaldirmak icin
data("Orange")
str(Orange)

Orange <- Orange[ ,-1]

# hepsini tek seferde yapmak icin
attach(Orange)
Orangenormalize <- scale(Orange)
