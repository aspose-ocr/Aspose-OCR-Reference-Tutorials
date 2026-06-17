---
date: 2026-02-22
description: Aprende cómo realizar análisis de diseño OCR reconociendo líneas de texto
  en una imagen y extrayendo rectángulos de línea usando Aspose.OCR para .NET.
linktitle: Layout Analysis OCR – Get Line Rectangles from Images
second_title: Aspose.OCR .NET API
title: Análisis de diseño OCR – Obtener rectángulos de líneas de imágenes
url: /es/net/image-and-drawing-recognition/get-rectangles-for-lines/
weight: 10
---

.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Análisis de Diseño OCR – Obtener Rectángulos de Líneas a partir de Imágenes

## Introducción

En este tutorial descubrirás **cómo obtener los rectángulos de líneas OCR** con Aspose.OCR para .NET. Al final de la guía podrás **reconocer líneas de texto en una imagen** y **extraer las coordenadas de las líneas** para cada línea detectada, ideal para procesamiento posterior como **análisis de diseño OCR**, extracción de datos o renderizado personalizado.

## Respuestas Rápidas
- **¿Qué significa “obtener rectángulos de líneas OCR”?** Devuelve los cuadros delimitadores de cada línea de texto detectada en una imagen.  
- **¿Qué método de la API se utiliza?** `AsposeOcr.GetRectangles(..., AreasType.LINES, ...)`.  
- **¿Necesito una licencia?** Una prueba gratuita funciona para desarrollo; se requiere una licencia comercial para producción.  
- **¿Formatos de imagen compatibles?** PNG, JPEG, BMP, TIFF y más.  
- **¿Puedo ejecutar esto en .NET Core?** Sí, Aspose.OCR soporta totalmente .NET Core y .NET 5/6.

## Requisitos Previos

Antes de profundizar en el tutorial, asegúrate de contar con los siguientes requisitos:

- Conocimientos básicos de C# y desarrollo .NET.  
- Un entorno de desarrollo integrado (IDE) como Visual Studio.  
- Biblioteca Aspose.OCR para .NET instalada. Puedes descargarla [aquí](https://releases.aspose.com/ocr/net/).  
- Una imagen de muestra que contenga texto para el reconocimiento OCR.

## Importar Espacios de Nombres

Asegúrate de haber importado los espacios de nombres necesarios en tu proyecto. Añade las siguientes líneas al inicio de tu archivo C#:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

Ahora, desglosaremos el proceso de obtención de rectángulos para líneas en el reconocimiento OCR de imágenes en pasos fáciles de seguir.

## análisis de diseño ocr – Guía Paso a Paso

### Paso 1: Configurar el Directorio de tu Documento

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

Reemplaza `"Your Document Directory"` con la ruta real a la carpeta que contiene tu imagen de muestra.

### Paso 2: Inicializar Aspose.OCR

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

Crea una instancia de la clase `AsposeOcr` para acceder a la funcionalidad OCR.

### Paso 3: Especificar la Ruta de la Imagen

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

Define la ruta completa a la imagen sobre la que deseas realizar OCR.

### Paso 4: Reconocer la Imagen y Obtener los Rectángulos

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

El método `GetRectangles` devuelve una lista de objetos `Rectangle`, cada uno representando las coordenadas de una línea de texto detectada. Este es el núcleo de **obtener rectángulos de líneas OCR** y permite **análisis de diseño OCR**.

### Paso 5: Imprimir el Resultado

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

Imprime las coordenadas de las áreas detectadas en la consola. Verás valores que podrás usar posteriormente para **extraer coordenadas de líneas** para procesamiento personalizado.

## ¿Por Qué Usar Aspose.OCR para Rectángulos de Líneas?

- **Alta precisión** – Algoritmos avanzados detectan líneas incluso en imágenes ruidosas o sesgadas.  
- **Multiplataforma** – Funciona en .NET Framework, .NET Core y .NET 5/6.  
- **Sin dependencias externas** – Biblioteca pura de .NET, sin DLLs nativas que distribuir.  
- **Salida rica** – Además de los rectángulos de líneas, puedes obtener palabras, caracteres y puntuaciones de confianza.

## Problemas Comunes y Soluciones

| Problema | Solución |
|----------|----------|
| **No se devuelven rectángulos** | Asegúrate de que la imagen contenga texto claro y horizontal y que `AreasType.LINES` esté especificado. |
| **Coordenadas incorrectas** | Verifica el DPI de la imagen; las imágenes de baja resolución pueden producir límites inexactos. |
| **Cuello de botella de rendimiento en imágenes grandes** | Redimensiona la imagen a una resolución razonable antes de llamar a `GetRectangles`. |
| **Excepción de licencia** | Usa una licencia de prueba para pruebas; aplica una licencia completa para producción y evitar límites de evaluación. |

## Preguntas Frecuentes

**P: ¿Puedo extraer palabras individuales en lugar de líneas completas?**  
R: Sí, usa `AreasType.WORDS` con el mismo método `GetRectangles` para obtener cuadros delimitadores a nivel de palabra.

**P: ¿La API soporta PDFs de varias páginas?**  
R: Convierte cada página del PDF a una imagen primero, luego llama a `GetRectangles` en cada imagen.

**P: ¿Cómo manejo texto rotado?**  
R: Habilita la opción de auto‑rotación en la configuración OCR o pre‑rota la imagen antes del procesamiento.

**P: ¿Hay forma de obtener puntuaciones de confianza para cada línea?**  
R: Después de obtener los rectángulos, llama a `api.RecognizeImage(...).Lines` para acceder a los objetos de línea que incluyen valores de confianza.

**P: ¿Qué versiones de .NET son compatibles?**  
R: La biblioteca funciona con .NET Framework 4.5+, .NET Core 3.1+ y .NET 5/6.

## Casos de Uso en el Mundo Real

- **Análisis de diseño de documentos OCR** – Alimenta los rectángulos de líneas a un motor de diseño para reconstruir estructuras de columnas.  
- **Extracción automática de datos** – Usa las coordenadas para recortar líneas individuales y enviarlas a pipelines de NLP posteriores.  
- **Renderizado personalizado** – Superpone los cuadros delimitadores sobre la imagen original para verificación visual o superposiciones en la UI.  

## Conclusión

¡Felicidades! Has obtenido con éxito **rectángulos de líneas OCR** para una imagen usando Aspose.OCR para .NET. Con los cuadros delimitadores en mano, ahora puedes alimentar las coordenadas de líneas a flujos de trabajo posteriores como renderizado personalizado, extracción de datos o **análisis de diseño OCR**.

---

**Última actualización:** 2026-02-22  
**Probado con:** Aspose.OCR 24.11 para .NET  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}