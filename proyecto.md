# Análisis de mortalidad por Neumonía en Colombia de 2010 - 2019

## Filtrado de base por Neumonía.



```R
start = Sys.time()
defun <- read.csv("DEFUN.csv")
end = Sys.time()
print(end-start)
```


```R
defun[,names(defun)] <- lapply(defun[,names(defun)],factor)
```


```R
library(tidyverse)
```


```R
#base filtrada por la enfermedad de neumonia.
neumonia <- defun %>% filter(C_BAS1 == "J189")
```

## Lectura de base de datos de neumonia 


```R
neumonia <- read.csv("neumo.csv", skipNul = 1)
```


```R
neumonia[,names(neumonia)] <- lapply(neumonia[,names(neumonia)],factor)
```

## Serie de tiempo univariada muertes por 1000


```R
freq_neumo <- as.data.frame(table(neumonia$MES,neumonia$ANO))
freq_neumo$tasa <- freq_neumo$Freq/1000
```


```R
time_neumo <- ts(freq_neumo$tasa,freq = 12, start = c(2010,1))
plot(time_neumo)
```


![png](output_11_0.png)

