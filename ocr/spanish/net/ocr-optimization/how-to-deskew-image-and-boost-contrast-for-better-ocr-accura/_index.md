---
category: general
date: 2025-12-30
description: Cómo enderezar la imagen rápidamente y aprender a aumentar el contraste
  mientras se extrae texto de la imagen para mejorar la precisión del OCR.
draft: false
keywords:
- how to deskew image
- how to boost contrast
- extract text from image
- recognize text image
- improve ocr accuracy
language: es
og_description: Cómo enderezar una imagen rápidamente y aprender a aumentar el contraste
  mientras se extrae texto de la imagen para mejorar la precisión del OCR.
og_title: Cómo corregir la inclinación de la imagen y aumentar el contraste para mejorar
  la precisión del OCR
tags:
- OCR
- C#
- Image Processing
title: Cómo enderezar la imagen y mejorar el contraste para una mayor precisión de
  OCR
url: /es/net/ocr-optimization/how-to-deskew-image-and-boost-contrast-for-better-ocr-accura/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo enderezar una imagen y aumentar el contraste para mejorar la precisión del OCR

¿Alguna vez te has preguntado **cómo enderezar una imagen** que proviene de un escáner o un smartphone?  
No estás solo: la mayoría de los desarrolladores se topan con ese problema cuando la foto de origen está un poco inclinada o ruidosa, y el resultado del OCR termina siendo un desastre.

La buena noticia es que con unas pocas líneas de C# puedes enderezar la foto, limpiar el fondo e incluso aumentar el contraste para que el motor lea el texto como un profesional. En esta guía también te mostraremos cómo **extraer texto de una imagen** y **reconocer contenido de imagen de texto** con Aspose.OCR, siempre manteniendo **mejorar la precisión del OCR** como prioridad.

## Qué necesitarás

- **.NET 6.0** o posterior (el código también compila en .NET Framework 4.7+)  
- Paquete NuGet **Aspose.OCR** (versión 23.12 o más reciente) – instala con `dotnet add package Aspose.OCR`  
- Una imagen de ejemplo que esté rotada y ruidosa (p. ej., `noisy_rotated.jpg`)  
- Visual Studio, VS Code o cualquier IDE que prefieras  

Eso es todo: sin bibliotecas nativas adicionales, sin enlaces pesados a OpenCV. Solo código administrado puro.

---

## Paso 1: Configura el proyecto e importa los espacios de nombres

Primero, crea una nueva aplicación de consola y trae los espacios de nombres requeridos al alcance. Este paso es la base de todo lo que sigue.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in later
        }
    }
}
```

**Por qué es importante:**  
`Aspose.OCR` te brinda la clase `OcrEngine`, mientras que `Aspose.OCR.Filters` proporciona filtros de pre‑procesamiento útiles como `DeskewFilter` y `ContrastBoostFilter`. Importarlos al inicio mantiene el código ordenado y le indica al compilador lo que vamos a usar.

---

## Paso 2: Inicializa el motor OCR y añade un filtro de enderezado

Ahora realmente **cómo enderezar una imagen**. El `DeskewFilter` detecta automáticamente el ángulo de rotación (hasta un máximo que tú establezcas) y gira el bitmap de vuelta a la horizontal.

```csharp
// Inside Main()
var ocrEngine = new OcrEngine();

// Deskew: correct up to 15 degrees of rotation
ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 15 });
```

**¿Qué ocurre bajo el capó?**  
El filtro escanea la imagen en busca de la línea horizontal de texto más larga, estima la inclinación y aplica una rotación inversa. Al limitar `MaxAngle` a 15°, evitamos sobre‑corregir imágenes que ya están rectas.

> **Consejo profesional:** Si tus imágenes de origen pueden estar al revés, aumenta `MaxAngle` a 180°; el filtro seguirá encontrando la orientación correcta.

---

## Paso 3: Reduce el ruido con un filtro de desruido

Un escaneo ruidoso puede engañar incluso al motor OCR más inteligente. Añadir un `DenoiseFilter` suaviza los puntos sin borrar los detalles finos.

```csharp
// Denoise: strength ranges from 0 (off) to 1 (max)
ocrEngine.Filters.Add(new DenoiseFilter { Strength = 0.7 });
```

**Por qué lo necesitas:**  
El ruido crea bordes falsos que el algoritmo OCR interpreta como caracteres. Una fuerza de `0.7` es un punto medio para la mayoría de los documentos escaneados; siéntete libre de ajustarla para entradas muy limpias o muy sucias.

---

## Paso 4: Aumenta el contraste – “Cómo aumentar el contraste” en acción

Aquí respondemos a la palabra clave secundaria **cómo aumentar el contraste**. El `ContrastBoostFilter` amplifica la diferencia entre el texto oscuro y el fondo claro, haciendo que las letras resalten.

```csharp
// Contrast boost: level > 1 increases contrast
ocrEngine.Filters.Add(new ContrastBoostFilter { Level = 1.3 });
```

**La lógica:**  
Mayor contraste reduce la probabilidad de que trazos tenues se pierdan. Un nivel de `1.3` funciona bien para documentos típicos negro‑sobre‑blanco; para fotos a color podrías necesitar `1.5` o más.

---

## Paso 5: Ejecuta OCR y extrae el texto

Con la imagen pre‑procesada, finalmente **extraemos texto de la imagen** usando el método `Recognize`. El método devuelve un objeto `OcrResult` que contiene la cadena cruda y los puntajes de confianza.

```csharp
// Perform OCR on the prepared image
var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/noisy_rotated.jpg");

// Output the recognized text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

**Lo que obtienes:**  
`ocrResult.Text` contiene la representación en texto plano de todo lo que el motor pudo leer. Si necesitas confianza a nivel de palabra, explora `ocrResult.Regions`; cada región incluye una propiedad `Confidence`.

---

## Ejemplo completo (listo para copiar‑pegar)

A continuación tienes el programa completo que puedes colocar en `Program.cs`. Asegúrate de que la ruta de la imagen apunte a un archivo real en tu máquina.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Deskew – correct up to 15° rotation
            ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 15 });

            // 3️⃣ Denoise – smooth out speckles (strength 0.7)
            ocrEngine.Filters.Add(new DenoiseFilter { Strength = 0.7 });

            // 4️⃣ Contrast boost – make text pop (level 1.3)
            ocrEngine.Filters.Add(new ContrastBoostFilter { Level = 1.3 });

            // 5️⃣ Recognize the image
            var imagePath = @"YOUR_DIRECTORY\noisy_rotated.jpg";
            var ocrResult = ocrEngine.Recognize(imagePath);

            // 6️⃣ Show the result
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**Salida esperada (ejemplo):**

```
=== OCR Output ===
Invoice #12345
Date: 2024-09-30
Total Amount: $1,250.00
Thank you for your business!
```

Si el resultado se ve desordenado, verifica la calidad de la imagen, ajusta `Strength` o `Level`, o incrementa `MaxAngle` para un enderezado más agresivo.

---

## Preguntas frecuentes y casos límite

### ¿Qué pasa si la imagen está al revés?

Establece `MaxAngle = 180` en el `DeskewFilter`. El filtro detectará una rotación de 180° y la volteará correctamente.

### Mi documento es a color (p. ej., un formulario escaneado con resaltados azules).  

Intenta añadir un `ColorFilter` antes del aumento de contraste, o convierte la imagen a escala de grises manualmente:

```csharp
ocrEngine.Filters.Add(new GrayscaleFilter());
```

### Necesito procesar muchos archivos en lote.

Envuelve la lógica OCR en un bucle `foreach` que recorra un directorio:

```csharp
foreach (var file in Directory.GetFiles(@"C:\Scans", "*.jpg"))
{
    var result = ocrEngine.Recognize(file);
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), result.Text);
}
```

### ¿Cómo conozco la confianza del OCR?

Inspecciona `ocrResult.Regions`:

```csharp
foreach (var region in ocrResult.Regions)
{
    Console.WriteLine($"Text: {region.Text} – Confidence: {region.Confidence:P2}");
}
```

Valores de confianza más altos (cerca de 100 %) suelen indicar que los pasos de pre‑procesamiento fueron exitosos.

---

## Consejos para maximizar la precisión del OCR

| Consejo | Por qué ayuda |
|-----|--------------|
| **Usa formatos de imagen sin pérdida** (PNG, TIFF) | La compresión JPEG puede difuminar bordes, perjudicando el reconocimiento. |
| **Mantén los DPI en 300+** | Más píxeles por carácter le dan al motor más datos para trabajar. |
| **Recorta márgenes irrelevantes** | Reduce el ruido y acelera el procesamiento. |
| **Aplica un umbral binario** (blanco/negro) después del aumento de contraste para documentos de solo texto | Simplifica la imagen a dos colores, lo que la mayoría de los motores OCR adoran. |
| **Prueba primero con una muestra pequeña** | Te permite afinar `Strength` y `Level` antes de escalar. |

---

## Conclusión

Hemos recorrido **cómo enderezar una imagen**, **cómo aumentar el contraste**, y todo el flujo para **extraer texto de una imagen** usando Aspose.OCR. Al encadenar un `DeskewFilter`, `DenoiseFilter` y `ContrastBoostFilter` antes de llamar a `Recognize`, notarás un tangible en **mejorar la precisión del OCR** para la mayoría de los escaneos del mundo real.

Prueba el código, ajusta los parámetros de los filtros según las particularidades de tus documentos y obtendrás texto limpio incluso de las fotos más caóticas en poco tiempo. ¿Quieres ir más allá? Prueba añadir diccionarios específicos por idioma, o pasa la salida por un corrector ortográfico para post‑procesamiento.

¡Feliz codificación, y que tus resultados de OCR sean siempre cristalinos!

--- 

![ejemplo de cómo enderezar imagen](deskew_example.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}