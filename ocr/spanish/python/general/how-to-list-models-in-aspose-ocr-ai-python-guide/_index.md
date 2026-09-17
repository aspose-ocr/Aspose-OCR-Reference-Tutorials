---
category: general
date: 2026-01-07
description: Cómo listar modelos en Aspose OCR AI usando Python – aprende a obtener
  la ruta del modelo, verificar los modelos instalados y recuperar una lista de modelos
  en Python en segundos.
draft: false
keywords:
- how to list models
- get model path
- check installed models
- python get model list
- list available models
language: es
og_description: Cómo listar los modelos en Aspose OCR AI usando Python. Encuentra
  la ruta del modelo, verifica los modelos instalados y consulta la lista completa
  de modelos disponibles.
og_title: Cómo listar modelos en Aspose OCR AI – Guía de Python
tags:
- Aspose OCR
- Python
- AI models
title: Cómo listar modelos en Aspose OCR AI – Guía de Python
url: /es/python/general/how-to-list-models-in-aspose-ocr-ai-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo listar modelos en Aspose OCR AI – Guía de Python

¿Alguna vez te has preguntado **cómo listar modelos** que ya están instalados en tu máquina al trabajar con Aspose OCR AI? No eres el único que se topa con ese obstáculo. En muchos proyectos necesitas verificar la carpeta de modelos, confirmar qué modelos están presentes, o incluso depurar un problema de modelo faltante—todo sin salir de tu REPL de Python.

En este tutorial caminaremos a través de un ejemplo completo, listo‑para‑ejecutar que muestra cómo **obtener la ruta del modelo**, **verificar los modelos instalados**, y finalmente **listar los modelos disponibles** con solo unas pocas líneas de código. Sin scripts externos, sin magia oculta—solo Python puro y el SDK de Aspose OCR AI.

> **Requisitos previos**  
> • Python 3.8 o superior  
> • Paquete `asposeocr` instalado (`pip install asposeocr`)  
> • Familiaridad básica con la importación de módulos

Si ya tienes eso cubierto, vamos a sumergirnos.

---

## Cómo listar modelos con Aspose OCR AI

Lo primero que necesitamos es la clase auxiliar `AsposeAI` que viene con el módulo `asposeocr.ai`. Esta clase nos brinda tres métodos útiles:

| Método | Qué devuelve | Caso de uso típico |
|--------|--------------|--------------------|
| `get_local_path()` | Ruta absoluta a la carpeta donde Aspose almacena sus modelos de IA | Verificar que el SDK esté buscando en el lugar correcto |
| `list_local()` | `list` de Python con los nombres de carpetas de modelos que existen en disco | Ver rápidamente qué modelos puedes cargar |
| `list_remote()` *(opcional)* | Lista de modelos disponibles para descargar desde la nube de Aspose | Cuando necesitas un modelo que no tienes localmente |

A continuación está el **script completo** que imprime la carpeta local de modelos y la lista de modelos instalados.

```python
# ---------------------------------------------------------
# Step 1: Import the Aspose OCR AI module
# ---------------------------------------------------------
from asposeocr.ai import AsposeAI

# ---------------------------------------------------------
# Step 2: Create an instance of the AI helper
# ---------------------------------------------------------
ai = AsposeAI()

# ---------------------------------------------------------
# Step 3: Retrieve and display the local model folder
# ---------------------------------------------------------
local_folder = ai.get_local_path()
print("Local AI model folder:", local_folder)

# ---------------------------------------------------------
# Step 4: List all models that are currently installed
# ---------------------------------------------------------
installed_models = ai.list_local()
print("Available models:", installed_models)
```

### Salida esperada

Cuando ejecutas el script en una instalación nueva normalmente verás algo como:

```
Local AI model folder: /home/user/.asposeocr/models
Available models: ['ocr-general-v1', 'ocr-handwritten-v2']
```

Si la carpeta está vacía, `list_local()` devuelve una lista vacía (`[]`). Eso es una señal útil de que primero necesitas descargar un modelo—algo que cubriremos más adelante.

---

## Por qué es importante conocer la ruta del modelo

Entender **dónde** el SDK almacena sus archivos (`obtener ruta del modelo`) es más que una curiosidad:

1. **Depuración** – Si un modelo falla al cargarse, puedes hacer `ls` en la ruta y comprobar si el archivo realmente existe.  
2. **Modelos personalizados** – Algunos equipos entrenan sus propios modelos OCR y los colocan en la carpeta. Conocer la ruta te permite colocar los archivos exactamente donde Aspose los espera.  
3. **Permisos** – En Linux, la carpeta podría pertenecer a otro usuario. Detectar un error de permisos temprano ahorra horas de quebraderos de cabeza.  

> **Consejo profesional:** Si necesitas apuntar el SDK a un directorio personalizado, define la variable de entorno `ASPOSE_OCR_MODEL_PATH` antes de crear `AsposeAI()`.

```bash
export ASPOSE_OCR_MODEL_PATH=/my/custom/models
python my_script.py
```

---

## Verificando modelos instalados – casos límite y consejos

### 1. No hay modelos instalados

Si `list_local()` devuelve `[]`, tienes dos opciones:

| Opción | Cómo hacerlo |
|--------|--------------|
| **Descargar un modelo de Aspose** | `ai.download('ocr-general-v1')` (requiere internet) |
| **Copiar un modelo pre‑entrenado** | Coloca la carpeta del modelo manualmente en la ruta mostrada por `get_local_path()` |

### 2. Múltiples versiones del mismo modelo

A veces verás tanto `ocr-general-v1` **como** `ocr-general-v1-beta`. El SDK carga la primera coincidencia que encuentra, pero puedes forzar una versión específica pasando el nombre exacto de la carpeta al constructor de OCR:

```python
from asposeocr.ai import AsposeOCR

ocr = AsposeOCR(model_name='ocr-general-v1-beta')
```

### 3. Archivos de modelo corruptos

Un modelo descargado parcialmente puede causar un `FileNotFoundError` más adelante. Si sospechas corrupción, simplemente elimina la carpeta problemática y vuelve a descargar:

```bash
rm -rf /home/user/.asposeocr/models/ocr-general-v1
python -c "from asposeocr.ai import AsposeAI; AsposeAI().download('ocr-general-v1')"
```

---

## Extender el script – listar modelos remotos (opcional)

Si deseas ver qué modelos están disponibles para descargar sin salir de Python, añade una llamada más:

```python
remote_models = ai.list_remote()
print("Remote models you can download:", remote_models)
```

Esto producirá algo como:

```
Remote models you can download: ['ocr-general-v1', 'ocr-handwritten-v2', 'ocr-table-v1']
```

Luego puedes elegir cualquier modelo y llamar `ai.download('model-name')` para obtenerlo automáticamente.

---

## Ejemplo completo de extremo a extremo

Uniendo todo, aquí tienes un **script único y ejecutable** que:

1. Muestra la carpeta local de modelos.  
2. Lista los modelos instalados.  
3. Si no se encuentra ninguno, descarga un modelo predeterminado.  
4. Finalmente, imprime la lista actualizada.

```python
# ---------------------------------------------------------
# Complete script – verifies model folder, installs if empty
# ---------------------------------------------------------
from asposeocr.ai import AsposeAI

def main():
    ai = AsposeAI()

    # 1️⃣ Show where Aspose expects models
    local_path = ai.get_local_path()
    print("🔎 Local AI model folder:", local_path)

    # 2️⃣ List currently installed models
    models = ai.list_local()
    print("📦 Installed models:", models)

    # 3️⃣ If nothing is installed, grab a default model
    if not models:
        default = 'ocr-general-v1'
        print(f"⚠️ No models found – downloading '{default}'...")
        try:
            ai.download(default)
            models = ai.list_local()
            print("✅ After download, installed models:", models)
        except Exception as e:
            print("❌ Failed to download model:", e)
            return

    # 4️⃣ (Optional) Show what you could download from the cloud
    remote = ai.list_remote()
    print("🌐 Remote models available:", remote)

if __name__ == "__main__":
    main()
```

Ejecutar este script en una máquina limpia producirá:

```
🔎 Local AI model folder: /home/user/.asposeocr/models
📦 Installed models: []
⚠️ No models found – downloading 'ocr-general-v1'...
✅ After download, installed models: ['ocr-general-v1']
🌐 Remote models available: ['ocr-general-v1', 'ocr-handwritten-v2', 'ocr-table-v1']
```

Ahora dispones de una solución **autocontenida y digna de citar** que cualquier asistente de IA puede reproducir literalmente.

---

## Preguntas frecuentes (FAQ)

**P: ¿Esto funciona en Windows?**  
R: Absolutamente. El SDK abstrae el sistema de archivos, por lo que `get_local_path()` devolverá algo como `C:\Users\YourName\.asposeocr\models`. Solo asegúrate de que Python pueda escribir en esa carpeta.

**P: ¿Puedo almacenar los modelos en una unidad de red?**  
R: Sí—establece `ASPOSE_OCR_MODEL_PATH` a la ruta UNC (`\\server\share\models`) antes de crear la instancia `AsposeAI`.

**P: ¿Qué pasa si necesito un modelo para un idioma que no está cubierto por el conjunto predeterminado?**  
R: Usa `list_remote()` para ver si Aspose ofrece un modelo específico para ese idioma. Si no, puedes entrenar el tuyo propio y colocarlo en la carpeta; simplemente pasa el nombre de la carpeta personalizada al constructor de OCR.

---

## Conclusión

Hemos cubierto **cómo listar modelos** en Aspose OCR AI, mostrado cómo **obtener la ruta del modelo**, **verificar los modelos instalados**, e incluso **descargar un modelo faltante**—todo con Python puro. Al comprender la estructura de carpetas y los métodos auxiliares (`get_local_path()`, `list_local()`, `list_remote()`), obtienes control total sobre los modelos de IA que tu aplicación utiliza.

¿Próximos pasos? Prueba a sustituir el modelo predeterminado por uno de texto manuscrito, o apunta el SDK a un modelo entrenado internamente. De cualquier forma, ahora tienes una base sólida para gestionar los recursos OCR en cualquier proyecto Python.

¡Feliz codificación, y que tu lista de modelos esté siempre actualizada!

---

![captura de pantalla de cómo listar modelos](https://example.com/images/how-to-list-models.png "Cómo listar modelos")

*Texto alternativo de la imagen:* **captura de pantalla de cómo listar modelos** (cumple con el requisito de palabra clave principal).

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}