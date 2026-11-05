---
category: general
date: 2026-02-09
description: Estrai il testo da un'immagine usando OCR offline in C#. Un esempio completo
  di OCR in C# mostra come caricare l'immagine per l'OCR, riconoscere il testo cirillico
  ed estrarre il testo dal passaporto.
draft: false
keywords:
- extract text from image
- c# ocr example
- load image for ocr
- recognize cyrillic text
- recognize text from passport
language: it
og_description: Estrai il testo da un'immagine con OCR offline in C#. Impara un esempio
  passo‑passo di OCR in C# che carica un'immagine per l'OCR, riconosce il testo cirillico
  ed estrae il testo da un passaporto.
og_title: Estrai testo da un'immagine in C# – Guida OCR offline
tags:
- OCR
- C#
- Aspose
title: Estrai testo da immagine in C# – Esempio di OCR offline
url: /it/net/text-recognition/extract-text-from-image-in-c-offline-ocr-example/
---








{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai Testo da Immagine in C# – Esempio OCR Offline

Hai mai dovuto **estrarre testo da immagine** ma ti sei bloccato con API dipendenti dalla rete? Non sei solo. Molti sviluppatori si trovano in difficoltà quando il servizio OCR tenta di scaricare i pacchetti linguistici a runtime, soprattutto in ambienti restrittivi.

In questa guida percorreremo un **c# ocr example** che funziona interamente offline, carica un'immagine per l'OCR e riconosce testo cirillico da un passaporto. Alla fine avrai un programma pronto all'uso che stampa il contenuto in testo semplice di qualsiasi immagine supportata direttamente sulla console.

## Cosa Imparerai

- Come configurare Aspose.OCR per l'elaborazione offline.  
- Il codice esatto per **caricare immagine per OCR** dal disco.  
- Come configurare il motore per **riconoscere testo cirillico**.  
- Un **c# ocr example** completo, pronto per copia‑incolla, che estrae testo da una foto in stile passaporto.  

Non è necessaria alcuna esperienza precedente con Aspose; basta un SDK .NET 6 (o successivo) e Visual Studio 2022 (o VS Code).

---

![Extract text from image using Aspose OCR on a passport photo](/images/ocr-passport.jpg "extract text from image")

## Passo 1: Configura il Progetto per Estrarre Testo da Immagine

Before writing any code, make sure the Aspose.OCR NuGet package is added to your project:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Use the `--version` flag to lock to the latest stable release (e.g., `13.9.0`). This guarantees compatibility with .NET 6.

Creating a new console app is as simple as:

```bash
dotnet new console -n OfflineOcrDemo
cd OfflineOcrDemo
```

Now you have a clean slate where we’ll **extract text from image** without ever touching the internet.

## Passo 2: Carica Immagine per OCR – Lettura della Foto del Passaporto

The first thing the OCR engine needs is a bitmap or stream representing the picture. In our scenario we’ll **load image for OCR** from a local file called `cyrillic_passport.jpg`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

// Step 2: Load the image file (this is the “load image for ocr” part)
var imagePath = @"YOUR_DIRECTORY\cyrillic_passport.jpg";

// Validate the file exists – helpful when the path is wrong.
if (!System.IO.File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// ImageStream abstracts the underlying format; it works with JPEG, PNG, etc.
var image = ImageStream.FromFile(imagePath);
```

> **Why this matters:** Supplying a stream rather than a raw `Bitmap` lets Aspose handle format detection internally, reducing boilerplate and potential bugs.

## Passo 3: Configura Modalità Offline e Scegli la Lingua Cirillica

Aspose.OCR can download language models on‑the‑fly, but that defeats the purpose of an offline solution. Turn off network calls and explicitly tell the engine which language to use.

```csharp
// Step 3: Create the OCR engine and switch to offline mode
var ocrEngine = new OcrEngine
{
    Configuration =
    {
        OfflineMode = true,               // No network traffic – perfect for secure environments
        Language = new[] { OcrLanguage.Cyrillic } // We want to **recognize cyrillic text**
    }
};
```

> **Edge case:** If you later need to recognise Latin characters in the same document, just add `OcrLanguage.English` to the array. The engine will handle multi‑language detection automatically.

## Passo 4: Esegui il Motore OCR e Riconosci Testo Cirillico

Now we actually **recognize text from passport**‑style images. The `Recognize` method returns a rich result object containing the plain text, confidence scores, and bounding boxes.

```csharp
// Step 4: Perform the OCR operation
OcrResult result = ocrEngine.Recognize(image);

// Step 5: Output the plain text – this is where we finally **extract text from image**
Console.WriteLine("📝 Extracted Text:");
Console.WriteLine("-------------------");
Console.WriteLine(result.PlainText);
```

### Output Atteso della Console

```
📝 Extracted Text:
-------------------
ПАСПОРТ РФ
Иванов Иван Иванович
01.01.1990
...
```

If the result looks garbled, double‑check that the source image is clear and that the `OfflineMode` language pack for Cyrillic is present in the Aspose installation folder (usually `\Aspose.OCR\resources\languages`).

## Esempio Completo C# OCR – Codice Sorgente Completo

Below is the **c# ocr example** in its entirety. Copy‑paste it into `Program.cs` and run `dotnet run`. Everything you need to **extract text from image** is right here.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

class OfflineExample
{
    static void Main()
    {
        // --------------------------------------------------------------
        // Step 1: Create the OCR engine (offline mode)
        // --------------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Configuration =
            {
                OfflineMode = true,                     // No network calls
                Language = new[] { OcrLanguage.Cyrillic } // Recognize Cyrillic text
            }
        };

        // --------------------------------------------------------------
        // Step 2: Load the image for OCR (passport photo)
        // --------------------------------------------------------------
        var imagePath = @"YOUR_DIRECTORY\cyrillic_passport.jpg";

        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"❌ Image not found at {imagePath}");
            return;
        }

        var image = ImageStream.FromFile(imagePath);

        // --------------------------------------------------------------
        // Step 3: Recognize the text
        // --------------------------------------------------------------
        var result = ocrEngine.Recognize(image);

        // --------------------------------------------------------------
        // Step 4: Output the plain text (the final extraction)
        // --------------------------------------------------------------
        Console.WriteLine("📝 Extracted Text:");
        Console.WriteLine("-------------------");
        Console.WriteLine(result.PlainText);
    }
}
```

### Esecuzione dell'Esempio

```bash
dotnet run
```

You should see the console print the passport details in Cyrillic. That’s the moment you know your **extract text from image** pipeline works.

## Problemi Comuni & Come Risolverli

| Sintomo | Causa Probabile | Soluzione |
|---------|-----------------|-----------|
| `PlainText` vuoto | Modello linguistico errato o immagine troppo scura | Assicurati che il linguaggio `OfflineMode` includa `Cyrillic` e aumenta il contrasto dell'immagine |
| `System.DllNotFoundException` | Binari nativi Aspose OCR mancanti | Re‑installa il pacchetto NuGet o copia `Aspose.OCR.Native.dll` nella cartella di output |
| Prestazioni lente su immagini grandi | Il motore elabora la risoluzione completa | Ridimensiona l'immagine a ≤ 1500 px di larghezza prima di passarla a `ImageStream` |
| Caratteri illeggibili | Immagine ruotata in modo errato | Usa `Image.RotateFlip(RotateFlipType.Rotate90FlipNone)` prima di creare lo stream |

## Prossimi Passi – Estendere il Flusso di Lavoro OCR Offline

- **Carica immagine per OCR** da un `MemoryStream` quando si gestiscono file caricati in ASP.NET Core.  
- Passa a **riconoscere testo da passaporto** in modalità batch iterando su una cartella di scansioni di passaporti.  
- Combina il risultato con **espressioni regolari** per estrarre campi come numero di passaporto o data di nascita.  
- Sperimenta con `ocrEngine.Configuration.UseParallelProcessing = true` per accelerazioni multi‑core.

---

### Conclusione

We’ve just shown you how to **extract text from image** using a fully offline C# OCR pipeline. The short, self‑contained **c# ocr example** loads an image, configures the engine to **recognize cyrillic text**, and prints the extracted passport data—all without a single network request.

Feel free to tweak the code, add more languages, or plug the output into a database. The sky’s the limit once you’ve mastered the basics of loading an image for OCR and recognising text from a passport‑style photo.

Got questions or want to share your own tweaks? Drop a comment below, and happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}