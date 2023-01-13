# **1. Definiciones del template**

## **1.1. Tipos de tablas requeridas**

- **main_data**: Hace referencia a la tabla principal, donde las columnas poseen datos numéricos sobre los que se basarán los cálculos para las métricas requeridas para el dashboard, o referencias a tablas que brinden información de contexto para el análisis de los datos.

- **dim_tiempo**: Brinda el contexto de tiempo a los datos principales, los componentes de tiempo no están presentes en una sola columna, sino separados como elementos únicos. Es decir hay una columna para Año, otra para Mes y así hasta el nivel de granularidad requerido.

- **dim_unidades**: Brinda el contexto sobre las unidades de negocio, información referente a ellos tal como a que regional pertenecen.

## **1.2. Columnas de salida del dataflow (origen de datos del dashboard)**

|**Columna**  |**Tabla**  |**Tipo de dato**  |**Descripcion**  |**Notas**|
|--|--|--|--|--|
|adopcion_por_un / adoção_por_un |main_data|Whole Number|Conteo de personas/eventos que (han adoptado)/(han sido realizados con) el producto digital.||
|total_por_un|main_data  |Whole Number|Conteo de personas/eventos que deberían (haber adoptado)/(haber sido realizados con) el producto digital.|solo incluye al personal que debería usar el producto digital (excluir personal de limpieza, mantenimiento, etc).|
|regional|main_data (dim_unidades)|Text|Sigla de la regional.||
|nombre_de_mes / nome_do_mes|Comp Tempo (dim_tiempo)|Text|Nombre del mes.||
|sigla_de_unidad / sigla_de_unidade|Comp Unidades (dim_unidades)|Text|Sigla de la unidad de negocio.||

## **1.3. Parámetros de template**
Los parámetros son los valores de entrada para el template.

|**Parámetro**|**Tipo de dato**|**Descripción**|**Notas** |
|--|--|--|--|
|fraccion_objetivo_de_adopcion / fração_alvo_de_adoção|Decimal Number|Es el porcentaje objetivo de (personas adoptando)/(eventos realizados con) una funcionalidad del producto digital.|La fracción esta definida con respecto al total de personas que se espera usen la funcionalidad del producto digital, se excluye personal de limpieza, mantenimiento.|
|dataflow_de_entrada|Text|Es la cadena de caracteres necesaria para conectarse al dataflow.|Se debe tomar en cuenta que se debe tener las credenciales correctas para poder extraer a información del dataflow.||

## **1.4. Tablas calculadas**



## **1.5. Columnas calculadas**



## **1.6. Medidas**

Tomar en cuenta que algunas medidas pueden hacer uso de columnas o tablas calculadas.

|**Medida**|**Tipo de dato**|**Descripción**|**Medidas**|**Columnas** |
|--|--|--|--|--|
|conteo_de_adopcion/contagem_de_adoção|Whole Number|Es la suma de los conteos por unidad de negocio de las personas que adoptaron la funcionalidad del producto digital.||main_data[adopcion_por_un] ||
|conteo_total|Whole number|Es la suma de los conteos por unidad de negocio del total de personas.|||
|%_de_adopcion/%_de_adoção|Decimal Number|Representa el porcentaje de (personas que han adoptado)/(eventos que se han realizado utilizando) la funcionalidad.|conteo_de_adopcion, conteo_total||