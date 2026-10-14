# Actividad 1.1 — Mi Tema de Investigación: Formulación Inicial y Delimitación Científica

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
| **Recurso base de aprendizaje:** | [1.1 Introducción a la investigación científica (Elsevier Researcher Academy)](https://researcheracademy.elsevier.com/research-preparation) |
| **Fecha de entrega:** | Octubre de 2026 |
| **Carrera / Semestre:** | Ingeniería en Tecnologías de la Información — 4.° Semestre |
| **Sede:** | Sangolquí, Ecuador |

---

> **Objetivo de la Actividad:**  
> Aplicar los conceptos fundamentales de introducción a la investigación científica proporcionados por Elsevier Researcher Academy (*Research Preparation*) para identificar una necesidad tecnológica real, seleccionar un tema científico preliminar, delimitar el problema de estudio, formular una pregunta investigable clara y sustentar su relevancia e impacto en el marco del análisis de datos de física de altas energías del CERN y las infraestructuras de tecnologías de la información.

---

## 1. Tema de Investigación: ¿Qué te gustaría investigar?

**Título preliminar del tema:**  
> *Evaluación de la eficiencia en la transferencia de datos y consumo de ancho de banda para el análisis distribuido de física de altas energías mediante formatos reducidos (CMS NanoAOD) en infraestructuras de red académicas.*

### Descripción del tema
El objeto de estudio se centra en el análisis del comportamiento de redes de transmisión de datos en entornos universitarios cuando se transfieren y procesan grandes conjuntos de datos científicos abiertos provistos por la Colaboración CMS (*Compact Muon Solenoid*) del CERN. Específicamente, se busca investigar la viabilidad y optimización que ofrece la transición hacia formatos compactos columnares (*NanoAOD*) frente a formatos intermedios tradicionales (*AOD* y *MiniAOD*) en estaciones de trabajo y laboratorios de instituciones de educación superior de América Latina.

---

## 2. Problema Identificado: ¿Qué situación, necesidad o dificultad has identificado?

### Diagnóstico de la situación y necesidad tecnológica
1. **Volúmenes masivos de datos frente a enlaces limitados:**  
   Los experimentos del Gran Colisionador de Hadrones (LHC) del CERN registran y simulan decenas de petabytes de datos por ciclo de operación. Aunque iniciativas como el portal *CMS Open Data* ponen a disposición pública cientos de terabytes de colisiones reales, su aprovechamiento práctico por parte de universidades fuera de las redes dedicadas de Europa o Norteamérica está condicionado por la infraestructura de conectividad disponible.
2. **Saturación de enlaces y limitaciones de almacenamiento local:**  
   En instituciones académicas como la Universidad de las Fuerzas Armadas ESPE, las redes de cómputo comparten el ancho de banda internacional entre labores docentes, administrativas e investigativas. Descargar conjuntos de colisiones en formatos tradicionales (como *AOD*, con un tamaño promedio de ~400 kB a 1 MB por evento, o *MiniAOD*, con ~30 a 50 kB por evento) satura los canales de comunicación, congestiona el almacenamiento en disco local y genera tiempos de espera excesivos antes de iniciar cualquier análisis físico.
3. **Brecha de acceso a la ciencia abierta:**  
   Esta sobrecarga de red actúa como una barrera técnica de entrada para estudiantes de pregrado e investigadores noveles, restringiendo la reproducibilidad de los estudios y limitando el potencial formativo del programa. Existe la necesidad de cuantificar con precisión si el empleo del formato de nivel de usuario *NanoAOD* (diseñado para ocupar únicamente ~1 a 2 kB por evento) resuelve de forma sostenible este cuello de botella en la capa de red y almacenamiento en centros universitarios.

---

## 3. Pregunta de Investigación: ¿Qué te gustaría descubrir o resolver?

### Pregunta principal de investigación
> **¿En qué medida el uso del formato compacto columnar NanoAOD optimiza los tiempos de transferencia de datos y el consumo de ancho de banda en infraestructuras de red académicas, en comparación con formatos intermedios tradicionales en el análisis distribuido de CMS Open Data?**

### Preguntas secundarias de soporte
* ¿Cuál es el porcentaje real de reducción en la latencia de transferencia y utilización de enlaces WAN/LAN alcanzado al sustituir muestras en MiniAOD por NanoAOD en un entorno de red universitario estándar?
* ¿Cómo incide la reducción del tamaño del dataset en la capacidad de ejecutar flujos de trabajo científicos locales utilizando bibliotecas de Python como `uproot` y estructuras de datos columnares sin sobrecargar la infraestructura del laboratorio?
* ¿Qué requisitos mínimos de conectividad y almacenamiento institucional son necesarios para que un equipo de estudiantes pueda replicar análisis de colisiones del CERN de manera completamente autónoma?

---

## 4. Relevancia y Justificación: ¿Por qué consideras que vale la pena investigar este tema?

La pertinencia de esta propuesta se fundamenta en tres ejes estratégicos de impacto:

### 1. Democratización de la Ciencia Abierta y Acceso Equitativo
Permite derribar las barreras geográficas y económicas que enfrentan las universidades de países en desarrollo. Al demostrar que es posible realizar análisis de frontera con una fracción mínima del consumo de ancho de banda, se viabiliza que instituciones con recursos de red moderados se integren de forma activa al ecosistema de investigación de física de partículas.

### 2. Eficiencia y Gobernanza de Infraestructuras de TI
Desde la perspectiva de la Ingeniería en Tecnologías de la Información, optimizar la transferencia de datos masivos es una prioridad operativa. Comprender la métrica de tráfico, latencia y compresión de los datos del CERN aporta evidencia cuantitativa para dimensionar políticas de caché, priorización de tráfico (*QoS*) y dimensionamiento de almacenamiento en redes de cómputo académico.

### 3. Aceleración del Aprendizaje y Formación de Talento Técnico
En el marco pedagógico del Programa de Preparación CERN, reducir el tiempo dedicado a descargar archivos de gran volumen permite a los estudiantes concentrarse en el análisis estadístico, el filtrado cinemático de partículas (como la reconstrucción de dimuones $J/\psi$ y $Z^0$) y el dominio de herramientas científicas en Python y ROOT, maximizando el aprovechamiento del programa.

---

## 5. Enfoque Metodológico y Aplicación en Tecnologías de la Información

Siguiendo las pautas metodológicas de *Elsevier Researcher Academy* en el módulo de preparación de investigaciones, la ejecución inicial de esta propuesta contempla las siguientes fases estructuradas:

```
[Fase 1: Revisión Bibliográfica]
   │  → Consulta en bases de datos indexadas (Scopus / ScienceDirect / arXiv)
   │  → Sistematización de antecedentes de computación en CMS (estándar Keshav)
   ▼
[Fase 2: Delimitación de Variables y Métricas]
   │  → Variables independientes: Formato de archivo (MiniAOD vs. NanoAOD)
   │  → Variables dependientes: Tasa de transferencia (MB/s), tiempo total (s), latencia y espacio en disco (MB)
   ▼
[Fase 3: Diseño Experimental y Medición de Red]
   │  → Entorno de pruebas en red de campus (ESPE) y estaciones locales
   │  → Scripts automatizados en Python para registro de métricas de red y análisis con uproot
   ▼
[Fase 4: Análisis Comparativo y Conclusiones]
   │  → Evaluación estadística de throughput y viabilidad operativa
   │  → Documentación abierta y reproducible en repositorio GitHub
```

### Variables preliminares de estudio
* **Variable Independiente:** Tipo de estructura y formato de datos utilizado (*MiniAOD* frente a *NanoAOD* de colisiones proton-protón registradas por CMS).
* **Variables Dependientes:**
  * Tiempo efectivo de transferencia y descarga a través de enlaces de red (segundos).
  * Consumo pico y promedio de ancho de banda (Mbps / MB/s).
  * Tasa de uso de almacenamiento secundario (megabytes / gigabytes por millón de eventos).
  * Tiempo de acceso a ramas cinemáticas de interés (`Muon_pt`, `Muon_eta`, `Muon_phi`) mediante lectura columnar en Python.

---

## 6. Reflexión Crítica: Proceso de Formulación de Preguntas Investigables

De acuerdo con las lecciones de *Elsevier Researcher Academy*:
1. **De la curiosidad general a la delimitación precisa:**  
   El principal reto inicial consistió en evitar temas excesivamente amplios (como "el análisis de datos en el CERN") y aterrizar en una problemática concreta, medible y directamente vinculada a la especialidad de Tecnologías de la Información: las limitaciones de red y almacenamiento en entornos académicos.
2. **Factibilidad técnica sin asumir soluciones prematuras:**  
   Se cuidó no condicionar la pregunta a una respuesta predeterminada, sino formular un cuestionamiento que pueda responderse empíricamente mediante pruebas de transferencia y experimentación controlada.
3. **Alineación con el perfil formativo:**  
   Este planteamiento articula coherentemente el aprendizaje de herramientas científicas (ROOT, NanoAOD, Python) con las materias curriculares de redes de datos, sistemas operativos y telecomunicaciones de la ESPE.

---

## 7. Referencias Bibliográficas y Recursos Consultados

1. **Elsevier Researcher Academy.** (2024). *Research Preparation: How to identify and formulate a research topic*. Recuperado de: [https://researcheracademy.elsevier.com/research-preparation](https://researcheracademy.elsevier.com/research-preparation)
2. **CMS Collaboration.** (2020). *The CMS NanoAOD format: A compact data tier for modern particle physics analysis*. Journal of Physics: Conference Series, CERN Open Data Workshop.
3. **Pivarski, J., et al.** (2021). *Columnar data analysis with Uproot and Awkward Array in high-energy physics*. Computing and Software for Big Science, Springer.
4. **Universidad de las Fuerzas Armadas – ESPE.** (2026). *Guía metodológica del Programa de Preparación para Oportunidades CERN (PREP CERN)*. Departamento de Ciencias Exactas y Dirección de TIC.
