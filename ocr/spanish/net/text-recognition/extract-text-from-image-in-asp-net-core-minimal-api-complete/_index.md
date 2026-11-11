---
category: general
date: 2026-05-25
description: Aprende a extraer texto de una imagen con una API mínima de ASP.NET Core.
  Sube la imagen mediante POST, lee los datos de formulario multipart y realiza OCR
  en la imagen.
draft: false
keywords:
- extract text from image
- upload image via post
- read multipart form data
- how to recognize text from image
- perform OCR on image
language: es
og_description: Extrae texto de una imagen usando una API mínima de ASP.NET Core.
  Esta guía muestra cómo subir una imagen mediante POST, leer datos de formulario
  multipart y realizar OCR en la imagen.
og_title: Extraer texto de una imagen en ASP.NET Core – Paso a paso
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Learn how to extract text from image with a minimal ASP.NET Core API.
    Upload image via POST, read multipart form data and perform OCR on image.
  headline: Extract Text from Image in ASP.NET Core Minimal API – Complete Guide
  type: TechArticle
- description: Learn how to extract text from image with a minimal ASP.NET Core API.
    Upload image via POST, read multipart form data and perform OCR on image.
  name: Extract Text from Image in ASP.NET Core Minimal API – Complete Guide
  steps:
  - name: Breaking Down the Logic
    text: '| Step | What Happens | Why It Matters | |------|--------------|----------------|
      | **ReadFormAsync** | Parses the incoming *multipart/form-data* request. | Without
      this, you can’t access the uploaded files. | | **form.Files["image"]** | Retrieves
      the file whose form‑field name is `image`. | Guarant'
  - name: 1. Large Files
    text: 'The default request body limit is 30 MB. For larger scans you might need
      to adjust:'
  - name: 2. Asynchronous OCR
    text: Some OCR libraries expose async methods (`RecognizeAsync`). If yours does,
      replace `ocr.Recognize(img)` with `await ocr.RecognizeAsync(img)` and mark the
      lambda as `async`.
  - name: 3. Security Considerations
    text: '- **Validate file size** before loading it into memory. - **Sanitize the
      filename** if you ever write it to disk. - **Rate‑limit** the endpoint to avoid
      denial‑of‑service attacks.'
  - name: 4. GPU Acceleration
    text: If you uncomment the `engine.GpuDevice = new GpuDevice(0);` line and your
      hardware supports CUDA or DirectML, you’ll see a noticeable speed boost, especially
      on high‑resolution images.
  type: HowTo
tags:
- ASP.NET Core
- OCR
- Minimal API
title: Extraer texto de una imagen en ASP.NET Core Minimal API – Guía completa
url: /es/net/text-recognition/extract-text-from-image-in-asp-net-core-minimal-api-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraer texto de una imagen en ASP.NET Core Minimal API – Guía completa

¿Alguna vez te has preguntado cómo **extraer texto de una imagen** sin lidiar con frameworks pesados? No estás solo. Muchos desarrolladores necesitan una forma rápida de permitir a los usuarios soltar una foto y obtener de vuelta los caracteres crudos, ya sea escaneando recibos, digitalizando notas manuscritas o alimentando un índice de búsqueda.

En este tutorial crearemos una pequeña ASP.NET Core Minimal API que **carga imágenes mediante POST**, analiza la carga *multipart/form‑data* y luego **realiza OCR en la imagen** usando un `OcrEngine` singleton. Al final tendrás una aplicación completamente ejecutable que puedes incorporar a cualquier proyecto .NET 8 y comenzar a extraer texto de imágenes de inmediato.

## Lo que construirás

- Una aplicación web mínima que escucha en `/ocr`.
- Un endpoint que acepta un archivo de imagen enviado con una solicitud POST `multipart/form-data`.
- Lógica que lee el archivo cargado, lo pasa al motor OCR y devuelve resultados en texto plano.
- Fragmento opcional de aceleración GPU (comentado) para quienes tengan una tarjeta compatible.

**Requisitos previos**  
- .NET 8 SDK (o posterior).  
- Familiaridad básica con C# y la línea de comandos.  
- Una biblioteca OCR que exponga una clase `OcrEngine` (el ejemplo asume un paquete NuGet hipotético).  

Si tienes eso, vamos a sumergirnos.

## Paso 1: Configurar el proyecto y agregar el paquete OCR

Primero, crea un nuevo proyecto web e incorpora la biblioteca OCR.

```bash
dotnet new web -n ImageOcrApi
cd ImageOcrApi
dotnet add package Awesome.Ocr --version 1.3.0   # replace with your actual OCR package
```

> **Consejo profesional:** Mantén tus dependencias actualizadas. Las versiones más recientes a menudo aportan mejoras de rendimiento, especialmente para inferencia acelerada por GPU.

## Paso 2: Registrar un motor OCR singleton (servicio principal)

Queremos una única instancia de `OcrEngine` para toda la aplicación—no es necesario crear un nuevo motor por solicitud. Regístralo en el contenedor de servicios del builder.

```csharp
using Awesome.Ocr;               // <-- the OCR library namespace
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Http;
using System.Drawing;            // System.Drawing.Common for Image handling

var builder = WebApplication.CreateBuilder(args);

// Register a singleton OCR engine (English language)
// Uncomment the GPU line if you have a compatible GPU and the library supports it.
builder.Services.AddSingleton<OcrEngine>(sp =>
{
    var engine = new OcrEngine { Language = OcrLanguage.English };
    // engine.GpuDevice = new GpuDevice(0); // enable GPU acceleration
    return engine;
});
```

**¿Por qué un singleton?**  
Crear un motor OCR puede ser costoso—piensa en cargar los pesos de una red neuronal en memoria. Al reutilizar la misma instancia ahorramos ciclos de CPU y RAM, lo que se traduce en tiempos de respuesta más rápidos para cada llamada a `/ocr`.

## Paso 3: Construir la aplicación

Ahora materializamos el objeto `WebApplication`.

```csharp
var app = builder.Build();
```

Esa línea parece casi mágica, pero bajo el capó configura el enrutamiento, el middleware y el contenedor DI que acabamos de configurar.

## Paso 4: Definir el endpoint POST – “Cargar imagen mediante POST”

Este es el corazón del tutorial: un endpoint que **carga una imagen mediante POST**, lee la carga multipart y entrega los datos al motor OCR.

```csharp
app.MapPost("/ocr", async (HttpRequest request, OcrEngine ocr) =>
{
    // Step 5: Read multipart form data and extract the uploaded image
    var form = await request.ReadFormAsync();               // <-- read multipart/form-data
    var file = form.Files["image"];                         // expects a field named "image"

    if (file is null || file.Length == 0)
    {
        return Results.BadRequest("No image file provided.");
    }

    // Guard against unsupported content types
    if (!file.ContentType.StartsWith("image/"))
    {
        return Results.BadRequest("Uploaded file is not an image.");
    }

    // Load the image into a System.Drawing.Image
    using var img = Image.FromStream(file.OpenReadStream());

    // Step 6: Perform OCR on the image
    string text = ocr.Recognize(img);                       // <-- perform OCR on image

    // Step 7: Return the extracted text as plain‑text
    return Results.Text(text);
});
```

### Desglosando la lógica

| Paso | Qué ocurre | Por qué es importante |
|------|------------|-----------------------|
| **ReadFormAsync** | Analiza la solicitud *multipart/form-data* entrante. | Sin esto, no puedes acceder a los archivos cargados. |
| **form.Files["image"]** | Obtiene el archivo cuyo nombre de campo de formulario es `image`. | Garantiza un contrato predecible para los llamadores. |
| **Content‑type check** | Verifica que el archivo sea una imagen (p.ej., `image/png`). | Evita que el motor OCR se bloquee con datos que no son imágenes. |
| **Image.FromStream** | Convierte el flujo bruto en un `System.Drawing.Image`. | La biblioteca OCR espera un objeto `Image`, no un arreglo de bytes bruto. |
| **ocr.Recognize(img)** | Llama al motor OCR para **reconocer texto de la imagen**. | Este es el paso central de **realizar OCR en la imagen**. |
| **Results.Text** | Envía de vuelta la respuesta en texto plano. | Un formato simple y consumible para servicios posteriores. |

## Paso 5: Ejecutar la API

Finalmente, inicia el servidor web.

```csharp
app.Run();
```

Cuando ejecutas `dotnet run`, la API escuchará en `http://localhost:5000` (o en el puerto que elijas). Puedes probarla con `curl`:

```bash
curl -X POST http://localhost:5000/ocr \
  -F "image=@/path/to/receipt.png" \
  -H "Accept: text/plain"
```

**Salida esperada:** La consola imprimirá los caracteres reconocidos, por ejemplo:

```
Total: $23.45
Date: 2026-05-20
Item A  $12.00
Item B  $11.45
```

Si la imagen está borrosa o el idioma no está soportado, el motor OCR devolverá una cadena vacía o un mensaje de error—maneja esos casos en código de producción.

## Casos límite y buenas prácticas

### 1. Archivos grandes

El límite predeterminado del cuerpo de la solicitud es 30 MB. Para escaneos más grandes podrías necesitar ajustar:

```csharp
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 100 * 1024 * 1024; // 100 MB
});
```

### 2. OCR asíncrono

Algunas bibliotecas OCR exponen métodos async (`RecognizeAsync`). Si la tuya lo hace, reemplaza `ocr.Recognize(img)` por `await ocr.RecognizeAsync(img)` y marca la lambda como `async`.

### 3. Consideraciones de seguridad

- **Validar el tamaño del archivo** antes de cargarlo en memoria.
- **Sanitizar el nombre del archivo** si alguna vez lo escribes en disco.
- **Limitar la tasa** del endpoint para evitar ataques de denegación de servicio.

### 4. Aceleración GPU

Si descomentas la línea `engine.GpuDevice = new GpuDevice(0);` y tu hardware soporta CUDA o DirectML, notarás un aumento de velocidad significativo, especialmente en imágenes de alta resolución.

## Ejemplo completo en funcionamiento

A continuación se muestra el `Program.cs` completo que puedes copiar y pegar en un nuevo proyecto Minimal API.

```csharp
using Awesome.Ocr;
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Http.Features;
using System.Drawing;

var builder = WebApplication.CreateBuilder(args);

// Optional: increase multipart limit for big images
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 50 * 1024 * 1024; // 50 MB
});

// Register the OCR engine as a singleton
builder.Services.AddSingleton<OcrEngine>(sp =>
{
    var engine = new OcrEngine { Language = OcrLanguage.English };
    // engine.GpuDevice = new GpuDevice(0); // enable GPU if available
    return engine;
});

var app = builder.Build();

app.MapPost("/ocr", async (HttpRequest request, OcrEngine ocr) =>
{
    var form = await request.ReadFormAsync();
    var file = form.Files["image"];

    if (file is null || file.Length == 0)
        return Results.BadRequest("No image file provided.");

    if (!file.ContentType.StartsWith("image/"))
        return Results.BadRequest("Uploaded file is not an image.");

    using var img = Image.FromStream(file.OpenReadStream());

    // Core OCR operation
    string text = ocr.Recognize(img);

    return Results.Text(text);
});

app.Run();
```

Guarda, ejecuta `dotnet run`, y estarás listo para **extraer texto de una imagen** bajo demanda.

## Conclusión

Hemos recorrido una **solución completa, de extremo a extremo** para extraer texto de una imagen usando ASP.NET Core Minimal API. Desde la generación del proyecto, **registramos un motor OCR singleton**, construimos un endpoint que **carga una imagen mediante POST**, **lee datos multipart del formulario**, y finalmente **realiza OCR en la imagen** para devolver texto plano limpio.

Desde aquí puedes:

- Agregar envoltorios JSON para respuestas más ricas.  
- Conectar una base de datos para almacenar el texto extraído.  
- Ampliar el soporte a múltiples idiomas (`OcrLanguage.Spanish`, etc.).  

El patrón escala bien—simplemente inserta el mismo endpoint en un microservicio más grande o expónlo detrás de un gateway API.

¿Tienes preguntas sobre el manejo de PDFs, procesamiento por lotes o afinación de GPU? Deja un comentario, ¡y feliz codificación!

## Tutoriales relacionados

- [Extraer texto de una imagen usando Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extraer texto de una imagen – Optimización OCR con Aspose.OCR para .NET](/ocr/english/net/ocr-optimization/)
- [Extraer texto de imagen en C# con selección de idioma usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}