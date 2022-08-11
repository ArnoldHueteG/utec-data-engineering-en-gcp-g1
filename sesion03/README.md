# Laboratorios

1. [Consultando datos publicos](https://cloud.google.com/bigquery/docs/quickstarts/query-public-dataset-console)
2. [Cargando tablas a Bigquery](./cargando_tablas_a_bigquery.md)
3. [Particionando y Clusterizando - Video](https://www.youtube.com/watch?v=wapi0aR4BZE)
4. [Particionando y Clusterizando - Blog](https://cloud.google.com/blog/topics/developers-practitioners/bigquery-explained-storage-overview)

# Bonus

1. [BigQuery for Data Warehousing](https://www.cloudskillsboost.google/quests/68?catalog_rank=%7B%22rank%22%3A3%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D&search_id=17649189)

# Preguntas

1. Se puede cargar data a google cloud storage usando la consola desde otras fuentes de datos? Ejemplo: Sharepoint

No existe una solucion nativa de gcp. Existen algunos servicios:

- [Pipes](https://pipes.datavirtuality.com/connectors/integrate/microsoft-sharepoint-online-connector/google-bigquery/)
- [Tray.io](https://tray.io/connectors/microsoft-office-365-sharepoint-google-bigquery-integrations)

2. Se pueden proteger tablas especificas de borrado?

El acceso se maneja por IAM y la habilitacion es por usuario. Si quieres proteger tablas, la unica opcion es quitando este permiso al grupo de usuarios o usuarios el premiso para borrado. Puedes ver mas [aquí](https://cloud.google.com/bigquery/docs/table-access-controls-intro).

Por otro lado tienes la opcion de acceder a una version antes de ser borrado puedes usar la siguiente opcion de Bigquery ["Time Travel"]
(https://cloud.google.com/bigquery/docs/time-travel)

3. Existe otra forma de cargar a Bigquery?

- La primera opcion siempre debe ser cargar datos a traves de cloud storage. Luego puedes utilizar streaming api pero tiene un costo asociado o crear registros mediantes sentencias DML (INSERT, UPDATE , DELETE) . Este ultimo no es desalentado porque genera costos de actualizacion por cada transaccion. Si estas trabajando con tablas de gran volumen puedes incurrir en un gasto enorme.