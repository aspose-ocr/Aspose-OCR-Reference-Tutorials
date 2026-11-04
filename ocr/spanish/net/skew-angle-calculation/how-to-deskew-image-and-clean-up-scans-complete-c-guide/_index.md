---
category: general
date: 2026-03-18
description: Cómo enderezar una imagen y reducir el ruido en archivos escaneados.
  Aprende a cargar la imagen desde un archivo, extraer texto de un TIFF y reconocer
  texto de la imagen con Aspose OCR.
draft: false
keywords:
- how to deskew image
- how to reduce noise
- recognize text from image
- load image from file
- extract text from tiff
language: es
og_description: Cómo enderezar una imagen rápidamente usando Aspose OCR. Esta guía
  muestra cómo reducir el ruido, cargar la imagen desde un archivo y extraer texto
  de un TIFF en C#.
og_title: Cómo enderezar una imagen – Tutorial completo de OCR en C#
tags:
- OCR
- C#
- Image Processing
title: Cómo enderezar imágenes y limpiar escaneos – Guía completa en C#
url: /es/net/skew-angle-calculation/how-to-deskew-image-and-clean-up-scans-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo enderezar una imagen – Tutorial completo de OCR en C#

¿Alguna vez te has preguntado **cómo enderezar una imagen** que parece haber sido escaneada con un escáner tambaleante? No estás solo. La mayoría de los desarrolladores se topan con ese problema cuando el TIFF de origen está un poco torcido y los resultados del OCR salen desordenados. ¿La buena noticia? Con un par de líneas de C# puedes enderezar la foto, eliminar el fondo granulado y extraer texto limpio y buscable directamente del archivo.

En esta guía recorreremos **cómo reducir el ruido**, **cargar la imagen desde un archivo**, y finalmente **reconocer texto de la imagen** usando Aspose OCR. Al final podrás **extraer texto de documentos tiff** sin despeinarte.

> **Consejo profesional:** Si ya estás usando Aspose OCR en otros proyectos, puedes incorporar estos filtros sin ningún problema adicional de licencias.

---

## Lo que necesitarás

- .NET 6 o posterior (el código también funciona en .NET Core)  
- Paquete NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- Un TIFF escaneado que esté ligeramente rotado o ruidoso (usaremos `skewed_scanned_doc.tif` como ejemplo)  
- Un editor de texto o IDE (Visual Studio, VS Code, Rider – elige el que prefieras)

No se requieren bibliotecas adicionales; los filtros que usaremos están integrados en Aspose OCR.

---

## Paso 1 – Crear el motor OCR (Cómo enderezar una imagen)

Lo primero que haces es iniciar un `OcrEngine`. Piensa en él como el cerebro que más tarde leerá los caracteres por ti.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Initialize the OCR engine – this object holds all settings
        var ocrEngine = new OcrEngine();
```

¿Por qué crear el motor al principio? Te brinda un único lugar para adjuntar filtros de preprocesamiento, paquetes de idioma y opciones de salida. Si omites este paso y llamas a `OcrEngine.Recognize` directamente, pierdes la oportunidad de limpiar la imagen primero, que es precisamente la razón por la que nos importa el enderezado.

---

## Paso 2 – Añadir filtros de enderezado y reducción de ruido (Cómo reducir el ruido)

Ahora adjuntamos dos filtros:

| Filtro | Qué hace | Por qué es importante |
|--------|----------|-----------------------|
| `AutoDeskewFilter` | Detecta y corrige la rotación | Endereza las líneas de texto para que el motor OCR pueda leerlas correctamente |
| `NoiseReductionFilterV2` | Elimina manchas y granulado de fondo | Los píxeles más limpios significan menos errores de reconocimiento |

```csharp
        // Add filters to improve OCR accuracy
        ocrEngine.Settings.Filters.Add(new AutoDeskewFilter());          // corrects rotation
        ocrEngine.Settings.Filters.Add(new NoiseReductionFilterV2());   // reduces background noise
```

Podrías cambiar `NoiseReductionFilterV2` por la versión anterior, pero el algoritmo v2 maneja mejor los escáneres modernos. Si tu documento ya está perfectamente plano, el filtro de enderezado simplemente pasará la imagen sin cambios—no causará daño.

---

## Paso 3 – Cargar la imagen desde un archivo (Cargar imagen desde archivo)

Aspose ofrece un práctico ayudante `ImageStream.FromFile` que lee una variedad de formatos, incluidos TIFF, JPEG, PNG y BMP. Así es como cargamos el archivo en memoria:

```csharp
        // Load the scanned image you want to preprocess
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_scanned_doc.tif");
```

Reemplaza `YOUR_DIRECTORY` con la ruta real en tu máquina. Si trabajas con una ruta relativa, asegúrate de que el archivo esté junto a tu ejecutable o configura el directorio de trabajo en consecuencia.

---

## Paso 4 – Ejecutar OCR en la imagen preprocesada (Reconocer texto de la imagen)

Con los filtros configurados y la imagen cargada, finalmente le pedimos a Aspose que lea los caracteres:

```csharp
        // Perform OCR – the engine will automatically apply the filters first
        var ocrResult = ocrEngine.Recognize(image);
```

Detrás de escena, el motor ejecuta el algoritmo de enderezado, suaviza el ruido y luego ejecuta un reconocedor basado en redes neuronales. El resultado se envuelve en un objeto `OcrResult` que te brinda el texto sin procesar, puntuaciones de confianza e incluso cajas delimitadoras si las necesitas más adelante.

---

## Paso 5 – Mostrar o guardar el texto extraído (Extraer texto de TIFF)

Para una demostración rápida simplemente volcamos el texto en la consola, pero podrías escribirlo en un archivo, una base de datos o enviarlo a un flujo de trabajo posterior.

```csharp
        // Show the recognized text in the console
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Salida esperada** (ejemplo, variará según tu documento):

```
Invoice #12345
Date: 2023‑04‑01
Total: $1,250.00
Thank you for your business!
```

Si la salida aún contiene caracteres distorsionados, verifica que el TIFF original no tenga una resolución demasiado baja (se recomiendan al menos 300 dpi) y que el idioma esté configurado correctamente en `ocrEngine.Settings.Language`.

---

## Ejemplo completo (Todos los pasos en un solo lugar)

A continuación se muestra el programa completo que puedes copiar y pegar en un nuevo proyecto de consola y ejecutar de inmediato.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Add preprocessing filters
        ocrEngine.Settings.Filters.Add(new AutoDeskewFilter());          // deskew image
        ocrEngine.Settings.Filters.Add(new NoiseReductionFilterV2());   // reduce noise

        // 3️⃣ Load the image file (TIFF, JPEG, etc.)
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_scanned_doc.tif");

        // 4️⃣ Recognize text – filters run automatically
        var ocrResult = ocrEngine.Recognize(image);

        // 5️⃣ Output the extracted text
        Console.WriteLine(ocrResult.Text);
    }
}
```

Guarda el archivo como `Program.cs`, ejecuta `dotnet run` y deberías ver el texto limpiado aparecer en tu terminal.

---

## Preguntas frecuentes y casos límite

### ¿Qué pasa si mi TIFF tiene varias páginas?
Aspose OCR puede procesar imágenes multipágina iterando sobre `image.GetPages()` (o usando `image.Pages`). Cada página devuelve su propio `OcrResult`. Combínalas con `StringBuilder` si necesitas una única cadena.

### ¿El filtro de enderezado funciona con imágenes muy rotadas?
Maneja rotaciones de hasta aproximadamente ±15°. Más allá de eso podrías necesitar pre‑rotar la imagen manualmente usando una biblioteca gráfica (p. ej., `System.Drawing` o `SkiaSharp`) antes de enviarla a Aspose.

### ¿Cómo puedo mejorar la precisión para texto no inglés?
Configura el idioma explícitamente:

```csharp
ocrEngine.Settings.Language = Language.English; // or Language.French, etc.
```

También puedes cargar paquetes de idioma personalizados si los incorporados no cubren tu alfabeto.

### ¿Puedo ejecutar esto en Linux?
Absolutamente. Aspose OCR es multiplataforma; solo asegúrate de que las dependencias nativas estén presentes (normalmente ninguna para la versión pura de .NET). Usa `dotnet publish -r linux-x64` para obtener un binario autocontenido.

---

## Bonus: Visualizar la imagen enderezada

Si deseas ver la imagen corregida antes del OCR, puedes guardarla nuevamente en disco:

```csharp
// After OCR, the filtered image is stored in ocrEngine.Settings.FiltersResult
var corrected = ocrEngine.Settings.FiltersResult;
corrected.Save(@"output/deskewed_cleaned.tif");
```

![ejemplo de cómo enderezar una imagen](https://example.com/deskew-demo.png "ejemplo de cómo enderezar una imagen")

*Texto alternativo de la imagen:* **ejemplo de cómo enderezar una imagen** – muestra un antes/después de un TIFF rotado corregido por AutoDeskewFilter.

---

## Conclusión

Hemos cubierto **cómo enderezar una imagen**, **cómo reducir el ruido**, y todo el flujo para **reconocer texto de la imagen**, **cargar la imagen desde un archivo**, y **extraer texto de tiff** usando Aspose OCR en C#. ¿La lección principal? Añadir solo dos filtros de preprocesamiento puede convertir un escaneo tembloroso y granulado en un documento nítido y buscable sin herramientas externas.

¿Listo para el siguiente paso? Prueba cambiar `AutoDeskewFilter` por `AutoRotateFilter` si tus documentos están al revés, o experimenta con `ContrastEnhancementFilter` para impresiones descoloridas. El mismo patrón—motor → filtros → carga → reconocimiento—se aplica a todos los escenarios de Aspose OCR, por lo que puedes reutilizar este esqueleto para PDFs, PNGs o incluso fotos de cámara.

¡Feliz codificación, y que tu OCR sea siempre preciso!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}