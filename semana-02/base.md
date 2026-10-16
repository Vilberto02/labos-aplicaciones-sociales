# 02\_RegresionLineal\_CasoCostoSeguro

Nombre y titulo del notebook: 02\_RegresionLineal\_CasoCostoSeguro

No utilizar emojis ni muchos adjetivos. Se preciso y conciso.

Se debe trabajar sobre el conjunto de datos de kaggle: [Medical Cost Personal Datasets](https://www.kaggle.com/datasets/mirichoi0218/insurance/data)

## Estructura del notebook

1. Configuración del entorno: instalación (en caso sea necesario) e importación de librerías.
2. Data: cargar el CSV, info(), describe(), revisar nulos y duplicados.
3. Exploración: histograma de charges, scatter de edad y de BMI contra costo coloreado por fumador, matriz de correlación.
4. Procesamiento: codificación one-hot, eliminar el duplicado y separar train/test (80/20).
5. Modelo: LinearRegression de scikit-learn, métricas R², MAE y RMSE.
6. Explicación de la técnica: la ecuación y = b₀ + b₁x₁ + …, mínimos cuadrados y los supuestos (linealidad, residuos normales, homocedasticidad) con el gráfico de residuos.
7. Explicación del modelo (centrate más aquí): tabla de coeficientes interpretados en dólares y la conclusión: una aseguradora puede usar el modelo para fijar primas, y fumar es el factor que más pesa. Puedes agregar interpretaciones que faciliten el entendimiento de los resultados del modelo.


## Diagrama Eraser (copiar en app.eraser.io)

```
// Regresion Lineal - Caso Costo de Seguro Medico
// Tipo: Flowchart

// ─── SECCION 1: CONFIGURACION ───
Configuracion [shape: hexagon, icon: settings, color: blue, label: "1. Configuracion del entorno"]

Librerias [label: "numpy, pandas, matplotlib\nseaborn, scikit-learn"]
Estilo [label: "Estilo de graficas\nsns.set_theme + rcParams"]

Configuracion > Librerias: Importar
Configuracion > Estilo: Aplicar

// ─── SECCION 2: DATA ───
Data [shape: hexagon, icon: database, color: green, label: "2. Data"]

CSV [shape: cylinder, label: "insurance.csv\n1,338 registros x 7 columnas", color: green]
Estructura [label: "info() + describe()\nTipos, estadisticas descriptivas"]
Calidad [shape: diamond, label: "Nulos: 0\nDuplicados: 1", color: green]

Librerias > Data
Estilo > Data
Data > CSV: Cargar
CSV > Estructura: Inspeccionar
Estructura > Calidad: Verificar

// ─── SECCION 3: EXPLORACION ───
Exploracion [shape: hexagon, icon: bar-chart, color: purple, label: "3. Exploracion"]

Histograma [label: "Histograma de charges\nDistribucion sesgada a la derecha"]
ScatterEdad [label: "Scatter: Edad vs Costo\nColoreado por fumador"]
ScatterBMI [label: "Scatter: BMI vs Costo\nColoreado por fumador"]
Correlacion [label: "Matriz de correlacion\nHeatmap variables numericas"]
Hallazgos [shape: document, label: "Hallazgos clave:\n- Fumar dispara el costo\n- Edad y BMI correlacionan\n  positivamente con charges", color: purple]

Calidad > Exploracion
Exploracion > Histograma
Exploracion > ScatterEdad
Exploracion > ScatterBMI
Exploracion > Correlacion
Histograma > Hallazgos
ScatterEdad > Hallazgos
ScatterBMI > Hallazgos
Correlacion > Hallazgos

// ─── SECCION 4: PROCESAMIENTO ───
Procesamiento [shape: hexagon, icon: tool, color: orange, label: "4. Procesamiento"]

DropDup [label: "Eliminar duplicado\n1,338 -> 1,337 registros"]
OneHot [label: "One-Hot Encoding\nsex, smoker, region\n(drop_first=True)"]
Split [shape: parallelogram, label: "Train/Test Split\n80/20 (random_state=42)\nTrain: 1,069 | Test: 268", color: orange]

Hallazgos > Procesamiento
Procesamiento > DropDup: Limpiar
DropDup > OneHot: Codificar
OneHot > Split: Particionar

// ─── SECCION 5: MODELO ───
Modelo [shape: hexagon, icon: cpu, color: red, label: "5. Modelo"]

LR [label: "LinearRegression()\nfit(X_train, y_train)"]
Prediccion [label: "predict(X_test)\ny_pred"]
Metricas [shape: document, label: "Metricas:\nR2 = 0.8069\nMAE = 4,177 USD\nRMSE = 5,956 USD", color: red]

Split > Modelo
Modelo > LR: Entrenar
LR > Prediccion: Predecir
Prediccion > Metricas: Evaluar

// ─── SECCION 6: TECNICA ───
Tecnica [shape: hexagon, icon: book, color: blue, label: "6. Explicacion de la tecnica"]

Ecuacion [label: "Ecuacion:\ny = b0 + b1*x1 + ... + bm*xm"]
OLS [label: "Minimos cuadrados:\nMinimizar distancia entre\nvalores reales y predichos"]
Supuestos [label: "Supuestos:\n- Linealidad\n- Residuos normales\n- Homocedasticidad"]
GraficoResiduos [label: "Grafico de residuos\ny_pred vs residuos"]

Metricas > Tecnica
Tecnica > Ecuacion
Tecnica > OLS
Tecnica > Supuestos
Supuestos > GraficoResiduos: Evaluar visualmente

// ─── SECCION 7: MODELADO ───
Modelado [shape: hexagon, icon: star, color: green, label: "7. Modelado"]

TablaCoef [shape: document, label: "Tabla de coeficientes\nInterpretados en USD\npor unidad de cambio", color: green]
GraficoImpacto [label: "Grafico de barras\nImpacto de cada variable"]
Interpretacion [label: "Interpretacion:\n- smoker_yes: mayor impacto\n- age: incremento por ano\n- bmi: incremento por punto\n- children: incremento moderado\n- sex, region: impacto menor"]
Conclusion [shape: oval, label: "Conclusion:\nFumar es el factor determinante.\nUna aseguradora puede usar\nel modelo para fijar primas.", color: green]

GraficoResiduos > Modelado
Ecuacion > Modelado
OLS > Modelado
Modelado > TablaCoef
Modelado > GraficoImpacto
TablaCoef > Interpretacion
GraficoImpacto > Interpretacion
Interpretacion > Conclusion
```
