# Evidencia 2 — Exploración de un dataset CMS

**Estudiante:** Angeles Julieth Zambrano Bravo  
**Recurso:** [Finding & Using Open Data — Dataset Scouting](https://cms-opendata-workshop.github.io/workshopqcd-2024-lesson-dataset-scouting/)

---

### 1. Nombre del dataset:
`/SingleMu/Run2012B-22Jan2013-v1/AOD`. CERN Open Data Portal. DOI: [10.7483/OPENDATA.CMS.IYVQ.1J0W](http://doi.org/10.7483/OPENDATA.CMS.IYVQ.1J0W)

### 2. Tipo de información:
Datos de colisiones reales del detector CMS (no simulados), correspondientes al periodo Run2012B, seleccionados por el trigger SingleMu eventos con al menos un muon detectado. Están en formato Analysis Object Data (AOD), la primera etapa procesada donde ya es posible hacer análisis de física.

### 3. ¿Qué te llamó la atención?
Que el nombre del dataset, aunque parece un código críptico, en realidad codifica información clave siguiendo una estructura de tres partes separadas por "/": el trigger usado, el periodo de toma de datos y su reprocesamiento, el nivel de formato. Haciendo que entender esa lógica lo vuelve mucho más legible.

### 4. Posible utilidad:
Sirve como base para análisis de física que involucren muones, por ejemplo, la reconstrucción de resonancias como el bosón Z o el J/ψ a través de pares de muones, o búsquedas de nueva física con estados finales que incluyan muones energéticos.

### 5. Dificultad encontrada:
La nomenclatura de los datasets (triggers, versiones de procesamiento como "22Jan2013-v1") no es intuitiva al inicio; fue necesario revisar la explicación paso a paso de la lección para descomponer el nombre y entender qué representaba cada parte.
