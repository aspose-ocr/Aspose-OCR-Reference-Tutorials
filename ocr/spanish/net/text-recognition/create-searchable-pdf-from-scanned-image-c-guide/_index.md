---
category: general
date: 2026-04-26
description: Crea un PDF buscable a partir de una imagen escaneada usando Aspose OCR
  en C#. Aprende cómo convertir la imagen escaneada, extraer texto y generar rápidamente
  un PDF buscable.
draft: false
keywords:
- create searchable pdf
- convert scanned image
- extract text from image
- how to ocr document
- convert tiff to pdf
language: es
og_description: Crea un PDF buscable a partir de una imagen escaneada usando Aspose
  OCR. Código C# paso a paso para convertir, extraer texto y generar un PDF buscable.
og_title: Crear PDF buscable a partir de una imagen escaneada – Guía de C#
tags:
- Aspose OCR
- C#
- PDF
- OCR
title: Crear PDF buscable a partir de una imagen escaneada – Guía C#
url: /es/net/text-recognition/create-searchable-pdf-from-scanned-image-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear PDF buscable a partir de imagen escaneada – Guía C#  

¿Alguna vez necesitaste **crear PDF buscables** a partir de contratos en papel, recibos o archivos antiguos? No estás solo—la mayoría de los desarrolladores se topan con ese obstáculo cuando un cliente entrega una pila de escaneos TIFF y espera un PDF buscable como entregable final.  

En este tutorial te mostraremos exactamente **cómo hacer OCR a un documento** y convertir una imagen escaneada en un **PDF buscable** con Aspose OCR para .NET. Al final podrás **convertir imágenes escaneadas**, **extraer texto de imágenes** y manejar TIFF de varias páginas sin sudar.  

## Lo que necesitarás  

* .NET 6.0 o posterior (la API funciona con .NET Core, .NET Framework y .NET 5+).  
* Una licencia válida de Aspose OCR o estar satisfecho con la marca de agua de evaluación.  
* El paquete NuGet `Aspose.OCR` instalado (`dotnet add package Aspose.OCR`).  
* Un archivo TIFF de ejemplo (p.ej., `contract_scan.tif`) que deseas convertir en un PDF buscable.  

Eso es todo—sin bibliotecas extra, sin configuraciones complicadas. ¿Listo? Vamos.  

![Crear ejemplo de PDF buscable](create-searchable-pdf.png "crear ejemplo de pdf buscable")  

## Paso 1 – Inicializar el motor OCR (Crear PDF buscable)  

Lo primero es lo primero: necesitas una instancia de `OcrEngine`. Este objeto es el motor que lee el mapa de bits, identifica los caracteres y te devuelve el texto.  

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine which language to look for – Latin works for most English documents
ocrEngine.Language = Language.Latin;
```  

**¿Por qué establecer el idioma?**  
Si lo dejas en el valor predeterminado, Aspose intentará todos los paquetes de idioma, lo que ralentiza el proceso. Especificar `Language.Latin` indica al motor que se centre en el alfabeto latino, dándote un aumento de velocidad y resultados más precisos para contratos en inglés.  

## Paso 2 – Cargar tu imagen escaneada (Convertir imagen escaneada)  

Ahora alimentamos al motor con la imagen que queremos procesar. Aspose puede leer una ruta de archivo, un flujo o incluso un `byte[]`. Para simplificar usaremos `ImageStream.FromFile`.  

```csharp
// Load the TIFF (or any supported image format)
ocrEngine.Image = ImageStream.FromFile(@"C:\Docs\contract_scan.tif");
```  

Si alguna vez necesitas **convertir TIFF a PDF** más adelante, ten en cuenta que los TIFF de varias páginas se manejan automáticamente—cada fotograma se convierte en una página PDF separada.  

## Paso 3 – Ejecutar OCR y obtener el texto (Extraer texto de la imagen)  

Ejecutar OCR es tan fácil como llamar a `Recognize`. El motor devolverá un `RecognitionResult` que contiene el texto plano, los puntajes de confianza y la información de diseño.  

```csharp
// Perform the OCR operation
RecognitionResult result = ocrEngine.Recognize();

// The raw text is available via the Text property
string extractedText = result.Text;

// Quick sanity check – print the first 200 characters
Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));
```  

**Consejo profesional:** Si solo necesitas el texto (sin PDF), puedes detenerte aquí y escribir `extractedText` en un archivo `.txt`. Pero la mayoría de las veces nuestro objetivo es un PDF buscable, así que continuaremos.  

## Paso 4 – Guardar como PDF buscable (Crear PDF buscable)  

Aspose hace que el paso final sea trivial: simplemente llama a `Save` con `SaveFormat.PdfSearchable`. Internamente la biblioteca incrusta el texto extraído como una capa invisible mientras preserva la apariencia original de la imagen.  

```csharp
// Save the result as a searchable PDF
ocrEngine.Save(@"C:\Docs\contract_searchable.pdf", SaveFormat.PdfSearchable);
```  

Cuando abras `contract_searchable.pdf` en cualquier visor de PDF, podrás seleccionar, copiar y buscar el texto—exactamente lo que un cliente espera de un “PDF buscable”.  

## Manejo de TIFF de varias páginas (Convertir TIFF a PDF)  

Si tu archivo de origen contiene varias páginas, Aspose tratará cada fotograma como una página separada automáticamente. No se requieren bucles extra. Sin embargo, podrías querer controlar el DPI o la calidad de imagen para cada página:  

```csharp
// Optional: tweak image processing settings before OCR
ocrEngine.ImageProcessingOptions.Dpi = 300; // higher DPI improves accuracy
ocrEngine.ImageProcessingOptions.Compression = ImageCompression.Jpeg;
```  

Después de establecer estas opciones, repite el **Paso 2** para cada fotograma, o simplemente apunta `ImageStream.FromFile` al TIFF de varias páginas y deja que Aspose haga el trabajo pesado.  

## Problemas comunes y cómo solucionarlos  

| Síntoma | Causa probable | Solución |
|---------|----------------|----------|
| El texto está distorsionado o falta | Idioma incorrecto configurado | Establece `ocrEngine.Language` al paquete de idioma correcto (p.ej., `Language.German`). |
| El PDF es enorme (10 MB para un escaneo de una sola página) | La compresión de imagen predeterminada es baja | Ajusta `ocrEngine.ImageProcessingOptions.Compression` a `Jpeg` y establece un valor razonable de `Quality` (0‑100). |
| El OCR se ejecuta muy lentamente | Uso de la detección de idioma `Auto` predeterminada | Establece explícitamente el idioma que esperas. |
| No aparece capa buscable | Guardado con `SaveFormat.Pdf` en lugar de `PdfSearchable` | Usa `PdfSearchable`. |

## Ejemplo completo de principio a fin  

Juntando todo, aquí tienes una aplicación de consola lista para ejecutar que puedes copiar y pegar en Visual Studio:  

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.Latin,
                // Optional: improve accuracy for low‑resolution scans
                ImageProcessingOptions = { Dpi = 300, Compression = ImageCompression.Jpeg }
            };

            // 2️⃣ Load the scanned image (convert scanned image)
            string inputPath = @"C:\Docs\contract_scan.tif";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Run OCR and extract text (extract text from image)
            RecognitionResult result = ocrEngine.Recognize();
            Console.WriteLine("First 200 characters of extracted text:");
            Console.WriteLine(result.Text.Substring(0, Math.Min(200, result.Text.Length)));

            // 4️⃣ Save as searchable PDF (create searchable pdf)
            string outputPath = @"C:\Docs\contract_searchable.pdf";
            ocrEngine.Save(outputPath, SaveFormat.PdfSearchable);
            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```  

**Lo que verás:**  
* Una ventana de consola que imprime un fragmento del texto OCRado.  
* Un archivo `contract_searchable.pdf` ubicado junto a tu TIFF original. Ábrelo, presiona **Ctrl + F**, y busca cualquier palabra que aparezca en el escaneo original—voilà, funciona.  

## Próximos pasos y temas relacionados  

* **Cómo hacer OCR a lotes de documentos** – envuelve el código anterior en un bucle `foreach` y procesa una carpeta completa.  
* **Convertir imágenes escaneadas** a formatos distintos de TIFF (PNG, JPEG) – la misma API funciona; solo cambia la extensión del archivo.  
* **Extraer texto de la imagen** para análisis posterior – pasa `result.Text` a una canalización de procesamiento de lenguaje natural.  
* **Optimizar el tamaño del PDF** – explora `PdfSaveOptions` para comprimir más las imágenes o incrustar fuentes solo cuando sea necesario.  

Experimenta con esas ideas, y rápidamente te convertirás en la persona de referencia para cualquier solicitud de “convertir este escaneo en un PDF buscable”.  

---  

### TL;DR  

Ahora sabes cómo **crear PDF buscables** a partir de imágenes escaneadas usando Aspose OCR en C#. El proceso es: inicializar el motor, cargar la imagen, ejecutar OCR y guardar con `PdfSearchable`. Ajusta la configuración de idioma, DPI y compresión para manejar casos extremos, y estarás listo para **convertir imágenes escaneadas**, **extraer texto de imágenes**, e incluso **convertir TIFF a PDF** a gran escala. ¡Feliz codificación!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}