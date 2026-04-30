## Validador de Estrategias v0.1 — Semana 1 completada

### Qué hace este repositorio
Backtesting manual del modelo de scoring del Analizador de PYMEs — simula qué habría
pasado si en 2022 hubieras invertido según los criterios del modelo, y mide si las
empresas con mejor score efectivamente crecieron más en 2023 y 2024.

### Premisa del backtest
**Pregunta:** ¿las empresas con mejor score en 2022 crecieron más en 2023 y 2024?
**Metodología:** scoring por percentiles (60% margen, 40% crecimiento) → clasificación
TOP / MID / LOW → simulación de inversión escalonada → comparación con crecimiento real

### Resultados clave — Semana 1
| Métrica | Valor |
|---|---|
| Correlación score-crecimiento | 0.57 ✓ poder predictivo positivo |
| Tasa de acierto empresas TOP | 67% |
| Retorno total estrategia | ~10.3% nominal (2022-2024) |
| Retorno real (ajustado inflación) | ~0% (inflación acumulada ~10.5%) |

### Inversión simulada por cuartil
| Cuartil | Inversión | Crecimiento medio | Retorno |
|---|---|---|---|
| TOP | 30.000€ | 10.5% | 10.5% |
| MID | 20.000€ | 10.8% | 10.7% |
| LOW | 4.000€ | 8.1% | 8.1% |

### Archivos
- **validador_estrategias_v01.ipynb** — notebook completo del backtest
- **backtest_v01.xlsx** — 3 hojas: Resultados empresa, Métricas por cuartil, Resumen ejecutivo
- **resultados_backtest.png** — scatter score vs crecimiento real + retorno por cuartil

### Conclusión
El modelo tiene poder predictivo positivo (correlación 0.57) con una muestra de 9 empresas.
Las limitaciones son el tamaño del dataset y la varianza estadística alta con pocos datos.
El Mes 5 añadirá Machine Learning para que el modelo aprenda los pesos óptimos automáticamente.

