# practica-12
desocupación


#reales
plot(window(tdesoc,start = 2005, end=2015), ylab ="Tasa de desocupacion", xlab="Año", main = "Tasa de desocupacion", col="red", type="b", pch=8)

#reales hasta 2010
plot(window(tdesoc,start = 2005, end=2010), ylab ="Desocupacion", xlab="Año", main = "Tasa de desocupación", col="red", type="b", pch=8)

#cortamos
desocupación
desc<-desocupación[1:24,]
desc

tdesoc<-ts(desc, frequency= 4, start=2005)
tdesoc
installed.packages("forecast")
require(forecast)

#*********************
########INGENUO######
#*********************

desm1<- naive (tdesoc, h=20) 
#*********************
########PROMEDIO######
#*********************

desm2<- meanf(tdesoc, h=20)
#*******************************
########INGENUO ESTACIONAL######
#*******************************

desm3<- snaive (tdesoc, h=20)
plot(desm3)
#*******************
########DERIVA######
#*******************

desm4<- rwf(tdesoc, h=20, drift=TRUE)

x11()
plot(desm2, main="Pronostico de desocupacion trimestral")
lines(desm1$mean, col=5)##mean=pronostico
lines(desm3$mean, col=6)
lines(desm4$mean, col=7)
legend("topleft", lty=1, col=c(5,6,7),
       legend=c("media", "ingenuo", "ingenuo estacional", "deriva"))


