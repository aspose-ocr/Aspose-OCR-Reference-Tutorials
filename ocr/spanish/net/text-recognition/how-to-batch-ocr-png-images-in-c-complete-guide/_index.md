---
category: general
date: 2026-03-17
description: Cómo procesar OCR por lotes de imágenes PNG en C# rápidamente. Aprende
  a extraer texto de archivos PNG, convertir PNG a texto y leer imágenes de un directorio
  con un script sencillo.
draft: false
keywords:
- how to batch OCR
- extract text png
- convert png to text
- read images from directory
language: es
og_description: Cómo procesar OCR por lotes de imágenes PNG en C# con código paso
  a paso. Extrae texto de archivos PNG, convierte PNG a texto y lee imágenes de un
  directorio sin esfuerzo.
og_title: Cómo hacer OCR por lotes de imágenes PNG en C# – Guía completa
tags:
- OCR
- C#
- Image Processing
title: Cómo hacer OCR por lotes de imágenes PNG en C# – Guía completa
url: /es/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

. alt text is inside brackets, we can translate. Title inside quotes also translate.

Proceed.

Let's craft final output.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo procesar OCR por lotes de imágenes PNG en C# – Guía completa

¿Alguna vez te has preguntado **cómo hacer OCR por lotes** en una carpeta llena de capturas de pantalla sin abrir cada archivo manualmente? No eres el único: los desarrolladores preguntan constantemente cómo hacer OCR por lotes de grandes colecciones de PNG, especialmente cuando el objetivo es extraer texto de archivos PNG para análisis posteriores.  

En este tutorial recorreremos un ejemplo listo‑para‑ejecutar en C# que **extrae texto de archivos PNG**, **convierte PNG a texto**, y te muestra la mejor manera de **leer imágenes desde un directorio**. Al final tendrás un único script que genera un `.txt` al lado de cada imagen, ahorrándote horas de copiar‑pegar manual.

## Lo que lograrás

- Inicializar un motor OCR una sola vez y reutilizarlo para todo el lote.  
- Escanear cada `*.png` en una carpeta dada sin escribir tú mismo un bucle.  
- Guardar cada resultado de OCR en su propio archivo de texto, preservando el nombre original del archivo.  
- Manejar casos comunes como carpetas vacías o archivos que no son imágenes de forma elegante.

### Requisitos previos

- .NET 6.0 o posterior (el código funciona también en .NET Core y .NET Framework).  
- Una biblioteca OCR que exponga los tipos `OcrEngine`, `ImageStream` y `OcrResult` (por ejemplo, el ficticio SDK **FastOCR** usado en los fragmentos).  
- Conocimientos básicos de C#—no se requieren patrones avanzados.

---

## Cómo procesar OCR por lotes de imágenes PNG – Visión general

A continuación tienes el **programa completo y ejecutable**. Siéntete libre de copiar‑pegarlo en un nuevo proyecto de consola, reemplazar las rutas de ejemplo y pulsar **F5**.

```csharp
using System;
using System.IO;
using System.Linq;
using FastOCR;               // <-- Replace with your actual OCR namespace

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize the OCR engine (language = English)
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();
        ocrEngine.Config.Language = Language.English;

        // -------------------------------------------------
        // Step 2: Locate every PNG file in the input folder
        // -------------------------------------------------
        string inputFolder = @"YOUR_DIRECTORY\images";
        string[] imagePaths = Directory.GetFiles(inputFolder, "*.png");

        if (imagePaths.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to process.");
            return;
        }

        // -------------------------------------------------
        // Step 3: Convert file paths to ImageStream objects
        // -------------------------------------------------
        var imageStreams = imagePaths
            .Select(path => ImageStream.FromFile(path))
            .ToList();

        // -------------------------------------------------
        // Step 4: Recognize text in the entire batch
        // -------------------------------------------------
        IReadOnlyList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // -------------------------------------------------
        // Step 5: Write each result to a .txt file next to the image
        // -------------------------------------------------
        string outputFolder = @"YOUR_DIRECTORY\output";
        Directory.CreateDirectory(outputFolder); // ensures the folder exists

        for (int i = 0; i < ocrResults.Count; i++)
        {
            string originalFileName = Path.GetFileNameWithoutExtension(imagePaths[i]);
            string outputPath = Path.Combine(outputFolder, $"{originalFileName}.txt");
            File.WriteAllText(outputPath, ocrResults[i].Text);
            Console.WriteLine($"✅ {originalFileName}.txt created");
        }

        Console.WriteLine("All done! Check the output folder for your text files.");
    }
}
```

> **Salida esperada:** Por cada `image01.png` encontrarás un `image01.txt` que contiene los caracteres reconocidos. La consola listará cada archivo a medida que se escribe.

![Cómo procesar OCR por lotes diagrama](how-to-batch-ocr-diagram.png "Diagrama que ilustra cómo procesar OCR por lotes de imágenes PNG usando C#")

---

## Explicación paso a paso

### 1. Inicializar el motor OCR – el corazón del proceso  

La línea `var ocrEngine = new OcrEngine();` crea una única instancia del motor que se reutilizará para todo el lote. Re‑usar el motor es **crucial** porque la mayoría de las bibliotecas OCR asignan recursos pesados (como modelos de lenguaje) al construirse. Inicializar una sola vez mejora el rendimiento de forma drástica—especialmente cuando tienes decenas o cientos de PNG.

> **Consejo profesional:** Si necesitas un idioma distinto al inglés, establece `ocrEngine.Config.Language = Language.Spanish;` (o cualquier enum soportado).  

### 2. Leer imágenes desde el directorio – localizar cada PNG  

`Directory.GetFiles(@"YOUR_DIRECTORY\images", "*.png")` hace exactamente lo que la palabra clave secundaria *read images from directory* promete. Devuelve un arreglo de rutas absolutas, que luego pasamos al motor OCR.  

> **¿Por qué no usar `SearchOption.AllDirectories`?** Si tus imágenes están anidadas, puedes cambiar a `GetFiles(path, "*.png", SearchOption.AllDirectories)`. Solo recuerda que los escaneos más profundos pueden traer archivos no deseados, así que filtra según corresponda.

### 3. Convertir rutas de archivo a objetos ImageStream  

La mayoría de los SDK OCR esperan un stream en lugar de una ruta cruda. La expresión LINQ `Select(path => ImageStream.FromFile(path)).ToList()` construye una **lista de streams** que el reconocedor por lotes puede consumir en una sola llamada. Este paso también asegura que los manejadores de archivo se abran solo una vez, reduciendo la sobrecarga de I/O.

> **Caso límite:** Si un archivo está corrupto, `ImageStream.FromFile` puede lanzar una excepción. Envuelve la conversión en un `try/catch` si necesitas resiliencia.

### 4. Reconocer texto en todo el lote  

`ocrEngine.RecognizeBatch(imageStreams)` es el punto óptimo para *how to batch OCR*. En lugar de iterar sobre cada imagen y llamar a un método de una sola imagen, entregamos toda la colección al motor. Internamente la biblioteca puede paralelizar el trabajo, dándote un impulso de velocidad en máquinas con varios núcleos.

> **Tip:** Si tu biblioteca OCR no expone un método por lotes, aún puedes lograr un rendimiento similar usando `Parallel.ForEach` alrededor de la llamada `Recognize` de una sola imagen.

### 5. Guardar cada resultado OCR – convertir PNG a texto  

El bucle `for` final escribe `ocrResults[i].Text` en un archivo `.txt` cuyo nombre refleja al PNG original. Esto es exactamente lo que describe la palabra clave secundaria *convert PNG to text*. La llamada `Path.Combine` garantiza que la carpeta de salida exista y previene errores de traversal de rutas.

> **Trampa común:** Olvidar crear la carpeta de salida primero provocará una `DirectoryNotFoundException`. La línea `Directory.CreateDirectory(outputFolder);` lo soluciona de forma preventiva.

---

## Manejo de variaciones del mundo real

| Situación | Qué cambiar | Por qué |
|-----------|-------------|---------|
| **Carpeta de entrada vacía** | Mantener la guardia `if (imagePaths.Length == 0)` al inicio | Evita una llamada OCR innecesaria y muestra un mensaje amigable |
| **Tipos de archivo mixtos** | Usar `Directory.EnumerateFiles(..., "*.*", SearchOption.TopDirectoryOnly).Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase))` | Garantiza que solo proceses PNG, cumpliendo *extract text png* sin errores |
| **Imágenes muy grandes ( > 5 MB )** | Reducir antes de pasar a OCR: `ImageStream.FromFile(path).Resize(1920, 1080)` (si la API lo soporta) | Reduce la presión de memoria y a menudo mejora la precisión del reconocimiento |
| **Idioma OCR diferente** | Establecer `ocrEngine.Config.Language = Language.French;` | Alinea el motor con el idioma de las imágenes de origen |

---

## Preguntas frecuentes (FAQ)

**P: ¿Funciona esto con archivos JPEG o TIFF?**  
R: La lógica central permanece igual; solo cambia el patrón de búsqueda a `"*.jpg"` o `"*.tif"` y asegura que la biblioteca OCR pueda decodificar esos formatos.

**P: ¿Cómo puedo procesar miles de imágenes sin quedarme sin memoria?**  
R: Sustituye la llamada por lotes por un enfoque de streaming—procesa un bloque de, por ejemplo, 50 imágenes a la vez, luego libera los streams antes de cargar el siguiente bloque.

**P: Necesito la puntuación de confianza del OCR. ¿Dónde la encuentro?**  
R: La mayoría de los objetos `OcrResult` exponen una propiedad `Confidence`. Puedes ampliar el paso de escritura:

```csharp
var result = ocrResults[i];
string content = $"Confidence: {result.Confidence:P2}\n{result.Text}";
File.WriteAllText(outputPath, content);
```

---

## Conclusión

Acabamos de cubrir **cómo hacer OCR por lotes** de imágenes PNG en C# de principio a fin. Al inicializar un solo motor, leer imágenes desde el directorio, convertirlas a streams, reconocer todo el lote y finalmente escribir cada resultado en un archivo de texto, ahora dispones de un patrón sólido y listo para producción para **extract text PNG**, **convert PNG to text** y **read images from directory**.

¿Qué sigue? Prueba cambiar el proveedor OCR, añade post‑procesamiento multihilo (p. ej., corrección ortográfica), o alimenta los archivos `.txt` a un índice de búsqueda. El cielo es el límite una vez que domines el flujo de trabajo por lotes.

¿Tienes alguna variante que quieras compartir? ¡Deja un comentario y feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}