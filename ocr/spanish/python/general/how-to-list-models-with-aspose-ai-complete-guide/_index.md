---
category: general
date: 2026-07-05
description: Cómo listar modelos con Aspose AI, habilitar la descarga automática y
  descargar un modelo de Hugging Face en Python. Sigue este tutorial paso a paso para
  configurar la caché y comenzar a usar Aspose AI hoy.
draft: false
keywords:
- how to list models
- enable auto download
- download hugging face model
- how to use aspose
- how to set cache
language: es
og_description: Cómo listar modelos con Aspose AI, habilitar la descarga automática
  y descargar un modelo de Hugging Face. Aprende a configurar la caché y usar Aspose
  AI en minutos.
og_title: Cómo listar modelos con Aspose AI – Tutorial completo
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to list models with Aspose AI, enable auto download, and download
    Hugging Face model in Python. Follow this step‑by‑step tutorial to set up cache
    and start using Aspose AI today.
  headline: How to list models with Aspose AI – Complete Guide
  type: TechArticle
- description: How to list models with Aspose AI, enable auto download, and download
    Hugging Face model in Python. Follow this step‑by‑step tutorial to set up cache
    and start using Aspose AI today.
  name: How to list models with Aspose AI – Complete Guide
  steps:
  - name: Create an `AsposeAI` object and a `AsposeAIModelConfig`.
    text: Create an `AsposeAI` object and a `AsposeAIModelConfig`.
  - name: Set `allow_auto_download = "true"` and point `directory_model_path` to a
      folder you control.
    text: Set `allow_auto_download = "true"` and point `directory_model_path` to a
      folder you control.
  - name: Initialise the AI, then call `list_local()` to see exactly what’s cached.
    text: Initialise the AI, then call `list_local()` to see exactly what’s cached.
  - name: Use the listed model name for inference, and you’re ready to build real‑world
      applications.
    text: Use the listed model name for inference, and you’re ready to build real‑world
      applications.
  type: HowTo
tags:
- Aspose
- Python
- LLM
- Model Management
title: Cómo listar modelos con Aspose AI – Guía completa
url: /es/python/general/how-to-list-models-with-aspose-ai-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo listar modelos con Aspose AI – Guía completa

Cómo listar modelos con Aspose AI es una pregunta que surge en el momento en que empiezas a experimentar con grandes modelos de lenguaje en Python. En este tutorial recorreremos la habilitación de **descarga automática**, la configuración de una caché local y la obtención de un modelo directamente de Hugging Face, para que puedas comenzar sin buscar archivos manualmente.

Si alguna vez te has preguntado *“¿cómo uso Aspose para IA impulsada por OCR?”* o *“¿cuál es la forma más fácil de establecer la caché para archivos de modelo?”*, estás en el lugar correcto. Al final tendrás un script totalmente funcional que lista cada modelo almacenado localmente, descarga automáticamente los que falten y muestra exactamente dónde viven los archivos en disco.

---

## Lo que necesitarás

Antes de sumergirnos, asegúrate de tener:

- Python 3.9 o superior (la biblioteca usa anotaciones de tipo que requieren un intérprete reciente)
- Acceso a `pip` para instalar el paquete **Aspose OCR** (`aocr`).  
  ```bash
  pip install aocr
  ```
- Una conexión a internet para la primera descarga desde Hugging Face.
- Una carpeta donde quieras guardar la caché de modelos (por ejemplo, `./model_cache`).

Eso es todo: sin contenedores Docker extra, sin entornos virtuales pesados más allá de una instalación limpia de Python.

---

## ## Cómo listar modelos con Aspose AI

El corazón de esta guía es la capacidad de **listar modelos** que Aspose AI ha almacenado en caché localmente. Una vez configurada la caché, la biblioteca puede enumerar todo lo que conoce, facilitando la depuración y el control de versiones.

```python
import aocr

# 1️⃣ Create an Aspose AI instance
ai = aocr.AsposeAI()

# 2️⃣ Configure the model cache and auto‑download behavior
cfg = aocr.AsposeAIModelConfig()
cfg.allow_auto_download = "true"                     # ← enable auto download
cfg.directory_model_path = r"./model_cache"          # ← how to set cache
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"

# 3️⃣ Initialise the AI with the config we just built
ai.initialize(cfg)

# 4️⃣ List the models that are already cached locally
print("🗂️ Models cached at:", ai.get_local_path())
print("📦 Available models:", ai.list_local())
```

**Por qué funciona esto:**  
- `AsposeAI()` crea el punto de entrada de alto nivel que se comunica con el motor de inferencia subyacente.  
- `AsposeAIModelConfig()` contiene todos los parámetros configurables; establecer `allow_auto_download` a `"true"` indica a la biblioteca que descargue automáticamente los archivos faltantes del repositorio que especifiques.  
- `directory_model_path` es el *directorio de caché*, el lugar donde viven todos los binarios descargados.  
- `initialize()` aplica la configuración, realizando la primera descarga si la caché está vacía.  
- Finalmente, `list_local()` escanea la carpeta de caché y devuelve una lista de Python con los identificadores de los modelos, que imprimimos.

### Salida esperada (primer ejecución)

```
🗂️ Models cached at: ./model_cache
📦 Available models: ['Qwen2.5-3B-Instruct-GGUF']
```

Si ejecutas el script nuevamente, la biblioteca omitirá la descarga y simplemente listará el modelo ya presente, demostrando que **cómo establecer la caché** realmente paga dividendos en ejecuciones posteriores.

---

## ## Habilitar descarga automática para modelos faltantes

A menudo trabajarás con varios modelos en diferentes proyectos. Descargar manualmente cada uno desde Hugging Face puede ser tedioso. Al habilitar la descarga automática, Aspose AI se encarga del trabajo pesado.

```python
cfg.allow_auto_download = "true"
```

> **Consejo profesional:** Mantén `allow_auto_download` en `"true"` **solo** en entornos de desarrollo o CI. En producción quizás quieras bloquear la caché para evitar tráfico de red inesperado.

Si más adelante decides desactivarla, simplemente pon la bandera a `"false"` antes de volver a llamar a `initialize()`.

---

## ## Descargar modelo de Hugging Face al vuelo

La línea

```python
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
```

indica a Aspose AI de qué repositorio remoto obtener el modelo. La biblioteca soporta cualquier modelo público en Hugging Face que proporcione un archivo GGUF. ¿Quieres otro modelo? Cambia el ID del repositorio:

```python
cfg.hugging_face_repo_id = "mistralai/Mistral-7B-Instruct-v0.2"
```

Al ejecutar el script, Aspose AI verifica la caché:

- **Si el modelo existe**, lo carga al instante.  
- **Si no existe**, la bandera de descarga automática dispara la descarga, almacena el archivo bajo `directory_model_path` y luego lo registra para uso inmediato.

Este enfoque elimina el proceso de “descargar‑luego‑ejecutar” en dos pasos que muchos tutoriales obligan a seguir.

---

## ## Cómo usar Aspose AI después de que el modelo esté listado

Listar modelos es solo la mitad de la historia. Una vez que sabes que un modelo está presente, puedes iniciar la inferencia:

```python
# Assume the model we just listed is the one we want to use
model_name = ai.list_local()[0]

# Create a simple prompt
prompt = "Explain the difference between supervised and unsupervised learning."

# Run inference
response = ai.run_inference(model_name, prompt)

print("🤖 Model response:", response)
```

**Por qué es importante:**  
- `run_inference()` abstrae la tokenización, el batching y el manejo de GPU.  
- Al pasar el *nombre del modelo* que obtuviste de `list_local()`, garantizas que la llamada de inferencia coincida con el archivo exacto en disco.

---

## ## Cómo establecer la ubicación de la caché para varios proyectos

Si manejas varios proyectos, quizá quieras que cada uno tenga su propia carpeta de caché. El campo `directory_model_path` es simplemente una cadena, por lo que puedes construirla dinámicamente:

```python
import os

project_name = "sentiment_analysis"
cache_root   = "./model_cache"
cfg.directory_model_path = os.path.join(cache_root, project_name)
```

Ahora cada proyecto obtiene una sub‑carpeta aislada (`./model_cache/sentiment_analysis`), evitando conflictos de versiones y facilitando la limpieza.

---

## ## Problemas comunes y cómo evitarlos

| Síntoma | Causa probable | Solución |
|---------|----------------|----------|
| **`PermissionError` al acceder a la caché** | La carpeta de caché pertenece a otro usuario (común en servidores compartidos) | Crea la carpeta manualmente con los permisos adecuados: `mkdir -p ./model_cache && chmod 775 ./model_cache` |
| **El modelo nunca aparece en `list_local()`** | `allow_auto_download` está en `"false"` y el modelo aún no está en caché | Activa la bandera temporalmente, ejecuta una vez, luego desactívala si lo deseas |
| **Versión de modelo inesperada** | Dos repositorios diferentes comparten el mismo nombre pero archivos distintos | Fija el ID exacto del repositorio (incluyendo etiqueta/commit) o bloquea la caché desactivando la descarga automática después del primer pull exitoso |
| **Errores de falta de memoria** | Archivos GGUF grandes en una máquina sin suficiente RAM/VRAM | Usa un modelo más pequeño (p. ej., `Qwen2.5-1.5B`) o establece `cfg.device = "cpu"` para forzar inferencia en CPU |

---

## ## Script completo que puedes copiar‑pegar

A continuación tienes el ejemplo completo, listo para ejecutar, que incorpora todos los conceptos anteriores. Guárdalo como `list_models_demo.py` y ejecútalo con `python list_models_demo.py`.

```python
# list_models_demo.py
import os
import aocr

def main():
    # ------------------------------------------------------------------
    # 1️⃣ Create the Aspose AI instance
    # ------------------------------------------------------------------
    ai = aocr.AsposeAI()

    # ------------------------------------------------------------------
    # 2️⃣ Build configuration: enable auto download, set cache path,
    #    and point at a Hugging Face repo
    # ------------------------------------------------------------------
    cfg = aocr.AsposeAIModelConfig()
    cfg.allow_auto_download = "true"                               # enable auto download
    cfg.directory_model_path = os.path.abspath("./model_cache")   # how to set cache
    cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"

    # ------------------------------------------------------------------
    # 3️⃣ Initialise the AI with the configuration
    # ------------------------------------------------------------------
    ai.initialize(cfg)

    # ------------------------------------------------------------------
    # 4️⃣ Verify cache location and list all locally available models
    # ------------------------------------------------------------------
    print("🗂️ Models cached at:", ai.get_local_path())
    print("📦 Available models:", ai.list_local())

    # ------------------------------------------------------------------
    # 5️⃣ (Optional) Run a quick inference using the first listed model
    # ------------------------------------------------------------------
    if ai.list_local():
        model_name = ai.list_local()[0]
        prompt = "Give a short summary of the Python GIL."
        response = ai.run_inference(model_name, prompt)
        print("\n🤖 Model response:", response)

if __name__ == "__main__":
    main()
```

**Al ejecutarlo** producirás una salida similar al ejemplo anterior, seguida de una respuesta concisa del modelo. Siéntete libre de reemplazar el prompt por lo que quieras; esta es la forma más rápida de comprobar que el modelo es realmente utilizable después de **cómo listar modelos**.

---

## ## Resumen

Hemos cubierto todo lo necesario para **cómo listar modelos** usando Aspose AI, desde habilitar **descarga automática** hasta configurar una **caché** persistente y obtener un **modelo de Hugging Face** bajo demanda. Los puntos clave:

1. Crea un objeto `AsposeAI` y una `AsposeAIModelConfig`.  
2. Establece `allow_auto_download = "true"` y apunta `directory_model_path` a una carpeta que controles.  
3. Inicializa la IA y luego llama a `list_local()` para ver exactamente qué está en caché.  
4. Usa el nombre del modelo listado para la inferencia y estarás listo para construir aplicaciones del mundo real.

---

## ## ¿Qué sigue?

- **Experimenta con diferentes modelos** – cambia `cfg.hugging_face_repo_id` por otro repositorio y observa cómo cambia la lista.  
- **Ajustar la caché**  

## ## ¿Qué deberías aprender a continuación?

Los tutoriales siguientes cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [How to Set Aspose OCR License and Verify It in Java](/ocr/english/java/ocr-basics/set-license/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}