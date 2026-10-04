# Proyecto análisis de venta en python

# Limpieza y Análisis de Datos

## Descripción del proyecto

Este proyecto corresponde a un proceso de **limpieza, transformación y análisis exploratorio de datos de ventas**, desarrollado utilizando **Python y Pandas** en Google Colab.

El objetivo principal es transformar una base de datos de ventas con información incompleta, valores nulos y registros duplicados en un conjunto de datos limpio y estructurado, preparado para realizar análisis posteriores y obtener indicadores relevantes para la toma de decisiones.

El proyecto forma parte del desarrollo de habilidades en **Python y análisis de datos**.

---

## 🎯 Objetivos

- Importar y explorar una base de datos de ventas.
- Identificar problemas de calidad en los datos.
- Detectar y tratar valores nulos.
- Identificar y gestionar registros duplicados.
- Revisar y corregir tipos de datos.
- Validar la consistencia de las variables.
- Crear y validar métricas de ventas.
- Realizar análisis exploratorio de los datos.
- Obtener información relevante sobre ventas, productos, sucursales, canales y vendedores.
- Generar una base de datos limpia para futuros análisis y visualizaciones.

---

## 🗂️ Dataset

El proyecto utiliza una base de datos de ventas con **650 registros y 15 variables**.

### Variables principales

| Variable | Descripción |
|---|---|
| `ID_Venta` | Identificador único de la venta |
| `Fecha` | Fecha en que se realizó la venta |
| `Sucursal` | Sucursal donde se realizó la venta |
| `Categoría` | Categoría del producto |
| `Producto` | Producto vendido |
| `Canal` | Canal utilizado para realizar la venta |
| `Vendedor` | Vendedor asociado a la operación |
| `Cliente_ID` | Identificador del cliente |
| `Unidades` | Cantidad de unidades vendidas |
| `Precio_Unitario` | Precio unitario del producto |
| `Descuento` | Descuento aplicado a la venta |
| `Costo_Unitario` | Costo unitario del producto |
| `Metodo_Pago` | Método de pago utilizado |
| `Estado_Entrega` | Estado de entrega del pedido |
| `Total_Venta` | Valor total de la venta |

---

## 🛠️ Tecnologías utilizadas

- Python
- Excel
- Google Colab

### Librerías principales

- import pandas as pd
- import numpy as np
- import Matplotlib as plt

---

# 🔄 Flujo del proyecto

El proyecto se desarrolló siguiendo las siguientes etapas:

1. Importación de librerías.
2. Carga del archivo Excel.
3. Exploración inicial de los datos.
4. Revisión de estructura y tipos de datos.
5. Identificación de valores nulos.
6. Identificación de registros duplicados.
7. Limpieza de datos.
8. Validación de la información.
9. Creación y validación de variables calculadas.
10. Análisis exploratorio.
11. Cálculo de indicadores.
12. Análisis de ventas y rentabilidad.
13. Obtención de conclusiones.

---

# Carga del archivo

El archivo Excel fue cargado en Google Colab utilizando Pandas.

~~~python
df = pd.read_excel("Datos_Proyecto_Intermedio.xlsx")
~~~

---

# Exploración inicial

Una vez cargado el dataset, se realizó una primera revisión para conocer su estructura.

~~~python
df.head()
~~~

También se revisaron las dimensiones del dataset:

~~~python
df.shape
~~~

Resultado inicial:

- 650 filas
- 15 columnas

---

# Revisión de columnas

Se revisaron los nombres de las variables disponibles.

~~~python
df.columns
~~~

Las columnas encontradas fueron:

`ID_Venta`, `Fecha`, `Sucursal`, `Categoría`, `Producto`, `Canal`, `Vendedor`, `Cliente_ID`, `Unidades`, `Precio_Unitario`, `Descuento`, `Costo_Unitario`, `Metodo_Pago`, `Estado_Entrega`, `Total_Venta`

---

# Información general del dataset

Se utilizó `info()` para revisar tipos de datos y valores no nulos.

~~~python
df.info()
~~~

Esta revisión permitió identificar las variables numéricas, categóricas y de fecha, además de detectar posibles problemas de calidad.

---

# Identificación de valores nulos

Se revisó la cantidad de valores faltantes por columna.

~~~python
df.isnull().sum()
~~~

Los valores nulos identificados inicialmente fueron:

| Columna | Valores nulos |
|---|---:|
| Fecha | 1 |
| Categoría | 1 |
| Producto | 2 |
| Canal | 1 |
| Vendedor | 3 |
| Precio_Unitario | 3 |
| Metodo_Pago | 1 |

Las demás variables no presentaron valores nulos.

---

# Identificación de duplicados

Se verificó la existencia de registros duplicados.

~~~python
df.duplicated().sum()
~~~

Se identificaron:

**4 registros duplicados.**

Estos registros fueron considerados durante el proceso de limpieza para evitar que afectaran los resultados del análisis.

---

# Limpieza de datos

Luego de identificar los problemas de calidad, se realizó el proceso de limpieza.

Entre las principales tareas realizadas estuvieron:

- Revisión de valores faltantes.
- Eliminación de registros duplicados.
- Revisión de tipos de datos.
- Validación de variables numéricas.
- Validación de variables categóricas.
- Revisión de consistencia de los cálculos.

Después del proceso de limpieza, el dataset quedó con:

**646 registros y 15 columnas.**

---

# Tratamiento de fechas

La columna `Fecha` fue revisada y convertida al formato correspondiente para facilitar posteriormente el análisis temporal.

~~~python
df["Fecha"] = pd.to_datetime(df["Fecha"], errors="coerce")
~~~

Esto permite realizar análisis por:

- Año
- Mes
- Día
- Periodos de venta

---

# Revisión de variables numéricas

Se revisaron las principales variables numéricas del dataset.

~~~python
df.describe()
~~~

Esta función permite analizar:

- Cantidad de registros.
- Promedio.
- Desviación estándar.
- Mínimo.
- Percentiles.
- Máximo.

Las variables revisadas incluyen:

- Unidades
- Precio_Unitario
- Descuento
- Costo_Unitario
- Total_Venta

---

# Validación de Total_Venta

Se verificó que el valor de `Total_Venta` tuviera relación con las variables utilizadas para calcularlo.

La fórmula utilizada fue:

`Total_Venta = Precio_Unitario × Unidades × (1 - Descuento)`

La lógica utilizada en Python fue:

~~~python
df["Total_Venta_Calculada"] = (
    df["Precio_Unitario"]
    * df["Unidades"]
    * (1 - df["Descuento"])
)
~~~

Posteriormente se compararon los valores calculados con los valores originales para validar la consistencia.

---

# Análisis de variables categóricas

Se revisaron las categorías principales del dataset.

Por ejemplo:

~~~python
df["Categoría"].value_counts()
~~~

También se analizaron otras variables categóricas como:

~~~python
df["Sucursal"].value_counts()
~~~

~~~python
df["Canal"].value_counts()
~~~

~~~python
df["Metodo_Pago"].value_counts()
~~~

~~~python
df["Estado_Entrega"].value_counts()
~~~

Esto permitió conocer la distribución de las ventas según diferentes dimensiones.

---

# Análisis de ventas

Se calculó el total de ventas:

~~~python
df["Total_Venta"].sum()
~~~

También se obtuvo el promedio:

~~~python
df["Total_Venta"].mean()
~~~

Y el valor máximo:

~~~python
df["Total_Venta"].max()
~~~

Estos indicadores permiten obtener una primera visión del comportamiento comercial.

---

# Análisis de unidades vendidas

Se calculó la cantidad total de unidades vendidas:

~~~python
df["Unidades"].sum()
~~~

También se analizó el promedio de unidades por venta:

~~~python
df["Unidades"].mean()
~~~

---

# Análisis de ventas por categoría

Se agrupó la información para conocer el desempeño de cada categoría.

~~~python
ventas_categoria = (
    df.groupby("Categoría")["Total_Venta"]
    .sum()
    .sort_values(ascending=False)
)

ventas_categoria
~~~

Este análisis permite identificar qué categorías concentran una mayor proporción de las ventas.

---

# Análisis de ventas por sucursal

Se analizaron las ventas por sucursal.

~~~python
ventas_sucursal = (
    df.groupby("Sucursal")["Total_Venta"]
    .sum()
    .sort_values(ascending=False)
)

ventas_sucursal
~~~

Esto permite comparar el desempeño comercial de las distintas sucursales.

---

# Análisis de ventas por canal

Se analizaron las ventas según el canal utilizado.

~~~python
ventas_canal = (
    df.groupby("Canal")["Total_Venta"]
    .sum()
    .sort_values(ascending=False)
)

ventas_canal
~~~

Este análisis permite determinar qué canales generan mayor volumen de ventas.

---

#  Análisis por vendedor

Se analizaron las ventas generadas por cada vendedor.

~~~python
ventas_vendedor = (
    df.groupby("Vendedor")["Total_Venta"]
    .sum()
    .sort_values(ascending=False)
)

ventas_vendedor
~~~

Esto permite identificar diferencias de desempeño entre vendedores.

---

# Análisis temporal

Se crearon variables relacionadas con el periodo de venta.

~~~python
df["Año"] = df["Fecha"].dt.year
df["Mes"] = df["Fecha"].dt.month
~~~

Posteriormente se pueden analizar las ventas por periodo:

~~~python
ventas_mes = (
    df.groupby(["Año", "Mes"])["Total_Venta"]
    .sum()
)

ventas_mes
~~~

Esto permite identificar tendencias y variaciones en el comportamiento de las ventas.

---

#  Análisis de rentabilidad

A partir del precio, costo y unidades se puede calcular el margen bruto.

Primero se calcula el costo total:

~~~python
df["Costo_Total"] = df["Costo_Unitario"] * df["Unidades"]
~~~

Luego se calcula el margen:

~~~python
df["Margen"] = df["Total_Venta"] - df["Costo_Total"]
~~~

Y finalmente el margen porcentual:

~~~python
df["Margen_%"] = (
    df["Margen"] / df["Total_Venta"]
) * 100
~~~

Este análisis permite complementar la visión de ventas con una perspectiva de rentabilidad.

---

# Indicadores principales

Los principales indicadores considerados en el análisis fueron:

### Ventas totales

~~~python
ventas_totales = df["Total_Venta"].sum()
~~~

### Unidades vendidas

~~~python
unidades_totales = df["Unidades"].sum()
~~~

### Ticket promedio

~~~python
ticket_promedio = df["Total_Venta"].mean()
~~~

### Costo total

~~~python
costo_total = df["Costo_Total"].sum()
~~~

### Margen total

~~~python
margen_total = df["Margen"].sum()
~~~

### Margen porcentual

~~~python
margen_porcentaje = (
    margen_total / ventas_totales
) * 100
~~~

---

# Visualización de datos

Para complementar el análisis se pueden utilizar gráficos con Matplotlib.

Ejemplo de ventas por categoría:

~~~python
ventas_categoria.plot(kind="bar")

plt.title("Ventas por Categoría")
plt.xlabel("Categoría")
plt.ylabel("Ventas")
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
~~~

<img width="630" height="470" alt="Ventas_Categoría" src="https://github.com/user-attachments/assets/29a49028-8ff0-4601-8a8e-5f07cbc359f1" />


Ejemplo de evolución temporal:

~~~python
ventas_mes.plot(kind="line")

plt.title("Evolución de las Ventas")
plt.xlabel("Periodo")
plt.ylabel("Ventas")
plt.tight_layout()
plt.show()
~~~

<img width="989" height="490" alt="Ventas_Mes" src="https://github.com/user-attachments/assets/4e69294e-3615-46ff-acae-438186b202ef" />

Otros gráficos de utilidad 

Top 10 productos 

<img width="989" height="590" alt="Top_10_productos" src="https://github.com/user-attachments/assets/8aeb1a24-c661-4907-b0cd-bf49290f20da" />

Ventas por canal

<img width="630" height="470" alt="Ventas_Canal" src="https://github.com/user-attachments/assets/e74194cb-ec76-4cef-af3e-42e57c9ebdbe" />


---

# Validación final

Antes de finalizar el análisis se realizó una revisión general del dataset.

~~~python
df.shape
~~~

~~~python
df.isnull().sum()
~~~

~~~python
df.duplicated().sum()
~~~

~~~python
df.info()
~~~

Estas comprobaciones permiten confirmar que el dataset utilizado para el análisis tenga una estructura consistente.

---

# Principales aprendizajes

Este proyecto permitió aplicar un flujo completo de análisis de datos utilizando Python y Pandas.

Las principales habilidades desarrolladas fueron:

- Importación de datos desde Excel.
- Exploración de datasets.
- Identificación de problemas de calidad.
- Tratamiento de valores faltantes.
- Eliminación de duplicados.
- Transformación de variables.
- Validación de información.
- Uso de `groupby()`.
- Uso de funciones de agregación.
- Análisis temporal.
- Creación de indicadores.
- Análisis de rentabilidad.
- Visualización de datos.
- Interpretación de resultados.

---

# Enfoque de negocio

Además del componente técnico, el proyecto busca aplicar los datos a preguntas relevantes para la gestión:

- ¿Qué categorías generan más ventas?
- ¿Qué sucursales presentan mejor desempeño?
- ¿Qué canales concentran mayores ingresos?
- ¿Qué vendedores generan mayor facturación?
- ¿Cómo evolucionan las ventas en el tiempo?
- ¿Cuál es el ticket promedio?
- ¿Cuál es el margen generado?
- ¿Qué categorías presentan mejor rentabilidad?

Este enfoque permite pasar de una simple limpieza de datos a un análisis orientado a la toma de decisiones.

---

#  Recomendaciones

Como continuación del proyecto se podrían incorporar:

- Dashboard en Power BI.
- Análisis de tendencias.
- Automatización del proceso de limpieza.
- Exportación automática de resultados.
- Integración con SQL.
- Desarrollo de un modelo predictivo de ventas.

---

# Conclusión

Este proyecto representa la aplicación práctica de Python y Pandas para transformar datos de ventas en información útil para el análisis y la gestión.

El objetivo no fue únicamente limpiar los datos, sino desarrollar un flujo de trabajo reproducible que permita explorar información, validar su calidad, construir indicadores y obtener insights orientados al negocio.
