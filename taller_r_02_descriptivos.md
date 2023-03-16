Taller 02
================
dacarras
Thu Mar 16, 2023

# Introducción

- La siguiente tarea contiene una serie de ejercicios en que vamos a
  producir resultados descriptivos.

- Vamos a emplear una copia de los datos del estudio de Poli
  victimizacion de Jovenes, realizada en Chile en Octubre de 2017.

- El link para cargar los datos, es el siguiente

<!-- -->


    'https://github.com/dacarras/psi4035_examples/raw/master/data/data_poly_all.rds'

- **Advertencia**: Los datos originales provienen de una muestra
  probabilística. Este tipo de datos, permite realizar inferencias a la
  población, si la información del diseño es empleada para producir
  estimaciones. En este ejercicio con fines ilustrativos, vamos a
  ignorar este aspecto, y solo vamos a producir resultados descriptivos.

# Referencias

Alvarez, E., Guajardo, H., & Messen, R. (1986). Estudio exploratorio
sobre una escala de autoevaluación para la depresión en niños y
adolescentes. Revista Chilena de Pediatria, 57(1), 21–25.
<https://doi.org/10.4067/s0370-41061986000100003>

Birleson, P., Hudson, I., Buchanan, D. G., & Wolff, S. (1987). Clinical
Evaluation of a Self‐Rating Scale for Depressive Disorder in Childhood
(Depression Self‐Rating Scale). Journal of Child Psychology and
Psychiatry, 28(1), 43–60.
<https://doi.org/10.1111/j.1469-7610.1987.tb00651.x>

Consejo Nacional de la Infancia. (2018). Análisis Multivariable de
Estudio de Polivictimización en Niños, Niñas y Adolescentes realizado
por la Pontificia Universidad Católica de Chile.
<http://biblioteca.digital.gob.cl/handle/123456789/3535>

Denda, K., Kako, Y., Kitagawa, N., & Koyama, T. (2006). Assessment of
depressive symptoms in Japanese school children and adolescents using
the birleson depression self-rating scale. International Journal of
Psychiatry in Medicine, 36(2), 231–241.
<https://doi.org/10.2190/3YCX-H0MT-49DK-C61Q>

MINSAL. (2013). Guía Clínica para el tratamiento de adolescentes de 10 a
14 años con Depresión.
<https://www.guiadisc.com/wp-content/pdfs/guia-clinica-tratamiento-depresion-adolescentes.pdf>

Subsecretaria Prevención del Delito. (2018). Primera Encuesta Nacional
de Polivictimización en Niñas, Niños y Adolescentes: Presentación de
Resultados. - El siguiente documento es una colección breve de funciones
básicas para producir resultados.

- Existen diferentes maneras de producir resultados en r. En este curso,
  emplearemos la generación de resultados mediante códigos
  reproducibles. Es decir, que son códigos que pueden ser ejecutados, y
  debieran producir el mismo resultado en diferentes equipos, y en
  diferentes momentos.

- Para lograr lo anterior, el código escrito debe cumplir ciertas
  características. Una de ellas, es que la secuencia de comandos
  empleados pueda ser ejecutada por un documento dinámico. El presente
  código esta escrito de esta forma. Una vez ejecutado, debiera poder
  ejecutarse completo, y producir un output en html.

- En particular, vamos a revisar diferentes funciones en `R` para abrir
  datos, y para manejar datos. Emplearemos funciones de R base, y de la
  libreria `dplyr`, la cual es una librería muy versatil para el manejo
  de datos (ver *[cheat
  sheet](https://www.rstudio.com/wp-content/uploads/2015/02/data-wrangling-cheatsheet.pdf)*)

# Librerias que vamos a emplear

``` r
#------------------------------------------------------------------------------
# instalar librerias
#------------------------------------------------------------------------------

#----------------------------------------------------------
# librerias
#----------------------------------------------------------

install.packages('tidyverse') # incluye a dplyr y ggplot2
                              # junto a otras librerias útiles

install.packages('dplyr')     # para manejo de datos

install.packages('knitr')     # para mostrar tablas como texto plano

install.packages("moments")   # para obtener asimetria
```

# Ejercicio 1. Abrir datos

## Abrir datos desde url

``` r
#------------------------------------------------------------------------------
# abrir datos desde archivo en una url
#------------------------------------------------------------------------------

#----------------------------------------------------------
# url datos
#----------------------------------------------------------

url_location <- url('https://github.com/dacarras/psi4035_examples/raw/master/data/data_poly_all.rds')

#--------------------------------------
# abrir datos
#--------------------------------------

data_poly <- readRDS(url_location)
```

# Ejercicio 2. Inspeccionar datos

## Vista rápida de datos

``` r
#------------------------------------------------------------------------------
# inspeccionar session
#------------------------------------------------------------------------------

#----------------------------------------------------------
# lista de objetos creados
#----------------------------------------------------------

dplyr::glimpse(data_poly)
```

    ## Rows: 19,684
    ## Columns: 319
    ## $ m16_rbd                    [3m[38;5;246m<dbl>[39m[23m 9071, 9071, 9071, 9071, 9071, 9071, 9071, 9…
    ## $ m17_rbd                    [3m[38;5;246m<dbl>[39m[23m 9071, 9071, 9071, 9071, 9071, 9071, 9071, 9…
    ## $ fuente                     [3m[38;5;246m<chr>[39m[23m "Salida_0", "Salida_0", "Salida_0", "Salida…
    ## $ folio                      [3m[38;5;246m<dbl>[39m[23m 47601, 47602, 47603, 47604, 47605, 47606, 4…
    ## $ P1_1                       [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, …
    ## $ P1_2                       [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 2, 1, 1, 2, 1, 1, 2, 1, 1, 1, 2, …
    ## $ P1_3                       [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 2, 1, 1, 2, 2, 2, 3, 3, 2, 3, …
    ## $ P1_4                       [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ P1_5                       [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  1, NA,  1,  1,  1,  1,  1,  1,…
    ## $ P1_6                       [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 8, 1, …
    ## $ P1_7_1                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  1,  1,  1,  1,  1,  1,  1,  1,…
    ## $ P1_7_2                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  1,  1, NA,  1, NA,  1,  1, NA,…
    ## $ P1_7_3                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  1,  1,  1,  1,  1,  1, NA,  1,…
    ## $ P1_7_4                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ P1_7_5                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA,  1, NA, NA, NA, NA,…
    ## $ P1_7_6                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ P1_7_7                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ P1_7_8                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ P1_8_1                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ P1_8_2                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ P1_8_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ P1_8_4                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ P1_8_5                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ P1_8_6                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  1,  1,  1,  1,  1,  1,  1,  1,…
    ## $ PA_1                       [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 1, 2, 2, 1, 1, 2, 1, 2, 1, 1, …
    ## $ PA_1_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 1, 2, 2, 2, 1, 2, 1, 2, 1, 1, …
    ## $ PA_1_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 2, 1, 1, 1, 2, 1, 2, 1, 2, 4, …
    ## $ PA_1_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA,  3, NA, NA,  2,  4, NA,  2,…
    ## $ PA_1_4                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA,  1, NA, NA,  4,  1, NA,  4,…
    ## $ PA_2                       [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2, NA,  2,  2,  2,  2,  2,  2,…
    ## $ PA_2_1                     [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2, NA,  2,  2,  2,  2,  2,  2,…
    ## $ PA_2_2                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  1, NA,  1,  1,  1,  1,  1,  1,…
    ## $ PA_2_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ PA_2_4                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ PA_3                       [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 2, 2, 2, 1, 2, 1, 2, 2, 1, 1, …
    ## $ PA_3_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, 2, 1, 1, …
    ## $ PA_3_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 3, 1, 1, 3, 4, …
    ## $ PA_3_3                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  2, NA, NA, NA,  2, NA,  2, NA,…
    ## $ PA_3_4                     [3m[38;5;246m<dbl+lbl>[39m[23m  3,  3,  3, NA, NA, NA,  4, NA,  3, NA,…
    ## $ PA_4                       [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  2,  2,  2,  2,  2,  1,  2,…
    ## $ PA_4_1                     [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  2,  2,  2,  2,  2,  1,  2,…
    ## $ PA_4_2                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  1,  1,  1,  1,  1,  1,  3,  1,…
    ## $ PA_4_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA,  2, NA,…
    ## $ PA_4_4                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA,  2, NA,…
    ## $ PA_4_5                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA,  3, NA,…
    ## $ PA_5                       [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, …
    ## $ PA_5_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, …
    ## $ PA_5_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ PA_5_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ PA_5_4                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ PA_6                       [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 1, 1, 2, 1, 1, 1, 1, 2, 2, 1, 2, …
    ## $ PA_6_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, 2, 2, 2, …
    ## $ PA_6_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 5, 1, 1, 1, 1, …
    ## $ PA_6_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA,  2,  2, NA,  2,  2,  2,  2, NA,…
    ## $ PA_6_4                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA,  2,  2, NA,  2,  3,  3,  2, NA,…
    ## $ PA_6_5                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA,  3,  4, NA,  3,  4,  3,  3, NA,…
    ## $ PA_7                       [3m[38;5;246m<dbl+lbl>[39m[23m 1, 2, 2, 2, 2, 1, 2, 2, 1, 2, 2, 1, 2, …
    ## $ PA_7_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 1, 2, 2, 2, 2, 2, 1, 2, …
    ## $ PA_7_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 3, 1, 1, 1, 1, 1, 6, 1, …
    ## $ PA_7_3                     [3m[38;5;246m<dbl+lbl>[39m[23m  2, NA, NA, NA, NA,  2, NA, NA,  2, NA,…
    ## $ PA_7_4                     [3m[38;5;246m<dbl+lbl>[39m[23m  3, NA, NA, NA, NA,  2, NA, NA,  3, NA,…
    ## $ PA_7_5                     [3m[38;5;246m<dbl+lbl>[39m[23m  3, NA, NA, NA, NA,  3, NA, NA,  1, NA,…
    ## $ PB_1                       [3m[38;5;246m<dbl+lbl>[39m[23m 2, 1, 2, 1, 2, 2, 1, 2, 1, 2, 2, 1, 1, …
    ## $ PB_1_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 1, 2, 1, 2, 2, 1, 2, 1, 2, 2, 1, 1, …
    ## $ PB_1_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 2, 1, 3, 1, 1, 3, 1, 6, 1, 1, 5, 6, …
    ## $ PB_1_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA,  1, NA,  1, NA, NA,  1, NA,  1, NA,…
    ## $ PB_1_4                     [3m[38;5;246m<dbl+lbl>[39m[23m NA,  1, NA, NA, NA, NA,  1, NA,  1, NA,…
    ## $ PB_2                       [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1, NA,  2,  2,  2,  1, NA,  1,  2,…
    ## $ PB_2_1                     [3m[38;5;246m<dbl+lbl>[39m[23m  2,  1, NA,  2,  2,  2,  1, NA,  1,  2,…
    ## $ PB_2_2                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  3, NA,  1,  1,  1,  3, NA,  5,  1,…
    ## $ PB_2_3                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1, NA, NA, NA, NA,  1, NA,  1, NA,…
    ## $ PB_2_4                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1, NA, NA, NA, NA,  1, NA,  1, NA,…
    ## $ PB_3                       [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, 2, 2, 2, …
    ## $ PB_3_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, 2, 2, 2, …
    ## $ PB_3_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 4, 1, 1, 1, 1, …
    ## $ PB_4                       [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, 2, 1, 2, …
    ## $ PB_4_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, 2, 1, 2, …
    ## $ PB_4_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 4, 1, 1, 4, 1, …
    ## $ PC_1                       [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 1, 2, 1, 1, 1, 2, 1, 2, 2, 2, 1, …
    ## $ PC_1_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 1, 1, 2, 2, 1, 2, 2, 2, 2, …
    ## $ PC_1_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 2, 3, 1, 1, 4, 1, 1, 1, 1, …
    ## $ PC_1_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA,  2, NA,  2,  2,  2, NA,  2, NA,…
    ## $ PC_2                       [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, …
    ## $ PC_2_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, …
    ## $ PC_2_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ PC_2_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ PC_3                       [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 2, 2, 2, 2, 1, 1, 2, 2, 1, 1, 2, …
    ## $ PC_3_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 1, 2, 2, 2, 1, 2, …
    ## $ PC_3_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 2, 1, 1, 1, 3, 1, …
    ## $ PC_3_3                     [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2, NA, NA, NA, NA, NA,  2, NA, NA,…
    ## $ PC_4                       [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  2,  2,  2,  2,  2,  2,  2,…
    ## $ PC_4_1                     [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  2,  2,  2,  2,  2,  2,  2,…
    ## $ PC_4_2                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  1,  1,  1,  1,  1,  1,  1,  1,…
    ## $ PC_4_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ PC_5                       [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, 2, 2, 2, …
    ## $ PC_5_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, 2, 2, 2, …
    ## $ PC_5_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 4, 1, 1, 1, 1, …
    ## $ PC_5_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA,  4, NA,…
    ## $ PD_1                       [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, …
    ## $ PD_1_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, …
    ## $ PD_1_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ PD_2                       [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, …
    ## $ PD_2_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, …
    ## $ PD_2_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 2, 1, …
    ## $ PD_2_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ PD_3                       [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 1, 1, 2, …
    ## $ PD_3_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, …
    ## $ PD_3_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ PD_3_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ PD_3_4                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ PD_3_5                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ PD_4                       [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, …
    ## $ PD_4_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, …
    ## $ PD_4_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ PD_4_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ PD_4_4                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ PD_5                       [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, 2, …
    ## $ PD_5_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, …
    ## $ PD_5_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ PD_5_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ PD_5_4                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ PD_6                       [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, 2, …
    ## $ PD_6_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, …
    ## $ PD_6_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ PD_6_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ PD_6_4                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ PD_6_5                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ PD_7                       [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, …
    ## $ PD_7_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, …
    ## $ PD_7_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ PD_7_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ PD_7_4                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ PD_7_5                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ PD_7_6                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ PE_1                       [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 1, 1, 1, 2, 1, 2, 2, 2, 2, 1, …
    ## $ PE_1_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, …
    ## $ PE_1_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ PE_2                       [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 1, 1, 1, 2, 1, 1, 1, 2, 1, 1, …
    ## $ PE_2_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 1, 2, 1, 2, 1, 1, 1, 2, 2, 1, …
    ## $ PE_2_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 4, 1, 3, 1, 5, 5, 2, 1, 1, 3, …
    ## $ PE_2_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA,  3,  2,  3, NA,  3,  3,  3,…
    ## $ PE_3                       [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 2, 2, 2, 1, 2, 1, 1, 1, 1, 1, 1, …
    ## $ PE_3_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 1, 2, 1, 1, 1, 1, 1, 1, …
    ## $ PE_3_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 3, 1, 2, 5, 3, 3, 5, 5, …
    ## $ PE_3_3                     [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2, NA, NA, NA,  3, NA,  2,  2,  2,…
    ## $ PE_4                       [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 1, 2, 2, 1, 2, 2, 2, 2, …
    ## $ PE_4_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, 2, 2, 2, …
    ## $ PE_4_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 4, 1, 1, 1, 1, …
    ## $ PE_4_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA,  4, NA, NA,  4, NA,…
    ## $ PE_5                       [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, …
    ## $ PE_5_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, …
    ## $ PE_5_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ PE_5_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ PE_6                       [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 1, 2, 2, 2, 2, 2, 2, 2, …
    ## $ PE_6_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, …
    ## $ PE_6_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ PE_6_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA,  4, NA, NA, NA, NA,…
    ## $ PE_6_4                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA,  2, NA, NA, NA, NA,…
    ## $ PE_7                       [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 1, 1, 2, …
    ## $ PE_7_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, …
    ## $ PE_7_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 3, 1, 1, 1, 1, 1, 1, 1, 1, 1, 3, 1, …
    ## $ PE_7_3                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ PE_7_4                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ PF_1                       [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 1, 2, 1, 2, 2, 2, 1, …
    ## $ PF_1_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 1, 2, 2, 2, 2, 2, 1, …
    ## $ PF_1_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 1, 3, 1, 1, 1, 1, 1, 4, …
    ## $ PF_1_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA,  4, NA,  4, NA,…
    ## $ PF_2                       [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  2,  2,  2,  2,  2,  2,  1,…
    ## $ PF_2_1                     [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  2,  2,  2,  2,  2,  2,  1,…
    ## $ PF_2_2                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  1,  1,  1,  1,  1,  1,  1,  3,…
    ## $ PF_2_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA,  3,…
    ## $ PG_1                       [3m[38;5;246m<dbl+lbl>[39m[23m 5, 5, 4, 3, 4, 4, 5, 5, 5, 5, 3, 4, 4, …
    ## $ PG_2                       [3m[38;5;246m<dbl+lbl>[39m[23m 5, 5, 5, 2, 4, 4, 5, 5, 5, 5, 3, 4, 4, …
    ## $ PG_3                       [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 3, 1, 2, 2, 2, 3, 2, 3, 4, 2, …
    ## $ PG_4                       [3m[38;5;246m<dbl+lbl>[39m[23m 5, 5, 5, 2, 5, 3, 4, 5, 5, 4, 3, 3, 4, …
    ## $ PG_5                       [3m[38;5;246m<dbl+lbl>[39m[23m 1, 2, 1, 2, 2, 4, 1, 1, 1, 1, 3, 3, 2, …
    ## $ PG_6                       [3m[38;5;246m<dbl+lbl>[39m[23m 5, 4, 5, 2, 5, 4, 5, 5, 5, 5, 3, 3, 4, …
    ## $ PG_7                       [3m[38;5;246m<dbl+lbl>[39m[23m 5, 4, 5, 1, 4, 3, 5, 5, 5, 5, 3, 4, 3, …
    ## $ PG_8                       [3m[38;5;246m<dbl+lbl>[39m[23m 1, 2, 2, 5, 4, 3, 5, 2, 1, 4, 3, 5, 3, …
    ## $ PG_9                       [3m[38;5;246m<dbl+lbl>[39m[23m 1, 2, 1, 4, 2, 2, 2, 2, 1, 4, 3, 5, 2, …
    ## $ PG_10                      [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 4, 1, 3, 2, 3, 1, 4, 4, 2, 2, …
    ## $ PH_1                       [3m[38;5;246m<dbl+lbl>[39m[23m 3, 2, 2, 2, 2, 3, 3, 1, 3, 2, 2, 2, 3, …
    ## $ PH_2                       [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 1, 2, 2, 3, 2, 3, 3, 1, …
    ## $ PH_3                       [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 2, 1, 1, 1, 1, 2, 2, 3, 3, 1, …
    ## $ PH_4                       [3m[38;5;246m<dbl+lbl>[39m[23m 1, 2, 2, 1, 1, 1, 1, 1, 2, 1, 2, 2, 2, …
    ## $ PH_5                       [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 1, 3, 2, 3, 3, 2, 1, 2, 2, 2, …
    ## $ PH_6                       [3m[38;5;246m<dbl+lbl>[39m[23m 3, 1, 3, 2, 2, 2, 3, 3, 1, 2, 2, 1, 1, …
    ## $ PH_7                       [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 3, 1, 2, 2, 2, 3, 3, 3, 2, 2, 3, …
    ## $ PH_8                       [3m[38;5;246m<dbl+lbl>[39m[23m 3, 3, 3, 3, 3, 3, 3, 3, 2, 3, 3, 2, 2, …
    ## $ PH_9                       [3m[38;5;246m<dbl+lbl>[39m[23m 2, 3, 3, 1, 2, 3, 1, 3, 3, 2, 2, 3, 2, …
    ## $ PH_10                      [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 2, 1, 1, …
    ## $ PH_11                      [3m[38;5;246m<dbl+lbl>[39m[23m 3, 2, 3, 2, 2, 2, 2, 3, 2, 2, 2, 2, 2, …
    ## $ PH_12                      [3m[38;5;246m<dbl+lbl>[39m[23m 3, 3, 3, 2, 2, 2, 2, 3, 1, 3, 2, 2, 2, …
    ## $ PH_13                      [3m[38;5;246m<dbl+lbl>[39m[23m 2, 3, 3, 2, 3, 2, 3, 3, 1, 3, 1, 2, 2, …
    ## $ PH_14                      [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 2, 1, 2, 1, 1, 1, 2, 2, 2, 3, 1, …
    ## $ PH_15                      [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  1,  2,  1,  1,  1,  1,  2,  2,…
    ## $ PH_16                      [3m[38;5;246m<dbl+lbl>[39m[23m 2, 3, 3, 2, 2, 3, 3, 3, 3, 3, 2, 2, 2, …
    ## $ PH_17                      [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 2, 1, 1, 1, 1, 2, 2, 1, 3, 1, …
    ## $ PH_18                      [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 3, 2, 2, 1, 2, 2, 2, 2, 2, 1, …
    ## $ P_19                       [3m[38;5;246m<dbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ Imagen                     [3m[38;5;246m<chr>[39m[23m "47601.TIF", "47602.TIF", "47603.TIF", "476…
    ## $ PG_autoestima              [3m[38;5;246m<dbl>[39m[23m 50, 45, 48, 22, 42, 34, 42, 45, 48, 39, 29,…
    ## $ PH_depresion               [3m[38;5;246m<dbl>[39m[23m 7, 9, 6, 18, 10, 7, 6, 4, 17, 12, 19, 22, 1…
    ## $ flag_imp_P1_1              [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ flag_imp_P1_2              [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ cuenta_99_caracter         [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ cuenta_99_victim           [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ cuenta_99_parrillas        [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ cuenta_99_total            [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ cuenta_NA_caracter         [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ cuenta_NA_victim           [3m[38;5;246m<dbl>[39m[23m 0, 0, 1, 1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0…
    ## $ cuenta_NA_parrillas        [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ cuenta_NA_total            [3m[38;5;246m<dbl>[39m[23m 0, 0, 1, 2, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0…
    ## $ cuenta_cambios_consis      [3m[38;5;246m<dbl>[39m[23m 0, 0, 3, 0, 0, 0, 1, 0, 0, 0, 2, 3, 0, 2, 0…
    ## $ comuna                     [3m[38;5;246m<dbl+lbl>[39m[23m 115, 115, 115, 115, 115, 115, 115, 115,…
    ## $ region                     [3m[38;5;246m<dbl>[39m[23m 13, 13, 13, 13, 13, 13, 13, 13, 13, 13, 13,…
    ## $ cod_depe2                  [3m[38;5;246m<chr>[39m[23m "Municipal", "Municipal", "Municipal", "Mun…
    ## $ cod_depe_estudio           [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ macrozona                  [3m[38;5;246m<dbl+lbl>[39m[23m 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, …
    ## $ edad_cat6                  [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 2, 1, 1, 2, 2, 2, 3, 3, 2, 3, …
    ## $ edad_cat3                  [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 2, 2, 1, 2, …
    ## $ m17_prop_alu_7a3_pri       [3m[38;5;246m<dbl>[39m[23m 0.1644245, 0.1644245, 0.1644245, 0.1644245,…
    ## $ m17_prop_alu_7a3_pri_grupo [3m[38;5;246m<dbl+lbl>[39m[23m 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, 3, …
    ## $ var_strat                  [3m[38;5;246m<dbl>[39m[23m 1131, 1131, 1131, 1131, 1131, 1131, 1131, 1…
    ## $ var_unit                   [3m[38;5;246m<dbl>[39m[23m 9071, 9071, 9071, 9071, 9071, 9071, 9071, 9…
    ## $ wgt_alu                    [3m[38;5;246m<dbl>[39m[23m 77.85358, 77.85358, 73.60340, 77.85358, 77.…
    ## $ victim_vida_cuenta         [3m[38;5;246m<dbl>[39m[23m 6, 6, 3, 5, 3, 8, 8, 6, 14, 4, 6, 15, 9, 6,…
    ## $ victim_vida_cuenta_na      [3m[38;5;246m<dbl>[39m[23m 0, 0, 1, 1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0…
    ## $ victim_ano_cuenta          [3m[38;5;246m<dbl>[39m[23m 1, 3, 0, 3, 1, 4, 3, 4, 12, 4, 1, 12, 7, 4,…
    ## $ victim_ano_cuenta_na       [3m[38;5;246m<dbl>[39m[23m 0, 0, 1, 1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0…
    ## $ poli_vida                  [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, 2, 1, 2, …
    ## $ poli_año                   [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, 2, 1, 2, …
    ## $ todas_al_menos_vida        [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ todas_al_menos_año         [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 2, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ A1_una_en_vida             [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 2, 1, 1, 1, 1, 1, 2, 1, 1, …
    ## $ A2_una_en_vida             [3m[38;5;246m<dbl+lbl>[39m[23m 1, 2, 2, 2, 2, 1, 2, 2, 1, 2, 2, 1, 2, …
    ## $ B_una_en_vida              [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 2, 1, 2, 2, 1, 2, 1, 2, 2, 1, 1, …
    ## $ C_una_en_vida              [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 2, 1, 1, 1, 1, 1, 2, 1, 1, 1, …
    ## $ D_una_en_vida              [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 1, 1, 2, …
    ## $ E1_una_en_vida             [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 2, 1, 1, 1, 2, 1, 1, 1, 1, 1, 1, …
    ## $ E2_una_en_vida             [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 2, 2, 2, 1, 2, 2, 2, 2, 1, 1, 2, …
    ## $ F_una_en_vida              [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 1, 2, 1, 1, 2, 1, 1, …
    ## $ A1_una_en_año              [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 1, 2, 2, 2, 1, 1, 1, 2, 1, 1, …
    ## $ A2_una_en_año              [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 1, 2, 2, 1, 2, 2, 1, 2, …
    ## $ B_una_en_año               [3m[38;5;246m<dbl+lbl>[39m[23m 2, 1, 2, 1, 2, 2, 1, 2, 1, 2, 2, 1, 1, …
    ## $ C_una_en_año               [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 1, 1, 2, 1, 1, 2, 2, 1, 2, …
    ## $ D_una_en_año               [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, …
    ## $ E1_una_en_año              [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 1, 2, 1, 2, 1, 1, 1, 1, 1, 1, …
    ## $ E2_una_en_año              [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, …
    ## $ F_una_en_año               [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 1, 2, 2, 1, 2, 1, 1, …
    ## $ pa1l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 1, 0, 0, 1, 1, 0, 1, 0, 1, 1, 0, 0…
    ## $ pa2l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, NA, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, …
    ## $ pa3l                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 0, 0, 0, 1, 0, 1, 0, 0, 1, 1, 1, 1…
    ## $ pa4l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0…
    ## $ pa5l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ pa6l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 1, 1, 0, 1, 1, 1, 1, 0, 0, 1, 0, 1, 0…
    ## $ pa7l                       [3m[38;5;246m<dbl>[39m[23m 1, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 1, 0, 0, 0…
    ## $ pb1l                       [3m[38;5;246m<dbl>[39m[23m 0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 0, 1, 1, 0, 1…
    ## $ pb2l                       [3m[38;5;246m<dbl>[39m[23m 1, 1, NA, 0, 0, 0, 1, NA, 1, 0, 0, 1, 1, 0,…
    ## $ pb3l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0…
    ## $ pb4l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0…
    ## $ pc1l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 1, 0, 1, 1, 1, 0, 1, 0, 0, 0, 1, 0, 0…
    ## $ pc2l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ pc3l                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 0, 0, 0, 0, 1, 1, 0, 0, 1, 1, 0, 0, 1…
    ## $ pc4l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0…
    ## $ pc5l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0…
    ## $ pd1l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ pd2l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0…
    ## $ pd3l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 0, 0, 0…
    ## $ pd4l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ pd5l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0…
    ## $ pd6l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0…
    ## $ pd7l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ pe1l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 1, 1, 1, 0, 1, 0, 0, 0, 0, 1, 0, 1…
    ## $ pe2l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 1, 1, 1, 0, 1, 1, 1, 0, 1, 1, 0, 1…
    ## $ pe3l                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 0, 0, 0, 1, 0, 1, 1, 1, 1, 1, 1, 0, 1…
    ## $ pe4l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 0, 1, 1…
    ## $ pe5l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1…
    ## $ pe6l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ pe7l                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 0, 0, 0…
    ## $ pf1l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 0, 1, 0, 1, 0, 0, 0, 1, 0, 0…
    ## $ pf2l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 1, 0, NA, …
    ## $ pa1y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 0, 1, 1, 1, 0, 1, 0, 1, 0, NA, 1, …
    ## $ pa2y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, NA, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, …
    ## $ pa3y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, NA, 1, 1, NA, NA, N…
    ## $ pa4y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, NA, 1, 1, 0, 1, 1, …
    ## $ pa5y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ pa6y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, NA, 1, 1, 1, 1, NA,…
    ## $ pa7y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, NA, 1, 1, 1, 1, 1, NA, 1, 1,…
    ## $ pb1y                       [3m[38;5;246m<dbl>[39m[23m 1, 0, 1, NA, 1, 1, NA, 1, NA, 1, 1, NA, NA,…
    ## $ pb2y                       [3m[38;5;246m<dbl>[39m[23m 1, NA, NA, 1, 1, 1, NA, NA, NA, 1, 1, NA, N…
    ## $ pb3y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, NA, 1, 1, 1, 1, 1, …
    ## $ pb4y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, NA, 1, 1, NA, 1, 1,…
    ## $ pc1y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 0, NA, 1, 1, NA, 1, 1, 1, 1, 1,…
    ## $ pc2y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ pc3y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 0, 1, 1, 1, NA, 1, 1, …
    ## $ pc4y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, NA, …
    ## $ pc5y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, NA, 1, 1, 1, 1, 1, …
    ## $ pd1y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ pd2y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 1, 1, 1…
    ## $ pd3y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ pd4y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ pd5y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ pd6y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ pd7y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ pe1y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ pe2y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, NA, 1, NA, 1, NA, NA, 0, 1, 1, NA,…
    ## $ pe3y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, NA, 1, 0, NA, NA, NA, NA, NA…
    ## $ pe4y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, NA, 1, 1, 1, 1, 1, …
    ## $ pe5y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ pe6y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ pe7y                       [3m[38;5;246m<dbl>[39m[23m 0, NA, 1, 1, 1, 1, 1, 1, 1, 1, 1, NA, 1, 1,…
    ## $ pf1y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, 1, NA, 1, 1, 1, 1, 1, NA, 1,…
    ## $ pf2y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, NA, 1, NA, 1, NA…
    ## $ id_k                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ id_s                       [3m[38;5;246m<dbl>[39m[23m 1131, 1131, 1131, 1131, 1131, 1131, 1131, 1…
    ## $ id_j                       [3m[38;5;246m<dbl>[39m[23m 9071, 9071, 9071, 9071, 9071, 9071, 9071, 9…
    ## $ id_i                       [3m[38;5;246m<int>[39m[23m 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, …
    ## $ ws                         [3m[38;5;246m<dbl>[39m[23m 0.07000842, 0.07000842, 0.06618652, 0.07000…

# Ejercicio 3. Crear subconjuntos de datos

## Crear datos exploratorios y confirmatorios (Submuestra de .50%)

``` r
#------------------------------------------------------------------------------
# sample
#------------------------------------------------------------------------------

#--------------------------------------
# 50% de los datos
#--------------------------------------

set.seed(20230316) # se usa fecha, en vez de RUT

library(dplyr)
data_exp <- dplyr::slice_sample(data_poly, prop = .5, by = region)

#--------------------------------------
# 50% de los otros datos
#--------------------------------------

data_con <- dplyr::filter(data_poly, !folio %in% data_exp$folio)
```

# Ejercicio 4. Visualizar distribución

## Histograma y Skewness

``` r
#------------------------------------------------------------------------------
# visualizacion
#------------------------------------------------------------------------------

#--------------------------------------
# histograma
#--------------------------------------

hist(data_exp$PH_depresion,
  main = 'Histograma de puntajes de Depresión (Escala de Birleson)',
  xlab = 'Puntajes')
```

![](taller_r_02_descriptivos_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

``` r
#--------------------------------------
# skewness
#--------------------------------------

moments::skewness(data_exp$PH_depresion, na.rm = TRUE)
```

    ## [1] 0.6330414

``` r
#--------------------------------------
# skewness mostrar inverso
#--------------------------------------

moments::skewness(r4sda::reverse(data_exp$PH_depresion), na.rm = TRUE)
```

    ## [1] -0.6330414

``` r
#--------------------------------------
# histograma, inverso
#--------------------------------------

hist(r4sda::reverse(data_exp$PH_depresion),
  main = 'Histograma de puntajes de Depresión (Escala de Birleson)\npuntajes invertidos',
  xlab = 'Puntajes')
```

![](taller_r_02_descriptivos_files/figure-gfm/unnamed-chunk-5-2.png)<!-- -->

- **Descripción**
  - Los puntajes de depresión presentan una distribución **asimétrica
    positiva**.
  - Hay una mayor cola de resultados extendidos entre las observaciones
    de mayor valor.
  - A medida que aumentan los valores observados, la cantidad de casos
    observados disminuye.
  - La prevalencia observada disminuye a medida que los puntajes
    aumemtan

## Boxplot

``` r
#------------------------------------------------------------------------------
# visualizacion
#------------------------------------------------------------------------------

#--------------------------------------
# histograma
#--------------------------------------

boxplot(PH_depresion ~ region, 
  data = data_poly,
  horizontal = TRUE
  )
```

![](taller_r_02_descriptivos_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

## Ejercicio 6. Medidas de tendencia central y de posición

``` r
#------------------------------------------------------------------------------
# muestreo de casos
#------------------------------------------------------------------------------

#--------------------------------------
# medidas de tendencia central
#--------------------------------------

library(dplyr)
data_exp %>%
summarize(
media   = mean(PH_depresion, na.rm = TRUE),
mediana = median(PH_depresion, na.rm = TRUE)
) %>%
knitr::kable(., digits = 2)
```

| media | mediana |
|------:|--------:|
| 11.81 |      11 |

``` r
#--------------------------------------
# percentiles
#--------------------------------------

library(dplyr)
data_exp %>%
summarize(
p05  = quantile(PH_depresion, probs = .05, na.rm = TRUE),
p10  = quantile(PH_depresion, probs = .10, na.rm = TRUE),
p25  = quantile(PH_depresion, probs = .25, na.rm = TRUE),
p50  = quantile(PH_depresion, probs = .50, na.rm = TRUE),
p75  = quantile(PH_depresion, probs = .75, na.rm = TRUE),
p90  = quantile(PH_depresion, probs = .90, na.rm = TRUE),
p95  = quantile(PH_depresion, probs = .95, na.rm = TRUE)
) %>%
knitr::kable(., digits = 2)
```

| p05 | p10 | p25 | p50 | p75 | p90 | p95 |
|----:|----:|----:|----:|----:|----:|----:|
|   3 |   4 |   7 |  11 |  16 |  20 |  23 |

## Ejercicio 7. Interpretacion de percentiles.

- Empleando el criterio de corte de 19 puntos (MINSAL, 2013), al menos
  10% de los casos estaría en riesgo de depresion.
- Si se emplea el criterio de Denda et al (2006), de 15 puntos, al menos
  25% de los jóvenes estaría en riesgo de depresion.

## Ejercicio 8. Recodificación y Proporción.

- **¿Qué proporción de casos tiene depresión?**

``` r
#------------------------------------------------------------------------------
# recodificacion
#------------------------------------------------------------------------------

#--------------------------------------
# con case_when
#--------------------------------------

library(dplyr)
data_exp %>%
mutate(depresion = case_when(
PH_depresion >= 19 ~ 1,
PH_depresion <  19 ~ 0
)) %>%
summarize(
  depresion = mean(depresion, na.rm = TRUE)
) %>%
knitr::kable(., digits = 2)
```

| depresion |
|----------:|
|      0.15 |

``` r
#--------------------------------------
# con if_else
#--------------------------------------

library(dplyr)
data_con %>%
mutate(depresion = dplyr::if_else(PH_depresion >= 19, 1, 0)) %>%
summarize(
  depresion = mean(depresion, na.rm = TRUE)
) %>%
knitr::kable(., digits = 2)
```

| depresion |
|----------:|
|      0.13 |

- **Respuesta**
  - 15% de los casos estaría en riesgo de depresión (datos
    exploratorios)
  - 13% de los casos estaría en riesgo de depresión (datos
    confirmatorios)

## Ejercicio 10. Contigencia

- Similares a las expectativas anterioes, se plantea que la prevalencia
  de depresión es mayor en mujeres. Calcule una tabla de contigencia
  donde se obtenga la proporción de mujeres y de hombres
  respectivamente.

- Emplee la variable creada en el ejercicio 8, la cual clasifica a los
  casos con o sin riesgo de depresión, empleando el puntaje de corte
  emmpleado en Chile (19 puntos o más).

``` r
#------------------------------------------------------------------------------
# tabla de contingencia
#------------------------------------------------------------------------------

#--------------------------------------
# prepar datos
#--------------------------------------

data_model <- data_exp %>%
mutate(depresion = case_when(
PH_depresion >= 19 ~ 1,
PH_depresion <  19 ~ 0
)) %>%
mutate(sexo = case_when(
P1_2 == 1 ~ 'mujeres',
P1_2 == 2 ~ 'hombres'
)) %>%
dplyr::glimpse()
```

    ## Rows: 9,838
    ## Columns: 321
    ## $ m16_rbd                    [3m[38;5;246m<dbl>[39m[23m 25496, 24898, 25027, 9897, 8945, 8490, 1019…
    ## $ m17_rbd                    [3m[38;5;246m<dbl>[39m[23m 25496, 24898, 25027, 9897, 8945, 8490, 1019…
    ## $ fuente                     [3m[38;5;246m<chr>[39m[23m "Salida_5", "Salida_1", "Salida_10", "Salid…
    ## $ folio                      [3m[38;5;246m<dbl>[39m[23m 53207, 46118, 58029, 57004, 83321, 81203, 5…
    ## $ P1_1                       [3m[38;5;246m<dbl+lbl>[39m[23m 3, 3, 5, 5, 4, 5, 3, 2, 4, 3, 4, 1, 1, …
    ## $ P1_2                       [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 2, 2, 1, 1, 1, 1, 2, 1, 2, 1, 1, …
    ## $ P1_3                       [3m[38;5;246m<dbl+lbl>[39m[23m 3, 3, 5, 5, 5, 6, 3, 2, 4, 3, 5, 1, 2, …
    ## $ P1_4                       [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 4, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ P1_5                       [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  1,  1,  4,  1,  1,  1,  1,  1,…
    ## $ P1_6                       [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 8, 1, 1, 1, 1, 1, …
    ## $ P1_7_1                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  1,  1,  1,  1,  1,  1,  1,  1,…
    ## $ P1_7_2                     [3m[38;5;246m<dbl+lbl>[39m[23m NA,  1, NA,  1, NA, NA,  1,  1,  1, NA,…
    ## $ P1_7_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA,  1,  1,  1,  1,  1, NA,…
    ## $ P1_7_4                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ P1_7_5                     [3m[38;5;246m<dbl+lbl>[39m[23m  1, NA,  1,  1, NA, NA, NA, NA, NA,  1,…
    ## $ P1_7_6                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA,  1, NA, NA, NA, NA, NA, NA,  1,…
    ## $ P1_7_7                     [3m[38;5;246m<dbl+lbl>[39m[23m  1, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ P1_7_8                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA,  1, NA, NA, NA, NA, NA, NA, NA,…
    ## $ P1_8_1                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ P1_8_2                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ P1_8_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ P1_8_4                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ P1_8_5                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ P1_8_6                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  1,  1,  1,  1,  1,  1,  1,  1,…
    ## $ PA_1                       [3m[38;5;246m<dbl+lbl>[39m[23m  1,  2,  1,  2,  2,  2,  2,  2,  1,  1,…
    ## $ PA_1_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 2, 1, 2, 2, 2, 2, 2, 2, 1, 1, 2, 2, …
    ## $ PA_1_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 1, 3, 1, 1, 1, 1, 1, 1, 2, 3, 1, 1, …
    ## $ PA_1_3                     [3m[38;5;246m<dbl+lbl>[39m[23m  3, NA,  4, NA, NA, NA, NA, NA,  3,  2,…
    ## $ PA_1_4                     [3m[38;5;246m<dbl+lbl>[39m[23m  2, NA,  1, NA, NA, NA, NA, NA,  1,  3,…
    ## $ PA_2                       [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, 2, …
    ## $ PA_2_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, 2, …
    ## $ PA_2_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 3, 1, 1, …
    ## $ PA_2_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ PA_2_4                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ PA_3                       [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 2, 2, 2, 2, 2, 2, 2, 1, 1, 1, 2, …
    ## $ PA_3_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 1, 2, 2, 2, 2, 2, 2, 2, 1, 2, 2, 2, …
    ## $ PA_3_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 2, 1, 1, 1, 1, 1, 1, 1, 2, 1, 1, 1, …
    ## $ PA_3_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA,  2, NA, NA, NA, NA, NA, NA, NA,  2,…
    ## $ PA_3_4                     [3m[38;5;246m<dbl+lbl>[39m[23m  4,  4, NA, NA, NA, NA, NA, NA, NA,  3,…
    ## $ PA_4                       [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  2,  2,  2,  2,  1,  2,  1, NA,…
    ## $ PA_4_1                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  2,  2,  2,  2,  2,  2,  1, NA,…
    ## $ PA_4_2                     [3m[38;5;246m<dbl+lbl>[39m[23m  2,  3,  1,  1,  1,  1,  1,  1,  2, NA,…
    ## $ PA_4_3                     [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2, NA, NA, NA, NA,  2, NA,  3, NA,…
    ## $ PA_4_4                     [3m[38;5;246m<dbl+lbl>[39m[23m  3,  2, NA, NA, NA, NA,  2, NA,  2, NA,…
    ## $ PA_4_5                     [3m[38;5;246m<dbl+lbl>[39m[23m  4,  4, NA, NA, NA, NA,  4, NA,  1, NA,…
    ## $ PA_5                       [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 1, 1, 1, 2, 2, …
    ## $ PA_5_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, 2, …
    ## $ PA_5_2                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  1,  1,  1,  1,  1,  1,  1,  1,…
    ## $ PA_5_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA,  3,  3,…
    ## $ PA_5_4                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA,  1,  3,…
    ## $ PA_6                       [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  2,  2,  1,  2,  1,  1,  1,  1,…
    ## $ PA_6_1                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  2,  2,  2,  2,  1,  2,  1,  2,…
    ## $ PA_6_2                     [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  1,  1,  1,  1,  2,  1,  2,  1,…
    ## $ PA_6_3                     [3m[38;5;246m<dbl+lbl>[39m[23m  3,  2, NA, NA,  4, NA,  2,  2,  3,  3,…
    ## $ PA_6_4                     [3m[38;5;246m<dbl+lbl>[39m[23m  3,  2, NA, NA,  3, NA,  3,  3,  3,  3,…
    ## $ PA_6_5                     [3m[38;5;246m<dbl+lbl>[39m[23m  4,  4, NA, NA,  3, NA,  4,  4,  3,  3,…
    ## $ PA_7                       [3m[38;5;246m<dbl+lbl>[39m[23m 2, 1, 2, 1, 1, 2, 1, 2, 2, 2, 2, 2, 2, …
    ## $ PA_7_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 1, 2, 2, 1, 2, 2, 2, 2, 2, 2, …
    ## $ PA_7_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 3, 1, 1, 3, 1, 1, 1, 1, 1, 1, …
    ## $ PA_7_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA,  2, NA,  4,  3, NA,  2, NA, NA, NA,…
    ## $ PA_7_4                     [3m[38;5;246m<dbl+lbl>[39m[23m NA,  2, NA,  3,  3, NA,  2, NA, NA, NA,…
    ## $ PA_7_5                     [3m[38;5;246m<dbl+lbl>[39m[23m NA,  4, NA,  3,  3, NA,  4, NA, NA, NA,…
    ## $ PB_1                       [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 2, 1, 1, 2, 1, 2, 2, 1, 2, 1, 2, …
    ## $ PB_1_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 2, 2, 1, 2, 2, 1, 2, 2, 1, 2, 1, 2, …
    ## $ PB_1_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 3, 1, 1, 3, 1, 1, 5, 1, 1, 3, 1, 3, 1, …
    ## $ PB_1_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA,  4, NA,  3,  4, NA,  1, NA, NA,  3,…
    ## $ PB_1_4                     [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2, NA,  2,  2, NA,  1, NA, NA,  1,…
    ## $ PB_2                       [3m[38;5;246m<dbl+lbl>[39m[23m 1, 2, 2, 2, 1, 2, 1, 2, 2, 2, 1, 1, 2, …
    ## $ PB_2_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, 2, …
    ## $ PB_2_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 4, 1, 1, …
    ## $ PB_2_3                     [3m[38;5;246m<dbl+lbl>[39m[23m  1, NA, NA, NA,  1, NA,  1, NA, NA, NA,…
    ## $ PB_2_4                     [3m[38;5;246m<dbl+lbl>[39m[23m  1, NA, NA, NA,  1, NA,  1, NA, NA, NA,…
    ## $ PB_3                       [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, …
    ## $ PB_3_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, …
    ## $ PB_3_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ PB_4                       [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 1, 2, 2, 2, 2, 2, 2, 2, 2, …
    ## $ PB_4_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, …
    ## $ PB_4_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ PC_1                       [3m[38;5;246m<dbl+lbl>[39m[23m 1, 2, 1, 1, 1, 2, 2, 2, 1, 2, 1, 2, 2, …
    ## $ PC_1_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 2, 2, 2, 2, 2, 2, 2, 1, 2, 2, 2, 2, …
    ## $ PC_1_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 1, 1, 1, 1, 1, 1, 1, 2, 1, 1, 1, 1, …
    ## $ PC_1_3                     [3m[38;5;246m<dbl+lbl>[39m[23m  3, NA,  2,  2,  4, NA, NA, NA,  3, NA,…
    ## $ PC_2                       [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 1, 2, 2, …
    ## $ PC_2_1                     [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, …
    ## $ PC_2_2                     [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ PC_2_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ PC_3                       [3m[38;5;246m<dbl+lbl>[39m[23m  2,  1,  1,  1,  2, NA,  1,  2,  2,  1,…
    ## $ PC_3_1                     [3m[38;5;246m<dbl+lbl>[39m[23m  2,  1,  2,  1,  2, NA,  1,  2,  2,  1,…
    ## $ PC_3_2                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  4,  1,  2,  1, NA,  3,  1,  1,  2,…
    ## $ PC_3_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA,  4,  2,  2, NA, NA,  2, NA, NA,  2,…
    ## $ PC_4                       [3m[38;5;246m<dbl+lbl>[39m[23m  2,  1,  1,  1,  2, NA,  1,  2,  2,  2,…
    ## $ PC_4_1                     [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  2,  2, NA,  2,  2,  2,  2,…
    ## $ PC_4_2                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  1,  1,  1, NA,  1,  1,  1,  1,…
    ## $ PC_4_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA,  2,  2,  4, NA, NA,  2, NA, NA, NA,…
    ## $ PC_5                       [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  2,  2, NA,  2,  2,  2,  2,…
    ## $ PC_5_1                     [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  2,  2, NA,  2,  2,  2,  2,…
    ## $ PC_5_2                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  1,  1,  1, NA,  1,  1,  1,  1,…
    ## $ PC_5_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ PD_1                       [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  1,  2, NA,  2,  2,  2,  2,…
    ## $ PD_1_1                     [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  1,  2, NA,  2,  2,  2,  2,…
    ## $ PD_1_2                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  1,  3,  1, NA,  1,  1,  1,  1,…
    ## $ PD_2                       [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  2,  2, NA,  1,  2,  2,  2,…
    ## $ PD_2_1                     [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  2,  2, NA,  2,  2,  2,  2,…
    ## $ PD_2_2                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  1,  1,  1, NA,  1,  1,  1,  1,…
    ## $ PD_2_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA,  4, NA, NA, NA,…
    ## $ PD_3                       [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  2,  1, NA,  2,  2,  2,  2,…
    ## $ PD_3_1                     [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  2,  2, NA,  2,  2,  2,  2,…
    ## $ PD_3_2                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  1,  1,  1, NA,  1,  1,  1,  1,…
    ## $ PD_3_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA,  4, NA, NA, NA, NA, NA,…
    ## $ PD_3_4                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA,  3, NA, NA, NA, NA, NA,…
    ## $ PD_3_5                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA,  1, NA, NA, NA, NA, NA,…
    ## $ PD_4                       [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  1,  2, NA,  2,  2,  2,  2,…
    ## $ PD_4_1                     [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  2,  2, NA,  2,  2,  2,  2,…
    ## $ PD_4_2                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  1,  1,  1, NA,  1,  1,  1,  1,…
    ## $ PD_4_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ PD_4_4                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA,  2, NA, NA, NA, NA, NA, NA,…
    ## $ PD_5                       [3m[38;5;246m<dbl+lbl>[39m[23m  2,  1,  2,  2,  2, NA,  2,  2,  2,  2,…
    ## $ PD_5_1                     [3m[38;5;246m<dbl+lbl>[39m[23m  2,  1,  2,  2,  2, NA,  2,  2,  2,  2,…
    ## $ PD_5_2                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  2,  1,  1,  1, NA,  1,  1,  1,  1,…
    ## $ PD_5_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA,  4, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ PD_5_4                     [3m[38;5;246m<dbl+lbl>[39m[23m NA,  2, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ PD_6                       [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  1,  2, NA,  2,  2,  2,  2,…
    ## $ PD_6_1                     [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  2,  2, NA,  2,  2,  2,  2,…
    ## $ PD_6_2                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  1,  1,  1, NA,  1,  1,  1,  1,…
    ## $ PD_6_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ PD_6_4                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA,  2, NA, NA, NA, NA, NA, NA,…
    ## $ PD_6_5                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA,  2, NA, NA, NA, NA, NA, NA,…
    ## $ PD_7                       [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  1,  2, NA,  2,  2,  2,  2,…
    ## $ PD_7_1                     [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  2,  2, NA,  2,  2,  2,  2,…
    ## $ PD_7_2                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  1,  1,  1, NA,  1,  1,  1,  1,…
    ## $ PD_7_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA,  4, NA, NA, NA, NA, NA, NA,…
    ## $ PD_7_4                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA,  2, NA, NA, NA, NA, NA, NA,…
    ## $ PD_7_5                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA,  3, NA, NA, NA, NA, NA, NA,…
    ## $ PD_7_6                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA,  2, NA, NA, NA, NA, NA, NA,…
    ## $ PE_1                       [3m[38;5;246m<dbl+lbl>[39m[23m  1,  2,  2,  2,  2, NA,  2,  1,  1,  1,…
    ## $ PE_1_1                     [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  2,  2, NA,  2,  2,  2,  2,…
    ## $ PE_1_2                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  1,  1,  1, NA,  1,  1,  1,  1,…
    ## $ PE_2                       [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  1,  1,  1, NA,  1,  2,  1,  1,…
    ## $ PE_2_1                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  1,  1,  1, NA,  2,  2,  1,  1,…
    ## $ PE_2_2                     [3m[38;5;246m<dbl+lbl>[39m[23m  3,  3,  4,  5,  6, NA,  1,  1,  4,  3,…
    ## $ PE_2_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA,  3,  3,  3,  3, NA,  1, NA,  3,  4,…
    ## $ PE_3                       [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  1,  1,  1, NA,  1,  1,  1,  1,…
    ## $ PE_3_1                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  2,  1,  1, NA,  2,  1,  1,  1,…
    ## $ PE_3_2                     [3m[38;5;246m<dbl+lbl>[39m[23m  3,  4,  1,  2,  4, NA,  1,  4,  4,  3,…
    ## $ PE_3_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA,  3,  4, NA,  3, NA,  3,  2,  2,  2,…
    ## $ PE_4                       [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  1,  1,  1, NA,  1,  2,  2,  1,…
    ## $ PE_4_1                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  2,  1,  2, NA,  2,  2,  2,  1,…
    ## $ PE_4_2                     [3m[38;5;246m<dbl+lbl>[39m[23m  2,  3,  1,  2,  1, NA,  1,  1,  1,  3,…
    ## $ PE_4_3                     [3m[38;5;246m<dbl+lbl>[39m[23m  2,  4,  3, NA,  3, NA,  2, NA, NA,  4,…
    ## $ PE_5                       [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  2,  1, NA,  1,  2,  1,  2,…
    ## $ PE_5_1                     [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  2,  2, NA,  2,  2,  1,  2,…
    ## $ PE_5_2                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  1,  1,  1, NA,  1,  1,  2,  1,…
    ## $ PE_5_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA,  3, NA,  3, NA,  3, NA,…
    ## $ PE_6                       [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  2,  2, NA,  2,  2,  2,  2,…
    ## $ PE_6_1                     [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  2,  2, NA,  2,  2,  2,  2,…
    ## $ PE_6_2                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  1,  1,  1, NA,  1,  1,  1,  1,…
    ## $ PE_6_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ PE_6_4                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ PE_7                       [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  2,  2, NA,  2,  2,  2,  2,…
    ## $ PE_7_1                     [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  2,  2, NA,  2,  2,  2,  2,…
    ## $ PE_7_2                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  1,  1,  1, NA,  1,  1,  1,  1,…
    ## $ PE_7_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ PE_7_4                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ PF_1                       [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  1,  1,  2, NA,  1,  2,  2,  1,…
    ## $ PF_1_1                     [3m[38;5;246m<dbl+lbl>[39m[23m  2,  1,  2,  2,  2, NA,  1,  2,  2,  2,…
    ## $ PF_1_2                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  2,  1,  1,  1, NA,  3,  1,  1,  1,…
    ## $ PF_1_3                     [3m[38;5;246m<dbl+lbl>[39m[23m  4,  1,  3,  4, NA, NA,  3, NA, NA,  3,…
    ## $ PF_2                       [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  2,  1, NA,  2,  2,  2,  2,…
    ## $ PF_2_1                     [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  2,  1, NA,  2,  2,  2,  2,…
    ## $ PF_2_2                     [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  1,  1,  2, NA,  1,  1,  1,  1,…
    ## $ PF_2_3                     [3m[38;5;246m<dbl+lbl>[39m[23m NA, NA, NA, NA,  1, NA, NA, NA, NA, NA,…
    ## $ PG_1                       [3m[38;5;246m<dbl+lbl>[39m[23m  3,  4,  2,  3,  3, NA,  2,  4,  4,  4,…
    ## $ PG_2                       [3m[38;5;246m<dbl+lbl>[39m[23m  4,  4,  3,  3,  5, NA,  3,  4,  4,  4,…
    ## $ PG_3                       [3m[38;5;246m<dbl+lbl>[39m[23m  5,  3,  5,  4,  1, NA,  4,  3,  2,  3,…
    ## $ PG_4                       [3m[38;5;246m<dbl+lbl>[39m[23m  3,  4,  2,  4,  4, NA,  2,  5,  4,  3,…
    ## $ PG_5                       [3m[38;5;246m<dbl+lbl>[39m[23m  3,  2,  3,  4,  3, NA,  4,  2,  2,  3,…
    ## $ PG_6                       [3m[38;5;246m<dbl+lbl>[39m[23m  3,  5,  4,  2,  4, NA,  3,  4,  5,  4,…
    ## $ PG_7                       [3m[38;5;246m<dbl+lbl>[39m[23m  2,  5,  1,  2,  2, NA,  2,  4,  5,  3,…
    ## $ PG_8                       [3m[38;5;246m<dbl+lbl>[39m[23m  5,  4,  4,  4,  3, NA,  3,  3,  3,  2,…
    ## $ PG_9                       [3m[38;5;246m<dbl+lbl>[39m[23m  5,  3,  5,  2,  3, NA,  4,  4,  2,  4,…
    ## $ PG_10                      [3m[38;5;246m<dbl+lbl>[39m[23m  5,  1,  4,  3,  3, NA,  4,  4,  2,  4,…
    ## $ PH_1                       [3m[38;5;246m<dbl+lbl>[39m[23m  2,  3,  2,  2,  3, NA,  2,  2,  3,  2,…
    ## $ PH_2                       [3m[38;5;246m<dbl+lbl>[39m[23m  3,  2,  3,  2,  2, NA,  3,  1,  1,  2,…
    ## $ PH_3                       [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  2,  3, NA,  2,  1,  2,  2,…
    ## $ PH_4                       [3m[38;5;246m<dbl+lbl>[39m[23m  2,  1,  1,  2,  2, NA,  2,  1,  2,  2,…
    ## $ PH_5                       [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  2,  3, NA,  1,  1,  2,  1,…
    ## $ PH_6                       [3m[38;5;246m<dbl+lbl>[39m[23m  2,  3,  1,  1,  2, NA,  2,  2,  3,  3,…
    ## $ PH_7                       [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  2,  2, NA,  1,  3,  3,  2,…
    ## $ PH_8                       [3m[38;5;246m<dbl+lbl>[39m[23m  3,  2,  2,  2,  2, NA,  2,  3,  3,  3,…
    ## $ PH_9                       [3m[38;5;246m<dbl+lbl>[39m[23m  3,  2,  1,  2,  3, NA,  2,  2,  3,  2,…
    ## $ PH_10                      [3m[38;5;246m<dbl+lbl>[39m[23m  2,  1,  2,  2,  1, NA,  2,  2,  1,  1,…
    ## $ PH_11                      [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  2,  2, NA,  2,  2,  2,  3,…
    ## $ PH_12                      [3m[38;5;246m<dbl+lbl>[39m[23m  2,  3,  1,  2,  2, NA,  2,  2,  2,  3,…
    ## $ PH_13                      [3m[38;5;246m<dbl+lbl>[39m[23m  2,  3,  2,  2,  2, NA,  2,  3,  3,  3,…
    ## $ PH_14                      [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  2,  1, NA,  2,  2,  2,  2,…
    ## $ PH_15                      [3m[38;5;246m<dbl+lbl>[39m[23m  3,  2,  3,  2,  3, NA,  3,  2,  1,  1,…
    ## $ PH_16                      [3m[38;5;246m<dbl+lbl>[39m[23m  1,  3,  2,  2,  2, NA,  1,  2,  2,  2,…
    ## $ PH_17                      [3m[38;5;246m<dbl+lbl>[39m[23m  3,  2,  3,  2,  1, NA,  2,  2,  1,  1,…
    ## $ PH_18                      [3m[38;5;246m<dbl+lbl>[39m[23m  3,  2,  3,  3,  2, NA,  2,  2,  1,  2,…
    ## $ P_19                       [3m[38;5;246m<dbl>[39m[23m NA, NA, NA, NA, NA, NA, NA, NA, NA, 1, NA, …
    ## $ Imagen                     [3m[38;5;246m<chr>[39m[23m "53207.TIF", "46118.TIF", "58029.TIF", "570…
    ## $ PG_autoestima              [3m[38;5;246m<dbl>[39m[23m 22, 39, 21, 27, 35, NA, 23, 35, 41, 32, 23,…
    ## $ PH_depresion               [3m[38;5;246m<dbl>[39m[23m 21, 11, 24, 20, 14, NA, 23, 13, 7, 11, 27, …
    ## $ flag_imp_P1_1              [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ flag_imp_P1_2              [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ cuenta_99_caracter         [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ cuenta_99_victim           [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0…
    ## $ cuenta_99_parrillas        [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ cuenta_99_total            [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0…
    ## $ cuenta_NA_caracter         [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ cuenta_NA_victim           [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 19, 0, 0, 0, 1, 0, 0, 0, 0, …
    ## $ cuenta_NA_parrillas        [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 28, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ cuenta_NA_total            [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 47, 0, 0, 0, 1, 0, 0, 0, 0, …
    ## $ cuenta_cambios_consis      [3m[38;5;246m<dbl>[39m[23m 1, 3, 2, 0, 9, 0, 1, 2, 0, 3, 5, 3, 0, 0, 3…
    ## $ comuna                     [3m[38;5;246m<dbl+lbl>[39m[23m 134, 101,  75, 101, 132, 172,  25,  40,…
    ## $ region                     [3m[38;5;246m<dbl>[39m[23m 13, 13, 13, 13, 13, 13, 13, 13, 13, 13, 13,…
    ## $ cod_depe2                  [3m[38;5;246m<chr>[39m[23m "Part. Subv.", "Part. Subv.", "Part. Subv."…
    ## $ cod_depe_estudio           [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 2, 2, 2, 1, 2, 2, 1, 2, 2, 1, 2, …
    ## $ macrozona                  [3m[38;5;246m<dbl+lbl>[39m[23m 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, …
    ## $ edad_cat6                  [3m[38;5;246m<dbl+lbl>[39m[23m 3, 3, 5, 5, 5, 6, 3, 2, 4, 3, 5, 1, 2, …
    ## $ edad_cat3                  [3m[38;5;246m<dbl+lbl>[39m[23m 2, 2, 3, 3, 3, 3, 2, 1, 2, 2, 3, 1, 1, …
    ## $ m17_prop_alu_7a3_pri       [3m[38;5;246m<dbl>[39m[23m 0.47614761, 0.29824561, 0.37386018, 0.40168…
    ## $ m17_prop_alu_7a3_pri_grupo [3m[38;5;246m<dbl+lbl>[39m[23m 2, 3, 3, 2, 2, 3, 2, 3, 3, 3, 3, 2, 2, …
    ## $ var_strat                  [3m[38;5;246m<dbl>[39m[23m 2132, 2132, 2132, 2132, 2132, 1132, 2132, 2…
    ## $ var_unit                   [3m[38;5;246m<dbl>[39m[23m 25496, 24898, 25027, 9897, 8945, 8490, 1019…
    ## $ wgt_alu                    [3m[38;5;246m<dbl>[39m[23m 102.25614, 72.40751, 63.29539, 38.56127, 60…
    ## $ victim_vida_cuenta         [3m[38;5;246m<dbl>[39m[23m 12, 12, 8, 13, 12, 0, 13, 3, 9, 11, 15, 12,…
    ## $ victim_vida_cuenta_na      [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 19, 0, 0, 0, 1, 0, 1, 0, 0, …
    ## $ victim_ano_cuenta          [3m[38;5;246m<dbl>[39m[23m 8, 9, 2, 7, 3, 0, 5, 1, 6, 7, 9, 3, 2, 4, 4…
    ## $ victim_ano_cuenta_na       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 19, 0, 0, 0, 1, 0, 0, 0, 0, …
    ## $ poli_vida                  [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  2,  2, NA,  2,  2,  2,  2,…
    ## $ poli_año                   [3m[38;5;246m<dbl+lbl>[39m[23m  2,  1,  2,  2,  2, NA,  2,  2,  2,  2,…
    ## $ todas_al_menos_vida        [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 2, 1, 1, 1, 1, 1, 1, 1, …
    ## $ todas_al_menos_año         [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 2, 1, 1, 1, 1, 1, 1, 1, …
    ## $ A1_una_en_vida             [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 2, 1, 2, 1, 1, 1, 1, 1, 1, 2, …
    ## $ A2_una_en_vida             [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 2, 1, 1, 2, 1, 2, 1, 2, 1, 1, 2, …
    ## $ B_una_en_vida              [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 2, 1, 1, 2, 1, 2, 2, 1, 1, 1, 2, …
    ## $ C_una_en_vida              [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 1, 1, 2, 1, 2, 1, 1, 1, 1, 2, …
    ## $ D_una_en_vida              [3m[38;5;246m<dbl+lbl>[39m[23m  2,  1,  2,  1,  1, NA,  1,  2,  2,  2,…
    ## $ E1_una_en_vida             [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  1,  1,  1, NA,  1,  1,  1,  1,…
    ## $ E2_una_en_vida             [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  2,  2, NA,  2,  2,  2,  2,…
    ## $ F_una_en_vida              [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  1,  1,  1, NA,  1,  2,  2,  1,…
    ## $ A1_una_en_año              [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 1, 2, 2, 2, 1, 2, 1, 1, 1, 2, 2, …
    ## $ A2_una_en_año              [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 2, 1, 2, 2, 1, 2, 1, 2, 1, 1, 2, …
    ## $ B_una_en_año               [3m[38;5;246m<dbl+lbl>[39m[23m 1, 2, 2, 1, 2, 2, 1, 2, 2, 1, 1, 1, 2, …
    ## $ C_una_en_año               [3m[38;5;246m<dbl+lbl>[39m[23m 1, 1, 2, 1, 2, 2, 1, 2, 1, 1, 2, 1, 2, …
    ## $ D_una_en_año               [3m[38;5;246m<dbl+lbl>[39m[23m  2,  1,  2,  1,  2, NA,  2,  2,  2,  2,…
    ## $ E1_una_en_año              [3m[38;5;246m<dbl+lbl>[39m[23m  1,  1,  1,  1,  1, NA,  2,  1,  1,  1,…
    ## $ E2_una_en_año              [3m[38;5;246m<dbl+lbl>[39m[23m  2,  2,  2,  2,  2, NA,  2,  2,  2,  2,…
    ## $ F_una_en_año               [3m[38;5;246m<dbl+lbl>[39m[23m  2,  1,  2,  2,  1, NA,  1,  2,  2,  2,…
    ## $ pa1l                       [3m[38;5;246m<dbl>[39m[23m 1, 0, 1, 0, 0, 0, 0, 0, 1, 1, 1, NA, 0, 1, …
    ## $ pa2l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0…
    ## $ pa3l                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 0, 0, 0…
    ## $ pa4l                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 0, 0, 0, 0, 1, 0, 1, NA, 1, 1, 0, 0, …
    ## $ pa5l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 0, 0, 0, 1…
    ## $ pa6l                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 0, 0, 1, 0, 1, 1, 1, 1, 1, 1, 0, 1, 0…
    ## $ pa7l                       [3m[38;5;246m<dbl>[39m[23m 0, 1, 0, 1, 1, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ pb1l                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 0, 1, 1, 0, 1, 0, 0, 1, 0, 1, 0, 1, 0…
    ## $ pb2l                       [3m[38;5;246m<dbl>[39m[23m 1, 0, 0, 0, 1, 0, 1, 0, 0, 0, 1, 1, 0, 1, 0…
    ## $ pb3l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ pb4l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ pc1l                       [3m[38;5;246m<dbl>[39m[23m 1, 0, 1, 1, 1, 0, 0, 0, 1, 0, 1, 0, 0, 1, 0…
    ## $ pc2l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0…
    ## $ pc3l                       [3m[38;5;246m<dbl>[39m[23m 0, 1, 1, 1, 0, NA, 1, 0, 0, 1, 0, 1, 0, 1, …
    ## $ pc4l                       [3m[38;5;246m<dbl>[39m[23m 0, 1, 1, 1, 0, NA, 1, 0, 0, 0, 0, 0, 0, 1, …
    ## $ pc5l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, NA, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ pd1l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 1, 0, NA, 0, 0, 0, 0, 1, 0, 0, 0, …
    ## $ pd2l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, NA, 1, 0, 0, 0, 0, 1, 0, 0, …
    ## $ pd3l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 1, NA, 0, 0, 0, 0, 0, 1, 0, 0, …
    ## $ pd4l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 1, 0, NA, 0, 0, 0, 0, 0, 1, 0, 0, …
    ## $ pd5l                       [3m[38;5;246m<dbl>[39m[23m 0, 1, 0, 0, 0, NA, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ pd6l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 1, 0, NA, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ pd7l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 1, 0, NA, 0, 0, 0, 0, 0, 1, 0, 0, …
    ## $ pe1l                       [3m[38;5;246m<dbl>[39m[23m 1, 0, 0, 0, 0, NA, 0, 1, 1, 1, 1, 0, 0, 1, …
    ## $ pe2l                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, NA, 1, 0, 1, 1, 1, 0, 1, 1, …
    ## $ pe3l                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, NA, 1, 1, 1, 1, 1, 0, 0, 0, …
    ## $ pe4l                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, NA, 1, 0, 0, 1, 1, 0, 1, 1, …
    ## $ pe5l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 1, NA, 1, 0, 1, 0, 1, 0, 0, 1, …
    ## $ pe6l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, NA, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ pe7l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 0, NA, 0, 0, 0, 0, 0, 1, 0, 0, …
    ## $ pf1l                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 0, NA, 1, 0, 0, 1, 0, 0, 0, 0, …
    ## $ pf2l                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 0, 0, 1, NA, 0, 0, 0, 0, 0, 1, 0, 1, …
    ## $ pa1y                       [3m[38;5;246m<dbl>[39m[23m 0, 1, NA, 1, 1, 1, 1, 1, 1, 0, NA, 1, 1, 0,…
    ## $ pa2y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, NA, 1, 1, 1, …
    ## $ pa3y                       [3m[38;5;246m<dbl>[39m[23m 1, 0, 1, 1, 1, 1, 1, 1, 1, 0, 1, 1, 1, 1, 1…
    ## $ pa4y                       [3m[38;5;246m<dbl>[39m[23m 0, NA, 1, 1, 1, 1, 1, 1, 0, NA, NA, NA, 1, …
    ## $ pa5y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 1, 1, 1, N…
    ## $ pa6y                       [3m[38;5;246m<dbl>[39m[23m 0, 0, 1, 1, 1, 1, 0, 1, 0, 1, NA, 1, 1, 1, …
    ## $ pa7y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, NA, 1, 1, NA, 1, 1, 1, 1, 1, 1, 1,…
    ## $ pb1y                       [3m[38;5;246m<dbl>[39m[23m NA, 1, 1, NA, 1, 1, NA, 1, 1, NA, 1, NA, 1,…
    ## $ pb2y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, NA, 1, 1, 1, …
    ## $ pb3y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ pb4y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ pc1y                       [3m[38;5;246m<dbl>[39m[23m 0, 1, 1, 1, 1, 1, 1, 1, 0, 1, 1, 1, 1, 0, 1…
    ## $ pc2y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ pc3y                       [3m[38;5;246m<dbl>[39m[23m 1, NA, 1, 0, 1, NA, NA, 1, 1, 0, 1, 0, 1, 1…
    ## $ pc4y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, NA, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ pc5y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, NA, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ pd1y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, NA, 1, NA, 1, 1, 1, 1, NA, 1, 1, 1…
    ## $ pd2y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, NA, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ pd3y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, NA, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ pd4y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, NA, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ pd5y                       [3m[38;5;246m<dbl>[39m[23m 1, 0, 1, 1, 1, NA, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ pd6y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, NA, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ pd7y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, NA, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ pe1y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, NA, 1, 1, 1, 1, NA, 1, 1, 1,…
    ## $ pe2y                       [3m[38;5;246m<dbl>[39m[23m NA, NA, NA, NA, NA, NA, 1, 1, NA, NA, NA, 1…
    ## $ pe3y                       [3m[38;5;246m<dbl>[39m[23m NA, NA, 1, 0, NA, NA, 1, NA, NA, NA, 1, 1, …
    ## $ pe4y                       [3m[38;5;246m<dbl>[39m[23m 0, NA, 1, 0, 1, NA, 1, 1, 1, NA, 1, 1, 0, 1…
    ## $ pe5y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, NA, 1, 1, 0, 1, 1, 1, 1, 1, …
    ## $ pe6y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, NA, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ pe7y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, NA, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ pf1y                       [3m[38;5;246m<dbl>[39m[23m 1, 0, 1, 1, 1, NA, NA, 1, 1, 1, 1, 1, 1, 1,…
    ## $ pf2y                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 0, NA, 1, 1, 1, 1, 1, 1, 1, 0, …
    ## $ id_k                       [3m[38;5;246m<dbl>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ id_s                       [3m[38;5;246m<dbl>[39m[23m 2132, 2132, 2132, 2132, 2132, 1132, 2132, 2…
    ## $ id_j                       [3m[38;5;246m<dbl>[39m[23m 25496, 24898, 25027, 9897, 8945, 8490, 1019…
    ## $ id_i                       [3m[38;5;246m<int>[39m[23m 14489, 2489, 5126, 3271, 15048, 18134, 1235…
    ## $ ws                         [3m[38;5;246m<dbl>[39m[23m 0.09195197, 0.06511113, 0.05691722, 0.03467…
    ## $ depresion                  [3m[38;5;246m<dbl>[39m[23m 1, 0, 1, 1, 0, NA, 1, 0, 0, 0, 1, 1, 0, 0, …
    ## $ sexo                       [3m[38;5;246m<chr>[39m[23m "mujeres", "mujeres", "hombres", "hombres",…

``` r
#--------------------------------------
# tabla de contingencia
#--------------------------------------

# metodo 1
prop.table(xtabs(~ depresion + sexo, data = data_model), 2)
```

    ##          sexo
    ## depresion    hombres    mujeres
    ##         0 0.92756904 0.77780168
    ##         1 0.07243096 0.22219832

``` r
# Nota: por convención, las tablas de contigencia incluyen a la variable de respuesta
#       entre las filas, como en el metodo 1.
```

## Ejercicio 11. Promedio por grupo.

- La polivictimización (variable `poli_vida`) es un factor de riesgo de
  calidad de vida grave. Esta, identifica a las personas que han
  vivenciado diferentes formas de violencia durante su trayectoria
  vital. Esto puede incluir asaltos con violencia, abusos por parte de
  cuidadores, por parte de pares, abuso sexual, entre otras formas de
  acoso.

- Qué proporcion de “polivictimas” y “no polivictimas” se encontraría en
  riesgo de depresión (19 puntos o más).

``` r
#------------------------------------------------------------------------------
# promedio por grupo de dummy
#------------------------------------------------------------------------------

#--------------------------------------
# depresion
#--------------------------------------

data_model %>%
group_by(poli_vida) %>%
summarize(
media   = mean(depresion, na.rm = TRUE)
) %>%
knitr::kable(., digits = 2)
```

| poli_vida | media |
|----------:|------:|
|         1 |  0.43 |
|         2 |  0.11 |
|        NA |  0.20 |
