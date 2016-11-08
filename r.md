# R

https:\/\/www.r-project.org\/

Bases

Fonctions

sum\(1,3,5\)

rep\("Yo ho!", times = 3\)

## Vector

v &lt;- c\(1,2,3\)

seq\(1,10,0.5\)

names\(v\)&lt;-c\("un","deux","trois"\)

### Visualisation

barplot\(vector\)

plot\(vector\)

## Matrices

matrix\(init,nb lignes, nb de colonnes\)

ou matrix\(vector,nb lignes, nb de colonnes\)

matrix\(0,3,4\)

dim: assigner le nb de lignes et de colonnes

p&lt;-1:8

dim\(p\)&lt;-c\(2,4\)

p\[2,3\]

ligne entiere

p\[2,\]

plusieurs colonnes

p\[,2:4\]

### Visualisation

contour\(matrix\)

Vue 3D

persp\(matrix\)

persp\(matrix, expand=0.2\)

Carte de chaleur

image\(matrix\)

## Statistics

mean\(vector\)

barplot\(vector\)

If we draw a line on the plot representing the mean, we can easily compare the various values to the average. The `abline` function can take an `h` parameter with a value at which to draw a horizontal line, or a `v` parameter for a vertical line.

abline\(h = mean\(vector\)\)

median\(vector\)

Statisticians use the concept of "standard deviation" from the mean to describe the range of typical values for a data set. For a group of numbers, it shows how much they typically vary from the average value. To calculate the standard deviation, you calculate the mean of the values, then subtract the mean from each number and square the result, then average those squares, and take the square root of that average.

sd\(vector\)

## Factors

Pour grouper par catégorie

factor\(vector\)

levels\(vector\)

Utiliser différents items pour les points avec pch:

types&lt;-factor\(vector\)

plot\(x,y, pch=as.integer\(types\)\)

La légende:

legend\(position, vector, pch\)

legend\("topright", c\("gems", "gold", "silver"\), pch=1:3\)

## Data Frames

Pour structurer les données \(comme dans une BD ou une feuille excel\)

treasure &lt;- data.frame\(weights, prices, types\)

Pour accéder aux données d'une colonne

treasure\[\["weights"\]\] ou treasure$weights

## I\/O

### Charger des fichiers

read.csv\("targets.csv"\)

read.table\("infantry.txt", sep="\t", header=TRUE\)

### Merger des fichiers

piracy &lt;- read.csv\("piracy.csv"\)

gdp &lt;- read.table\("gdp.txt", sep="\t", header=TRUE\)

countries&lt;-merge\(x = gdp, y = piracy\)

## Statistiques

### Tester la corrélation

Tester la corrélation entre 2 vecteurs:

cor.test\(countries$GDP, countries$Piracy\)

## Prédiction

We have more countries represented in our GDP data than we do our piracy rate data. If we know a country's GDP, can we use that to estimate its piracy rate?

We can, if we calculate the linear model that best represents all our data points \(with a certain degree of error\). The `lm` function takes a _model formula_, which is represented by a _response variable_ \(piracy rate\), a tilde character \(`~`\), and a _predictor variable_ \(GDP\). \(Note that the response variable comes _first_.\)

line &lt;- lm\(countries$Piracy ~ countries$GDP\)

## Packages

### Installer un package

install.packages\("ggplot2"\)

help\(package = "ggplot2"\)

library\("ggplot2"\)

