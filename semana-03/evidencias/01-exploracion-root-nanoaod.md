# ROOT, Python y NanoAOD
### Comprensión de conceptos y relación con el análisis de datos

**Estudiante:** Angeles Zambrano  
**Asignatura:** CERN  
**Actividad:** Preguntas sobre ROOT, Python y NanoAOD  
**Entorno de trabajo:** Python (`~Semana-03`)  
**Institución:** Universidad de las Fuerzas Armadas – ESPE (Sangolquí – Ecuador, 2026)

---

## 1. ROOT

**¿Qué función cumple ROOT dentro del análisis de datos de física de partículas?**

ROOT es el software desarrollado para trabajar con los datos de física de partículas de experimentos como CMS. Cumple dos funciones principales: define el formato de archivo en el que se almacenan todos los datos abiertos de CMS (los archivos `.root`), y ofrece las herramientas para leer, escribir y analizar esos datos rápidamente, por ejemplo llenando y visualizando histogramas de forma sencilla para hacer un primer diagnóstico de la información, sin necesidad de herramientas externas.

---

## 2. Python

**¿Qué ventajas observas al utilizar Python para trabajar con archivos ROOT?**

Usar Python para trabajar con archivos ROOT tiene varias ventajas frente a usar solo C++: no es necesario compilar el código antes de ejecutarlo (Python se interpreta directamente, lo que agiliza las pruebas y correcciones); librerías como `uproot` permiten abrir y leer archivos ROOT sin tener que instalar todo el ecosistema completo de ROOT, lo cual es más simple; y además Python conecta ese análisis con todo el ecosistema científico general (gráficos, estadística, machine learning, etc.) a través de herramientas como Scikit-HEP, awkward arrays y PyROOT (esta última da acceso completo a las funciones de ROOT directamente desde Python).

---

## 3. NanoAOD

**¿Qué es NanoAOD y qué tipo de información puede contener?**

NanoAOD es uno de los formatos de datos abiertos de CMS, usado para datos publicados desde 2016 en adelante. A diferencia de sus predecesores (AOD y MiniAOD), que se almacenan como clases de C++ propias de CMSSW, NanoAOD se guarda directamente como objetos ROOT TTree, lo que permite analizarlo con ROOT o con librerías de Python sin necesitar software específico de CMS. Contiene variables de tipos fundamentales (números flotantes, enteros, booleanos) que describen los objetos físicos reconstruidos en cada evento: electrones, muones, jets, vértices secundarios, energía faltante (MET), entre otros.

---

## 4. NanoAOD vs. MiniAOD

**Menciona una diferencia que hayas identificado entre ambos formatos.**

Una diferencia clara es que MiniAOD conserva la mayoría de los constituyentes de un objeto físico (por ejemplo, el track completo o los clusters de calorímetro asociados a un electrón), mientras que NanoAOD solo guarda un resumen de esa información (por ejemplo, en vez del track completo guarda solo su parámetro de impacto respecto al vértice primario). Esto hace a NanoAOD mucho más liviano y fácil de analizar, aunque con menos detalle que MiniAOD.

---

## 5. Aplicación

**Imagina que tienes que analizar una gran cantidad de eventos registrados por CMS. ¿Por qué podría ser útil utilizar NanoAOD y herramientas como Python/ROOT?**

Si se necesita analizar una gran cantidad de eventos de CMS, usar NanoAOD junto con Python (`uproot`, `awkward`) y/o ROOT es muy útil porque: NanoAOD ya viene reducido a la información esencial de cada evento, lo que hace los archivos más pequeños y rápidos de procesar; al estar en formato ROOT TTree, se puede leer sin instalar el software completo de CMSSW, ahorrando tiempo de configuración; y Python permite automatizar el análisis de miles o millones de eventos con pocas líneas de código, aplicar filtros, graficar distribuciones y manejar de forma eficiente estructuras de datos irregulares (como el número variable de partículas por evento) usando awkward arrays.

---

## Reflexión final

**¿Qué parte de la actividad te resultó más difícil de comprender?**

La parte que resultó más difícil de comprender fue el manejo de los arreglos de longitud variable ("jagged arrays") con la librería awkward, ya que a diferencia de un arreglo normal de NumPy, cada evento puede tener un número distinto de partículas, y es necesario usar funciones como `flatten()` para poder graficar correctamente esos valores.
