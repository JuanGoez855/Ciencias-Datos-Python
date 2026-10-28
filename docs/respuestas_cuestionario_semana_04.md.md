# Cuestionario de Conocimientos — Semana 4
**Programa:** Ciencia de Datos con Python / ADSO  
**Módulo:** Selección, filtrado y lectura crítica de datos con Pandas (GFPI-F-135)

---

### 1. Explique la diferencia entre `df["nombre"]` y `df[["documento", "nombre"]]`.
- **`df["nombre"]`**: Utiliza un solo par de corchetes y selecciona una única columna, devolviendo una estructura unidimensional de tipo **`pandas.Series`**.
- **`df[["documento", "nombre"]]`**: Utiliza doble par de corchetes y selecciona una o más columnas especificadas en una lista, conservando la estructura bidimensional de tabla de tipo **`pandas.DataFrame`**.

---

### 2. ¿En qué se diferencian `loc` e `iloc`? Dé un ejemplo relacionado con su CSV.
- **`loc`**: Selecciona filas y columnas basándose en **etiquetas** (nombres de índices y nombres de columnas) o en máscaras booleanas. Los cortes por rango en `loc` son **inclusivos** en ambos extremos (ej. `0:4` incluye la fila 4).
- **`iloc`**: Selecciona filas y columnas basándose exclusivamente en **posiciones enteras** (basadas en índice 0). El extremo derecho del corte en `iloc` es **exclusivo** (ej. `0:4` toma las filas 0, 1, 2 y 3).

*Ejemplo sobre el CSV:*
```python
# loc por etiqueta de columna
df.loc[:, ["documento", "nombre", "asistencia"]]

# iloc por posición (primeras 4 filas, primeras 3 columnas)
df.iloc[:4, :3]
```

---

### 3. ¿Por qué es obligatorio agrupar cada comparación entre paréntesis cuando usa `&` o `|`?
En Python, los operadores bit a bit (`&` para Y, `|` para O) tienen una mayor prioridad/precedencia sintáctica que los operadores de comparación (`<`, `>`, `==`). Sin los paréntesis, Python intentaría evaluar primero la operación lógica entre los operandos internos antes de hacer la comparación de las Series, desencadenando errores de tipo (`TypeError` o `ValueError`). 

*Correcto:* `(df["asistencia"] < 80) & (df["programa_normalizado"] == "ADSO")`

---

### 4. ¿Qué ocurre con los extremos de un intervalo en `between(3, 4)` por defecto?
Por defecto, el método `Series.between(a, b)` aplica el argumento `inclusive="both"`. Esto significa que el intervalo es **inclusivo en ambos extremos** ($\ge 3.0$ y $\le 4.0$), incluyendo tanto las notas exactas de 3.0 como las de 4.0 en el resultado.

---

### 5. ¿Cuándo conviene utilizar `isin()` en vez de comparar con una sola categoría?
Conviene utilizar `isin()` cuando se requiere evaluar la pertenencia a un **conjunto o lista de múltiples categorías** de forma limpia y eficiente. Evita escribir múltiples condiciones compuestas repetitivas conectadas por el operador `|` (O).

*Ejemplo:* `df["programa_normalizado"].isin(["ADSO", "Ciencia de datos con Python"])`

---

### 6. ¿Para qué sirve `@variable` en una expresión `query()`?
La sintaxis `@variable` dentro del método `.query()` permite hacer referencia e **inyectar dinámicamente el valor de una variable del entorno local de Python** dentro de la cadena de consulta de Pandas, manteniendo el código limpio, reutilizable y seguro.

---

### 7. ¿Por qué una asistencia vacía (`NaN`) no equivale a asistencia igual a cero (`0`)?
Un valor nulo o ausente (`NaN`) representa una **falta de información o dato no registrado**, mientras que un valor de `0` representa un **hecho medido e informado** (asistir al 0% de las clases). Tratar un nulo como cero invalida la calidad del dato al imponer un valor falso que sesga negativamente los promedios y reportes.

---

### 8. Si un documento se repite con notas distintas, ¿qué precaución debe tener al contar aprendices?
No se debe asumir que cada fila/registro equivale a una persona o aprendiz único. Contar simplemente la cantidad de filas (`len(df)`) inflaría artificialmente las cifras de aprendices. Es obligatorio aplicar filtros de unicidad o aislar y documentar las claves en conflicto antes de computar métricas de personas.

---

### 9. ¿Qué controles aplicaría para asegurar que un subconjunto cumple todos los filtros?
1. **Comprobación lógicas con `assert`**: Evaluar invariantes del subconjunto (ej. `assert sub["asistencia"].lt(80).all()`).
2. **Verificación de nulos**: Asegurar que los campos no contengan ausencias imprevistas con `.notna().all()`.
3. **Auditoría de dimensiones**: Validar que la cantidad de filas en el resultado coincida exactamente con la suma de la máscara booleana (`len(sub) == int(mascara.sum())`).

---

### 10. Escriba una conclusión que los datos permitan y otra que los datos no permitan afirmar.
- **Conclusión permitida por los datos:** *"En el conjunto de datos preparado existen 3 registros únicos correspondientes al programa ADSO cuya asistencia registrada es inferior al umbral didáctico del 80%."*
- **Conclusión NO permitida por los datos:** *"Los aprendices con bajo porcentaje de asistencia perdieron la materia debido a problemas de conectividad a internet."* (El conjunto de datos no registra causales de deserción ni factores socioeconómicos).