---
category: general
date: 2026-03-13
description: Cómo enderezar la imagen y aumentar el contraste para OCR. Aprende a
  eliminar el ruido, extraer la imagen de texto y obtener resultados fiables con Aspose
  OCR.
draft: false
keywords:
- how to deskew image
- extract text image
- how to remove noise
- how to boost contrast
- how to extract text
language: es
og_description: Cómo corregir la inclinación de una imagen en C# y extraer texto.
  Esta guía muestra cómo eliminar el ruido, aumentar el contraste y obtener resultados
  precisos de OCR.
og_title: Cómo enderezar una imagen – OCR rápido con Aspose en C#
tags:
- OCR
- C#
- Image Processing
title: Cómo corregir la inclinación de una imagen y extraer texto en C# – Guía completa
url: /es/net/ocr-optimization/how-to-deskew-image-and-extract-text-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo enderezar una imagen y extraer texto en C# – Guía completa

¿Alguna vez te has preguntado **cómo enderezar una imagen** antes de enviarla a un motor OCR? No estás solo. Un escaneo torcido puede convertir una extracción de texto perfecta en un juego de adivinanzas, especialmente cuando la imagen también es ruidosa o de bajo contraste. En este tutorial recorreremos los pasos exactos para enderezar, limpiar y aclarar una imagen para que puedas **extraer texto de la imagen** de forma fiable. A lo largo del camino también cubriremos **cómo eliminar ruido**, **cómo aumentar el contraste**, y finalmente **cómo extraer texto** usando Aspose.OCR.

Al final de esta guía tendrás un programa C# listo para ejecutar que toma un PNG torcido y con manchas, lo corrige y muestra el texto reconocido en la consola. Sin enlaces misteriosos de “ver la documentación”, solo una solución completa y autónoma que puedes copiar y pegar.

## Qué necesitarás

- **.NET 6.0** o posterior (el código también funciona en .NET Framework 4.7+).  
- **Aspose.OCR para .NET** – instalar vía NuGet: `Install-Package Aspose.OCR`.  
- Una imagen de ejemplo que esté rotada, ruidosa o de bajo contraste (usaremos `skewed_noisy.png`).  
- Cualquier IDE que prefieras—Visual Studio, Rider o VS Code sirve.

Eso es todo. Sin bibliotecas nativas adicionales, sin servicios externos.

![ejemplo de cómo enderezar imagen](image-placeholder.png)

*(Texto alternativo de la imagen: ejemplo de cómo enderezar imagen – antes y después del procesamiento)*

## Cómo enderezar una imagen – Visión general

La idea central detrás de **cómo enderezar una imagen** es simple: detectar el ángulo de rotación y girar el bitmap de vuelta a una línea base horizontal. Aspose.OCR incluye un `DeskewFilter` que hace exactamente eso. Pero una buena canalización OCR rara vez se detiene en el enderezado; también deseas **eliminar ruido**, **aumentar el contraste**, y finalmente **extraer texto**. Las siguientes secciones desglosan cada componente.

### Por qué importa una canalización de preprocesamiento

Imagina intentar leer una nota manuscrita que ha sido escaneada con un ligero ángulo, con manchas de café esparcidas por la página. Incluso el motor OCR más inteligente tropezará. Al proporcionar una imagen limpia y enderezada, le das al motor una señal clara, lo que se traduce en mayor precisión y menos correcciones posteriores.

## Paso 1: Cargar tu imagen

Primero, necesitamos un `ImageStream` que apunte al archivo fuente. Aspose.OCR puede leer muchos formatos (PNG, JPEG, TIFF), así que elige el que tengas.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Load the image from disk
ImageStream imageStream = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.png");
```

**Por qué es importante:** Cargar la imagen en un `ImageStream` le brinda al motor OCR una forma unificada de acceder a los datos de píxeles, sin importar el tipo de archivo original.

## Paso 2: Construir una canalización de preprocesamiento (Enderezado, Eliminación de ruido, Aumento de contraste)

Aquí es donde respondemos **cómo eliminar ruido**, **cómo aumentar el contraste**, y por supuesto **cómo enderezar una imagen**, todo en un `FilterPipeline`.

```csharp
// Create a pipeline to hold the filters
FilterPipeline preprocessingPipeline = new FilterPipeline();

// 1️⃣ Deskew – correct rotation up to 15 degrees
preprocessingPipeline.Add(new DeskewFilter { MaxAngleDegrees = 15 });

// 2️⃣ Despeckle – eliminate isolated dark/bright pixels (noise)
preprocessingPipeline.Add(new DespeckleFilter());

// 3️⃣ Contrast boost – make darks darker, lights lighter (Level 30 is a good start)
preprocessingPipeline.Add(new ContrastBoostFilter { Level = 30 });

// 4️⃣ Binarize – convert to pure black‑and‑white using Otsu’s method
preprocessingPipeline.Add(new BinarizeOtsuFilter());
```

### Cómo ayuda cada filtro

| Filtro | Propósito | Caso de uso típico |
|--------|-----------|--------------------|
| **DeskewFilter** | Rota la imagen de vuelta a horizontal. | Páginas escaneadas que están ligeramente inclinadas. |
| **DespeckleFilter** | Elimina manchas aisladas que parecen caracteres sueltos. | Escaneos de periódicos antiguos o fotocopias de baja calidad. |
| **ContrastBoostFilter** | Amplifica la diferencia entre el primer plano y el fondo. | Tinta desvanecida o capturas de pantalla de bajo contraste. |
| **BinarizeOtsuFilter** | Produce una imagen limpia en blanco y negro, ideal para OCR. | Cualquier escenario donde el color no sea necesario para el reconocimiento de texto. |

**Consejo profesional:** Si tu imagen está gravemente rotada (más de 15°), aumenta `MaxAngleDegrees` a 30 o 45, pero ten en cuenta que ángulos extremos pueden introducir artefactos de interpolación.

## Paso 3: Configurar el motor OCR

Ahora vinculamos la imagen y la canalización, indicamos a Aspose qué idioma esperamos y creamos la instancia `OcrEngine`.

```csharp
// Set up the OCR engine with the image, pipeline, and language
OcrEngine ocrEngine = new OcrEngine
{
    Image = imageStream,
    PreProcessingFilters = preprocessingPipeline,
    Language = Language.English      // Change if you need another language
};
```

**Por qué establecemos el idioma:** Especificar `Language.English` reduce el conjunto de caracteres que el motor busca, lo que acelera el procesamiento y reduce falsos positivos. Si necesitas soporte multilingüe, puedes pasar una lista separada por comas (p. ej., `Language.English | Language.French`).

## Paso 4: Reconocer y extraer texto

Con todo preparado, el reconocimiento real es una única llamada a método.

```csharp
// Perform the OCR operation
ocrEngine.Recognize();

// The recognized text is now available via the Text property
string extractedText = ocrEngine.Text;
Console.WriteLine(extractedText);
```

Esa línea imprime el resultado OCR directamente en la consola, lo cual es perfecto para una verificación rápida o para canalizarlo a otro sistema.

## Salida esperada y verificación

Ejecutar el programa completo con `skewed_noisy.png` debería producir algo como:

```
Lorem ipsum dolor sit amet,
consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut
labore et dolore magna aliqua.
```

Si la salida se ve desordenada, verifica lo siguiente:

1. **Rango de ángulo:** ¿Fue la rotación original mayor que `MaxAngleDegrees`?  
2. **Nivel de ruido:** ¿Está la imagen muy manchada? Considera añadir un segundo `DespeckleFilter`.  
3. **Nivel de contraste:** Para tinta muy tenue, aumenta `ContrastBoostFilter.Level` a 40‑50.

## Cómo eliminar ruido – Opciones avanzadas

A veces un solo `DespeckleFilter` no es suficiente, especialmente con escaneos de película granosa. Aspose ofrece un `MedianFilter` que funciona bien en fondos texturizados.

```csharp
preprocessingPipeline.Add(new MedianFilter { KernelSize = 3 });
```

Añade esto **antes** del `DespeckleFilter` para obtener los mejores resultados. La operación de mediana suaviza las regiones mientras preserva los bordes, lo que ayuda a mantener los caracteres intactos.

## Cómo aumentar el contraste – Ajuste fino

Si el valor predeterminado `Level = 30` deja algunos caracteres tenues, puedes encadenar varios aumentos de contraste:

```csharp
preprocessingPipeline.Add(new ContrastBoostFilter { Level = 20 });
preprocessingPipeline.Add(new ContrastBoostFilter { Level = 20 });
```

Dos aumentos modestos a menudo superan a un solo aumento agresivo, porque evitan el recorte de píxeles extremos.

## Extraer texto de la imagen usando Aspose – Consejos de post‑procesamiento

Después de obtener `ocrEngine.Text`, podrías querer:

- **Eliminar espacios en blanco**: `extractedText = extractedText.Trim();`
- **Normalizar finales de línea**: `extractedText = extractedText.Replace("\r\n", "\n");`
- **Eliminar caracteres no ASCII** (si solo esperas inglés): `extractedText = Regex.Replace(extractedText, @"[^\x00-\x7F]+", string.Empty);`

Estos pasos convierten la salida OCR cruda en cadenas limpias y buscables, perfectas para indexar o alimentar a una canalización NLP posterior.

## Problemas comunes y consejos

| Síntoma | Causa probable | Solución |
|---------|----------------|----------|
| El texto está inclinado después del OCR | `DeskewFilter` con ángulo máximo demasiado bajo | Aumentar `MaxAngleDegrees`. |
| Muchos caracteres aleatorios | El ruido no se eliminó por completo | Añadir `MedianFilter` o incrementar la agresividad de `DespeckleFilter`. |
| Las letras tenues se pierden | El contraste no es suficiente | Apilar dos `ContrastBoostFilter`s o elevar `Level`. |
| El rendimiento es lento en imágenes grandes | La canalización se ejecuta en el bitmap de resolución completa | Reducir primero: `preprocessingPipeline.Add(new ResizeFilter { Width = 1200 });` |

**Recuerda:** La mejor canalización OCR suele ser un equilibrio entre la calidad de la imagen y el tiempo de procesamiento. Prueba con algunas muestras representativas antes de fijar los ajustes.

## Ejemplo completo y funcional

A continuación se muestra el programa completo, listo para copiar y pegar. Guárdalo como `Program.cs`, restaura el paquete NuGet y ejecútalo.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the source image that needs OCR
        // -------------------------------------------------
        ImageStream imageStream = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.png");

        // -------------------------------------------------
        // Step 2: Build a preprocessing pipeline
        // -------------------------------------------------
        FilterPipeline preprocessingPipeline = new FilterPipeline();

        // Deskew – fix rotation up to 15°
        preprocessingPipeline.Add(new DeskewFilter { MaxAngleDegrees = 15 });

        // Despeckle – remove isolated noise pixels
        preprocessingPipeline.Add(new DespeckleFilter());

        // Optional: Median filter for heavy grain
        // preprocessingPipeline.Add(new MedianFilter { KernelSize = 3 });
{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}