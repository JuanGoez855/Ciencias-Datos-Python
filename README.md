# Ciencia de Datos con Python — SENA CTMA

**Aprendiz:** Juan David Londoño Goez  
**Programa:** Tecnología en Análisis y Desarrollo de Software (ADSO) — SENA CTMA  
**Ficha:** 3223875  
**Instructor:** Wilson Castro Gil  
**Entorno de Trabajo:** Python 3.11+ | Jupyter Notebooks | Pandas | NumPy  

---

## 📌 Descripción del Proyecto
Este repositorio documenta la progresión práctica y los laboratorios del componente de **Ciencia de Datos con Python**. El proyecto está estructurado como un ambiente de trabajo reproducible para el seguimiento académico ficticio de aprendices, abarcando desde los fundamentos del entorno hasta la evaluación técnica de calidad de datos[cite: 1, 5].

---

## 📂 Estructura Reproducible del Proyecto

diagnostico_nosql/
├── data/
│   ├── raw/                                                # Datos originales sin modificar (protegidos)
│   │   ├── seguimiento_aprendices_semana2.csv             # Insumo base Semana 2
│   │   ├── seguimiento_aprendices_semana2.xlsx            # Insumo base Excel Semana 2
│   │   └── seguimiento_academico_semana3_con_errores.csv  # Dataset sucio de prueba para perfilamiento (Semana 3)
│   └── processed/                                          # Datasets transformados y limpios
│       ├── seguimiento_semana2_procesado.csv
│       ├── seguimiento_semana2_procesado.xlsx
│       └── seguimiento_academico_semana3_preparado.csv    # Dataset procesado y validado (Semana 3)
├── notebooks/
│   ├── semana2_laboratorio.ipynb                           # Estructuras básicas, NumPy, Pandas e inspección (Semana 2)
│   └── Laboratorio_Semana_03_Perfilamiento_Calidad_Datos.ipynb # Perfilamiento, diagnóstico de calidad y reglas (Semana 3)
├── outputs/                                                # Evidencias exportadas y reportes de calidad
│   ├── reporte_incidencias_semana3.csv                    # Matriz de validación de reglas (Semana 3)
│   └── duplicados_exactos_retirados.csv                   # Auditoría de filas descartadas (Semana 3)
├── docs/                                                   # Guías de aprendizaje y documentación técnica
├── scripts/                                                # Scripts auxiliares de automatización
├── .gitignore                                              # Exclusión de entornos virtuales y cachés
├── README.md                                               # Documentación principal del repositorio
└── requirements.txt                                        # Dependencias del proyecto (pandas, numpy, openpyxl, jupyter)

---

##  Resumen de Módulos y Avance por Semanas

### 🔹 Semana 1: Entorno Reproducible y Ética de Datos
- Configuración del ambiente virtual (`.venv`) e instalación del stack analítico.
- Creación de la matriz dato-información-decisión y formulación de preguntas analíticas iniciales.

### 🔹 Semana 2: Estructuras Básicas, Pandas e Inspección Inicial
- Manipulación de estructuras nativas (listas, diccionarios) y arreglos vectorizados con **NumPy**[cite: 1].
- Manejo de **Series** y **DataFrames** con **Pandas**[cite: 1].
- Lectura/Escritura reproducible con rutas relativas (`pathlib.Path`) en formatos CSV y Excel[cite: 1].
- Primer informe exploratorio mediante `head()`, `tail()`, `info()`, `describe()`, `shape` y `dtypes`[cite: 1].

### 🔹 Semana 3: Perfilamiento, Diagnóstico de Calidad y Limpieza Técnica
- **Perfilamiento de Fuentes:** Auditoría de valores nulos, detección de inconsistencias en cadenas de texto y duplicados exactos vs. claves duplicadas.
- **Tipado Seguro:** Conversión de tipos numéricos (`Float64`, `Int64`), manejo de formato decimal latino (reemplazo de `,` por `.`) y parseo riguroso de fechas con `to_datetime`.
- **Evaluación de Dimensiones de Calidad de Datos:**
  - *Completitud:* Evaluación de presencia de datos clave.
  - *Unicidad:* Retiro controlado únicamente de filas exactamente repetidas (`reporte_exactos`).
  - *Consistencia:* Normalización categórica de variables (`programa`, `ciudad`) con mapeos dict[cite: 5].
  - *Validez:* Validación de rangos permitidos en notas **[0.0, 5.0]** y porcentajes de asistencia **[0, 100]**[cite: 5].
  - *Oportunidad:* Evaluación de la ventana de vigencia de registros basada en una fecha de corte fija[cite: 5].
  - *Trazabilidad:* Inserción de trazadores de fila fuente (`fila_fuente`) y archivo de origen[cite: 5].

---

##  Instrucciones de Ejecución

### 1. Activar el Entorno Virtual
Desde PowerShell en la raíz del proyecto:
```powershell
.venv\Scripts\Activate.ps1

### 2. Ejecutar los Notebooks
Abre VS Code o Jupyter Lab en la carpeta `notebooks/` y ejecuta las celdas ordenadamente:
- **Semana 2:** `notebooks/semana2_laboratorio.ipynb`
- **Semana 3:** `notebooks/Laboratorio_Semana_03_Perfilamiento_Calidad_Datos.ipynb`

---

##  Principales Hallazgos Técnicos de Calidad (Semana 3)

1. **Conservación de Claves Duplicadas:** Se demostró que un documento de identidad repetido con notas o datos divergentes no se elimina automáticamente, ya que requiere verificación previa con la fuente de origen.
2. **Protección de Datos Académicos:** Se estableció la regla técnica de **no imputar notas académicas** con promedios o medianas sin evidencia sustantiva, marcando valores fuera de rango o erróneos como valores faltantes (`pd.NA`) para preservar la validez del reporte.
3. **Auditoría de Incidencias:** Se generaron reportes independientes en `outputs/` para auditar exactamente qué filas incumplen las reglas de validez y completitud sin alterar la fuente original.

## Semana 4: Selección, filtrado y lectura crítica de datos con Pandas
- **Notebook principal:** `notebooks/semana_04_seleccion_filtrado.ipynb`
- **Dataset de entrada:** `data/processed/seguimiento_academico_semana3_preparado.csv`
- **Salidas / Evidencias:** 
  - `outputs/semana4_adso_asistencia_baja_validado.csv`
  - `outputs/semana4_bitacora_consultas.csv`
- **Temas aplicados:** Selección por etiquetas y posiciones (`loc`/`iloc`), filtros booleanos con operadores lógicos estrictos (`&`, `|`, `~`), métodos `isin()` y `between()`, validación de nulos y exclusión controlada de claves en conflicto.