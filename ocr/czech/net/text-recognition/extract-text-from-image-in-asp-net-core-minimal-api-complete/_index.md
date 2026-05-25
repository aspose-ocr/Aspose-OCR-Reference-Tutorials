---
category: general
date: 2026-05-25
description: Naučte se, jak extrahovat text z obrázku pomocí minimalistického ASP.NET
  Core API. Nahrajte obrázek pomocí POST, načtěte multipart data formuláře a proveďte
  OCR na obrázku.
draft: false
keywords:
- extract text from image
- upload image via post
- read multipart form data
- how to recognize text from image
- perform OCR on image
language: cs
og_description: Extrahujte text z obrázku pomocí minimalistického ASP.NET Core API.
  Tento průvodce ukazuje, jak nahrát obrázek pomocí POST, číst multipart data formuláře
  a provést OCR na obrázku.
og_title: Extrahování textu z obrázku v ASP.NET Core – krok po kroku
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
title: Extrahování textu z obrázku v ASP.NET Core Minimal API – kompletní průvodce
url: /cs/net/text-recognition/extract-text-from-image-in-asp-net-core-minimal-api-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahování textu z obrázku v ASP.NET Core Minimal API – Kompletní průvodce

Už jste se někdy zamýšleli, jak **extrahovat text z obrázku** bez zbytečného boje s těžkými frameworky? Nejste sami. Mnoho vývojářů potřebuje rychlý způsob, jak uživatelům umožnit nahrát obrázek a získat zpět surové znaky, ať už jde o skenování účtenek, digitalizaci ručně psaných poznámek nebo napájení vyhledávacího indexu.

V tomto tutoriálu vytvoříme malou ASP.NET Core Minimal API, která **nahrává obrázek pomocí POST**, zpracuje *multipart/form‑data* payload a následně **provádí OCR na obrázku** pomocí singletonu `OcrEngine`. Na konci budete mít plně funkční aplikaci, kterou můžete vložit do libovolného .NET 8 projektu a okamžitě začít extrahovat text z obrázku.

## Co vytvoříte

- Minimální webovou aplikaci naslouchající na `/ocr`.
- Endpoint, který přijímá soubor obrázku odeslaný pomocí `multipart/form-data` POST požadavku.
- Logiku, která načte nahraný soubor, předá jej OCR enginu a vrátí výsledek jako prostý text.
- Volitelný úryvek pro akceleraci pomocí GPU (zakomentovaný) pro ty, kteří mají kompatibilní kartu.

**Předpoklady**  
- .NET 8 SDK (nebo novější).  
- Základní znalost C# a práce s příkazovým řádkem.  
- OCR knihovna, která poskytuje třídu `OcrEngine` (ukázka předpokládá hypotetický NuGet balíček).  

Pokud máte vše připravené, pojďme na to.

## Krok 1: Nastavení projektu a přidání OCR balíčku

Nejprve vytvořte nový webový projekt a přidejte OCR knihovnu.

```bash
dotnet new web -n ImageOcrApi
cd ImageOcrApi
dotnet add package Awesome.Ocr --version 1.3.0   # replace with your actual OCR package
```

> **Tip:** Udržujte své závislosti aktuální. Novější verze často přinášejí výkonnostní zlepšení, zejména u inference akcelerované GPU.

## Krok 2: Registrace singletonu OCR Engine (hlavní služba)

Potřebujeme jedinou instanci `OcrEngine` pro celou aplikaci – není nutné spouštět nový engine pro každý požadavek. Zaregistrujte ji v kontejneru služeb builderu.

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

**Proč singleton?**  
Vytvoření OCR enginu může být nákladné – například načítání vah neuronové sítě do paměti. Opakovaným používáním stejné instance šetříme jak CPU cykly, tak RAM, což se projeví rychlejšími odezvami pro každý volání `/ocr`.

## Krok 3: Sestavení aplikace

Nyní materializujeme objekt `WebApplication`.

```csharp
var app = builder.Build();
```

Ten řádek vypadá téměř magicky, ale pod povrchem propojuje routování, middleware a DI kontejner, který jsme právě nakonfigurovali.

## Krok 4: Definice POST endpointu – „Nahrát obrázek pomocí POST“

Tady je jádro tutoriálu: endpoint, který **nahrává obrázek pomocí POST**, načte multipart payload a předá data OCR enginu.

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

### Rozbor logiky

| Krok | Co se děje | Proč je to důležité |
|------|------------|---------------------|
| **ReadFormAsync** | Parsuje příchozí *multipart/form-data* požadavek. | Bez toho nemůžete přistupovat k nahraným souborům. |
| **form.Files["image"]** | Načte soubor, jehož název pole ve formuláři je `image`. | Zajišťuje předvídatelný kontrakt pro volající. |
| **Kontrola Content‑type** | Ověřuje, že soubor je obrázek (např. `image/png`). | Zabraňuje tomu, aby OCR engine selhal na ne‑obrázkových datech. |
| **Image.FromStream** | Převádí surový stream na `System.Drawing.Image`. | OCR knihovna očekává objekt `Image`, ne jen pole bajtů. |
| **ocr.Recognize(img)** | Volá OCR engine k **rozpoznání textu z obrázku**. | Toto je jádro kroku **perform OCR on image**. |
| **Results.Text** | Vrací výsledek jako prostý text. | Jednoduchý, snadno konzumovatelný formát pro downstream služby. |

## Krok 5: Spuštění API

Nakonec spusťte webový server.

```csharp
app.Run();
```

Po spuštění `dotnet run` bude API naslouchat na `http://localhost:5000` (nebo na vámi zvoleném portu). Můžete to otestovat pomocí `curl`:

```bash
curl -X POST http://localhost:5000/ocr \
  -F "image=@/path/to/receipt.png" \
  -H "Accept: text/plain"
```

**Očekávaný výstup:** Konzole vypíše rozpoznané znaky, např.:

```
Total: $23.45
Date: 2026-05-20
Item A  $12.00
Item B  $11.45
```

Pokud je obrázek rozmazaný nebo není podporovaný jazyk, OCR engine vrátí prázdný řetězec nebo chybovou zprávu – v produkčním kódu byste tyto případy měli ošetřit.

## Okrajové případy a osvědčené postupy

### 1. Velké soubory

Výchozí limit těla požadavku je 30 MB. Pro větší skeny možná budete muset upravit:

```csharp
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 100 * 1024 * 1024; // 100 MB
});
```

### 2. Asynchronní OCR

Některé OCR knihovny nabízejí asynchronní metody (`RecognizeAsync`). Pokud je máte, nahraďte `ocr.Recognize(img)` za `await ocr.RecognizeAsync(img)` a označte lambda výraz jako `async`.

### 3. Bezpečnostní úvahy

- **Ověřte velikost souboru** před načtením do paměti.  
- **Sanitizujte název souboru**, pokud jej někdy zapisujete na disk.  
- **Omezte rychlost** (rate‑limit) endpointu, aby se předešlo útokům typu denial‑of‑service.

### 4. Akcelerace pomocí GPU

Pokud odkomentujete řádek `engine.GpuDevice = new GpuDevice(0);` a váš hardware podporuje CUDA nebo DirectML, zaznamenáte výrazné zrychlení, zejména u vysoce rozlišených obrázků.

## Kompletní funkční příklad

Níže je kompletní `Program.cs`, který můžete zkopírovat a vložit do nového Minimal API projektu.

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

Uložte, spusťte `dotnet run` a jste připraveni **extrahovat text z obrázku** na vyžádání.

## Závěr

Prošli jsme **kompletním, end‑to‑end řešením** pro extrahování textu z obrázku pomocí ASP.NET Core Minimal API. Od vytvoření projektu až po **registraci singletonu OCR engine**, vytvoření endpointu, který **nahrává obrázek pomocí POST**, **čte multipart form data** a nakonec **provádí OCR na obrázku** a vrací čistý prostý text.

Dále můžete:

- Přidat JSON obálky pro bohatší odpovědi.  
- Připojit databázi pro ukládání extrahovaného textu.  
- Rozšířit podporu o více jazyků (`OcrLanguage.Spanish` atd.).  

Tento vzor se dobře škáluje – stačí vložit stejný endpoint do většího mikroservisu nebo jej vystavit za API gateway.

Máte otázky ohledně zpracování PDF, hromadného zpracování nebo ladění GPU? Zanechte komentář a šťastné kódování!

## Související tutoriály

- [Extract Text from Image Using Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}