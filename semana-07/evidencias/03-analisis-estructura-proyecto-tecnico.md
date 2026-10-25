# Actividad 3.1 — Análisis de la Estructura de un Proyecto Técnico
### Evaluación Arquitectónica, Gestión de Repositorios, Reproducibilidad y Flujos de Revisión por Pares

**Universidad de las Fuerzas Armadas – ESPE**  
**Departamento de Ciencias Exactas / Ingeniería en Tecnologías de la Información**  
**Programa de Preparación para Oportunidades CERN 2026 (PREP CERN)**  
**Módulo 7:** Sprint Técnico y Gestión Ágil de Proyectos

---

### Metadatos del Informe Técnico

| Parámetro Institucional | Especificación |
| :--- | :--- |
| **Estudiante / Autora:** | Angeles Julieth Zambrano Bravo |
| **Identificación Digital / GitHub:** | [@ajzambrano12-cloud](https://github.com/ajzambrano12-cloud) |
| **Programa Académico:** | Ingeniería en Tecnologías de la Información (4.° Semestre) — ESPE |
| **Asignatura / Actividad:** | CERN / Actividad 3.1 — Análisis de la Estructura de un Proyecto Técnico |
| **Proyecto Técnico Analizado:** | CMS Open Data Analyses Project (CERN Open Data Ecosystem) |
| **Recursos de Referencia:** | [CMS Open Data GitHub](https://github.com/cms-opendata-analyses) · [CERN Open Data Portal](https://opendata.cern.ch) |
| **Período Académico:** | Octubre de 2026 (Semana 07) |
| **Sede:** | Sangolquí, Ecuador |

---

> ### Resumen Ejecutivo
> El presente informe técnico analiza los principios estructurales, metodológicos y operativos que rigen la organización de un proyecto tecnológico de nivel internacional. Tomando como caso de estudio el ecosistema de análisis de datos abiertos de la colaboración CMS del CERN ([cms-opendata-analyses](https://github.com/cms-opendata-analyses) y [CERN Open Data](https://opendata.cern.ch/)), se examina cómo la arquitectura de repositorios distribuidos, el desacoplamiento de datos y código, la documentación exhaustiva y los flujos de integración mediante Pull Requests resuelven la brecha de reproducibilidad en la investigación científica y la ingeniería de software moderna. Finalmente, se articula la extrapolación directa de estas prácticas al diseño de infraestructuras de red seguras en el proyecto *HospitaLink-Secure*.

---

## 1. Problema y Necesidad que Aborda el Proyecto Analizado

El ecosistema de análisis abiertos de **CMS Open Data** aborda una necesidad crítica en la ciencia contemporánea: la **democratización del acceso a datos científicos de frontera y la eliminación de barreras computacionales**.

Históricamente, los experimentos del Gran Colisionador de Hadrones (LHC) producían decenas de petabytes de colisiones por año, procesables exclusivamente mediante la infraestructura de computación distribuida de la malla WLCG (*Worldwide LHC Computing Grid*) y dependientes del framework monolítico CMSSW (*CMS Software*). Esto creaba una barrera insalvable para investigadores independientes, estudiantes de pregrado e instituciones universitarias que no contaban con clusters de alto rendimiento ni membresías institucionales formales.

El proyecto analizado resuelve este problema al:
1. Publicar conjuntos de datos reales calibrados de colisiones protón-protón en formatos estructurados y accesibles.
2. Desacoplar el análisis físico del framework monolítico, permitiendo la extracción columnar mediante librerías estándares de Python (`uproot`, `awkward-array`, `vector`, `matplotlib`).
3. Habilitar la validación y el descubrimiento pedagógico de fenómenos del Modelo Estándar (como la masa invariante del bosón $Z$ a 91.2 GeV o del mesón $J/\psi$ a 3.1 GeV) en estaciones de trabajo convencionales y entornos locales.

---

## 2. El Papel de los Datos y los Recursos Técnicos

En la estructura de un proyecto tecnológico, los datos y los recursos técnicos constituyen el **sustrato operativo** que valida o invalida los objetivos de diseño:

* **Arquitectura de Datos Columnar:** Los datos no se almacenan como blobs binarios opacos ni en tablas relacionales rígidas. En CMS Open Data, se emplea el formato columnar ROOT (específicamente la especificación ligera *NanoAOD*). Este enfoque aísla las variables cinemáticas (momentos transversales $p_T$, pseudorrapideces $\eta$, ángulos azimutales $\phi$) en arreglos contiguos de memoria. Esto permite leer exclusivamente las ramas requeridas (por ejemplo, muones aislados), reduciendo el tamaño por evento de megabytes a solo ~1.5–2 kB/evento.
* **Recursos Técnicos y Software Libre:** El empleo de librerías abiertas de la suite Scikit-HEP permite procesar arrays multidimensionales e irregulares (*jagged arrays*) a velocidad nativa de C++ mediante NumPy, eliminando la necesidad de licencias privativas y permitiendo la ejecución dentro de terminales Linux bajo WSL o entornos locales Windows sin dependencias propietarias.

---

## 3. Organización del Trabajo a través del Repositorio Git

El repositorio en Git y plataformas colaborativas (GitHub/GitLab) actúa como la **única fuente de la verdad** (*Single Source of Truth*). La organización observada en proyectos como `cms-opendata-analyses` estructura el trabajo de forma modular y predecible:

```text
proyecto-tecnico/
├── .github/              # Automatizaciones CI/CD, plantillas de Issues y Pull Requests
├── code/ / src/          # Código fuente modular, algoritmos de filtrado y scripts ejecutables
├── notebooks/            # Cuadernos interactivos para exploración guiada y visualización
├── data/ / metadata/     # Esquemas de datos, metadatos JSON y descriptores de datasets (no datos pesados)
├── docs/                 # Documentación técnica, manuales de instalación y diagramas de arquitectura
├── tests/                # Pruebas unitarias y validaciones de consistencia física o funcional
├── .gitignore            # Exclusión estricta de binarios, archivos temporales y datos crudos
├── LICENSE               # Licencia de código abierto (Apache 2.0 / MIT / CC-BY-4.0)
└── README.md             # Punto de entrada principal con instrucciones de reproducibilidad
```

Esta estructura previene la contaminación del historial de Git con datos masivos (manejados vía enlaces DOI o clientes CLI dedicados), delimita las responsabilidades de cada componente y permite a múltiples desarrolladores trabajar en paralelo sin colisiones de código.

---

## 4. Importancia de la Documentación y la Reproducibilidad

En ingeniería de software y computación aplicada, **un desarrollo que no es reproducible carece de rigor técnico y valor profesional**:

1. **La Documentación como Interfaz Humana:** El archivo `README.md` no es un mero adorno; es el contrato operativo del proyecto. Especifica el contexto científico, la arquitectura del software, los requisitos de hardware y el procedimiento determinista paso a paso para desplegar la solución.
2. **Especificación Determinista de Entornos:** La inclusión explícita de archivos de dependencias (`requirements.txt` o `environment.yml` con versiones fijas) evita el síndrome de *"en mi máquina sí funciona"*.
3. **Persistencia y Validación Científica:** La reproducibilidad garantiza que cualquier ingeniero, evaluador del CERN o auditor externo pueda clonar el repositorio, ejecutar el pipeline de procesamiento y obtener exactamente el mismo resultado experimental, asegurando la transparencia y la auditabilidad técnica.

---

## 5. Función de la Revisión de Pull Requests en el Desarrollo en Equipo

La revisión de Pull Requests (*Peer Code Review*) en un modelo de ramas protegidas (*Protected Main Branch*) cumple cuatro funciones primordiales:

| Dimensión de Control | Función Operativa en el Pull Request |
| :--- | :--- |
| **Control de Calidad (QA):** | Detección precoz de bugs lógicos, fugas de memoria, loops ineficientes o vulnerabilidades de seguridad antes de fusionar el código a la rama principal. |
| **Mantenimiento de Estándares:** | Verificación del cumplimiento de guías de estilo (PEP 8, convenciones de nombres, estructura de commits descriptivos). |
| **Integración Continua (CI):** | Disparo automático de flujos de prueba (linters, pruebas de integración y validación de sintaxis) que certifican que los cambios no rompen funcionalidades previas. |
| **Transferencia de Conocimiento:** | Espacio pedagógico donde revisores y contribuidores intercambian retroalimentación técnica, asegurando que todo el equipo conozca la evolución del sistema. |

---

## 6. Prácticas Adoptadas para Proyectos Propios

A partir de la evaluación estructural, aplico e implemento formalmente las siguientes prácticas en mi portafolio técnico y en la formulación de mi proyecto de red hospitalaria (**HospitaLink-Secure**):

1. **Flujo de Trabajo Estricto con Ramas (*Feature Branching*):**  
   Aislamiento completo de nuevas funcionalidades en ramas independientes (`feat/vlan-segmentation`, `feat/acl-security`), prohibiendo commits directos sobre `main` y exigiendo revisiones sistemáticas antes de la fusión.
2. **Modularidad y Desacoplamiento Arquitectónico:**  
   Separación limpia entre archivos de configuración de red (`.cfg`), documentación técnica (`.md`) y topologías en emulador GNS3, asegurando trazabilidad sin saturar el repositorio.
3. **Documentación Exhaustiva y Control de Versiones Atómico:**  
   Adopción del estándar *Conventional Commits* (`docs:`, `feat:`, `fix:`) y redacción de bitácoras (*Sprint Logs*) que documenten no solo el éxito de una implementación, sino las incidencias técnicas y su resolución metódica.

---

## 7. Evidencias Concretas y Enlaces a los Recursos Revisados

| Recurso / Evidencia | Identificador / Enlace Web | Evidencia Concreta Observada |
| :--- | :--- | :--- |
| **Repositorio Oficial Analizado:** | [cms-opendata-analyses](https://github.com/cms-opendata-analyses) | Estructura modular de análisis abiertos, separación de dependencias y scripts de lectura de datos de colisiones CMS. |
| **Portal de Datos Abiertos CERN:** | [CERN Open Data Portal](https://opendata.cern.ch) | Catálogo indexado por DOI, registros de metadatos de colisiones `/SingleMu/` y licencias abiertas para investigación. |
| **Contribución Open Source Propia:** | [First Contributions PR #125407](https://github.com/firstcontributions/first-contributions/pull/125407) | Ejecución real del flujo *Forking Workflow*, apertura de Pull Request, revisión por mantenedores y merge a la rama principal. |
| **Análisis Práctico en Portafolio:** | [`Analisis_Dimuones_CERN.ipynb`](https://github.com/ajzambrano12-cloud/-cern-preparation-program-Angeles/blob/main/semana-02/ejercicios/Analisis_Dimuones_CERN.ipynb) | Reconstrucción cinemática reproducible de la masa invariante de dimuones ($J/\psi$ y $Z$) usando datos abiertos reales. |
| **Planificación del Proyecto Propio:** | [`01-planificacion-inicial-proyecto.md`](https://github.com/ajzambrano12-cloud/-cern-preparation-program-Angeles/blob/main/semana-07/evidencias/01-planificacion-inicial-proyecto.md) | Estructuración del proyecto HospitaLink-Secure (GNS3, 4 VLANs, ACLs y matriz de riesgos) siguiendo metodología ágil. |
