# Regresion Visual - Artear
# 🔍 Regresión Visual Estructural 

Este repositorio contiene el script principal para la **Regresión Visual Estructural** de los sitio web **TN (Todo Noticias)**, **El Trece**, **El Doce** y **Ciudad Magazine**.

El objetivo es garantizar la **estabilidad de la geometría y el posicionamiento del DOM** (X, Y, Ancho, Alto) de los elementos críticos de los sitio en cada nuevo despliegue. Es un control de calidad esencial para prevenir quiebres de diseño causados por el "efecto dominó" o por cambios no intencionados en la maquetación.

## 🎯 Características Principales del Motor de Pruebas

El script utiliza **Selenium** para la automatización y **OpenCV** para la generación de reportes visuales, con una lógica de comparación de cuatro puntos (X, Y, W, H) extremadamente rigurosa.

### 1. Comparación Geométrica Avanzada

* **Auditoría de 4 Puntos:** Compara la posición absoluta (X, Y) y la dimensión (Ancho, Alto) de cada elemento `<div>` en la página entre la Versión Base (`V1`) y la Versión de Prueba (`V2`).
* **Precisión Píxel Perfecta:** El umbral de tolerancia está configurado a **0 píxeles**, exigiendo que la estructura permanezca idéntica.
* **Análisis Empírico:** Utiliza un argumento de línea de comandos para diferenciar la versión a testear (ej: `?d=639`).

### 2. Gestión Inteligente de Errores

* **Clasificación de Gravedad:** Las diferencias se agrupan y clasifican automáticamente en:
    * **🔴 Graves:** Cambios de dimensión (W/H), o elementos que aparecen/desaparecen.
    * **🔵 Menores:** Solo cambios de posición (X/Y), que a menudo son un "efecto dominó" causado por un fallo anterior.
* **Marcado Visual Automático:** Las capturas de pantalla de la V2 son procesadas por OpenCV para dibujar un rectángulo **Rojo (Grave)** o **Azul (Menor)** sobre el elemento diferente.

### 3. Estabilización de Entorno (Anti-Flotantes)

* **Limpieza de Popups:** Antes de medir el DOM, el script inyecta JavaScript para eliminar y ocultar elementos flotantes comunes (banners de cookies, notificaciones OneSignal, modales de suscripción, etc.).
* **Medición Estructural de Ads:** El script está diseñado intencionalmente para **mantener visibles los contenedores de anuncios** (DFP) durante la medición. Esto permite detectar si un nuevo despliegue causa un movimiento estructural debido a una carga incorrecta o un cambio de tamaño en los slots publicitarios.

### 4. Output y Reporting (Ideal para Jenkins)

* **Reporte Interactivo:** Genera un único archivo HTML (`Reporte_DOM_Estructural...html`) que:
    * Muestra un resumen global y el tiempo total de ejecución.
    * Lista las fallas detalladas por cada URL testeada, incluyendo el selector CSS.
    * Presenta el contexto visual lado a lado (V1 vs V2 marcado).
* **Archivos de Salida:** Todos los reportes y capturas se guardan en la carpeta: Ej.:`Reportes HTML - TN - DESKTOP - PROD`.

## 🛠️ Requisitos y Uso

### Dependencias de Python

Se requiere un entorno Python 3.x con las librerías listadas en `requirements.txt`:

```bash
selenium
opencv-python
numpy
Pillow
webdriver-manager
