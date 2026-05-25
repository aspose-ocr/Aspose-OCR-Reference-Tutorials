---
category: general
date: 2026-05-25
description: Erfahren Sie, wie Sie Text aus einem Bild mit einer minimalen ASP.NET Core‑API
  extrahieren. Bild per POST hochladen, Multipart‑Formulardaten lesen und OCR auf
  dem Bild durchführen.
draft: false
keywords:
- extract text from image
- upload image via post
- read multipart form data
- how to recognize text from image
- perform OCR on image
language: de
og_description: Extrahiere Text aus einem Bild mit einer minimalen ASP.NET Core‑API.
  Dieser Leitfaden zeigt, wie man ein Bild per POST hochlädt, Multipart‑Formulardaten
  liest und OCR auf dem Bild durchführt.
og_title: Text aus Bild in ASP.NET Core extrahieren – Schritt für Schritt
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
title: Text aus Bild in ASP.NET Core Minimal API extrahieren – Vollständige Anleitung
url: /de/net/text-recognition/extract-text-from-image-in-asp-net-core-minimal-api-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Text aus Bild in ASP.NET Core Minimal API extrahieren – Vollständige Anleitung

Haben Sie sich jemals gefragt, wie man **Text aus Bild** extrahiert, ohne sich mit schweren Frameworks herumzuschlagen? Sie sind nicht allein. Viele Entwickler benötigen eine schnelle Möglichkeit, Benutzern das Hochladen eines Bildes zu ermöglichen und die rohen Zeichen zurückzubekommen, sei es beim Scannen von Quittungen, der Digitalisierung handgeschriebener Notizen oder beim Betreiben eines Suchindex.

In diesem Tutorial erstellen wir eine kleine ASP.NET Core Minimal API, die **Bild per POST hochlädt**, die *multipart/form‑data* Nutzlast analysiert und dann **OCR auf Bild ausführt** mithilfe einer Singleton‑Instanz `OcrEngine`. Am Ende haben Sie eine vollständig ausführbare Anwendung, die Sie in jedes .NET 8‑Projekt einbinden können und sofort Text aus Bild extrahieren können.

## Was Sie bauen werden

- Eine minimale Web‑App, die auf `/ocr` lauscht.
- Ein Endpunkt, der eine Bilddatei akzeptiert, die mit einer `multipart/form-data` POST‑Anfrage gesendet wird.
- Logik, die die hochgeladene Datei liest, sie an die OCR‑Engine übergibt und reine Text‑Ergebnisse zurückgibt.
- Optionaler GPU‑Beschleunigungs‑Snippet (auskommentiert) für Nutzer mit kompatibler Karte.

**Voraussetzungen**  
- .NET 8 SDK (oder neuer).  
- Grundlegende Kenntnisse in C# und der Befehlszeile.  
- Eine OCR‑Bibliothek, die eine `OcrEngine`‑Klasse bereitstellt (das Beispiel geht von einem hypothetischen NuGet‑Paket aus).

Wenn Sie das haben, lassen Sie uns eintauchen.

## Schritt 1: Projekt einrichten und OCR‑Paket hinzufügen

Zuerst erstellen Sie ein neues Web‑Projekt und binden die OCR‑Bibliothek ein.

```bash
dotnet new web -n ImageOcrApi
cd ImageOcrApi
dotnet add package Awesome.Ocr --version 1.3.0   # replace with your actual OCR package
```

> **Pro Tipp:** Halten Sie Ihre Abhängigkeiten aktuell. Neuere Versionen bringen oft Leistungsverbesserungen, besonders bei GPU‑beschleunigter Inferenz.

## Schritt 2: Singleton‑OCR‑Engine registrieren (Primärdienst)

Wir benötigen eine einzige `OcrEngine`‑Instanz für die gesamte Anwendung – es ist nicht nötig, für jede Anfrage eine neue Engine zu starten. Registrieren Sie sie im Service‑Container des Builders.

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

**Warum ein Singleton?**  
Das Erstellen einer OCR‑Engine kann teuer sein – denken Sie an das Laden von neuronalen Netzwerk‑Gewichten in den Speicher. Durch die Wiederverwendung derselben Instanz sparen wir sowohl CPU‑Zyklen als auch RAM, was zu schnelleren Antwortzeiten für jeden `/ocr`‑Aufruf führt.

## Schritt 3: Anwendung erstellen

Jetzt materialisieren wir das `WebApplication`‑Objekt.

```csharp
var app = builder.Build();
```

Diese Zeile wirkt fast magisch, aber im Hintergrund richtet sie Routing, Middleware und den DI‑Container ein, den wir gerade konfiguriert haben.

## Schritt 4: POST‑Endpunkt definieren – „Bild per POST hochladen“

Hier ist das Herzstück des Tutorials: ein Endpunkt, der **Bild per POST hochlädt**, die multipart‑Nutzlast liest und die Daten an die OCR‑Engine übergibt.

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

### Aufschlüsselung der Logik

| Schritt | Was passiert | Warum es wichtig ist |
|------|--------------|----------------|
| **ReadFormAsync** | Parst die eingehende *multipart/form-data* Anfrage. | Ohne dies können Sie nicht auf die hochgeladenen Dateien zugreifen. |
| **form.Files["image"]** | Ruft die Datei ab, deren Formularfeld‑Name `image` ist. | Garantiert einen vorhersehbaren Vertrag für Aufrufer. |
| **Content‑type check** | Überprüft, ob die Datei ein Bild ist (z. B. `image/png`). | Verhindert, dass die OCR‑Engine bei Nicht‑Bild‑Daten scheitert. |
| **Image.FromStream** | Konvertiert den Roh‑Stream in ein `System.Drawing.Image`. | Die OCR‑Bibliothek erwartet ein `Image`‑Objekt, nicht ein rohes Byte‑Array. |
| **ocr.Recognize(img)** | Ruft die OCR‑Engine auf, um **Text aus Bild zu erkennen**. | Dies ist der zentrale **OCR auf Bild ausführen**‑Schritt. |
| **Results.Text** | Sendet die reine Text‑Antwort zurück. | Ein einfaches, konsumierbares Format für nachgelagerte Dienste. |

## Schritt 5: API ausführen

Zum Schluss starten Sie den Web‑Server.

```csharp
app.Run();
```

Wenn Sie `dotnet run` ausführen, hört die API auf `http://localhost:5000` (oder einem von Ihnen gewählten Port). Sie können sie mit `curl` testen:

```bash
curl -X POST http://localhost:5000/ocr \
  -F "image=@/path/to/receipt.png" \
  -H "Accept: text/plain"
```

**Erwartete Ausgabe:** Die Konsole gibt die erkannten Zeichen aus, z. B.:

```
Total: $23.45
Date: 2026-05-20
Item A  $12.00
Item B  $11.45
```

Wenn das Bild unscharf ist oder die Sprache nicht unterstützt wird, gibt die OCR‑Engine einen leeren String oder eine Fehlermeldung zurück – behandeln Sie diese Fälle im Produktionscode.

## Randfälle & bewährte Methoden

### 1. Große Dateien

Das Standard‑Limit für den Anforderungskörper beträgt 30 MB. Für größere Scans müssen Sie möglicherweise anpassen:

```csharp
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 100 * 1024 * 1024; // 100 MB
});
```

### 2. Asynchrones OCR

Einige OCR‑Bibliotheken stellen asynchrone Methoden bereit (`RecognizeAsync`). Wenn Ihre das tut, ersetzen Sie `ocr.Recognize(img)` durch `await ocr.RecognizeAsync(img)` und markieren Sie das Lambda als `async`.

### 3. Sicherheitsüberlegungen

- **Dateigröße validieren** bevor Sie sie in den Speicher laden.
- **Dateinamen bereinigen**, falls Sie ihn jemals auf die Festplatte schreiben.
- **Rate‑Limiting** des Endpunkts, um Denial‑of‑Service‑Angriffe zu vermeiden.

### 4. GPU‑Beschleunigung

Wenn Sie die Zeile `engine.GpuDevice = new GpuDevice(0);` auskommentieren und Ihre Hardware CUDA oder DirectML unterstützt, werden Sie einen spürbaren Geschwindigkeitszuwachs sehen, besonders bei hochauflösenden Bildern.

## Vollständiges funktionierendes Beispiel

Unten finden Sie das vollständige `Program.cs`, das Sie in ein frisches Minimal‑API‑Projekt kopieren können.

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

Speichern Sie, führen Sie `dotnet run` aus, und Sie sind bereit, **Text aus Bild** bei Bedarf zu extrahieren.

## Fazit

Wir haben eine **vollständige End‑zu‑End‑Lösung** zum Extrahieren von Text aus Bild mit ASP.NET Core Minimal API durchlaufen. Beginnend mit dem Projekt‑Scaffolding haben wir **eine Singleton‑OCR‑Engine registriert**, einen Endpunkt gebaut, der **Bild per POST hochlädt**, **multipart‑Formulardaten liest** und schließlich **OCR auf Bild ausführt**, um sauberen Klartext zurückzugeben.

Von hier aus können Sie:

- JSON‑Wrapper hinzufügen für umfangreichere Antworten.  
- Eine Datenbank einbinden, um den extrahierten Text zu speichern.  
- Unterstützung für mehrere Sprachen erweitern (`OcrLanguage.Spanish`, usw.).

Das Muster skaliert gut – fügen Sie einfach denselben Endpunkt in einen größeren Microservice ein oder stellen Sie ihn hinter einem API‑Gateway bereit.

Haben Sie Fragen zur Verarbeitung von PDFs, Batch‑Verarbeitung oder GPU‑Optimierung? Hinterlassen Sie einen Kommentar, und happy coding!

## Verwandte Tutorials

- [Text aus Bild mit Aspose.OCR .NET extrahieren](/ocr/english/net/image-and-drawing-recognition/)
- [Text aus Bild – OCR‑Optimierung mit Aspose.OCR für .NET](/ocr/english/net/ocr-optimization/)
- [Bildtext in C# mit Sprachauswahl mithilfe von Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}