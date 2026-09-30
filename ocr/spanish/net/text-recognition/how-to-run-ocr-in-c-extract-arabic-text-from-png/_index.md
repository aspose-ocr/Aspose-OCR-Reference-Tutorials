---
category: general
date: 2026-01-10
description: Cómo ejecutar OCR rápidamente y extraer texto árabe de una imagen. Aprende
  a convertir imagen a texto, leer texto de PNG y descubre cómo extraer texto con
  Aspose OCR.
draft: false
keywords:
- how to run OCR
- extract arabic text
- convert image to text
- read text from png
- how to extract text
language: es
og_description: Cómo ejecutar OCR en C# y extraer texto árabe de una imagen PNG. Esta
  guía muestra cómo convertir la imagen a texto y leer el texto de un PNG paso a paso.
og_title: Cómo ejecutar OCR en C# – Extraer texto árabe de PNG
tags:
- OCR
- C#
- Aspose
title: Cómo ejecutar OCR en C# – Extraer texto árabe de PNG
url: /es/net/text-recognition/how-to-run-ocr-in-c-extract-arabic-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo ejecutar OCR en C# – Extraer texto árabe de PNG

¿Alguna vez te has preguntado **cómo ejecutar OCR** en una imagen que contiene caracteres árabes? No estás solo. Muchos desarrolladores se quedan atascados cuando necesitan **extraer texto árabe** de un PNG y no saben qué biblioteca manejará scripts de derecha a izquierda sin dolores de cabeza.  

En este tutorial recorreremos todo lo que necesitas saber para **convertir imagen a texto**, **leer texto de PNG**, y finalmente **cómo extraer texto** usando Aspose.OCR en una aplicación de consola C# limpia. Al final tendrás un programa listo‑para‑ejecutar que imprimirá la cadena árabe directamente en tu terminal.

## Qué aprenderás

- Instalar y referenciar el paquete NuGet Aspose.OCR.  
- Configurar el motor OCR para soporte del idioma árabe.  
- Cargar una imagen PNG y ejecutar el proceso de reconocimiento.  
- Recuperar y mostrar el texto extraído.  
- Ajustar configuraciones para mayor precisión y manejar problemas comunes.

No se requiere experiencia previa con OCR, solo un entendimiento básico de C# y un entorno de desarrollo .NET (Visual Studio, Rider, o la CLI `dotnet` será suficiente).

---

## Cómo ejecutar OCR – Configurando Aspose OCR

### Paso 1: Añadir el paquete NuGet Aspose.OCR

Lo primero que necesitamos es la propia biblioteca OCR. Aspose.OCR es un producto comercial, pero ofrece una prueba gratuita que funciona perfectamente para propósitos de aprendizaje.

```bash
# Using the .NET CLI
dotnet add package Aspose.OCR
```

Alternativamente, abre el **NuGet Package Manager** en Visual Studio, busca **Aspose.OCR**, y haz clic en **Install**.

> **Consejo profesional:** Si planeas usar la biblioteca en una canalización CI, añade la bandera `-v` para bloquear la versión, por ejemplo, `dotnet add package Aspose.OCR -v 23.10`.

### Paso 2: Crear un nuevo proyecto de consola (si no tienes uno)

```bash
dotnet new console -n ArabicOcrDemo
cd ArabicOcrDemo
```

Ahora tienes un archivo `Program.cs` fresco listo para nuestro código.

---

## Extraer texto árabe – Escribiendo el código OCR

A continuación tienes el programa completo, listo‑para‑ejecutar. Guárdalo como `Program.cs` (o reemplaza el archivo autogenerado).

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Config;

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine instance
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // Step 2: Choose the language for recognition.
            // Here we use Arabic. You can swap this for
            // OcrLanguage.Korean, OcrLanguage.SerbianCyrillic, etc.
            // -------------------------------------------------
            ocrEngine.Language = OcrLanguage.Arabic;

            // -------------------------------------------------
            // Step 3: Load the image containing the text.
            // Replace the path with the location of your PNG.
            // -------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/arabic_sample.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // Step 4: Run the OCR process.
            // -------------------------------------------------
            ocrEngine.Recognize();

            // -------------------------------------------------
            // Step 5: Display the extracted text.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Arabic Text ===");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

#### Por qué cada línea es importante

- **`OcrEngine`**: La clase central que coordina la carga de la imagen, la selección del idioma y el reconocimiento.  
- **`Language = OcrLanguage.Arabic`**: El árabe usa un script de derecha a izquierda y glifos únicos; establecer el idioma indica al motor que aplique los modelos de caracteres correctos.  
- **`ImageStream.FromFile`**: Maneja PNG, JPEG, BMP y muchos otros formatos. Si alguna vez necesitas leer desde un `MemoryStream` (p. ej., un archivo subido), reemplaza esta llamada en consecuencia.  
- **`Recognize()`**: Realiza el trabajo pesado—análisis de píxeles, segmentación y clasificación de caracteres.  
- **`ocrEngine.Text`**: La cadena Unicode final, lista para procesamiento adicional, almacenamiento o visualización.

### Salida esperada

Si `arabic_sample.png` contiene la frase “مرحبا بالعالم” (Hello World), la consola imprimirá:

```
=== Extracted Arabic Text ===
مرحبا بالعالم
```

Si la salida se ve distorsionada, verifica que la imagen sea clara, que el idioma esté configurado a árabe y que la versión del motor OCR coincida con la documentación.

---

## Convertir imagen a texto – Ajustando la precisión

Aunque la configuración predeterminada funciona para la mayoría de escaneos limpios, las imágenes del mundo real a menudo necesitan un poco de atención extra.

| Configuración | Qué hace | Cuándo usar |
|---------------|----------|-------------|
| `ocrEngine.Config.Preprocess = true` | Habilita binarización automática y eliminación de ruido. | Documentos escaneados con sombras. |
| `ocrEngine.Config.Deskew = true` | Rota la imagen para corregir una ligera inclinación. | Fotos tomadas en ángulo. |
| `ocrEngine.Config.PageSegMode = PageSegMode.SingleBlock` | Trata toda la imagen como un bloque único de texto. | Leyendas simples o etiquetas de una sola línea. |
| `ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزس شصضطظعغفقكلمنهوية"` | Limita el reconocimiento solo a caracteres árabes. | Reduce falsos positivos en páginas multilingües. |

Puedes añadir estas líneas justo después de crear el motor:

```csharp
ocrEngine.Config.Preprocess = true;
ocrEngine.Config.Deskew = true;
ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزسشصضطظعغفقكلمنهوية";
```

---

## Leer texto de PNG – Manejo de diferentes fuentes de imagen

A veces el PNG está almacenado en una base de datos o proviene de una solicitud web. Aquí tienes una variante rápida que lee desde un `byte[]`:

```csharp
byte[] pngBytes = File.ReadAllBytes("YOUR_DIRECTORY/arabic_sample.png");
using var ms = new MemoryStream(pngBytes);
ocrEngine.Image = ImageStream.FromStream(ms);
ocrEngine.Recognize();
Console.WriteLine(ocrEngine.Text);
```

El resto del flujo permanece idéntico, lo que significa que **cómo extraer texto** sigue siendo consistente sin importar la fuente.

---

## Cómo extraer texto – Opciones avanzadas y casos límite

### 1. PDFs o TIFFs de varias páginas

Si necesitas OCR en un documento de varias páginas, itera sobre cada una:

```csharp
var pdfDoc = new Aspose.Pdf.Document("multi_page.pdf");
foreach (var page in pdfDoc.Pages)
{
    using var img = page.ConvertToImage();
    ocrEngine.Image = ImageStream.FromBitmap(img);
    ocrEngine.Recognize();
    Console.WriteLine($"Page {page.Number}: {ocrEngine.Text}");
}
```

> **Nota:** Necesitarás el paquete `Aspose.PDF` para este fragmento.

### 2. Detección automática de idioma

Aspose.OCR también ofrece auto‑detección, pero es más lenta. Si no estás seguro de si la imagen contiene árabe u otro script, habilítala:

```csharp
ocrEngine.Language = OcrLanguage.AutoDetect;
```

El motor probará cada modelo de idioma y elegirá la mejor coincidencia.

### 3. Consejos de rendimiento

- **Reutiliza el objeto `OcrEngine`** para múltiples imágenes; crear una nueva instancia cada vez añade sobrecarga.  
- **Ejecuta en paralelo** solo si tienes instancias de motor separadas por hilo—compartir una única instancia provoca condiciones de carrera.

---

## Conclusión

Hemos cubierto **cómo ejecutar OCR** en C# de principio a fin, mostrándote cómo **extraer texto árabe**, **convertir imagen a texto**, **leer texto de PNG**, y responder **cómo extraer texto** en una variedad de escenarios. El código de ejemplo está completo, autocontenido y listo para que lo pegues en cualquier proyecto de consola .NET.

¿Próximos pasos? Prueba cambiar `OcrLanguage.Arabic` por coreano o serbio cirílico para ver el poder multilingüe de la biblioteca. Experimenta con las banderas de preprocesamiento para mejorar la precisión en escaneos ruidosos, o integra la rutina OCR en una API web para que los usuarios suban imágenes y obtengan resultados de texto al instante.

¡Feliz codificación, y que tus resultados de OCR siempre sean nítidos!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}