# Dashboard para el análisis y planeamiento del presupuesto público del Perú 2025–2026

Proyecto del curso **Costos y Presupuestos** (Universidad Nacional de Juliaca, 2026-2).

Respuesta al enunciado *Dashboard para el análisis y planeamiento del presupuesto público*.

**Objetivo:** desarrollar un dashboard que permita analizar el comportamiento del presupuesto público, formular indicadores y establecer metas que contribuyan al Planeamiento Operativo Anual (POA).

## Enlace al dashboard

| Entregable | Enlace |
|---|---|
| Dashboard de Power BI (archivo editable `.pbix`) | [dashboard/presupuesto_publico_poa.pbix](https://github.com/aslenwis/presupuesto-publico-2025-2026/blob/main/dashboard/presupuesto_publico_poa.pbix) |
| Descarga directa | https://github.com/aslenwis/presupuesto-publico-2025-2026/raw/main/dashboard/presupuesto_publico_poa.pbix |
| Manual Técnico | [docs/Manual_Tecnico.docx](docs/Manual_Tecnico.docx) |
| Manual de Usuario | [docs/Manual_de_Usuario.docx](docs/Manual_de_Usuario.docx) |
| Notebook (ETL, EDA, indicadores y metas) | [notebooks/eda_presupuesto_publico_poa.ipynb](notebooks/eda_presupuesto_publico_poa.ipynb) |

## Inicio rápido (solo ver el dashboard)

```bash
git clone https://github.com/aslenwis/presupuesto-publico-2025-2026.git
cd presupuesto-publico-2025-2026
```

1. Abra `dashboard/presupuesto_publico_poa.pbix` con **Power BI Desktop** (gratuito). Los datos ya vienen cargados.
2. Para actualizar los datos desde su copia: **Inicio → Transformar datos → Editar parámetros → RutaGold** = ruta de `data\gold\gasto_publico\` (terminada en `\`) → **Aceptar → Aplicar cambios**.

## Arquitectura

```
CSV del MEF (5.4 M filas) → Bronze (Parquet) → Silver (limpio, formato largo) → Gold (modelo estrella + tablas POA) → Power BI
```

- **Bronze:** ingesta fiel, detección de codificación y delimitador, contrato de 73 columnas, linaje por fila.
- **Silver:** limpieza de textos, tipos, formato largo mensual, reglas de calidad DAMA.
- **Gold:** 2 tablas de hechos + 9 dimensiones, tablas del análisis integral (proyección, clasificación, estacionalidad, atípicos), contraste con la Ley N.º 32513 y tablas del POA.
- **Power BI:** un dashboard de **7 módulos** (13 páginas): 1 Resumen ejecutivo · 2 Diagnóstico presupuestario · 3 Indicadores de gestión · 4.1–4.5 Análisis integral (las cinco líneas obligatorias) · 5 Presupuesto Público 2026 (Ley N.º 32513) · 6.1–6.2 Planeamiento operativo anual · 7 Seguimiento y consulta.

## Ejecutar en Google Colab

Suba el repositorio a Google Drive (`Mi unidad/presupuesto-publico-2025-2026`) con los CSV en `data/bronze/`, abra el notebook con el botón **Abrir en Colab** y ejecute todo. Si la carpeta tiene otro nombre, cambie `RUTA_COLAB`.

## Reproducir el ETL

1. Descargue los CSV 2025 y 2026 (ver [data/bronze/LEEME.md](data/bronze/LEEME.md)) y cópielos en `data/bronze/`.
2. Cree el entorno e instale dependencias:
   ```bash
   python -m venv .venv
   .venv\Scripts\activate
   pip install -r requirements.txt
   ```
3. Abra `notebooks/eda_presupuesto_publico_poa.ipynb` y ejecute **Restart → Run All** (≈ 15–30 min la primera vez).
4. En Power BI, **Inicio → Actualizar**.

## Estructura

```
data/bronze/        CSV del MEF y Parquet Bronze (no se versionan)
data/silver/        Parquet Silver (no se versiona)
data/gold/          13 tablas Parquet de la capa Gold (sí se versionan)
notebooks/          Notebook del proyecto
dashboard/          .pbix (entregable) y pbip/ (mismo tablero en texto)
docs/               Manual Técnico y Manual de Usuario
outputs/            Reportes de calidad, diccionario de datos y tablas POA en CSV
reports/            Gráficos del notebook
```

## Fuente de datos

Ministerio de Economía y Finanzas (MEF). *Presupuesto y Ejecución de Gasto – Devengado Mensual*. Plataforma Nacional de Datos Abiertos: https://datosabiertos.mef.gob.pe/dataset/presupuesto-y-ejecucion-de-gasto-devengado-mensual

