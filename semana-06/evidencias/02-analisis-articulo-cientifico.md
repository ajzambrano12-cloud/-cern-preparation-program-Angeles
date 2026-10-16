# Actividad 2.1 — Análisis de un Artículo Científico: The CMS NanoAOD Format

**Programa de Preparación para Oportunidades CERN 2026 (PREP CERN)**  
**Departamento de Ciencias Exactas / Tecnologías de la Información**  
**Universidad de las Fuerzas Armadas – ESPE**

---

### Metadatos de la Entrega

| Parámetro | Detalle |
| :--- | :--- |
| **Estudiante:** | Angeles Julieth Zambrano Bravo |
| **Cuenta institucional / GitHub:** | [@ajzambrano12-cloud](https://github.com/ajzambrano12-cloud) |
| **Módulo académico:** | Módulo 6: Metodología e Introducción a la Investigación Científica |
| **Recurso metodológico base:** | [2.1 Lectura y análisis de artículos científicos (S. Keshav — The Three-Pass Approach)](https://cs.uwaterloo.ca/~brecht/courses/856/readings/how-to-read/keshav-paper-reading.pdf) |
| **Fecha de entrega:** | Octubre de 2026 |
| **Carrera / Semestre:** | Ingeniería en Tecnologías de la Información — 4.° Semestre |
| **Sede:** | Sangolquí, Ecuador |

---

> **Objetivo de la Actividad:**  
> Aplicar el método de lectura crítica de artículos científicos en tres pasadas propuesto por S. Keshav (*How to Read a Paper*, ACM SIGCOMM CCR, 2007) para examinar en profundidad un artículo de frontera tecnológica relevante para el CERN y la ingeniería de datos, extrayendo de forma sintética su problemática, metodología, hallazgos, limitaciones y formulando una reflexión técnica con proyección a la carrera de Tecnologías de la Información.

---

## 1. Referencia y Enlace del Artículo

* **Título:** *The CMS NanoAOD format: a compact data tier for modern particle physics analysis*
* **Autores:** Andrea Rizzi, Gokhan Gokbulut, Marco Peruzzi (en representación de la Colaboración CMS del CERN)
* **Publicación científica:** *EPJ Web of Conferences*, Volumen 214, Artículo 06021 (2019). Presentado en la *23rd International Conference on Computing in High Energy and Nuclear Physics* (CHEP 2018).
* **DOI oficial (Acceso Abierto):** [https://doi.org/10.1051/epjconf/201921406021](https://doi.org/10.1051/epjconf/201921406021)
* **Preprint en arXiv:** [https://arxiv.org/abs/1904.03223](https://arxiv.org/abs/1904.03223)

---

## 2. Aplicación del Método de las Tres Pasadas de Keshav

Para garantizar una lectura analítica y evitar la saturación de detalles prematuros, se aplicó el enfoque metodológico de S. Keshav:

```
┌────────────────────────────────────────────────────────────────────────┐
│                      MÉTODO DE S. KESHAV (2007)                        │
├────────────────────────────────────────────────────────────────────────┤
│  1.ª Pasada (5-10 min)  │ Título, abstract, introducción, conclusiones │
│                         │ y 5 Cs (Category, Context, Correctness, ...)  │
├─────────────────────────┼──────────────────────────────────────────────┤
│  2.ª Pasada (≤ 1 hora)  │ Gráficos, tablas, estructura de datos y      │
│                         │ argumentos centrales sin demostraciones      │
├─────────────────────────┼──────────────────────────────────────────────┤
│  3.ª Pasada (Detallada) │ Reconstrucción virtual, supuestos ocultos,   │
│                         │ limitaciones técnicas e ideas futuras        │
└────────────────────────────────────────────────────────────────────────┘
```

### Respuestas a las 5 Cs de la Primera Pasada (Keshav)
1. **Category (Categoría):** Artículo de descripción de arquitectura de software y análisis de un nuevo sistema de almacenamiento de datos científicos en física de altas energías.
2. **Context (Contexto):** Se sitúa en la evolución de formatos de datos del experimento CMS (de AOD y MiniAOD hacia tiers ligeros) ante la avalancha de datos del Gran Colisionador de Hadrones (LHC Run 2 y preparación para HL-LHC).
3. **Correctness (Corrección):** Las premisas son válidas; se fundamentan en mediciones directas sobre petabytes de datos reales de colisiones en el WLCG (*Worldwide LHC Computing Grid*).
4. **Contributions (Contribuciones):** Diseño de un formato columnar puro (~1-2 kB/evento, 95% menor a MiniAOD) legible sin dependencias de CMSSW mediante ROOT y ecosistemas de Python (`uproot`).
5. **Clarity (Claridad):** El manuscrito está sólidamente estructurado, con tablas comparativas precisas de tamaño por partícula y flujos de análisis claros.

---

## 3. Problema: ¿Qué problema intenta resolver?

El aumento continuo de la luminosidad y tasa de colisiones en el LHC generó una **crisis de almacenamiento y ancho de banda** en la red de cómputo del CERN:
* **Escala masiva y cuellos de botella:** El tier de análisis intermedio estándar (*MiniAOD*), aunque redujo el formato primario *AOD*, mantenía un tamaño promedio de ~30 a 50 kB por evento. Al multiplicar esto por decenas de miles de millones de eventos registrados y simulados durante el Run 2, el volumen superó decenas de petabytes.
* **Sobrecarga de red y ciclos lentos:** Cientos de físicos requerían descargar o transmitir continuamente conjuntos masivos a través de enlaces de red institucionales para análisis finales, saturando el almacenamiento en disco de las universidades y obligando a esperas de días para completar una iteración analítica.
* **Dependencia de software pesado:** MiniAOD requería vincular las librerías completas del framework central *CMSSW* en C++, lo que dificultaba el uso directo de herramientas contemporáneas de ciencia de datos en Python.

---

## 4. Objetivo: ¿Qué busca demostrar o conseguir?

El trabajo busca concebir, implementar y validar un nivel de datos ultra-compacto (*NanoAOD*) que cumpla simultáneamente con:
1. **Compresión extrema sin pérdida crítica:** Reducir el tamaño medio por evento a **1–2 kB** (alrededor del 5% del tamaño de MiniAOD), permitiendo que la totalidad de los datos analizables de un año quepan en unos pocos terabytes.
2. **Autonomía tecnológica:** Almacenar los datos como árboles planos (`TTree` de ROOT) sin clases complejas de C++, de modo que puedan leerse directamente en Python nativo (`uproot`, `pandas`, `numpy`) sin necesidad de instalar o compilar el framework de CMS.
3. **Cobertura funcional elevada:** Satisfacer al menos el **50% de los análisis de física finales** de la colaboración (estudios del bosón de Higgs, búsquedas de nueva física, mediciones del Modelo Estándar) directamente sobre este formato.

---

## 5. Metodología: ¿Qué métodos, herramientas y procedimientos utiliza?

Para lograr esta drástica optimización, los autores implementaron las siguientes técnicas de ingeniería de datos:

1. **Aplanamiento Columnar (Flat Tables):**
   * Transformación de grafos orientados a objetos complejos en colecciones de tablas planas basadas en tipos primitivos (`float`, `int`, `bool`) y arreglos dinámicos de longitud variable (por ejemplo, `Muon_pt[nMuon]`).
2. **Compresión Cuantitativa con Precisión Truncada:**
   * En lugar de almacenar números en coma flotante estándar de 32 o 64 bits, se redujo el tamaño de la mantisa (*bit truncation*) adaptándola a la resolución experimental del detector. Por ejemplo, los ángulos directores de partículas ($\eta, \phi$) se truncan a 8 o 12 bits de mantisa sin impacto físico apreciable.
3. **Eliminación de Información de Muy Bajo Nivel:**
   * Se descartaron trazas detalladas de impactos individuales en sensores (*hits* de silicio) y conglomerados calorimétricos secundarios, preservando únicamente las propiedades físicas ya reconstruidas y calibradas de cada partícula (leptones, fotones, jets, energía faltante).
4. **Compatibilidad Estándar y Evaluación Empírica:**
   * Almacenamiento en archivos `.root` nativos procesables con librerías abiertas (`uproot`, `awkward`). Pruebas de rendimiento sobre datasets de colisiones reales proton-protón a $\sqrt{s} = 13\text{ TeV}$.

---

## 6. Resultados: ¿Cuáles son los principales hallazgos?

* **Reducción de tamaño del 95%:**  
  El tamaño por evento se redujo con éxito a **~1.5 a 2.0 kB/evento**, logrando un factor de compresión de 20 a 1 respecto a MiniAOD y de más de 200 a 1 respecto al AOD original.
* **Viabilidad de almacenamiento local:**  
  Un dataset completo de colisiones y simulaciones de un año completo (~100 mil millones de eventos) ocupa únicamente unos **150 a 200 TB**, lo que hace factible mantener réplicas completas en centros de cómputo universitarios estándar sin requerir almacenamiento masivo de clase petabyte.
* **Aceleración drástica de los ciclos de análisis:**  
  El tiempo necesario para procesar millones de eventos se redujo de horas a escasos minutos, permitiendo un flujo de análisis interactivo mediante Jupyter Notebooks y Python.
* **Independencia de plataforma:**  
  Se demostró que herramientas ligeras como `uproot` en Python alcanzan tasas de lectura de varios millones de eventos por segundo, democratizando el acceso a estudiantes e instituciones con estaciones de trabajo convencionales.

---

## 7. Limitaciones: ¿Qué dificultades o restricciones se identifican?

1. **Compresión con pérdida (Lossy Compression):**  
   Al descartar los datos primarios de detectores, los análisis que requieren recalibrar algoritmos de identificación o investigar fenómenos que dependen de la topología cruda de las trazas no pueden utilizar NanoAOD y deben recurrir obligatoriamente a MiniAOD o AOD.
2. **Inflexibilidad en correcciones post-procesamiento:**  
   Si una nueva escala de energía de jets o corrección de eficiencia de muones requiere variables no incluidas en el esquema predeterminado de NanoAOD, es necesario reprocesar la muestra desde tiers superiores o esperar a una nueva versión del esquema.
3. **Sensibilidad de la mantisa truncada:**  
   Para búsquedas de extrema precisión angular o cinemática fina, la truncación de coma flotante podría introducir sesgos sistemáticos si no se calibran rigurosamente las cotas de error.

---

## 8. Reflexión Crítica y Pregunta Resultante

### ¿Qué aprendí al analizar este artículo?
Comprendí que la investigación en física de altas energías moderna es, en esencia, un desafío interdisciplinario de **Ingeniería en Tecnologías de la Información y Computación Científica**. El diseño de estructuras de datos columnares y la compresión adaptativa marcan la diferencia entre una ciencia reservada a unos pocos laboratorios con centros de datos masivos y una ciencia verdaderamente colaborativa y global. Asimismo, aplicar la técnica de lectura de Keshav me permitió concentrarme primero en el propósito y las contribuciones antes de perderme en las fórmulas matemáticas o particularidades de C++.

### Pregunta que me queda tras la lectura
> *¿En qué medida es posible implementar técnicas de streaming inteligente y descompresión columnar en memoria (Zero-Copy) al transferir NanoAOD a través de redes académicas internacionales, de forma que el cómputo en Python comience en paralelo a la descarga sin esperar la llegada del archivo completo?*

---

## 9. Referencias Bibliográficas

1. **Keshav, S.** (2007). *How to Read a Paper*. ACM SIGCOMM Computer Communication Review, 37(3), 83–84. https://doi.org/10.1145/1273445.1273458
2. **Rizzi, A., Gokbulut, G., & Peruzzi, M.** (2019). *The CMS NanoAOD format: a compact data tier for modern particle physics analysis*. EPJ Web of Conferences, 214, 06021. https://doi.org/10.1051/epjconf/201921406021
3. **Pivarski, J., et al.** (2020). *Columnar data analysis with Uproot and Awkward Array in high-energy physics*. Computing and Software for Big Science, Springer.
