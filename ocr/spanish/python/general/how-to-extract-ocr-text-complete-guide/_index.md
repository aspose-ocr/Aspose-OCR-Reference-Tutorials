---
category: general
date: 2026-02-22
description: Aprende cómo extraer texto OCR y mejorar la precisión del OCR con post‑procesamiento
  de IA. Limpia texto OCR fácilmente en Python con un ejemplo paso a paso.
draft: false
keywords:
- how to extract OCR
- improve OCR accuracy
- clean OCR text
- OCR post‑processing
- AI OCR enhancement
language: es
og_description: Descubre cómo extraer texto OCR, mejorar la precisión del OCR y limpiar
  el texto OCR utilizando un flujo de trabajo simple en Python con post‑procesamiento
  de IA.
og_title: Cómo extraer texto OCR – Guía paso a paso
tags:
- OCR
- AI
- Python
title: Cómo extraer texto OCR – Guía completa
url: /es/python/general/how-to-extract-ocr-text-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo extraer texto OCR – Tutorial de programación completo

¿Alguna vez te has preguntado **cómo extraer OCR** de un documento escaneado sin terminar con un desastre de errores tipográficos y líneas rotas? No estás solo. En muchos proyectos del mundo real, la salida cruda de un motor OCR se ve como un párrafo desordenado, y limpiarlo se siente como una tarea tediosa.  

¿La buena noticia? Siguiendo esta guía verás una forma práctica de obtener datos OCR estructurados, ejecutar un post‑procesador de IA y terminar con **texto OCR limpio** listo para análisis posteriores. También abordaremos técnicas para **mejorar la precisión del OCR** para que los resultados sean fiables desde el primer intento.

En los próximos minutos cubriremos todo lo que necesitas: bibliotecas requeridas, un script completo ejecutable y consejos para evitar errores comunes. No atajos vagos como “ver la documentación”, solo una solución completa y autónoma que puedes copiar‑pegar y ejecutar.

## Lo que necesitarás

- Python 3.9+ (el código usa anotaciones de tipo pero funciona en versiones 3.x más antiguas)
- Un motor OCR que pueda devolver un resultado estructurado (p. ej., Tesseract vía `pytesseract` con la bandera `--psm 1`, o una API comercial que ofrezca metadatos de bloque/línea)
- Un modelo de post‑procesamiento de IA – para este ejemplo lo simularemos con una función simple, pero puedes sustituirlo por `gpt‑4o-mini` de OpenAI, Claude, o cualquier LLM que acepte texto y devuelva una salida limpia
- Algunas líneas de imagen de muestra (PNG/JPG) para probar

Si tienes todo listo, vamos a sumergirnos.

## Cómo extraer OCR – Recuperación inicial

El primer paso es llamar al motor OCR y solicitarle una **representación estructurada** en lugar de una cadena simple. Los resultados estructurados preservan los límites de bloques, líneas y palabras, lo que facilita mucho la limpieza posterior.

```python
import pytesseract
from PIL import Image
from dataclasses import dataclass, field
from typing import List

# Simple data classes mirroring a typical structured OCR response
@dataclass
class Line:
    text: str

@dataclass
class Block:
    lines: List[Line] = field(default_factory=list)

@dataclass
class StructuredResult:
    blocks: List[Block] = field(default_factory=list)

def recognize_structured(image_path: str) -> StructuredResult:
    """
    Run Tesseract with the `--psm 1` layout mode to get block/line info.
    In a real engine you would get JSON directly; here we simulate it.
    """
    img = Image.open(image_path)

    # Tesseract's TSV output includes level, page_num, block_num, par_num, line_num, word_num, text…
    tsv = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT)

    result = StructuredResult()
    current_block_idx = -1
    current_line_idx = -1

    for i, level in enumerate(tsv["level"]):
        if level == 3:  # block level
            result.blocks.append(Block())
            current_block_idx += 1
            current_line_idx = -1
        elif level == 4:  # line level
            result.blocks[current_block_idx].lines.append(Line(text=""))
            current_line_idx += 1

        # level 5 is word; concatenate words into the current line
        if level == 5:
            word = tsv["text"][i]
            if word.strip():
                line_obj = result.blocks[current_block_idx].lines[current_line_idx]
                line_obj.text += (word + " ")

    # Trim trailing spaces
    for block in result.blocks:
        for line in block.lines:
            line.text = line.text.strip()
    return result
```

> **Por qué es importante:** Al preservar bloques y líneas evitamos tener que adivinar dónde comienzan los párrafos. La función `recognize_structured` nos brinda una jerarquía limpia que luego podemos alimentar a un modelo de IA.

```python
# Demo call – replace with your own image path
structured_result = recognize_structured("sample_scan.png")
print("Before AI:", structured_result.blocks[0].lines[0].text)
```

Ejecutar el fragmento imprime la primera línea exactamente como la vio el motor OCR, lo que a menudo contiene errores de reconocimiento como “0cr” en lugar de “OCR”.

## Mejorar la precisión del OCR con post‑procesamiento de IA

Ahora que tenemos la salida estructurada cruda, entregémosla a un post‑procesador de IA. El objetivo es **mejorar la precisión del OCR** corrigiendo errores comunes, normalizando la puntuación e incluso resegmentando líneas cuando sea necesario.

```python
import openai  # Example: using OpenAI's API; replace with your provider

def run_postprocessor(structured: StructuredResult) -> StructuredResult:
    """
    Sends each line to an LLM that returns a cleaned version.
    This simple loop can be parallelized for large documents.
    """
    api_key = "YOUR_OPENAI_API_KEY"
    openai.api_key = api_key

    for block in structured.blocks:
        for line in block.lines:
            prompt = (
                "You are an OCR cleanup assistant. Fix any spelling, spacing, "
                "or punctuation errors in the following line while preserving the original meaning:\n\n"
                f"\"{line.text}\""
            )
            response = openai.ChatCompletion.create(
                model="gpt-4o-mini",
                messages=[{"role": "user", "content": prompt}],
                temperature=0.0,
                max_tokens=200,
            )
            cleaned = response.choices[0].message.content.strip()
            line.text = cleaned
    return structured
```

> **Consejo profesional:** Si no tienes suscripción a un LLM, puedes reemplazar la llamada con un transformador local (p. ej., `sentence‑transformers` + un modelo de corrección afinado) o incluso con un enfoque basado en reglas. La idea clave es que la IA ve cada línea de forma aislada, lo que suele ser suficiente para **limpiar texto OCR**.

```python
# Apply the AI post‑processor
structured_result = run_postprocessor(structured_result)
print("After AI:", structured_result.blocks[0].lines[0].text)
```

Ahora deberías ver una oración mucho más limpia: errores tipográficos corregidos, espacios extra eliminados y puntuación arreglada.

## Limpiar texto OCR para mejores resultados

Incluso después de la corrección de IA, puede que quieras aplicar un paso final de sanitización: eliminar caracteres no ASCII, unificar saltos de línea y colapsar espacios múltiples. Esta pasada extra garantiza que la salida esté lista para tareas posteriores como NLP o ingestión en bases de datos.

```python
import re

def final_cleanup(structured: StructuredResult) -> str:
    """
    Flattens the hierarchy into a single string and performs
    additional regex‑based cleaning.
    """
    lines = []
    for block in structured.blocks:
        for line in block.lines:
            # Remove any lingering non‑printable characters
            cleaned = re.sub(r"[^\x20-\x7E]", "", line.text)
            # Collapse multiple spaces
            cleaned = re.sub(r"\s+", " ", cleaned).strip()
            lines.append(cleaned)
    # Join blocks with double newline to preserve paragraph breaks
    return "\n\n".join(lines)

clean_text = final_cleanup(structured_result)
print("\n=== Cleaned OCR Text ===\n")
print(clean_text)
```

La función `final_cleanup` te brinda una cadena simple que puedes alimentar directamente a un índice de búsqueda, un modelo de lenguaje o una exportación CSV. Como mantuvimos los límites de bloque, la estructura de párrafos se conserva.

## Casos límite y escenarios hipotéticos

- **Diseños de múltiples columnas:** Si tu fuente tiene columnas, el motor OCR podría entrelazar líneas. Puedes detectar las coordenadas de columna a partir de la salida TSV y reordenar las líneas antes de enviarlas a la IA.
- **Scripts no latinos:** Para idiomas como chino o árabe, cambia el prompt del LLM para solicitar corrección específica del idioma, o usa un modelo afinado en ese script.
- **Documentos grandes:** Enviar cada línea individualmente puede ser lento. Agrupa líneas (p. ej., 10 por solicitud) y permite que el LLM devuelva una lista de líneas limpias. Recuerda respetar los límites de tokens.
- **Bloques faltantes:** Algunos motores OCR devuelven solo una lista plana de palabras. En ese caso, puedes reconstruir líneas agrupando palabras con valores similares de `line_num`.

## Ejemplo completo funcional

Juntando todo, aquí tienes un archivo único que puedes ejecutar de extremo a extremo. Reemplaza los marcadores de posición con tu propia clave API y ruta de imagen.

```python
# ocr_cleanup.py
import re
import pytesseract
from PIL import Image
from dataclasses import dataclass, field
from typing import List
import openai

# ---------- Data structures ----------
@dataclass
class Line:
    text: str

@dataclass
class Block:
    lines: List[Line] = field(default_factory=list)

@dataclass
class StructuredResult:
    blocks: List[Block] = field(default_factory=list)

# ---------- Step 1: Extract OCR ----------
def recognize_structured(image_path: str) -> StructuredResult:
    img = Image.open(image_path)
    tsv = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT)

    result = StructuredResult()
    cur_block = -1
    cur_line = -1

    for i, lvl in enumerate(tsv["level"]):
        if lvl == 3:                # block
            result.blocks.append(Block())
            cur_block += 1
            cur_line = -1
        elif lvl == 4:              # line
            result.blocks[cur_block].lines.append(Line(text=""))
            cur_line += 1
        elif lvl == 5:              # word
            word = tsv["text"][i]
            if word.strip():
                result.blocks[cur_block].lines[cur_line].text += word + " "

    # Trim spaces
    for blk in result.blocks:
        for ln in blk.lines:
            ln.text = ln.text.strip()
    return result

# ---------- Step 2: AI post‑processor ----------
def run_postprocessor(structured: StructuredResult) -> StructuredResult:
    openai.api_key = "YOUR_OPENAI_API_KEY"
    for block in structured.blocks:
        for line in block.lines:
            prompt = (
                "Correct OCR errors (spelling, spacing, punctuation) in this line:\n"
                f"\"{line.text}\""
            )
            resp = openai.ChatCompletion.create(
                model="gpt-4o-mini",
                messages=[{"role": "user", "content": prompt}],
                temperature=0.0,
                max_tokens=150,
            )
            line.text = resp.choices[0].message.content.strip()
    return structured

# ---------- Step 3: Final cleanup ----------
def final_cleanup(structured: StructuredResult) -> str:
    out = []
    for block in structured.blocks:
        for line in block.lines:
            txt = re.sub(r"[^\x20-\x7E]", "", line.text)   # strip non‑ASCII
            txt = re.sub(r"\s+", " ", txt).strip

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}