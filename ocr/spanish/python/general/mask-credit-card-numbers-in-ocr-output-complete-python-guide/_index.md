---
category: general
date: 2026-04-26
description: Enmascara rápidamente los números de tarjetas de crédito usando el post‑procesamiento
  OCR de AsposeAI. Aprende sobre cumplimiento PCI, enmascaramiento con expresiones
  regulares y sanitización de datos en un tutorial paso a paso.
draft: false
keywords:
- mask credit card numbers
- PCI compliance
- OCR post‑processing
- AsposeAI
- regular expression masking
- data sanitization
language: es
og_description: Enmascara los números de tarjetas de crédito en los resultados de
  OCR con AsposeAI. Este tutorial cubre el cumplimiento PCI, el enmascaramiento mediante
  expresiones regulares y la sanitización de datos.
og_title: Enmascarar números de tarjetas de crédito – Guía completa de post‑procesamiento
  OCR en Python
tags:
- OCR
- Python
- security
title: Enmascarar números de tarjetas de crédito en la salida OCR – Guía completa
  de Python
url: /es/python/general/mask-credit-card-numbers-in-ocr-output-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Enmascarar números de tarjetas de crédito – Guía completa de Python

¿Alguna vez necesitaste **enmascarar números de tarjetas de crédito** en texto que proviene directamente de un motor OCR? No eres el único. En industrias reguladas, exponer un PAN completo (Primary Account Number) puede meterte en problemas con los auditores de cumplimiento PCI. ¿La buena noticia? Con unas pocas líneas de Python y el hook de post‑procesamiento de AsposeAI, puedes ocultar automáticamente los ocho dígitos del medio y mantenerte en el lado seguro.

En este tutorial recorreremos un escenario del mundo real: ejecutar OCR sobre una imagen de recibo y luego aplicar una función personalizada de **post‑processing OCR** que sanea cualquier dato PCI. Al final tendrás un fragmento reutilizable que puedes insertar en cualquier flujo de trabajo de AsposeAI, además de varios consejos prácticos para manejar casos límite y escalar la solución.

## Lo que aprenderás

- Cómo registrar un post‑processor personalizado con **AsposeAI**.  
- Por qué un enfoque de **enmascaramiento con expresiones regulares** es rápido y fiable.  
- Los conceptos básicos de **cumplimiento PCI** relacionados con la sanitización de datos.  
- Formas de extender el patrón para múltiples formatos de tarjetas o números internacionales.  
- Salida esperada y cómo verificar que el enmascaramiento funcionó.

> **Requisitos previos** – Debes contar con un entorno Python 3 funcional, el paquete Aspose.AI for OCR instalado (`pip install aspose-ocr`), y una imagen de muestra (p. ej., `receipt.png`) que contenga un número de tarjeta de crédito. No se requieren otros servicios externos.

---

## Paso 1: Definir un post‑processor que enmascare números de tarjetas de crédito

El corazón de la solución vive en una pequeña función que recibe el resultado del OCR, ejecuta una rutina de **enmascaramiento con expresiones regulares** y devuelve el texto saneado.

```python
def mask_pci(data, settings):
    """
    Replace the middle 8 digits of any 16‑digit card number with asterisks.
    Keeps the first and last four digits visible for reference.
    """
    import re
    # Pattern captures groups: first 4 digits, middle 8, last 4
    pattern = r'(\d{4})\d{8}(\d{4})'
    # Replace middle portion with ****
    return re.sub(pattern, r'\1****\2', data.text)
```

**Por qué funciona esto:**  
- La expresión regular `(\d{4})\d{8}(\d{4})` coincide exactamente con 16 dígitos consecutivos, el formato común para Visa, MasterCard y muchas otras.  
- Al capturar los primeros y últimos cuatro dígitos (`\1` y `\2`) conservamos suficiente información para depuración mientras cumplimos con las reglas de **cumplimiento PCI** que prohíben almacenar el PAN completo.  
- La sustitución `\1****\2` oculta los ocho dígitos sensibles del medio, convirtiendo `1234567812345678` en `1234****5678`.

> **Consejo profesional:** Si necesitas soportar números American Express de 15 dígitos, añade un segundo patrón como `r'(\d{4})\d{6}(\d{5})'` y ejecuta ambas sustituciones secuencialmente.

---

## Paso 2: Inicializar el motor AsposeAI

Antes de poder adjuntar nuestro post‑processor, necesitamos una instancia del motor OCR. AsposeAI incluye el modelo OCR y una API sencilla para procesamiento personalizado.

```python
from aspose.ocr import AsposeAI

# Initialise the AI engine – it will handle image loading, recognition, and post‑processing
ai = AsposeAI()
```

**¿Por qué inicializar aquí?**  
Crear el objeto `AsposeAI` una sola vez y reutilizarlo en múltiples imágenes reduce la sobrecarga. El motor también almacena en caché los modelos de idioma, lo que acelera llamadas posteriores—útil cuando escaneas lotes de recibos.

---

## Paso 3: Registrar la función de enmascaramiento personalizada

AsposeAI expone un método `set_post_processor` que permite conectar cualquier callable. Pasamos nuestra función `mask_pci` junto con un diccionario de configuraciones opcional (vacío por ahora).

```python
# Register our masking routine; custom_settings can hold flags like "log_masked" if you expand later
ai.set_post_processor(mask_pci, custom_settings={})
```

**¿Qué ocurre tras bambalinas?**  
Cuando más adelante invoques `run_postprocessor`, AsposeAI entregará el resultado bruto del OCR a `mask_pci`. La función recibe un objeto ligero (`data`) que contiene el texto reconocido, y tú devuelves una nueva cadena. Este diseño mantiene el OCR central intacto mientras te permite aplicar políticas de **sanitización de datos** en un solo lugar.

---

## Paso 4: Ejecutar OCR sobre la imagen del recibo

Ahora que el motor sabe cómo limpiar la salida, le pasamos una imagen. Para este tutorial asumimos que ya dispones de un objeto `engine` configurado con el idioma y la resolución adecuados.

```python
# Assume `engine` is a pre‑configured OCR object (e.g., with language='en')
ocr_engine = engine
raw_result = ocr_engine.recognize_image("receipt.png")
```

**Consejo:** Si no tienes un objeto preconfigurado, puedes crear uno con:

```python
from aspose.ocr import OcrEngine
ocr_engine = OcrEngine(language='en')
```

La llamada `recognize_image` devuelve un objeto cuyo atributo `text` contiene la cadena cruda, sin enmascarar.

---

## Paso 5: Aplicar el post‑processor registrado

Con los datos OCR sin procesar en mano, los entregamos a la instancia de IA. El motor ejecuta automáticamente la función `mask_pci` que registramos anteriormente.

```python
# This triggers the post‑processor and returns a new result object
final_result = ai.run_postprocessor(raw_result)
```

**¿Por qué usar `run_postprocessor` en lugar de llamar a la función manualmente?**  
Hacerlo mantiene el flujo de trabajo coherente, especialmente cuando tienes varios post‑processors (p. ej., corrección ortográfica, detección de idioma). AsposeAI los encola en el orden en que los registras, garantizando una salida determinista.

---

## Paso 6: Verificar la salida saneada

Finalmente, imprimamos el texto saneado y confirmemos que cualquier número de tarjeta de crédito está correctamente enmascarado.

```python
print(final_result.text)
```

**Salida esperada** (extracto):

```
Purchase at Café Latte – Total: $4.75
Card: 1234****5678
Date: 2026-04-25
Thank you!
```

Si el recibo no contenía número de tarjeta, el texto permanece sin cambios—nada que enmascarar, nada de qué preocuparse.

---

## Manejo de casos límite y variaciones comunes

### Múltiples números de tarjeta en un mismo documento
Si un recibo incluye más de un PAN (p. ej., una tarjeta de fidelidad más una tarjeta de pago), la expresión regular se ejecuta globalmente, enmascarando todas las coincidencias automáticamente. No se necesita código adicional.

### Formato no estándar
A veces el OCR inserta espacios o guiones (`1234 5678 1234 5678` o `1234-5678-1234-5678`). Amplía el patrón para ignorar esos caracteres:

```python
pattern = r'(\d{4})[ -]?\d{4}[ -]?\d{4}[ -]?\d{4}'
```

El añadido `[ -]?` tolera espacios o guiones opcionales entre bloques de dígitos.

### Tarjetas internacionales
Para PAN de 19 dígitos usados en algunas regiones, puedes ampliar el patrón:

```python
pattern = r'(\d{4})\d{11,15}(\d{4})'
```

Solo recuerda que **cumplimiento PCI** sigue exigiendo enmascarar los dígitos del medio, sin importar la longitud.

### Registro de valores enmascarados (opcional)
Si necesitas auditorías, pasa una bandera mediante `custom_settings` y ajusta la función:

```python
def mask_pci(data, settings):
    import re, logging
    pattern = r'(\d{4})\d{8}(\d{4})'
    def repl(match):
        masked = f"{match.group(1)}****{match.group(2)}"
        if settings.get('log'):
            logging.info(f"Masked PAN: {masked}")
        return masked
    return re.sub(pattern, repl, data.text)
```

Luego regístrala con:

```python
ai.set_post_processor(mask_pci, custom_settings={'log': True})
```

---

## Ejemplo completo listo para copiar y pegar

```python
# ------------------------------------------------------------
# Mask Credit Card Numbers in OCR Output – Complete Example
# ------------------------------------------------------------
import re
from aspose.ocr import AsposeAI, OcrEngine

# 1️⃣ Define the post‑processor
def mask_pci(data, settings):
    """
    Hide the middle eight digits of any 16‑digit credit‑card number.
    """
    pattern = r'(\d{4})\d{8}(\d{4})'          # keep first & last 4 digits
    return re.sub(pattern, r'\1****\2', data.text)

# 2️⃣ Initialise the OCR engine and AsposeAI wrapper
ocr_engine = OcrEngine(language='en')       # configure as needed
ai = AsposeAI()

# 3️⃣ Register the masking function
ai.set_post_processor(mask_pci, custom_settings={})

# 4️⃣ Run OCR on a sample receipt
raw_result = ocr_engine.recognize_image("receipt.png")

# 5️⃣ Apply post‑processing (masking)
final_result = ai.run_postprocessor(raw_result)

# 6️⃣ Display sanitized text
print("Sanitized OCR output:")
print(final_result.text)
```

Ejecutar este script sobre un recibo que contenga `4111111111111111` producirá:

```
Sanitized OCR output:
Purchase at Bookstore – $12.99
Card: 4111****1111
Date: 2026-04-26
```

Ese es todo el pipeline—desde OCR crudo hasta **sanitización de datos**—envuelto en unas pocas líneas limpias de Python.

---

## Conclusión

Acabamos de mostrarte cómo **enmascarar números de tarjetas de crédito** en resultados OCR usando el hook de post‑processing de AsposeAI, una rutina concisa de expresiones regulares y varios consejos de mejores prácticas para **cumplimiento PCI**. La solución es totalmente autónoma, funciona con cualquier imagen que el motor OCR pueda leer y puede ampliarse para cubrir formatos de tarjeta más complejos o requisitos de registro.

¿Listo para el siguiente paso? Prueba combinar este enmascarado con una rutina de **inserción en base de datos** que almacene solo los últimos cuatro dígitos como referencia, o integra un **procesador por lotes** que escanee una carpeta completa de recibos durante la noche. También podrías explorar otras tareas de **post‑processing OCR** como la estandarización de direcciones o la detección de idioma—cada una sigue el mismo patrón que usamos aquí.

¿Tienes preguntas sobre casos límite, rendimiento o cómo adaptar el código a otra biblioteca OCR? Deja un comentario abajo y mantengamos la conversación. ¡Feliz codificación y mantente seguro!  

![Diagram illustrating how mask credit card numbers works in an OCR pipeline](https://example.com/images/ocr-mask-flow.png "Diagram of OCR post‑processing masking flow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}