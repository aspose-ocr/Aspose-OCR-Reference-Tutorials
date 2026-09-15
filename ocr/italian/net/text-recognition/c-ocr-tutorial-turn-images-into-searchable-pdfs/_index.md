---
category: general
date: 2026-01-12
description: Tutorial OCR in C# che mostra come riconoscere un'immagine di testo,
  estrarre il testo da un'immagine in C# e generare un file OCR da immagine a PDF
  con punteggi di confidenza.
draft: false
keywords:
- c# ocr tutorial
- image to pdf ocr
- recognize text image
- ocr confidence scores
- extract text image c#
language: it
og_description: Impara un tutorial completo di OCR in C# per riconoscere immagini
  di testo, estrarre testo da immagini in C# e creare un documento OCR da immagine
  a PDF con punteggi di confidenza.
og_title: c# tutorial OCR – Converti le immagini in PDF ricercabili
tags:
- OCR
- C#
- PDF
title: c# tutorial OCR – Trasforma le immagini in PDF ricercabili
url: /it/net/text-recognition/c-ocr-tutorial-turn-images-into-searchable-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tutorial c# ocr – Trasforma le Immagini in PDF Ricercabili

Ti sei mai chiesto come **riconoscere immagini di testo** file in un progetto C# senza cercare servizi di terze parti? Non sei solo. In molte app reali—pensa a scanner di fatture, tracciatori di ricevute o archivi di documenti multilingue—gli sviluppatori hanno bisogno di un motore OCR affidabile, on‑premise, che fornisca anche i punteggi di confidenza.  

Questo **c# ocr tutorial** ti guiderà attraverso tutto ciò di cui hai bisogno: dal caricamento di un'immagine, alla selezione dei modelli linguistici, all'attivazione dell'accelerazione GPU, fino al salvataggio del risultato come PDF ricercabile. Alla fine avrai un esempio di codice pronto‑all'uso che estrae il testo, riporta la confidenza OCR e, opzionalmente, crea un file *image to pdf ocr*—tutto in meno di un minuto di programmazione.

## Cosa Costruirai

- Carica un'immagine multilingua (`sample_multi_lang.jpg` è usata come segnaposto).  
- Scegli i modelli linguistici Arabic, Hindi e Russian (puoi aggiungerne altri).  
- Attiva l'elaborazione GPU se la tua macchina lo supporta.  
- Ottieni il risultato OCR grezzo **con i punteggi di confidenza**.  
- Serializza il risultato in JSON formattato **o** scrivi un PDF ricercabile.  

Nessun servizio web esterno, nessuna magia nascosta—solo Aspose.OCR per .NET, qualche riga di C# e una chiara spiegazione del **perché** ogni riga è importante.

## Prerequisiti

- .NET 6.0 o successivo (il codice si compila su .NET Core e .NET Framework).  
- Visual Studio 2022 (o qualsiasi IDE tu preferisca).  
- Una licenza Aspose.OCR per .NET (la versione di prova gratuita funziona per i test).  
- Opzionale: una GPU compatibile CUDA se vuoi accelerare il riconoscimento.

> **Consiglio professionale:** Se non hai una GPU, imposta semplicemente `UseGpu = false` e il motore tornerà alla CPU senza alcuna modifica al codice.

## Passo 1: Installa i Pacchetti NuGet Necessari

Apri la **Package Manager Console** ed esegui:

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Gpu
Install-Package Newtonsoft.Json
```

Questi tre pacchetti ti forniscono il motore OCR, l'accelerazione GPU e un comodo serializzatore JSON per l'output delle confidenze.

## Passo 2: Configura la Struttura del Progetto

Crea un nuovo progetto console (`dotnet new console -n AsposeOcrDemo`) e sostituisci il file `Program.cs` generato con il codice seguente.  
Tutta la logica risiede nella classe `Program`; l'unico tipo aggiuntivo è un piccolo metodo di estensione che formatta il risultato OCR in JSON.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Gpu;
using Aspose.OCR.Models;
using Newtonsoft.Json;

namespace AsposeOcrDemo
{
    class Program
    {
        // Step 1: Input image and language models
        private const string InputImagePath = @"YOUR_DIRECTORY/sample_multi_lang.jpg";
        private static readonly string[] Languages = { LanguageModel.Arabic, LanguageModel.Hindi, LanguageModel.Russian };

        // Step 2: Processing options (GPU toggle & output format)
        private const bool UseGpu = true;               // set false if no GPU
        private const string OutputFormat = "Json";     // change to "Pdf" for PDF output

        static void Main()
        {
            // Step 3: Initialise the appropriate OCR engine
            IOcrEngine engine = UseGpu ? (IOcrEngine)new GpuOcrEngine() : new OcrEngine();

            // Step 4: Run OCR – language models are auto‑downloaded if missing
            OcrResult result = engine.Recognize(
                InputImagePath,
                new OcrOptions { LanguageModels = Languages, AutoDownloadResources = true });

            // Step 5: Emit the result in the chosen format
            if (OutputFormat.Equals("json", StringComparison.OrdinalIgnoreCase))
            {
                string json = JsonConvert.SerializeObject(
                    result.GetWordsWithConfidence(),
                    Formatting.Indented);
                Console.WriteLine(json);
            }
            else if (OutputFormat.Equals("pdf", StringComparison.OrdinalIgnoreCase))
            {
                string pdfPath = Path.ChangeExtension(InputImagePath, ".pdf");
                File.WriteAllBytes(pdfPath, result.Pdf);
                Console.WriteLine($"PDF saved to: {pdfPath}");
            }
        }
    }

    // Helper that flattens OcrResult into a JSON‑friendly structure
    internal static class OcrResultExtensions
    {
        public static object GetWordsWithConfidence(this OcrResult result)
        {
            var words = new System.Collections.Generic.List<object>();
            foreach (var w in result.Words)
                words.Add(new
                {
                    Text = w.Text,
                    Confidence = w.Confidence,
                    BoundingBox = new { w.Bounds.X, w.Bounds.Y, w.Bounds.Width, w.Bounds.Height }
                });

            return new
            {
                RecognizedText = result.Text,
                LanguageModels = result.UsedLanguageModels,
                Words = words,
                ProcessingTimeMs = result.ProcessingTime.TotalMilliseconds
            };
        }
    }
}
```

### Perché Questo Codice Funziona

1. **GPU toggle** – `GpuOcrEngine` sfrutta i core CUDA; l'operatore ternario rende il passaggio senza sforzo.  
2. **Automatic language download** – `AutoDownloadResources = true` garantisce che i modelli Arabic, Hindi e Russian vengano scaricati al primo avvio dell'app.  
3. **Confidence scores** – `result.Words` contiene una `Confidence` per ogni parola riconosciuta; il metodo di estensione le formatta in un oggetto JSON pulito.  
4. **Searchable PDF** – `result.Pdf` è già un PDF completamente ricercabile, quindi scriviamo semplicemente l'array di byte su disco. Non servono librerie aggiuntive.

## Passo 6: Esegui il Campione

Apri un terminale, spostati nella cartella del progetto ed esegui:

```bash
dotnet run
```

Se hai scelto l'output **JSON**, vedrai qualcosa del genere:

```json
{
  "RecognizedText": "مرحبا Hello Привет",
  "LanguageModels": [
    "Arabic",
    "Hindi",
    "Russian"
  ],
  "Words": [
    {
      "Text": "مرحبا",
      "Confidence": 0.98,
      "BoundingBox": { "X": 45, "Y": 12, "Width": 120, "Height": 30 }
    },
    {
      "Text": "Hello",
      "Confidence": 0.99,
      "BoundingBox": { "X": 180, "Y": 12, "Width": 80, "Height": 30 }
    },
    {
      "Text": "Привет",
      "Confidence": 0.97,
      "BoundingBox": { "X": 280, "Y": 12, "Width": 110, "Height": 30 }
    }
  ],
  "ProcessingTimeMs": 312
}
```

Se hai cambiato in **PDF**, la console stampa il percorso e troverai un PDF ricercabile proprio accanto all'immagine di origine.

## Domande Frequenti & Casi Limite

- **Cosa succede se un modello linguistico non è disponibile?**  
  Il motore OCR lancia una chiara `ResourceNotFoundException`. Poiché abbiamo impostato `AutoDownloadResources = true`, il modello mancante viene scaricato automaticamente al primo avvio, quindi l'eccezione appare raramente in produzione.

- **Posso elaborare un batch di immagini?**  
  Assolutamente. Avvolgi la chiamata `engine.Recognize` in un ciclo `foreach` su una directory di file. Lo stesso `OcrResultExtensions` funziona per ogni immagine.

- **Ho bisogno di una licenza per la GPU?**  
  No. La versione di prova gratuita funziona sia per CPU che per GPU. Una licenza completa rimuove la filigrana di prova e elimina le restrizioni sul numero di pagine.

- **Quanto sono accurate le confidence scores?**  
  I punteggi vanno da 0.0 (nessuna confidenza) a 1.0 (confidenza perfetta). In pratica, tutto sopra 0.90 è affidabile per l'elaborazione successiva; puoi filtrare le parole a bassa confidenza se necessiti di una validazione più rigorosa.

## Passo 7: Prossimi Passi (Espandi il Tuo Toolkit OCR)

1. **Aggiungi più lingue** – basta aggiungere `LanguageModel.French` (o qualsiasi modello supportato) all'array `Languages`.  
2. **Combina OCR con la conversione PDF/A** – Aspose.PDF può incorporare lo strato OCR in un documento conforme PDF/A‑2b per l'archiviazione.  
3. **Integra con Azure Functions** – avvolgi la logica in un endpoint serverless per elaborare i caricamenti al volo.  
4. **Regola finemente le soglie di confidenza** – usa `result.Words.Where(w => w.Confidence < 0.85)` per segnalare parole incerte per una revisione manuale.

---

### TL;DR

Questo **c# ocr tutorial** ti mostra come:

- Caricare un'immagine e selezionare più modelli linguistici.  
- Attivare l'accelerazione GPU con un singolo flag booleano.  
- Recuperare i risultati OCR **con i punteggi di confidenza** e serializzarli in JSON.  
- Facoltativamente scrivere un PDF ricercabile (**image to pdf ocr**).  

Tutto ciò è realizzabile con poche righe di codice, una prova gratuita di Aspose.OCR e il codice sopra. Provalo, modifica l'elenco delle lingue e avrai una pipeline OCR pronta per la produzione in pochi minuti.

![c# ocr tutorial example image](https://example.com/placeholder-image.jpg "c# ocr tutorial example image")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}