# Analisis de Tienda

Se genera un analisis para poder observar que tiene tiene un menor ingreso en facturacion y realizar una comparativa 

Se genera la conexion del origen de los datos

```
url = "https://raw.githubusercontent.com/alura-es-cursos/challenge1-data-science-latam/refs/heads/main/base-de-datos-challenge1-latam/tienda_1%20.csv"
url2 = "https://raw.githubusercontent.com/alura-es-cursos/challenge1-data-science-latam/refs/heads/main/base-de-datos-challenge1-latam/tienda_2.csv"
url3 = "https://raw.githubusercontent.com/alura-es-cursos/challenge1-data-science-latam/refs/heads/main/base-de-datos-challenge1-latam/tienda_3.csv"
url4 = "https://raw.githubusercontent.com/alura-es-cursos/challenge1-data-science-latam/refs/heads/main/base-de-datos-challenge1-latam/tienda_4.csv"
```

Se genera un dataframe con pandas, para poder realizar el analisi de los datos 
```
import pandas as pd

tienda = pd.read_csv(url)
tienda2 = pd.read_csv(url2)
tienda3 = pd.read_csv(url3)
tienda4 = pd.read_csv(url4)

tienda.head()
```

Para realizar un mejor analisis y una mejor comparativa se creo dos columnas en el df para una con la clasificacion de las tiendas, otro con las facturacion mas el costo de envio
```
tienda['Tienda'] = 'T1'
tienda2['Tienda'] = 'T2'
tienda3['Tienda'] = 'T3'
tienda4['Tienda'] = 'T4'

tienda['Facturacion'] = tienda['Precio'] + tienda['Costo de envío']
tienda2['Facturacion'] = tienda2['Precio'] + tienda2['Costo de envío']
tienda3['Facturacion'] = tienda3['Precio'] + tienda3['Costo de envío']
tienda4['Facturacion'] = tienda4['Precio'] + tienda4['Costo de envío']
```

Se genera un append para unir todas las tiendas y realizar un mejor analisis
```
Tiendas = pd.concat([tienda, tienda2, tienda3, tienda4])
Tiendas.head()
```
### Uso de funciones y listas

el metodo de analisi fue a vase de listas creadas en pandas para y un mejor desarrollo y uso de funciones ya predeterminadas del mismo python
```
facturacion_por_tienda = Tiendas.groupby('Tienda')['Facturacion'].sum()
facturacion_por_tienda = facturacion_por_tienda / 1000000

lista = facturacion_por_tienda.sort_values(ascending=False)
lista
```

## Graficos

se crean diferentes graficos vasados en los analisis para una mejor visualizacion y comparativa de las tiendas


### Graficos de Barras
```
plt.figure(figsize=(12, 6))
plt.bar(calificacion_promedio.index, calificacion_promedio.values, color=['#1f77b4', '#ff7f0e', '#2ca02c', '#d62728'], width=0.8)
plt.xlabel("Categoría")
plt.ylabel("Ventas")
plt.title("Ventas por Categoría")
plt.xticks(rotation=0, ha='right')

for i, v in enumerate(calificacion_promedio.values):
    plt.text(i, v, f"{v:.2f}", ha='center')

plt.tight_layout()
plt.show()

```
![alt text](image.png)

### Grafico de puntos comparativos

```
ventas_tabla = ventas_tabla[ordenar_mes]

plt.figure(figsize=(12, 6))

for tienda in ventas_tabla.index:
    plt.plot(ventas_tabla.columns, ventas_tabla.loc[tienda], label=tienda, marker='o')

plt.xlabel("Mes")
plt.ylabel("Facturación")
plt.title("Tienda vs Mes")
plt.legend()
plt.grid(True)
```
![alt text](image-1.png)

## Tablero

Se creo un tablero para una mejor visualizacion de todo el analisi y que se tenga una mejor comprencion de todas los graficos generados

![alt text](image-2.png)



#### recursos

```
fig = make_subplots(rows=3, cols=2, subplot_titles=("Facturación por Tienda", "Facturación Mensual","Ventas por Categoría", "Ventas por Categoría y Tienda","Calificación Promedio", "Calificación Mensual"))
```

se utiliza **make_subplots** para poder generar el tablero dependiendo de la necesidades **rows=3** las cantidad de filas que va tener el lienzo **cols=2** cantidad de columans va a tener tu lienzo eso te ayudara a poder colocar los graficos a donde quieras mas personalizado

> [!NOTE]
> las funciones principales de esta desarollo es que se pueden modificar a la necesidad del negocio o a la cantidad de origenes de datos para llegar a un mejor analisis ya que se utilizaron recursos que estan dento del mismo colab que no se nesesita modificar un ambiente especial
