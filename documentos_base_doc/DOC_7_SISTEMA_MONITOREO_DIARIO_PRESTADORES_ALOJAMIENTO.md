# DOCUMENTO 7: EL SISTEMA DE MONITOREO DIARIO DE PRESTADORES DE ALOJAMIENTO
**Destino:** Esquel, Provincia del Chubut, Patagonia Argentina  
**Fuente Directa:** Planillas Operativas de Relevamiento Diario de Alojamientos Turísticos – Secretaría de Turismo de Esquel (Archivos: Septiembre, Octubre y Noviembre 2026)  
**Propósito del Documento:** Explicar y documentar la arquitectura de datos, el modelo de muestreo diario, los criterios de ajuste y las fórmulas matemáticas con las que se construye la estadística oficial de ocupación y capacidad hotelera del destino.

---

## 1. ARQUITECTURA DEL SISTEMA Y METODOLOGÍA DE RECOLECCIÓN

El monitoreo de prestadores de Esquel opera como un censo diario estratificado con control estricto de cobertura:
1. **Universo Relevado:** 100% de los establecimientos habilitados por la Dirección de Habilitaciones Comerciales de la Municipalidad de Esquel.
2. **Periodicidad:** Diaria (los 30 o 31 días del mes cuentan con una hoja individual en la planilla, e.g., `011026` a `311026`).
3. **Mecanismo de Contacto:** Llamadas telefónicas y mensajería directa diaria a los administradores o recepcionistas de cada establecimiento consultando la ocupación de la noche anterior y la disponibilidad del día.
4. **Tratamiento de Datos:**
   - *Pestaña "Datos Limpios":* Base normalizada con Fecha, Categoría, Nombre del Alojamiento, Capacidad UF, Capacidad PAX, UF Disponibles, PAX Disponibles, UF Ocupadas, PAX Ocupadas y Estado del prestador (Abierto, Cerrado por refacción, Fuera de temporada, Alquiler permanente).
   - *Pestaña "Cobertura de Datos":* Control del umbral mínimo muestral por categoría.

---

## 2. EL MODELO DE VARIABLES: CAPACIDAD NOMINAL VS. CAPACIDAD REAL

Uno de los aportes metodológicos más valiosos de estas planillas es la diferenciación rigurosa entre lo legalmente habilitado y lo comercialmente operativo:

### A. Definición de Variables por Establecimiento:
- **UF Habilitada (UF Hab):** Unidades Funcionales nominales autorizadas según la habilitación comercial municipal.
- **UF Trabajando / Reales (UF Reales T):** Unidades Funcionales que el prestador efectivamente pone a la venta para turistas en el día.
- **PAX Habilitada (PAX Hab):** Cantidad de camas habilitadas legalmente.
- **PAX Trabajando / Reales (PAX Reales T):** Cantidad de camas operativas puestas a la venta.
- **UF Ocupada:** Cantidad de unidades comerciales con huéspedes esa noche.
- **PAX Ocupada:** Cantidad de personas alojadas efectivamente en esas unidades.

### B. Desglose Operativo por Categoría (Mes Benchmark - Septiembre 2026):
| Categoría de Alojamiento | UF Habilitadas | UF Reales Trabajando | Camas Habilitadas | Camas Reales Trabajando | % Operatividad de la Oferta |
|:---|:---:|:---:|:---:|:---:|:---:|
| **Hoteles** | 180 | 178 | 463 | 461 | 98,9% |
| **Hosterías** | 94 | 93 | 271 | 237 | 87,5% |
| **Cabañas** | 175 | 159 | 893 | 764 | 85,6% |
| **Complejos de Alquiler Temporario (CAT)** | 163 | 144 | 692 | 596 | 86,1% |
| **Hostels** | 82 | 82 | 118 | 118 | 100,0% |
| **Viviendas Turísticas** | 40 | 38 | 190 | 181 | 95,3% |
| **Departamentos** | 30 | 30 | 153 | 146 | 95,4% |
| **Hospedaje Complementario** | 41 | 30 | 152 | 125 | 82,2% |
| **Bed & Breakfast** | 17 | 17 | 29 | 29 | 100,0% |
| **Alojamiento Familiar** | 13 | 13 | 33 | 33 | 100,0% |
| **Alojamientos de Montaña (La Hoya)** | 21 | 11 | 53 | 28 | 52,8% |
| **Refugios** | 4 | 4 | 16 | 16 | 100,0% |
| **Campings** | 93 | 0 (cerrado invierno)| 465 | 0 | 0,0% |
| **Total Ciudad** | **953** | **798** | **3.528** | **2.734** | **77,5%** |

**Hallazgo Operativo:**  
En un mes de transición como septiembre, de las 3.528 plazas habilitadas en los registros comerciales, **solo 2.734 plazas están realmente disponibles** para recibir turistas (el 22,5% de la oferta se encuentra inactiva por cierre estacional de campings y refugios, o por mantenimiento).

---

## 3. UMBRALES MÍNIMOS DE COBERTURA Y FORMULACIÓN MATEMÁTICA

Para garantizar la representatividad estadística cuando algún prestador no responde a los llamados diarios, el sistema aplica un protocolo de **mínimo muestral requerido** por categoría:
- Cabañas: Mínimo 14 establecimientos con dato diario reportado.
- Complejos CAT: Mínimo 14 establecimientos.
- Hospedaje Complementario: Mínimo 9 establecimientos.
- Vivienda Turística: Mínimo 6 establecimientos.
- Departamentos: Mínimo 5 establecimientos.
- Hosterías: Mínimo 4 establecimientos.
- Hoteles: Mínimo 3 establecimientos.
- Hostels: Mínimo 3 establecimientos.
- Bed & Breakfast: Mínimo 2 establecimientos.
- Alojamientos Familiares: Mínimo 2 establecimientos.
- Refugios y Montaña: Mínimo 1 establecimiento.

### Fórmulas de Extrapolación de Ocupación:
1. **Ocupación Diaria de la Categoría ($O_{cat}$):**
   $$\% O_{cat} = rac{\sum 	ext{UF Ocupadas reportadas}}{\sum 	ext{UF Reales reportadas}}$$
2. **Extrapolación a la Categoría Completa ($UF_{ocup\_total}$):**
   $$UF_{ocup\_total} = \% O_{cat} 	imes 	ext{UF Reales Totales de la Categoría}$$
3. **Ocupación General Diaria de Esquel ($\% O_{general}$):**
   $$\% O_{general} = rac{\sum_{cat=1}^{k} UF_{ocup\_total}}{\sum_{cat=1}^{k} 	ext{UF Reales Totales}}$$
4. **Cierre Mensual Ponderado:**
   $$\% O_{mensual} = rac{\sum_{dia=1}^{N} UF_{ocup\_general\_dia}}{N 	imes 	ext{UF Reales Promedio}}$$

---

## 4. PATRONES DE FLUCTUACIÓN INTRADÍARIA: ENTRE SEMANA VS. FIN DE SEMANA

A partir del análisis de las hojas diarias de septiembre, octubre y noviembre:
- **Días de Semana (Lunes a Jueves):**
  - La ocupación se desploma a niveles de entre el **8% y el 15%** en meses regulares.
  - La demanda está sostenida casi exclusivamente por Hoteles (viajeros corporativos, funcionarios provinciales y comisiones de servicio).
- **Fines de Semana (Viernes a Domingo):**
  - La ocupación salta bruscamente al **35% - 48%** en fines de semana comunes y al **80% - 100%** en fines de semana largos.
  - El salto lo lideran Cabañas, Complejos CAT y Viviendas Turísticas impulsadas por familias y parejas provenientes de Comodoro Rivadavia, Trelew y Puerto Madryn.

**Implicancia Directa para el Plan de Marketing:**  
Existe una asimetría radical de ocupación dentro de la misma semana. Las estrategias comerciales y de precios deben segmentar agresivamente entre tarifas de fin de semana (inelásticas) y tarifas corporativas / escapadas de lunes a jueves (muy elásticas al precio).
