# Módulo 2 — Herramientas Fundamentales de Cómputo y Análisis

**Período:** 7 al 11 de septiembre de 2026  
**Dedicación estimada:** 6 horas (trabajo autónomo)

---

### Descripción del módulo
Este módulo abarcó el dominio práctico de tres pilares del desarrollo de software científico: el control de versiones con Git y la sincronización con repositorios remotos en GitHub, la interacción y gestión de archivos mediante la terminal Unix en un entorno WSL (Ubuntu), y el desarrollo de un flujo de análisis exploratorio con Python sobre datos reales de colisiones del detector CMS.

---

### Entregables del módulo

#### Evidencias documentadas
* **[01. Control de Versiones con Git y GitHub](evidencias/01-control-versiones-git.md):**  
  Registro del flujo de trabajo local (staging, commits, historial con `git log --oneline`), vinculación del repositorio remoto `mi-proyecto-git` y resolución de autenticación segura.
* **[02. Gestión de Archivos con Terminal Linux (WSL)](evidencias/02-terminal-linux-wsl.md):**  
  Comandos fundamentales de navegación y manipulación de texto (`pwd`, `ls`, `mkdir`, `cat`, `cp`, `tree`) y reflexión sobre la importancia de la línea de comandos en cómputo científico.
* **[03. Análisis Físico del Espectro de Dimuones](evidencias/03-analisis-dimuones.md):**  
  Síntesis teórica e interpretación de resultados obtenidos a partir de $100\,000$ eventos de colisión del dataset `Dimuon_DoubleMu.csv` (CMS Run2011A).

#### Cuaderno de análisis
* **[`ejercicios/Analisis_Dimuones_CERN.ipynb`](ejercicios/Analisis_Dimuones_CERN.ipynb):**  
  Jupyter Notebook completo y reproducible que incluye carga de datos, verificación de valores nulos, conservación de carga ($Q_1 \neq Q_2$), histogramas de masa invariante (evidencia de los picos del mesón $J/\psi$ y el bosón $Z$) y gráficos de dispersión de momentos transversos.
