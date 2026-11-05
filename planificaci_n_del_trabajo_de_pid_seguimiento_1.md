# Planificación del Trabajo - PID (Seguimiento 1)

**Título del trabajo:** Detección y Reconocimiento de Señales de Tráfico mediante Segmentación de Color Adaptativa y Deep Learning  
**Artículo de referencia:** *Road Traffic Sign Detection and Recognition using Adaptive Color Segmentation and Deep Learning* (IEEE ICSIPA 2021)  
**Bases de datos:** GTSDB (Detección en escenas) y GTSRB (Clasificación de parches)  
**Dedicación exigida:** 50 horas por persona (150 horas totales de grupo)

---

## 1. Asignación de Roles Generales

* **Rafael Martín Del Pino:** Responsable del módulo de **Clasificación y Deep Learning** (Dataset GTSRB y arquitectura CNN).
* **Antonio Trujillo Ramos:** Responsable del módulo de **Detección Primaria y Segmentación** (Dataset GTSDB, espacio HSV, Imagen Integral y CHT exterior).
* **Alberto López López:** Responsable del módulo de **Validación y Filtrado de Falsas Alarmas** (Algoritmo CAD, CHT interior y preprocesamiento a $60 \times 60$ px).

---

## 2. Desglose Detallado por Fases y Miembro

### FASE 1: Planteamiento Teórico y Definición de Interfaces (Semanas 1 y 2)
> **Dedicación:** 10 horas por persona (30 horas en total)  
> **Objetivo:** Comprender las bases matemáticas, definir el contrato de datos entre módulos y superar el **Seguimiento 1**.

* **Rafael (10 h):**
  * Estudio teórico de arquitecturas convolucionales y de la formulación matemática de *Batch Normalization* (4 h).
  * Estudio del funcionamiento del optimizador SGDM: ecuaciones de momento y tasa de aprendizaje (3 h).
  * Redacción en LaTeX del marco teórico correspondiente a Deep Learning (3 h).
* **Antonio (10 h):**
  * Estudio matemático de la conversión de RGB al espacio HSV y análisis del canal de Saturación ($S$) ante cambios de iluminación (4 h).
  * Estudio del algoritmo de Imagen Integral aplicado al cálculo rápido de medias de vecindad local (3 h).
  * Redacción en LaTeX del marco teórico correspondiente a la segmentación adaptativa (3 h).
* **Alberto (10 h):**
  * Estudio analítico de la ecuación de descomposición cromática/acromática ($CAD$) y análisis de la variable de escala $D$ (4 h).
  * Estudio teórico de la Transformada Circular de Hough (CHT) y la acumulación en el espacio de parámetros (3 h).
  * Redacción en LaTeX del marco teórico correspondiente a la validación de falsas alarmas (3 h).

---

### FASE 2: Implementación Modular y MVP (Semanas 3 a 5)
> **Dedicación:** 20 horas por persona (60 horas en total)  
> **Objetivo:** Desarrollar en paralelo los tres bloques en código ejecutable independiente y superar el **Seguimiento 2**.

* **Rafael (20 h):**
  * Descarga y acondicionamiento del dataset GTSRB: filtrado de las 12 clases de prohibición (3 h).
  * Programación de la arquitectura CNN de 4 capas convolucionales, *Batch Normalization*, activaciones y *pooling* (5 h).
  * Programación del bucle de entrenamiento utilizando optimizador SGDM y función de pérdida *Cross-Entropy* (5 h).
  * Ejecución de los primeros entrenamientos, guardado de pesos del modelo y verificación de inferencia (3 h).
  * Redacción en LaTeX del capítulo de implementación del modelo de Deep Learning (4 h).
* **Antonio (20 h):**
  * Programación del conversor de imágenes de RGB a HSV (3 h).
  * Programación del algoritmo de Imagen Integral para cálculo rápido de medias locales sobre matrices 2D (5 h).
  * Programación del umbralizado adaptativo local sobre el canal $S$ ($umbral = \mu_{local} + 0.01$) (4 h).
  * Implementación de la eliminación de ruido morfológico (<50 px) y suavizado con filtro `conv2` (4 h).
  * Redacción en LaTeX del capítulo de implementación de la segmentación (4 h).
* **Alberto (20 h):**
  * Creación de un banco de imágenes de prueba con falsos positivos comunes: faros de coches, adornos circulares (3 h).
  * Programación de la función $CAD(R,G,B)$ con el parámetro $D=19$ para aislar la zona acromática interna (5 h).
  * Programación de CHT interior para verificar la presencia del círculo blanco concéntrico (4 h).
  * Programación de la función de preprocesamiento: redimensión a $60 \times 60$ px y conversión a grises ITU-R BT.601-7 (4 h).
  * Redacción en LaTeX del capítulo de implementación del módulo de validación (4 h).

---

### FASE 3: Integración, Experimentación y Cierre (Semanas 6 a 8)
> **Dedicación:** 20 horas por persona (60 horas en total)  
> **Objetivo:** Unir los módulos, realizar pruebas paramétricas, completar la memoria en LaTeX y preparar la defensa oral (**Seguimiento 3** y Entrega Final).

* **Rafael (20 h):**
  * Experimento comparativo de arquitecturas CNN: entrenar y contrastar versiones con 3, 4 y 5 capas convolucionales (5 h).
  * Medición empírica del tiempo de inferencia por imagen (evaluando el objetivo de ~0.54 ms) y matriz de confusión multiclase (4 h).
  * Redacción en LaTeX de la sección de experimentación y resultados de la CNN (3 h).
  * Programación del script interactivo para la demostración en directo del pipeline completo en la defensa (4 h).
  * Elaboración de diapositivas de la parte de clasificación y ensayo de la exposición oral (4 h).
* **Antonio (20 h):**
  * Programación de la CHT exterior para delimitar los círculos rojos candidatos (radios entre 8 y 60 px) (4 h).
  * Experimento didáctico comparativo: umbral global frente a adaptativo bajo sombras y contraluz en GTSDB (5 h).
  * Redacción en LaTeX de los resultados y figuras del módulo de detección (3 h).
  * Consolidación y verificación de la tabla final de tiempos de los 3 integrantes asegurando 50 h por alumno (3 h).
  * Limpieza del repositorio en GitHub, redacción del manual (`README.md`) y diapositivas de segmentación (5 h).
* **Alberto (20 h):**
  * Integración del filtro de validación CAD inmediatamente a la salida de las detecciones de Antonio (4 h).
  * Experimento de sensibilidad paramétrica: evaluar la tasa de acierto variando el factor $D \in [10, 30]$ (5 h).
  * Redacción en LaTeX de los resultados de reducción de falsas alarmas (3 h).
  * Redacción obligatoria de la sección «6. Uso de IA en este trabajo»: herramientas, prompts, verificación y licencias (4 h).
  * Revisión editorial final de la memoria en LaTeX (`documentacion.pdf`), bibliografía y diapositivas de validación (4 h).

---

## 3. Resumen de Dedicación Horaria

| Miembro | Fase 1 | Fase 2 | Fase 3 | Total Horas |
| :--- | :---: | :---: | :---: | :---: |
| **Rafael Martín Del Pino** | 10 h | 20 h | 20 h | **50 h** |
| **Antonio Trujillo Ramos** | 10 h | 20 h | 20 h | **50 h** |
| **Alberto López López** | 10 h | 20 h | 20 h | **50 h** |
| **Total Proyecto** | **30 h** | **60 h** | **60 h** | **150 h** |