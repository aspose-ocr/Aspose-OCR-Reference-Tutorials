---
date: 2025-12-17
description: Aprende cómo obtener rectángulos de líneas OCR usando Aspose.OCR para
  .NET para reconocer líneas de texto en imágenes y extraer fácilmente las coordenadas
  de las líneas.
linktitle: Get OCR Line Rectangles for Image Text Lines
second_title: Aspose.OCR .NET API
title: Obtener rectángulos de líneas OCR para las líneas de texto de la imagen
url: /es/net/image-and-drawing-recognition/get-rectangles-for-lines/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Obtener rectángulos de líneas OCR para líneas de texto en imágenes

## Introducción

En este tutorial descubrirás **cómo obtener rectángulos de líneas OCR** con Aspose.OCR para .NET. Al final de la guía podrás **reconocer líneas de texto en una imagen** y **extraer las coordenadas de las líneas** para cada línea detectada, perfecto para procesamiento posterior como análisis de diseño, extracción de datos o renderizado personalizado.

## Respuestas rápidas
- **¿Qué significa “obtener rectángulos de líneas OCR”?** Devuelve los cuadros delimitadores de cada línea de texto detectada en una imagen.  
- **¿Qué método de la API se utiliza?** `AsposeOcr.GetRectangles(..., AreasType.LINES, ...)`.  
- **¿Necesito una licencia?** Una prueba gratuita funciona para desarrollo; se requiere una licencia comercial para producción.  
- **¿Qué formatos de imagen son compatibles?** PNG, JPEG, BMP, TIFF y más.  
- **¿Puedo ejecutarlo en .NET Core?** Sí, Aspose.OCR soporta totalmente .NET Core y .NET 5/6.

## Requisitos previos

Antes de sumergirte en el tutorial, asegúrate de contar con los siguientes requisitos previos:

- Conocimientos básicos de C# y desarrollo .NET.  
- Un entorno de desarrollo integrado (IDE) como Visual Studio.  
- Biblioteca Aspose.OCR para .NET instalada. Puedes descargarla [aquí](https://releases.aspose.com/ocr/net/).  
- Una imagen de ejemplo que contenga texto para el reconocimiento OCR.

## Importar espacios de nombres

Asegúrate de haber importado los espacios de nombres necesarios en tu proyecto. Añade las siguientes líneas al inicio de tu archivo C#:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

Ahora, desglosaremos el proceso de obtener rectángulos para líneas en el reconocimiento OCR de imágenes en pasos fáciles de seguir.

## Paso 1: Configura tu directorio de documentos

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

Reemplaza `"Your Document Directory"` con la ruta real a la carpeta que contiene tu imagen de ejemplo.

## Paso 2: Inicializa Aspose.OCR

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

Crea una instancia de la clase `AsposeOcr` para acceder a la funcionalidad OCR.

## Paso 3: Especifica la ruta de la imagen

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

Define la ruta completa a la imagen sobre la que deseas realizar OCR.

## Paso 4: Reconoce la imagen y obtén los rectángulos

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

El método `GetRectangles` devuelve una lista de objetos `Rectangle`, cada uno representando las coordenadas de una línea de texto detectada. Este es el núcleo de **obtener rectángulos de líneas OCR**.

## Paso 5: Imprime el resultado

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

Imprime las coordenadas de las áreas detectadas en la consola. Verás valores que luego podrás usar para **extraer coordenadas de líneas** para procesamiento personalizado.

## ¿Por qué usar Aspose.OCR para rectángulos de líneas?

- **Alta precisión** – Algoritmos avanzados detectan líneas incluso en imágenes ruidosas o sesgadas.  
- **Multiplataforma** – Funciona en .NET Framework, .NET Core y .NET 5/6.  
- **Sin dependencias externas** – Biblioteca .NET pura, sin DLLs nativas que distribuir.  
- **Salida rica** – Además de los rectángulos de líneas, puedes obtener palabras, caracteres y puntuaciones de confianza.

## Problemas comunes y soluciones

| Problema | Solución |
|----------|----------|
| **No se devuelven rectángulos** | Asegúrate de que la imagen contenga texto claro y horizontal y que se haya especificado `AreasType.LINES`. |
| **Coordenadas incorrectas** | Verifica el DPI de la imagen; las imágenes de baja resolución pueden causar límites inexactos. |
| **Cuello de botella de rendimiento en imágenes grandes** | Redimensiona la imagen a una resolución razonable antes de llamar a `GetRectangles`. |
| **Excepción de licencia** | Usa una licencia de prueba para pruebas; aplica una licencia completa para producción y evitar límites de evaluación. |

## Preguntas frecuentes

### Q1: ¿Puedo usar Aspose.OCR para .NET con cualquier tipo de imagen?

A1: Aspose.OCR admite una amplia gama de formatos de imagen, garantizando flexibilidad en tus aplicaciones OCR.

### Q2: ¿Qué tan precisa es el reconocimiento OCR?

A2: Aspose.OCR aprovecha algoritmos avanzados para alta precisión, lo que lo hace adecuado para varios escenarios de reconocimiento de texto.

### Q3: ¿Hay una versión de prueba disponible?

A3: Sí, puedes explorar las capacidades de Aspose.OCR para .NET con la [prueba gratuita](https://releases.aspose.com/).

### Q4: ¿Dónde puedo encontrar documentación completa?

A4: Consulta la [documentación](https://reference.aspose.com/ocr/net/) para información detallada y guías de uso.

### Q5: ¿Necesitas asistencia o tienes preguntas específicas?

A5: Visita el [foro de Aspose.OCR](https://forum.aspose.com/c/ocr/16) para soporte de la comunidad y discusiones.

## Preguntas frecuentes

**P: ¿Puedo extraer palabras individuales en lugar de líneas completas?**  
R: Sí, usa `AreasType.WORDS` con el mismo método `GetRectangles` para obtener cuadros delimitadores a nivel de palabra.

**P: ¿La API soporta PDFs de varias páginas?**  
R: Convierte cada página del PDF a una imagen primero, luego llama a `GetRectangles` en cada imagen.

**P: ¿Cómo manejo texto rotado?**  
R: Habilita la opción de auto‑rotación en la configuración OCR o pre‑rota la imagen antes del procesamiento.

**P: ¿Hay una forma de obtener puntuaciones de confianza para cada línea?**  
R: Después de obtener los rectángulos, llama a `api.RecognizeImage(...).Lines` para acceder a los objetos de línea que incluyen valores de confianza.

**P: ¿Qué versiones de .NET son compatibles?**  
R: La biblioteca funciona con .NET Framework 4.5+, .NET Core 3.1+ y .NET 5/6.

## Conclusión

¡Felicidades! Has obtenido **rectángulos de líneas OCR** para una imagen usando Aspose.OCR para .NET. Con los cuadros delimitadores en mano, ahora puedes alimentar las coordenadas de líneas en flujos de trabajo posteriores como renderizado personalizado, extracción de datos o análisis de diseño.

---

**Última actualización:** 2025-12-17  
**Probado con:** Aspose.OCR 24.11 for .NET  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}