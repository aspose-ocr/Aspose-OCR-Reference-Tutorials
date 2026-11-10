---
category: general
date: 2026-04-04
description: Crear PDF buscable a partir de una imagen TIF en C# – aprende cómo convertir
  la imagen a PDF, agregar metadatos al PDF y generar un documento buscable usando
  Aspose.OCR.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- add metadata to pdf
- add pdf metadata
- create pdf from tif
language: es
og_description: Crear PDF buscable a partir de un archivo TIF con C#. Convertir la
  imagen a PDF, agregar metadatos al PDF y producir un documento buscable usando Aspose.OCR.
og_title: Crear PDF buscable a partir de TIF – Guía paso a paso
tags:
- Aspose.OCR
- C#
- PDF generation
title: Crear PDF buscable a partir de TIF – Convertir imagen a PDF, agregar metadatos
  al PDF
url: /es/net/text-recognition/create-searchable-pdf-from-tif-convert-image-to-pdf-add-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear PDF buscable a partir de TIF – Guía completa en C#

¿Alguna vez necesitaste **crear PDF buscable** a partir de una factura escaneada pero no estabas seguro de cómo mantener el texto buscable y los metadatos del archivo ordenados? No estás solo. En muchos proyectos de automatización el PDF debe ser tanto legible por máquina como correctamente etiquetado con información como título, autor y umbrales de confianza.  

En esta guía recorreremos una solución completa que **convierte una imagen a PDF**, inserta **metadatos PDF**, y filtra resultados OCR de baja confianza, todo con la biblioteca Aspose.OCR. Al final tendrás un fragmento listo para usar que puedes insertar en cualquier proyecto .NET, además de varios consejos para manejar casos extremos.

## Requisitos previos

- .NET 6.0 o posterior (el código también funciona en .NET Framework 4.6+).  
- Paquete NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- Una imagen TIF que deseas convertir en un PDF buscable (p. ej., `input.tif`)  
- Familiaridad básica con C# y Visual Studio (o tu IDE favorito)

No se requieren otros servicios externos: todo el proceso se ejecuta localmente.

## Paso 1 – Configurar el motor OCR (Crear núcleo de PDF buscable)

Lo primero que necesitamos es una instancia de `OcrEngine` que sepa qué idioma reconocer. En la mayoría de los escenarios empresariales el inglés es suficiente, pero puedes cambiar `Language.English` por cualquier idioma admitido.

```csharp
using Aspose.OCR;
using Aspose.OCR.Pdf;   // PDF‑related extensions

// Initialize OCR engine with English language
OcrEngine ocrEngine = new OcrEngine
{
    Language = Language.English
};
```

**Por qué es importante:** El motor OCR realiza el trabajo pesado de convertir píxeles raster a texto Unicode. Configurar el idioma correctamente mejora la precisión y reduce la cantidad de palabras de baja confianza que luego se filtran.

> **Consejo profesional:** Si procesas documentos multilingües, instancia varios motores o usa `Language.Multilingual` para que Aspose detecte automáticamente el idioma.

## Paso 2 – Cargar la imagen TIF (Crear PDF a partir de TIF)

Ahora apuntamos el motor al archivo de origen. El ayudante `ImageStream.FromFile` lee la imagen en un flujo que el motor OCR puede consumir.

```csharp
// Load the TIF image you want to make searchable
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.tif");
```

Puede que te preguntes, *“¿Puedo usar un JPEG o PNG en su lugar?”* Absolutamente—Aspose.OCR admite la mayoría de los formatos raster. Simplemente cambia la extensión del archivo y listo.

## Paso 3 – Configurar opciones PDF (Agregar metadatos al PDF)

Antes de convertir, definimos un objeto `PdfOptions`. Aquí es donde **agregamos metadatos PDF** como título y autor, y también indicamos al motor que elimine palabras cuya confianza esté por debajo de un umbral.

```csharp
PdfOptions searchablePdfOptions = new PdfOptions
{
    Title = "Invoice #12345",
    Author = "MyCompany",
    // Hide words with confidence lower than 0.8 (80%)
    MinConfidence = 0.8f
};
```

**¿Qué está sucediendo aquí?**  
- `Title` y `Author` pasan a formar parte del diccionario de información del documento PDF, facilitando la indexación en sistemas de gestión documental.  
- `MinConfidence` actúa como una barrera de seguridad: OCR a menudo interpreta mal caracteres tenues; filtrarlos mantiene la capa buscable limpia y mejora la extracción de texto posterior.

Si necesitas metadatos personalizados (p. ej., `Subject`, `Keywords`), puedes establecerlos mediante `PdfOptions.CustomProperties`.

## Paso 4 – Convertir la imagen a un PDF buscable (Convertir imagen a PDF)

Con el motor preparado y las opciones definidas, la llamada final realiza la conversión. Escribe un PDF buscable en disco, incrustando la capa de texto OCR bajo la imagen original.

```csharp
ocrEngine.ConvertToSearchablePdf(
    outputPath: @"YOUR_DIRECTORY/output.pdf",
    pdfOptions: searchablePdfOptions);
```

Después de ejecutar esta línea, `output.pdf` contiene:
- La imagen TIF original como fondo visual  
- Una capa de texto invisible que los motores de búsqueda y las operaciones de copiar‑pegar pueden leer  
- Los metadatos que definimos antes (título, autor, etc.)

### Resultado esperado

Abre el PDF generado en Adobe Reader o cualquier visor de PDF y prueba a seleccionar texto. Deberías poder copiar frases que coincidan con el escaneo original. El cuadro de diálogo **Propiedades** del documento mostrará el título “Invoice #12345” y el autor “MyCompany”.

## Paso 5 – Verificar el filtrado de confianza (Por qué MinConfidence ayuda)

Es útil confirmar que las palabras de baja confianza fueron realmente eliminadas. Puedes inspeccionar el texto oculto del PDF usando una herramienta como `pdftotext`:

```bash
pdftotext output.pdf - | grep -i "unlikelyword"
```

Si la palabra nunca aparece, el filtro `MinConfidence` funcionó como se esperaba. Ajusta el umbral (p. ej., `0.7f`) si necesitas un filtro más agresivo o más indulgente.

## Paso 6 – Manejar múltiples páginas (Crear PDF buscable a partir de TIF multipágina)

Muchas facturas vienen como TIFFs multipágina. Aspose.OCR trata cada fotograma como una página separada automáticamente. Simplemente apunta el motor al archivo multipágina; la misma llamada `ConvertToSearchablePdf` generará un PDF buscable multipágina.

```csharp
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/multi_page.tif");
ocrEngine.ConvertToSearchablePdf(@"YOUR_DIRECTORY/multi_output.pdf", searchablePdfOptions);
```

**Caso extremo:** Si una página está en blanco, OCR puede generar aún así una capa de texto vacía, lo cual no causa problemas. Sin embargo, puedes omitir páginas en blanco verificando `ocrEngine.HasText` antes de la conversión.

## Paso 7 – Empaquetar el ejemplo completo (Todos los pasos juntos)

A continuación tienes un programa único, listo para ejecutar, que une todo. Reemplaza `YOUR_DIRECTORY` con la ruta real de la carpeta en tu máquina.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // 2️⃣ Load the TIF image (create pdf from tif)
        string inputPath = @"YOUR_DIRECTORY/input.tif";
        ocrEngine.Image = ImageStream.FromFile(inputPath);

        // 3️⃣ Set PDF metadata and confidence filter
        PdfOptions pdfOptions = new PdfOptions
        {
            Title = "Invoice #12345",
            Author = "MyCompany",
            MinConfidence = 0.8f
        };

        // 4️⃣ Convert to searchable PDF (convert image to pdf)
        string outputPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.ConvertToSearchablePdf(outputPath, pdfOptions);

        Console.WriteLine($"✅ Searchable PDF created at: {outputPath}");
    }
}
```

Ejecuta el programa (`dotnet run` o pulsa **F5** en Visual Studio) y verás el mensaje de confirmación. El PDF generado quedará junto a tu imagen de origen, listo para indexar o archivar.

## Preguntas frecuentes y trucos

| Pregunta | Respuesta |
|----------|-----------|
| **¿Puedo agregar una fuente personalizada a la capa buscable?** | La capa OCR usa Unicode; la apariencia visual está determinada por la imagen subyacente, por lo que no se requiere incrustar fuentes adicionales. |
| **¿Qué pasa si mi TIF está en color?** | Aspose.OCR convierte automáticamente las imágenes en color a escala de grises para OCR, pero puedes conservar los colores originales en el PDF estableciendo `PdfOptions.PreserveColor = true`. |
| **¿La biblioteca es segura para subprocesos?** | Cada instancia de `OcrEngine` debe usarse en un solo subproceso. Para procesamiento paralelo, crea un motor separado por subproceso. |
| **¿Cómo encripto el PDF?** | Usa `PdfOptions.Security` para establecer una contraseña y permisos después de la conversión OCR. |

## Próximos pasos (Amplía tu kit de herramientas PDF)

- **Procesamiento por lotes:** Recorre una carpeta de TIFFs y genera un PDF buscable para cada uno.  
- **Post‑procesamiento:** Usa Aspose.PDF para combinar los PDFs generados en un documento maestro único.  
- **Metadatos avanzados:** Rellena campos XMP personalizados para una mejor integración con SharePoint o sistemas ECM.  

Todas estas extensiones se basan en el patrón central que acabamos de cubrir: **crear PDF buscable**, **convertir imagen a PDF** y **agregar metadatos PDF**.

---

*¡Feliz codificación! Si encuentras algún inconveniente, deja un comentario abajo o consulta la documentación de Aspose.OCR para conocer las últimas actualizaciones de la API.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}