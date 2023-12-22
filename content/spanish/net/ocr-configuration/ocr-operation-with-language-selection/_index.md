---
title: OCROperación con selección de idioma en reconocimiento de imágenes OCR
linktitle: OCROperación con selección de idioma en reconocimiento de imágenes OCR
second_title: API Aspose.OCR .NET
description: Desbloquee potentes capacidades de OCR con Aspose.OCR para .NET. Extraiga texto de imágenes sin problemas.
type: docs
weight: 12
url: /es/net/ocr-configuration/ocr-operation-with-language-selection/
---
## Introducción

En el mundo del reconocimiento de imágenes y el reconocimiento óptico de caracteres (OCR), Aspose.OCR para .NET se destaca como una herramienta poderosa para los desarrolladores que buscan una extracción de texto precisa y eficiente a partir de imágenes. Esta guía paso a paso lo guiará a través del proceso de reconocimiento de imágenes OCR utilizando Aspose.OCR para .NET, centrándose en la operación con la selección de idioma.

## Requisitos previos

Antes de profundizar en el tutorial, asegúrese de cumplir con los siguientes requisitos previos:

-  Aspose.OCR para .NET: asegúrese de tener instalada la biblioteca Aspose.OCR. Puedes descargarlo desde el[Página de descarga de Aspose.OCR para .NET](https://releases.aspose.com/ocr/net/).

- Entorno de desarrollo: Configure un entorno de trabajo con una aplicación .NET. Si aún no lo ha hecho, consulte la[documentación](https://reference.aspose.com/ocr/net/) para obtener instrucciones detalladas.

## Importar espacios de nombres

En su aplicación .NET, comience importando los espacios de nombres necesarios:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Paso 1: Inicializar Aspose.OCR

Comience inicializando una instancia de la clase Aspose.OCR. Esto prepara el escenario para utilizar las capacidades de OCR dentro de su aplicación.

```csharp
// ExInicio:1
// La ruta al directorio de documentos.
string dataDir = "Your Document Directory";

// Inicializar una instancia de AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Paso 2: especificar la ruta de la imagen

A continuación, defina la ruta a la imagen en la que desea realizar el OCR. Asegúrese de que se pueda acceder a la imagen desde su aplicación.

```csharp
//Ruta de la imagen
string fullPath = dataDir + "sample.png";
```

## Paso 3: reconocer la imagen con la selección de idioma

Ahora viene la operación principal de OCR. Utilice la biblioteca Aspose.OCR para reconocer texto de la imagen especificada. Ajuste la configuración de reconocimiento, incluida la selección de idioma.

```csharp
// Reconocer imagen
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    SkewAngle = 0.2F,
    Language = Language.Eng, // Elija el idioma: none, eng, deu, por, spa, fra, ita, cze, dan, dum, est, fin, lav, lit, nor, pol, rum, srp_hrv, slk, slv, swe, chi.
});
```

## Paso 4: imprimir y mostrar resultados

Después de la operación de OCR, imprima y muestre los resultados, incluido el texto reconocido, áreas, advertencias y representación JSON.

```csharp
// Imprimir resultado
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
// Fin final: 1
```

## Conclusión

¡Felicidades! Ha realizado con éxito el reconocimiento de imágenes OCR con selección de idioma utilizando Aspose.OCR para .NET. Este tutorial demostró los pasos esenciales para extraer texto de imágenes y destacó la flexibilidad de las opciones de idioma.

## Preguntas frecuentes

### P1: ¿Aspose.OCR es adecuado para el reconocimiento de texto multilingüe?

R1: Sí, Aspose.OCR admite varios idiomas, lo que brinda flexibilidad para tareas de OCR multilingües.

### P2: ¿Puedo ajustar la configuración de OCR para características de imagen específicas?

R2: ¡Absolutamente! Ajuste parámetros como el ángulo de inclinación, el reconocimiento de líneas y la detección de área para optimizar el OCR para diferentes escenarios.

### P3: ¿Dónde puedo encontrar apoyo adicional o debates comunitarios?

 A3: Visita el[Foro Aspose.OCR](https://forum.aspose.com/c/ocr/16) para apoyo y discusiones con la comunidad.

### P4: ¿Hay una prueba gratuita disponible?

 R4: Sí, explora el[prueba gratis](https://releases.aspose.com/) para experimentar las capacidades de Aspose.OCR.

### P5: ¿Cómo puedo comprar Aspose.OCR para .NET?

 R5: Para comprar, visite el[pagina de compra](https://purchase.aspose.com/buy).
