# Rúbrica de Evaluación — Módulo 4 · Tema 2 (GLM con Python)
### Archivo evaluado: `evaluacion_M4T2.md` respondido por cada alumno

**Escala:** 100 puntos → calificación /10. Aprobatorio ≥ 60.
Cada alumno responde 9 preguntas sobre **su variable asignada** (ver `asignaciones.csv`).

| Componente | Preguntas | Puntos |
|---|---|---|
| Parte 1 · Frecuencia | P1, P2, P3 | 30 (10 c/u) |
| Parte 2 · Severidad y selección | P4, P5, P6 | 30 (10 c/u) |
| Parte 3 · Validación y tarifa | P7, P8, P9 | 30 (10 c/u) |
| Redacción / nota técnica (global) | — | 10 |
| **Total** | | **100** |

## Bandas por pregunta (cada una vale 10)

| Banda | Puntos | Qué es |
|---|---|---|
| Completa | 8–10 | Contesta todo lo pedido, interpreta correctamente los números, sin errores conceptuales |
| Parcial | 4–7 | Interpreta la mayoría pero con imprecisiones u omisiones |
| Insuficiente | 1–3 | Solo describe/pega el número sin interpretarlo, o lo malinterpreta |
| Vacía | 0 | Sin responder |

---

## Clave de respuestas (qué debe contener cada pregunta completa)

**P1 · Equidispersión.** Debe decir que φ ≈ 1.17 > 1 y que Cameron-Trivedi (p ≈ 10⁻⁵⁶) **rechaza**
la equidispersión → hay sobredispersión, pero **leve** (φ < 1.5), por lo que **QuasiPoisson** basta
(no hace falta Binomial Negativa, que se justifica con φ > 2).

**P2 · Rating factors de frecuencia.** Identifica el nivel de mayor y menor RF de su variable,
los traduce a % de recargo/descuento sobre la referencia, y revisa si algún IC cruza 1 / p > 0.05
(si es así, agruparlo con la referencia; si no, mantenerlo). Debe usar SUS números.

**P3 · Puente empírico.** Porque las ecuaciones de score del Poisson-log obligan a que la suma de
predichos iguale la de observados por nivel → `exp(η)=Σn/Σe` = tasa empírica. El GLM aporta combinar
muchas variables de forma multiplicativa e intervalos de confianza — algo que una tabla no da.

**P4 · Gamma vs log(Y).** CV constante de la Gamma (variabilidad relativa igual en todos los niveles);
Lognormal no pertenece a la familia exponencial natural (estadístico suficiente log y, no y), y una
regresión sobre log(Y) modela E[log Y] ≠ E[Y] y necesita corrección por sesgo. Gamma modela E[Y] directo.

**P5 · Comparación de modelos.** Elige por **menor AIC/BIC** (en la tabla gana Binomial Negativa por poco).
Explica que el pseudo R² bajo (~0.02) es **normal en seguros** por la aleatoriedad irreducible de la
frecuencia, y que lo relevante es la comparación relativa y la discriminación (Gini), no un R² alto.

**P6 · Freq vs Sev.** Compara la dirección de los RF de frecuencia vs severidad de su variable.
Puede que apunten distinto (una variable predice "cuántos" pero no "de qué tamaño"), lo que **justifica**
modelar Frecuencia × Severidad por separado.

**P7 · Validación.** Ratio pred/obs ≈ 1 → bien **calibrado** en promedio. Gini mide **discriminación**
(qué tan bien separa riesgos altos de bajos); un Gini ~0.23 es modesto (< 0.30) — el modelo calibra bien
pero discrimina de forma limitada. Debe distinguir calibración de discriminación.

**P8 · Tarifa.** Identifica el nivel con prima pura más alta y más baja de su variable y traduce el
factor de tarifa a recargo/descuento sobre la prima promedio (factor 1.73 = +73%, factor 0.70 = −30%).

**P9 · Nota técnica.** Integra frecuencia + severidad + prima pura de su variable en 3–4 líneas, con
lenguaje actuarial claro y defendible ante CNSF (incluir un rating/factor con su IC).

## Redacción (10 puntos globales)
Claridad, lenguaje actuarial correcto, concisión y coherencia entre las tres partes. Excelente 8–10,
suficiente 4–7, deficiente 0–3.

## Penalizaciones
- Responder sobre una variable que no es la asignada (posible copia): anular las preguntas afectadas.
- Pegar tablas sin interpretación: máximo 40% de la pregunta.
- Respuestas idénticas entre alumnos con la misma variable: revisar por copia.
