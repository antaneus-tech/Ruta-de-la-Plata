# Ruta de la Plata: ¿puede amortizarse un tren mixto Gijón–Sevilla?

Análisis coste-beneficio del tramo cerrado Astorga–Plasencia (347 km) de la Ruta de la Plata, con efecto red. Este repositorio contiene un dashboard visual, un modelo en Excel con supuestos editables y la explicación completa del proceso de cálculo.

Realizado por: **@bcnopenmind**

## 1. Contenido del repositorio

| Archivo | Descripción |
|---|---|
| `index.html` (o `ruta_plata_dashboard.html`) | Dashboard autoexplicativo con 11 gráficos. Cada gráfico lleva incrustados el título, las fuentes y la autoría, para poder usarlos por separado. |
| `ruta_plata_modelo.xlsx` | Modelo de cálculo con supuestos editables, escenarios y sensibilidades. |
| `README.md` | Este documento: proceso del modelo, resultados, limitaciones e instrucciones de publicación. |

Los tres archivos deben estar en la misma carpeta, porque el dashboard enlaza al Excel con una ruta relativa.

## 2. Pregunta que responde el modelo

¿Cuánto costaría reabrir la Ruta de la Plata como línea mixta de viajeros y mercancías, y qué beneficios económicos generaría? Es decir, ¿se amortiza?

El modelo responde con el método de la Comisión Europea para evaluar proyectos de inversión (*Guide to Cost-Benefit Analysis*, 2014): mide cuánto cuesta la obra, cuánto vale cada año lo que la línea aporta a la sociedad, y compara ambas cosas con la relación beneficio/coste (B/C). Un B/C de 1 es el umbral de rentabilidad.

La propuesta evaluada es una vía única electrificada, preparada para 250 km/h y para doble vía, que reconstruye solo Astorga–Plasencia y reutiliza lo existente en el resto (Gijón–León por Pajares, Plasencia–Mérida ya construido).

## 3. El proceso del modelo, paso a paso

El Excel sigue siempre el mismo orden. Cada hoja alimenta a la siguiente:

```
Supuestos → Costes ─────────────┐
    │                           ├→ ACB → Sensibilidad
    └→ Demanda → Beneficios ────┘
```

### Paso 1. Supuestos (hoja `Supuestos`)

Es la única hoja de entradas. Todos los parámetros están en celdas azules, con su unidad, su tipo de dato y su fuente. Las celdas con fondo amarillo son los supuestos clave. Las demás hojas calculan con fórmulas que apuntan aquí; la única excepción son los factores de demanda de la hoja `Sensibilidad`, que también son editables.

### Paso 2. Costes de construcción (hoja `Costes`)

Se parte de costes finales oficiales de líneas españolas, no de presupuestos iniciales, y se ajustan a una vía única con tramos de sierra:

```
Capex = ref × f_vía_única × (km_llano + mult_sierra × km_sierra) + electrificación × km_total
```

- `ref`: 11,3 M€/km (Plasencia–Mérida: 1.700 M€ en 150 km, Ministerio 2024). En el caso alto, 14,4 M€/km (Madrid–Barcelona, Tribunal de Cuentas).
- `f_vía_única`: 0,65 / 0,70 / 0,80 en los casos bajo, central y alto. Supone que una vía única preparada para doble vía cuesta entre el 65 % y el 80 % de la doble.
- `mult_sierra`: 1,5 / 1,75 / 2,0 en los 147 km de Salamanca–Plasencia, por variantes y túneles.
- Electrificación: 0,5 M€/km (90 M€ para 195 km en Plasencia–Badajoz).

Ejemplo del caso central: 11,3 × 0,70 = 7,91 M€/km en llano × 200 km = 1.582 M€. En sierra, 7,91 × 1,75 = 13,84 M€/km × 147 km = 2.035 M€. Electrificación: 0,5 × 347 = 173,5 M€. Total: **≈3.790 M€** (3.262 en el caso bajo y 5.864 en el alto).

La misma hoja compara el resultado con las cifras que circulan:

| Concepto | M€ totales | M€/km | Tipo |
|---|---|---|---|
| Promotores | 1.900 | 5,5 | Atribuida |
| Promotores + uplift P50 (+40 %) | 2.660 | 7,7 | Propia |
| Promotores + uplift P90 (+68 %) | 3.192 | 9,2 | Propia |
| Propuesta, caso central | 3.790 | 10,9 | Propia |
| Plasencia–Mérida × 347 km | 3.921 | 11,3 | Oficial |
| Comisionado | 4.000 | 11,5 | Atribuida |
| Madrid–Barcelona × 347 km | 4.997 | 14,4 | Oficial* |
| Ministro | 6.000 | 17,3 | Atribuida |
| Media de líneas AV (Tribunal de Cuentas Europeo) × 347 km | 8.675 | 25 | Oficial |

El uplift del 40 % y del 68 % procede del método de previsión por clase de referencia del Departamento de Transporte británico (Flyvbjerg y COWI, 2004). Sirve para comprobar si los 1.900 M€ de los promotores son creíbles: incluso con ese ajuste quedan por debajo del caso bajo de la propuesta.

### Paso 3. Demanda (hoja `Demanda`)

No hay estudio oficial de demanda, así que el modelo trabaja con escenarios de oferta de trenes. Hay siete: cuatro de línea y tres con efecto red.

**Escenarios de línea (1 Bajo, 2 Medio, 3 Alto, 4 Muy optimista):**

```
Viajes al año (M) = pares de trenes de viajeros × 2 sentidos × 300 plazas × 45 % de ocupación × 365 / 1.000.000
Mercancías (Mt)   = pares de trenes de mercancías × 2 × 365 × 600 t netas × 0,7 factor de retorno / 1.000.000
Mercancías (M t·km) = Mt × 350 km
```

Ejemplo del escenario Medio: 6 pares de viajeros dan 0,591 M de viajes al año. 4 pares de mercancías dan 1,226 Mt al año, es decir, 429 M t·km. Con 12 trenes de viajeros y 8 de mercancías al día, el total es de 20 trenes diarios.

**Uso de la capacidad:** trenes totales al día dividido por la capacidad de cada alternativa: 30 trenes (renovación básica), 50 (propuesta mixta en vía única) y 150 (AVE de doble vía), según el método UIC 406 con parámetros asumidos. El escenario Medio ocupa el 67 %, el 40 % y el 13 %, respectivamente.

**Escenarios de red (5 Red plausible-alta, 6 Red techo, 7 Techo con valores +50 %):** añaden los flujos que llegan de fuera del corredor: Galicia, Asturias y Cantabria con Andalucía, y los puertos andaluces.

- Los viajeros locales son los del escenario Alto (0,986 M).
- Se suman viajeros pasantes: 0,5 M (plausible) o 1,0 M (techo).
- Las mercancías son de 2 Mt (plausible) o 4 Mt (techo) con un recorrido medio de 700 km, y los trenes de mercancías se derivan de ese tonelaje.

**Peso frente al total:** la hoja divide las mercancías de cada escenario entre el ferrocarril nacional (22,5 Mt/año, anualizado del segundo trimestre de 2026 del INE), entre las t·km ferroviarias nacionales (8.900 M t·km en 2024), entre las de carretera (271.600 M t·km) y frente al Puerto de Algeciras (≈101 Mt/año, anualizado de ocho meses). El techo representa el 17,8 % de las toneladas y el 31,5 % de las t·km del ferrocarril nacional.

### Paso 4. Beneficios económicos (hoja `Beneficios`)

Cada viaje y cada t·km se convierten en euros:

```
Valor por viaje = tiempo de los desviados + tiempo de los generados + externalidades evitadas
  tiempo desviados  = (40 % coche + 20 % autobús + 15 % otro tren) × 0,4 h × 12 €/h        = 3,60 €
  tiempo generados  = 25 % × 0,4 h × 12 €/h / 2   (regla de la mitad)                      = 0,60 €
  externalidades    = (40 % × 0,06 + 20 % × 0,015 − 25 % × 0,01) €/pkm × 150 km           = 3,68 €
  Total                                                                                     = 7,88 €

Valor por t·km = 0,05 €/t·km × 70 % desviado de la carretera = 0,035 €
```

El beneficio anual de cada escenario es:

```
B = (viajes locales × 7,88 + pasantes × 46 € + M t·km × 0,035) × factor de valores
```

El factor de valores es 1 salvo en «Muy optimista» y «Techo con valores +50 %», donde vale 1,5. El viaje pasante vale 46 € (3 h de ahorro a 12 €/h más externalidades) porque evita el rodeo por Madrid.

Ejemplo del escenario Medio: 0,591 × 7,88 = 4,7 M€ de viajeros más 429 × 0,035 = 15,0 M€ de mercancías, es decir, **≈19,7 M€ al año**.

### Paso 5. Análisis coste-beneficio (hoja `ACB`)

Se descuentan todos los flujos al inicio de las obras con tres elementos: 6 años de obra con el capex repartido por igual, 30 años de explotación y dos tasas sociales (3 % y 5 %, según la guía europea). No se incluye valor residual.

```
Factor de anualidad       A  = (1 − (1+r)^−30) / r
Factor de descuento       DF = (1+r)^−6
VA del capex              = capex × (1 − (1+r)^−6) / (r × 6)
VA del mantenimiento      = mantenimiento × A × DF          (0,06 M€/km·año × 347 km = 20,8 M€/año)
VA de los beneficios      = B × A × DF
B/C                       = VA beneficios / (VA capex + VA mantenimiento)
VAN económico             = VA beneficios − (VA capex + VA mantenimiento)
Beneficio necesario (B/C = 1) = (VA capex + VA mantenimiento) / (A × DF)
```

Ejemplo al 3 %, escenario Medio: A = 19,60 y DF = 0,8375, de modo que A × DF = 16,42. El VA del capex es 3.790 × 0,9028 = 3.422 M€ y el del mantenimiento 20,8 × 16,42 = 342 M€. Los costes suman 3.764 M€. Los beneficios valen 19,7 × 16,42 = 323 M€. Resultado: **B/C = 323 / 3.764 = 0,086**, con un VAN económico de −3.441 M€.

La hoja produce cinco bloques:

1. **Beneficio anual necesario para B/C = 1**, por alternativa de coste.
2. **B/C y VAN de la propuesta** en los siete escenarios.
3. **Las tres alternativas con los beneficios del escenario Medio.** Los beneficios se escalan: ×0,5 para la renovación básica (menos velocidad y mercancías limitadas), ×1,0 para la propuesta mixta y ×1,1 para el AVE de doble vía.
4. **Análisis financiero del gestor de la infraestructura:** ingresos por canon (2, 5 o 10 € por tren·km), mantenimiento, resultado de explotación y brecha de financiación, definida como (VA capex − VA neto de explotación) / VA capex.
5. **Brecha social:** el beneficio que haría falta menos el estimado, repartido entre ≈1,33 M de habitantes de León, Zamora, Salamanca y Cáceres.

### Paso 6. Sensibilidad (hoja `Sensibilidad`)

Cruza un factor de demanda (de 0,5× a 20×) con cinco alternativas de coste y devuelve el B/C de cada combinación, con cada una de las dos tasas. Debajo de cada tabla calcula el factor de demanda necesario para llegar a B/C = 1. Los factores de las filas son editables.

## 4. Resultados

**B/C de la propuesta por escenario** (capex central ≈3.790 M€):

| Escenario | B anual (M€) | B/C al 3 % | B/C al 5 % |
|---|---|---|---|
| 1 Bajo | 9,8 | 0,043 | 0,033 |
| 2 Medio | 19,7 | 0,086 | 0,066 |
| 3 Alto | 30,3 | 0,132 | 0,101 |
| 4 Muy optimista | 90,9 | 0,396 | 0,303 |
| 5 Red plausible-alta | 79,8 | 0,348 | 0,266 |
| 6 Red, techo | 151,8 | 0,662 | 0,505 |
| 7 Red, techo con valores +50 % | 227,6 | 0,993 | 0,758 |

**Beneficio anual necesario para B/C = 1** (M€ al año, tasa del 3 % y del 5 %): promotores 125 y 161; propuesta 229 y 300; comisionado 241 y 316; ministro 351 y 463. Frente a ellos, el escenario Medio genera unos 20 M€ al año.

**Alternativas con los beneficios del escenario Medio:** renovación básica 0,079 y 0,061; propuesta mixta 0,086 y 0,066; AVE de doble vía 0,062 y 0,047. Ninguna alcanza 1.

**Financiero:** con 20 trenes al día, la línea recorre 2,5 millones de tren·km al año. El canon aporta entre 5,1 y 25,3 M€ al año frente a 20,8 M€ de mantenimiento, con un resultado de explotación de entre −15,8 y +4,5 M€ al año. La brecha de financiación está entre el 98 % y el 108 % del capex.

**Social:** la brecha entre el beneficio necesario y el del escenario Medio es de unos 210 M€ al año con el 3 % y 281 con el 5 %, es decir, 158 y 211 € por habitante y año. Hace falta entre 11,7 y 15,3 veces el beneficio del escenario Medio.

**Sensibilidad (tasa del 3 %):** el factor de demanda necesario para B/C = 1 es 6,4× con el coste de los promotores, 10,2× con el caso bajo, 11,7× con el central, 17,4× con el alto y 17,8× con el del ministro.

**Lectura:** es un proyecto con sentido estratégico, pero no rentable en términos económicos ni financieros, y su sostenibilidad depende de cuánto valoren la cohesión territorial, la resiliencia y la logística. Solo roza B/C = 1 en un techo que exige mover por esta vía casi un tercio de las t·km ferroviarias del país. Mientras no haya un estudio oficial de viabilidad, conviene actuar por fases.

## 5. Cómo modificar el modelo

Edita solo las celdas azules de la hoja `Supuestos`. Todo lo demás se recalcula.

| Quieres comprobar... | Cambia en `Supuestos` | Mira en |
|---|---|---|
| El efecto de un coste distinto | `Caso de coste` (1, 2 o 3) o los costes de referencia | `Costes`, `ACB` |
| Más o menos tráfico | Pares de trenes de viajeros y de mercancías | `Demanda`, `ACB` |
| Otra valoración del tiempo | Valor del tiempo y ahorro de tiempo | `Beneficios`, `ACB` |
| Más carga de largo recorrido | Mercancías de red y recorrido medio | `Demanda`, `ACB` |
| Otra tasa o plazo | Tasas sociales, horizonte y años de obra | `ACB` |
| Un mantenimiento o canon distinto | Mantenimiento por km y canon | `ACB` (análisis financiero) |
| Cuánta demanda haría falta | Factores de demanda de la hoja `Sensibilidad` | `Sensibilidad` |

Las celdas azules con fondo amarillo son los supuestos más influyentes. El archivo contiene 487 fórmulas y no devuelve errores al recalcular.

Diferencias con el dashboard: el modelo calcula el capex central en 3.790 M€ y el mantenimiento en 20,8 M€ al año, mientras que el dashboard usó 3.800 y 21. Los resultados coinciden salvo en el tercer decimal.

## 6. Qué muestra cada gráfico del dashboard

| Gráfico | Hoja de origen |
|---|---|
| Trazado por tramos | `Supuestos` (longitudes) |
| Coste por kilómetro frente a referencias oficiales | `Costes` |
| Evolución de la cifra oficial de Plasencia–Badajoz | Fuentes oficiales (`Fuentes`) |
| Demanda de viajeros | `Demanda` |
| Mercancías de la línea | `Demanda` |
| Volumen de mercancías frente al total nacional y Algeciras | `Demanda` |
| Toneladas-kilómetro frente al total | `Demanda` |
| Uso de la capacidad | `Demanda` |
| Flujos anuales y beneficio necesario | `ACB` |
| B/C de la línea | `ACB` |
| B/C con efecto red | `ACB` |

Cada gráfico indica con color qué dato es oficial, cuál es oficial leído en prensa (\*), cuál es una cifra atribuida y cuál es estimación propia.

## 7. Tipos de dato

- **Oficial:** procede de una fuente oficial.
- **Oficial\*:** leído a través de prensa que cita la fuente oficial. Conviene contrastarlo con el documento original.
- **Atribuida:** cifra de prensa no oficial (totales de promotores, comisionado y ministro).
- **Propia:** supuesto del autor.

## 8. Limitaciones

- No existe estudio oficial de demanda ni de coste del corredor. El estudio de viabilidad Plasencia–León está licitado y con retraso.
- La demanda sale de la oferta de trenes que se supone, no de un modelo de gravedad ni de un modelo origen-destino calibrado con datos de movilidad. Es la principal debilidad del modelo.
- Los viajeros pasantes, el recorrido medio de 700 km de las mercancías de red y el reparto entre modos son supuestos propios.
- Mantenimiento, canon, valor del tiempo y externalidades son órdenes de magnitud sin verificar cifra a cifra.
- Las anualizaciones del ferrocarril nacional (×4 sobre el segundo trimestre de 2026) y de Algeciras (×1,5 sobre ocho meses) son aproximaciones propias. Algeciras incluye mucho transbordo marítimo, de modo que sobreestima la carga que entra por tierra.
- No se valoran las inversiones complementarias (Sevilla–Algeciras y Málaga, enlace con Galicia, Mérida–Sevilla) ni las emisiones de construcción.
- El modelo no incluye efectos económicos regionales ni valor de defensa o resiliencia. La guía europea los admite solo si se miden con rigor y sin doble cómputo.

## 9. Fuentes principales

- Tribunal de Cuentas Europeo, Informe Especial 19/2018 sobre la alta velocidad ferroviaria.
- Tribunal de Cuentas de España, fiscalización de Madrid–Barcelona (leído a través de prensa).
- Presidencia del Gobierno y Ministerio de Transportes, notas sobre Plasencia–Badajoz (2022, 2024 y 2025).
- Departamento de Transporte británico, Flyvbjerg y COWI (2004), previsión por clase de referencia.
- Comisión Europea, *Guide to Cost-Benefit Analysis of Investment Projects* (2014) y *Handbook on the External Costs of Transport* (2019).
- Observatorio del Ferrocarril en España, Anuario 2025; INE y OTLE; Puertos del Estado.
- Cifras atribuidas: Diario de León y El Salto.

Los enlaces completos están en la hoja `Fuentes` del Excel y en el desplegable de fuentes del dashboard.

## 10. Cómo publicarlo en GitHub Pages

1. Crea un repositorio público y sube los tres archivos a la raíz.
2. En *Settings → Pages*, elige *Deploy from a branch*, la rama `main` y la carpeta `/ (root)`, y pulsa *Save*.
3. Sin un archivo `index.html`, GitHub Pages muestra este README en la dirección raíz. Para que el dashboard sea la página de inicio, renombra `ruta_plata_dashboard.html` a `index.html`; los enlaces al Excel siguen funcionando. Si prefieres dejar el nombre actual, el dashboard está en `https://TU-USUARIO.github.io/NOMBRE-REPO/ruta_plata_dashboard.html`.
4. Espera entre uno y diez minutos y recarga con Ctrl+F5.

El enlace de descarga del Excel solo funciona si el HTML se sirve desde Pages y el Excel está en la misma carpeta. Si lo abres desde la vista de código de GitHub, no se enlazará bien.

## 11. Cómo citar

> @bcnopenmind. *Ruta de la Plata: ¿puede amortizarse un tren mixto Gijón–Sevilla?* Dashboard y modelo de análisis coste-beneficio, 2026.
