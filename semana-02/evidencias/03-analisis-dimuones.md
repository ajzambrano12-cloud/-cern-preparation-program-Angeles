# Evidencia 3 — Primer análisis de datos con Python

**Estudiante:** Angeles Julieth Zambrano Bravo  
**Actividad:** Análisis de datos utilizando Python y Jupyter Notebook  
**Cuaderno:** [`semana-02/ejercicios/Analisis_Dimuones_CERN.ipynb`](../ejercicios/Analisis_Dimuones_CERN.ipynb)  
**Dataset:** `Dimuon_DoubleMu.csv` — CMS Open Data, Run2011A ([Enlace al dataset](https://opendata.cern.ch/record/545))

---

## 1. Descripción del ejercicio

Se desarrolló un ejercicio de análisis exploratorio en Python con datos de colisiones reales protón-protón del detector CMS (LHC, 2011) en las que se detectaron pares de muones. El cuaderno sigue los 5 pasos solicitados:

1. **Carga de datos:**  
   Se importaron las librerías `pandas`, `numpy` y `matplotlib`. Se cargó el archivo con 100,000 filas y 21 columnas.
2. **Exploración:**  
   Se revisó la estructura de las columnas (momentos, energías, cargas de cada muon y masa invariante `M`), tipos de datos y se confirmó que no hay valores nulos.
3. **Análisis:**  
   - Se verificó la conservación de carga: todos los pares del dataset filtrado tienen carga opuesta ($Q_1 \neq Q_2$).
   - Se calcularon estadísticas descriptivas de los momentos transversos y las masas invariantes en distintas regiones.
4. **Visualización:**  
   - Histograma de la masa invariante ($M$) con escala logarítmica para observar las resonancias.
   - Gráfico de dispersión de $p_{T1}$ vs $p_{T2}$ mostrando la concentración en momentos transversos bajos.
5. **Interpretación:**  
   - El histograma muestra picos claros correspondientes a partículas conocidas: el pico en ~3.1 GeV corresponde al mesón $J/\psi$ y alrededor de 91 GeV aparece el pico del bosón $Z$.
   - La mayoría de los pares provienen de la desintegración de una partícula neutra (carga neta 0).
   - Estos resultados demuestran cómo a partir de datos abiertos se pueden redescubrir experimentalmente partículas del Modelo Estándar.
