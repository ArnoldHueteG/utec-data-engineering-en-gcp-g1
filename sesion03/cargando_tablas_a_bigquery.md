# Cargando Tablas a Bigquery

1. Descargar el archivo y cargarlo a cloud storage. antes de ejecutar el comando debes reemplazar el bucket de destino. En este laboratorio estamos usando "rimac-arnold-huete".

```bash
curl -O "https://data.binance.vision/data/spot/monthly/klines/BTCUSDT/1m/BTCUSDT-1m-2022-07.zip"
unzip BTCUSDT-1m-2022-07.zip
gsutil cp BTCUSDT-1m-2022-07.csv gs://rimac-arnold-huete/binance-data/BTCUSDT-1m-2022-07.csv
```

2. Cargar la tabla desde la consola de gcp.

3. Cargar la tabla desde la linea de comandos.

```bash
bq load --source_format=CSV --replace --allow_quoted_newlines binance.BTCUSDT gs://rimac-arnold-huete/binance-data/BTCUSDT-1m-2022-07.csv sesion03/schema.json
```
