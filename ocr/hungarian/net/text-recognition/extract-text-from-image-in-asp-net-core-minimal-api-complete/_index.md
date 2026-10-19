---
category: general
date: 2026-05-25
description: Tanulja meg, hogyan lehet szöveget kinyerni egy képből egy minimális
  ASP.NET Core API-val. Töltsön fel képet POST-kéréssel, olvassa a multipart űrlap
  adatokat, és hajtson végre OCR-t a képen.
draft: false
keywords:
- extract text from image
- upload image via post
- read multipart form data
- how to recognize text from image
- perform OCR on image
language: hu
og_description: Szöveg kinyerése képből egy minimalista ASP.NET Core API segítségével.
  Ez az útmutató bemutatja, hogyan töltsünk fel képet POST kéréssel, hogyan olvassuk
  a multipart űrlap adatokat, és hogyan hajtsunk végre OCR-t a képen.
og_title: Szöveg kinyerése képből ASP.NET Core-ban – Lépésről lépésre
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
title: Képből szöveg kinyerése ASP.NET Core Minimal API-ban – Teljes útmutató
url: /hu/net/text-recognition/extract-text-from-image-in-asp-net-core-minimal-api-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kép szövegének kinyerése ASP.NET Core Minimal API‑val – Teljes útmutató

Gondolkodtál már azon, hogyan **extract text from image** anélkül, hogy nehéz keretrendszerekkel bajlódnál? Nem vagy egyedül. Sok fejlesztőnek gyors megoldásra van szüksége, hogy a felhasználók egy képet feltölthessenek, és visszakapják a nyers karaktereket, legyen szó számlák beolvasásáról, kézírásos jegyzetek digitalizálásáról vagy keresőindex működtetéséről.

Ebben az útmutatóban egy apró ASP.NET Core Minimal API‑t hozunk létre, amely **uploads image via POST**, feldolgozza a *multipart/form‑data* terhet, majd **perform OCR on image** egy singleton `OcrEngine` segítségével. A végére egy teljesen futtatható alkalmazásod lesz, amelyet bármely .NET 8 projektbe beilleszthetsz, és azonnal elkezdhetsz **extract text from image**.

## Mit fogsz építeni

- Egy minimal web app, amely a `/ocr` útvonalra figyel.
- Egy végpont, amely egy `multipart/form-data` POST kérésben küldött képfájlt fogad.
- Logika, amely beolvassa a feltöltött fájlt, átadja az OCR motornak, és egyszerű szöveges eredményt ad vissza.
- Opcionális GPU gyorsítási kódrészlet (kikommentezve) azok számára, akiknek kompatibilis kártyájuk van.

**Előfeltételek**  
- .NET 8 SDK (vagy újabb).  
- Alapvető ismeretek C#‑ban és a parancssorban.  
- Egy OCR könyvtár, amely egy `OcrEngine` osztályt biztosít (a példa egy hipotetikus NuGet csomagot feltételez).  

Ha ezek megvannak, vágjunk bele.

## 1. lépés: A projekt beállítása és az OCR csomag hozzáadása

Először hozz létre egy új webprojektet, és húzd be az OCR könyvtárat.

```bash
dotnet new web -n ImageOcrApi
cd ImageOcrApi
dotnet add package Awesome.Ocr --version 1.3.0   # replace with your actual OCR package
```

> **Pro tipp:** Tartsd naprakészen a függőségeket. Az újabb verziók gyakran hoznak teljesítményjavulást, különösen a GPU‑gyorsított következtetés esetén.

## 2. lépés: Singleton OCR motor regisztrálása (elsődleges szolgáltatás)

Egyetlen `OcrEngine` példányt szeretnénk az egész alkalmazás számára – nincs szükség új motor indítására kérésenként. Regisztráld a builder szolgáltatáskontejnerében.

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

**Miért singleton?**  
Egy OCR motor létrehozása költséges lehet – gondolj a neurális hálózat súlyainak memóriába töltésére. Az ugyanazon példány újrafelhasználásával CPU‑ciklusokat és RAM‑ot takarítunk meg, ami gyorsabb válaszidőt jelent minden `/ocr` hívásnál.

## 3. lépés: Az alkalmazás felépítése

Most megvalósítjuk a `WebApplication` objektumot.

```csharp
var app = builder.Build();
```

Ez a sor szinte varázslatosnak tűnik, de a háttérben felállítja a routingot, a middleware‑t és a DI konténert, amelyet épp konfiguráltunk.

## 4. lépés: A POST végpont definiálása – „Upload Image via POST”

Itt van az útmutató szíve: egy végpont, amely **upload image via POST**, beolvassa a multipart terhet, és átadja az adatot az OCR motornak.

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

### A logika részletezése

| Lépés | Mi történik | Miért fontos |
|------|--------------|----------------|
| **ReadFormAsync** | Feldolgozza a bejövő *multipart/form-data* kérést. | Enélkül nem férhetsz hozzá a feltöltött fájlokhoz. |
| **form.Files["image"]** | Lekéri azt a fájlt, amelynek a form‑field neve `image`. | Biztosítja a hívók számára a kiszámítható szerződést. |
| **Content‑type ellenőrzés** | Ellenőrzi, hogy a fájl kép (pl. `image/png`). | Megakadályozza, hogy az OCR motor ne képes legyen nem‑képadatokon. |
| **Image.FromStream** | Átalakítja a nyers streamet `System.Drawing.Image`‑dé. | Az OCR könyvtár egy `Image` objektumot vár, nem nyers byte‑tömböt. |
| **ocr.Recognize(img)** | Az OCR motor meghívása a **how to recognize text from image**-re. | Ez a fő **perform OCR on image** lépés. |
| **Results.Text** | Visszaküldi az egyszerű szöveges választ. | Egyszerű, fogyasztható formátum a downstream szolgáltatások számára. |

## 5. lépés: Az API futtatása

Végül indítsd el a webkiszolgálót.

```csharp
app.Run();
```

Amikor a `dotnet run` parancsot futtatod, az API a `http://localhost:5000` (vagy általad választott port) címen fog figyelni. Tesztelheted `curl`‑lel:

```bash
curl -X POST http://localhost:5000/ocr \
  -F "image=@/path/to/receipt.png" \
  -H "Accept: text/plain"
```

**Várható kimenet:** A konzol kiírja a felismert karaktereket, például:

```
Total: $23.45
Date: 2026-05-20
Item A  $12.00
Item B  $11.45
```

Ha a kép homályos vagy a nyelv nem támogatott, az OCR motor egy üres stringet vagy hibaüzenetet ad vissza – ezeket az eseteket kezeld a produkciós kódban.

## Szélsőséges esetek és legjobb gyakorlatok

### 1. Nagy fájlok

Az alapértelmezett kérés‑test limit 30 MB. Nagyobb beolvasásokhoz lehet, hogy módosítanod kell:

```csharp
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 100 * 1024 * 1024; // 100 MB
});
```

### 2. Aszinkron OCR

Néhány OCR könyvtár aszinkron metódusokat (`RecognizeAsync`) biztosít. Ha a tiéd is, cseréld le a `ocr.Recognize(img)`‑t `await ocr.RecognizeAsync(img)`‑re, és jelöld a lambda‑t `async`‑ként.

### 3. Biztonsági megfontolások

- **Érvényesítsd a fájlméretet** a memóriába töltés előtt.  
- **Tisztítsd meg a fájlnevet** ha valaha leírod a lemezre.  
- **Rate‑limit** a végpontot a szolgáltatásmegtagadási támadások elkerülése érdekében.

### 4. GPU gyorsítás

Ha kikommentezed a `engine.GpuDevice = new GpuDevice(0);` sort, és a hardvered támogatja a CUDA‑t vagy a DirectML‑t, jelentős sebességnövekedést fogsz látni, különösen nagy felbontású képeknél.

## Teljes működő példa

Az alábbiakban a teljes `Program.cs` található, amelyet beilleszthetsz egy új Minimal API projektbe.

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

Mentsd el, futtasd a `dotnet run`‑t, és készen állsz a **extract text from image** igény szerint.

## Következtetés

Áttekintettünk egy **complete, end‑to‑end solution**‑t a kép szövegének kinyerésére ASP.NET Core Minimal API‑val. A projekt felépítésétől kezdve **registered a singleton OCR engine**, felépítettünk egy végpontot, amely **uploads image via POST**, **read multipart form data**, és végül **perform OCR on image**, hogy tiszta egyszerű szöveget adjon vissza.

Innen tovább:

- Adj hozzá JSON burkolókat a gazdagabb válaszokért.  
- Csatlakoztass egy adatbázist a kinyert szöveg tárolásához.  
- Bővítsd a támogatást több nyelvre (`OcrLanguage.Spanish`, stb.).  

A minta jól skálázható – egyszerűen helyezd el ugyanazt a végpontot egy nagyobb mikroszolgáltatásba, vagy tedd elérhetővé egy API gateway mögött.

Van kérdésed a PDF‑ek kezelésével, kötegelt feldolgozással vagy GPU hangolással kapcsolatban? Írj egy megjegyzést, és jó kódolást!

## Kapcsolódó útmutatók

- [Kép szövegének kinyerése Aspose.OCR .NET használatával](/ocr/english/net/image-and-drawing-recognition/)
- [Kép szövegének kinyerése – OCR optimalizálás Aspose.OCR .NET‑hez](/ocr/english/net/ocr-optimization/)
- [Kép szövegének kinyerése C#‑ben nyelvválasztással Aspose.OCR használatával](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}