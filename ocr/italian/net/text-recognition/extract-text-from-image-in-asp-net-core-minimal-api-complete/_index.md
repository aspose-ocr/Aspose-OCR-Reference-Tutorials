---
category: general
date: 2026-05-25
description: Scopri come estrarre testo da un'immagine con una API ASP.NET Core minimale.
  Carica l'immagine via POST, leggi i dati multipart del form ed esegui l'OCR sull'immagine.
draft: false
keywords:
- extract text from image
- upload image via post
- read multipart form data
- how to recognize text from image
- perform OCR on image
language: it
og_description: Estrai il testo da un'immagine usando un'API minimal di ASP.NET Core.
  Questa guida mostra come caricare l'immagine tramite POST, leggere i dati multipart/form
  e eseguire l'OCR sull'immagine.
og_title: Estrai testo da un'immagine in ASP.NET Core – Passo dopo passo
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
title: Estrai testo da un'immagine in ASP.NET Core Minimal API – Guida completa
url: /it/net/text-recognition/extract-text-from-image-in-asp-net-core-minimal-api-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrarre Testo da Immagine in ASP.NET Core Minimal API – Guida Completa

Ti sei mai chiesto come **estrarre testo da un'immagine** senza impazzire con framework ingombranti? Non sei l'unico. Molti sviluppatori hanno bisogno di un modo rapido per far caricare all'utente una foto e ottenere subito i caratteri grezzi, sia per la scansione di ricevute, la digitalizzazione di appunti scritti a mano o per alimentare un indice di ricerca.

In questo tutorial creeremo una piccola ASP.NET Core Minimal API che **carica l'immagine via POST**, analizza il payload *multipart/form‑data* e poi **esegue OCR sull'immagine** usando un singleton `OcrEngine`. Alla fine avrai un'app completamente funzionante che potrai inserire in qualsiasi progetto .NET 8 e iniziare subito a estrarre testo da immagine.

## Cosa Costruirai

- Un'app web minimale che ascolta su `/ocr`.
- Un endpoint che accetta un file immagine inviato con una richiesta POST `multipart/form-data`.
- Una logica che legge il file caricato, lo passa al motore OCR e restituisce il risultato in testo semplice.
- Un frammento opzionale per l'accelerazione GPU (commentato) per chi dispone di una scheda compatibile.

**Prerequisiti**  
- .NET 8 SDK (o successivo).  
- Familiarità di base con C# e la riga di comando.  
- Una libreria OCR che espone una classe `OcrEngine` (l'esempio presuppone un pacchetto NuGet ipotetico).  

Se hai tutto questo, immergiamoci.

## Passo 1: Configura il Progetto e Aggiungi il Pacchetto OCR

Per prima cosa, crea un nuovo progetto web e includi la libreria OCR.

```bash
dotnet new web -n ImageOcrApi
cd ImageOcrApi
dotnet add package Awesome.Ocr --version 1.3.0   # replace with your actual OCR package
```

> **Suggerimento:** Mantieni le dipendenze aggiornate. Le versioni più recenti spesso introducono miglioramenti di prestazioni, soprattutto per l'inferenza accelerata da GPU.

## Passo 2: Registra un Singleton OCR Engine (Servizio Principale)

Vogliamo un'unica istanza di `OcrEngine` per tutta l'app—non è necessario creare un nuovo motore per ogni richiesta. Registrala nel contenitore dei servizi del builder.

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

**Perché un singleton?**  
Creare un motore OCR può essere costoso—pensa al caricamento dei pesi della rete neurale in memoria. Riutilizzando la stessa istanza risparmi cicli CPU e RAM, il che si traduce in tempi di risposta più rapidi per ogni chiamata a `/ocr`.

## Passo 3: Costruisci l'Applicazione

Ora materializziamo l'oggetto `WebApplication`.

```csharp
var app = builder.Build();
```

Quella riga sembra quasi magica, ma dietro le quinte collega il routing, il middleware e il contenitore DI che abbiamo appena configurato.

## Passo 4: Definisci l'Endpoint POST – “Carica Immagine via POST”

Ecco il cuore del tutorial: un endpoint che **carica immagine via POST**, legge il payload multipart e passa i dati al motore OCR.

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

### Analisi della Logica

| Passo | Cosa Succede | Perché è Importante |
|------|--------------|----------------------|
| **ReadFormAsync** | Analizza la richiesta *multipart/form-data* in arrivo. | Senza questo non è possibile accedere ai file caricati. |
| **form.Files["image"]** | Recupera il file il cui nome del campo è `image`. | Garantisce un contratto prevedibile per chi chiama l'endpoint. |
| **Controllo Content‑type** | Verifica che il file sia un'immagine (es. `image/png`). | Impedisce al motore OCR di bloccarsi su dati non‑immagine. |
| **Image.FromStream** | Converte lo stream grezzo in un `System.Drawing.Image`. | La libreria OCR si aspetta un oggetto `Image`, non un array di byte. |
| **ocr.Recognize(img)** | Chiama il motore OCR per **riconoscere testo da immagine**. | Questo è il passaggio centrale per **eseguire OCR sull'immagine**. |
| **Results.Text** | Restituisce la risposta in testo semplice. | Un formato semplice e facilmente consumabile da altri servizi. |

## Passo 5: Avvia l'API

Infine, avvia il server web.

```csharp
app.Run();
```

Quando esegui `dotnet run`, l'API ascolterà su `http://localhost:5000` (o su una porta a tua scelta). Puoi testarla con `curl`:

```bash
curl -X POST http://localhost:5000/ocr \
  -F "image=@/path/to/receipt.png" \
  -H "Accept: text/plain"
```

**Output previsto:** la console stamperà i caratteri riconosciuti, ad esempio:

```
Total: $23.45
Date: 2026-05-20
Item A  $12.00
Item B  $11.45
```

Se l'immagine è sfocata o la lingua non è supportata, il motore OCR restituirà una stringa vuota o un messaggio di errore—gestisci questi casi nel codice di produzione.

## Casi Limite & Buone Pratiche

### 1. File di grandi dimensioni

Il limite predefinito del corpo della richiesta è 30 MB. Per scansioni più grandi potresti doverlo modificare:

```csharp
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 100 * 1024 * 1024; // 100 MB
});
```

### 2. OCR Asincrono

Alcune librerie OCR espongono metodi async (`RecognizeAsync`). Se la tua lo fa, sostituisci `ocr.Recognize(img)` con `await ocr.RecognizeAsync(img)` e marca il lambda come `async`.

### 3. Considerazioni di Sicurezza

- **Valida la dimensione del file** prima di caricarlo in memoria.  
- **Sanitizza il nome del file** se lo scrivi su disco.  
- **Limita la frequenza** delle richieste per evitare attacchi di denial‑of‑service.

### 4. Accelerazione GPU

Se decommenti la riga `engine.GpuDevice = new GpuDevice(0);` e il tuo hardware supporta CUDA o DirectML, noterai un notevole aumento di velocità, soprattutto con immagini ad alta risoluzione.

## Esempio Completo

Di seguito trovi il file `Program.cs` completo da copiare‑incollare in un nuovo progetto Minimal API.

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

Salva, esegui `dotnet run` e sei pronto a **estrarre testo da immagine** su richiesta.

## Conclusione

Abbiamo percorso una **soluzione completa, end‑to‑end** per estrarre testo da immagine usando ASP.NET Core Minimal API. Partendo dallo scaffolding del progetto, abbiamo **registrato un singleton OCR engine**, costruito un endpoint che **carica immagine via POST**, **legge i dati multipart** e infine **esegue OCR sull'immagine** restituendo testo pulito.

Da qui puoi:

- Aggiungere wrapper JSON per risposte più ricche.  
- Collegare un database per memorizzare il testo estratto.  
- Estendere il supporto a più lingue (`OcrLanguage.Spanish`, ecc.).  

Il pattern scala bene—basta inserire lo stesso endpoint in un microservizio più grande o esporlo dietro un API gateway.

Hai domande su come gestire PDF, elaborazione batch o ottimizzazione GPU? Lascia un commento, e buona programmazione!

## Tutorial Correlati

- [Extract Text from Image Using Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}