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

## Validador de Estrategias v0.2 — Semana 2 completada

### Qué hace esta semana
Backtesting con vectorbt sobre precios reales de DAL, UAL y AAL — las 3 aerolíneas
del Comparador del Mes 1. Estrategia basada en cruces de medias móviles (20 y 50 días).

### Por qué cotizadas y no PYMEs
vectorbt necesita series de precios densas (datos diarios). Las PYMEs solo tienen datos
anuales — insuficientes para simular operaciones de compra y venta. Las aerolíneas son
el proxy natural: mismo sector, datos de alta frecuencia.

### Estrategia — cruce de medias móviles
- **Compra** cuando la MA 20 días cruza hacia arriba la MA 50 días (golden cross)
- **Venta** cuando la MA 20 días cruza hacia abajo la MA 50 días (death cross)
- Comisión del 0.1% por operación + deslizamiento del 0.1%

### Resultados del backtest (mayo 2024 → mayo 2026)
| Empresa | Total Return | Sharpe Ratio | Max Drawdown | Win Rate |
|---|---|---|---|---|
| United | 151.4% | 1.93 | 23.3% | 100% |
| American | 48.1% | 0.94 | 27.9% | 50% |
| Delta | 14.2% | 0.45 | 31.5% | 50% |
| **Portfolio** | **71.2%** | **1.11** | **27.6%** | **67%** |

### Estrategia vs Buy & Hold
| | Estrategia MA | Buy & Hold pasivo |
|---|---|---|
| Return total | 71.2% | 37.0% |
| Veredicto | ✅ La estrategia bate al mercado casi el doble |

### Archivos
- **validador_estrategias_v02.ipynb** — notebook completo
- **senales_trading.png** — señales de compra y venta sobre Delta Airlines
- **equity_curve.png** — evolución del capital vs buy & hold

### Conclusión
United Airlines responde muy bien a la estrategia de media móvil — todas las operaciones
fueron ganadoras. Delta responde mal — el Sharpe de 0.45 no justifica la estrategia activa
frente al buy & hold. La Semana 3 optimizará las ventanas de media móvil para mejorar
los resultados en Delta y American.
