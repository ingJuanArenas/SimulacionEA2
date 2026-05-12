  # Modelo Oculto de Markov
### Mantenimiento Predictivo de Maquinaria Industrial

## 📋 Descripción

Implementación de un **Modelo Oculto de Markov (HMM)** para simular el comportamiento de una máquina industrial y predecir fallas antes de que ocurran. El modelo separa dos capas:

- **Capa oculta:** estado real de la máquina (Normal / Desgaste / Falla)
- **Capa observable:** nivel de vibración medido en Hz

Se realizan múltiples simulaciones para validar la convergencia empírica hacia la distribución estacionaria teórica, y se implementan los algoritmos de Viterbi y Forward desde cero con NumPy.

---

## 🗂️ Estructura del repositorio

```
SimulacionEA2/
├── SimulacionEA2.ipynb    
└── README.md
```

---

## 🧠 Modelo

| Parámetro | Detalle |
|-----------|---------|
| Estados ocultos | Normal, Desgaste, Falla |
| Observaciones | Vibración Baja, Media, Alta |
| Distribución inicial π | [0.80, 0.15, 0.05] |
| Horizonte de simulación | 60 horas |
| Simulaciones Monte Carlo | 1000 iteraciones |

**Distribuciones de vibración por estado:**

| Estado | Distribución | Media | Desv. Estándar |
|--------|-------------|-------|----------------|
| Normal | N(20, 5) | 20 Hz | 5 Hz |
| Desgaste | N(55, 10) | 55 Hz | 10 Hz |
| Falla | N(95, 15) | 95 Hz | 15 Hz |

---

## ⚙️ Algoritmos implementados

| Algoritmo | Descripción |
|-----------|-------------|
| `simulate_sequence` | Genera una trayectoria de 60 pasos según π, A, B |
| `run_monte_carlo` | Corre n simulaciones independientes |
| `viterbi` | Infiere la secuencia de estados más probable (log-prob, evita underflow) |
| `forward` | Calcula P(estado\|t) en cada instante — normalizado |

---

## 📊 Resultados principales

- **Convergencia:** las probabilidades empíricas convergen a la distribución estacionaria teórica antes de las 300 iteraciones (error < 0.01)
- **Validación paso a paso:** P(estado|t) = π · A^t coincide con el promedio empírico de 1 000 simulaciones en todos los pasos t ∈ [0, 60]
- **Precisión Viterbi:** 70–85% usando solo observaciones categóricas
- **Forward:** detecta tendencia de degradación antes de que Viterbi declare Falla

---

## 🚀 Cómo ejecutar

1. Abrir `SimulacionEA2.ipynb` en [Google Colab](https://colab.research.google.com/)
2. `Entorno de ejecución → Ejecutar todo`
3. Los gráficos y el reporte de salud se generan automáticamente

No requiere instalación de librerías adicionales — solo `numpy`, `pandas`, `matplotlib` y `seaborn`, disponibles por defecto en Colab.

---



Uso académico. Institución Universitaria Digital de Antioquia — 2026.
