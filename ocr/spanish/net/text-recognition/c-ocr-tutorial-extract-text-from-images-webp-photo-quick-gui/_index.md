---
category: general
date: 2026-03-17
description: c# tutorial de OCR – descubre cómo extraer texto de archivos de imagen,
  leer texto de fotos WebP y convertir una imagen a texto usando un OcrEngine sencillo.
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- read text from webp
- recognize text from photo
- convert image to text
language: es
og_description: El tutorial de OCR en C# te muestra cómo extraer texto de archivos
  de imagen, leer texto de fotos WebP y convertir una imagen a texto con unas pocas
  líneas de código.
og_title: Tutorial de OCR en C# – Extrae texto de imágenes en minutos
tags:
- C#
- OCR
- Image Processing
title: 'Tutorial de OCR en C#: Extraer texto de imágenes (WebP, foto) – Guía rápida'
url: /es/net/text-recognition/c-ocr-tutorial-extract-text-from-images-webp-photo-quick-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tutorial c# OCR – Extraer texto de imágenes (WebP, Foto)

¿Alguna vez necesitaste **extraer texto de una imagen** pero no estabas seguro por dónde empezar en C#? Tal vez tienes una captura de pantalla en WebP, un JPEG de un recibo, o una página de PDF escaneada y solo quieres las palabras dentro. En este **tutorial c# OCR** recorreremos un ejemplo completo, listo‑para‑ejecutar que lee texto de una foto, maneja WebP y otros formatos modernos, y convierte la imagen a texto plano—todo en unas pocas líneas.

**¿Cuál es el beneficio?** Podrás convertir cualquier imagen con texto en cadenas buscables, ingresarlas en bases de datos, o pasarlas a pipelines de IA posteriores. No hay magia, solo un motor OCR sólido, algunas APIs de .NET y explicaciones claras del “por qué” detrás de cada paso.

## Lo que necesitarás

- **.NET 6 SDK** (o posterior). El código a continuación se compila con .NET 6+ y se ejecuta en Windows, Linux o macOS.
- **Visual Studio 2022** o cualquier editor que prefieras (VS Code funciona bien).
- El paquete NuGet **`Microsoft.Windows.SDK.Contracts`** (provee `Windows.Media.Ocr`). Instálalo con:

```bash
dotnet add package Microsoft.Windows.SDK.Contracts
```

- Un archivo de imagen que deseas procesar – para este tutorial usaremos una foto **WebP** llamada `photo.webp` ubicada en una carpeta llamada `YOUR_DIRECTORY`.

> Consejo profesional: Si estás en una plataforma que no sea Windows, puedes cambiar el `OcrEngine` por una biblioteca multiplataforma como **Tesseract**. El código circundante permanece prácticamente igual.

## Paso 1: Configurar un proyecto tutorial C# OCR

Primero, crea una nueva aplicación de consola. Abre una terminal y ejecuta:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Agrega el paquete requerido (como se muestra arriba) y abre el proyecto en tu IDE. Esta estructura nos brinda una base limpia para el **tutorial c# OCR**.

## Paso 2: Importar espacios de nombres y preparar la imagen

Necesitamos algunas directivas `using` para que el compilador sepa dónde encontrar `OcrEngine`, `SoftwareBitmap` y los ayudantes de carga de imágenes.

```csharp
using System;
using System.IO;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;
```

> **¿Por qué estos espacios de nombres?**  
> `Windows.Media.Ocr` contiene la clase `OcrEngine` que realmente realiza el reconocimiento. `Windows.Graphics.Imaging` nos permite decodificar la imagen (incluido WebP) a un `SoftwareBitmap` que el motor puede entender. Los ayudantes `System.IO` y `Windows.Storage.Streams` hacen que la carga de archivos sea sencilla.

Ahora, carga la imagen. El decodificador incorporado puede manejar WebP, HEIF, PNG, JPEG y más, por lo que puedes **leer texto de WebP** sin complementos adicionales.

```csharp
// Step 2: Load the image file into a SoftwareBitmap
string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

// Open the file as a random access stream
using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
{
    // Decode the image (auto-detects format)
    BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
    SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();
    
    // Optional: Convert to grayscale for better OCR accuracy
    SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);
    
    // Pass the bitmap to the next step
    await RecognizeTextAsync(grayBitmap);
}
```

> **Caso límite:** Si tu imagen ya es en blanco y negro, puedes omitir el paso de conversión. La conversión a escala de grises es una pequeña mejora de rendimiento y a menudo mejora el reconocimiento en fotos ruidosas.

## Paso 3: Ejecutar el motor OCR – Reconocer texto de la foto

Este es el corazón del **tutorial c# OCR**. Creamos una instancia de `OcrEngine`, le pasamos el bitmap y extraemos el texto reconocido.

```csharp
static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
{
    // Step 3: Create the OCR engine instance – it automatically picks the best language
    OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

    if (ocrEngine == null)
    {
        Console.WriteLine("❌ No OCR engine available for the current language.");
        return;
    }

    // Perform recognition
    OcrResult ocrResult = await ocrEngine.RecognizeAsync(bitmap);

    // Step 4: Display the extracted text – this is the “convert image to text” part
    Console.WriteLine("📝 Recognized text:");
    Console.WriteLine(ocrResult.Text);
}
```

**¿Qué está sucediendo?**  
- `TryCreateFromUserProfileLanguages()` elige el/los idioma(s) configurados en el perfil de usuario de Windows, que normalmente cubren inglés, español, etc. Si necesitas un idioma específico, usa `OcrEngine.TryCreateFromLanguage(new Language("fr-FR"))`.  
- `RecognizeAsync` realiza el trabajo pesado en un hilo en segundo plano, devolviendo un `OcrResult` que contiene la cadena cruda, los cuadros delimitadores de palabras y los puntajes de confianza.  
- Finalmente, imprimimos `ocrResult.Text`, dándote el resultado de **convertir imagen a texto** que puedes enviar a otro lugar.

## Paso 4: Ejemplo completo y ejecutable

Juntando todo, aquí tienes un programa autónomo que puedes copiar y pegar en `Program.cs`. Compila, se ejecuta y muestra el texto extraído de `photo.webp`.

```csharp
// Program.cs – Complete c# OCR tutorial example
using System;
using System.IO;
using System.Threading.Tasks;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;

class Program
{
    static async Task Main(string[] args)
    {
        // Replace with your actual directory and file name
        string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"❗ Image not found: {imagePath}");
            return;
        }

        // Load and optionally preprocess the image
        using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
        {
            BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
            SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();

            // Convert to grayscale – improves OCR accuracy on many photos
            SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);

            // Run OCR
            await RecognizeTextAsync(grayBitmap);
        }
    }

    static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
    {
        // Create OCR engine (auto‑detect language)
        OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

        if (ocrEngine == null)
        {
            Console.WriteLine("❌ Unable to create OCR engine. Ensure language packs are installed.");
            return;
        }

        // Perform recognition
        OcrResult result = await ocrEngine.RecognizeAsync(bitmap);

        // Output the extracted text
        Console.WriteLine("\n--- OCR Output ---");
        Console.WriteLine(result.Text);
        Console.WriteLine("--- End of Output ---\n");
    }
}
```

### Salida esperada

Si `photo.webp` contiene la frase “Hello, world! This is a test.” verás algo como:

```
--- OCR Output ---
Hello, world!
This is a test.
--- End of Output ---
```

Los saltos de línea exactos dependen del diseño de la imagen fuente, pero el resultado de **extraer texto de la imagen** siempre será una cadena simple que puedes manipular más adelante.

## Preguntas frecuentes y casos límite

### ¿Funciona con otros formatos de imagen?

Absolutamente. El decodificador usado (`BitmapDecoder`) detecta automáticamente JPEG, PNG, BMP, GIF, **WebP**, HEIF y más. Así que puedes **leer texto de WebP**, JPEG o incluso un TIFF sin cambiar el código.

### ¿Qué pasa si el motor OCR devuelve baja confianza?

Puedes inspeccionar `ocrResult.Lines` y cada `OcrWord` para obtener un `ConfidenceScore`. Si el puntaje está por debajo de un umbral (p.ej., 0.6), considera:
- Pre‑procesar la imagen (aumentar contraste, enfocar, enderezar).
- Usar una imagen fuente de mayor resolución.
- Cambiar a una biblioteca dedicada como **Tesseract** para soporte multilingüe.

### ¿Cómo manejar varios idiomas en la misma imagen?

Crea instancias separadas de `OcrEngine` para cada idioma y ejecútalas secuencialmente, o usa una biblioteca que soporte detección de idiomas mixtos. Para el motor incorporado, puedes pasar un objeto `Language`:

```csharp
var spanishEngine = OcrEngine.TryCreateFromLanguage(new Language("es-ES"));
```

### ¿Puedo ejecutar esto en Linux/macOS?

La API `Windows.Media.Ocr` es solo para Windows. En plataformas que no sean Windows, reemplaza la sección OCR con **Tesseract** (a través de `Tesseract.Net.SDK`). El código de carga y preprocesamiento sigue siendo idéntico, por lo que el resto de este **tutorial c# OCR** sigue siendo aplicable.

## Consejos profesionales para mayor precisión

- **Redimensiona** imágenes grandes a un máximo de 2000 px en el lado más largo – los motores OCR funcionan más rápido con tamaños moderados.
- **Desruida** usando un simple desenfoque gaussiano si la foto es granulada.
- **Endereza** el bitmap si el texto no está perfectamente horizontal; `SoftwareBitmap` puede rotarse antes de pasarlo a `OcrEngine`.
- **Cachea** la instancia de `OcrEngine` si estás procesando muchas imágenes en lote; crearla repetidamente añade sobrecarga.

## Temas relacionados para explorar

- **Convertir imagen a texto** usando **Tesseract** para proyectos multiplataforma.
- **Extraer texto de PDF** renderizando cada página a una imagen primero.
- **OCR por lotes**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}