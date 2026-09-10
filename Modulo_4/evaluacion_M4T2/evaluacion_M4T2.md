# Evaluación — Módulo 4 · Tema 2: GLM con Python

**Alumno:** Víctor Fernando
**Variable asignada:** `antiguedad_vehiculo_cat`  (antigüedad del vehículo)
**Fecha de entrega:** ________________

> **Instrucciones.** Este archivo evalúa las tres sesiones del tema. Las tablas ya vienen
> calculadas; tu trabajo es **responder las preguntas de interpretación** en el espacio
> "**Tu respuesta:**". Se evalúa la interpretación, no el código. Máx. 4–6 líneas por respuesta.
> Todas tus preguntas usan **tu variable asignada** (`antiguedad_vehiculo_cat`). Guarda y sube este archivo a tu repositorio.

---

## Parte 1 · Sesión 1 — Modelo de Frecuencia

**Diagnóstico del supuesto de Poisson (modelo completo):**

| métrica | valor |
| --- | --- |
| φ de Pearson | 1.1664 |
| Cameron-Trivedi α | 0.0744 |
| z | 15.80 |
| p-value | 3.7e-56 |

**Rating factors de frecuencia para `antiguedad_vehiculo_cat`** (base × RF reproduce la tasa empírica; diferencia máx = 5.2e-05):

| nivel | RF_frec | IC_inf | IC_sup | p | tasa_emp |
| --- | --- | --- | --- | --- | --- |
| (-1, 1] (ref) | 1 | 1 | 1 | 0 | 0.1698 |
| (1, 2] | 0.76 | 0.7037 | 0.8207 | 0 | 0.129 |
| (10, 15] | 0.8825 | 0.826 | 0.9428 | 0.0002 | 0.1498 |
| (15, 50] | 0.6795 | 0.6113 | 0.7553 | 0 | 0.1154 |
| (2, 3] | 0.7254 | 0.6703 | 0.785 | 0 | 0.1231 |
| (3, 4] | 0.7923 | 0.7336 | 0.8557 | 0 | 0.1345 |
| (4, 5] | 0.7934 | 0.7344 | 0.8573 | 0 | 0.1347 |
| (5, 10] | 0.8216 | 0.7718 | 0.8746 | 0 | 0.1395 |

**P1.** ¿Se cumple la equidispersión? Justifica con φ **y** con Cameron-Trivedi, y di qué familia usarías.
**Tu respuesta:**

**P2.** Interpreta los rating factors de tu variable: nivel más alto y más bajo, traducidos a % de
recargo/descuento. ¿Algún IC cruza 1 o tiene p > 0.05? ¿Qué harías con ese nivel?
**Tu respuesta:**

**P3.** ¿Por qué el GLM one-way reproduce exactamente la tasa empírica, y qué aporta el GLM que una
tabla empírica no puede dar?
**Tu respuesta:**

---

## Parte 2 · Sesión 2 — Severidad y Selección de Modelos

**Comparación de modelos de frecuencia:**

| modelo | AIC | BIC | pseudoR2_McF |
| --- | --- | --- | --- |
| Poisson | 125,081.7 | 125,261.7 | 0.0198 |
| Binomial Negativa | 124,925.7 | 125,105.8 | 0.021 |

**Rating factors de severidad (Gamma) para `antiguedad_vehiculo_cat`:**

| nivel | RF_sev | severidad_emp |
| --- | --- | --- |
| (-1, 1] (ref) | 1 | 1,766 |
| (1, 2] | 0.7141 | 1,261 |
| (10, 15] | 0.74 | 1,307 |
| (15, 50] | 0.9099 | 1,607 |
| (2, 3] | 0.6865 | 1,212 |
| (3, 4] | 0.6275 | 1,108 |
| (4, 5] | 0.7341 | 1,296 |
| (5, 10] | 0.7342 | 1,297 |

**P4.** ¿Por qué se usa **Gamma** para severidad y no una regresión lineal sobre log(Y)? (menciona la
propiedad del CV y por qué Lognormal no es GLM).
**Tu respuesta:**

**P5.** Según la tabla de comparación, ¿qué modelo elegirías? Justifica con AIC/BIC. ¿Por qué el pseudo R²
es tan bajo y eso NO significa que el modelo sea malo?
**Tu respuesta:**

**P6.** Compara tus rating factors de frecuencia (Parte 1) con los de severidad para `antiguedad_vehiculo_cat`. ¿Apuntan en
la misma dirección? ¿Qué implica eso para separar Frecuencia × Severidad?
**Tu respuesta:**

---

## Parte 3 · Sesión 3 — Validación y Tarifa

**Validación out-of-sample del modelo de frecuencia:**

| metrica | valor | ideal |
| --- | --- | --- |
| Gini (test) | 0.2315 | > 0.30 aceptable |
| Ratio pred/obs (test) | 1.0249 | ≈ 1.00 |

**Prima pura por nivel de `antiguedad_vehiculo_cat`** (Frecuencia × Severidad, con su factor de tarifa):

| nivel | prima_pura_modelo | factor_tarifa |
| --- | --- | --- |
| (-1, 1] (ref) | 305.2 | 1.6738 |
| (1, 2] | 163.76 | 0.8981 |
| (10, 15] | 194.41 | 1.0662 |
| (15, 50] | 186.66 | 1.0237 |
| (2, 3] | 148.41 | 0.814 |
| (3, 4] | 150.55 | 0.8256 |
| (4, 5] | 176.12 | 0.9659 |
| (5, 10] | 180.37 | 0.9892 |

**P7.** Interpreta las métricas de validación: ¿el modelo está bien calibrado (ratio pred/obs)? ¿discrimina
bien el riesgo (Gini)? ¿Qué mide cada una?
**Tu respuesta:**

**P8.** Lee la tabla de tarifa: ¿qué nivel de tu variable paga la prima pura más alta y cuál la más baja?
Traduce el factor de tarifa a un recargo/descuento sobre la prima promedio.
**Tu respuesta:**

**P9. (Conclusión de nota técnica).** En 3–4 líneas, redacta cómo `antiguedad_vehiculo_cat` afecta la tarifa, integrando
frecuencia, severidad y prima pura, en estilo defendible ante la CNSF.
**Tu respuesta:**

---
*Evaluación generada automáticamente · Diplomado ML en Seguros · FC UNAM · Módulo 4 · Tema 2*
