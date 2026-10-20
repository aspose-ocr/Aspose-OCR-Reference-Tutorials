---
category: general
date: 2026-04-11
description: Aprende cómo desactivar OCR en Aspose OCR para C# para ejecutarlo sin
  conexión, extraer texto de una imagen sin internet y cargar correctamente la imagen
  para OCR.
draft: false
keywords:
- how to disable OCR
- extract text from image
- load image for OCR
- offline OCR C#
- Aspose OCR resources
language: es
og_description: Cómo desactivar OCR en Aspose OCR para C# y ejecutarlo sin conexión,
  extraer texto de una imagen sin necesidad de internet y cargar la imagen para OCR
  fácilmente.
og_title: Cómo desactivar OCR en C# – Guía de Aspose OCR sin conexión
tags:
- C#
- OCR
- Aspose
- Offline Processing
title: Cómo desactivar OCR en C# – Guía offline de Aspose OCR
url: /es/net/ocr-configuration/how-to-disable-ocr-in-c-offline-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo desactivar OCR en C# – Guía offline de Aspose OCR

¿Alguna vez te has preguntado **cómo desactivar OCR** cuando necesitas una solución verdaderamente offline? Tal vez estés construyendo una aplicación de escritorio segura que no pueda depender de una conexión de red, o simplemente quieras evitar descargas inesperadas. Sea cual sea el caso, la buena noticia es que Aspose OCR te permite desactivar su obtención automática de recursos, apuntar a una carpeta local y mantener todo en las instalaciones. En este tutorial también verás cómo **extraer texto de una imagen** y **cargar la imagen para OCR** sin contratiempos.

Recorreremos un ejemplo completo, listo para ejecutar, que muestra cada paso: desde la inicialización del motor hasta la impresión del texto japonés reconocido. Sin documentación externa, sin magia oculta; solo código C# puro que puedes incorporar a tu proyecto hoy mismo. Al final sabrás por qué es importante desactivar la función de descarga automática, cómo establecer la ruta de recursos y qué trampas evitar.

## Requisitos previos

- .NET 6.0 (o cualquier versión reciente de .NET) instalado en tu máquina.  
- Paquete NuGet Aspose.OCR for .NET (`Install-Package Aspose.OCR`).  
- Una carpeta que ya contenga los recursos de idioma que necesitas (por ejemplo, el modelo japonés).  
- Un archivo de imagen (`japan_doc.png`) contra el que quieras ejecutar OCR.  

Si te faltan los paquetes de idioma, descárgalos una vez desde el portal de Aspose, descomprímelos en una carpeta como `AsposeOCRResources` y listo. No se producirán más descargas una vez que hayas desactivado la función de descarga automática.

![Cómo desactivar OCR offline](/images/how-to-disable-ocr.png "ilustración de cómo desactivar OCR")

## Paso 1 – Crear la instancia del motor OCR  

Lo primero que haces es instanciar `OcrEngine`. Piensa en este objeto como el cerebro que leerá tu imagen.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class OfflineDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **Por qué es importante:** Sin un motor no puedes configurar nada. El objeto contiene todas las configuraciones, incluido el indicador crucial que le dice a la biblioteca si puede o no acceder a Internet.

## Paso 2 – Desactivar la descarga automática de recursos  

Por defecto Aspose OCR intentará obtener los archivos de idioma faltantes sobre la marcha. Para mantener todo offline, cambia el interruptor `AutoDownloadResources` a `false`.

```csharp
        // Step 2: Disable automatic resource download to work offline
        ocrEngine.Settings.AutoDownloadResources = false;
```

> **Consejo profesional:** Desactivar esto no solo garantiza la privacidad, sino que también acelera la primera ejecución de reconocimiento porque el motor no pierde tiempo verificando actualizaciones.

## Paso 3 – Apuntar a tu carpeta local de recursos  

Ahora indica al motor dónde viven los paquetes de idioma pre‑descargados. Esta es la ruta que configuraste en los requisitos previos.

```csharp
        // Step 3: Point the engine to the folder containing pre‑downloaded resources
        ocrEngine.Settings.ResourcesPath = @"YOUR_DIRECTORY/AsposeOCRResources";
```

> **¿Qué podría fallar?** Si la ruta es incorrecta o falta el archivo de idioma requerido, el motor lanzará una `ResourceNotFoundException`. Verifica la ortografía de la carpeta y que el modelo japonés (`jpn.traineddata`) esté presente.

## Paso 4 – Seleccionar el modelo de idioma local  

Elige el idioma que realmente tienes en disco. En nuestro ejemplo usamos japonés, pero puedes cambiar `Language.Japanese` por cualquier otro idioma que hayas descargado.

```csharp
        // Step 4: Select the language model that is available locally
        ocrEngine.Settings.Language = Language.Japanese;
```

> **Caso límite:** Algunos idiomas requieren diccionarios adicionales (p. ej., chino). Asegúrate de que esos archivos auxiliares también estén en la misma carpeta de recursos.

## Paso 5 – Cargar la imagen para OCR  

Aquí es donde **cargamos la imagen para OCR**. El método `ImageStream.FromFile` lee el archivo en un flujo que Aspose puede procesar.

```csharp
        // Step 5: Load the image you want to recognize
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/japan_doc.png");
```

> **Consejo:** Los formatos compatibles incluyen PNG, JPEG, BMP y TIFF. Si necesitas manejar PDFs, conviértelos primero a imágenes, una página por imagen.

## Paso 6 – Ejecutar el proceso de reconocimiento  

Ahora el motor realmente lee los píxeles y trata de convertirlos en texto.

```csharp
        // Step 6: Run the OCR process
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

> **Por qué este paso puede ser lento:** OCR es intensivo en CPU, especialmente para imágenes de alta resolución. Si el rendimiento es una preocupación, considera reducir la escala de la imagen antes del reconocimiento.

## Paso 7 – Mostrar el texto extraído  

Finalmente, **extraemos texto de la imagen** y lo imprimimos en la consola.

```csharp
        // Step 7: Output the recognized text
        Console.WriteLine(ocrResult.Text);
    }
}
```

Ejecutar el programa debería mostrar los caracteres japoneses que estaban en `japan_doc.png`. Si todo está configurado correctamente, verás un bloque limpio de texto Unicode en tu consola.

### Salida esperada

```
これはサンプルの日本語テキストです。
```

(Tu salida real dependerá del contenido de la imagen.)

## Problemas comunes y cómo evitarlos  

| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| **Falta el archivo de idioma** | `AutoDownloadResources` está en false, por lo que el motor no puede obtenerlo. | Verifica que `ResourcesPath` apunte a la carpeta que contiene `jpn.traineddata`. |
| **Ruta de imagen incorrecta** | `ImageStream.FromFile` lanza `FileNotFoundException`. | Usa rutas absolutas o asegura que el directorio de trabajo esté configurado correctamente. |
| **Formato de imagen no compatible** | Aspose solo lee ciertos formatos. | Convierte tu imagen a PNG o JPEG antes de llamar a `FromFile`. |
| **Falta de memoria con imágenes grandes** | OCR carga la imagen completa en memoria. | Redimensiona o divide la imagen en mosaicos, o incrementa el límite de memoria del proceso. |

## Extensión del ejemplo  

- **Procesamiento por lotes:** Recorre un directorio de imágenes, llama al mismo código de reconocimiento y escribe cada resultado en un archivo `.txt` separado.  
- **Idiomas diferentes:** Reemplaza `Language.Japanese` por `Language.English` (o cualquier otro) después de colocar los archivos de recursos correspondientes.  
- **Preprocesamiento personalizado:** Usa Aspose.Imaging para corregir la inclinación o mejorar el contraste antes de OCR y obtener mayor precisión.

## Conclusión  

Ahora sabes **cómo desactivar OCR** en Aspose OCR para C# y ejecutarlo completamente offline. Al establecer `AutoDownloadResources` en `false`, apuntar el motor a una carpeta local de recursos y **cargar la imagen para OCR** correctamente, puedes **extraer texto de una imagen** sin tocar nunca Internet. Este enfoque es ideal para entornos seguros, pipelines de CI o cualquier escenario donde el acceso a la red sea limitado.

¿Listo para el siguiente paso? Prueba procesar una carpeta completa de PDFs escaneados, experimenta con diferentes paquetes de idioma o integra el resultado de OCR en una base de datos searchable. La configuración offline que has creado hoy es una base sólida para cualquier flujo de trabajo de procesamiento de documentos on‑premises.

¡Feliz codificación, y no dudes en dejar un comentario si encuentras algún obstáculo!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}