---
category: general
date: 2026-05-25
description: Leer hoe je tekst uit een afbeelding kunt extraheren met een minimale
  ASP.NET Core‑API. Upload de afbeelding via POST, lees multipart‑formuliagegevens
  en voer OCR uit op de afbeelding.
draft: false
keywords:
- extract text from image
- upload image via post
- read multipart form data
- how to recognize text from image
- perform OCR on image
language: nl
og_description: Tekst extraheren uit een afbeelding met een minimale ASP.NET Core
  API. Deze gids laat zien hoe je een afbeelding uploadt via POST, multipart form‑data
  leest en OCR op de afbeelding uitvoert.
og_title: Tekst uit afbeelding extraheren in ASP.NET Core – Stap voor stap
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
title: Tekst uit afbeelding extraheren in ASP.NET Core Minimal API – Complete gids
url: /nl/net/text-recognition/extract-text-from-image-in-asp-net-core-minimal-api-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tekst uit afbeelding extraheren in ASP.NET Core Minimal API – Complete gids

Heb je je ooit afgevraagd hoe je **tekst uit afbeelding** kunt extraheren zonder te worstelen met zware frameworks? Je bent niet de enige. Veel ontwikkelaars hebben een snelle manier nodig om gebruikers een foto te laten uploaden en de ruwe tekens terug te krijgen, of het nu gaat om het scannen van bonnetjes, het digitaliseren van handgeschreven notities, of het voeden van een zoekindex.

In deze tutorial zetten we een kleine ASP.NET Core Minimal API op die **afbeelding uploadt via POST**, de *multipart/form‑data* payload verwerkt, en vervolgens **OCR op afbeelding uitvoert** met een singleton `OcrEngine`. Aan het einde heb je een volledig werkende app die je in elk .NET 8‑project kunt plaatsen en meteen tekst uit afbeelding kunt extraheren.

## Wat je gaat bouwen

- Een minimale webapp die luistert op `/ocr`.
- Een endpoint dat een afbeeldingsbestand accepteert dat wordt verzonden met een `multipart/form-data` POST‑verzoek.
- Logica die het geüploade bestand leest, het aan de OCR‑engine doorgeeft en platte‑tekstresultaten retourneert.
- Optioneel GPU‑versnellingsfragment (uitgecommentarieerd) voor degenen met een compatibele kaart.

**Prerequisites**  
- .NET 8 SDK (of later).  
- Basiskennis van C# en de commandoregel.  
- Een OCR‑bibliotheek die een `OcrEngine`‑klasse exposeert (het voorbeeld gaat uit van een hypothetisch NuGet‑pakket).  

Als je dat hebt, laten we erin duiken.

## Stap 1: Het project opzetten en het OCR‑pakket toevoegen

Maak eerst een nieuw webproject aan en haal de OCR‑bibliotheek binnen.

```bash
dotnet new web -n ImageOcrApi
cd ImageOcrApi
dotnet add package Awesome.Ocr --version 1.3.0   # replace with your actual OCR package
```

> **Pro tip:** Houd je afhankelijkheden up‑to‑date. Nieuwere versies brengen vaak prestatieverbeteringen, vooral voor GPU‑versnelde inferentie.

## Stap 2: Registreer een Singleton OCR‑Engine (Primaire service)

We willen één `OcrEngine`‑instantie voor de hele app—geen noodzaak om per verzoek een nieuwe engine te starten. Registreer deze in de servicecontainer van de builder.

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

**Waarom een singleton?**  
Het creëren van een OCR‑engine kan duur zijn—denk aan het laden van neurale‑netwerkgewichten in het geheugen. Door dezelfde instantie te hergebruiken besparen we zowel CPU‑cycli als RAM, wat zich vertaalt naar snellere responstijden voor elke `/ocr`‑aanroep.

## Stap 3: Bouw de applicatie

Nu materialiseren we het `WebApplication`‑object.

```csharp
var app = builder.Build();
```

Die regel lijkt bijna magisch, maar onder de motorkap zet het routing, middleware en de DI‑container die we zojuist hebben geconfigureerd op elkaar.

## Stap 4: Definieer de POST‑endpoint – “Afbeelding uploaden via POST”

Hier is het hart van de tutorial: een endpoint die **afbeelding uploadt via POST**, de multipart‑payload leest, en de gegevens aan de OCR‑engine doorgeeft.

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

### De logica ontleden

| Stap | Wat gebeurt er | Waarom het belangrijk is |
|------|----------------|--------------------------|
| **ReadFormAsync** | Parseert het binnenkomende *multipart/form-data* verzoek. | Zonder dit kun je geen toegang krijgen tot de geüploade bestanden. |
| **form.Files["image"]** | Haalt het bestand op waarvan de form‑field naam `image` is. | Garandeert een voorspelbaar contract voor aanroepers. |
| **Content‑type check** | Verifieert dat het bestand een afbeelding is (bijv. `image/png`). | Voorkomt dat de OCR‑engine vastloopt op niet‑afbeeldingsdata. |
| **Image.FromStream** | Converteert de ruwe stream naar een `System.Drawing.Image`. | De OCR‑bibliotheek verwacht een `Image`‑object, niet een ruwe byte‑array. |
| **ocr.Recognize(img)** | Roept de OCR‑engine aan om **tekst uit afbeelding te herkennen**. | Dit is de kernstap **OCR op afbeelding uitvoeren**. |
| **Results.Text** | Stuurt de platte‑tekst respons terug. | Een eenvoudig, bruikbaar formaat voor downstream services. |

## Stap 5: De API draaien

Start tenslotte de webserver.

```csharp
app.Run();
```

Wanneer je `dotnet run` uitvoert, zal de API luisteren op `http://localhost:5000` (of een poort naar keuze). Je kunt het testen met `curl`:

```bash
curl -X POST http://localhost:5000/ocr \
  -F "image=@/path/to/receipt.png" \
  -H "Accept: text/plain"
```

**Verwachte output:** De console zal de herkende tekens afdrukken, bijv.:

```
Total: $23.45
Date: 2026-05-20
Item A  $12.00
Item B  $11.45
```

Als de afbeelding onscherp is of de taal niet wordt ondersteund, zal de OCR‑engine een lege string of een foutmelding teruggeven—handel deze gevallen af in productcode.

## Randgevallen & Best practices

### 1. Grote bestanden

De standaardlimiet voor de request‑body is 30 MB. Voor grotere scans moet je mogelijk aanpassen:

```csharp
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 100 * 1024 * 1024; // 100 MB
});
```

### 2. Asynchrone OCR

Sommige OCR‑bibliotheken bieden async‑methoden (`RecognizeAsync`). Als die van jou dat doet, vervang `ocr.Recognize(img)` door `await ocr.RecognizeAsync(img)` en markeer de lambda als `async`.

### 3. Beveiligingsoverwegingen

- **Valideer de bestandsgrootte** voordat je het in het geheugen laadt.
- **Sanitiseer de bestandsnaam** als je deze ooit naar schijf schrijft.
- **Rate‑limit** de endpoint om denial‑of‑service‑aanvallen te voorkomen.

### 4. GPU‑versnelling

Als je de regel `engine.GpuDevice = new GpuDevice(0);` uitcommentarieert en je hardware ondersteunt CUDA of DirectML, zul je een merkbare snelheidsverbetering zien, vooral bij hoge‑resolutie‑afbeeldingen.

## Volledig werkend voorbeeld

Hieronder staat de volledige `Program.cs` die je kunt copy‑pasten in een nieuw Minimal API‑project.

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

Sla op, voer `dotnet run` uit, en je bent klaar om **tekst uit afbeelding** op aanvraag te extraheren.

## Conclusie

We hebben een **complete, end‑to‑end oplossing** doorlopen voor het extraheren van tekst uit afbeelding met ASP.NET Core Minimal API. Beginnend met het opzetten van het project, hebben we **een singleton OCR‑engine geregistreerd**, een endpoint gebouwd dat **afbeelding uploadt via POST**, **multipart‑form‑data leest**, en uiteindelijk **OCR op afbeelding uitvoert** om schone platte‑tekst terug te geven.

Vanaf hier kun je:

- JSON‑wrappers toevoegen voor rijkere responsen.  
- Een database aansluiten om de geëxtraheerde tekst op te slaan.  
- Ondersteuning uitbreiden naar meerdere talen (`OcrLanguage.Spanish`, enz.).  

Het patroon schaalt goed—zet simpelweg dezelfde endpoint in een grotere microservice of exposeer het achter een API‑gateway.

Heb je vragen over het verwerken van PDF’s, batchverwerking, of GPU‑afstemming? Laat een reactie achter, en happy coding!

## Gerelateerde tutorials

- [Extract Text from Image Using Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}