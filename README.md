# VigiTexto IA

VigiTexto IA es un prototipo de aprendizaje automático desarrollado para apoyar la detección preventiva de mensajes SMS potencialmente fraudulentos.

La herramienta permite ingresar un mensaje escrito en inglés y obtener una clasificación orientativa como **legítimo** o **potencialmente sospechoso**. También presenta un nivel de confianza, una clasificación del riesgo, indicadores detectados y recomendaciones básicas de seguridad.

Este proyecto fue desarrollado en el marco de la **Escuela de Verano Internacional Cyber Quantum 2026 de la Universidad EAN**.

---

## Integrantes

- María Fernanda Cruz Baena
- Andrés David Muñoz Caro

**Director:** Alexander García Pérez  
**Línea temática:** Analítica de datos y machine learning aplicado.

---

## Objetivo del proyecto

Desarrollar y evaluar un prototipo web basado en aprendizaje automático que permita clasificar mensajes SMS como legítimos o potencialmente sospechosos y presentar al usuario indicadores de riesgo y recomendaciones preventivas.

---

## Alcance

La versión actual corresponde a un producto mínimo viable o **MVP** y analiza únicamente mensajes SMS escritos en inglés.

El prototipo:

- Clasifica mensajes como legítimos o potencialmente sospechosos.
- Muestra el nivel de confianza de la predicción.
- Asigna un nivel de riesgo bajo, medio o alto.
- Detecta palabras y enlaces potencialmente sospechosos.
- Presenta recomendaciones básicas de seguridad.
- No almacena permanentemente los mensajes ingresados.

La herramienta no reemplaza el análisis de un profesional de ciberseguridad. Su resultado debe entenderse como una orientación preventiva.
---

## Tecnologías utilizadas

El proyecto fue desarrollado con las siguientes tecnologías:

- Python 3.12.13
- Gradio 6.20.0
- Scikit-learn 1.6.1
- Pandas 2.2.2
- NumPy 2.0.2
- Matplotlib 3.10.0
- Joblib 1.5.3
- Google Colab

Las versiones exactas de las dependencias también se encuentran en el archivo `requirements.txt`.

---

## Conjunto de datos

Para entrenar el modelo se utilizó el conjunto de datos **SMS Spam Collection**, disponible en el UCI Machine Learning Repository.

El dataset contiene **5.574 mensajes SMS escritos en inglés**, organizados originalmente en dos categorías:

- `ham`: mensaje legítimo.
- `spam`: mensaje no deseado.

En este proyecto, la categoría `spam` se utilizó como una aproximación a mensajes potencialmente sospechosos.

**Fuente:** Almeida, T., & Hidalgo, J. (2011). *SMS Spam Collection*. UCI Machine Learning Repository.

**DOI:** https://doi.org/10.24432/C5CC84

**Licencia del dataset:** Creative Commons Attribution 4.0 International (CC BY 4.0).

---

## Preparación de los datos

La preparación de los mensajes incluyó:

1. Limpieza básica del texto.
2. Conversión de los mensajes a minúsculas.
3. División del dataset en entrenamiento y prueba.
4. Transformación del texto mediante TF-IDF.
5. Entrenamiento del modelo de clasificación.

El conjunto de datos se dividió de la siguiente manera:

- 80 % para entrenamiento.
- 20 % para prueba.

Para mantener la reproducibilidad del proceso se utilizó la semilla:

`random_state=42`

---

## Modelo utilizado

El modelo de clasificación utilizado fue **Multinomial Naive Bayes**, combinado con la técnica de representación de texto **TF-IDF**.

El vectorizador TF-IDF y el clasificador se integraron mediante un `Pipeline` de Scikit-learn.

El modelo entrenado se encuentra almacenado en el archivo:

`modelo_vigitextoIA.pkl`

El vectorizador no se encuentra como un archivo independiente, porque está integrado dentro del mismo archivo `.pkl` junto con el clasificador.
---

## Resultados obtenidos

El modelo fue evaluado sobre **1.115 mensajes** del conjunto de prueba.

Los resultados finales fueron:

| Métrica | Resultado |
|---|---:|
| Exactitud general | 96,23 % |
| Precisión para mensajes sospechosos | 1,00 |
| Recall para mensajes sospechosos | 0,72 |
| F1-score para mensajes sospechosos | 0,84 |

La matriz de confusión presentó los siguientes valores:

- 965 mensajes legítimos clasificados correctamente.
- 0 mensajes legítimos clasificados como sospechosos.
- 42 mensajes sospechosos clasificados como legítimos.
- 108 mensajes sospechosos clasificados correctamente.

También se realizó una prueba interna con 20 mensajes SMS en inglés. En 17 casos el resultado fue satisfactorio, lo que corresponde al **85 %**.

Las capturas de las métricas, la matriz de confusión y los casos de prueba se encuentran dentro del repositorio.

---

## Estructura del repositorio

```text
VigiTexto-IA/
│
├── .gitignore
├── LICENSE
├── README.md
├── requirements.txt
├── VIGITEXTO_IA.ipynb
├── modelo_vigitextoIA.pkl
├── spam.csv
│
├── Accuracy y Reporte de clasificacion.PNG
├── Comparación de umbrales.PNG
├── Matriz de confusión.PNG
├── Semilla.PNG
│
├── Caso_1.PNG
├── Caso_2.PNG
├── Caso_3.PNG
├── ...
└── Caso_20.PNG
---

## Instalación y ejecución

El proyecto se ejecuta principalmente en **Google Colab**, por lo que no es necesario instalarlo directamente en el computador. Solo se requiere un navegador y una cuenta de Google.

### Paso 1. Abrir el notebook

Abrir el archivo:

`VIGITEXTO_IA.ipynb`

Puede utilizarse la opción **Open in Colab** o descargar el notebook y subirlo manualmente a Google Colab.

### Paso 2. Instalar las dependencias

Ejecutar la primera celda del notebook, encargada de instalar las librerías necesarias.

También es posible instalar las dependencias mediante el archivo `requirements.txt` con el siguiente comando:

```bash
pip install -r requirements.txt
```

### Paso 3. Cargar el dataset

Descargar desde el repositorio el archivo:

`spam.csv`

Cuando Google Colab solicite elegir un archivo, se debe seleccionar `spam.csv` desde el computador.

Este paso es obligatorio, ya que el dataset no se encuentra incluido directamente dentro del código del notebook.

### Paso 4. Ejecutar las celdas

Ejecutar todas las celdas del notebook en orden, desde la primera hasta la última.

Este proceso permite:

- Cargar y preparar los datos.
- Entrenar el modelo.
- Calcular las métricas.
- Generar la matriz de confusión.
- Preparar la interfaz web.

### Paso 5. Abrir la interfaz

Al ejecutar la última celda, Gradio generará una dirección temporal similar a:

`https://xxxxxxxxxxxx.gradio.live`

Al abrir este enlace se mostrará la interfaz de VigiTexto IA.

El enlace es temporal y solamente funciona mientras la sesión de Google Colab permanezca activa.

No es necesario volver a entrenar el modelo cuando se utiliza el archivo `modelo_vigitextoIA.pkl`, ya que este contiene el modelo previamente entrenado.

---

## Uso del prototipo

1. Escribir o pegar un mensaje SMS en inglés.
2. Seleccionar el botón **Analizar SMS**.
3. Revisar la clasificación obtenida.
4. Consultar el nivel de confianza.
5. Revisar el nivel de riesgo y los indicadores detectados.
6. Leer las recomendaciones de seguridad.
7. Utilizar el botón **Limpiar** para realizar una nueva consulta.
8. ---

## Privacidad y seguridad

VigiTexto IA no almacena permanentemente los mensajes ingresados por el usuario.

Sin embargo, se recomienda no ingresar:

- Contraseñas.
- Números de cuentas bancarias.
- Códigos de verificación.
- Información financiera.
- Datos personales sensibles.

El repositorio no contiene credenciales, contraseñas, tokens ni información personal identificable.

---

## Limitaciones

La versión actual presenta las siguientes limitaciones:

- Funciona principalmente con mensajes escritos en inglés.
- Fue entrenada con un único conjunto de datos.
- El dataset contiene más mensajes legítimos que sospechosos.
- La categoría `spam` no representa todas las modalidades de phishing o smishing.
- Puede presentar errores frente a nuevas formas de fraude.
- No analiza imágenes, audios, archivos adjuntos ni códigos QR.
- No verifica la identidad real del remitente.
- No abre ni comprueba directamente los enlaces.
- No ha sido validada con usuarios externos.

La herramienta no garantiza que un mensaje clasificado como legítimo sea completamente seguro.

---

## Trabajo futuro

Como mejoras futuras se propone:

- Adaptar el modelo a mensajes escritos en español.
- Ampliar y actualizar el conjunto de datos.
- Mejorar el recall para reducir los falsos negativos.
- Comparar otros algoritmos de clasificación.
- Realizar pruebas de usabilidad con usuarios.
- Desarrollar una aplicación web o móvil permanente.
- Incorporar análisis de enlaces y códigos QR.
- Mejorar los controles de privacidad y seguridad.

---

## Licencia

Este proyecto se distribuye bajo la licencia MIT.

Las condiciones pueden consultarse en el archivo:

`LICENSE`

---

## Autores

**María Fernanda Cruz Baena**

Liderazgo e interlocución del equipo, formulación y documentación del proyecto, elaboración del anteproyecto y del informe final, creación y organización del repositorio, análisis de riesgos, privacidad, limitaciones y ruta futura.

**Andrés David Muñoz Caro**

Preparación de los datos, entrenamiento y evaluación del modelo, desarrollo de la interfaz en Gradio, generación de métricas, matriz de confusión, casos de prueba y archivos técnicos.

---

## Advertencia

VigiTexto IA es un prototipo académico y preventivo. Los resultados generados por el modelo son orientativos y no deben utilizarse como única fuente para determinar si un mensaje es seguro.

Ante cualquier duda, se recomienda verificar la información directamente con la empresa o entidad mediante sus canales oficiales.
