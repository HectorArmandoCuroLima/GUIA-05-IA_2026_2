# Práctica 05: Arquitecturas CNN y Análisis de Resultados (MNIST vs. Fashion-MNIST)

## 👤 Datos del Estudiante
- **Curso:** SIS070 - Inteligencia Artificial
- **Unidad:** Unidad II - Redes Neuronales Convolucionales

## 🎯 Objetivos
- Implementar, ejecutar y comparar CNNs en los datasets MNIST y Fashion-MNIST.
- Interpretar shapes, cálculo de parámetros, vectores Softmax y métricas de entrenamiento.
- Gestionar el proyecto con Git y GitHub.

## 🛠️ Herramientas Utilizadas
- Python 3.14
- TensorFlow 2.22.0rc0 (con Keras)
- NumPy, Matplotlib
- VS Code, Git, GitHub

## 📁 Estructura del Repositorio
practica-cnn-comparativa/
├── mnist_cnn.py # Script CNN para dígitos
├── fashion_cnn.py # Script CNN para prendas
├── README.md # Este informe
└── .gitignore # Exclusión de archivos temporales

---

## 🧠 Parte 1: MNIST (Dígitos Escritos a Mano)

### 📸 Capturas
![Visualización MNIST](capturas/mnist_visual.png)
*Figura 1: Visualización de 9 dígitos del dataset MNIST con sus etiquetas.*

![Summary MNIST](capturas/mnist_summary.png)
*Figura 2: Resumen del modelo CNN para MNIST (`model.summary()`).*

![Entrenamiento MNIST](capturas/mnist_train.png)
*Figura 3: Resultados del entrenamiento (accuracy y loss).*

![Softmax MNIST](capturas/mnist_softmax.png)
*Figura 4: Vector de probabilidades Softmax y predicción final.*

### 📊 Resultados Obtenidos
- **Parámetros Totales:** 121,930
- **Entrenamiento:** `accuracy: 0.7580` - `loss: 0.8337`
- **Predicción:** Clase predicha = 7, Clase real = 7 (Acierto)
- **Vector Softmax:** `[0, 0, 0, 0.0001, 0, 0, 0, 0.9992, 0, 0.0007]`

### 📝 Análisis
1. **Inspección Visual:** Los dígitos son trazos simples, centrados y en escala de grises. Es útil visualizarlos para entender la variabilidad de la caligrafía y confirmar que las etiquetas son correctas.
2. **Shapes y Capas:** `Conv_1` reduce de 28x28 a 26x26 (kernel 3x3 sin padding). `MaxPool_1` reduce a 13x13. `Conv_2` reduce a 11x11. `MaxPool_2` reduce a 5x5. `Flatten` convierte 5x5x64 = 1600 en un vector 1D.
3. **Cálculo de Parámetros:** `Conv_2`: (3x3x32 + 1) x 64 = 18,496. `Dense oculta`: (1600 x 64) + 64 = 102,464. `Salida`: (64 x 10) + 10 = 650.
4. **Interpretación Softmax:** La suma del vector es 1.0. `np.argmax()` encontró el índice 7 con 99.92% de confianza, coincidiendo con la etiqueta real.

---

## 👕 Parte 2: Fashion-MNIST (Clasificación de Prendas)

### 📸 Capturas
![Visualización Fashion](capturas/fashion_visual.png)
*Figura 5: Visualización de 9 prendas del dataset Fashion-MNIST con sus nombres.*

![Summary Fashion](capturas/fashion_summary.png)
*Figura 6: Resumen del modelo CNN para Fashion-MNIST (`model.summary()`).*

![Entrenamiento Fashion](capturas/fashion_train.png)
*Figura 7: Resultados del entrenamiento (accuracy y loss).*

![Softmax Fashion](capturas/fashion_softmax.png)
*Figura 8: Vector de probabilidades Softmax y predicción con nombres.*

### 📊 Resultados Obtenidos
- **Parámetros Totales:** 225,034
- **Entrenamiento:** `accuracy: 0.6620` - `loss: 0.9867`
- **Predicción:** Clase predicha = Botín (Índice 9), Clase real = Botín (Índice 9) (Acierto)
- **Vector Softmax:** `[3e-04, 1e-04, 2.1e-03, 7e-04, 2e-04, 9.83e-02, 1e-03, 1.45e-01, 2.52e-02, 7.271e-01]`

### 📝 Análisis
1. **Inspección Visual:** Las prendas tienen siluetas complejas, texturas y formas variadas. No siempre están centradas. Esto hace la clasificación más difícil que los dígitos.
2. **Salida Nominal:** `class_names` transforma el índice entero (0-9) en un nombre legible, facilitando la interpretación del resultado.
3. **Capa Densa Modificada:** Al pasar de 64 a 128 neuronas, los parámetros de la capa densa aumentaron de 102,464 a 204,928. Esto le da a la red más capacidad para capturar patrones visuales complejos de la ropa, aunque también aumenta el riesgo de sobreajuste.

---

## 📈 Parte 3: Análisis Comparativo

### 1. Métricas de Entrenamiento
MNIST obtuvo mejor `accuracy` (75.8% vs 66.2%) y menor `loss` (0.83 vs 0.98) en una sola época. El aprendizaje es más rápido en MNIST porque los dígitos son más simples y están mejor centrados.

### 2. Complejidad Visual y de Patrones
Las prendas de Fashion-MNIST tienen mayor complejidad morfológica (pliegues, sombras, texturas) que los trazos numéricos. Esto afecta la confianza del Softmax: en MNIST la probabilidad es casi 1.0, mientras que en Fashion-MNIST está más dispersa (ej. 72% Botín vs 14% Zapatilla).

### 3. Distribución de Confianza
En MNIST, el vector Softmax tiene un valor dominante (99.92%). En Fashion-MNIST, la distribución es más dispersa, reflejando la incertidumbre de la red ante patrones visuales más ricos y ambiguos.

---

## ☁️ Parte 4: Repositorio GitHub
- **Enlace del repositorio:** https://github.com/tu-usuario/nombre-de-tu-repo
- **Commits realizados:** "Entrega completa: Practica comparativa CNN MNIST y Fashion-MNIST con visualizacion y analisis"

---

## ✅ Conclusiones
- La arquitectura CNN implementada es capaz de aprender tanto de dígitos como de prendas.
- MNIST es un problema más sencillo y la red converge más rápido.
- Fashion-MNIST requiere mayor capacidad de red (más neuronas) y más épocas para mejorar su precisión.
- El análisis de los vectores Softmax permite entender la confianza del modelo en sus predicciones.