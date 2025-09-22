
# FNO0XXX - [MBA] Contexto y manejo de la herramienta Gzip

![MasterBase®](https://masterbase.com/wp-content/uploads/2023/09/Logo.png?w=150 "MasterBase®")

Versión del documento: 202509.1

Fecha de esta versión: 16 de septiembre de 2025

---

## Tabla de contenidos

- [FNO0XXX - \[MBA\] Contexto y manejo de la herramienta Gzip](#fno0xxx---mba-contexto-y-manejo-de-la-herramienta-gzip)
  - [Tabla de contenidos](#tabla-de-contenidos)
  - [Historial de versiones](#historial-de-versiones)
  - [Herramienta Gzip (mb.tool-gzip) para procesos MasterBase®](#herramienta-gzip-mbtool-gzip-para-procesos-masterbase)
  - [Casos de uso](#casos-de-uso)
    - [Caso 1](#caso-1)
  - [Contexto y manejo de la herramienta Gzip (mb.tool-gzip)](#contexto-y-manejo-de-la-herramienta-gzip-mbtool-gzip)
    - [Restricciones - límites - observaciones](#restricciones---límites---observaciones)
  - [Estructura global de un proceso](#estructura-global-de-un-proceso)
  - [Estructura de la herramienta Gzip, para 1) comprimir archivo](#estructura-de-la-herramienta-gzip-para-1-comprimir-archivo)
  - [Elementos y atributos contenidos en la estructura de la herramienta Gzip, para 1) comprimir archivo](#elementos-y-atributos-contenidos-en-la-estructura-de-la-herramienta-gzip-para-1-comprimir-archivo)
  - [Ejemplo de uso de la herramienta Gzip, para 1) comprimir archivo](#ejemplo-de-uso-de-la-herramienta-gzip-para-1-comprimir-archivo)
  - [Ejemplo de respuesta de la herramienta Gzip, para 1) comprimir archivo](#ejemplo-de-respuesta-de-la-herramienta-gzip-para-1-comprimir-archivo)
  - [Estructura de la herramienta Gzip, para 2) desencriptar archivo .gz](#estructura-de-la-herramienta-gzip-para-2-desencriptar-archivo-gz)
  - [Elementos y atributos contenidos en la estructura de la herramienta Gzip, para 2) desencriptar archivo .gz](#elementos-y-atributos-contenidos-en-la-estructura-de-la-herramienta-gzip-para-2-desencriptar-archivo-gz)
  - [Ejemplo de uso de la herramienta Gzip, para 2) desencriptar archivo .gz](#ejemplo-de-uso-de-la-herramienta-gzip-para-2-desencriptar-archivo-gz)
  - [Ejemplo de respuesta de la herramienta Gzip, para 2) desencriptar archivo .gz](#ejemplo-de-respuesta-de-la-herramienta-gzip-para-2-desencriptar-archivo-gz)

---

## Historial de versiones

|Versión|Fecha|Cambios realizados|
|---|---|---|
|202509.1|16.09.2025|Versión inicial|

Material para uso interno de MasterBase® y clientes autorizados.

Copyright© 2025 MasterBase®.  Todos los derechos reservados. Prohibida su reproducción total o parcial

---

## Herramienta Gzip (mb.tool-gzip) para procesos MasterBase®

|Nombre|Gzip (mb.tool-gzip)|
|---|---|
|Tipo|Herramienta|
|Descripción|Herramienta que permite comprimir archivos en formato .gz y descomprimirlos para recuperar su contenido original|
|Creador|MasterBase®|
|**Entorno**|**Plataforma Automata - MBA**|
|Ubicación|Alojada en un servidor MasterBase®|
|Valor|Free|
|Versión del documento|202509.1|
|Uso|Interno y de clientes MasterBase® autorizados|
|Fecha de documentación|16 de septiembre de 2025|
|Última actualización|16 de septiembre de 2025|

---

## Casos de uso

### Caso 1

**Necesidad**: Una universidad guarda reportes académicos en formato CSV. Con el paso del tiempo, se acumulan miles de archivos en su servidor, ocupando mucho espacio de almacenamiento. Se necesita una forma de reducir el tamaño de esos archivos, pero que sigan siendo accesibles cuando se requieran para auditorías o consultas.

**Propuesta**: Se configura un proceso que utiliza la herramienta Gzip, instruida con la acción de compress, para reducir el tamaño de cada archivo entregado por el cliente. De esta forma, los archivos pueden descargarse en formato .gz o almacenarse de manera optimizada en una base de datos de la plataforma.

---

## Contexto y manejo de la herramienta Gzip (mb.tool-gzip)

La herramienta Gzip ha sido desarrollada por MasterBase® y está alojada en un servidor interno. Puede ser utilizada sólo desde la plataforma MasterBase®.

- Esta herramienta provee los siguientes usos:
  - Comprimir un archivo a formato .gz (compress)
  - Descomprimir un archivo en formato .gz (uncompress)
- Permite comprimir un archivo a la vez
  
### Restricciones - límites - observaciones

fileSize limit: Peso máximo del archivo JSON: 20 MB

Esta herramienta sólo puede ser incorporada a un proceso MasterBase® en formato JSON, con una estructura y parámetros definidos, que se explica en detalle en este documento.

---

## Estructura global de un proceso

![Estructura](https://out.filebunker.com/I1011/68c98f69df005d0012093e4c/il8n42oijdcnbsqxgoipl5x18drr9zf2ckh5q9hfeepq16d2f2eutprlveirkynq "Estructura de proceso con esta herramienta")

---

## Estructura de la herramienta Gzip, para 1) comprimir archivo

```JSON
{
  "toolName": "mb.tool-gzip",
  "request":{
    "method": "post",
    "action": "compress",
    "type": "multipart",
    "streams": [
      {
        "fieldName": "file",
        "path": "archivo a comprimir"
      }
    ]
  }
}
```

---

## Elementos y atributos contenidos en la estructura de la herramienta Gzip, para 1) comprimir archivo

- **toolName**: atributo que corresponde al nombre de la herramienta a utilizar. Para utilizar funciones Gzip, su valor debe ser mb.tool-gzip **(atributo obligatorio)**.
- **request**: elemento que agrupa todos los atributos que la herramienta requiere para su correcto funcionamiento y que, por tanto, constituyen los **datos de entrada** (input).
  - **request.method**: atributo que corresponde al método con el cual se va a consumir esta herramienta. Para aplicar funciones, el valor debe ser *post* **(atributo obligatorio)**.
  - **request.action**: atributo que corresponde al tipo de acción que ejecutará esta herramienta, este valor debe ser *compress* **(atributo obligatorio)**.
  - **request.type**: atributo que corresponde al tipo de tratamiento de la información, este valor debe ser *multipart* **(atributo obligatorio)**.
  - **request.streams**: elemento que contiene la información a ser evaluada y las funciones que se aplicará a dicha información.
    - **request.streams.fieldName**: atributo que indica al proceso el nombre del campo donde se almacena la ruta del archivo a comprimir, este valor debe ser *file* **(atributo obligatorio)**.
    - **request.streams.path**: atributo que establece la ruta donde está contenido el archivo a comprimir **(atributo obligatorio)**.

## Ejemplo de uso de la herramienta Gzip, para 1) comprimir archivo

```JSON
{
  "toolName": "mb.tool-gzip",
  "request":{
    "method": "post",
    "action": "compress",
    "type": "multipart",
    "streams": [
      {
        "fieldName": "file",
        "path": "gzip.tasks.[0].data"
      }
    ]
  }
}
```

## Ejemplo de respuesta de la herramienta Gzip, para 1) comprimir archivo

![Respuesta](https://out.filebunker.com/I1011/68cad7782c5db60019668ad7/zla94kronkan4yozbip3zuy21tjlshvt7yvt8o3r0fjszfnqsic8zkrijoi7hs5c "Respuesta de la herramienta")

(entregada en el proceso en que se ejecuta esta herramienta)

---

## Estructura de la herramienta Gzip, para 2) desencriptar archivo .gz

```JSON
{
  "toolName": "mb.tool-gzip",
  "request":{
    "method": "post",
    "action": "uncompress",
    "type": "multipart",
    "streams": [
      {
        "fieldName": "file",
        "path": "archivo a desencriptar"
      }
    ]
  }
}
```

---

## Elementos y atributos contenidos en la estructura de la herramienta Gzip, para 2) desencriptar archivo .gz

- **toolName**: atributo que corresponde al nombre de la herramienta a utilizar. Para utilizar funciones Gzip, su valor debe ser mb.tool-gzip **(atributo obligatorio)**.
- **request**: elemento que agrupa todos los atributos que la herramienta requiere para su correcto funcionamiento y que, por tanto, constituyen los **datos de entrada** (input).
  - **request.method**: atributo que corresponde al método con el cual se va a consumir esta herramienta. Para aplicar funciones, el valor debe ser *post* **(atributo obligatorio)**.
  - **request.action**: atributo que corresponde al tipo de acción que ejecutará esta herramienta, este valor debe ser *uncompress* **(atributo obligatorio)**.
  - **request.type**: atributo que corresponde al tipo de tratamiento de la información, este valor debe ser *multipart* **(atributo obligatorio)**.
  - **request.streams**: elemento que contiene la información a ser evaluada y las funciones que se aplicará a dicha información.
    - **request.streams.fieldName**: atributo que indica al proceso el nombre del campo donde se almacena la ruta del archivo a comprimir, este valor debe ser *file* **(atributo obligatorio)**.
    - **request.streams.path**: atributo que establece la ruta donde está contenido el archivo .gz a descomprimir **(atributo obligatorio)**.

## Ejemplo de uso de la herramienta Gzip, para 2) desencriptar archivo .gz

```JSON
{
  "toolName": "mb.tool-gzip",
  "request":{
    "method": "post",
    "action": "uncompress",
    "type": "multipart",
    "streams": [
      {
        "fieldName": "file",
        "path": "gzip.tasks.[0].data"
      }
    ]
  }
}
```

## Ejemplo de respuesta de la herramienta Gzip, para 2) desencriptar archivo .gz

![Respuesta](https://out.filebunker.com/I1013/68cad5d34c1f2200123c2e9d/5bf0955wmh2hxf9qfb2d1igy7eixxht8eg9e29m9wusr7erkay796h6i6yoo5m5x "Respuesta de la herramienta")

(entregada en el proceso en que se ejecuta esta herramienta)

---
