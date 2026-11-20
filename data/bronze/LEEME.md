# Datos de origen (capa Bronze)

Los CSV no se suben al repositorio porque pesan ~5 GB. Para reproducir el ETL:

1. Entre a la Plataforma Nacional de Datos Abiertos, conjunto **Presupuesto y Ejecución de Gasto – Devengado Mensual** (MEF):
   https://datosabiertos.mef.gob.pe/dataset/presupuesto-y-ejecucion-de-gasto-devengado-mensual
2. Descargue `2025-Gasto-Devengado-Mensual.csv` y `2026-Gasto-Devengado-Mensual.csv`.
3. Cópielos en esta carpeta (`data/bronze/`) sin cambiarles el nombre.

| Archivo | Tamaño aproximado | Filas |
|---|---|---|
| 2025-Gasto-Devengado-Mensual.csv | 2.6 GB | 2 807 176 |
| 2026-Gasto-Devengado-Mensual.csv | 2.4 GB | 2 596 564 |

El notebook crea aquí la subcarpeta `gasto_publico/` con la versión Parquet (Bronze).
