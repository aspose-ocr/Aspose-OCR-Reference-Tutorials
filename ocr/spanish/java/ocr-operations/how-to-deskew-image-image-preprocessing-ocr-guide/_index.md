---
category: general
date: 2026-06-22
description: 'Cómo corregir la inclinación de la imagen para OCR: aprende los pasos
  de preprocesamiento de imágenes para OCR, elimina el ruido de sal y pimienta y mejora
  la precisión.'
draft: false
keywords:
- how to deskew image
- image preprocessing ocr
- remove salt pepper
- preprocess images OCR
language: es
og_description: Cómo corregir la inclinación de una imagen para OCR, eliminar el ruido
  de sal y pimienta y aplicar técnicas de preprocesamiento de imágenes OCR en un ejemplo
  completo en Java.
og_title: Cómo corregir la inclinación de una imagen – Guía de preprocesamiento de
  imágenes para OCR
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: 'How to deskew image for OCR: learn image preprocessing OCR steps,
    remove salt pepper noise, and boost accuracy.'
  headline: How to Deskew Image – Image Preprocessing OCR Guide
  type: TechArticle
tags:
- OCR
- image-processing
- Java
title: Cómo enderezar la imagen – Guía de preprocesamiento de imágenes para OCR
url: /es/java/ocr-operations/how-to-deskew-image-image-preprocessing-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo enderezar una imagen – Guía de preprocesamiento de imágenes OCR

¿Alguna vez te has preguntado **cómo enderezar una imagen** para que tu motor OCR realmente lea el texto? No eres el único. Un escaneo inclinado puede convertir un documento perfecto en un desastre confuso, y la mayoría de los desarrolladores se topan con ese problema al menos una vez.

En este tutorial recorreremos una canalización completa de **image preprocessing OCR** que no solo corrige la rotación sino que también **elimina** artefactos de *salt‑pepper* y aumenta el contraste—básicamente todo lo que necesitas para **preprocess images OCR**‑style antes de enviarlas al motor. Al final tendrás un fragmento de Java listo para ejecutar y un modelo mental claro de por qué cada paso es importante.

## Cómo enderezar una imagen – Construyendo la canalización de preprocesamiento

El corazón de cualquier flujo de trabajo amigable con OCR es un objeto **preprocess options** que encadena una serie de filtros. Piensa en él como una cinta transportadora: cada filtro realiza una tarea y luego pasa la imagen al siguiente. A continuación se muestra un ejemplo mínimo pero completo usando una biblioteca OCR hipotética que incluye `DeskewFilter`, `DenoiseFilter` y `ContrastBoostFilter`.

```java
import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.DeskewFilter;
import com.example.ocr.filters.DenoiseFilter;
import com.example.ocr.filters.ContrastBoostFilter;

/**
 * Demonstrates how to deskew image and apply common OCR preprocessing steps.
 */
public class OcrPreprocessDemo {

    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine (replace with your actual implementation)
        Engine engine = new Engine();

        // 2️⃣ Build the preprocessing pipeline
        ImagePreprocessOptions preprocessOptions = new ImagePreprocessOptions();

        // 2a️⃣ Deskew – correct rotation up to ±15°
        preprocessOptions.addFilter(new DeskewFilter(15));

        // 2b️⃣ Denoise – remove salt‑and‑pepper noise
        preprocessOptions.addFilter(new DenoiseFilter());

        // 2c️⃣ Contrast boost – make low‑contrast scans more readable
        preprocessOptions.addFilter(new ContrastBoostFilter(1.5f));

        // 3️⃣ Attach the pipeline to the engine
        engine.setPreprocessOptions(preprocessOptions);

        // 4️⃣ Run OCR on a sample image
        String result = engine.recognizeText("sample-scanned-page.png");

        // 5️⃣ Output the recognized text
        System.out.println("=== OCR RESULT ===");
        System.out.println(result);
    }
}
```

### Por qué esto funciona

* **DeskewFilter** analiza las líneas de texto dominantes de la imagen, estima el ángulo y rota el bitmap de vuelta a la horizontal. La mayoría de las bibliotecas limitan la corrección a ±15° porque ángulos mayores suelen indicar una página escaneada mal que necesita intervención manual.
* **DenoiseFilter** apunta al patrón clásico de *salt‑and‑pepper*—esos píxeles negros o blancos aislados que parecen estática en una TV. Eliminarlos evita que el motor OCR confunda el ruido con caracteres.
* **ContrastBoostFilter** estira el histograma, haciendo que los trazos tenues resalten. Un multiplicador de `1.5f` es un valor predeterminado seguro; puedes aumentarlo si tus escaneos están especialmente deslavados.

> **Consejo profesional:** Si sabes que tus documentos nunca superan una inclinación de 10°, pasa ese límite menor a `DeskewFilter`—el algoritmo se ejecuta más rápido y es menos probable que sobre‑corrija.

## Image Preprocessing OCR: Añadiendo filtros en el orden correcto

El orden importa. Imagina que eliminas el ruido *antes* de enderezar; el ruido podría alterar la detección del ángulo, provocando un resultado desalineado. Por el contrario, aplicar el aumento de contraste *después* de enderezar garantiza que la rotación no introduzca nuevos artefactos.

A continuación tienes una lista de verificación rápida que puedes copiar y pegar en cualquier proyecto:

| Paso | Filtro | Razón |
|------|--------|--------|
| 1 | `DeskewFilter` | Alinea la línea base del texto |
| 2 | `DenoiseFilter` | Elimina el ruido de píxeles aislados |
| 3 | `ContrastBoostFilter` | Mejora la legibilidad para OCR |

Si necesitas insertar pasos adicionales—por ejemplo, un filtro de **binarización** para OCR binario—lo colocarías **después** del aumento de contraste, porque una imagen limpia y de alto contraste se binariza con mayor precisión.

## Eliminar ruido de sal y pimienta con DenoiseFilter

El ruido de *salt‑and‑pepper* es notorio en escaneos de baja calidad, especialmente los provenientes de cámaras de teléfonos baratos. El `DenoiseFilter` de nuestra biblioteca implementa un kernel de filtro mediano, que reemplaza cada píxel por la mediana de su vecindario circundante. ¿El efecto? esas manchas desaparecen sin difuminar los caracteres reales.

```java
// Example: customizing the median kernel size (default is 3x3)
preprocessOptions.addFilter(new DenoiseFilter(5)); // 5x5 kernel for heavy noise
```

*¿Cuándo aumentar el tamaño del kernel?* Si tus imágenes de origen están plagadas de manchas grandes, un kernel más grande las limpiará, pero ten cuidado: si es demasiado grande podrías empezar a borrar trazos finos en fuentes diminutas.

## Preprocess Images OCR – Aplicando la canalización

Una vez que has ensamblado la cadena de filtros, adjuntarla al motor es una sola línea (`engine.setPreprocessOptions`). Desde ese momento, cada llamada a `recognizeText` se ejecuta automáticamente a través de la canalización. No es necesario invocar manualmente cada filtro—tu código se mantiene ordenado, y los cambios futuros (añadir un nuevo filtro, ajustar parámetros) están centralizados.

Así es como se ve una ejecución exitosa con un escaneo de muestra que originalmente tenía una inclinación de 12° y ruido de pimienta notable:

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

Observa cómo el texto está limpio, correctamente orientado y libre de caracteres errantes que de otro modo aparecerían como “I n v o i c e” o “$‑‑‑”.

## Casos límite y errores comunes

| Situación | Qué observar | Solución sugerida |
|-----------|--------------|-------------------|
| Rotación > 15° | DeskewFilter puede abandonar | Pre‑rotar manualmente o usar un filtro de rango mayor |
| Resolución extremadamente baja ( < 100 dpi ) | El aumento de contraste no puede recuperar detalles | Remuestrear la imagen primero (p. ej., `ResampleFilter`) |
| Ruido mixto (Gaussiano + sal‑pimienta) | DenoiseFilter solo no es suficiente | Encadenar un `GaussianBlurFilter` antes de `DenoiseFilter` |
| Escaneos en color con texto coloreado | Necesaria conversión a escala de grises | Insertar `GrayscaleFilter` antes del aumento de contraste |

Al anticipar estos escenarios te ahorras horas de depuración más adelante.

## Ejemplo completo y funcional (Todo‑en‑uno)

A continuación tienes una clase Java autónoma que puedes agregar a cualquier proyecto Maven o Gradle que incluya la dependencia `com.example.ocr`. Demuestra **cómo enderezar una imagen**, **eliminar ruido de sal y pimienta**, y **preprocess images OCR**‑style.

```java
package com.myapp.demo;

import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.*;

public class CompleteOcrPipeline {

    public static void main(String[] args) {
        // -------------------------------------------------
        // 1️⃣ Initialise OCR engine (replace with your own)
        // -------------------------------------------------
        Engine engine = new Engine();

        // -------------------------------------------------
        // 2️⃣ Configure preprocessing pipeline
        // -------------------------------------------------
        ImagePreprocessOptions options = new ImagePreprocessOptions();

        // Deskew up to ±15° – the core of "how to deskew image"
        options.addFilter(new DeskewFilter(15));

        // Remove salt‑and‑pepper artifacts
        options.addFilter(new DenoiseFilter());

        // Boost contrast by 1.5× to aid OCR recognition
        options.addFilter(new ContrastBoostFilter(1.5f));

        // (Optional) Convert to grayscale – often improves OCR accuracy
        options.addFilter(new GrayscaleFilter());

        // Attach the pipeline
        engine.setPreprocessOptions(options);

        // -------------------------------------------------
        // 3️⃣ Perform OCR on a test file
        // -------------------------------------------------
        String imagePath = "src/main/resources/scanned-document.png";
        String text = engine.recognizeText(imagePath);

        // -------------------------------------------------
        // 4️⃣ Show the result
        // -------------------------------------------------
        System.out.println("=== OCR RESULT ===");
        System.out.println(text);
    }
}
```

**Salida esperada** (asumiendo que `scanned-document.png` contiene una factura clara):

```
=== OCR RESULT ===
Invoice #98765
Date: 2024‑02‑28
Amount Due: $2,340.75
Please remit payment within 30 days.
```

Si sustituyes la imagen por una que ya está perfectamente alineada, notarás que la canalización sigue ejecutándose—nada se rompe y la precisión del OCR se mantiene alta.

## Conclusión

Ahora tienes una comprensión sólida de **cómo enderezar una imagen** y por qué cada paso de preprocesamiento—**image preprocessing OCR**, **remove salt pepper**, y **preprocess images OCR**—desempeña un papel crucial en la entrega de texto limpio y buscable. El ejemplo anterior es completo,

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo usar AspOCR: filtros de preprocesamiento de imagen OCR para .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Calcular ángulo de sesgo para preprocesamiento de imagen OCR](/ocr/english/net/skew-angle-calculation/calculate-skew-angle/)
- [Cómo establecer el valor de umbral en reconocimiento de imagen OCR](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}