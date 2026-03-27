---
category: general
date: 2026-01-12
description: Aprende a mostrar información de AsposeAI enumerando los modelos locales,
  mostrando el nombre del modelo, el tamaño y la marca de tiempo de la última vez
  que se usó, en un ejemplo claro de Python.
draft: false
keywords:
- how to display info
- list local models
- display model name
- show model size
- show last used
language: es
og_description: 'Cómo mostrar información de AsposeAI: listar modelos locales, mostrar
  el nombre del modelo, el tamaño y la marca de tiempo de la última vez que se usó,
  con una guía completa en Python.'
og_title: Cómo mostrar información – Lista de modelos locales, nombre, tamaño, último
  uso
tags:
- AsposeAI
- Python
- Model Management
title: Cómo mostrar información – Listar modelos locales, nombre, tamaño, último uso
url: /es/python/general/how-to-display-info-list-local-models-name-size-last-used/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo mostrar información – Listar modelos locales, nombre, tamaño, último uso

¿Alguna vez te has preguntado **cómo mostrar información** de tu instalación de AsposeAI sin tener que hurgar en los registros o en la interfaz? No eres el único. En muchos flujos de trabajo de ciencia de datos lo primero que necesitas es una visión rápida de qué modelos están en tu máquina, cómo se llaman, qué tan grandes son y cuándo los usaste por última vez.

Eso es exactamente lo que cubriremos: un fragmento conciso y de extremo a extremo en Python que **lista modelos locales**, luego **muestra el nombre del modelo**, **muestra el tamaño del modelo** y **muestra la marca de tiempo del último uso**. Sin bibliotecas externas, sin magia oculta—solo el cliente de AsposeAI que ya tienes.

Al final de este tutorial podrás insertar el código en cualquier script, ejecutarlo y obtener al instante una tabla ordenada de tus modelos almacenados localmente. Es perfecto para validar entornos, crear paneles de salud o simplemente saciar la curiosidad sobre qué se esconde en el disco.

## Requisitos previos

- Python 3.8 o superior (el ejemplo usa f‑strings, así que 3.6+ es obligatorio)
- Paquete `asposeai` instalado (`pip install asposeai`)
- Una licencia de AsposeAI válida o una clave de prueba (el cliente tomará las credenciales de variables de entorno o de un archivo de configuración)

Si ya tienes todo eso listo, genial—¡vamos al grano!

## Paso 1: Cómo mostrar información – Inicializar el cliente de AsposeAI

Antes de poder **listar modelos locales**, necesitamos un objeto cliente que se comunique con el runtime de AsposeAI. Este paso es la base; sin él el resto del código lanzaría un `NameError`.

```python
# Step 1: Create an instance of the AsposeAI client
# The client automatically reads credentials from the environment
aspose_ai = AsposeAI()
```

*Por qué es importante*: Inicializar el cliente establece una sesión con el motor de inferencia local, cargando las bibliotecas nativas necesarias. También valida que tu licencia esté activa, evitando errores crípticos más adelante cuando intentes consultar los modelos.

> **Consejo profesional**: Si ejecutas esto en un servidor CI, define `ASPOSEAI_LICENSE` en el entorno para que el cliente pueda iniciarse sin prompts interactivos.

## Paso 2: Listar modelos locales – Recuperar los modelos disponibles

Ahora que el cliente está listo, podemos **listar modelos locales**. El método `list_local()` devuelve una colección de objetos, cada uno con propiedades como `name`, `size_mb` y `last_used`.

```python
# Step 2: Retrieve the list of locally available models
local_models = aspose_ai.list_local()
```

*Qué ocurre tras bambalinas*: `list_local()` escanea el directorio donde AsposeAI almacena en caché los archivos de modelo (`~/.asposeai/models` por defecto) y crea objetos de metadatos ligeros. Es rápido porque no carga los pesos del modelo—solo lee un pequeño manifiesto JSON.

Si alguna vez te preguntas si un modelo concreto ya está en caché, esta llamada es la forma más rápida de confirmarlo.

## Paso 3: Mostrar nombre del modelo, mostrar tamaño del modelo y mostrar último uso

Con los modelos en mano, finalmente **mostramos información** iterando sobre la colección e imprimiendo cada atributo. Aquí **mostramos el nombre del modelo**, **mostramos el tamaño del modelo** y **mostramos el último uso** en una sola línea ordenada.

```python
# Step 3: Print each model's name, size (in MB), and last‑used timestamp
print("Available local models:")
print("-" * 50)
for model_info in local_models:
    # Using an f‑string to format the output cleanly
    print(f"{model_info.name} – {model_info.size_mb} MB – last used {model_info.last_used}")
```

**Salida esperada** (tus marcas de tiempo serán diferentes):

```
Available local models:
--------------------------------------------------
gpt‑tiny‑en – 120 MB – last used 2025-11-02 14:23:11
bert‑base‑fr – 420 MB – last used 2025-10-18 09:07:45
whisper‑large‑audio – 1580 MB – last used 2025-09-30 22:41:02
```

*Por qué lo formateamos así*: El guion (`–`) separa los campos para mayor legibilidad, y la línea de encabezado hace que la salida en consola sea fácil de escanear. Si más adelante necesitas un formato legible por máquinas (CSV, JSON), puedes cambiar fácilmente la llamada a `print` por un `writer.writerow` o `json.dump`.

### Manejo de casos límite

- **No hay modelos en caché** – `list_local()` devuelve una lista vacía. El bucle simplemente se omitirá, dejándote solo con el encabezado. Podrías añadir una protección:

  ```python
  if not local_models:
      print("No local models found. Use aspose_ai.download(...) to fetch one.")
  ```

- **Atributos faltantes** – En casos raros un manifiesto puede estar corrupto. Acceder a `model_info.last_used` podría lanzar `AttributeError`. Envuelve la impresión en un `try/except` si anticipas esos problemas.

- **Directorios de modelos muy grandes** – Si tienes cientos de modelos, considera paginar la salida o escribir a un archivo en lugar de imprimir en la consola.

## Resumen visual (opcional)

Si prefieres una pista visual rápida, el diagrama a continuación ilustra el flujo desde la inicialización del cliente hasta la visualización final.  

![Diagrama que muestra cómo mostrar información desde el cliente de AsposeAI](/images/how-to-display-info.png "diagrama de cómo mostrar información")

*Texto alternativo*: **cómo mostrar información** – esquema de la inicialización del cliente de AsposeAI, listado de modelos y visualización de información.

## Script completo y funcional

Uniendo todo, aquí tienes el script completo y listo para ejecutar:

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

"""
How to display info from AsposeAI:
List local models and show each model's name, size, and last‑used timestamp.
"""

from asposeai import AsposeAI

def main():
    # Initialize client
    aspose_ai = AsposeAI()

    # Retrieve local models
    local_models = aspose_ai.list_local()

    # Header
    print("Available local models:")
    print("-" * 50)

    if not local_models:
        print("No local models found. Use aspose_ai.download(...) to fetch one.")
        return

    # Display each model's details
    for model_info in local_models:
        try:
            print(f"{model_info.name} – {model_info.size_mb} MB – last used {model_info.last_used}")
        except AttributeError:
            # Fallback if any attribute is missing
            print(f"{model_info.name} – info incomplete")

if __name__ == "__main__":
    main()
```

Guárdalo como `list_models.py`, hazlo ejecutable (`chmod +x list_models.py`) y ejecútalo:

```bash
./list_models.py
```

Verás la lista ordenada que se mostró antes.

## Conclusión

Hemos recorrido **cómo mostrar información** de AsposeAI mediante **listado de modelos locales**, luego **mostrando el nombre del modelo**, **mostrando el tamaño del modelo** y **mostrando la marca de tiempo del último uso**. El enfoque es ligero, solo requiere el paquete estándar `asposeai` y puede insertarse en cualquier pipeline de automatización o sesión de depuración.

A partir de aquí podrías:

- Exportar la salida a CSV para análisis en hojas de cálculo (módulo `csv`).
- Alimentar las marcas de tiempo a un panel de monitoreo para alertar sobre modelos obsoletos.
- Combinar este script con `aspose_ai.download()` para refrescar automáticamente los modelos que no se han usado en mucho tiempo.

Recuerda, una visibilidad clara de tu inventario de modelos ahorra tiempo, reduce el exceso de almacenamiento y mantiene tus servicios de IA funcionando sin problemas. Prueba el script, ajusta el formato a tu gusto y conviértelo en una herramienta esencial en tu caja de herramientas.

¡Feliz codificación, y que tus modelos estén siempre frescos!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}