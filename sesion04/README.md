# Usando Bigquery Data Transfer

0. Diagrama de Arquitectura de la solucion a implementar.

![alt text](arquitectura.png)

1. Siempre antes de empezar establecer el proyecto en el que se ejecutaran los comandos. Ejemplo:

```bash
gcloud config set project nth-victory-357100
```

2. Despliega la funcion con el siguiente comando:

```bash
cd $HOME/utec-data-engineering-en-gcp-g1/sesion04/cloud_functions/daily
gcloud functions deploy python-http-function \
--gen2 \
--timeout=3600 \
--runtime=python38 \
--region=us-east1 \
--source=. \
--entry-point=my_http_function \
--trigger-http \
--allow-unauthenticated
```

3. Ejecuta la funcion:

```bash
#gcloud functions call "python-http-function" --region=us-east1 --gen2
curl \
  --request GET \
  --header "Authorization: Bearer $(gcloud auth print-access-token)" \
  $(gcloud functions describe python-http-function \
    --region=us-east1 --gen2\
    --format="value(serviceConfig.uri)")
```

4. Abre otra terminal y crea la tabla destino

```bash
bq rm -f -t binance.BTCUSDT
bq mk --table --time_partitioning_field open_time \
    --time_partitioning_type DAY \
    binance.BTCUSDT sesion04/schema.json
```

5. Ejecuta el transfer:

```bash
bq mk --transfer_config \
--project_id=nth-victory-357100 \
--target_dataset=binance \
--display_name='Binance' \
--params='{"data_path_template":"gs://rimac-arnold-huete/binance-data/daily/BTCUSDT-1m-*.csv",
"destination_table_name_template":"BTCUSDT",
"file_format":"CSV",
"ignore_unknown_values":"true",
"field_delimiter":",",
"allow_quoted_newlines":"true",
"allow_jagged_rows":"false"}' \
--data_source=google_cloud_storage \
--schedule='every 15 minutes'
```