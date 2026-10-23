# Actividad 2.1 — Registro y Bitácora del Trabajo de la Sesión (Sprint Log)
### Reporte de Progreso, Trazabilidad de Evidencias, Resolución de Incidencias Técnicas y Próximos Pasos

**Universidad de las Fuerzas Armadas – ESPE**  
**Departamento de Ciencias Exactas / Ingeniería en Tecnologías de la Información**  
**Programa de Preparación para Oportunidades CERN 2026 (PREP CERN)**  
**Módulo 7:** Sprint Técnico y Gestión Ágil de Proyectos

---

### Metadatos del Registro

| Parámetro Institucional | Especificación |
| :--- | :--- |
| **Estudiante / Autora:** | Angeles Julieth Zambrano Bravo |
| **Identificación Digital / GitHub:** | [@ajzambrano12-cloud](https://github.com/ajzambrano12-cloud) |
| **Programa Académico:** | Ingeniería en Tecnologías de la Información (4.° Semestre) — ESPE |
| **Asignatura / Actividad:** | CERN / Actividad 2.1 — Registro del Trabajo de la Sesión |
| **Marco Metodológico:** | *Sprint Review & Retrospective* (Atlassian Agile Guide / Scrum) |
| **Período de Ejecución:** | Octubre de 2026 (Semana 07) |
| **Sede:** | Sangolquí, Ecuador |

---

> ### Resumen Ejecutivo de la Sesión
> El presente documento constituye el registro formal de actividades (*Sprint Log & Progress Review*) desarrollado durante la Semana 07 del programa. Se sintetizan los avances acumulados en el dominio de datos del CERN y la formulación de proyectos tecnológicos, la consolidación de la propuesta **HospitaLink-Secure** (simulación de red hospitalaria segmentada en GNS3 con VLANs y políticas de seguridad ACLs), la trazabilidad completa mediante enlaces a repositorios y evidencias, la documentación de tres problemas técnicos reales resueltos exitosamente, el inventario de actividades pendientes y la definición de próximos pasos para la etapa de desarrollo y mentorías internacionales.

---

## 1. Actividades en las que se Avanzó

Durante este ciclo y sesión de trabajo, el progreso técnico se consolidó en los siguientes ejes fundamentales:

1. **Planificación Inicial del Proyecto Tecnológico HospitaLink-Secure (Semana 07):**  
   * Selección y delimitación temática orientada a infraestructura y seguridad: diseño de una red hospitalaria emulada en **GNS3** que segmenta de forma estricta los departamentos de **Urgencias, Laboratorio, Farmacia y Administración**.
   * Definición del objetivo general y específicos, alcance riguroso (*In-Scope* vs. *Out-of-Scope*), determinación de tres hitos clave de entrega, distribución de roles en equipo ágil (Líder TI, Ciberseguridad y UX/Documentación), matriz de mitigación de riesgos técnicos (saturación de CPU en GNS3 y bloqueo erróneo de tráfico médico) y diseño del *roadmap* en cuatro fases iterativas.
2. **Consolidación Metodológica y Científica Previa (Semanas 01 a 06):**  
   * **Cómputo Científico con CMS Open Data:** Lectura columnar con `uproot`, manipulación de arreglos irregulares con `awkward-array` y reconstrucción cinemática de masa invariante para resonancias de dimuones ($J/\psi$ y $Z$).
   * **Control de Versiones y Trabajo Colaborativo:** Dominio de ramas de características, resolución de Pull Requests locales (PR #1 y PR #2) y contribución Open Source verificada en el repositorio global *First Contributions* (PR #125407).
   * **Perfil y Proyección Profesional:** Optimización del perfil de LinkedIn, estructuración del CV técnico en estándar Europass y redacción formal de la carta de motivación en inglés para el *CERN Summer Student Programme*.
   * **Metodología de Investigación (Elsevier & S. Keshav):** Delimitación del problema de ancho de banda en redes académicas con CMS NanoAOD y análisis crítico en tres pasadas del artículo de referencia *The CMS NanoAOD format* (Rizzi et al., 2019).
3. **Saneamiento Integral y Reorganización del Portafolio:**  
   * Estandarización de la estructura de directorios (`README.md`, `ejercicios/` y `evidencias/`) en todos los módulos.
   * Purgado exhaustivo de referencias ajenas al perfil de la estudiante, garantizando total fidelidad con la formación en Tecnologías de la Información y experiencia en soporte técnico.

---

## 2. Enlaces a Repositorios, Documentos y Evidencias Relevantes

Toda la producción técnica se encuentra versionada de forma transparente y pública:

* **Repositorio Oficial del Programa:**  
  [https://github.com/ajzambrano12-cloud/-cern-preparation-program-Angeles](https://github.com/ajzambrano12-cloud/-cern-preparation-program-Angeles)
* **Directorio y Evidencias de la Semana 07:**  
  [https://github.com/ajzambrano12-cloud/-cern-preparation-program-Angeles/tree/main/semana-07](https://github.com/ajzambrano12-cloud/-cern-preparation-program-Angeles/tree/main/semana-07)
* **Planificación del Proyecto HospitaLink-Secure (Evidencia 1):**  
  [`semana-07/evidencias/01-planificacion-inicial-proyecto.md`](https://github.com/ajzambrano12-cloud/-cern-preparation-program-Angeles/blob/main/semana-07/evidencias/01-planificacion-inicial-proyecto.md)
* **Repositorio de Práctica Fundamental de Git:**  
  [https://github.com/ajzambrano12-cloud/mi-proyecto-git](https://github.com/ajzambrano12-cloud/mi-proyecto-git)
* **Primera Contribución Open Source Aprobada (PR #125407):**  
  [https://github.com/firstcontributions/first-contributions/pull/125407](https://github.com/firstcontributions/first-contributions/pull/125407)
* **Perfil Profesional Optimizado en LinkedIn:**  
  [https://www.linkedin.com/in/angeles-julieth-zambrano-angeles-a94327303/](https://www.linkedin.com/in/angeles-julieth-zambrano-angeles-a94327303/)
* **Perfil Oficial de Desarrolladora en GitHub:**  
  [https://github.com/ajzambrano12-cloud](https://github.com/ajzambrano12-cloud)

---

## 3. Problemas Técnicos Encontrados y Soluciones Implementadas

Durante el desarrollo de la sesión se identificaron y solventaron tres incidencias técnicas complejas:

| Incidencia / Desafío Técnico | Causa Raíz Diagnosticada | Solución y Mitigación Aplicada |
| :--- | :--- | :--- |
| **1. Deformación de diagramas ASCII en renderizado web** | Los bloques de código con cajas Unicode (`┌─┐`) para el método de Keshav y flujo de datos no eran responsivos y sufrían saltos de línea automáticos en GitHub y pantallas móviles, haciéndolos ilegibles. | Se eliminaron por completo las cajas ASCII y se rediseñó el contenido utilizando **tablas Markdown nativas** con alineación centrada y columnas estructuradas, garantizando visualización perfecta en cualquier resolución. |
| **2. Rechazo de `git push` por desincronización de commits** | La rama remota en GitHub contenía un commit previo (`Update 02-analisis...`) no integrado en el historial local, generando un error `rejected (fetch first)`. | Se ejecutó un flujo de sincronización limpio: `git fetch origin main` seguido de `git pull --rebase origin main`, integrando los cambios remotos y preservando una historia de commits atómica y lineal antes del push definitivo. |
| **3. Bloqueos de procesos en automatización de Word COM** | Al compilar documentos `.docx` a `.pdf` mediante PowerShell, la instancia de Microsoft Word quedaba bloqueada si existían procesos huérfanos previos en memoria o alertas interactivas. | Se desarrolló un script con gestión estricta de ciclo de vida: cierre forzoso de instancias residuales (`Stop-Process WINWORD`), generación a archivos temporales aislados (`_Tmp.docx` / `_Tmp.pdf`) y liberación explícita de objetos COM (`ReleaseComObject`). |

---

## 4. Actividades que Todavía Quedan Pendientes

* **Implementación Práctica de la Topología en GNS3:** Montaje efectivo de los nodos Cisco IOS y configuración de subinterfaces en el entorno local (Fases 1 y 2 del roadmap de HospitaLink-Secure).
* **Participación en las Fases Avanzadas del Programa (Semanas 08 a 10):**
  * Semana 08: Delimitación temática formal y conformación definitiva de equipos.
  * Semana 09: Sesiones de mentoría técnica y retroalimentación con especialistas internacionales.
  * Semana 10: Preparación de la presentación ejecutiva y defensa técnica final de proyectos.
* **Continuidad en la Certificación de Inglés Técnico:** Progresión del plan lingüístico desde nivel A2 hacia B1/B2 enfocado en correspondencia científica y entrevistas técnicas (*English for Interviews*).

---

## 5. Próximos Pasos para Continuar Avanzando

1. **Configuración de Imágenes y Optimización en GNS3:**  
   Importar las imágenes de routers Cisco IOS (c7200 / IOSv) en GNS3, calcular y fijar los valores óptimos de `Idle-PC` para evitar la saturación de CPU en la estación anfitriona Windows/WSL.
2. **Generación de Archivos de Configuración Base:**  
   Crear plantillas de configuración inicial de switches (`VLAN_setup.cfg`) y router (`interVLAN_routing.cfg`) en el directorio `semana-07/ejercicios/`.
3. **Alineación con la Semana 08 (Formulación de Proyectos):**  
   Revisar la guía de conformación de equipos y especificación de hitos del programa PREP CERN para presentar formalmente la propuesta ante los mentores.
