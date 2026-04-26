# Hey Score 🏦

**Datathon Hey Banco 2026 · DSC x Hey 2026**

Sistema de puntuación de salud financiera (0–100) por usuario, que alimenta a **Havi** — un chatbot proactivo que detecta necesidades implícitas y genera mensajes personalizados antes de que el usuario los pida.

---

## ¿Qué es Hey Score?

Hey Score combina datos bancarios estructurados (transacciones, productos, perfil) con análisis de conversaciones de soporte para construir un perfil multidimensional de cada usuario. El resultado es un score con 5 dimensiones que Havi usa para anticipar, no solo reaccionar.

### Las 5 dimensiones

| Dimensión | Qué mide |
|-----------|----------|
| **Salud crediticia** | Score buró, utilización de crédito, rechazos |
| **Actividad transaccional** | Frecuencia, volumen y consistencia de movimientos |
| **Profundidad de relación** | Número de productos activos, antigüedad, nómina domiciliada |
| **Engagement digital** | Login reciente, canal preferido, uso de Hey Shop |
| **Sentimiento conversacional** | Tono y temas dominantes en interacciones con soporte |

---

## Estructura del repositorio

```
hey-score/
├── hey_score_pipeline.ipynb      # Par A: feature engineering + cálculo del Hey Score
├── hey_score_demo.ipynb          # Par B: clustering K-Means + demo Gradio + Havi
├── data/
│   ├── hey_clientes.csv          # 15,025 usuarios · perfil demográfico y comportamental
│   ├── hey_productos.csv         # 38,909 productos · portafolio por usuario
│   ├── hey_transacciones.csv     # ~802k movimientos · historial completo
│   └── dataset_50k_anonymized.csv # 50k interacciones con Havi · soporte conversacional
├── outputs/                      # Artefactos generados (master_df, modelos, gráficas)
└── README.md
```

---

## Cómo correrlo

### Requisitos

- Google Colab (gratis funciona; T4 GPU recomendada para transacciones)

### Paso 1 — Pipeline (`hey_score_pipeline.ipynb`)

1. Subir los 4 archivos de `data/` a Google Drive en `/MyDrive/hey_datathon/data/`
2. Montar Drive en Colab y correr el notebook de inicio a fin
3. Output: `master_df.parquet` y `score_per_user.csv` en `/MyDrive/hey_datathon/outputs/`

> ⚠️ El dataset de transacciones es pesado (~802k filas). Si hay OOM, el notebook incluye una celda de fallback con `nrows=500_000`.

### Paso 2 — Demo (`hey_score_demo.ipynb`)

1. Asegurarse de que `master_df.parquet` ya está en Drive (output del Paso 1)
2. Correr el notebook. Al final levanta una app Gradio con `share=True`
3. La URL pública del demo aparece en el output de la última celda

### Qué hace el demo

- Recibe un `user_id` (formato `USR-00001`)
- Muestra tarjeta con Hey Score total y segmento del usuario
- Radar chart con las 5 dimensiones
- Mensaje proactivo generado por Havi vía API de Claude
- Botón "¿Qué pasa si activo Hey Pro?" — counterfactual en tiempo real

---

## Datasets

Todos los datos son **100% sintéticos**, generados para el Datathon Hey Banco 2026. No representan usuarios ni transacciones reales.

| Archivo | Filas | Descripción |
|---------|-------|-------------|
| `hey_clientes.csv` | 15,025 | Un registro por usuario |
| `hey_productos.csv` | 38,909 | Un registro por producto contratado |
| `hey_transacciones.csv` | ~802k | Un registro por movimiento |
| `dataset_50k_anonymized.csv` | 49,999 | Conversaciones usuario ↔ Havi |

Ver `DICCIONARIO_DATOS.md` para descripción completa de columnas.

---

## Equipo

**Par A — Pipeline & Score**
Construcción del `master_df`, feature engineering, cálculo del Hey Score.

**Par B — Clustering & Demo**
K-Means, validación cuantitativa, integración con API de Claude, demo Gradio, pitch.

---

*Hey Banco · Datathon 2026 · Datos 100% sintéticos*
