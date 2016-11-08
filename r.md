# R

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

