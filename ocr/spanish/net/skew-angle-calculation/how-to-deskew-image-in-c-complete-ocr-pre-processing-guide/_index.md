---
category: general
date: 2026-01-10
description: Cómo corregir la inclinación de una imagen y mejorar los resultados de
  OCR con Aspose.OCR. Aprende a preprocesar la imagen para OCR, eliminar el ruido
  del escaneo y reconocer texto del escaneo.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- recognize text from scan
- how to use ocr
- remove noise from scan
language: es
og_description: Cómo enderezar la imagen y mejorar la precisión del OCR. Esta guía
  muestra cómo preprocesar la imagen para OCR, eliminar el ruido del escaneo y reconocer
  el texto del escaneo usando Aspose.OCR.
og_title: Cómo desinclinar una imagen en C# – Guía completa de preprocesamiento OCR
tags:
- OCR
- C#
- Image Processing
title: Cómo corregir la inclinación de una imagen en C# – Guía completa de preprocesamiento
  OCR
url: /es/net/skew-angle-calculation/how-to-deskew-image-in-c-complete-ocr-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo enderezar una imagen en C# – Guía completa de pre‑procesamiento OCR

¿Alguna vez te has preguntado **cómo enderezar una imagen** antes de enviarla a un motor OCR? No eres el único. Los documentos escaneados a menudo están torcidos, ruidosos o con bajo contraste, y eso complica cualquier intento de reconocimiento de texto.  

En este tutorial recorreremos un ejemplo completo y ejecutable que **preprocesa la imagen para OCR**, elimina el ruido del escaneo y, finalmente, **reconoce texto del escaneo** usando la biblioteca Aspose.OCR. Al final tendrás una visión clara de **cómo usar OCR** en C# manteniendo el código breve y sencillo.

> **Consejo profesional:** Incluso una pequeña rotación (5‑10°) puede reducir la precisión del OCR en un 30 % o más. Enderezar la imagen es el primer paso que nunca debes omitir.

---

## Lo que necesitarás

- **.NET 6+** (el código funciona también en .NET Framework, pero .NET 6 es la LTS actual)
- **Aspose.OCR para .NET** – puedes obtenerlo desde NuGet (`Install-Package Aspose.OCR`)
- Un archivo de muestra TIFF/PNG/JPEG que esté rotado o ruidoso (usaremos `noisy_rotated.tif` en el ejemplo)
- Cualquier IDE que prefieras – Visual Studio, Rider o VS Code sirven

Eso es todo. Sin bibliotecas adicionales, sin servicios externos.

---

## Paso 1 – Cargar la imagen fuente (por qué importa)

Antes de poder **enderezar la imagen**, necesitamos leerla en un `ImageStream` de Aspose. Este objeto abstrae la entrada/salida de archivos y le brinda al motor OCR una interfaz consistente.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Load the original scan – replace the path with your own file
var sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/noisy_rotated.tif");

// Quick sanity check – make sure the image loaded
if (sourceImage == null)
{
    Console.WriteLine("Failed to load the image. Check the path and file permissions.");
    return;
}
```

*¿Por qué cargar primero?* Porque todos los filtros posteriores operan sobre una imagen en memoria. Si el archivo no se puede leer, toda la cadena se colapsa.

---

## Paso 2 – Construir una canalización de pre‑procesamiento (Enderezar + Desruido + Contraste)

Un flujo de trabajo OCR robusto suele encadenar varios filtros. Aquí es donde **preprocesamos la imagen para OCR** y, lo que es más importante, **cómo enderezar la imagen** automáticamente.

```csharp
// Create a pipeline that will run three filters in order
var preprocessPipeline = new PreprocessPipeline()
{
    // 1️⃣ DeskewFilter – detects rotation up to 30° and corrects it
    new DeskewFilter { MaxAngle = 30 },

    // 2️⃣ DenoiseFilter – smooths out speckles while keeping edges
    new DenoiseFilter { Strength = 0.8 },

    // 3️⃣ ContrastBoostFilter – makes faint characters pop
    new ContrastBoostFilter { Level = 1.3 }
};
```

**¿Por qué estos tres?**  
- **DeskewFilter** resuelve automáticamente el problema de “cómo enderezar la imagen”; no necesitas adivinar el ángulo.  
- **DenoiseFilter** aborda el requisito de “eliminar ruido del escaneo”, que de otro modo crea caracteres fantasma.  
- **ContrastBoostFilter** ayuda al motor OCR a distinguir texto oscuro de un fondo claro, un problema clásico cuando *preprocesas la imagen para OCR*.

---

## Paso 3 – Aplicar la canalización (Viendo la transformación)

Ahora ejecutamos realmente los filtros. La `processedImage` devuelta es lo que alimentaremos al motor OCR.

```csharp
// Apply all filters – the result is a cleaned‑up bitmap
var processedImage = preprocessPipeline.Apply(sourceImage);

// Optional: Save the cleaned image for visual verification
processedImage.Save("cleaned_output.tif");
Console.WriteLine("Image preprocessing complete – cleaned_output.tif saved.");
```

Si abres `cleaned_output.tif`, deberías notar que el texto está recto, menos granuloso y con mayor contraste. Esta verificación visual es útil cuando *eliminás ruido del escaneo* y quieres confirmar que el enderezado funcionó.

---

## Paso 4 – Crear y configurar el motor OCR (Cómo usar OCR)

Con una imagen ordenada en mano, instanciamos `OcrEngine`. Este es el núcleo de **cómo usar OCR** con Aspose.

```csharp
// Initialize the OCR engine
var ocrEngine = new OcrEngine
{
    // Assign the pre‑processed image
    Image = processedImage,

    // Optional: Set language (English is default)
    // Language = Language.English,
    
    // Enable automatic page segmentation (helps with multi‑column scans)
    AutoPageSegmentation = true
};
```

*¿Por qué establecer `AutoPageSegmentation`?* Porque muchos escaneos contienen tablas o múltiples columnas. Activarlo permite que el motor divida la página de forma inteligente, mejorando el resultado final de **reconocer texto del escaneo**.

---

## Paso 5 – Ejecutar el proceso de reconocimiento (Finalmente reconocer texto)

Ahora llega el momento de la verdad: le pedimos al motor que lea el texto.

```csharp
// Kick off the OCR process
ocrEngine.Recognize();

// Retrieve the plain‑text result
string recognizedText = ocrEngine.Text;

// Show the output in the console
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(recognizedText);
```

Si todo salió sin problemas, verás un bloque limpio de texto que coincide con el documento original. Esa es la recompensa por **enderezar la imagen** correctamente, **eliminar ruido** y **preprocesar la imagen para OCR**.

---

## Paso 6 – Ejemplo completo funcional (Listo para copiar‑pegar)

A continuación se muestra el programa completo, listo para compilar. Simplemente reemplaza la ruta del archivo y estarás listo.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the source image
        // -------------------------------------------------
        var sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/noisy_rotated.tif");
        if (sourceImage == null)
        {
            Console.WriteLine("Unable to load image. Check the path.");
            return;
        }

        // -------------------------------------------------
        // 2️⃣ Build the preprocessing pipeline
        // -------------------------------------------------
        var preprocessPipeline = new PreprocessPipeline()
        {
            new DeskewFilter { MaxAngle = 30 },          // how to deskew image
            new DenoiseFilter { Strength = 0.8 },       // remove noise from scan
            new ContrastBoostFilter { Level = 1.3 }      // improves OCR accuracy
        };

        // -------------------------------------------------
        // 3️⃣ Apply the pipeline
        // -------------------------------------------------
        var processedImage = preprocessPipeline.Apply(sourceImage);
        processedImage.Save("cleaned_output.tif");
        Console.WriteLine("Preprocessing finished – cleaned_output.tif saved.");

        // -------------------------------------------------
        // 4️⃣ Configure the OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Image = processedImage,
            AutoPageSegmentation = true   // how to use OCR effectively
        };

        // -------------------------------------------------
        // 5️⃣ Recognize text from scan
        // -------------------------------------------------
        ocrEngine.Recognize();
        string result = ocrEngine.Text;

        Console.WriteLine("\n=== Recognized Text ===");
        Console.WriteLine(result);
    }
}
```

**Salida esperada** (truncada por brevedad):

```
=== Recognized Text ===
This is a sample scanned document.
It contains several lines of text,
and the OCR engine has correctly read them.
```

Si la salida se ve distorsionada, verifica que la imagen fuente no esté rotada más de 30°, o aumenta `DeskewFilter.MaxAngle`.

---

## Preguntas frecuentes (Casos límite y variaciones)

| Pregunta | Respuesta |
|----------|-----------|
| **¿Qué pasa si mi escaneo está rotado 45°?** | `DeskewFilter` tiene un límite en `MaxAngle`. Auméntalo (p.ej., `MaxAngle = 60`) o pre‑rota la imagen con una biblioteca gráfica antes de enviarla a la canalización. |
| **¿Puedo procesar PDFs página por página?** | Sí. Convierte cada página PDF a una imagen (p.ej., usando `Aspose.Pdf`) y ejecuta la misma canalización en cada bitmap. |
| **Mi documento está en francés – ¿debo cambiar algo?** | Configura `ocrEngine.Language = Language.French;` o carga un paquete de idioma personalizado. El resto de la canalización permanece igual. |
| **¿Hay alguna forma de mantener la resolución original?** | `PreprocessPipeline` trabaja sobre el bitmap original, preservando DPI. Simplemente evita llamar a `ImageStream.Resize` a menos que necesites reducir la escala por rendimiento. |
| **¿Cómo afecta el aumento de contraste a escaneos en color?** | `ContrastBoostFilter` actúa sobre cada canal; es seguro para imágenes en escala de grises o a color, pero también puedes convertir a escala de grises primero con `new GrayscaleFilter()`. |

---

## Ejemplo de imagen (Ayuda visual)

![ejemplo de cómo enderezar una imagen](/images/deskew-example.png)

*La imagen muestra un antes/después de un escaneo ruidoso rotado 12° que ha sido enderezado y limpiado.*

---

## Conclusión

Hemos cubierto **cómo enderezar una imagen** usando Aspose.OCR, demostrado una canalización completa de **preprocesamiento de imagen para OCR**, mostrado cómo **eliminar ruido del escaneo**, y finalmente **reconocer texto del escaneo** con unas pocas líneas de C#. Al encadenar `DeskewFilter`, `DenoiseFilter` y `ContrastBoostFilter` obtienes un bitmap ordenado que permite al motor OCR hacer su trabajo sin atascarse en artefactos.  

¿Próximos pasos? Prueba a experimentar con diferentes intensidades de filtro, agrega un `BinarizationFilter` para obtener una salida en blanco y negro puro, o alimenta la imagen limpiada a una canalización NLP posterior. El mismo patrón funciona para recibos, pasaportes y documentos históricos por igual.

¿Tienes más preguntas sobre **cómo usar OCR** en otros lenguajes o frameworks? Deja un comentario, ¡y feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}