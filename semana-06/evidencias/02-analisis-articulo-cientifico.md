# Análisis Crítico de Publicación Científica: Arquitectura del Formato CMS NanoAOD
### Evaluación Metodológica bajo el Enfoque de Tres Pasadas de S. Keshav

**Universidad de las Fuerzas Armadas – ESPE**  
**Departamento de Ciencias Exactas / Ingeniería en Tecnologías de la Información**  
**Programa de Preparación para Oportunidades CERN 2026 (PREP CERN)**  
**Módulo 6:** Metodología e Introducción a la Investigación Científica

---

### Ficha Técnica de la Entrega

| Parámetro Institucional | Especificación |
| :--- | :--- |
| **Autora / Estudiante:** | Angeles Julieth Zambrano Bravo |
| **Identificación Digital / GitHub:** | [@ajzambrano12-cloud](https://github.com/ajzambrano12-cloud) |
| **Programa Académico:** | Ingeniería en Tecnologías de la Información (4.° Semestre) |
| **Asignatura / Actividad:** | CERN / Actividad 2.1 — Análisis de un Artículo Científico |
| **Marco Metodológico de Lectura:** | *How to Read a Paper* (S. Keshav, ACM SIGCOMM CCR, 2007) |
| **Fecha de Presentación:** | Octubre de 2026 |
| **Sede:** | Sangolquí, Ecuador |

---

> ### Sinopsis Ejecutiva
> El presente informe constituye una evaluación analítica y metodológica del artículo de referencia *«The CMS NanoAOD format: a compact data tier for modern particle physics analysis»* (Rizzi et al., 2019). Empleando el enfoque estructurado de lectura crítica en tres pasadas de S. Keshav, se desglosa la transición paradigmática de la Colaboración CMS hacia arquitecturas de almacenamiento columnar ligero. Se examina la crisis de petabytes y cuellos de botella en la red de cómputo del CERN, los mecanismos de optimización mediante truncamiento adaptativo de mantisa y aplanamiento de árboles ROOT, los resultados empíricos que alcanzaron una compresión del 95% (~1.5–2 kB/evento), los compromisos técnicos (*trade-offs*) derivados de la compresión con pérdida, y se articula una reflexión ingenieril sobre la democratización del acceso a datos abiertos en infraestructuras académicas de TI.

---

## 1. Referencia Bibliográfica y Acceso al Documento

* **Título:** *The CMS NanoAOD format: a compact data tier for modern particle physics analysis*
* **Autores:** Andrea Rizzi, Gokhan Gokbulut, Marco Peruzzi (en representación de la Colaboración CMS del CERN).
* **Publicación científica:** *EPJ Web of Conferences*, Volumen 214, Artículo 06021 (2019).
* **Foro de divulgación:** *23rd International Conference on Computing in High Energy and Nuclear Physics* (CHEP 2018), Sofía, Bulgaria.
* **DOI oficial (Acceso Abierto):** [https://doi.org/10.1051/epjconf/201921406021](https://doi.org/10.1051/epjconf/201921406021)
* **Preprint en arXiv:** [arXiv:1904.03223 [physics.comp-ph]](https://arxiv.org/abs/1904.03223)

---

## 2. Marco Metodológico: Aplicación del Enfoque de Tres Pasadas (S. Keshav)

Para abordar la complejidad técnica del manuscrito sin incurrir en saturación cognitiva prematura, la revisión se ejecutó siguiendo las tres etapas sistemáticas propuestas por S. Keshav:

### Fases del Método de Lectura Crítica (S. Keshav)

| Etapa del Método | Tiempo Sugerido | Enfoque de Lectura | Acciones Clave Ejecutadas |
| :--- | :---: | :--- | :--- |
| **1.ª Pasada: Vista Panorámica** | 5 – 10 min | Visión estructural y propósito global | Inspección de título, resumen ejecutivo, subtítulos y conclusiones. Aplicación inmediata del filtro de las **5 Cs**. |
| **2.ª Pasada: Contenido Clave** | $\le 1$ hora | Comprensión conceptual y técnica | Examen detallado de tablas de reducción por objeto, figuras de compresión y lógica de datos, prescindiendo de pruebas analíticas profundas. |
| **3.ª Pasada: Profundización** | 1 – 2 horas | Análisis crítico y reconstrucción mental | Reconstrucción virtual de la arquitectura del formato, examen de supuestos implícitos, identificación de limitaciones y proyección técnica. |

### Matriz de Diagnóstico Inicial: Evaluación de las 5 Cs
Durante la **primera pasada**, se sometió la publicación al filtro de las cinco preguntas críticas de Keshav:

| Criterio (5 Cs) | Evaluación Crítica | Diagnóstico Técnico |
| :--- | :--- | :--- |
| **Categoría (Category)** | ¿Qué tipo de artículo es? | Publicación de **arquitectura de software científico e ingeniería de datos**. Describe el diseño, implementación y benchmarking de un nuevo formato de almacenamiento para física de altas energías. |
| **Contexto (Context)** | ¿Con qué otros trabajos se conecta? | Se sitúa en la evolución de los formatos de datos del experimento CMS del LHC (*AOD* y *MiniAOD*) frente al desafío de escalabilidad impuesto por el aumento de luminosidad en el Run 2 y el futuro *High-Luminosity LHC (HL-LHC)*. |
| **Corrección (Correctness)** | ¿Los supuestos y métodos son válidos? | Sí. Los resultados se fundamentan en pruebas empíricas directas sobre petabytes de datos reales de colisiones proton-protón a 13 TeV procesados en el *Worldwide LHC Computing Grid* (WLCG). |
| **Contribución (Contributions)** | ¿Cuáles son los aportes principales? | Creación de un tier ultraligero (~1.5–2 kB/evento) que reduce en un **95%** el tamaño frente a MiniAOD, prescinde de dependencias complejas de C++ (*CMSSW*) y permite lectura nativa columnar en Python (uproot). |
| **Claridad (Clarity)** | ¿El documento está bien escrito? | Excelente. Presenta tablas desglosadas de presupuesto de almacenamiento por partícula, justificación física de la precisión requerida y flujos claros de producción y análisis. |

---

## 3. Diagnóstico del Problema: Cuellos de Botella en la Red y Cómputo del LHC

El Gran Colisionador de Hadrones (LHC) genera una de las mayores densidades de flujo de datos del planeta, con tasas de interacción de 40 MHz. Con el incremento progresivo de la tasa de colisiones y la luminosidad instantánea, la infraestructura de cómputo del CERN (*Worldwide LHC Computing Grid*, WLCG) enfrentó restricciones severas a lo largo de su cadena de datos:

### Flujo de Datos y Cuello de Botella Detectado en el LHC

| Nivel / Tier de Datos | Tamaño Promedio por Evento | Volumen Acumulado | Infraestructura y Desafío Técnico Identificado |
| :--- | :---: | :---: | :--- |
| **1. Colisiones Primarias (RAW / AOD)** | ~400 kB – 1 MB / evento | Decenas de Petabytes (PB) | Almacenamiento primario en cinta y disco en el Tier-0 del CERN. Contiene trazas crudas de toda la instrumentación física. |
| **2. Tier Intermedio (MiniAOD - 2014)** | ~30 – 50 kB / evento | Cientos de Terabytes por muestra | Diseñado para selecciones físicas generales; sin embargo, saturó discos en centros Tier-2/Tier-3 universitarios durante el Run 2. Exigía el framework pesado C++ (*CMSSW*). |
| **3. Cuello de Botella Detectado (WLCG)** | Enlaces WAN congestionados | Latencias de días a semanas | Grupos de investigación esperaban días para transferir muestras completas sobre enlaces compartidos; barrera técnica de acceso para universidades locales. |
| **4. Solución Arquitectónica (NanoAOD)** | **~1.5 – 2.0 kB / evento** | **15 – 20 TB anuales** | **Reducción del 95%** en peso, tablas columnares planas, lectura nativa en Python (uproot) sin requerir CMSSW. |

### Factores Críticos del Diagnóstico
1. **Escala masiva e insostenibilidad de almacenamiento:**  
   Aunque el formato intermedio *MiniAOD* (introducido en 2014) logró reducir el formato original *AOD* a ~30–50 kB por evento, la acumulación de decenas de miles de millones de colisiones y simulaciones Monte Carlo durante el Run 2 saturó las capacidades de almacenamiento en disco en los centros de cómputo Tier-2 y Tier-3 del WLCG.
2. **Saturación de ancho de banda y latencia analítica:**  
   Los grupos de investigación universitarios debían transferir rutinariamente petabytes de datos sobre enlaces WAN para refinar sus selecciones. Este proceso demoraba días o semanas, limitando la iteración rápida de hipótesis físicas y saturando los enlaces institucionales.
3. **Dependencia arquitectónica de frameworks propietarios:**  
   MiniAOD se diseñó como un grafo de objetos C++ estrechamente acoplado al framework institucional *CMSSW*. Esto impedía a los investigadores emplear el floreciente ecosistema de ciencia de datos e interactividad en Python (Jupyter, NumPy, Pandas, Matplotlib) sin desplegar complejas capas de emulación.

---

## 4. Objetivos y Criterios de Diseño de la Arquitectura NanoAOD

Para erradicar estos cuellos de botella, la colaboración CMS concibió el formato **NanoAOD** bajo tres objetivos estratégicos de ingeniería de software:

* **Compresión extrema con fidelidad física:** Reducir el tamaño promedio por evento a una cota de **1–2 kB/evento** (un factor de reducción de ~20× respecto a MiniAOD y ~200× frente a AOD), permitiendo que un año completo de datos analizables quepa en unas decenas de terabytes.
* **Autonomía tecnológica e interoperabilidad:** Eliminar por completo el acoplamiento con CMSSW en la fase de análisis de usuario final. La información debía serializarse en tablas planas de TTree de ROOT utilizando exclusivamente tipos primitivos, garantizando lectura inmediata con bibliotecas abiertas en Python (uproot, wkward-array).
* **Cobertura funcional representativa:** Garantizar que el formato contenga el contenido informativo necesario para sustentar de manera autónoma al menos el **50% de los análisis de física finales** de la colaboración (estudios de precisión del bosón de Higgs, mediciones electrodébiles y búsquedas de física más allá del Modelo Estándar).

---

## 5. Metodología e Innovaciones de Ingeniería de Datos

Para alcanzar una tasa de compresión del 95% sin desvirtuar la validez científica de las colisiones, los autores desplegaron cuatro estrategias metodológicas de optimización:

### 5.1. Aplanamiento Columnar de Estructuras de Datos (Flat Columnar Tables)
Se desmantelaron las jerarquías de herencia y grafos de punteros de C++. Los datos de cada partícula se organizaron como columnas independientes indexadas por arreglos unidimensionales basados en tipos nativos:
* Arreglos de tamaño variable por evento para colecciones dinámicas de partículas:  
  Muon_pt[nMuon], Muon_eta[nMuon], Muon_phi[nMuon], Muon_charge[nMuon].
* Variables escalares para magnitudes globales del evento:  
  MET_pt (energía faltante), PV_npvs (número de vértices primarios).

### 5.2. Compresión Adaptativa con Pérdida mediante Truncamiento de Mantisa (Bit Truncation)
Los estándares de coma flotante IEEE 754 de 32 bits (*single precision*) asignan 23 bits a la mantisa, ofreciendo una precisión numérica de ~7 dígitos decimales. Sin embargo, la resolución intrínseca de los calorímetros y detectores de trazas de CMS no supera el 1% en muchas variables cinemáticas.

Para optimizar drásticamente la compresión sin pérdida posterior (ZLIB/LZMA), se implementó un truncamiento adaptativo de bits:

| Campo del Estándar IEEE 754 | Formato Float32 Convencional | Optimización NanoAOD (Bit Truncation) | Justificación y Ganancia en Compresión |
| :--- | :---: | :---: | :--- |
| **Signo (s)** | 1 bit | 1 bit | Preserva el sentido direccional y carga de las partículas. |
| **Exponente (e)** | 8 bits | 8 bits | Mantiene el orden de magnitud y rango dinámico físico original. |
| **Mantisa (m)** | 23 bits (alta entropía de bits aleatorios) | **8 a 12 bits útiles** + **11 a 15 bits en ceros** | La resolución física experimental es de ~1%; los bits de menor peso constituyen ruido. |
| **Efecto en Compresión ZLIB / LZMA** | Baja tasa de compresión por ruido aleatorio | **Compresión extrema por secuencias uniformes de ceros** | Al rellenar los bits de menor peso con ceros continuos, los algoritmos colapsan las cadenas idénticas. |

### 5.3. Filtrado Selectivo de Objetos y Poda de Trazas de Bajo Nivel
Se descartaron los impactos crudos en celdas de silicio (*rechits*), trazas incompletas de partículas cargadas y conglomerados calorimétricos individuales. Únicamente se exportan los cuatro-vectores reconstruidos de partículas de alto nivel y banderas booleanas precalculadas de algoritmos de identificación (*ID working points*).

### 5.4. Comparativa Arquitectónica de los Tiers de Datos de CMS

| Atributo Técnico | AOD (Analysis Object Data) | MiniAOD (Miniaturized AOD) | NanoAOD (Nano AOD) |
| :--- | :---: | :---: | :---: |
| **Tamaño medio por evento** | ~400 kB – 1 MB | ~30 – 50 kB | **~1.5 – 2.0 kB (-95%)** |
| **Factor de compactación** | 1× (Línea base) | ~10 – 15× | **~200× (vs AOD)** |
| **Estructura subyacente** | Clases C++ CMSSW complejas | Clases C++ optimizadas | **Tablas planas ROOT TTree** |
| **Dependencia de CMSSW** | Estricta y obligatoria | Estricta y obligatoria | **Ninguna (Lectura en Python/uproot)** |
| **Acceso a tracks crudos** | Total | Parcial (solo tracks clave) | Nulo (solo física reconstruida) |
| **Caso de uso principal** | Calibración y reprocesamiento | Selección física general | **Análisis final y ciencia de datos** |

---

## 6. Resultados y Validación Empírica

La evaluación del formato NanoAOD demostró beneficios cuantitativos contundentes en el ecosistema computacional de CMS:

1. **Reducción volumétrica sostenida (~95%):**  
   El tamaño final promedio se estabilizó entre **1.5 y 2.0 kB/evento**. Al analizar el desglose, los jets de partículas representan aproximadamente el 30% del volumen, los muones y electrones el 25%, y los indicadores de disparadores (HLT) y vértices el 45% restante.
2. **Sostenibilidad del almacenamiento distribuido:**  
   Una muestra de colisiones de 10 mil millones de eventos (típica de un año del Run 2) se almacena en únicamente **15 a 20 TB**, en marcado contraste con los 400 TB requeridos por MiniAOD o los más de 4 PB exigidos por AOD. Esto viabiliza la tenencia de copias locales en clústeres departamentales.
3. **Aceleración en tasas de lectura y procesamiento:**  
   Al emplear el modelo columnar plano, el ancho de banda de procesamiento en memoria superó los **5 millones de eventos por segundo** sobre núcleos estándar utilizando uproot, permitiendo a los físicos generar histogramas de colisiones en tiempo interactivo en cuestión de segundos.
4. **Democratización científica:**  
   El desacoplamiento del framework CMSSW permitió que investigadores y estudiantes ejecuten flujos analíticos en plataformas en la nube (como Google Colab o Binder) y estaciones portátiles convencionales.

---

## 7. Análisis Crítico de Limitaciones y Compromisos de Diseño (*Trade-offs*)

Desde la perspectiva de la arquitectura de software y la física experimental, el formato introduce compromisos inevitables:

1. **Compresión con pérdida irreversible (Lossy Nature):**  
   Al descartar los elementos primarios de los detectores, cualquier análisis que requiera recalibrar algoritmos de identificación de partículas, aplicar nuevos alineamientos geométricos de detectores o estudiar resonancias exóticas que dejen trazas atípicas no puede ejecutarse en NanoAOD; los científicos deben recurrir obligatoriamente a MiniAOD o AOD.
2. **Inflexibilidad del esquema estático de datos:**  
   Si la colaboración científica desarrolla una nueva corrección cinemática o un parámetro de aprendizaje profundo para clasificación de jets que no fue contemplado en el esquema de producción de NanoAOD, toda la comunidad debe esperar a un nuevo ciclo de centralizado de reprocesamiento (*re-nanoAOD*) para acceder a dicha variable.
3. **Propagación de incertidumbre por truncamiento de mantisa:**  
   En análisis de precisión sub-porcentual (como la medición ultraprecisa de la masa del bosón W o mediciones de polarización angular fina), la reducción de bits en la mantisa podría inducir sesgos sistemáticos si las cotas de redondeo no se calibran de forma exhaustiva para cada canal cinemático.

---

## 8. Síntesis Reflexiva y Proyección en Ingeniería de TI

### 8.1. Aprendizajes Clave Adquiridos
La revisión de este manuscrito evidencia que el avance de la física fundamental de frontera está intrínsecamente supeditado a la **arquitectura y eficiencia de las Tecnologías de la Información**. Lejos de constituir un mero problema de almacenamiento físico, la gestión de datos a escala de exabytes exige innovaciones en serialización columnar, técnicas de reducción de entropía (bit-truncation) y diseño de APIs orientadas a la reproducibilidad. 

Asimismo, la aplicación del método de Keshav demostró ser una competencia invaluable: permitió abstraer la arquitectura global y los compromisos de diseño antes de sumergirse en detalles de bajo nivel, fortaleciendo mi capacidad de juicio técnico ante literatura científica internacional.

### 8.2. Formulación de Pregunta Técnica de Frontera
Articulando los hallazgos de este paper con mi formación en redes, programación y soporte de infraestructura en la ESPE, formulo la siguiente interrogante técnica de investigación:

> **«¿En qué medida es factible combinar la arquitectura columnar de CMS NanoAOD con protocolos de transporte orientados a flujos (Zero-Copy Memory Streaming y compresión LZ4 en vuelo) para permitir que estaciones de trabajo universitarias procesen eventos en Python en tiempo real a medida que ingresan por la red, eliminando el almacenamiento intermedio en disco local?»**

---

## 9. Referencias Bibliográficas 

1. S. Keshav, «How to Read a Paper», *ACM SIGCOMM Computer Communication Review*, vol. 37, n.º 3, pp. 83–84, jul. 2007. doi: [10.1145/1273445.1273458](https://doi.org/10.1145/1273445.1273458).
2. A. Rizzi, G. Gokbulut, y M. Peruzzi, «The CMS NanoAOD format: a compact data tier for modern particle physics analysis», *EPJ Web of Conferences*, vol. 214, p. 06021, 2019. doi: [10.1051/epjconf/201921406021](https://doi.org/10.1051/epjconf/201921406021).
3. CMS Collaboration, «The CMS Experiment at the CERN LHC», *Journal of Instrumentation*, vol. 3, n.º 08, p. S08004, ago. 2008. doi: [10.1088/1748-0221/3/08/S08004](https://doi.org/10.1088/1748-0221/3/08/S08004).
4. J. Pivarski et al., «Columnar data analysis with Uproot and Awkward Array in high-energy physics», en *Proc. of the 24th Int. Conf. on Computing in High Energy and Nuclear Physics (CHEP 2019)*, Adelaida, Australia, 2020.
