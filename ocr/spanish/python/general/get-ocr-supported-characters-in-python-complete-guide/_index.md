---
category: general
date: 2026-06-25
description: Obtén rápidamente los caracteres compatibles con OCR usando la biblioteca
  aocr. Aprende cómo listar los caracteres OCR, configurar los idiomas y depurar tu
  motor OCR en Python.
draft: false
keywords:
- get OCR supported characters
- OCR engine Python
- list OCR characters
- supported OCR languages
- aocr library
language: es
og_description: Obtén los caracteres compatibles con OCR usando aocr. Esta guía te
  muestra cómo listar los caracteres OCR, elegir idiomas y manejar casos especiales
  en Python.
og_title: Obtén los caracteres compatibles con OCR en Python – Tutorial completo
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  headline: Get OCR Supported Characters in Python – Complete Guide
  type: TechArticle
- description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  name: Get OCR Supported Characters in Python – Complete Guide
  steps:
  - name: What if the language pack is missing?
    text: 'If you request a language that isn’t bundled, `aocr.Language` won’t contain
      the enum, and you’ll hit an `AttributeError`. Guard against this with a simple
      check:'
  - name: Empty character list
    text: 'Some niche languages might return an empty list if the underlying training
      data is incomplete. In that scenario, you can fall back to a default (e.g.,
      English) or raise a warning:'
  - name: Unicode normalization
    text: 'The list may contain combined characters (e.g., “é” as `e` + acute accent).
      If your downstream processing expects pre‑composed glyphs, run a normalization
      step:'
  type: HowTo
- questions:
  - answer: Yes, the `get_supported_characters()` method is stable across 1.x and
      2.x. The only change is that language enums were moved to `aocr.languages`.
    question: Does this work with aocr version 2.x?
  - answer: 'Absolutely. Use `ord(ch)` inside a list comprehension: ```python code_points
      = [hex(ord(ch)) for ch in supported_chars] ```'
    question: Can I get the Unicode code point for each character?
  - answer: 'aocr includes an `ARABIC` enum. The character list will contain Arabic
      glyphs, but you may need to enable RTL rendering in your downstream UI. ---
      ## Conclusion You now know **how to get OCR supported characters** using the
      aocr library in Python, how to switch between **supported OCR languages**, a'
    question: What about right‑to‑left scripts like Arabic?
  type: FAQPage
tags:
- OCR
- Python
- aocr
title: Obtén los caracteres compatibles con OCR en Python – Guía completa
url: /es/python/general/get-ocr-supported-characters-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Obtén los caracteres compatibles con OCR en Python – Guía completa

¿Alguna vez te has preguntado cómo **obtener los caracteres compatibles con OCR** para un idioma específico mientras juegas con un motor OCR? No estás solo. Ya sea que estés construyendo un escáner de recibos o un analizador de documentos multilingüe, saber exactamente qué glifos puede reconocer tu motor es una salvación. En este tutorial recorreremos todo el proceso: instalar la biblioteca, configurar el idioma y, finalmente, listar esos caracteres, para que puedas depurar y afinar tu canalización OCR en minutos.

Usaremos la biblioteca **aocr**, un motor OCR ligero para Python que hace que consultar las capacidades de idioma sea sencillo. Al final de esta guía podrás **listar los caracteres OCR**, cambiar entre **idiomas OCR compatibles** e incluso detectar brechas en la cobertura antes de que te afecten en producción.

---

## Requisitos previos

Antes de comenzar, asegúrate de tener:

* Python 3.8 o superior (el paquete aocr deja de soportar 3.7)
* Una terminal o símbolo del sistema con acceso a internet
* Familiaridad básica con scripting en Python (si has escrito un `print()` antes, estás listo)

No hay dependencias externas pesadas—solo el paquete `aocr` de pip.

---

## Instala la biblioteca aocr (Motor OCR Python)

Lo primero que necesitas es una instalación funcional de **OCR engine Python**. El paquete aocr está disponible en PyPI, así que un solo comando pip hace el trabajo:

```bash
pip install aocr
```

Si estás usando un entorno virtual (altamente recomendado), actívalo primero:

```bash
python -m venv .venv
source .venv/bin/activate   # macOS/Linux
.\.venv\Scripts\activate    # Windows
```

> **Consejo profesional:** fija la versión (`pip install aocr==1.2.4`) para evitar cambios inesperados en la API más adelante.

---

## Elige un idioma (Idiomas OCR compatibles)

aocr incluye un puñado de paquetes de idioma integrados. Cada paquete define el conjunto de puntos de código Unicode que el motor puede reconocer. Para consultar esos paquetes deberás establecer el atributo `language` en la instancia del motor.

```python
import aocr

# Create the OCR engine instance
ocr_engine = aocr.OcrEngine()

# Pick the language you care about – here we use English
ocr_engine.language = aocr.Language.ENGLISH
```

Puedes reemplazar `aocr.Language.ENGLISH` por cualquier otro valor enum (`FRENCH`, `GERMAN`, etc.). Si intentas asignar un idioma que no está incluido, aocr lanza un `ValueError`. Por eso es buena idea revisar primero la lista de **idiomas OCR compatibles**:

```python
print("Available languages:", [lang.name for lang in aocr.Language])
```

---

## Recupera el conjunto de caracteres (Obtener caracteres compatibles con OCR)

Ahora llega el corazón del tutorial: realmente **obtener los caracteres compatibles con OCR**. El motor expone un método práctico llamado `get_supported_characters()` que devuelve una lista de cadenas de un solo carácter.

```python
# Step 3: Retrieve the set of characters that the engine can recognize
supported_chars = ocr_engine.get_supported_characters()
```

Detrás de escena, aocr lee un archivo JSON incluido con el paquete de idioma y convierte cada punto de código Unicode en una cadena de Python. El resultado es determinista, lo que significa que obtendrás la misma lista cada vez que ejecutes el script con la misma versión de idioma.

---

## Muestra cuántos caracteres son compatibles

Conocer el recuento te ayuda a medir rápidamente la amplitud de la cobertura. Para inglés, típicamente verás unos pocos miles de caracteres (incluyendo puntuación y dígitos).

```python
# Step 4: Show how many characters are supported
print(f"{len(supported_chars)} characters supported for ENGLISH:")
```

La llamada `len()` es O(1) porque Python almacena la longitud de la lista internamente, por lo que no hay penalización de rendimiento incluso para alfabetos grandes.

---

## Vista previa de los primeros 100 caracteres compatibles

Una verificación visual rápida puede revelar si el motor incluye los símbolos que necesitas (piensa en el signo de euro o comillas tipográficas). Imprimamos los primeros cien caracteres:

```python
# Step 5: Preview the first 100 supported characters
print("".join(supported_chars[:100]), "...")
```

La operación `join` concatena la porción en una única cadena, lo que es más legible que imprimir una lista de Python.

---

## Script completo – Todos los pasos en un solo lugar

A continuación tienes el ejemplo completo y ejecutable que une todo. Guárdalo como `list_supported_chars.py` y ejecuta `python list_supported_chars.py` desde tu terminal.

```python
# list_supported_chars.py
"""
Complete example showing how to get OCR supported characters
using the aocr library in Python.
"""

import aocr

def main():
    # 1️⃣ Create an OCR engine instance
    ocr_engine = aocr.OcrEngine()

    # 2️⃣ Select the language you want to work with (e.g., English)
    # You can change this to any language supported by aocr.
    ocr_engine.language = aocr.Language.ENGLISH

    # 3️⃣ Retrieve the set of characters that the engine can recognize
    supported_chars = ocr_engine.get_supported_characters()

    # 4️⃣ Show how many characters are supported
    print(f"{len(supported_chars)} characters supported for ENGLISH:")

    # 5️⃣ Preview the first 100 supported characters
    preview = "".join(supported_chars[:100])
    print(preview, "...")

if __name__ == "__main__":
    main()
```

**Salida esperada (truncada por brevedad):**

```
2565 characters supported for ENGLISH:
ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789.,!?'"()[]{}-+*/%$#@&... 
```

El recuento exacto puede variar ligeramente según la versión de aocr, pero siempre verás un alfabeto extenso más la puntuación común.

---

## Manejo de casos límite

### ¿Qué pasa si falta el paquete de idioma?

Si solicitas un idioma que no está incluido, `aocr.Language` no contendrá el enum y obtendrás un `AttributeError`. Protege tu código con una verificación simple:

```python
if hasattr(aocr.Language, "SPANISH"):
    ocr_engine.language = aocr.Language.SPANISH
else:
    raise RuntimeError("Spanish language pack not installed.")
```

### Lista de caracteres vacía

Algunos idiomas poco comunes pueden devolver una lista vacía si los datos de entrenamiento subyacentes están incompletos. En ese caso, puedes recurrir a un valor predeterminado (p. ej., inglés) o lanzar una advertencia:

```python
if not supported_chars:
    print("Warning: No characters returned for the selected language.")
```

### Normalización Unicode

La lista puede contener caracteres combinados (p. ej., “é” como `e` + acento agudo). Si tu procesamiento posterior espera glifos precompuestos, ejecuta un paso de normalización:

```python
import unicodedata
normalized = [unicodedata.normalize("NFC", ch) for ch in supported_chars]
```

---

## Consejos profesionales para proyectos del mundo real

* **Cachea la lista de caracteres** – Si procesas miles de imágenes, llamar a `get_supported_characters()` en cada iteración añade una sobrecarga innecesaria. Guarda la lista en una variable a nivel de módulo o serialízala a JSON para reutilizarla después.
* **Validación cruzada de idiomas** – Cuando soportas varios idiomas en una sola aplicación, intersecta los conjuntos de caracteres para encontrar un subconjunto común. Esto te ayuda a diseñar elementos UI que permanezcan consistentes entre distintas configuraciones regionales.
* **Depuración de fallos OCR** – Si el motor clasifica incorrectamente un glifo, compara el carácter problemático con la salida de `list_supported_chars`. Si falta, has identificado una brecha de cobertura que puede requerir un entrenamiento personalizado.
* **Combina con fuentes personalizadas** – aocr respeta el rango Unicode, pero la calidad de renderizado puede variar según la fuente. Prueba tus caracteres compatibles con la fuente exacta que usarás en producción para evitar sorpresas.

---

## Preguntas frecuentes

**P: ¿Esto funciona con la versión 2.x de aocr?**  
R: Sí, el método `get_supported_characters()` es estable en 1.x y 2.x. El único cambio es que los enums de idioma se movieron a `aocr.languages`.

**P: ¿Puedo obtener el punto de código Unicode de cada carácter?**  
R: Por supuesto. Usa `ord(ch)` dentro de una comprensión de listas:

```python
code_points = [hex(ord(ch)) for ch in supported_chars]
```

**P: ¿Qué pasa con los scripts de derecha a izquierda como el árabe?**  
R: aocr incluye un enum `ARABIC`. La lista de caracteres contendrá glifos árabes, pero puede que necesites habilitar el renderizado RTL en tu UI posterior.

---

## Conclusión

Ahora sabes **cómo obtener los caracteres compatibles con OCR** usando la biblioteca aocr en Python, cómo cambiar entre **idiomas OCR compatibles** y por qué **listar los caracteres OCR** es esencial para canalizaciones de reconocimiento de texto robustas. Con el script completo y los consejos anteriores, puedes verificar rápidamente la cobertura de idioma, depurar glifos faltantes y crear aplicaciones OCR más inteligentes.

¿Listo para el siguiente paso? Prueba combinar esta lista de caracteres con un filtro de lista de palabras personalizado, o experimenta con otro motor OCR (Tesseract, EasyOCR) y compara los resultados. Cuanto más explores, mejores serán tus soluciones OCR.

¡Feliz codificación, y que tus conjuntos de caracteres estén siempre completos!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Especificar caracteres permitidos OCR – Usando Aspose.OCR para .NET](/ocr/english/net/ocr-settings/specify-allowed-characters/)
- [Cómo OCR texto de imagen con idioma usando Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Post‑procesamiento OCR – Obtener opciones de caracteres](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}