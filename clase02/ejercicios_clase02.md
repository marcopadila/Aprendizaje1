
# Clase 2 — Resumen Enriquecido de Ejercicios (desde *Evaluación de Residuos*)

Este documento sintetiza y enriquece los puntos trabajados en el notebook de la Clase 2,
a partir de la sección **1. Evaluación de Residuos**. Incluye consignas, notas catalogadas
como *IMPORTANTE*, conclusiones de bloques de código y aportes adicionales.

---

## 1. Evaluación de Residuos
- **Qué se hace:** Se grafican residuos vs predicciones (`LassoCV`).
- **Conclusión del código:**
  - Los residuos se distribuyen alrededor de 0, de manera aleatoria.
  - No hay patrón evidente → el modelo está capturando bien la relación lineal.
  - Los errores no dependen del valor predicho → condición deseable en un modelo lineal.
- **Idea clave:** Una buena regresión lineal debe mostrar residuos aleatorios, no estructurados.

---

## 2. Cambiar la Métrica de CV
- **Consigna:** Probar `mean_absolute_error` en lugar de `MSE` en `RidgeCV` y `LassoCV`.
- **Notas teóricas (IMPORTANTE en markdown):**
  - **OLS:** minimiza errores cuadrados → sin regularización.
  - **Ridge (L2):** penaliza magnitud de coeficientes, evita sobreajuste.
  - **Lasso (L1):** fuerza algunos coeficientes a cero → selección de variables.
  - **RidgeCV/LassoCV:** usan CV para elegir α automáticamente.
- **Conclusión del código:**
  - Los valores de α cambian según la métrica.
  - **MAE** da más peso a errores medios, **MSE** castiga más los errores grandes.
- **Idea clave:** La métrica de evaluación condiciona la elección de hiperparámetros y la “forma” del modelo.

---

## 3. Implementar K-Fold a Mano
- **Consigna:** Reproducir lo que hace `RidgeCV` usando `KFold(n_splits=5)` manualmente.
- **Notas (IMPORTANTE):**
  - KFold divide los datos en 5 pliegues.
  - Cada observación se usa tanto en train como en validación, pero nunca simultáneamente.
- **Conclusión del código:**
  - El `MSE` promedio manual ≈ resultado de `RidgeCV`.
  - Confirma que CV robusto entrega resultados estables.
- **Idea clave:** KFold da una estimación más confiable que un único split.

---

## 4. Características Polinómicas
- **Consigna:** Agregar `GrLivArea²` y comparar R².
- **Conclusión del código:**
  - El R² mejora ligeramente al agregar el término cuadrático.
  - Muestra que capturar relaciones no lineales (aunque simples) puede aumentar el poder explicativo.
- **Idea clave:** El *feature engineering* polinómico es útil cuando la relación no es estrictamente lineal.

---

## 5. Impacto de Outliers
- **Consigna:** Quitar la casa más cara y reentrenar OLS.
- **Conclusión del código:**
  - R² mejora (ej: de 0.8346 → 0.8357).
  - Los coeficientes cambian, mostrando que los outliers distorsionaban el ajuste.
- **Idea clave:** Los outliers tienen efecto desproporcionado en regresión lineal → conviene detectarlos.

---

## 6. Comparar MAE vs MSE
- **Consigna:** Calcular MAE en OLS, RidgeCV y LassoCV.
- **Notas teóricas (IMPORTANTE):**
  - **MAE:** promedio de errores absolutos → más interpretable.
  - **MSE:** errores al cuadrado → castiga fuertemente los grandes errores.
- **Conclusión del código:**
  - Siempre MAE < MSE porque el cuadrado amplifica los errores.
- **Idea clave:** La métrica elegida refleja qué tipo de error se quiere minimizar.

---

## 7. Importancia de Características
- **Consigna:** Ordenar coeficientes de RidgeCV en valor absoluto.
- **Conclusión del código:**
  - Identifica las 3 variables más influyentes en el precio.
- **Idea clave:** Ridge no elimina variables, pero sí revela cuáles dominan el modelo.

---

## 8. Efecto del Alpha en Lasso
- **Consigna:** Graficar coeficientes vs α con `lasso_path`.
- **Conclusión visual:**
  - Al aumentar α, los coeficientes se reducen hasta volverse cero.
  - Se observa la **selección de variables** en acción.
- **Idea clave:** Lasso controla complejidad → a mayor α, modelo más simple.

---

## 9. Regresión Lineal Simple vs Múltiple
- **Consigna:** Comparar coeficientes de modelos simples vs OLS múltiple.
- **Notas (IMPORTANTE):**
  - En regresión simple, el coef mide el efecto bruto de la variable.
  - En múltiple, mide el efecto **controlando por las otras**.
- **Conclusión del código:**
  - Los coeficientes difieren mucho cuando hay correlación entre variables (multicolinealidad).
- **Idea clave:** La interpretación depende de si analizamos una variable sola o en conjunto.

---

## 10. Modelo para Producción
- **Pregunta:** ¿Qué modelo elegirías para producción?
- **Respuesta (IMPORTANTE en markdown):** **LassoCV**.
- **Justificación:**
  - R² y MSE similares a Ridge.
  - Selección automática de variables → interpretabilidad.
  - Simplicidad y menor riesgo de sobreajuste.
- **Idea clave:** En producción, no siempre se busca el mejor R², sino un balance entre precisión, interpretabilidad y simplicidad.

---

# 📌 Síntesis General (puntos 1–10)
- Se cubren conceptos de **validación cruzada, métricas, regularización, outliers, polinomios y selección de modelo**.
- El hilo conductor es entender que **las decisiones técnicas (métrica, α, outliers, features) alteran fuertemente el modelo final**.
- Conclusión global: **LassoCV es la mejor elección en este caso** porque equilibra desempeño, interpretabilidad y simplicidad.
