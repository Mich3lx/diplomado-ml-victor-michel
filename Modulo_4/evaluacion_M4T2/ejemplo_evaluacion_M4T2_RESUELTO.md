# Evaluación — Módulo 4 · Tema 2: GLM con Python

**Alumno:** EJEMPLO RESUELTO (así se entrega — variable `edad_conductor_cat`)
**Variable asignada:** `edad_conductor_cat`  (edad del conductor)
**Fecha de entrega:** 28/08/2026

> **Este es el ejemplo de cómo se entrega.** Las respuestas muestran el nivel de interpretación
> esperado (calificación cercana a 100). Cada alumno responde sobre SU variable asignada.

---

## Parte 1 · Sesión 1 — Modelo de Frecuencia

**Diagnóstico del supuesto de Poisson (modelo completo):**

| métrica | valor |
| --- | --- |
| φ de Pearson | 1.1664 |
| Cameron-Trivedi α | 0.0744 |
| z | 15.80 |
| p-value | 3.7e-56 |

**Rating factors de frecuencia para `edad_conductor_cat`** (base × RF reproduce la tasa empírica; diferencia máx = 4.9e-05):

| nivel | RF_frec | IC_inf | IC_sup | p | tasa_emp |
| --- | --- | --- | --- | --- | --- |
| (17, 30] (ref) | 1 | 1 | 1 | 0 | 0.2134 |
| (30, 35] | 0.7276 | 0.6926 | 0.7643 | 0 | 0.1553 |
| (35, 45] | 0.6583 | 0.632 | 0.6857 | 0 | 0.1405 |
| (45, 50] | 0.6221 | 0.5915 | 0.6543 | 0 | 0.1328 |
| (50, 55] | 0.5934 | 0.5617 | 0.6269 | 0 | 0.1267 |
| (55, 60] | 0.5299 | 0.498 | 0.5638 | 0 | 0.1131 |
| (60, 95] | 0.4665 | 0.4458 | 0.4882 | 0 | 0.0996 |

**P1.** ¿Se cumple la equidispersión? Justifica con φ **y** con Cameron-Trivedi, y di qué familia usarías.
**Tu respuesta:** No se cumple del todo: φ = 1.166 > 1 indica que la varianza excede a la media, y
Cameron-Trivedi lo confirma (α = 0.074, p ≈ 10⁻⁵⁶ ≪ 0.05), así que **rechazamos la equidispersión**.
La sobredispersión es **leve** (φ < 1.5), por lo que **QuasiPoisson** basta —mantiene los coeficientes
y corrige los errores por √φ—; no hace falta Binomial Negativa (esa se justifica con φ > 2).

**P2.** Interpreta los rating factors de tu variable: nivel más alto y más bajo, traducidos a % de
recargo/descuento. ¿Algún IC cruza 1 o tiene p > 0.05? ¿Qué harías con ese nivel?
**Tu respuesta:** La referencia es (17,30] (RF = 1), el grupo de mayor riesgo. El RF más bajo es
(60,95] con 0.467 → un **descuento del 53.3%** en frecuencia respecto a los jóvenes; el más alto,
después de la referencia, es (30,35] con 0.728 → **−27.2%**. La tendencia es monótona decreciente:
a mayor edad, menor frecuencia. **Ningún IC cruza el 1** y todos los p ≈ 0, así que **mantengo los
siete niveles** — cada uno diferencia riesgo de forma significativa.

**P3.** ¿Por qué el GLM one-way reproduce exactamente la tasa empírica, y qué aporta el GLM que una
tabla empírica no puede dar?
**Tu respuesta:** Porque las ecuaciones de score del Poisson con liga log y offset obligan a que, por
nivel, la suma de siniestros predichos iguale la observada: eso hace `exp(η) = Σn/Σe`, exactamente la
tasa empírica ponderada (la diferencia de 4.9×10⁻⁵ es solo ruido numérico). Lo que el GLM aporta **de
más** es combinar muchas variables de forma **multiplicativa** a la vez —algo que una tabla cruzada no
puede— y dar un **intervalo de confianza** para cada rating factor.

---

## Parte 2 · Sesión 2 — Severidad y Selección de Modelos

**Comparación de modelos de frecuencia:**

| modelo | AIC | BIC | pseudoR2_McF |
| --- | --- | --- | --- |
| Poisson | 125,081.7 | 125,261.7 | 0.0198 |
| Binomial Negativa | 124,925.7 | 125,105.8 | 0.021 |

**Rating factors de severidad (Gamma) para `edad_conductor_cat`:**

| nivel | RF_sev | severidad_emp |
| --- | --- | --- |
| (17, 30] (ref) | 1 | 1,478 |
| (30, 35] | 0.9212 | 1,362 |
| (35, 45] | 0.8334 | 1,232 |
| (45, 50] | 0.9047 | 1,337 |
| (50, 55] | 0.7743 | 1,144 |
| (55, 60] | 0.7505 | 1,109 |
| (60, 95] | 0.8802 | 1,301 |

**P4.** ¿Por qué se usa **Gamma** para severidad y no una regresión lineal sobre log(Y)? (menciona la
propiedad del CV y por qué Lognormal no es GLM).
**Tu respuesta:** Porque la Gamma tiene **CV constante** (la variabilidad relativa del monto es
parecida en todos los niveles), lo que ajusta bien a la severidad de seguros. Y la **Lognormal no es
un GLM**: no pertenece a la familia exponencial natural (su estadístico suficiente es log y, no y).
Además, una regresión sobre log(Y) modela E[log Y], no E[Y], y volver a la escala original exige un
factor de corrección exp(σ̂²/2). La Gamma con liga log modela E[Y] **directamente**, sin corrección.

**P5.** Según la tabla de comparación, ¿qué modelo elegirías? Justifica con AIC/BIC. ¿Por qué el pseudo R²
es tan bajo y eso NO significa que el modelo sea malo?
**Tu respuesta:** Elegiría **Binomial Negativa**: tiene menor AIC (124,926 vs 125,082) y menor BIC
(125,106 vs 125,262), lo que refleja la sobredispersión leve que detectamos. El pseudo R² es bajo
(~0.02) porque la ocurrencia de un siniestro tiene una **enorme componente aleatoria irreducible** que
ningún modelo explica — no es comparable con un R² de OLS. Lo que importa es la comparación **relativa**
entre modelos y la **discriminación** (Gini), no un número alto.

**P6.** Compara tus rating factors de frecuencia (Parte 1) con los de severidad para `edad_conductor_cat`. ¿Apuntan en
la misma dirección? ¿Qué implica eso para separar Frecuencia × Severidad?
**Tu respuesta:** Apuntan en la misma dirección pero con **fuerza muy distinta**. En frecuencia el
efecto de la edad es fuerte (de RF 1.0 a 0.47, −53%); en severidad es mucho más plano (de 1.0 a ~0.75–0.88).
Es decir, la edad predice bien **cuántos** siniestros, pero apenas **de qué tamaño**. Justo por eso se
modela Frecuencia × Severidad **por separado**: cada componente tiene su propia estructura de riesgo y
mezclarlos escondería que la edad casi no mueve la severidad.

---

## Parte 3 · Sesión 3 — Validación y Tarifa

**Validación out-of-sample del modelo de frecuencia:**

| metrica | valor | ideal |
| --- | --- | --- |
| Gini (test) | 0.2315 | > 0.30 aceptable |
| Ratio pred/obs (test) | 1.0249 | ≈ 1.00 |

**Prima pura por nivel de `edad_conductor_cat`** (Frecuencia × Severidad, con su factor de tarifa):

| nivel | prima_pura_modelo | factor_tarifa |
| --- | --- | --- |
| (17, 30] (ref) | 314.77 | 1.7277 |
| (30, 35] | 212.33 | 1.1654 |
| (35, 45] | 172.49 | 0.9468 |
| (45, 50] | 179.28 | 0.984 |
| (50, 55] | 143.1 | 0.7854 |
| (55, 60] | 127.07 | 0.6975 |
| (60, 95] | 129.33 | 0.7099 |

**P7.** Interpreta las métricas de validación: ¿el modelo está bien calibrado (ratio pred/obs)? ¿discrimina
bien el riesgo (Gini)? ¿Qué mide cada una?
**Tu respuesta:** El ratio pred/obs en test es 1.025 (≈ 1), así que el modelo está **bien calibrado**:
en promedio predice casi el total de siniestros observados. El **Gini** es 0.23, que mide
**discriminación** (qué tan bien ordena de menor a mayor riesgo); está por debajo de 0.30, así que el
modelo discrimina de forma **modesta**. Son cosas distintas: se puede estar bien calibrado (acierta el
total) y discriminar poco (no separa tan bien buenos de malos riesgos).

**P8.** Lee la tabla de tarifa: ¿qué nivel de tu variable paga la prima pura más alta y cuál la más baja?
Traduce el factor de tarifa a un recargo/descuento sobre la prima promedio.
**Tu respuesta:** La prima pura más alta es la de (17,30] con $314.77 y factor de tarifa 1.728 → un
**recargo del 72.8%** sobre la prima promedio. La más baja es (55,60] con $127.07 y factor 0.698 → un
**descuento del 30.2%**. El patrón confirma lo esperado: los conductores jóvenes concentran la prima
pura más cara (más frecuencia y algo más de severidad), y el riesgo baja con la edad hasta estabilizarse
alrededor de los 55–60 años.

**P9. (Conclusión de nota técnica).** En 3–4 líneas, redacta cómo `edad_conductor_cat` afecta la tarifa, integrando
frecuencia, severidad y prima pura, en estilo defendible ante la CNSF.
**Tu respuesta:** La edad del conductor es un factor de tarificación de primer orden. El efecto se
concentra en la **frecuencia**: los conductores de 17–30 años presentan una frecuencia esperada 2.1
veces la de los mayores de 60 (RF 0.467; IC 95% [0.446, 0.488] para el grupo 60+), mientras que su
efecto sobre la **severidad** es moderado. Combinando ambos componentes, la **prima pura** del grupo
17–30 es 1.73 veces la prima promedio, frente a un descuento cercano al 30% en los mayores de 55. Se
recomienda conservar la edad segmentada en las siete bandas, por su fuerte poder de diferenciación y su
consistencia actuarial.

---
*Evaluación generada automáticamente · Diplomado ML en Seguros · FC UNAM · Módulo 4 · Tema 2*
