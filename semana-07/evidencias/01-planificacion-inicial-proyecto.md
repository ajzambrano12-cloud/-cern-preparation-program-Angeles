# Planificación Inicial de Proyecto Tecnológico: CMS-DataStream
### Pipeline Ligero de Ingesta, Filtrado y Visualización de CMS NanoAOD para Redes Académicas

**Universidad de las Fuerzas Armadas – ESPE**  
**Departamento de Ciencias Exactas / Ingeniería en Tecnologías de la Información**  
**Programa de Preparación para Oportunidades CERN 2026 (PREP CERN)**  
**Módulo 7:** Sprint Técnico y Gestión Ágil de Proyectos

---

### Ficha Técnica de la Planificación

| Parámetro Institucional | Especificación Técnica |
| :--- | :--- |
| **Estudiante / Proponente:** | Angeles Julieth Zambrano Bravo |
| **Identificación Digital / GitHub:** | [@ajzambrano12-cloud](https://github.com/ajzambrano12-cloud) |
| **Programa Académico:** | Ingeniería en Tecnologías de la Información (4.° Semestre) — ESPE |
| **Asignatura / Actividad:** | CERN / Evidencia 1 — Planificación Inicial de un Proyecto Tecnológico |
| **Marco Metodológico:** | Metodologías Ágiles de Gestión de Proyectos (*Atlassian Agile Guide / Scrum*) |
| **Período de Planificación:** | Octubre de 2026 (Semana 07) |
| **Sede:** | Sangolquí, Ecuador |

---

> ### Resumen Ejecutivo
> El presente documento expone la planificación inicial del proyecto tecnológico **CMS-DataStream**, concebido para resolver el problema de acceso y análisis interactivo de datos de física de altas energías del CERN en laboratorios académicos con recursos computacionales y de red convencionales. Articulando las competencias adquiridas en el manejo de formatos compactos (**CMS NanoAOD**) con herramientas modernas del ecosistema Scikit-HEP (`uproot`, `awkward-array`, Python), se definen el objetivo central, la demarcación estricta del alcance (*In-Scope* vs. *Out-of-Scope*), tres hitos principales de entrega, una matriz de responsabilidades por rol, la mitigación de riesgos de saturación de memoria y latencia de red, y un *roadmap* temporal secuencial dividido en cuatro fases iterativas.

---

## 1. Nombre del Proyecto

**CMS-DataStream: Pipeline Ligero de Ingesta, Filtrado y Visualización de Colisiones CMS NanoAOD para Redes Académicas**

* **Acrónimo / Identificador:** `CMS-DataStream`
* **Tipo de proyecto:** Software científico y de infraestructura de análisis de datos de código abierto (*Open Source Data Pipeline*).

---

## 2. Objetivo del Proyecto

### 2.1. Objetivo General
Diseñar e implementar un prototipo de pipeline computacional en Python que permita ingerir, filtrar cinemáticamente y visualizar eventos de colisión en formato **CMS NanoAOD** de forma eficiente en estaciones de trabajo académicas de recursos estándar, optimizando el consumo de memoria RAM y minimizando la demanda de ancho de banda sin requerir la instalación del framework institucional pesado de CMS (*CMSSW*).

### 2.2. Objetivos Específicos
1. **Optimización de ingesta:** Desarrollar un módulo de carga columnar mediante `uproot` que lea archivos `.root` en bloques dinámicos (*chunks*), evitando sobrepasar el límite de 4 GB de memoria RAM en equipos de laboratorio.
2. **Filtrado cinemático vectorizado:** Implementar algoritmos de selección de eventos en `awkward-array` para reconstruir la masa invariante de pares de muones de carga opuesta ($Q_1 \neq Q_2$) en las resonancias del mesón $J/\psi$ (alrededor de 3.1 GeV) y el bosón $Z$ (alrededor de 91.2 GeV).
3. **Visualización y reproducibilidad:** Generar reportes gráficos interactivos de distribuciones cinemáticas y métricas de rendimiento (tiempo de CPU, tasa de eventos/segundo y volumen transferido) en entornos Jupyter Notebook y scripts reproducibles en GitHub.

---

## 3. Alcance del Proyecto (Scope Management)

Para garantizar la viabilidad del proyecto dentro de un marco temporal ágil y con recursos universitarios estándar, se delimitan rigurosamente los componentes incluidos y excluidos:

| Componente | Qué INCLUIRÁ el Proyecto (In-Scope) | Qué QUEDARÁ FUERA del Proyecto (Out-of-Scope) |
| :--- | :--- | :--- |
| **Tiers de Datos** | Datasets abiertos oficiales en formato **CMS NanoAOD** (colisiones reales con muones a 7, 8 y 13 TeV). | Formatos complejos o de bajo nivel como **RAW, AOD o MiniAOD**, debido a su gran tamaño y dependencia de C++ CMSSW. |
| **Infraestructura** | Ejecución local en entornos Linux estándar (Ubuntu bajo WSL) y estaciones de laboratorio universitarias estándar (8-16 GB RAM). | Despliegue en clústeres de supercómputo del Worldwide LHC Computing Grid (WLCG Tier-1/Tier-2) o servidores dedicados. |
| **Física y Selección** | Reconstrucción cinemática en estados finales con muones ($J/\psi \to \mu^+\mu^-$ y $Z \to \mu^+\mu^-$), filtrado por $p_T$, $\eta$ y carga. | Búsquedas de física más allá del Modelo Estándar (BSM), física de quarks pesados (b-jets complejos) o recalibración de detectores. |
| **Modelos Analíticos** | Operaciones matemáticas y vectorizadas con NumPy y Awkward Array para cálculo de masa invariante relativista. | Modelos de Machine Learning / Deep Learning pesados para clasificación de trazas o generación sintética de eventos. |
| **Interfaz de Usuario** | Cuadernos interactivos documentados en Jupyter Notebook y scripts modulares de terminal (CLI en Python). | Desarrollo de aplicaciones web complejas con microservicios, bases de datos externas o paneles comerciales cerrados. |

---

## 4. Hitos Principales del Proyecto (Milestones)

El desarrollo del proyecto se estructura en tres hitos fundamentales que marcan la entrega de valor funcional verificable:

| Hito | Nombre del Hito | Plazo Estimado | Entregable Clave Verificable | Criterio de Éxito Técnico |
| :---: | :--- | :---: | :--- | :--- |
| **Hito 1** | **Banco de Pruebas e Ingesta Columnar** | Semanas 1 – 2 | Módulo de lectura `ingestion.py` y notebook de benchmarking de lectura con `uproot`. | Carga exitosa de 100 000 eventos de colisión en menos de 10 segundos con un consumo de RAM menor a 1.5 GB. |
| **Hito 2** | **Motor de Filtrado y Reconstrucción Cinemática** | Semanas 3 – 4 | Módulo analítico `kinematics.py` con filtrado vectorial de dimuones ($p_T > 3\text{ GeV}$, $Q_1 \neq Q_2$). | Reconstrucción clara y visible del pico de masa invariante del mesón $J/\psi$ y del bosón $Z$ sin pérdida de precisión. |
| **Hito 3** | **Monitoreo de Recursos, Documentación y Release** | Semanas 5 – 6 | Repositorio GitHub documentado, script integrado de análisis con métricas y guía de reproducción. | Pipeline ejecutable de inicio a fin con un solo comando; métricas de ancho de banda y memoria documentadas. |

---

## 5. Asignación de Roles y Responsabilidades

Para simular una dinámica colaborativa ágil basada en el marco Scrum, el trabajo se distribuye entre roles complementarios:

### 5.1. Tareas asumidas por Angeles Zambrano (Líder Técnica & Especialista en Infraestructura TI)
* **Arquitectura de Software y Entorno:** Configuración del entorno reproducible en Linux WSL, estructura del repositorio Git y control de ramas (*feature branches*).
* **Desarrollo del Módulo de Ingesta:** Programación del lector de datos con `uproot` y manejo de estructuras de arreglos irregulares con `awkward-array`.
* **Monitoreo de Recursos:** Medición empírica del consumo de ancho de banda, tiempos de I/O y uso de memoria RAM en el sistema operativo.
* **Control de Calidad y Merge:** Revisión de código (*Code Review*) mediante Pull Requests e integración en la rama principal `main`.

### 5.2. Tareas asignadas a Colaboradores Técnicos
* **Colaborador 1 — Especialista en Física y Validación de Datos:**
  * Definición de criterios de selección cinemática (cortes de $p_T$, pseudorapidez $|\eta| < 2.4$, aislamiento de muones).
  * Validación teórica de las fórmulas cinemáticas relativistas para cálculo de masa invariante.
  * Comprobación física de las áreas de integración bajo los picos resonantes.
* **Colaborador 2 — Desarrollador de Visualización y Experiencia de Usuario:**
  * Diseño y estilización de histogramas con Matplotlib y Seaborn (escalas logarítmicas, barras de error y leyendas físicas).
  * Elaboración del cuaderno interactivo Jupyter con explicaciones didácticas paso a paso para estudiantes universitarios.
  * Redacción del manual de instalación de dependencias (`requirements.txt`) y guía de primeros pasos.

---

## 6. Gestión de Riesgos Técnicos y Mitigación

Se identifican las dos principales dificultades operativas del proyecto y sus correspondientes estrategias de mitigación proactiva:

### Riesgo 1: Saturación de Memoria RAM por Carga de Grandes Volúmenes de Eventos
* **Descripción de la dificultad:** Al intentar cargar muestras de cientos de miles de eventos en memoria sin particionar, las estructuras dinámicas de `awkward-array` pueden provocar errores de *Out Of Memory (OOM)* en equipos de cómputo estándar (con 8 GB de RAM).
* **Probabilidad:** Alta | **Impacto:** Alto.
* **Estrategia de mitigación:**  
  1. Implementar lectura iterativa en bloques continuos (*chunking*) utilizando el parámetro `step_size="100MB"` o por lotes fijos (ej. 50 000 eventos por iteración) provisto por `uproot.iterate()`.
  2. Aplicar los filtros de corte cinemático inmediatamente después de cargar cada bloque en memoria, descartando eventos no relevantes antes de acumularlos en el arreglo global.
  3. Ejecutar recolección explícita de basura (`gc.collect()`) tras el procesamiento de cada lote de datos.

### Riesgo 2: Inestabilidad o Cuello de Botella en la Red al Descargar Datos Remotos
* **Descripción de la dificultad:** Los enlaces WAN de las universidades pueden experimentar caídas intermitentes o fluctuaciones severas de ancho de banda al intentar leer archivos `.root` directamente desde los servidores internacionales del CERN.
* **Probabilidad:** Media | **Impacto:** Alto.
* **Estrategia de mitigación:**  
  1. Diseñar un mecanismo de **caché local inteligente**: el pipeline verifica si la muestra reducida ya existe en disco antes de iniciar peticiones remotas.
  2. Implementar descargas resumibles con validación criptográfica de integridad mediante sumas de verificación (checksums SHA-256).
  3. Trabajar preliminarmente con un subconjunto local representativo (*downsampled dataset*) de 50 000 a 100 000 eventos para depuración y validación del código antes de ejecutar pruebas sobre datasets mayores.

---

## 7. Roadmap y Secuencia Temporal de Ejecución

El proyecto sigue una secuencia temporal lineal y progresiva de 6 semanas de duración, organizada en 4 fases metodológicas:

| Fase | Período Temporal | Actividades Principales de la Fase | Entregable / Hito Vinculado |
| :---: | :---: | :--- | :--- |
| **Fase 1: Preparación y Arquitectura** | Semana 1 | • Selección del dataset NanoAOD de muones en CMS Open Data.<br>• Creación del repositorio en GitHub con estándares de ramas y `.gitignore`.<br>• Definición del entorno virtual Python con dependencias (`uproot`, `awkward`). | Entorno de desarrollo funcional y repositorio inicializado. |
| **Fase 2: Ingesta y Benchmarking** | Semana 2 | • Desarrollo del script `ingestion.py` con lectura por bloques (*chunking*).<br>• Medición de tiempos de lectura y consumo de RAM.<br>• Pruebas de lectura remota vs. lectura local en disco SSD. | **Hito 1:** Módulo de ingesta validado (100k eventos en < 10 s). |
| **Fase 3: Filtrado y Reconstrucción** | Semanas 3 – 4 | • Implementación de filtros de calidad de muones ($p_T > 3\text{ GeV}$, $|\eta| < 2.4$).<br>• Cálculo de masa invariante vectorizada para pares de signo opuesto.<br>• Generación de histogramas preliminares de dimuones ($J/\psi$ y $Z$). | **Hito 2:** Motor cinemático y gráficos de resonancias validados. |
| **Fase 4: Optimización, Monitoreo y Release** | Semanas 5 – 6 | • Medición y registro de métricas de red (ancho de banda consumido).<br>• Limpieza de código y revisión por pares (*code review*) en GitHub.<br>• Redacción de documentación técnica, guía de usuario y empaquetado final. | **Hito 3:** Versión final v1.0 publicada en GitHub con informe técnico. |

---

## 8. Fundamentación Metodológica y Conexión con el Perfil TI

1. **Alineación con la Filosofía Ágil (Atlassian Agile Guide):**  
   La planificación adopta un enfoque iterativo e incremental: en lugar de esperar semanas para obtener resultados, el Hito 1 produce un componente funcional de ingesta en 14 días. Las historias de usuario se priorizan según el valor directo para la estudiante y los investigadores locales.
2. **Transferencia Tecnológica hacia la Carrera de TI:**  
   El proyecto conecta directamente la formación en soporte técnico y redes de la estudiante con la computación científica de vanguardia del CERN, demostrando cómo una adecuada gestión de memoria y protocolos de ingesta columnar resuelve barreras de infraestructura en universidades latinoamericanas.
