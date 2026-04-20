---
category: general
date: 2026-02-22
description: Aprende a listar los modelos en caché y a mostrar rápidamente el directorio
  de caché en tu máquina. Incluye pasos para ver la carpeta de caché y gestionar el
  almacenamiento local de modelos de IA.
draft: false
keywords:
- list cached models
- show cache directory
- how to view cache folder
- AI model cache
- local model storage
language: es
og_description: Descubre cómo listar los modelos en caché, mostrar el directorio de
  caché y ver la carpeta de caché en unos pocos pasos fáciles. Ejemplo completo en
  Python incluido.
og_title: Listar modelos en caché – guía rápida para ver el directorio de caché
tags:
- AI
- caching
- Python
- development
title: Listar modelos en caché – cómo ver la carpeta de caché y mostrar el directorio
  de caché
url: /es/python/general/list-cached-models-how-to-view-cache-folder-and-show-cache-d/
---

"# list cached models – quick guide to view cache directory" translate to Spanish: "# listar modelos en caché – guía rápida para ver el directorio de caché". Keep same heading level.

Then paragraph.

Translate.

Make sure to keep bold formatting **text**.

Proceed.

Also table: translate column headers and content.

Proceed.

Let's craft final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# listar modelos en caché – guía rápida para ver el directorio de caché

¿Alguna vez te has preguntado cómo **listar modelos en caché** en tu estación de trabajo sin tener que hurgar en carpetas obscuras? No eres el único. Muchos desarrolladores se topan con un muro cuando necesitan verificar qué modelos de IA ya están almacenados localmente, especialmente cuando el espacio en disco es limitado. ¿La buena noticia? En solo unas cuantas líneas puedes **listar modelos en caché** y **mostrar el directorio de caché**, dándote total visibilidad de tu carpeta de caché.

En este tutorial recorreremos un script de Python autocontenido que hace exactamente eso. Al final sabrás cómo ver la carpeta de caché, entender dónde vive la caché en diferentes sistemas operativos y, además, ver una lista impresa ordenada de cada modelo que se haya descargado. Sin documentación externa, sin conjeturas—solo código claro y explicaciones que puedes copiar‑pegar ahora mismo.

## Qué aprenderás

- Cómo inicializar un cliente de IA (o un stub) que ofrezca utilidades de caché.  
- Los comandos exactos para **listar modelos en caché** y **mostrar el directorio de caché**.  
- Dónde se encuentra la caché en Windows, macOS y Linux, para que puedas navegar a ella manualmente si lo deseas.  
- Consejos para manejar casos límite como una caché vacía o una ruta de caché personalizada.  

**Requisitos previos** – necesitas Python 3.8+ y un cliente de IA instalable con pip que implemente `list_local()`, `get_local_path()` y, opcionalmente, `clear_local()`. Si aún no tienes uno, el ejemplo usa una clase mock `YourAIClient` que puedes reemplazar con el SDK real (p. ej., `openai`, `huggingface_hub`, etc.).  

¿Listo? Vamos al grano.

## Paso 1: Configura el cliente de IA (o un mock)

Si ya tienes un objeto cliente, omite este bloque. De lo contrario, crea un pequeño sustituto que imite la interfaz de caché. Esto hace que el script sea ejecutable incluso sin un SDK real.

```python
# step_1_client_setup.py
import os
from pathlib import Path

class YourAIClient:
    """
    Minimal mock of an AI client that stores downloaded models in a
    directory called `.ai_cache` inside the user's home folder.
    """
    def __init__(self, cache_dir: Path | None = None):
        # Use a custom path if supplied, otherwise default to ~/.ai_cache
        self.cache_dir = Path(cache_dir) if cache_dir else Path.home() / ".ai_cache"
        self.cache_dir.mkdir(parents=True, exist_ok=True)

    def list_local(self):
        """Return a list of model folder names that exist in the cache."""
        return [p.name for p in self.cache_dir.iterdir() if p.is_dir()]

    def get_local_path(self):
        """Absolute path to the cache directory."""
        return str(self.cache_dir.resolve())

    # Optional helper for demonstration purposes
    def _populate_dummy_models(self, count=3):
        for i in range(1, count + 1):
            (self.cache_dir / f"model_{i}").mkdir(exist_ok=True)

# Initialize the client (replace with real client if you have one)
ai = YourAIClient()
# Populate with dummy data the first time you run the script
if not ai.list_local():
    ai._populate_dummy_models()
```

> **Consejo profesional:** Si ya dispones de un cliente real (p. ej., `from huggingface_hub import HfApi`), simplemente reemplaza la llamada `YourAIClient()` por `HfApi()` y asegúrate de que existan o estén envueltos los métodos `list_local` y `get_local_path`.

## Paso 2: **listar modelos en caché** – obtenerlos y mostrarlos

Ahora que el cliente está listo, podemos pedirle que enumere todo lo que conoce localmente. Este es el núcleo de nuestra operación **listar modelos en caché**.

```python
# step_2_list_models.py
print("Cached models:")
for model_name in ai.list_local():
    print(" -", model_name)
```

**Salida esperada** (con los datos ficticios del paso 1):

```
Cached models:
 - model_1
 - model_2
 - model_3
```

Si la caché está vacía verás simplemente:

```
Cached models:
```

Esa línea en blanco indica que aún no hay nada almacenado—útil cuando estás creando rutinas de limpieza.

## Paso 3: **mostrar directorio de caché** – ¿dónde vive la caché?

Conocer la ruta suele ser la mitad de la batalla. Los diferentes sistemas operativos colocan las cachés en ubicaciones predeterminadas distintas, y algunos SDK permiten sobrescribirla mediante variables de entorno. El fragmento siguiente imprime la ruta absoluta para que puedas `cd` dentro de ella o abrirla en el explorador de archivos.

```python
# step_3_show_path.py
print("\nCache directory:", ai.get_local_path())
```

**Salida típica** en un sistema tipo Unix:

```
Cache directory: /home/youruser/.ai_cache
```

En Windows podrías ver algo como:

```
Cache directory: C:\Users\YourUser\.ai_cache
```

Ahora sabes exactamente **cómo ver la carpeta de caché** en cualquier plataforma.

## Paso 4: Junta todo – un script único ejecutable

A continuación tienes el programa completo, listo para ejecutarse, que combina los tres pasos. Guárdalo como `view_ai_cache.py` y ejecuta `python view_ai_cache.py`.

```python
# view_ai_cache.py
import os
from pathlib import Path

class YourAIClient:
    """Simple mock client exposing cache‑related utilities."""
    def __init__(self, cache_dir: Path | None = None):
        self.cache_dir = Path(cache_dir) if cache_dir else Path.home() / ".ai_cache"
        self.cache_dir.mkdir(parents=True, exist_ok=True)

    def list_local(self):
        return [p.name for p in self.cache_dir.iterdir() if p.is_dir()]

    def get_local_path(self):
        return str(self.cache_dir.resolve())

    def _populate_dummy_models(self, count=3):
        for i in range(1, count + 1):
            (self.cache_dir / f"model_{i}").mkdir(exist_ok=True)

# ----------------------------------------------------------------------
# Main execution block
# ----------------------------------------------------------------------
if __name__ == "__main__":
    # Initialize (replace with real client if available)
    ai = YourAIClient()

    # Populate dummy data only on first run – remove this in production
    if not ai.list_local():
        ai._populate_dummy_models()

    # Step 1: list cached models
    print("Cached models:")
    for model_name in ai.list_local():
        print(" -", model_name)

    # Step 2: show cache directory
    print("\nCache directory:", ai.get_local_path())
```

Ejecuta el script y verás al instante tanto la lista de modelos en caché **como** la ubicación del directorio de caché.

## Casos límite y variaciones

| Situación | Qué hacer |
|-----------|-----------|
| **Caché vacía** | El script imprimirá “Cached models:” sin entradas. Puedes añadir una advertencia condicional: `if not models: print("⚠️ No models cached yet.")` |
| **Ruta de caché personalizada** | Pasa una ruta al crear el cliente: `YourAIClient(cache_dir=Path("/tmp/my_ai_cache"))`. La llamada a `get_local_path()` reflejará esa ubicación personalizada. |
| **Errores de permiso** | En máquinas con restricciones, el cliente puede lanzar `PermissionError`. Envuelve la inicialización en un bloque `try/except` y recurre a un directorio escribible por el usuario. |
| **Uso de SDK real** | Sustituye `YourAIClient` por la clase cliente real y asegura que los nombres de método coincidan. Muchos SDK exponen un atributo `cache_dir` que puedes leer directamente. |

## Consejos profesionales para gestionar tu caché

- **Limpieza periódica:** Si sueles descargar modelos grandes, programa una tarea cron que llame a `shutil.rmtree(ai.get_local_path())` después de confirmar que ya no los necesitas.  
- **Monitoreo de uso de disco:** Usa `du -sh $(ai.get_local_path())` en Linux/macOS o `Get-ChildItem -Recurse | Measure-Object -Property Length -Sum` en PowerShell para vigilar el tamaño.  
- **Carpetas versionadas:** Algunos clientes crean subcarpetas por versión de modelo. Cuando **listas modelos en caché**, verás cada versión como una entrada separada—útil para podar revisiones antiguas.  

## Visión general visual

![list cached models screenshot](https://example.com/images/list-cached-models.png "list cached models – console output showing models and cache path")

*Texto alternativo:* *list cached models – salida de consola que muestra nombres de modelos en caché y la ruta del directorio de caché.*

## Conclusión

Hemos cubierto todo lo necesario para **listar modelos en caché**, **mostrar el directorio de caché** y, en general, **cómo ver la carpeta de caché** en cualquier sistema. El script breve muestra una solución completa y ejecutable, explica **por qué** cada paso es importante y ofrece consejos prácticos para su uso en entornos reales.  

A continuación, podrías explorar **cómo limpiar la caché** programáticamente, o integrar estas llamadas en una canalización de despliegue más grande que valide la disponibilidad de modelos antes de lanzar trabajos de inferencia. Sea como sea, ahora tienes la base para gestionar el almacenamiento local de modelos de IA con confianza.

¿Tienes preguntas sobre un SDK de IA específico? Deja un comentario abajo, ¡y feliz caché!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}