---
category: general
date: 2026-05-25
description: Learn how to extract text from image with a minimal ASP.NET Core API.
  Upload image via POST, read multipart form data and perform OCR on image.
draft: false
keywords:
- extract text from image
- upload image via post
- read multipart form data
- how to recognize text from image
- perform OCR on image
language: en
og_description: Extract text from image using a minimal ASP.NET Core API. This guide
  shows how to upload image via POST, read multipart form data, and perform OCR on
  image.
og_title: Extract Text from Image in ASP.NET Core – Step‑by‑Step
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
title: Extract Text from Image in ASP.NET Core Minimal API – Complete Guide
url: /net/text-recognition/extract-text-from-image-in-asp-net-core-minimal-api-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extract Text from Image in ASP.NET Core Minimal API – Complete Guide

Ever wondered how to **extract text from image** without wrestling with heavyweight frameworks? You’re not alone. Many developers need a quick way to let users drop a picture and get back the raw characters, whether it’s scanning receipts, digitizing handwritten notes, or powering a search index.

In this tutorial we’ll spin up a tiny ASP.NET Core Minimal API that **uploads image via POST**, parses the *multipart/form‑data* payload, and then **perform OCR on image** using a singleton `OcrEngine`. By the end you’ll have a fully runnable app that you can drop into any .NET 8 project and start extracting text from image right away.

## What You’ll Build

- A minimal web app that listens on `/ocr`.
- An endpoint that accepts an image file sent with a `multipart/form-data` POST request.
- Logic that reads the uploaded file, feeds it to the OCR engine, and returns plain‑text results.
- Optional GPU acceleration snippet (commented out) for those with a compatible card.

**Prerequisites**  
- .NET 8 SDK (or later).  
- Basic familiarity with C# and the command line.  
- An OCR library that exposes an `OcrEngine` class (the sample assumes a hypothetical NuGet package).  

If you’ve got those, let’s dive in.

## Step 1: Set Up the Project and Add the OCR Package

First, create a new web project and pull in the OCR library.

```bash
dotnet new web -n ImageOcrApi
cd ImageOcrApi
dotnet add package Awesome.Ocr --version 1.3.0   # replace with your actual OCR package
```

> **Pro tip:** Keep your dependencies up to date. Newer versions often bring performance gains, especially for GPU‑accelerated inference.

## Step 2: Register a Singleton OCR Engine (Primary Service)

We want a single `OcrEngine` instance for the whole app—no need to spin up a new engine per request. Register it in the builder’s service container.

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

**Why a singleton?**  
Creating an OCR engine can be expensive—think loading neural‑network weights into memory. By reusing the same instance we save both CPU cycles and RAM, which translates to faster response times for every `/ocr` call.

## Step 3: Build the Application

Now we materialize the `WebApplication` object.

```csharp
var app = builder.Build();
```

That line looks almost magical, but under the hood it wires up routing, middleware, and the DI container we just configured.

## Step 4: Define the POST Endpoint – “Upload Image via POST”

Here’s the heart of the tutorial: an endpoint that **upload image via POST**, reads the multipart payload, and hands the data to the OCR engine.

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

### Breaking Down the Logic

| Step | What Happens | Why It Matters |
|------|--------------|----------------|
| **ReadFormAsync** | Parses the incoming *multipart/form-data* request. | Without this, you can’t access the uploaded files. |
| **form.Files["image"]** | Retrieves the file whose form‑field name is `image`. | Guarantees a predictable contract for callers. |
| **Content‑type check** | Verifies the file is an image (e.g., `image/png`). | Prevents the OCR engine from choking on non‑image data. |
| **Image.FromStream** | Converts the raw stream into a `System.Drawing.Image`. | The OCR library expects an `Image` object, not a raw byte array. |
| **ocr.Recognize(img)** | Calls the OCR engine to **how to recognize text from image**. | This is the core **perform OCR on image** step. |
| **Results.Text** | Sends back the plain‑text response. | A simple, consumable format for downstream services. |

## Step 5: Run the API

Finally, start the web server.

```csharp
app.Run();
```

When you execute `dotnet run`, the API will listen on `http://localhost:5000` (or a port of your choosing). You can test it with `curl`:

```bash
curl -X POST http://localhost:5000/ocr \
  -F "image=@/path/to/receipt.png" \
  -H "Accept: text/plain"
```

**Expected output:** The console will print the recognized characters, e.g.:

```
Total: $23.45
Date: 2026-05-20
Item A  $12.00
Item B  $11.45
```

If the image is blurry or the language isn’t supported, the OCR engine will return an empty string or an error message—handle those cases in production code.

## Edge Cases & Best Practices

### 1. Large Files

The default request body limit is 30 MB. For larger scans you might need to adjust:

```csharp
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 100 * 1024 * 1024; // 100 MB
});
```

### 2. Asynchronous OCR

Some OCR libraries expose async methods (`RecognizeAsync`). If yours does, replace `ocr.Recognize(img)` with `await ocr.RecognizeAsync(img)` and mark the lambda as `async`.

### 3. Security Considerations

- **Validate file size** before loading it into memory.
- **Sanitize the filename** if you ever write it to disk.
- **Rate‑limit** the endpoint to avoid denial‑of‑service attacks.

### 4. GPU Acceleration

If you uncomment the `engine.GpuDevice = new GpuDevice(0);` line and your hardware supports CUDA or DirectML, you’ll see a noticeable speed boost, especially on high‑resolution images.

## Full Working Example

Below is the complete `Program.cs` you can copy‑paste into a fresh Minimal API project.

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

Save, run `dotnet run`, and you’re ready to **extract text from image** on demand.

## Conclusion

We’ve walked through a **complete, end‑to‑end solution** for extracting text from image using ASP.NET Core Minimal API. Starting from project scaffolding, we **registered a singleton OCR engine**, built an endpoint that **uploads image via POST**, **read multipart form data**, and finally **perform OCR on image** to return clean plain‑text. 

From here you can:

- Add JSON wrappers for richer responses.  
- Plug in a database to store the extracted text.  
- Extend support to multiple languages (`OcrLanguage.Spanish`, etc.).  

The pattern scales nicely—just drop the same endpoint into a larger microservice or expose it behind an API gateway.

Got questions about handling PDFs, batch processing, or GPU tuning? Drop a comment, and happy coding!


## Related Tutorials

- [Extract Text from Image Using Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}