---
category: general
date: 2026-05-02
description: Tutorial OCR in C# che mostra come estrarre testo da un'immagine in C#
  e riconoscere il testo PNG, quindi scrivere JSON indentato usando JsonSerializer
  in C#. Guida passo‑passo per sviluppatori.
draft: false
keywords:
- c# ocr tutorial
- extract text image c#
- recognize png text
- write indented json
- use jsonserializer c#
language: it
og_description: Tutorial OCR in C# che dimostra come estrarre testo da un'immagine
  in C# e riconoscere testo PNG, quindi scrivere JSON indentato con JsonSerializer
  C#. Esempio completo e eseguibile.
og_title: c# OCR tutorial – Estrai testo ed esporta come JSON indentato
tags:
- OCR
- C#
- Aspose
- JSON
title: c# tutorial OCR – Estrai testo da immagini ed esporta come JSON indentato
url: /it/net/text-recognition/c-ocr-tutorial-extract-text-from-images-and-export-as-indent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Estrai Testo da Immagini ed Esporta come JSON Indentato

Ti è mai capitato di aver bisogno di un **c# ocr tutorial** che passi da un'immagine di testo direttamente a un file JSON ben formattato? Non sei l'unico. In molti progetti – pensa alla scansione di fatture, all'analisi di ricevute o anche all'estrazione di testo da meme – ti ritrovi con un file PNG e ti chiedi come estrarre le parole senza scrivere un riconoscitore personalizzato.  

Questa guida ti offre una soluzione pratica: **estrarremo testo immagine c#** usando Aspose.OCR, **riconosceremo testo png**, e poi **scriveremo json indentato** con `JsonSerializer` in C#. Alla fine avrai un'app console autonoma che potrai inserire in qualsiasi soluzione .NET. Niente link vaghi tipo “vedi la documentazione”, solo un esempio completo pronto per il copia‑incolla.

## Cosa Ti Serve

- **.NET 6** (o qualsiasi versione .NET recente). I framework più vecchi funzionano, ma la sintassi mostrata è rivolta a .NET 6+.
- **Aspose.OCR per .NET** – installa via NuGet: `dotnet add package Aspose.OCR`.
- Un'immagine PNG di esempio (`text.png`) contenente testo chiaro e leggibile dalla macchina.
- Un IDE o editor a tua scelta – Visual Studio, VS Code, Rider, ecc.

> **Consiglio professionale:** Se prevedi di elaborare molte immagini, considera di riutilizzare una singola istanza di `OcrEngine` invece di crearne una nuova per ogni file. Riduce l'overhead e migliora il throughput.

## Passo 1: Configura un Progetto c# ocr tutorial

Prima, crea un progetto console. I comandi seguenti creano lo scheletro e includono la libreria OCR:

```bash
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo
dotnet add package Aspose.OCR
```

Adesso apri il file `Program.cs` generato. Sostituiremo il suo contenuto con l'esempio completo più tardi, ma per ora assicurati che il progetto compili:

```bash
dotnet build
```

Se non vedi errori, sei pronto a procedere.

## Passo 2: Riconosci Testo PNG da un'Immagine

Il cuore di qualsiasi **c# ocr tutorial** è il motore OCR stesso. Aspose.OCR astrae i dettagli di basso livello e ti fornisce una classe `OcrEngine` pulita. Di seguito creiamo il motore, lo puntiamo a un file PNG e gli chiediamo di riconoscere il testo.

```csharp
using Aspose.OCR;
using System;
using System.Text.Json;

class JsonExportExample
{
    public static void Run()
    {
        // 1️⃣ Create an OCR engine instance – this is the entry point for all OCR work.
        var ocrEngine = new OcrEngine();

        // 2️⃣ Recognize text from the input image. 
        //    The method automatically detects the language (default is English) and returns an OcrResult.
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/text.png");

        // If the image couldn't be read, handle it gracefully.
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("No text detected – double‑check the file path and image quality.");
            return;
        }

        // Continue to serialization...
```

### Perché Funziona

- **`RecognizeImage`** accetta molti formati (PNG, JPEG, BMP). Riconosciamo specificamente **testo png** perché PNG conserva i dettagli senza perdita, il che è ideale per l'OCR.
- Il `OcrResult` restituito contiene non solo il testo semplice ma anche un punteggio di confidenza per ogni glifo, utile se in seguito devi filtrare i caratteri a bassa confidenza.

## Passo 3: Scrivi JSON Indentato con JsonSerializer c#

Ora che abbiamo `ocrResult`, il passo logico successivo nel nostro **c# ocr tutorial** è trasformare quell'oggetto in JSON leggibile dall'uomo. Il serializer integrato `System.Text.Json` fa il lavoro, e lo configureremo per **scrivere json indentato** per chiarezza.

```csharp
        // 3️⃣ Serialize the OCR result (including confidence per glyph) to indented JSON.
        var jsonOptions = new JsonSerializerOptions
        {
            WriteIndented = true // This makes the output pretty‑printed.
        };

        string jsonOutput = JsonSerializer.Serialize(ocrResult, jsonOptions);

        // 4️⃣ Display the JSON result – you could also write it to a file if you prefer.
        Console.WriteLine(jsonOutput);
    }
}
```

### Usare Correttamente `JsonSerializer`

- Il flag `WriteIndented` è il modo più semplice per **scrivere json indentato** senza introdurre librerie di terze parti.
- Se mai avrai bisogno di nomi di proprietà in camel‑case, aggiungi `PropertyNamingPolicy = JsonNamingPolicy.CamelCase` alle opzioni.
- La stringa `jsonOutput` può essere salvata con `File.WriteAllText("result.json", jsonOutput);` – una modifica utile per pipeline reali.

## Passo 4: Esegui e Verifica l'Uscita

Compila ed esegui il programma:

```bash
dotnet run
```

Supponendo che `text.png` contenga la frase *“Hello, OCR World!”*, dovresti vedere qualcosa del genere:

```json
{
  "Text": "Hello, OCR World!",
  "Confidence": 0.9875,
  "Lines": [
    {
      "Text": "Hello, OCR World!",
      "Confidence": 0.9875,
      "Words": [
        {
          "Text": "Hello,",
          "Confidence": 0.9921,
          "BoundingBox": { "X": 12, "Y": 34, "Width": 58, "Height": 20 }
        },
        {
          "Text": "OCR",
          "Confidence": 0.9812,
          "BoundingBox": { "X": 78, "Y": 34, "Width": 34, "Height": 20 }
        },
        {
          "Text": "World!",
          "Confidence": 0.9890,
          "BoundingBox": { "X": 118, "Y": 34, "Width": 62, "Height": 20 }
        }
      ]
    }
  ]
}
```

Quel JSON è **indentato**, rendendolo facile da leggere nei log o da passare a servizi downstream.

### Casi Limite & Suggerimenti

| Situazione | Cosa Fare |
|-----------|------------|
| **L'immagine è sfocata** | Aumenta `ocrEngine.Config.Dpi` (es., `ocrEngine.Config.Dpi = 300`) prima di chiamare `RecognizeImage`. |
| **Lingua non inglese** | Imposta `ocrEngine.Config.Language = OcrLanguage.German` (o qualsiasi lingua supportata). |
| **Grande batch di file** | Itera su una directory, riutilizzando la stessa istanza di `OcrEngine`; salva ogni risultato JSON con un nome file unico. |
| **Necessità di testo ad alta confidenza** | Filtra `ocrResult.Lines` dove `Confidence` ≥ 0.95 prima della serializzazione. |

## Esempio Completo Funzionante (Pronto per Copia‑Incolla)

Di seguito trovi il programma *intero*, pronto da inserire in `Program.cs`. Include tutti i passaggi, la gestione degli errori e i commenti che rendono il codice auto‑esplicativo.

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    public static void Main()
    {
        // 👉 Step 1: Initialize the OCR engine.
        var ocrEngine = new OcrEngine();

        // 👉 Step 2: Path to the PNG image you want to process.
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "text.png");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found at {imagePath}");
            return;
        }

        // 👉 Step 3: Perform OCR – this is where we **recognize png text**.
        var ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 👉 Step 4: Validate the result.
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("No recognizable text found. Try a clearer image or adjust DPI settings.");
            return;
        }

        // 👉 Step 5: Configure JsonSerializer to **write indented json**.
        var jsonOptions = new JsonSerializerOptions
        {
            WriteIndented = true // Pretty‑print the JSON.
        };

        // 👉 Step 6: Serialize the OCR result – this demonstrates **use jsonserializer c#**.
        string jsonOutput = JsonSerializer.Serialize(ocrResult, jsonOptions);

        // 👉 Step 7: Output to console (or write to a file).
        Console.WriteLine(jsonOutput);

        // Optional: Save to disk.
        string outputPath = Path.ChangeExtension(imagePath, ".json");
        File.WriteAllText(outputPath, jsonOutput);
        Console.WriteLine($"JSON saved to {outputPath}");
    }
}
```

Esegui il codice, ispeziona la console o il file `.json` generato, e vedrai il testo estratto insieme ai punteggi di confidenza, tutto ordinatamente **indentato**.

## Conclusione

Ora hai un solido **c# ocr tutorial** che mostra come **estrarre testo immagine c#**, **riconoscere testo png**, e **scrivere json indentato** usando `JsonSerializer`. L'esempio è completo, eseguibile e include consigli pratici per scenari reali.  

Prossimi passi? Prova a sostituire Aspose.OCR con un altro motore (es., Tesseract) e osserva come cambia la struttura di `OcrResult`, oppure invia il JSON a un'API downstream che memorizza i dati OCR in un database. Puoi anche sperimentare le opzioni **use jsonserializer c#** come convertitori personalizzati per la formattazione delle date o la gestione degli enum.

Buona programmazione, e che le tue pipeline OCR siano sempre accurate!  

---  

![diagramma tutorial c# ocr](image.png "Diagramma che illustra il flusso OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}