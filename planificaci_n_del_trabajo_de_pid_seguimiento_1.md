# Planificación del Trabajo - PID (Seguimiento 1)

**Título del trabajo:** Detección y Reconocimiento de Señales de Tráfico mediante Segmentación de Color Adaptativa y Deep Learning  
**Artículo de referencia:** *Road Traffic Sign Detection and Recognition using Adaptive Color Segmentation and Deep Learning* (IEEE ICSIPA 2021)  
**Bases de datos:** GTSDB (Detección en escenas) y GTSRB (Clasificación de parches)  
**Dedicación exigida:** 50 horas por persona (150 horas totales de grupo)

---

## 1. Asignación de Roles Generales

> Reparto **provisional**: pendiente de confirmación definitiva por el grupo.

* **Rafael Martín Del Pino:** Responsable del módulo de **Clasificación y Deep Learning** (Dataset GTSRB y arquitectura CNN).
* **Antonio Trujillo Ramos:** Responsable del módulo de **Detección Primaria y Segmentación** (Dataset GTSDB, espacio HSV, Imagen Integral y CHT exterior).
* **Alberto López López:** Responsable del módulo de **Validación y Filtrado de Falsas Alarmas** (Algoritmo CAD, CHT interior y preprocesamiento a $60 \times 60$ px).

**Tareas transversales (todas las fases):** cada miembro anota sus horas en la hoja de tiempos individual y registra los *prompts* de IA utilizados, su resultado y cómo se verificó (material para la sección «6. Uso de IA en este trabajo»).

---

## 2. Desglose Detallado por Fases y Miembro

### FASE 1: Investigación y Planteamiento Teórico
> **Dedicación:** 10 horas por persona (30 horas en total)  
> **Objetivo:** Buscar y elegir el artículo, leerlo y comprender su planteamiento teórico, y establecer la lista de objetivos y la planificación (**Seguimiento 1**).

* **Rafael (10 h):**
  * Búsqueda de artículos, selección del tema y lectura completa del artículo (3 h).
  * Estudio teórico de arquitecturas convolucionales, *Batch Normalization* y optimizador SGDM (momento y tasa de aprendizaje) (4 h).
  * Elaboración de la lista de objetivos, planificación temporal y reparto de tareas (3 h).
* **Antonio (10 h):**
  * Búsqueda de artículos, selección del tema y lectura completa del artículo (3 h).
  * Estudio de la conversión RGB a HSV, análisis del canal de Saturación ($S$) ante cambios de iluminación e Imagen Integral para medias de vecindad local (4 h).
  * Elaboración de la lista de objetivos, planificación temporal y reparto de tareas (3 h).
* **Alberto (10 h):**
  * Búsqueda de artículos, selección del tema y lectura completa del artículo (3 h).
  * Estudio de la ecuación de descomposición cromática/acromática ($CAD$), de la variable de escala $D$ y de la Transformada Circular de Hough (acumulación en el espacio de parámetros) (4 h).
  * Elaboración de la lista de objetivos, planificación temporal y reparto de tareas (3 h).

---

### FASE 2: Implementación de la Primera Versión
> **Dedicación:** 15 horas por persona (45 horas en total)  
> **Objetivo:** Desarrollar la primera versión de los módulos de detección (segmentación adaptativa y detección de forma circular) y de reconocimiento (redes CNN), e iniciar la escritura de la documentación.

* **Rafael (15 h):**
  * Descarga y acondicionamiento del dataset GTSRB: filtrado de las 12 clases de prohibición (2 h).
  * Programación de la arquitectura CNN de 4 capas convolucionales, *Batch Normalization*, activaciones y *pooling* (4 h).
  * Programación del bucle de entrenamiento con optimizador SGDM y función de pérdida *Cross-Entropy* (4 h).
  * Primeros entrenamientos, guardado de pesos y verificación de inferencia (3 h).
  * Inicio de la documentación: planteamiento teórico de Deep Learning e implementación del modelo (2 h).
* **Antonio (15 h):**
  * Conversión de imágenes de RGB a HSV y segmentación del rojo (2 h).
  * Algoritmo de Imagen Integral para cálculo rápido de medias locales (3 h).
  * Umbralizado adaptativo local sobre el canal $S$ ($umbral = \mu_{local} + 0.01$) (3 h).
  * Eliminación de ruido morfológico (<50 px) y suavizado con filtro `conv2` (2 h).
  * CHT exterior para delimitar los círculos rojos candidatos (radios entre 8 y 60 px) (3 h).
  * Inicio de la documentación: planteamiento teórico de segmentación e implementación del módulo de detección (2 h).
* **Alberto (15 h):**
  * Creación de un banco de imágenes de prueba con falsos positivos comunes: faros de coches, adornos circulares (3 h).
  * Programación de la función $CAD(R,G,B)$ con el parámetro $D=19$ para aislar la zona acromática interna (4 h).
  * Programación de la CHT interior para verificar la presencia del círculo blanco concéntrico (4 h).
  * Función de preprocesamiento: redimensión a $60 \times 60$ px y conversión a grises ITU-R BT.601-7 (2 h).
  * Inicio de la documentación: planteamiento teórico de validación e implementación del módulo (2 h).

---

### FASE 3: Experimentación y Depuración
> **Dedicación:** 15 horas por persona (45 horas en total)  
> **Objetivo:** Integrar los módulos, experimentar con parámetros, realizar pruebas sobre GTSDB/GTSRB, extraer conclusiones, depurar el código y revisar los objetivos.

* **Rafael (15 h):**
  * Experimento comparativo de arquitecturas CNN: entrenar y contrastar versiones con 3, 4 y 5 capas convolucionales (5 h).
  * Medición del tiempo de inferencia por imagen (referencia del artículo: ~0.54 ms) y matriz de confusión multiclase (4 h).
  * Depuración del código de clasificación y revisión de objetivos (2 h).
  * Redacción de la sección de experimentación y resultados de la CNN (4 h).
* **Antonio (15 h):**
  * Experimento comparativo: umbral global frente a adaptativo bajo sombras y contraluz en GTSDB (5 h).
  * Pruebas de variación de parámetros de detección (tamaño del vecindario, constante 0.01, rango de radios) (3 h).
  * Depuración del módulo de detección y limpieza del repositorio en GitHub (4 h).
  * Redacción de los resultados y figuras del módulo de detección (3 h).
* **Alberto (15 h):**
  * Integración del filtro de validación CAD a la salida de las detecciones de Antonio (4 h).
  * Experimento de sensibilidad paramétrica: tasa de acierto variando el factor $D \in [10, 30]$ (5 h).
  * Pruebas sobre el banco de falsos positivos y depuración del módulo de validación (2 h).
  * Redacción de los resultados de reducción de falsas alarmas (4 h).

---

### FASE 4: Documentación Final y Defensa
> **Dedicación:** 10 horas por persona (30 horas en total)  
> **Objetivo:** Redacción final de la documentación, revisión de conclusiones, autoevaluación de los miembros y preparación de la presentación de 20 minutos para la defensa en clase.

* **Rafael (10 h):**
  * Script interactivo para la demostración en directo del pipeline completo (4 h).
  * Diapositivas de la parte de clasificación y ensayo de la exposición oral (3 h).
  * Revisión final de sus secciones de la memoria y autoevaluación (3 h).
* **Antonio (10 h):**
  * Manual de usuario (`README.md`) y cierre del repositorio en GitHub (4 h).
  * Consolidación y verificación de la tabla final de tiempos de los 3 integrantes, asegurando 50 h por alumno (2 h).
  * Diapositivas de segmentación y ensayo de la exposición oral (2 h).
  * Autoevaluación (2 h).
* **Alberto (10 h):**
  * Redacción de la sección «6. Uso de IA en este trabajo»: herramientas, prompts, verificación y licencias (3 h).
  * Revisión editorial final de la memoria (`documentacion.pdf`) y bibliografía (3 h).
  * Redacción de resumen y conclusiones (2 h).
  * Diapositivas de validación y autoevaluación (2 h).

---

## 3. Resumen de Dedicación Horaria

| Miembro | Fase 1 | Fase 2 | Fase 3 | Fase 4 | Total Horas |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Rafael Martín Del Pino** | 10 h | 15 h | 15 h | 10 h | **50 h** |
| **Antonio Trujillo Ramos** | 10 h | 15 h | 15 h | 10 h | **50 h** |
| **Alberto López López** | 10 h | 15 h | 15 h | 10 h | **50 h** |
| **Total Proyecto** | **30 h** | **45 h** | **45 h** | **30 h** | **150 h** |
