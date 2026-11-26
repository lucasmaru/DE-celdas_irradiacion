# Ensayo de irradiación de celdas solares: análisis de datos de la BeagleBone

Trabajo final de Dispositivos Electrónicos (UNSAM). Análisis de los datos de un ensayo de irradiación de celdas solares, adquiridos con una BeagleBone.

## Qué se midió

Se registró la tensión sobre la celda con una carga fija. Una lámpara se prende 8 minutos y se apaga 8 minutos, de forma cíclica. Hay una muestra cada ~8 s.

Cada línea de los archivos de datos tiene este formato:

```
fecha hora, voltage1, voltage2, estado_luz
2026-11-14 12:58:15.66, 1.1042, 1.4954, 1
```

- `voltage1`: canal que se pensaba usar para medir corriente. Al final no se usó con ese fin.
- `voltage2`: tensión sobre la celda, que es la señal que se analiza.
- `estado_luz`: 1 = lámpara prendida, 0 = apagada.

## Ventanas de análisis

| Ventana | Desde | Hasta | Lugar |
|---|---|---|---|
| Sin radiación | 14/11 12:58 | 16/11 21:29 | UTN (pruebas) |
| Con radiación | 17/11 11:24 | 25/11 19:45 | CNEA (fuente de irradiación) |

Entre ambas hay un tramo de traslado de la UTN a la CNEA. En el análisis se descartan las primeras y las últimas 3 horas de cada ventana, porque corresponden a la instalación y a los ajustes.

## Contenido del repositorio

- `Analisis.ipynb`: notebook con todo el análisis (carga de datos, ventanas, resumen por ciclo, tendencia y perfiles medianos).
- `Archivos/`: datos crudos de la BeagleBone (2867 archivos `.txt`, unas 40 mediciones cada uno).
- `Gráficos/`: figuras generadas por el notebook.
- `Consulta.odt` / `Consulta.pdf`: borrador de la consulta a la cátedra.
- `requirements.txt`: librerías necesarias.

## Cómo correrlo

1. Clonar el repositorio y entrar a la carpeta.
2. Crear y activar un entorno virtual:

   ```bash
   python3 -m venv .venv
   source .venv/bin/activate
   ```

3. Instalar las dependencias:

   ```bash
   pip install -r requirements.txt
   ```

4. Abrir `Analisis.ipynb` (en VSCode o con `jupyter notebook`), elegir el entorno `.venv` como kernel y ejecutar todas las celdas.

El notebook espera encontrar las carpetas `Archivos` y `Gráficos` al lado de él. Si lo abrís desde otro lugar, ajustá las rutas de la primera celda.
