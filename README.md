# Correlación Vial‑Peaje: Identificando Zonas de Alto Riesgo

[**➔ Ver en Google Colab**](https://colab.research.google.com/github/AndrewP05/Identificaci-n_zonas_alto_riesgo/blob/main/Cruzar.ipynb)

## Descripcion datos
El presente analisis tiene como fuente dos bases de datos tomadas de la pagina [**Datos Abiertos Colombia**](https://https://www.datos.gov.co/) que nos ayudaran a estudiar, formular y presentar conclusiones sobre la correlacion que puede haber entre las vias nacionales y los peajes.


#### DB - SECTORES CRITICOS DE SINIESTRALIDAD VIAL


*   Ultima Actualizacion: 20 de abril de 2024
*   Fuente: [SECTORES CRITICOS DE SINIESTRALIDAD VIAL](https://www.datos.gov.co/Transporte/SECTORES-CRITICOS-DE-SINIESTRALIDAD-VIAL/rs3u-8r4q/about_data)
*   Diccionario de datos: Tenemos **316** filas y **13** Columnas con:

| Nombre de la columna | Descripción | Tipo de dato               |
|----------------------|-------------|----------------------------|
| `ID_MT`              | Identificador vía Ministerio de Transporte             | Texto                                    |
| `ENTIDAD`            | Entidad a cargo de la Vía | Texto        |
| `GiZScore`           | Calificación según análisis espacial     |  Número                 |
| `Fallecidos`         | Cantidad de fallecidos en el sector      | Número                 |
| `GiPValue`           | Probabilidad de ocurrencia en el sector  | Número                 |
| `Tramo`              | Identificación de la vía en una longitud determinada            | Texto                                    |
| `Nombre`             | Nombre de vía concesionada               |   Texto                  |
| `Latitud`            | Coordenada geográfica respecto al norte  |  Número                 |
| `Longitud`           | Coordenada geográfica respecto al este   | Número                 |
| `PR`                 | Punto de referencia en la vía            |  Texto                  |
| `Municipio`          | Municipio ente territorial               |  	Texto                  |
| `Departamento`       | Departamento ente territorial            |  	Texto                  |
| `divipola`           | Código división política                 |  Texto                  |


#### DB - PEAJES


*   Ultima Actualizacion: 7 de marzo de 2025
*   Fuente: [SECTORES CRITICOS DE SINIESTRALIDAD VIAL](https://www.datos.gov.co/Transporte/Peajes/68qj-5xux/about_data)
*   Diccionario de datos: Tenemos **181** filas y **44** Columnas con:

| Nombre de la columna   | Descripción    | Tipo de dato    |
|--------------|--------------|--------------|
| `point `            |  Coordenadas           |  Punto            |
| 	`nombre_peaje`            | 	Nombre del Peaje             | 	Texto             |
|  	`ubicaci_n`           |  Ubicación            | 	Texto             |
| `sector`             |   Sector           |   	Texto           |
| 	`sentido`             |   	Sentido           |   	Texto           |
| 	`poste_de_referencia_pr`             | Poste de Referencia              | 	Número             |
| 	`distancia_pr`             |  Distancia al Poste de Referencia            |  	Número            |
| 	`telefono_gr_a`             |  	Telefono de la Grua            |   	Texto           |
| `telefono_peaje`             | 	Telefono del Peaje             |  	Texto            |
| 	`url_foto`             | 	Link Foto             |  	URL            |
|  `categoria_i` al `categoria_viie`            |Categoria             |  	Número            |
| `administrador`             | Administrador del Peaje.              |    Número          |
| 	`c_digo_peaje`             |  Código del Peaje            |  	Número            |
| `c_digo_tramo`             |  Código Tramo            |  	Texto            |
|  `eje_adicional`            | 	Eje Adicional             |  	Número            |
| `eje_adicional_r`             |  	Eje Adicional R            |	Número              |
|  	`eje_grua`            | Eje Grua             |  Número            |
|  	`latitud`            |   Latitud           |  	Número            |
| 	`longitud`             |  Longitud            |  Número            |
|    `responsable`          |   Responsable           | 	Texto             |
|    `territorial`         |   	Dominio Territorial            | 		Número             |


## Objetivos

### General

1. Analizar la relación entre la ubicación de los peajes y los sectores críticos de siniestralidad vial para identificar patrones, zonas de riesgo y posibles factores asociados a los accidentes de tránsito en las vías analizadas.

### Especificos

1. Identificar la proximidad geográfica entre peajes y sectores críticos de siniestralidad vial.
2. Clasificar los sectores críticos según su distancia a los peajes.
3. Generar insights y hallazgos relevantes para la toma de decisiones.

# Preguntas de negocio

## 1. ¿En qué Peajes se concentran las tarifas más altas y las mas bajas?
<img width="989" height="690" alt="image" src="https://github.com/user-attachments/assets/2b000ed0-bff1-4fbf-9d71-dba8685aa16e" />
<img width="985" height="690" alt="image" src="https://github.com/user-attachments/assets/d3db78a8-38ef-4e0d-9a29-b21038249bd4" />
A partir de las anteriores gráficas, podemos concluir que los peajes con tarifa más altas se ubican entre los 16.800 y los 23.000 pesos, donde encabeza **Pimpal**, **Guacio** y **Aburra**. Los peajes con tarifas más bajas oscilan entre los 2.300 y 5.900 pesos, donde destacan **Baluarte**, **La parada** y **Nuña**.

El contraste entre ambos grupos es significativo, pues las tarifas más altas pueden ser hasta diez veces mayores que las más bajas, lo cual sugiere diferencias sustanciales de costo según la ubicación, operación de cada peaje y un posible indicio de si es o no causal de siniestros viales.

## 2. ¿Influye la distacia del peaje en la concentracion de siniestros viales?
| Rango de Distancia | Fallecidos |
| :--- | :--- |
| <1 km | 0 |
| 1-5 km | 10 |
| 5-10 km | 0 |
| 10-20 km | 58 |
| 20-50 km | 364 |
| 50-100 km | 586 |
| 100-500 km | 586 |
<img width="571" height="643" alt="image" src="https://github.com/user-attachments/assets/90d23054-ccfb-4b5c-8fe8-7fb5d95e2d6b" />
<img width="689" height="690" alt="image" src="https://github.com/user-attachments/assets/7318fd71-e557-4993-b342-56938c90a7b3" />

En el análisis de fallecidos por peaje más cercano, se observó que algunos peajes están más asociados a siniestros graves, ya que presentan un mayor número de fallecidos. Este hallazgo puede reflejar que ciertos peajes están ubicados en áreas más peligrosas o con mayor tránsito, lo que incrementa la probabilidad de accidentes graves. La concentración de fallecidos en ciertos peajes sugiere que es necesario un análisis más detallado de las condiciones de esas zonas, como el tipo de carretera, la visibilidad, la señalización y otros factores de seguridad vial.

## 3. ¿Que peajes tienen mas siniestros asociados?
<img width="562" height="642" alt="image" src="https://github.com/user-attachments/assets/791a3928-3e0a-4d42-b44a-d9e57e7f0636" />

De acuerdo con la gráfica, los peajes con mayor número de siniestros asociados son Carimagua y Casablanca, seguidos por Bicentenario en un segundo lugar notable. El resto de peajes muestran concentraciones de siniestros menores, indicando que los esfuerzos de control y prevención podrían priorizarse en los corredores viales de Carimagua y Casablanca para mitigar y reducir estos incidentes.

## 4. ¿Qué peajes registran un promedio de fallecidos por siniestro más elevado?
<img width="563" height="634" alt="image" src="https://github.com/user-attachments/assets/f0bbf05e-c003-4a26-9321-495fa1d32627" />

En cuanto al promedio de fallecidos por siniestro cerca de cada peaje, los resultados mostraron que algunos peajes tienen un mayor promedio de fallecidos por accidente en comparación con otros. Esto puede ser un indicio de que, en determinadas áreas, los accidentes tienden a ser más graves, lo que podría estar relacionado con factores como la velocidad en esas zonas, el diseño de las carreteras o la falta de medidas de seguridad adecuadas. Estos datos son esenciales para priorizar acciones preventivas que no solo aborden la cantidad de siniestros, sino también la gravedad de los mismos.

# Conclusiones

Los análisis realizados sobre la relación entre los siniestros y los peajes cercanos proporcionan una comprensión valiosa de los puntos críticos en la red vial. Al estudiar la cantidad de fallecidos, la frecuencia de los siniestros y el promedio de fallecidos por accidente en la cercanía de cada peaje, se identificaron áreas con mayor riesgo, tanto en términos de la cantidad de accidentes como en su gravedad. Este tipo de análisis es fundamental para priorizar intervenciones en zonas de alto riesgo y mejorar la seguridad vial.

Entre los hallazgos relevantes se destacan:

* Identificación de Zonas Críticas:
Los peajes que se encuentran próximos a zonas con mayor número de siniestros o fallecidos fueron identificados como áreas críticas. La concentración de siniestros en determinadas ubicaciones resalta la importancia de revisar las condiciones de la infraestructura vial en estos puntos.

* Evaluación del Impacto en la Gravedad de los Accidentes:
El análisis del promedio de fallecidos por siniestro permitió identificar aquellos peajes en los que, aunque la frecuencia de accidentes pudiera ser moderada, la gravedad de los mismos es mayor. Esto sugiere la necesidad de medidas específicas para mitigar la severidad de los accidentes, más allá de simplemente reducir su ocurrencia.

* Priorización de Intervenciones:
Los resultados obtenidos permiten orientar la planificación de políticas de seguridad vial, dirigiendo recursos y esfuerzos a aquellas zonas en las que tanto la cantidad como la gravedad de los siniestros alcanzan niveles críticos. Entre las medidas recomendadas se encuentran la revisión de la señalización, la implementación de controles de velocidad, mejoras en la iluminación y en el estado de la carretera.

* Importante Observación:
A partir de los datos analizados, se concluye que no existe una relación directa entre el costo del peaje y la cantidad o gravedad de los siniestros. En otras palabras, el valor cobrado en el peaje no se correlaciona de forma sistemática con el riesgo o la frecuencia de accidentes en sus cercanías. Esta conclusión enfatiza que otros factores —como el volumen de tráfico, las condiciones geomorfológicas del trayecto, la calidad de la infraestructura, entre otros— resultan ser mucho más determinantes en el nivel de siniestralidad.

# Bibliografia

Base de datos - Sectores Criticos De Siniestralidad vial: [Link](https://www.datos.gov.co/Transporte/SECTORES-CRITICOS-DE-SINIESTRALIDAD-VIAL/rs3u-8r4q/data_preview)

Base de datos - Peajes: [Link](https://www.datos.gov.co/Transporte/Peajes/68qj-5xux/data_preview)

Pandas: [Link](https://pandas.pydata.org/)

# Autores

Andres Santiago Puentes Munevar

Juan David Ramirez Marin

Realizado el 10/04/2025 - Data analytics
