---
category: general
date: 2026-05-25
description: Lär dig hur du extraherar text från en bild med ett minimalt ASP.NET
  Core‑API. Ladda upp bild via POST, läs multipart‑formulärdata och utför OCR på bilden.
draft: false
keywords:
- extract text from image
- upload image via post
- read multipart form data
- how to recognize text from image
- perform OCR on image
language: sv
og_description: Extrahera text från bild med ett minimalt ASP.NET Core‑API. Denna
  guide visar hur du laddar upp en bild via POST, läser multipart‑formulärdata och
  utför OCR på bilden.
og_title: Extrahera text från bild i ASP.NET Core – Steg för steg
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
title: Extrahera text från bild i ASP.NET Core Minimal API – Komplett guide
url: /sv/net/text-recognition/extract-text-from-image-in-asp-net-core-minimal-api-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text från bild i ASP.NET Core Minimal API – Komplett guide

Har du någonsin undrat hur man **extraherar text från bild** utan att kämpa med tunga ramverk? Du är inte ensam. Många utvecklare behöver ett snabbt sätt att låta användare släppa en bild och få tillbaka de råa tecknen, oavsett om det handlar om att skanna kvitton, digitalisera handskrivna anteckningar eller driva ett sökindex.

I den här handledningen kommer vi att starta ett litet ASP.NET Core Minimal API som **laddar upp bild via POST**, analyserar *multipart/form‑data*‑payloaden och sedan **utför OCR på bild** med en singleton `OcrEngine`. I slutet har du en fullt körbar app som du kan lägga in i vilket .NET 8‑projekt som helst och börja extrahera text från bild omedelbart.

## Vad du kommer att bygga

- En minimal webbapp som lyssnar på `/ocr`.
- En endpoint som accepterar en bildfil som skickas med en `multipart/form-data` POST‑förfrågan.
- Logik som läser den uppladdade filen, matar den till OCR‑motorn och returnerar ren‑textresultat.
- Valfritt GPU‑accelerationssnutt (kommenterad) för dem med ett kompatibelt kort.

**Förutsättningar**  
- .NET 8 SDK (eller senare).  
- Grundläggande kunskap om C# och kommandoraden.  
- Ett OCR‑bibliotek som exponerar en `OcrEngine`‑klass (exemplet förutsätter ett hypotetiskt NuGet‑paket).

Om du har detta, låt oss dyka ner.

## Steg 1: Ställ in projektet och lägg till OCR‑paketet

Först, skapa ett nytt webbprojekt och hämta OCR‑biblioteket.

```bash
dotnet new web -n ImageOcrApi
cd ImageOcrApi
dotnet add package Awesome.Ocr --version 1.3.0   # replace with your actual OCR package
```

> **Proffstips:** Håll dina beroenden uppdaterade. Nyare versioner ger ofta prestandaförbättringar, särskilt för GPU‑accelererad inferens.

## Steg 2: Registrera en singleton‑OCR‑motor (primär tjänst)

Vi vill ha en enda `OcrEngine`‑instans för hela appen—ingen anledning att starta en ny motor per begäran. Registrera den i builderns service‑container.

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

**Varför en singleton?**  
Att skapa en OCR‑motor kan vara dyrt—tänk på att ladda neurala nätverksvikter i minnet. Genom att återanvända samma instans sparar vi både CPU‑cykler och RAM, vilket ger snabbare svarstider för varje `/ocr`‑anrop.

## Steg 3: Bygg applikationen

Nu materialiserar vi `WebApplication`‑objektet.

```csharp
var app = builder.Build();
```

Den raden ser nästan magisk ut, men under huven kopplar den upp routing, middleware och DI‑containern som vi just konfigurerade.

## Steg 4: Definiera POST‑endpointen – “Ladda upp bild via POST”

Här är hjärtat i handledningen: en endpoint som **laddar upp bild via POST**, läser multipart‑payloaden och överlämnar data till OCR‑motorn.

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

### Genomgång av logiken

| Steg | Vad händer | Varför det är viktigt |
|------|------------|-----------------------|
| **ReadFormAsync** | Tolkar den inkommande *multipart/form-data*‑förfrågan. | Utan detta kan du inte komma åt de uppladdade filerna. |
| **form.Files["image"]** | Hämtar filen vars formulärfält‑namn är `image`. | Säkerställer ett förutsägbart kontrakt för anroparna. |
| **Content‑type check** | Kontrollerar att filen är en bild (t.ex. `image/png`). | Förhindrar att OCR‑motorn kraschar på icke‑bilddata. |
| **Image.FromStream** | Konverterar den råa strömmen till ett `System.Drawing.Image`. | OCR‑biblioteket förväntar sig ett `Image`‑objekt, inte en rå byte‑array. |
| **ocr.Recognize(img)** | Anropar OCR‑motorn för att **känna igen text från bild**. | Detta är det centrala steget **utföra OCR på bild**. |
| **Results.Text** | Skickar tillbaka ren‑text‑svaret. | Ett enkelt, konsumerbart format för nedströms tjänster. |

## Steg 5: Kör API:t

Till sist, starta webbservern.

```csharp
app.Run();
```

När du kör `dotnet run` kommer API:t att lyssna på `http://localhost:5000` (eller en port du väljer). Du kan testa det med `curl`:

```bash
curl -X POST http://localhost:5000/ocr \
  -F "image=@/path/to/receipt.png" \
  -H "Accept: text/plain"
```

**Förväntad output:** Konsolen kommer att skriva ut de igenkända tecknen, t.ex.:

```
Total: $23.45
Date: 2026-05-20
Item A  $12.00
Item B  $11.45
```

Om bilden är suddig eller språket inte stöds kommer OCR‑motorn att returnera en tom sträng eller ett felmeddelande—hantera dessa fall i produktionskod.

## Särskilda fall & bästa praxis

### 1. Stora filer

Standardgränsen för request‑body är 30 MB. För större skanningar kan du behöva justera:

```csharp
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 100 * 1024 * 1024; // 100 MB
});
```

### 2. Asynkron OCR

Vissa OCR‑bibliotek exponerar asynkrona metoder (`RecognizeAsync`). Om ditt gör det, ersätt `ocr.Recognize(img)` med `await ocr.RecognizeAsync(img)` och markera lambda‑uttrycket som `async`.

### 3. Säkerhetsaspekter

- **Validera filstorlek** innan du laddar den i minnet.
- **Sanitera filnamnet** om du någonsin skriver det till disk.
- **Rate‑limit** endpointen för att undvika denial‑of‑service‑attacker.

### 4. GPU‑acceleration

Om du avkommenterar raden `engine.GpuDevice = new GpuDevice(0);` och din hårdvara stödjer CUDA eller DirectML, kommer du märka en tydlig hastighetsökning, särskilt på högupplösta bilder.

## Fullt fungerande exempel

Nedan är den kompletta `Program.cs` som du kan kopiera‑klistra in i ett nytt Minimal API‑projekt.

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

Spara, kör `dotnet run`, och du är redo att **extrahera text från bild** på begäran.

## Slutsats

Vi har gått igenom en **komplett, end‑to‑end‑lösning** för att extrahera text från bild med ASP.NET Core Minimal API. Från projekt‑scaffolding har vi **registrerat en singleton‑OCR‑motor**, byggt en endpoint som **laddar upp bild via POST**, **läser multipart‑form‑data**, och slutligen **utför OCR på bild** för att returnera ren ren‑text.

Från här kan du:

- Lägg till JSON‑omslag för rikare svar.  
- Anslut en databas för att lagra den extraherade texten.  
- Utöka stöd till flera språk (`OcrLanguage.Spanish`, etc.).

Mönstret skalar bra—släng bara samma endpoint i en större mikrotjänst eller exponera den bakom en API‑gateway.

Har du frågor om hantering av PDF‑filer, batch‑behandling eller GPU‑optimering? Lämna en kommentar, och lycka till med kodandet!

## Relaterade handledningar

- [Extrahera text från bild med Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extrahera text från bild – OCR‑optimering med Aspose.OCR för .NET](/ocr/english/net/ocr-optimization/)
- [Extrahera bildtext i C# med språkval med Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}