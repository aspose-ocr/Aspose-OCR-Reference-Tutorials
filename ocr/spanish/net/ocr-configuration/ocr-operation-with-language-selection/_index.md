---
date: 2025-12-21
description: Aprenda a realizar OCR y extraer texto de una imagen usando Aspose.OCR
  para .NET. Esta guía paso a paso muestra el reconocimiento de texto multilingüe
  y la selección de idioma.
linktitle: How to Perform OCR with Language Selection in Aspose.OCR
second_title: Aspose.OCR .NET API
title: Cómo realizar OCR con selección de idioma en Aspose.OCR
url: /es/net/ocr-configuration/ocr-operation-with-language-selection/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo realizar OCR con selección de idioma en Aspose.OCR

## Introducción

Si necesitas **cómo realizar OCR** en imágenes y extraer texto de archivos de imagen en una aplicación .NET, Aspose.OCR para .NET ofrece una solución rápida, precisa y con reconocimiento de idioma. En este tutorial recorreremos un ejemplo del mundo real que demuestra el reconocimiento de imágenes OCR con selección de idioma, para que puedas obtener texto multilingüe de fotos con solo unas pocas líneas de código.

## Respuestas rápidas
- **¿Qué hace Aspose.OCR?** Reconoce texto impreso y manuscrito en imágenes y devuelve el texto extraído.  
- **¿Puedo elegir el idioma?** Sí, puedes especificar cualquier idioma compatible como English, German, Spanish, Chinese, etc.  
- **¿Necesito una licencia para desarrollo?** Una prueba gratuita funciona para evaluación; se requiere una licencia para uso en producción.  
- **¿Qué versiones de .NET son compatibles?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **¿La corrección de sesgo es automática?** Puedes habilitar `AutoSkew` y ajustar finamente la configuración `SkewAngle`.

## ¿Por qué elegir Aspose.OCR para tareas de OCR?

- **Alta precisión** en múltiples fuentes y calidades de imagen.  
- **Selección de idioma incorporada** que elimina la necesidad de paquetes de idioma externos.  
- **API sencilla** que se integra limpiamente con proyectos C# existentes.  
- **Sin dependencias externas** – todo se ejecuta localmente, manteniendo tus datos seguros.

## Requisitos previos

Antes de sumergirnos en el código, asegúrate de contar con los siguientes requisitos:

- Aspose.OCR para .NET: Verifica que tienes la biblioteca Aspose.OCR instalada. Puedes descargarla desde la [página de descarga de Aspose.OCR para .NET](https://releases.aspose.com/ocr/net/).

- Entorno de desarrollo: Configura un entorno de trabajo con una aplicación .NET. Si aún no lo has hecho, consulta la [documentación](https://reference.aspose.com/ocr/net/) para obtener instrucciones detalladas.

## Importar espacios de nombres

En tu aplicación .NET, comienza importando los espacios de nombres necesarios:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Paso 1: Inicializar Aspose.OCR

Comienza inicializando una instancia de la clase Aspose.OCR. Esto prepara el escenario para utilizar las capacidades de OCR dentro de tu aplicación.

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Paso 2: Especificar la ruta de la imagen

A continuación, define la ruta a la imagen en la que deseas realizar OCR. Asegúrate de que la imagen sea accesible desde tu aplicación.

```csharp
// Image Path
string fullPath = dataDir + "sample.png";
```

## Paso 3: Reconocer la imagen con selección de idioma

Ahora llega la operación central de OCR. Utiliza la biblioteca Aspose.OCR para reconocer texto de la imagen especificada. Ajusta la configuración de reconocimiento, incluida la selección de idioma.

```csharp
// Recognize image           
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    SkewAngle = 0.2F,
    Language = Language.Eng, // Choose the language: none, eng, deu, por, spa, fra, ita, cze, dan, dum, est, fin, lav, lit, nor, pol, rum, srp_hrv, slk, slv, swe, chi
});
```

## Paso 4: Imprimir y mostrar los resultados

Después de la operación de OCR, imprime y muestra los resultados, incluidos el texto reconocido, áreas, advertencias y la representación JSON.

```csharp
// Print result
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
// ExEnd:1
```

## Problemas comunes y consejos

- **Selección de idioma incorrecta** – Si la salida se ve distorsionada, verifica que la propiedad `Language` coincida con el idioma de la imagen original.  
- **Imágenes sesgadas** – Habilita `AutoSkew` o ajusta manualmente `SkewAngle` para obtener mayor precisión en escaneos inclinados.  
- **Archivos grandes** – Procesa imágenes grandes en fragmentos o reduce la resolución antes de pasarlas a `RecognizeImage` para conservar memoria.

## Conclusión

¡Felicidades! Has aprendido **cómo realizar OCR** con selección de idioma usando Aspose.OCR para .NET. Este tutorial te mostró cómo extraer texto de archivos de imagen, personalizar la configuración de reconocimiento y manejar contenido multilingüe sin esfuerzo.

## Preguntas frecuentes

### Q1: ¿Es Aspose.OCR adecuado para el reconocimiento de texto multilingüe?

A1: Sí, Aspose.OCR admite varios idiomas, proporcionando flexibilidad para tareas de OCR multilingüe.

### Q2: ¿Puedo afinar la configuración de OCR para características específicas de la imagen?

A2: ¡Absolutamente! Ajusta parámetros como el ángulo de sesgo, el reconocimiento de líneas y la detección de áreas para optimizar el OCR en diferentes escenarios.

### Q3: ¿Dónde puedo encontrar soporte adicional o discusiones de la comunidad?

A3: Visita el [foro de Aspose.OCR](https://forum.aspose.com/c/ocr/16) para obtener soporte y participar en discusiones con la comunidad.

### Q4: ¿Hay una prueba gratuita disponible?

A4: Sí, explora la [prueba gratuita](https://releases.aspose.com/) para experimentar las capacidades de Aspose.OCR.

### Q5: ¿Cómo puedo comprar Aspose.OCR para .NET?

A5: Para comprar, visita la [página de compra](https://purchase.aspose.com/buy).

---

**Última actualización:** 2025-12-21  
**Probado con:** Aspose.OCR 24.11 para .NET  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}