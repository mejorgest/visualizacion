# visualizacion

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt



iris = pd.read_csv("../../../datos/iris_v1.csv", sep = ";")
iris


#Para observar las partes del gráfico vamos a utilizar los siguientes datos de ejemplo:

x, y = [1, 2, 3, 4], [1, 4, 2, 3]

#Podemos verlo como el contenedor completo de la figura o gráfico. Aquí se van a almacenar cada uno de los ejes, elementos especiales como los títulos y las leyendas, así como también otras figuras.
fig, ax = plt.subplots()
plt.show()

#El Axes es un Artist que se añade a la Figura. Es aquí donde se define el gráfico a dibujar y generalmente esta asociado a 2 objetos Axis, aunque podrían ser 3 (para gráficos en 3D). Se puede definir, ademas del #gráfico, elementos como el título, la etiqueta del eje x, la etiqueta del eje y, etc.


fig, ax = plt.subplots()

ax.plot(x, y)
no_print = ax.set_title("Este es el título")
no_print = ax.set_xlabel("Este es el eje X")
no_print = ax.set_ylabel("Este es el eje Y")

plt.show()


#Los objetos Axis definen la escala, los limites del gráfico, los ticks y los tickslabels.


fig, ax = plt.subplots()

ax.plot(x, y)
no_print = ax.set_title("Este es el título")
no_print = ax.set_xlabel("Este es el eje X")
no_print = ax.set_ylabel("Este es el eje Y")

no_print = ax.set_xlim(0, 10)
no_print = ax.set_xticks(range(0, 11, 2), ['A', 'B', 'C', 'D', 'E', 'F'], rotation = 20)
#ax.set_xticklabels(['A', 'B', 'C', 'D', 'E', 'F'])

no_print = ax.set_ylim(-3, 5)
no_print = ax.set_yticks([0, 1, 2, 3])

plt.show()

#Se refiere a todo lo visible en el gráfico o figura.
fig, ax = plt.subplots()

ax.plot(x, y)
no_print = ax.set_title("Este es el título")
no_print = ax.set_xlabel("Este es el eje X")
no_print = ax.set_ylabel("Este es el eje Y")

no_print = ax.set_xlim(0, 10)
no_print = ax.set_xticks(range(0, 11, 2), ['A', 'B', 'C', 'D', 'E', 'F'], rotation = 20)
no_print = ax.set_xticklabels(['A1', 'B2', 'C3', 'D4', 'E5', 'F6'])

no_print = ax.set_ylim(-3, 5)
no_print = ax.set_yticks([0, 1, 2, 3])

plt.show()

#lineas: Este es el tipo de gráfico más básico, en el caso de Matplotlib basta con utilizar el método plot.

x, y = [1, 2, 3, 4], [1, 4, 2, 3]

fig, ax = plt.subplots()

ax.plot(x, y)

plt.show()


#dispersion También conocido como scatter, para ello debemos llamar al método scatter.

x, y = [1, 2, 3, 4], [1, 4, 2, 3]

fig, ax = plt.subplots()

ax.scatter(x, y)

plt.show()

#Para los gráficos de barra contamos con 2 instrucciones: bar para graficar de forma vertical y barh para graficar de forma horizontal.

aux = iris.groupby('tipo')['s_largo'].mean().reset_index()
aux
#Vertical
x = aux.tipo
y = aux.s_largo

fig, ax = plt.subplots()

no_print = ax.bar(x, y, width = 1, edgecolor = "white", linewidth = 1.5)

plt.show()



#Horizontal
fig, ax = plt.subplots()

no_print = ax.barh(x, y, height = 1, edgecolor = "white", linewidth = 1.5)

plt.show()

#estilo de barra 

fig, ax = plt.subplots()

bar1 = ax.bar(x, y, width = 1, edgecolor = "white", linewidth = 1.5, color = "pink")

no_print = ax.bar_label(bar1, padding = 3) # Agregar texto del valor

plt.show()


#agrupar
df = iris.copy()
df["tam_s_ancho"] = ["ancho" if x > 3 else "angosto" for x in df.s_ancho]
aux = df.groupby(['tipo', 'tam_s_ancho'])['s_largo'].mean().reset_index()
aux

etq = aux.tipo.unique()
x = np.arange(len(etq))
grupo_ancho   = aux.loc[aux.tam_s_ancho == 'ancho', 's_largo'].values
grupo_angosto = aux.loc[aux.tam_s_ancho == 'angosto', 's_largo'].values

width = 0.35

fig, ax = plt.subplots()

no_print = ax.bar(x - width/2, grupo_ancho, width = width, edgecolor = "white", linewidth = 1.5)
no_print = ax.bar(x + width/2, grupo_angosto, width = width, edgecolor = "white", linewidth = 1.5)
no_print = ax.set_xticks(x, etq)

plt.show()

#histgrama Para un histograma utilizaremos la función hist.
y = iris.s_ancho

fig, ax = plt.subplots()
no_print = ax.hist(y, bins = 30, linewidth = 0.5, edgecolor = "white", color = "darkgreen")
plt.show()


#boxplot Para un Boxplot utilizaremos la función boxplot.

y = iris.s_ancho

fig, ax = plt.subplots()
no_print = ax.boxplot(y, widths = 0.5, patch_artist = True,
           flierprops = {'marker': 'x', 'markersize': 10, 'markeredgecolor': 'darkred'}, # Estilo del punto
           medianprops = {"color": "white", "linewidth": 2}, # Estilo de la línea del promedio
           boxprops = {"facecolor": "darkblue", "edgecolor": "white", "linewidth": 0.5}, # Estilo de la caja
           whiskerprops = {"color": "darkblue", "linewidth": 1.5}, # Estilo de las líneas verticales
           capprops={"color": "darkblue", "linewidth": 1.5} # Estilo de las líneas horizontales
          )
plt.show()


#Se puede pasar un data.frame, este debe contener solo variables numéricas.
aux = iris.drop(columns = ["tipo"])

fig, ax = plt.subplots()
no_print = ax.boxplot(aux, widths = 0.5, patch_artist = True,
           flierprops = {'marker': 'x', 'markersize': 10, 'markeredgecolor': 'darkred'}, # Estilo del punto
           medianprops = {"color": "white", "linewidth": 2}, # Estilo de la línea del promedio
           boxprops = {"facecolor": "darkblue", "edgecolor": "white", "linewidth": 0.5}, # Estilo de la caja
           whiskerprops = {"color": "darkblue", "linewidth": 1.5}, # Estilo de las líneas verticales
           capprops={"color": "darkblue", "linewidth": 1.5} # Estilo de las líneas horizontales
          )
no_print = ax.set_xticks(range(1, 5), aux.columns)
plt.show()

#circular Para realizar el gráfico circular, también conocido como pie o pastel, vamos a utilizar la función pie.

aux = iris.groupby('tipo')['s_largo'].mean().reset_index()
aux

x = aux.tipo
y = aux.s_largo

# plot
fig, ax = plt.subplots()
no_print = ax.pie(y,
       labels = x, # Etiquetas
       colors = ["pink", "orange", "red", "darkred"], # Colores
       radius = 2, # Radio del circulo.
       center = (3, 3), # Punto central donde dibujar el circulo.
       wedgeprops = {"linewidth": 1.5, "edgecolor": "white"}, # Estilo del borde
       frame = True # Centrar el gráfico
      )

plt.show()

#Matplotlib provee un conjunto de temas que podemos utilizar, algunos de ellos son:

plt.style.use('fivethirtyeight')
fig, ax = plt.subplots()
ax.plot([1, 2, 3, 4, 5], [5, 4, 3, 2, 1], '-->')
plt.show()

plt.style.use('ggplot')
fig, ax = plt.subplots()
ax.plot([1, 2, 3, 4, 5], [5, 4, 3, 2, 1], '-->')
plt.show()

plt.style.use('bmh')
fig, ax = plt.subplots()
ax.plot([1, 2, 3, 4, 5], [5, 4, 3, 2, 1], '-->')
plt.show()

plt.style.use('dark_background')
fig, ax = plt.subplots()
ax.plot([1, 2, 3, 4, 5], [5, 4, 3, 2, 1], '-->')
plt.show()

plt.style.use('grayscale')
fig, ax = plt.subplots()
ax.plot([1, 2, 3, 4, 5], [5, 4, 3, 2, 1], '-->')
plt.show()

plt.style.use('classic')
fig, ax = plt.subplots()
ax.plot([1, 2, 3, 4, 5], [5, 4, 3, 2, 1], '-->')
plt.show()

plt.style.use('default')
fig, ax = plt.subplots()
ax.plot([1, 2, 3, 4, 5], [5, 4, 3, 2, 1], '-->')
plt.show()

#La leyenda nos ayuda a identificar elementos en el gráfico. Por tanto, es muy importante saber como utilizarla.

#Definir la leyenda
#Cuando agregamos varios gráficos podemos agregar el parámetro label para nombrar cada uno de esos gráficos. De esta manera solo tendremos que invocar a la función legend.


df = iris.copy()
df["tam_s_ancho"] = ["ancho" if x > 3 else "angosto" for x in df.s_ancho]
aux = df.groupby(['tipo', 'tam_s_ancho'])['s_largo'].mean().reset_index()
etq = aux.tipo.unique()
x = np.arange(len(etq))
grupo_ancho   = aux.loc[aux.tam_s_ancho == 'ancho', 's_largo'].values
grupo_angosto = aux.loc[aux.tam_s_ancho == 'angosto', 's_largo'].values

width = 0.35

fig, ax = plt.subplots()

no_print = ax.bar(x - width/2, grupo_ancho, width = width, edgecolor = "white", linewidth = 1.5, label = "Ancho")
no_print = ax.bar(x + width/2, grupo_angosto, width = width, edgecolor = "white", linewidth = 1.5, label = "Angosto")
no_print = ax.set_xticks(x, etq)

no_print = ax.legend(title = "Grupos")

plt.show()

#En ocasiones se puede presentar un solo gráfico, pero que contiene multiples categorías.

aux = iris.groupby('tipo')['s_largo'].mean().reset_index()
x = aux.tipo
y = aux.s_largo

# plot
fig, ax = plt.subplots()
no_print = ax.pie(
  y,
  colors = ["pink", "orange", "red"], # Colores
  radius = 2, # Radio del circulo.
  center = (3, 3), # Punto central donde dibujar el circulo.
  wedgeprops = {"linewidth": 1.5, "edgecolor": "white"}, # Estilo del borde
  frame = True # Centrar el gráfico
)

no_print = ax.legend(labels = x)

no_print = plt.axis('off') # Eliminar ejes
plt.show()

#Posicionar la leyenda
#Para posicionar la leyenda podemos utilizar el parámetro loc.

#loc: Con este parámetro indicamos en que lugar queremos la leyenda, los posibles valores son: ‘best’, ‘upper right’, ‘upper left’, ‘lower left’, ‘lower right’, ‘right’, ‘center left’, ‘center right’, ‘lower #center’, ‘upper center’, ‘center’. También puede ser un par ordenado.

#Utilizando un valor de posición.


aux = iris.groupby('tipo')['s_largo'].mean().reset_index()
x = aux.tipo
y = aux.s_largo

# plot
fig, ax = plt.subplots()
no_print = ax.pie(
  y,
  colors = ["pink", "orange", "red"], # Colores
  radius = 2, # Radio del circulo.
  center = (3, 3), # Punto central donde dibujar el circulo.
  wedgeprops = {"linewidth": 1.5, "edgecolor": "white"}, # Estilo del borde
  frame = True # Centrar el gráfico
)

no_print = ax.legend(labels = x, loc = "upper right")

no_print = plt.axis('off') # Eliminar ejes
plt.show()

#Utilizando un valor de par ordenado.

df = iris.copy()
df["tam_s_ancho"] = ["ancho" if x > 3 else "angosto" for x in df.s_ancho]
aux = df.groupby(['tipo', 'tam_s_ancho'])['s_largo'].mean().reset_index()
etq = aux.tipo.unique()
x = np.arange(len(etq))
grupo_ancho   = aux.loc[aux.tam_s_ancho == 'ancho', 's_largo'].values
grupo_angosto = aux.loc[aux.tam_s_ancho == 'angosto', 's_largo'].values

width = 0.35

fig, ax = plt.subplots()

no_print = ax.bar(x - width/2, grupo_ancho, width = width, edgecolor = "white", linewidth = 1.5, label = "Ancho")
no_print = ax.bar(x + width/2, grupo_angosto, width = width, edgecolor = "white", linewidth = 1.5, label = "Angosto")
no_print = ax.set_xticks(x, etq)

no_print = ax.legend(title = "Grupos", loc = (1.05, 0.8))

plt.tight_layout() # Agregar esta instrucción para ajustar el gráfico y la leyenda.
plt.show()


#El paquete seaborn es otra librería de visualización que se basa en Matplotlib. Esta librería depende de Matplotlib y en ocasiones utiliza varios de los componentes de Matplotlib para realizar gráficos.

#pip install seaborn
#Una vez instalado podemos empezar a usarlo cargandolo de la siguiente manera:

#import seaborn as sns

plt.style.use('seaborn-v0_8')


#lineas

fig, ax = plt.subplots()
sns.lineplot(x = range(150), y = iris.s_largo, hue = iris.tipo, ax = ax)
ax.legend(loc = "upper left")
plt.show()
#dispersion
fig, ax = plt.subplots()
sns.scatterplot(x = iris.s_ancho, y = iris.s_largo, hue = iris.tipo, 
                size = iris.p_ancho, alpha = 0.6, ax = ax)
ax.legend(loc = "upper right")
plt.show()

#barras
tam_s_largo = ["ancho" if x > 3 else "angosto" for x in iris.s_ancho]

fig, ax = plt.subplots()
sns.barplot(x = iris.tipo, y = iris.s_largo, hue = tam_s_largo, ax = ax)
ax.legend(loc = "upper left")
plt.show()


#histograma 

fig, ax = plt.subplots()
sns.histplot(x = iris.s_ancho, ax = ax)
plt.show()


#boxplot

fig, ax = plt.subplots()
sns.boxplot(x = iris.s_ancho, ax = ax)
plt.show()

#mapa de calor 
corr = iris.iloc[:, 0:4].corr()

fig, ax = plt.subplots()
sns.heatmap(corr, annot = True, vmin = -1, vmax = 1, cmap = 'RdBu', ax = ax)
plt.show()

#grafico de pares 

sns.pairplot(iris, hue = "tipo")
