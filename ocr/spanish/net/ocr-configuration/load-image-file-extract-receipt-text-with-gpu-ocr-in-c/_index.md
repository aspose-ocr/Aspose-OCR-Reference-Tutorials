---
category: general
date: 2026-02-14
description: Cargar archivo de imagen y extraer texto del recibo usando el motor OCR
  GPU de Aspose. Aprenda a establecer la memoria máxima de GPU, configurar la memoria
  de GPU y ejecutar OCR en la imagen de manera eficiente.
draft: false
keywords:
- load image file
- extract text from receipt
- set max gpu memory
- run OCR on image
- configure gpu memory
language: es
og_description: Cargar archivo de imagen y extraer texto del recibo usando el motor
  OCR GPU de Aspose. Esta guía muestra cómo establecer la memoria máxima de GPU y
  ejecutar OCR en la imagen en C#.
og_title: Cargar archivo de imagen y extraer texto del recibo con OCR GPU en C#
tags:
- C#
- OCR
- Aspose
- GPU
title: Cargar archivo de imagen y extraer texto del recibo con OCR GPU en C#
url: /es/net/ocr-configuration/load-image-file-extract-receipt-text-with-gpu-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cargar archivo de imagen y extraer texto de recibo con OCR GPU en C#

¿Alguna vez necesitaste **cargar archivo de imagen** y extraer el texto exacto de un recibo pero te quedaste atascado en el paso de OCR? No eres el único. En muchas aplicaciones del mundo real—seguidores de gastos, sistemas de inventario, o incluso bots simples de escaneo de recibos—la capacidad de leer rápidamente una imagen de recibo puede ser un factor decisivo.  

¿La buena noticia? Con el motor acelerado por GPU de Aspose.OCR puedes **cargar archivo de imagen**, **establecer la memoria máxima de GPU**, y **ejecutar OCR en la imagen** todo en unas pocas líneas ordenadas de C#. A continuación, recorreremos todo el proceso, desde la configuración de la GPU hasta la impresión del texto plano extraído.

## Lo que aprenderás

* **Cargar archivo de imagen** desde disco usando `ImageStream` de Aspose.
* **Configurar la memoria de GPU** para que el motor nunca consuma más RAM de la que permitas.
* **Ejecutar OCR en la imagen** y extraer cada carácter de un recibo.
* Manejar obstáculos comunes—como errores de falta de memoria o escaneos borrosos.
* Verificar la salida y ajustar la configuración para mayor precisión.

Sin servicios externos, sin trucos oscuros—solo código puro de C# que puedes insertar en cualquier proyecto .NET 6+.

---

## Requisitos previos

Antes de sumergirnos, asegúrate de tener:

* .NET 6 SDK o posterior instalado.
* Una licencia válida de Aspose.OCR (o puedes usar el modo de evaluación gratuito).
* Los paquetes NuGet `Aspose.OCR` y `Aspose.OCR.Gpu` añadidos a tu proyecto.
* Una imagen de muestra de recibo (`receipt.png`) lista en el disco.

Si alguno de esos te resulta desconocido, haz una pausa y instala los paquetes:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

Eso es todo—no se requieren bibliotecas nativas adicionales porque el soporte de GPU está integrado directamente en el paquete NuGet.

---

## Cargar archivo de imagen y preparar el motor GPU

Lo primero que debes hacer es **cargar archivo de imagen** en un `ImageStream`. Este objeto abstrae los detalles del sistema de archivos y le brinda al motor OCR una representación limpia en memoria.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;

// Step 1️⃣: Initialize the GPU‑accelerated engine.
var gpuEngine = new GpuEngine
{
    // Step 2️⃣: Set a safety net for GPU RAM usage.
    // Here we limit the engine to 1024 MB (1 GB). Adjust as needed.
    MaxDeviceMemory = 1024 // MB
};

// Step 3️⃣: Load the receipt image from disk.
var receiptImage = ImageStream.FromFile(@"C:\MyReceipts\receipt.png");

// At this point the image is ready for OCR.
```

**Por qué es importante:**  
*Cargar el archivo de imagen* mediante `ImageStream.FromFile` garantiza que el motor vea los datos de píxeles exactos, preservando DPI y profundidad de color. Omitir este paso o proporcionar un flujo corrupto hará que el OCR omita caracteres o lance excepciones.

> **Consejo profesional:** Si estás manejando archivos subidos por usuarios, envuelve la llamada `FromFile` en un bloque try‑catch y valida primero el tamaño del archivo. Las imágenes grandes pueden agotar la memoria de GPU si no has **configurado la memoria de GPU** correctamente.

---

## Establecer la memoria máxima de GPU para un rendimiento óptimo

Los recursos de GPU son valiosos, especialmente en servidores compartidos o portátiles con VRAM limitada. La propiedad `MaxDeviceMemory` indica a Aspose cuánta memoria de la GPU puede asignar de forma segura.

```csharp
// Example: Restrict to 512 MB for low‑end GPUs.
gpuEngine.MaxDeviceMemory = 512; // MB
```

Cuando **estableces la memoria máxima de GPU**, el motor retrocederá automáticamente al procesamiento por CPU si no puede cumplir la solicitud—evitando bloqueos. Esta es la forma más segura de **configurar la memoria de GPU** sin codificar límites específicos del dispositivo.

**Cuándo ajustar:**  
* Si notas `OutOfMemoryException` durante un procesamiento por lotes intensivo, reduce el límite.  
* Si tus recibos son de alta resolución (¡300 DPI+), aumenta a 2 GB para mantener alta velocidad.

---

## Ejecutar OCR en la imagen para extraer texto del recibo

Ahora la parte divertida—realmente **ejecutar OCR en la imagen** y extraer el texto del recibo. El método `Recognize` devuelve un objeto `OcrResult` que contiene una propiedad `Text` con la salida de texto plano.

```csharp
// Step 4️⃣: Perform OCR.
OcrResult ocrResult = gpuEngine.Recognize(receiptImage);

// Step 5️⃣: Output the extracted text.
Console.WriteLine("=== Receipt Text ===");
Console.WriteLine(ocrResult.Text);
```

La consola mostrará algo como:

```
=== Receipt Text ===
Store: Coffee Corner
Date: 02/13/2026
Item            Qty   Price
Latte           2     $5.00
Muffin          1     $2.50
Total                     $12.50
```

**Por qué funciona:**  
El motor GPU ejecuta un modelo de deep‑learning que ha sido entrenado en una variedad de diseños de documentos. Al proporcionar una imagen limpia y cargada correctamente, le das al modelo la mejor oportunidad de **extraer texto del recibo** con precisión.

---

## Verificar la salida y problemas comunes

Incluso con un motor potente, el OCR no es magia. Aquí hay algunas cosas a tener en cuenta:

| Problema | Causa | Solución |
|----------|-------|----------|
| Caracteres distorsionados | Bajo contraste o imagen borrosa | Pre‑procesar con `ImageProcessor` de Aspose para aumentar el contraste |
| Líneas faltantes | Imagen recortada demasiado estrechamente | Asegúrate de que el recibo encaje completamente dentro de los límites de la imagen |
| Errores de falta de memoria | `MaxDeviceMemory` demasiado bajo para el tamaño de la imagen | Incrementa `MaxDeviceMemory` o reduce la escala de la imagen primero |
| Idioma incorrecto | El recibo contiene texto no inglés | Establece `gpuEngine.Language = OcrLanguage.Spanish;` (o el apropiado) |

Si te encuentras con alguno de estos, la solución rápida es redimensionar la imagen a menos de 2000 px en el lado más largo—esto reduce drásticamente la carga de la GPU sin sacrificar la legibilidad para la mayoría de los recibos.

---

## Ejemplo completo funcional (listo para copiar y pegar)

A continuación se muestra el programa completo, listo para compilar. Reemplaza la ruta del archivo con la ubicación de tu propio recibo.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

class ReceiptOcrDemo
{
    static void Main()
    {
        // 1️⃣ Create GPU‑accelerated engine with a safe memory cap.
        var gpuEngine = new GpuEngine
        {
            MaxDeviceMemory = 1024 // MB – adjust for your hardware
        };

        // 2️⃣ Load the receipt image from disk.
        //    Make sure the path points to a valid PNG/JPEG file.
        var receiptImage = ImageStream.FromFile(@"C:\MyReceipts\receipt.png");

        // 3️⃣ Run OCR – this will automatically use the GPU if available.
        OcrResult ocrResult = gpuEngine.Recognize(receiptImage);

        // 4️⃣ Print the extracted text.
        Console.WriteLine("=== Receipt Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Salida esperada en la consola** (tu recibo será diferente, por supuesto):

```
=== Receipt Text ===
Store: Coffee Corner
Date: 02/13/2026
Item            Qty   Price
Latte           2     $5.00
Muffin          1     $2.50
Total                     $12.50
```

Ejecuta el programa con `dotnet run`. Si ves el texto impreso, felicidades—has **cargado archivo de imagen**, **establecido la memoria máxima de GPU**, y **ejecutado OCR en la imagen** para **extraer texto del recibo**.

---

## Preguntas frecuentes

**P: ¿Esto funciona en máquinas sin GPU dedicada?**  
R: Sí. Aspose.OCR retrocederá elegantemente al modo CPU si no se detecta una GPU compatible. Aún podrás **cargar archivo de imagen** y **ejecutar OCR en la imagen**, solo un poco más lento.

**P: ¿Puedo procesar varios recibos en lote?**  
R: Absolutamente. Envuelve el código de reconocimiento en un bucle `foreach`, pero recuerda reutilizar la misma instancia de `GpuEngine`—esto evita volver a inicializar los recursos de GPU para cada archivo.

**P: ¿Qué pasa si mi recibo está en un idioma distinto al inglés?**  
R: Establece el idioma antes de llamar a `Recognize`:

```csharp
gpuEngine.Language = OcrLanguage.French;
```

## Próximos pasos y temas relacionados

Ahora que dominas lo básico, considera explorar:

* **Ajustar la precisión del OCR** – experimenta con `gpuEngine.RecognitionOptions` como `EnableDeskew` o `ContrastEnhancement`.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}