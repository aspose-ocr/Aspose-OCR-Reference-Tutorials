---
category: general
date: 2026-06-22
description: Aprende a listar los modelos de IA en caché usando el SDK de IA en Python.
  Incluye pasos para obtener el directorio de caché de modelos y gestionar eficientemente
  los modelos de IA locales.
draft: false
keywords:
- list cached ai models
- retrieve model cache directory
- list local ai models
- ai sdk python
- manage ai model cache
language: es
og_description: Enumera los modelos de IA almacenados en caché con Python usando el
  SDK de IA. Sigue este tutorial paso a paso para obtener el directorio de caché de
  modelos y gestionar los modelos de IA locales.
og_title: Lista de modelos de IA en caché en Python – Guía completa
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to list cached AI models using the AI SDK in Python. Includes
    steps to retrieve model cache directory and manage local AI models efficiently.
  headline: List Cached AI Models in Python – Complete Guide
  type: TechArticle
- description: Learn how to list cached AI models using the AI SDK in Python. Includes
    steps to retrieve model cache directory and manage local AI models efficiently.
  name: List Cached AI Models in Python – Complete Guide
  steps:
  - name: Import the AI SDK
    text: '```python # Step 1: Import the AI SDK (replace with the actual package
      name if different) import ai ```'
  - name: List All Cached Models
    text: '```python # Step 2: List all models that are cached locally cached_models
      = ai.list_local() print("Cached models:", cached_models) ```'
  - name: Retrieve the Model Cache Directory
    text: '```python # Step 3: Retrieve the directory where the model files are stored
      cache_dir = ai.get_local_path() print("Model cache directory:", cache_dir) ```'
  - name: Empty Cache
    text: If `ai.list_local()` returns an empty list, you might wonder whether the
      SDK is misconfigured. Double‑check the environment variable `AI_CACHE_DIR` (or
      the SDK’s config file) to ensure it points to a writable location.
  - name: Permissions Issues
    text: When accessing `ai.get_local_path()`, a `PermissionError` can surface on
      restrictive systems. The fix is usually to run the script with appropriate user
      rights or to adjust the directory’s ACLs.
  - name: Version Mismatches
    text: 'Sometimes the cache contains an older version of a model while your code
      requests a newer one. The SDK will automatically download the newer version,
      but you can pre‑empt this by inspecting the version tag in the list:'
  - name: Cleaning Up Old Models
    text: 'If you need to free up space, you can delete a specific model folder directly:'
  type: HowTo
- questions:
  - answer: Yes. The SDK abstracts away OS‑specific paths, so `ai.get_local_path()`
      returns a valid string on Linux, macOS, and Windows.
    question: Does this work on all operating systems?
  - answer: The built‑in `list_local()` only reports locally stored artifacts. For
      remote registries you’d use `ai.list_remote()` (if your SDK version provides
      it).
    question: Can I list models from a remote cache?
  - answer: 'Replace the import line with the actual package name, e.g., `import myai
      as ai`. All subsequent calls stay the same because the API contract is consistent
      across implementations. --- ## Conclusion You now have a solid, production‑ready
      method to **list cached AI models** using the **AI SDK Python** '
    question: What if the SDK name isn’t `ai`?
  type: FAQPage
tags:
- python
- ai
- sdk
title: Lista de modelos de IA en caché en Python – Guía completa
url: /es/python/general/list-cached-ai-models-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Listar modelos de IA en caché en Python – Guía completa

¿Alguna vez te has preguntado cómo **listar modelos de IA en caché** en tu estación de trabajo sin tener que buscar en carpetas poco claras? No estás solo. Muchos desarrolladores se topan con un obstáculo cuando necesitan verificar qué modelos ya están almacenados localmente, especialmente al trabajar con ancho de banda limitado o despliegues sin conexión. En este tutorial verás una forma rápida y sin rodeos de consultar el AI SDK, imprimir el contenido de la caché y descubrir exactamente dónde viven esos archivos.

También abordaremos temas relacionados como **recuperar el directorio de caché del modelo**, manejar cachés vacías y buenas prácticas para **gestionar la caché de modelos de IA** en scripts de producción. Al final tendrás un fragmento autónomo que puedes insertar en cualquier proyecto Python.

## Requisitos previos

- Python 3.8 o superior instalado.
- El AI SDK (el paquete `ai`) instalado mediante `pip install ai-sdk` o el repositorio interno de tu organización.
- Familiaridad básica con la ejecución de scripts desde la línea de comandos.

No se requieren bibliotecas adicionales, por lo que el ejemplo sigue siendo liviano y portátil.

---

## Listar modelos de IA en caché – Visión rápida

Lo primero que debes hacer es importar el SDK y llamar a sus funciones auxiliares. El SDK expone dos métodos útiles:

1. `ai.list_local()` – devuelve una lista de Python con los identificadores de los modelos que ya están en caché.
2. `ai.get_local_path()` – devuelve el directorio absoluto donde residen esos archivos de modelo.

Ambas llamadas son síncronas y generan un `AIError` claro si algo falla, lo que simplifica el manejo de errores.

> **¿Por qué usar estas funciones?**  
> Conocer el conjunto exacto de modelos en caché te permite evitar descargas innecesarias, depurar incompatibilidades de versiones y limpiar artefactos antiguos automáticamente. Es una pequeña parte del flujo de trabajo más amplio del **AI SDK Python**, pero puede ahorrarte horas de búsqueda manual en el sistema de archivos.

### Paso 1: Importar el AI SDK

```python
# Step 1: Import the AI SDK (replace with the actual package name if different)
import ai
```

*Por qué es importante:* Importar el paquete registra las extensiones C subyacentes y carga archivos de configuración (como rutas de caché) desde tu entorno. Omitir este paso generará un `ModuleNotFoundError` en el momento en que llames a cualquier función del SDK.

### Paso 2: Listar todos los modelos en caché

```python
# Step 2: List all models that are cached locally
cached_models = ai.list_local()
print("Cached models:", cached_models)
```

**Lo que verás:** Si tienes tres modelos almacenados, la salida podría ser:

```
Cached models: ['gpt-4-mini', 'bert-base-uncased', 'stable-diffusion-v1']
```

Si la caché está vacía, obtendrás una lista vacía:

```
Cached models: []
```

> **Consejo profesional:** Envuelve la llamada en un bloque try/except si sospechas que el SDK podría no estar inicializado correctamente.

```python
try:
    cached_models = ai.list_local()
except ai.AIError as e:
    print("Failed to list cached models:", e)
    cached_models = []
```

### Paso 3: Recuperar el directorio de caché del modelo

```python
# Step 3: Retrieve the directory where the model files are stored
cache_dir = ai.get_local_path()
print("Model cache directory:", cache_dir)
```

Salida típica en un sistema tipo Unix:

```
Model cache directory: /home/you/.cache/ai/models
```

En Windows podrías ver algo como `C:\Users\you\AppData\Local\ai\models`. Conocer esta ruta es esencial cuando necesitas **gestionar la caché de modelos de IA** manualmente—quizá para purgar versiones antiguas o copiar archivos a una unidad compartida.

---

## Resumen visual

![Diagram showing how to list cached AI models, retrieve their names, and locate the cache directory](https://example.com/images/list-cached-ai-models.png)

*Texto alternativo:* Diagrama que ilustra el proceso para **listar modelos de IA en caché** usando el AI SDK en Python.

## Manejo de casos límite y errores comunes

### Caché vacía

Si `ai.list_local()` devuelve una lista vacía, podrías preguntarte si el SDK está mal configurado. Verifica la variable de entorno `AI_CACHE_DIR` (o el archivo de configuración del SDK) para asegurarte de que apunta a una ubicación escribible.

```python
if not cached_models:
    print("No models are cached. Consider downloading a model first.")
```

### Problemas de permisos

Al acceder a `ai.get_local_path()`, puede aparecer un `PermissionError` en sistemas restrictivos. La solución suele ser ejecutar el script con los derechos de usuario apropiados o ajustar las ACL del directorio.

### Incompatibilidades de versión

A veces la caché contiene una versión antigua de un modelo mientras tu código solicita una más reciente. El SDK descargará automáticamente la versión más nueva, pero puedes anticiparte inspeccionando la etiqueta de versión en la lista:

```python
for model in cached_models:
    if "v2" not in model:
        print(f"Model {model} may be outdated.")
```

### Limpieza de modelos antiguos

Si necesitas liberar espacio, puedes eliminar directamente una carpeta de modelo específica:

```python
import shutil, os

def purge_model(model_name):
    path = os.path.join(cache_dir, model_name)
    if os.path.isdir(path):
        shutil.rmtree(path)
        print(f"Purged {model_name} from cache.")
    else:
        print(f"{model_name} not found in cache.")
```

Ejecutar `purge_model('bert-base-uncased')` eliminará ese modelo y liberará espacio en disco.

## Script completo que puedes copiar‑pegar

A continuación tienes un script listo para ejecutar que combina todos los pasos, agrega manejo básico de errores y muestra un resumen amigable.

```python
#!/usr/bin/env python3
"""
Complete example: list cached AI models and show cache directory.
"""

import ai
import os
import sys
import shutil

def main():
    try:
        # Retrieve cached model list
        cached = ai.list_local()
        print("Cached models:", cached)

        # Retrieve cache directory
        cache_dir = ai.get_local_path()
        print("Model cache directory:", cache_dir)

        # Summarize status
        if not cached:
            print("\n⚠️  No models are currently cached.")
        else:
            print("\n✅  Found {} model(s) in cache.".format(len(cached)))

        # Optional: ask user if they want to purge an old model
        if cached:
            to_purge = input("\nEnter a model name to purge (or press Enter to skip): ").strip()
            if to_purge:
                purge_path = os.path.join(cache_dir, to_purge)
                if os.path.isdir(purge_path):
                    shutil.rmtree(purge_path)
                    print(f"🗑️  Purged {to_purge} from cache.")
                else:
                    print(f"❌  Model {to_purge} not found in cache.")
    except ai.AIError as err:
        print("AI SDK error:", err, file=sys.stderr)
        sys.exit(1)
    except Exception as exc:
        print("Unexpected error:", exc, file=sys.stderr)
        sys.exit(1)

if __name__ == "__main__":
    main()
```

**Salida esperada (cuando la caché está poblada):**

```
Cached models: ['gpt-4-mini', 'bert-base-uncased', 'stable-diffusion-v1']
Model cache directory: /home/you/.cache/ai/models

✅  Found 3 model(s) in cache.

Enter a model name to purge (or press Enter to skip):
```

Ejecuta el script con `python list_models.py` y sabrás al instante qué está almacenado en disco.

---

## Preguntas frecuentes

**P: ¿Funciona esto en todos los sistemas operativos?**  
R: Sí. El SDK abstrae las rutas específicas del SO, por lo que `ai.get_local_path()` devuelve una cadena válida en Linux, macOS y Windows.

**P: ¿Puedo listar modelos de una caché remota?**  
R: El `list_local()` incorporado solo informa de los artefactos almacenados localmente. Para registros remotos usarías `ai.list_remote()` (si tu versión del SDK lo proporciona).

**P: ¿Qué pasa si el nombre del SDK no es `ai`?**  
R: Reemplaza la línea de importación con el nombre real del paquete, por ejemplo, `import myai as ai`. Todas las llamadas posteriores permanecen iguales porque el contrato de la API es consistente entre implementaciones.

## Conclusión

Ahora tienes un método sólido y listo para producción para **listar modelos de IA en caché** usando la biblioteca **AI SDK Python**, recuperar el **directorio de caché del modelo** y hasta limpiar archivos antiguos. Este conocimiento te ayuda a mantener tu entorno ordenado, evitar descargas redundantes y depurar problemas de versiones con facilidad.

¿Listo para el siguiente paso? Intenta ampliar el script para descargar automáticamente los modelos faltantes, o intégralo en una canalización CI que valide la salud de la caché antes de cada compilación. Explorar estrategias para **gestionar la caché de modelos de IA** hará que tus aplicaciones impulsadas por IA sean más rápidas y fiables.

¡Feliz codificación, y que tus cachés se mantengan ligeras!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo procesar por lotes imágenes OCR con List en Aspose.OCR para .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Extraer texto de imagen en C# con selección de idioma usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Cómo extraer texto de archivos ZIP usando Aspose.OCR para .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}