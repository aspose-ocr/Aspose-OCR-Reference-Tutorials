---
category: general
date: 2026-03-23
description: Estrai il testo da un'immagine usando Aspose OCR in C# e scopri come
  aggiungere un logger console per un feedback in tempo reale.
draft: false
keywords:
- extract text from image
- add console logger
language: it
og_description: Estrai il testo da un'immagine con Aspose OCR e aggiungi un logger
  della console per monitorare il processo. Tutorial passo‑passo in C#.
og_title: Estrai testo da immagine in C# – Guida completa alla programmazione
tags:
- OCR
- C#
- logging
title: Estrai testo da immagine in C# – Guida completa
url: /it/net/text-recognition/extract-text-from-image-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai testo da immagine in C# – Guida completa

Hai bisogno di **estrarre testo da immagine** in modo rapido e affidabile? Con Aspose OCR puoi fare esattamente questo in poche righe di C#.  
Ti mostreremo anche come **aggiungere un logger console** così potrai osservare l'engine OCR sussurrare i suoi progressi direttamente nel tuo terminale.

Immagina di avere una ricevuta scannerizzata, una nota scritta a mano o una pagina PDF salvata come PNG. Vuoi i caratteri grezzi senza aprire un'interfaccia ingombrante. Questo tutorial ti guida attraverso una soluzione completa, pronta da copiare‑incollare, che funziona oggi con .NET 6+ e l'ultima libreria Aspose OCR.

Alla fine di questa guida sarai in grado di:

* Caricare un file immagine ed eseguire l'OCR per **estrarre testo da immagine**.  
* Collegare un logger console a Aspose AI così da vedere cosa sta facendo la libreria dietro le quinte.  
* Applicare il post‑processore di correzione ortografica integrato per pulire gli errori OCR.  

> **Prerequisiti** – Un ambiente di sviluppo .NET funzionante (Visual Studio 2022, VS Code o Rider), .NET 6 SDK o più recente, e una licenza Aspose OCR (o una prova gratuita). Non sono richiesti altri pacchetti di terze parti.

---

## Cosa ti servirà

| Elemento | Perché è importante |
|------|----------------|
| **Aspose.OCR** NuGet package | Fornisce la classe `OcrEngine` che legge effettivamente l'immagine. |
| **Aspose.OCR.AI** NuGet package | Fornisce il framework `AsposeAI` per il post‑processore, inclusa la correzione ortografica. |
| **Microsoft.Extensions.Logging** (optional) | Fornisce l'interfaccia `ILogger` per il passaggio **add console logger**. |
| **An input image** (`input.png`) | Il file sorgente da cui **estrarremo testo da immagine**. |

Puoi installare i pacchetti tramite il terminale:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.AI
dotnet add package Microsoft.Extensions.Logging.Abstractions
```

---

## Passo 1 – Estrarre testo da immagine con Aspose OCR

La prima cosa che facciamo è passare l'immagine all'engine OCR. Questo blocco esegue il lavoro pesante e restituisce una stringa grezza che può ancora contenere errori di battitura.

```csharp
using Aspose.OCR;
using System;

class OcrDemo
{
    static string PerformOcr(string imagePath)
    {
        // Initialise the OCR engine
        using (OcrEngine ocr = new OcrEngine())
        {
            // Load the image – replace with your own path if needed
            ocr.Image = ImageStream.FromFile(imagePath);

            // Run recognition; if it fails we return an empty string
            if (!ocr.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return string.Empty;
            }

            // The engine populates the Text property with the recognised characters
            string rawText = ocr.Text;
            Console.WriteLine("Raw OCR output:\n" + rawText);
            return rawText;
        }
    }
}
```

**Perché funziona:** `OcrEngine` astrae tutta la pre‑elaborazione dell'immagine a basso livello (binarizzazione, correzione dell'inclinazione, ecc.). Quando `Recognize()` restituisce `true`, la proprietà `Text` contiene già i caratteri con la migliore ipotesi.  

> **Suggerimento:** Se la tua immagine è grande, considera di ridimensionarla a ≤ 2000 px sul lato più lungo prima di passarla all'engine. Questo velocizza l'elaborazione senza compromettere l'accuratezza.

---

## Passo 2 – Aggiungere logger console per insight in tempo reale

Ora introduciamo la parte **add console logger**. Il logging non serve solo al debug; ti offre visibilità sui download dei modelli, sui passaggi del processore AI e su eventuali avvisi che la libreria può emettere.

```csharp
using Microsoft.Extensions.Logging;
using System;

public class ConsoleLogger : ILogger
{
    // Minimal ILogger implementation that writes to the console.
    public IDisposable BeginScope<TState>(TState state) => null;
    public bool IsEnabled(LogLevel logLevel) => true;

    public void Log<TState>(LogLevel logLevel, EventId eventId,
        TState state, Exception exception, Func<TState, Exception, string> formatter)
    {
        Console.WriteLine($"[{logLevel}] {formatter(state, exception)}");
    }
}
```

Ora puoi collegare questo logger a Aspose AI:

```csharp
using Aspose.OCR.AI;
using Aspose.OCR.AI.PostProcessors;

// ...

ILogger consoleLogger = new ConsoleLogger();   // Implements ILogger
AsposeAI ai = new AsposeAI(consoleLogger);
```

**Cosa vedrai:** Quando il modello di correzione ortografica viene scaricato automaticamente, la console stamperà una riga simile a:

```
[Information] Downloading model to YOUR_DIRECTORY/Models/spellcheck.onnx …
```

Questo è il vantaggio del **add console logger** – non ti chiederai mai se un'operazione in background è riuscita.

---

## Passo 3 – Configurare e registrare il post‑processore di correzione ortografica

Aspose AI include un comodo post‑processore di correzione ortografica che pulisce gli errori OCR comuni (ad esempio, “rec0gn1ze” → “recognize”). Lo configureremo, opzionalmente indicheremo alla libreria dove salvare il modello, e poi lo registreremo.

```csharp
// Create the built‑in spell‑check processor
SpellCheckAIProcessor spellProcessor = new SpellCheckAIProcessor();

// Optional: tell AsposeAI where to keep downloaded models
AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
{
    AllowAutoDownload = true,
    DirectoryModelPath = "YOUR_DIRECTORY/Models"
};

// Register the processor with the AI engine
ai.SetPostProcessor(spellProcessor, modelConfig);
```

**Perché potresti volere un percorso personalizzato:** Nei pipeline CI/CD spesso vuoi memorizzare nella cache i modelli in una directory nota per evitare download ripetuti. Il flag `AllowAutoDownload` garantisce che il modello venga scaricato la prima volta che esegui il codice.

---

## Passo 4 – Eseguire il post‑processore sul risultato OCR

Con il testo OCR a disposizione e il processore di correzione ortografica pronto, passiamo la stringa grezza a `AsposeAI`. L'engine esegue il modello, e il processore memorizza internamente il testo corretto.

```csharp
// Assume ocrResult contains the raw OCR output from Step 1
string ocrResult = PerformOcr("YOUR_DIRECTORY/input.png");

// Run the post‑processor – it expects an IEnumerable<string>
ai.RunPostprocessor(new[] { ocrResult });
```

Dopo questa chiamata, `spellProcessor` contiene una collezione di oggetti `RecognitionResult`, ognuno con una proprietà `RecognitionText` che contiene la versione pulita.

---

## Passo 5 – Recuperare e visualizzare il testo corretto

Infine estraiamo la stringa corretta dal processore e la stampiamo. Questo è il momento in cui vedi davvero il beneficio sia dell'OCR sia del flusso di lavoro **add console logger**.

```csharp
// Grab the first (and only) result
string correctedText = spellProcessor.GetResult()[0].RecognitionText;
Console.WriteLine("\nCorrected OCR output:\n" + correctedText);
```

**Output previsto** (supponendo che l'immagine contenga la frase “Aspose OCR demo” con qualche difetto OCR):

```
Raw OCR output:
Asp0se OCR d3mo

[Information] Model downloaded successfully.
[Information] Spell‑check completed.

Corrected OCR output:
Aspose OCR demo
```

Nota come il logger ci abbia indicato che il modello era pronto, e la riga corretta è leggibile.

---

## Passo 6 – Pulire le risorse

Sia `AsposeAI` che `OcrEngine` implementano `IDisposable`. Disporli rilascia la memoria nativa e i handle dei file, cosa particolarmente importante nei servizi a lungo termine.

```csharp
// At the end of Main()
ai.Dispose();   // Releases AI resources
// OcrEngine is already disposed via the using‑statement in PerformOcr()
```

---

## Esempio completo funzionante

Di seguito trovi l'intero programma che puoi copiare‑incollare in un nuovo progetto console (`dotnet new console`). Sostituisci `"YOUR_DIRECTORY"` con una cartella reale sul tuo computer.

```csharp
using Aspose.OCR;
using Aspose.OCR.AI;
using Aspose.OCR.AI.PostProcessors;
using Microsoft.Extensions.Logging; // optional logger
using System;

class SpellCheckDemo
{
    static void Main()
    {
        // ---------- Step 1: OCR ----------
        string ocrResult = PerformOcr("YOUR_DIRECTORY/input.png");
        if (string.IsNullOrEmpty(ocrResult)) return;

        // ---------- Step 2: Initialise AI with console logger ----------
        ILogger consoleLogger = new ConsoleLogger(); // implements ILogger
        AsposeAI ai = new AsposeAI(consoleLogger);

        // ---------- Step 3: Spell‑check processor ----------
        SpellCheckAIProcessor spellProcessor = new SpellCheckAIProcessor();

        // ---------- Step 4: Model configuration (optional) ----------
        AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
        {
            AllowAutoDownload = true,
            DirectoryModelPath = "YOUR_DIRECTORY/Models"
        };

        // ---------- Step 5: Register and run ----------
        ai.SetPostProcessor(spellProcessor, modelConfig);
        ai.RunPostprocessor(new[] { ocrResult });

        // ---------- Step 6: Show corrected text ----------
        string correctedText = spellProcessor.GetResult()[0].RecognitionText;
        Console.WriteLine("\nCorrected OCR output:\n" + correctedText);

        // ---------- Clean up ----------
        ai.Dispose();
    }

    static string PerformOcr(string imagePath)
    {
        using (OcrEngine ocr = new OcrEngine())
        {
            ocr.Image = ImageStream.FromFile(imagePath);
            if (!ocr.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return string.Empty;
            }
            string raw = ocr.Text;
            Console.WriteLine("Raw OCR output:\n" + raw);
            return raw;
        }
    }
}

// Minimal console logger implementation
public class ConsoleLogger : ILogger
{
    public IDisposable BeginScope<TState>(TState state) => null;
    public bool

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}