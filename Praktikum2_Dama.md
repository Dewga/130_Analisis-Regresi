Anreg
================
Dama
2026-02-04

# Input Data

Jika data berupa csv, maka tidak perlu pemanggilan `library(readxl)`
karena R sudah memiliki fungsi bawaan terhadap hal tersebut. Apabila
file .csv pada software excel ditunjukkan dengan delimiter “,” maka
dapat menggunakan fungsi `read.csv`, apabila delimiter berupa “;” maka
dapat menggunakan fungsi `read.csv2`.

``` r
library(readxl)
library(ggplot2)

data_anreg <- data.frame(read_excel("C:\\Users\\USER\\Documents\\A MATKUL IPB/Semester 4/Anreg/Bahan data/NSC-2025.xlsx"))

colnames(data_anreg) <- c("Kabupaten/Kota", "Y", paste0("X", 1:9))
head(data_anreg)
```

    ##         Kabupaten/Kota     Y    X1       X2    X3    X4    X5   X6    X7    X8
    ## 1     Kepulauan Seribu 76.69  9.26   3268.5 13.03 89.10  4.06 0.37 93.62 72.58
    ## 2 Kota Jakarta Selatan 87.57 11.95 500422.7  3.03 92.61  1.38 3.74 97.30 64.81
    ## 3   Kota Jakarta Timur 84.76 11.99 362068.1  4.09 97.15 26.73 2.13 95.90 64.49
    ## 4   Kota Jakarta Pusat 83.75 11.61 532606.9  4.63 90.30  0.84 0.01 96.24 65.12
    ## 5   Kota Jakarta Barat 84.40 11.24 383113.1  3.94 94.94  5.30 2.16 95.66 64.12
    ## 6   Kota Jakarta Utara 82.13 10.85 380461.1  6.44 91.39 30.31 0.52 94.43 67.77
    ##     X9
    ## 1 7.93
    ## 2 5.22
    ## 3 6.95
    ## 4 6.24
    ## 5 6.18
    ## 6 6.18

# Eksplorasi

## Informasi Data

``` r
str(data_anreg)
```

    ## 'data.frame':    119 obs. of  11 variables:
    ##  $ Kabupaten/Kota: chr  "Kepulauan Seribu" "Kota Jakarta Selatan" "Kota Jakarta Timur" "Kota Jakarta Pusat" ...
    ##  $ Y             : num  76.7 87.6 84.8 83.8 84.4 ...
    ##  $ X1            : num  9.26 11.95 11.99 11.61 11.24 ...
    ##  $ X2            : num  3268 500423 362068 532607 383113 ...
    ##  $ X3            : num  13.03 3.03 4.09 4.63 3.94 ...
    ##  $ X4            : num  89.1 92.6 97.2 90.3 94.9 ...
    ##  $ X5            : num  4.06 1.38 26.73 0.84 5.3 ...
    ##  $ X6            : num  0.37 3.74 2.13 0.01 2.16 0.52 3.94 7.72 5.48 6.21 ...
    ##  $ X7            : num  93.6 97.3 95.9 96.2 95.7 ...
    ##  $ X8            : num  72.6 64.8 64.5 65.1 64.1 ...
    ##  $ X9            : num  7.93 5.22 6.95 6.24 6.18 6.18 7.34 7.11 5.99 6.36 ...

``` r
summary(data_anreg)
```

    ##  Kabupaten/Kota           Y               X1               X2        
    ##  Length:119         Min.   :66.72   Min.   : 5.080   Min.   :  3268  
    ##  Class :character   1st Qu.:71.91   1st Qu.: 7.735   1st Qu.: 17677  
    ##  Mode  :character   Median :74.57   Median : 8.330   Median : 28880  
    ##                     Mean   :75.75   Mean   : 8.832   Mean   : 64614  
    ##                     3rd Qu.:78.86   3rd Qu.:10.020   3rd Qu.: 63076  
    ##                     Max.   :89.10   Max.   :12.120   Max.   :532607  
    ##        X3               X4              X5              X6        
    ##  Min.   : 2.340   Min.   :45.88   Min.   : 0.84   Min.   :-1.130  
    ##  1st Qu.: 6.380   1st Qu.:82.23   1st Qu.:10.20   1st Qu.: 3.485  
    ##  Median : 8.980   Median :88.55   Median :19.86   Median : 5.010  
    ##  Mean   : 9.074   Mean   :84.75   Mean   :24.18   Mean   : 4.823  
    ##  3rd Qu.:11.425   3rd Qu.:95.45   3rd Qu.:32.19   3rd Qu.: 6.320  
    ##  Max.   :20.830   Max.   :99.34   Max.   :79.64   Max.   : 9.570  
    ##        X7              X8              X9       
    ##  Min.   :81.59   Min.   :58.13   Min.   :1.560  
    ##  1st Qu.:89.28   1st Qu.:67.99   1st Qu.:3.700  
    ##  Median :92.93   Median :71.92   Median :4.910  
    ##  Mean   :92.27   Mean   :71.58   Mean   :5.026  
    ##  3rd Qu.:95.42   3rd Qu.:74.83   3rd Qu.:6.260  
    ##  Max.   :99.25   Max.   :86.62   Max.   :9.180

1.  Menggunakan Package psych.Cara paling populer di kalangan peneliti
    untuk mendapatkan rangkuman lengkap adalah menggunakan fungsi
    describe() dari package psych.

- sd: Standard Deviation.
- var (opsional di versi tertentu): Jika tidak muncul, Anda bisa
  menghitungnya (SD kuadrat).
- skew: Kemiringan data.
- kurtosis: Keruncingan data.
- se: Standard Error.

``` r
library(psych)
describe(data_anreg)
```

    ##                 vars   n     mean        sd   median  trimmed      mad     min
    ## Kabupaten/Kota*    1 119    60.00     34.50    60.00    60.00    44.48    1.00
    ## Y                  2 119    75.75      5.02    74.57    75.40     4.74   66.72
    ## X1                 3 119     8.83      1.64     8.33     8.78     1.44    5.08
    ## X2                 4 119 64614.02 100110.46 28879.68 40045.02 19694.38 3268.50
    ## X3                 5 119     9.07      3.72     8.98     8.87     3.75    2.34
    ## X4                 6 119    84.75     13.43    88.55    86.72    10.14   45.88
    ## X5                 7 119    24.18     17.31    19.86    22.05    15.18    0.84
    ## X6                 8 119     4.82      2.17     5.01     4.88     2.13   -1.13
    ## X7                 9 119    92.27      3.83    92.93    92.49     4.34   81.59
    ## X8                10 119    71.58      4.67    71.92    71.61     5.10   58.13
    ## X9                11 119     5.03      1.80     4.91     4.98     1.90    1.56
    ##                       max     range  skew kurtosis      se
    ## Kabupaten/Kota*    119.00    118.00  0.00    -1.23    3.16
    ## Y                   89.10     22.38  0.64    -0.52    0.46
    ## X1                  12.12      7.04  0.38    -0.82    0.15
    ## X2              532606.90 529338.40  3.07     9.40 9177.11
    ## X3                  20.83     18.49  0.50    -0.01    0.34
    ## X4                  99.34     53.46 -1.20     0.48    1.23
    ## X5                  79.64     78.80  1.15     1.02    1.59
    ## X6                   9.57     10.70 -0.23    -0.15    0.20
    ## X7                  99.25     17.66 -0.58    -0.37    0.35
    ## X8                  86.62     28.49 -0.01     0.09    0.43
    ## X9                   9.18      7.62  0.24    -0.71    0.16

2.  Menggunakan Package skimr.

Kelebihan skimr:

- Memisahkan rangkuman antara kolom teks dan kolom angka.
- Menampilkan jumlah NA secara jelas.
- Menampilkan SD secara otomatis.
- Ada histogram mini yang menunjukkan distribusi data (apakah data Anda
  menumpuk di angka tinggi atau rendah).

``` r
library(skimr)
skim(data_anreg)
```

|                                                  |            |
|:-------------------------------------------------|:-----------|
| Name                                             | data_anreg |
| Number of rows                                   | 119        |
| Number of columns                                | 11         |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_   |            |
| Column type frequency:                           |            |
| character                                        | 1          |
| numeric                                          | 10         |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |            |
| Group variables                                  | None       |

Data summary

**Variable type: character**

| skim_variable  | n_missing | complete_rate | min | max | empty | n_unique | whitespace |
|:---------------|----------:|--------------:|----:|----:|------:|---------:|-----------:|
| Kabupaten/Kota |         0 |             1 |   4 |  22 |     0 |      119 |          0 |

**Variable type: numeric**

| skim_variable | n_missing | complete_rate | mean | sd | p0 | p25 | p50 | p75 | p100 | hist |
|:---|---:|---:|---:|---:|---:|---:|---:|---:|---:|:---|
| Y | 0 | 1 | 75.75 | 5.02 | 66.72 | 71.90 | 74.57 | 78.87 | 89.10 | ▃▇▃▃▁ |
| X1 | 0 | 1 | 8.83 | 1.64 | 5.08 | 7.74 | 8.33 | 10.02 | 12.12 | ▁▇▇▃▅ |
| X2 | 0 | 1 | 64614.02 | 100110.46 | 3268.50 | 17676.55 | 28879.68 | 63076.26 | 532606.90 | ▇▁▁▁▁ |
| X3 | 0 | 1 | 9.07 | 3.72 | 2.34 | 6.38 | 8.98 | 11.43 | 20.83 | ▃▇▅▂▁ |
| X4 | 0 | 1 | 84.75 | 13.43 | 45.88 | 82.23 | 88.55 | 95.46 | 99.34 | ▁▁▂▅▇ |
| X5 | 0 | 1 | 24.18 | 17.31 | 0.84 | 10.20 | 19.86 | 32.19 | 79.64 | ▇▇▃▂▁ |
| X6 | 0 | 1 | 4.82 | 2.17 | -1.13 | 3.48 | 5.01 | 6.32 | 9.57 | ▂▃▇▇▃ |
| X7 | 0 | 1 | 92.27 | 3.83 | 81.59 | 89.28 | 92.93 | 95.41 | 99.25 | ▁▅▃▇▅ |
| X8 | 0 | 1 | 71.58 | 4.67 | 58.13 | 67.99 | 71.92 | 74.84 | 86.62 | ▁▆▇▅▁ |
| X9 | 0 | 1 | 5.03 | 1.80 | 1.56 | 3.70 | 4.91 | 6.26 | 9.18 | ▂▇▅▅▂ |

## Data NA

``` r
library(dplyr)
library(tidyr)
colSums(is.na(data_anreg))
```

    ## Kabupaten/Kota              Y             X1             X2             X3 
    ##              0              0              0              0              0 
    ##             X4             X5             X6             X7             X8 
    ##              0              0              0              0              0 
    ##             X9 
    ##              0

DISINI TERLIHAT ADA DATA **na** di Kolom X1-X7

Menghapus semua baris yang punya minimal satu NA

``` r
# Menghapus semua baris yang punya minimal satu NA
data_bersih_anreg = na.omit(data_anreg)
summary(data_bersih_anreg)
```

    ##  Kabupaten/Kota           Y               X1               X2        
    ##  Length:119         Min.   :66.72   Min.   : 5.080   Min.   :  3268  
    ##  Class :character   1st Qu.:71.91   1st Qu.: 7.735   1st Qu.: 17677  
    ##  Mode  :character   Median :74.57   Median : 8.330   Median : 28880  
    ##                     Mean   :75.75   Mean   : 8.832   Mean   : 64614  
    ##                     3rd Qu.:78.86   3rd Qu.:10.020   3rd Qu.: 63076  
    ##                     Max.   :89.10   Max.   :12.120   Max.   :532607  
    ##        X3               X4              X5              X6        
    ##  Min.   : 2.340   Min.   :45.88   Min.   : 0.84   Min.   :-1.130  
    ##  1st Qu.: 6.380   1st Qu.:82.23   1st Qu.:10.20   1st Qu.: 3.485  
    ##  Median : 8.980   Median :88.55   Median :19.86   Median : 5.010  
    ##  Mean   : 9.074   Mean   :84.75   Mean   :24.18   Mean   : 4.823  
    ##  3rd Qu.:11.425   3rd Qu.:95.45   3rd Qu.:32.19   3rd Qu.: 6.320  
    ##  Max.   :20.830   Max.   :99.34   Max.   :79.64   Max.   : 9.570  
    ##        X7              X8              X9       
    ##  Min.   :81.59   Min.   :58.13   Min.   :1.560  
    ##  1st Qu.:89.28   1st Qu.:67.99   1st Qu.:3.700  
    ##  Median :92.93   Median :71.92   Median :4.910  
    ##  Mean   :92.27   Mean   :71.58   Mean   :5.026  
    ##  3rd Qu.:95.42   3rd Qu.:74.83   3rd Qu.:6.260  
    ##  Max.   :99.25   Max.   :86.62   Max.   :9.180

# Pembentukan Model

``` r
y = data_bersih_anreg$Y
x = data_bersih_anreg$X9
n <- nrow(data_bersih_anreg)
```

``` r
b1 = (sum(x*y)-sum(x)*sum(y)/n)/(sum(x^2)-(sum(x)^2/n))
b0 <- mean(y)-b1*mean(x)

cat("Koefisien b0:", b0, "\n")  
```

    ## Koefisien b0: 73.49741

``` r
cat("Koefisien b1:", b1, "\n")
```

    ## Koefisien b1: 0.4473984

## Standar Error Parameter Regresi

Standar error menunjukan seberapa besar ketidakpastian dalam estimasi
koefisien

``` r
galat <- y-(b0+b1*x)
ragam_galat <- sum(galat^2)/(n-2)

se_b0 <- sqrt(ragam_galat*(1/n+mean(x)^2/sum((x-mean(x))^2)))
se_b1 <- sqrt(ragam_galat/sum((x-mean(x))^2))

cat("Standar error b0:", se_b0, "\n") 
```

    ## Standar error b0: 1.357898

``` r
cat("Standar error b1:", se_b1, "\n")
```

    ## Standar error b1: 0.2544849

## Signifikansi Parameter (nilai-t)

Nilai ini menunjukkan tingkat signifikansi secara parsial dari setiap
koefisien peubah berdasarkan nilai t dan probabilitas nilai p

``` r
t_b0 <- b0/se_b0
t_b1 <- b1/se_b1
p_b0 <- 2*pt(-abs(t_b0 ),df<-n-2)
p_b1 <- 2*pt(-abs(t_b1 ),df<-n-2)

cat("Nilai t pada b0 adalah", t_b0, "dengan nilai p sebesar", p_b0, "\n")  
```

    ## Nilai t pada b0 adalah 54.12587 dengan nilai p sebesar 1.150449e-84

``` r
cat("Nilai t pada b1 adalah", t_b1, "dengan nilai p sebesar", p_b1, "\n") 
```

    ## Nilai t pada b1 adalah 1.758055 dengan nilai p sebesar 0.08135316

Nilai p kurang dari alpha 0.05 untuk b0 maupun b1 sehingga signifikan
pada taraf nyata 5%

## Koefisien Determinasi dan Penyesuaiannya

Pada analisis regresi linier sederhana, koefisien determinasi yang
digunakan adalah multiple R Squared, sedangkan regresi linier berganda
menggunakan adjusted R Squared yang disesuaikan dengan banyaknya peubah

``` r
r <- (sum(x*y)-sum(x)*sum(y)/n)/
sqrt((sum(x^2)-(sum(x)^2/n))*(sum(y^2)-(sum(y)^2/n)))
Koef_det <- r^2
Koef_det
```

    ## [1] 0.02573685

``` r
Adj_R2 <- 1-((1-Koef_det)*(n-1)/(n-1-1))
Adj_R2
```

    ## [1] 0.01740982

## Signifikansi Simultan (F)

Nilai ini menunjukkan signifikansi dan kebaikan model secara simultan
(bersamaan seluruh peubah) yang menjelaskan model secara keseluruhan
memiliki hubungan berarti antara X dan Y

``` r
galat<-y-(b0+b1*x)

JKG <- sum((y - (b0+b1*x))^2)
JKReg <- sum(((b0+b1*x)- mean(y))^2)
JKT <- sum((y - mean(y))^2)
JKT <- JKReg+JKG

dbReg <- 1
dbg <- n-2
dbt <- n-1

(Fhit <- (JKReg/dbReg)/(JKG/dbg))
```

    ## [1] 3.090758

``` r
(p_Fhit <- 1-pf(Fhit, dbReg, dbg, lower.tail = F))
```

    ## [1] 0.9186468

Nilai p kurang dari alpha 0.05 sehingga secara simultan X dan Y saling
memengaruhi

## Menggunakan Fungsi `lm()`

Dalam penggunaan fungsi `lm()`, kita akan memperoleh secara langsung
nilai-nilai pada pemodelan regresi dari data yang kita miliki. Hanya
dengan mengeluarkan summary dan anova dari model yang terbentuk maka
dapat diperoleh nilai parameter, signifikansinya, standar eror,
koefisien determinasi hingga ukuran keragamannya.

``` r
model <- lm(Y~X1, data = data_anreg)
summary(model)
```

    ## 
    ## Call:
    ## lm(formula = Y ~ X1, data = data_anreg)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -4.3344 -0.8075  0.0218  1.0481  3.9020 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept) 50.35333    0.84613   59.51   <2e-16 ***
    ## X1           2.87498    0.09419   30.52   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 1.683 on 117 degrees of freedom
    ## Multiple R-squared:  0.8884, Adjusted R-squared:  0.8875 
    ## F-statistic: 931.6 on 1 and 117 DF,  p-value: < 2.2e-16

Berdasarkan hasil diperoleh bahwa kedua cara valid dan memberikan hasil
yang sama dalam membuat pemodelan regresi linear sederhana.

``` r
anova(model)
```

    ## Analysis of Variance Table
    ## 
    ## Response: Y
    ##            Df  Sum Sq Mean Sq F value    Pr(>F)    
    ## X1          1 2638.28 2638.28   931.6 < 2.2e-16 ***
    ## Residuals 117  331.34    2.83                      
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

# Visualisasi

``` r
boxplot(data_bersih_anreg$Y)
```

![](Praktikum2_Dama_files/figure-gfm/unnamed-chunk-19-1.png)<!-- -->

``` r
boxplot(data_bersih_anreg$X9)
```

![](Praktikum2_Dama_files/figure-gfm/unnamed-chunk-20-1.png)<!-- -->

# Kesimpulan

Model yang terbentuk adalah sebagai berikut:

$$\hat{Y} = 73.49741  + 0.4473984   X_1$$
