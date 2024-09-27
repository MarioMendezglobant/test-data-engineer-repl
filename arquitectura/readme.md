# Arquitectura

Después de revisar el ejercicio me surgieron las siguientes preguntas:
1. La información proporcionada no menciona si la replicación de datos es desde On-Premise a la nube, de nube a nube o si estos servidores y bases de datos ya se encuentran en la nube de GCP.
2. ¿Cuál es el propósito de buscar la menor latencia posible? Las tablas destino dentro del data warehouse de bigquery servirán para ¿dashboards en línea?, ¿dashboards cada cierto tiempo?, ¿se necesita extraer esta información para otro proceso?, ¿staging/landing? etc,.

##  Replicacion On-Premise a BigQuery

Esta arquitectura parte del supuesto que se tiene que usar CDC y SQL replicate.

![SA-SqlToBigQuery](https://github.com/user-attachments/assets/082b2a6b-8795-4f24-8ffb-c91cf7a18aea)


1. Los datos son propagados a la nube de GCP por medio de SQL replicate.
   Para esto se debe de contar con otra(s) bases de datos en la nube en la modalidad de PAS o SAS(los cuales son indicados en la arquitectura)
2. Existen varias opciones para capturar los cambios realizados en las tablas origen.
   Las opciones mostradas en la arquitectura son las siguientes:
 El servicio de DataFusion puede usarse con su modalidad de Replication.
Para esto solo se deben hacer un par de configuraciones y se puede replicar datos desde Sql Server CDC a BigQuery.
La arquitectura muestra que el consumo de datos provenientes de CDC pueden ser desde PAS o SAS.
3. Otra opción es usar Datastream ya sea recibiendo datos de CDC desde las bases de datos On-Premise o
   ya una vez que los datos fueron replicados a la nube usar el CDC dentro de la nube de las respectivas bases de datos.Datastream solo requiere un par de configuraciones para lograr esta sincronización entre origen y destino aka Sql Server - BigQuery.
