# Análisis reproducible de adsorción de litio en materiales LDH

**Python · Pandas · NumPy · SciPy · Matplotlib · Análisis de datos científicos**

## Descripción

Este repositorio presenta un **reanálisis computacional** de datos de adsorción de litio en materiales LDH, reconstruidos a partir de un informe académico de Laboratorio 6 y 7 de la Universidad de Buenos Aires (2024).

El objetivo es organizar los datos experimentales disponibles, calcular la capacidad de adsorción, ajustar una isoterma de Langmuir y evaluar críticamente el ajuste mediante residuos y análisis de sensibilidad.

**Distinción de autoría y alcance:** el trabajo experimental de 2024 fue realizado en coautoría por **Kai Hain y Facundo Sánchez**. El notebook de Python es una reconstrucción y extensión analítica posterior para portfolio; **no constituye nuevas mediciones ni empleo profesional en el laboratorio**.

## Qué incluye

- Transcripción de seis muestras (A, A', B, B', C y C') de la tabla del informe.
- Organización de datos y cálculos con **Pandas** y **NumPy**.
- Estimación de la capacidad de adsorción de litio, \(Q_e\).
- Ajuste no lineal del modelo de **Langmuir** mediante `scipy.optimize.curve_fit`.
- Gráficos de datos, ajuste y residuos con **Matplotlib**.
- Cálculo de \(R^2\) y contribuciones al error cuadrático.
- Análisis de sensibilidad ante posibles valores redondeados de concentración final.
- Exportación de tablas procesadas a CSV.

## Datos y metodología

Los datos proceden de la **tabla 3, página 16**, del informe *Inserción química y electroquímica de litio en materiales nanoestructurados* (UBA, 2024). Se utiliza la ecuación de capacidad de adsorción presentada en el informe:

\[
Q_e=\frac{(C_0-C_e)\,V\,M_{Li}\,1000}{m_{LDH}}
\]

Donde \(C_0\) y \(C_e\) son concentraciones en mol/L, \(V\) es volumen de solución en L, \(M_{Li}=6.94\) g/mol y \(m_{LDH}\) es la masa de adsorbente en g. El resultado se expresa en mg de Li por g de LDH.

**Hipótesis explícita:** el informe proporciona masa de solución en gramos, pero no el volumen necesario para esta ecuación. Para realizar la reconstrucción se utiliza una **densidad supuesta de 1.00 g/mL**, editable en el notebook. **No es una densidad medida** y puede ser inadecuada, especialmente para soluciones concentradas de LiCl.

La isoterma ajustada es:

\[
Q_e(C_e)=\frac{Q_{\max}K_L C_e}{1+K_L C_e}
\]

Como \(C_e\) se expresa en mol/L, la constante \(K_L\) del ajuste tiene unidades de **L/mol**. El informe original utiliza otra etiqueta de unidades para esta constante, por lo que sus valores no deben compararse directamente sin resolver esa diferencia.

## Resultados e interpretación

En la reconstrucción con densidad supuesta de 1.00 g/mL, el ajuste presenta aproximadamente **\(R^2\approx0.455\)**, frente al **\(R^2=0.80\)** consignado en el informe original. Esta diferencia **no demuestra por sí sola que Langmuir sea incorrecto**.

El análisis de residuos permite identificar muestras que contribuyen de forma importante al error. En particular, las muestras **A y A'** comparten el mismo \(C_e=0.02\) mol/L **reportado con redondeo**, pero sus valores reconstruidos de \(Q_e\) son aproximadamente **2.88 y 11.12 mg/g**, respectivamente. El notebook explora de manera hipotética cuánto influiría variar ese valor de concentración final; estos escenarios **no reemplazan las mediciones originales**.

## Limitaciones

1. Los **archivos primarios de medición se perdieron**; solo están disponibles los valores incluidos en el informe académico.
2. Las concentraciones publicadas están redondeadas y no se conocen sus valores completos.
3. La conversión de masa de solución a volumen depende de una densidad **supuesta**, no verificada experimentalmente.
4. No se dispone de incertidumbres completas para todas las magnitudes; **no se inventan barras de error**.
5. Se analizaron solamente **seis muestras**; los resultados no permiten establecer conclusiones definitivas sobre la validez física del modelo.
6. No es posible reproducir exactamente el procedimiento de ajuste original ni atribuir con certeza la diferencia de \(R^2\) a una causa particular.

Por estas razones, los resultados se presentan como una **reconstrucción reproducible con supuestos declarados**, no como una validación definitiva del experimento.

## Cómo ejecutar el proyecto

1. Abrir [`Portfolio_Adsorcion_Litio_LDH_Colab_ACTUALIZADO.ipynb`](Portfolio_Adsorcion_Litio_LDH_Colab_ACTUALIZADO.ipynb) en **Google Colab** o Jupyter Notebook.
2. Ejecutar todas las celdas en orden, desde un entorno limpio.
3. Revisar la variable `densidad_g_mL` y sus implicaciones físicas.
4. Consultar las tablas y gráficos del ajuste, los residuos y el análisis de sensibilidad.
5. Ejecutar la sección final para exportar los archivos CSV generados.

Bibliotecas necesarias: `numpy`, `pandas`, `scipy`, `matplotlib`.

## Organización sugerida del repositorio

```text
adsorcion-litio-ldh/
├── README.md
├── Portfolio_Adsorcion_Litio_LDH_Colab_ACTUALIZADO.ipynb
└── datos/                  # CSV exportados desde el notebook (opcional)
```

El informe académico original puede citarse como fuente. **No subir el PDF completo sin confirmar que corresponde compartirlo y contar con la autorización pertinente de su coautor y demás titulares de derechos, si aplica.**

## Contexto académico

**Informe de origen:** *Inserción química y electroquímica de litio en materiales nanoestructurados* (2024).  
**Autores del informe:** Kai Hain y Facundo Sánchez.  
**Ámbito:** Laboratorio 6 y 7, Universidad de Buenos Aires; actividades experimentales desarrolladas en el Centro Atómico Constituyentes (CNEA).

Este proyecto muestra habilidades de análisis de datos científicos, programación en Python, ajuste de modelos y documentación transparente de limitaciones experimentales.
