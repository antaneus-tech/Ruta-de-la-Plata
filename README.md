# Ruta de la Plata: ¿puede amortizarse un tren mixto Gijón–Sevilla?

Análisis coste-beneficio del tramo cerrado Astorga–Plasencia (347 km) de la Ruta de la Plata, con efecto red. Incluye un dashboard visual y un modelo en Excel con supuestos editables.

Realizado por: **@bcnopenmind**

## Contenido

| Archivo | Descripción |
|---|---|
| `ruta_plata_dashboard.html` | Dashboard autoexplicativo con 11 gráficos. Cada gráfico lleva incrustados el título, las fuentes y la autoría, para poder usarlos por separado. |
| `ruta_plata_modelo.xlsx` | Modelo de cálculo con supuestos editables, escenarios y sensibilidades. |
| `README.md` | Este documento. |

Los tres archivos deben estar en la misma carpeta: el dashboard enlaza al Excel con una ruta relativa.

## Cómo publicarlo en GitHub Pages

1. Sube los archivos a la raíz del repositorio.
2. En *Settings → Pages*, elige la rama y la carpeta raíz.
3. Si quieres que el dashboard sea la página de inicio, renombra `ruta_plata_dashboard.html` a `index.html` y cambia los dos enlaces que apuntan a él, o deja el nombre actual y accede por su URL.

El enlace de descarga del Excel solo funciona si el HTML se sirve desde Pages. Si lo abres desde la vista de código de GitHub, no se enlazará bien.

## Resultados principales

Estimaciones propias, con el método de la Comisión Europea. Dependen de los supuestos listados abajo.

| Concepto | Resultado |
|---|---|
| Coste de Astorga–Plasencia | ≈3.800 M€ (rango 3.300–5.900), unos 11 M€/km |
| Relación beneficio/coste, caso medio de línea | ≈0,09 |
| Relación beneficio/coste, efecto red plausible-alto | 0,27–0,35 |
| Relación beneficio/coste, techo con valores +50 % | 0,76–0,99 |
| Beneficio anual necesario para B/C = 1 | 230–301 M€/año |
| Beneficio anual del caso medio | ≈20 M€/año, frente a ≈21 M€/año de mantenimiento |
| Canon del gestor | 5–25 M€/año |
| Mercancías de la línea | 1,2–4,0 Mt/año, entre el 5,5 % y el 17,8 % del ferrocarril nacional |

Lectura: es un proyecto con sentido estratégico, pero no rentable en términos económicos ni financieros, y su sostenibilidad depende de cuánto valoren la cohesión territorial, la resiliencia y la logística. Mientras no haya un estudio oficial de viabilidad, conviene actuar por fases.

## Método

- **Costes:** se parte de costes finales oficiales (Plasencia–Mérida, 11,3 M€/km; Madrid–Barcelona, 14,4 M€/km), con factores para vía única y para tramos de sierra.
- **Contraste con las cifras atribuidas:** los totales de promotores, comisionado y ministro se comparan con el método de previsión por clase de referencia (uplift ferroviario del 40 % y 68 %).
- **Demanda:** son escenarios de oferta de trenes (pares de trenes al día, plazas, ocupación), no una previsión basada en modelo de gravedad.
- **Beneficios:** ahorro de tiempo y externalidades evitadas por viaje; ahorro de recursos y externalidades por t·km de mercancía desviada de la carretera.
- **Evaluación:** obra de 6 años, explotación de 30 años, tasas sociales del 3 % y 5 %, según la guía de análisis coste-beneficio de la Comisión Europea de 2014.
- **Capacidad:** método UIC 406 con parámetros asumidos.

## Modelo en Excel

Edita solo las celdas con texto azul de la hoja `Supuestos`. Las de fondo amarillo son los supuestos clave. Todo lo demás se recalcula.

| Hoja | Contenido |
|---|---|
| `Leeme` | Instrucciones, colores, límites y diferencias con el dashboard. |
| `Supuestos` | Todas las entradas, con su tipo de dato y su fuente. |
| `Costes` | Capex en tres casos y comparación con cifras oficiales y atribuidas. |
| `Demanda` | Siete escenarios, uso de capacidad y peso frente al total nacional y Algeciras. |
| `Beneficios` | Valor por viaje y por t·km, y beneficio anual por escenario. |
| `ACB` | B/C, VAN económico, beneficio necesario, análisis financiero y brecha por habitante. |
| `Sensibilidad` | Cruce de demanda y coste, y factor de demanda necesario para B/C = 1. |
| `Fuentes` | Fuentes con enlaces. |

El selector de caso de coste (1 bajo, 2 central, 3 alto) de `Supuestos` cambia todo el análisis.

Diferencias con el dashboard: el modelo calcula el capex central en 3.790 M€ y el mantenimiento en 20,8 M€/año. El dashboard usó 3.800 y 21. Los resultados coinciden salvo en el tercer decimal.

## Tipos de dato

- **Oficial:** procede de una fuente oficial.
- **Oficial\*:** leído a través de prensa que cita la fuente oficial. Conviene contrastarlo con el documento original.
- **Atribuida:** cifra de prensa no oficial (totales de promotores, comisionado y ministro).
- **Propia:** supuesto del autor.

## Limitaciones

- No existe estudio oficial de demanda ni de coste del corredor. El estudio de viabilidad Plasencia–León está licitado y con retraso.
- La demanda sale de la oferta de trenes que se supone. No hay modelo origen-destino calibrado con datos de movilidad.
- Los viajeros pasantes, el recorrido medio de 700 km de las mercancías de red y el reparto entre modos son supuestos propios.
- Mantenimiento, canon, valor del tiempo y externalidades son órdenes de magnitud sin verificar cifra a cifra.
- Las anualizaciones del ferrocarril nacional (×4 sobre el segundo trimestre de 2026) y de Algeciras (×1,5 sobre ocho meses) son aproximaciones propias. Algeciras incluye mucho transbordo marítimo.
- No se valoran las inversiones complementarias (Sevilla–Algeciras y Málaga, enlace con Galicia, Mérida–Sevilla) ni las emisiones de construcción.

## Fuentes principales

- Tribunal de Cuentas Europeo, Informe Especial 19/2018 sobre la alta velocidad ferroviaria.
- Tribunal de Cuentas de España, fiscalización de Madrid–Barcelona (leído a través de prensa).
- Presidencia del Gobierno y Ministerio de Transportes, notas sobre Plasencia–Badajoz (2022, 2024 y 2025).
- Departamento de Transporte británico, Flyvbjerg y COWI (2004), previsión por clase de referencia.
- Comisión Europea, *Guide to Cost-Benefit Analysis of Investment Projects* (2014) y *Handbook on the External Costs of Transport* (2019).
- Observatorio del Ferrocarril en España, Anuario 2025; INE y OTLE; Puertos del Estado.
- Cifras atribuidas: Diario de León y El Salto.

Los enlaces completos están en la hoja `Fuentes` del Excel y en el desplegable de fuentes del dashboard.

## Cómo citar

> @bcnopenmind. *Ruta de la Plata: ¿puede amortizarse un tren mixto Gijón–Sevilla?* Dashboard y modelo de análisis coste-beneficio, 2026.

## Licencia

Por definir por el autor.
