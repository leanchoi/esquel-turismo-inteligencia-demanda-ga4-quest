# Inteligencia de Demanda Turística y Auditoría Digital GA4 — Esquel, Chubut (`UN Tourism QUEST`)

**Repositorio oficial de evidencia empírica, informes técnicos y bases de datos normalizadas** para la Subsecretaría de Turismo de Esquel, el Ente Mixto de Turismo y el proceso de certificación **UN Tourism QUEST (`Q01AM2547AR2026` — Indicador `1.3.1.b` y pilares de Marketing, Gobernanza y Gestión Digital)** · PETS Esquel 2030 (`INT-1958/26` · `Res. 27/26`).

---

## 1. Procedencia de los Datos y Metodología de Extracción

### A. Demanda Física, Oferta y Presupuesto (`2007–2026`, Regímenes `R1–R4`)
- **`R1` (Microdatos de Mostrador / Oficina de Informes):** `18.844` grupos encuestados (`51.613` PAX) across `2017–2019`, `2022` y `2026 YTD`, depurados con separación determinística de `CABA`, `GBA (24 Partidos)` e `Interior Prov. Bs.As.`, y resolución de inversión de códigos `Córdoba/Santa Fe`.
- **`R2` (Anuarios y Series Históricas Oficiales):** `2007–2026` (`839.269` turistas en series mensuales `2016–2025`, ocupación hotelera y evolución de oferta).
- **`R3` (Monitoreo Diario de Prestadores):** Tablero de ocupación y reservas.
- **`R4` (Fuentes Externas y Presupuesto Público):** Ingresos `PNLA` (`133.282` en `2025`), tráfico aéreo `ANAC`, `metrica-db` / tarifas OTA, y ejecución devengada del **Ente Mixto (`ARS 206,01M` en `74` partidas)** incluyendo pauta (`Estudio 1640 ARS 71,78M`, `Plaza Córdoba ARS 22,04M`).

### B. Inteligencia Digital Histórica — Google Analytics 4 (`esquel.tur.ar`, `2023-04-21` a `2026-11-26`)
- **Propiedad auditada:** `Esquel Turismo - GA4` (ID `371239202`, Cuenta `123758941`, Huso `GMT-03:00`, Moneda `USD`, Industria `Travel`).
- **Método de extracción:** Extracción directa autenticada desde los **Reportes Estándar** y el módulo de **Publicidad** de `analytics.google.com` el `26/11/2026`, cubriendo el **100% de la historia con datos no nulos (`44` meses completos, desde `2023-04-21` hasta `2026-11-26`)**. Este procedimiento sorteó la limitación estructural de la propiedad (retención en *Explore* bloqueada en el mínimo de `2` meses) mediante la extracción de tablas cruzadas `Channel x Month` por año calendario (`364` filas).
- **Depuración y auditoría aplicada (preservando siempre columnas crudas + columnas depuradas):**
  1. Identificación de la **inflación del `92,7%` en `Key Events`** desde marzo `2026` causada por la marcación errónea de `user_engagement` como *Key Event* (separando las señales reales: `generate_lead = 14.321`, `file_download = 2.737`, `form_submit = 93`).
  2. Armonización de etiquetas **GeoIP *legacy*** (`2023–2024` sin sufijo `"Province"` vs `2025–2026` con `"Province"`).
  3. Marcado explícito (`audit_flag`) de **bots y *datacenters cloud*** (`>= 33%` del tráfico extranjero: `Wright-Patterson AFB/Ohio`, `Oregon/Virginia AWS`, `China/Gansu`, `Singapore`, `Ireland/Dublin`, `Sweden/Norrbotten`, `Indonesia`).
  4. Marcado de **contaminación LAN municipal** (`192.168.0.x:8088`, `578` sesiones) y separación del tráfico **local / *in-destination* (`Esquel`: `41.503` usuarios = `51,3%` de Chubut)**.
  5. Cruce econométrico (`N = 39` meses `2023-04` a `2026-06`) entre GA4 y arribos físicos reales (`matriz_mensual_turistas_2008_2026.csv`): **`Organic Search` correlaciona con `r = +0,6256 (p = 2,05e-05 ***)` (`r = +0,9176 ***` en `2025-09..2026-06`) y anticipa `+1` mes (`rho = +0,5411 ***`)**, mientras que **`Paid Total` tiene correlación nula (`r = +0,0972`, `p = 0,556`, NS)**.

---

## 2. Estructura del Repositorio

```text
.
├── README.md
├── informes_oficiales_itd/          # Serie Oficial de 6 Informes Técnicos de Demanda (QA = 0 issues)
│   ├── ITD-ESQ-01_PERFIL_CONSOLIDADO_DEMANDA_2022_2026.md
│   ├── ITD-ESQ-02_PERFIL_DEMANDA_INVIERNO_Y_LA_HOYA_2016_2026.md
│   ├── ITD-ESQ-03_PERFIL_DEMANDA_ESTIVAL_RUTERO_Y_PNLA_2016_2026.md
│   ├── ITD-ESQ-04_PERFIL_DEMANDA_OTONO_PRIMAVERA_Y_TULIPANES_2016_2026.md
│   ├── ITD-ESQ-05_MERCADOS_PROXIMIDAD_REGIONAL_VS_EXTRAREGIONALES_2016_2026.md
│   └── ITD-ESQ-06_INTELIGENCIA_DIGITAL_GA4_ESQUEL_TUR_AR_2023_2026.md
├── documentos_base_doc/             # Serie Base Metodológica y Estratégica (DOC 1 a DOC 8)
│   ├── DOC_1_MATRIZ_HISTORICA_SERIES_TEMPORALES_2007_2026.md
│   ├── DOC_2_PERFIL_DEMANDA_ORIGEN_Y_SEGMENTACION.md
│   ├── DOC_3_COMPORTAMIENTO_CONSUMO_CANALES_Y_LOGISTICA.md
│   ├── DOC_4_ESTRUCTURA_OFERTA_ESTACIONALIDAD_Y_SHOCKS.md
│   ├── DOC_5_INSIGHTS_Y_OPORTUNIDADES_PLAN_MARKETING_ESQUEL.md
│   ├── DOC_6_MICRODATOS_PERFIL_DEMANDA_OFICINA_INFORMES.md
│   ├── DOC_7_SISTEMA_MONITOREO_DIARIO_PRESTADORES_ALOJAMIENTO.md
│   └── DOC_8_CRUCE_ESTRATEGICO_ANUARIOS_VS_PERFIL_MOSTRADOR.md
├── datos_demanda_fisica/            # 4 Matrices CSV Oficiales (2007-2026)
│   ├── matriz_encuestas_mostrador_2017_2026.csv
│   ├── matriz_historica_anual_2007_2026.csv
│   ├── matriz_mensual_turistas_2008_2026.csv
│   └── matriz_ocupacion_historica.csv
└── datos_ga4_esquel_tur_ar/         # Base Maestra GA4 (esquel.tur.ar, 44 meses)
    ├── GA4_ESQUEL_TUR_AR_BASE_MAESTRA_2023_2026.xlsx   # Libro Excel Maestro (20 hojas)
    ├── ga4_esquel_2023_2026.sqlite                     # Base SQLite (24 tablas)
    └── csv/                                            # 25 CSVs normalizados (UTF-8)
        ├── ga4_01_channels_full.csv
        ├── ga4_02_channels_yearly.csv
        ├── ga4_03_monthly_44m_summary.csv
        ├── ga4_04_monthly_44m_by_channel.csv
        ├── ga4_05_source_medium_top80.csv
        ├── ga4_06_campaigns_all72.csv
        ├── ga4_07_google_ads_roi.csv
        ├── ga4_08_advertising_channels_cost.csv
        ├── ga4_09_countries_full_top50.csv
        ├── ga4_10_countries_yearly_2024_2026.csv
        ├── ga4_11_regions_full_raw_top61.csv
        ├── ga4_12_regions_full_harmonized.csv
        ├── ga4_13_regions_yearly_2024_2026.csv
        ├── ga4_14_cities_full_top80.csv
        ├── ga4_15_demographics_gender.csv
        ├── ga4_16_demographics_age.csv
        ├── ga4_17_demographics_language.csv
        ├── ga4_18_events_and_key_events.csv
        ├── ga4_19_pages_top80.csv
        ├── ga4_20_landing_pages_top50.csv
        ├── ga4_21_tech_devices.csv
        ├── ga4_22_tech_os.csv
        ├── ga4_23_tech_browsers.csv
        ├── ga4_24_explore_2026_sep_nov.csv
        └── ga4_25_cruce_mensual_digital_vs_fisico.csv
```

---

## 3. Hallazgos Clave que Impulsan la Actualización del Plan de Marketing y QUEST

1. **Espejismo de Volumen Pago (`2024 -> 2026`):** Sesiones `+342,9%` (`160.024 -> 708.678`), pero tiempo medio `-85,1%` (`87s -> 13s`); `86,62%` del tráfico `2026` es pauta con correlación nula con arribos físicos (`r = +0,0972`, NS).
2. **Colapso Orgánico Silencioso:** `Organic Search` cayó `-44,02%` en ventana homóloga `Ene–Nov` (`2024 -> 2026`), aun siendo el canal que concentra `40,1%` de los *key events* y predice arribos físicos a `+1` mes (`rho = +0,5411 ***`).
3. **Desperdicio de Pauta Google Ads (`71,87%` del gasto):** `USD 13.322,65` de `USD 18.537,28` absorbidos por `YouTube` (`USD 4.474` -> `188` clics = `USD 23,80/clic`, `USD 1.118,50/sesión comprometida`) y `Display` genérico (`15–19%` eng, `3–4s`), frente a `Display Escapate` (`USD 0,030`, `67,3%` eng) y `Search Esquel` (`60,1%` eng, `46s`).
4. **Brechas Críticas de Gobernanza GA4:** `user_engagement` infla `92,7%` de *Key Events*, retención `Explore` en `2` meses, sin `Google Search Console`, sin `BigQuery` y sin filtro LAN (`192.168.0.x`).
5. **Activos Subexplotados:** `Eclipse Anular 2027` (`78.042` vistas anticipadas sin *landing* de captura de *leads*), ausencia de *landing* evergreen de `Tulipanes` (pico orgánico #1 del año en octubre), brecha UX `mobile` (`89,1%` de usuarios a `27s` vs `desktop` `3m 23s`; `Safari iOS 23,2%` eng) y ascenso de `AI Search` (`ChatGPT` + `Gemini`: `1.527` sesiones, `70%–82%` eng).
