---
category: general
date: 2026-04-06
description: Riconoscere il testo delle immagini usando Aspose OCR in C#. Impara come
  estrarre il testo, caricare un file immagine in C# e scrivere JSON in C# con un
  semplice esempio passo‑passo.
draft: false
keywords:
- recognize image text
- how to extract text
- write json in c#
- load image file c#
language: it
og_description: Riconosci il testo delle immagini con Aspose OCR in C#. Questa guida
  mostra come estrarre il testo, caricare un file immagine in C# e scrivere JSON in
  C# rapidamente.
og_title: Riconoscere il testo delle immagini in C# – Guida completa passo passo
tags:
- OCR
- C#
- Aspose
title: Riconoscere il testo delle immagini in C# – Guida completa con esportazione
  JSON
url: /it/net/text-recognition/recognize-image-text-in-c-full-guide-with-json-export/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# riconoscere il testo dell'immagine in C# – Guida completa passo‑passo

Ti è mai capitato di dover **recognize image text** da una ricevuta scansionata ma non eri sicuro quale libreria scegliere? Non sei l'unico. In molte app del mondo reale—tracciatori di spese, elaboratori di fatture, persino strumenti di accessibilità—estrarre le parole da un'immagine è il primo ostacolo.  

In questo tutorial percorreremo una soluzione pratica che **recognize image text** usando la libreria Aspose OCR, mostra **how to extract text**, dimostra **load image file c#** correttamente, e infine **write json in c#** così potrai memorizzare o trasmettere i risultati. Alla fine avrai un'app console pronta all'uso che trasforma qualsiasi PNG in un payload JSON ordinato.

---

## Cosa ti servirà

- **.NET 6+** (il codice funziona anche con .NET Framework 4.8, ma .NET 6 è l'opzione ideale).
- **Aspose.OCR for .NET** pacchetto NuGet. Installalo con `dotnet add package Aspose.OCR`.
- Un'immagine di esempio (`input.png`) posizionata in un luogo accessibile dall'app.  
- Visual Studio 2022 o qualsiasi editor tu preferisca—non servono trucchi avanzati dell'IDE.

> Suggerimento: conserva i file immagine in una cartella chiamata `Resources` all'interno del progetto; mantiene i percorsi ordinati ed evita problemi di “file not found”.

---

## Passo 1: recognize image text – Carica il file immagine

Prima che il motore OCR possa fare la sua magia, devi **load image file c#** in modo sicuro. Il metodo `Image.FromFile` genera un'eccezione se il percorso è errato o il file non è in un formato supportato, quindi lo proteggeremo.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Export;

class Program
{
    static void Main()
    {
        // Define input and output paths
        string inputPath  = Path.Combine("Resources", "input.png");
        string outputPath = Path.Combine("Resources", "output.json");

        // Verify the image exists
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"❌ Image not found at {inputPath}");
            return;
        }

        // Load the image – this is the “load image file c#” step
        using (Image receiptImage = Image.FromFile(inputPath))
        {
            // Continue to OCR...
        }
    }
}
```

*Perché è importante*: Caricare l'immagine all'interno di un blocco `using` garantisce che le risorse GDI+ non gestite vengano rilasciate tempestivamente, evitando perdite di memoria nei servizi a lungo termine.

---

## Passo 2: How to extract text with Aspose OCR

Ora che il bitmap è in memoria, lo passiamo al motore **recognize image text**. L'`OcrEngine` di Aspose è semplice: istanziarlo, chiamare `Recognize` e otterrai un oggetto `OcrResult` che contiene il testo grezzo, i punteggi di confidenza e persino le bounding box.

```csharp
// Inside the using block from Step 1
var ocrEngine = new OcrEngine();

// Perform OCR – this is the core “how to extract text” operation
OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

// Quick sanity check
if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
{
    Console.WriteLine("⚠️ No text detected. Try a clearer image.");
    return;
}
Console.WriteLine("✅ OCR succeeded. Extracted text:");
Console.WriteLine(ocrResult.Text);
```

*Spiegazione*: Il metodo `Recognize` esegue la rete neurale integrata. Funziona al meglio con immagini ad alto contrasto e 300 DPI. Se gli fornisci una foto sfocata, la confidenza diminuisce—considera un pre‑processing (raddrizzamento, binarizzazione) per il codice di produzione.

---

## Passo 3: Write JSON in C# – Esportare il risultato OCR

La maggior parte delle API si aspetta JSON, quindi **write json in c#** usando `JsonExport` di Aspose. La libreria serializza l'intero `OcrResult`, preservando le informazioni di riga e i valori di confidenza.

```csharp
// Still inside the same using block
string jsonResult = JsonExport.ToJson(ocrResult);

// Persist the JSON to disk
File.WriteAllText(outputPath, jsonResult);
Console.WriteLine($"💾 JSON written to {outputPath}");
```

### Output JSON previsto

```json
{
  "Text": "Total: $12.34\r\nDate: 2026-04-01\r\n...",
  "Words": [
    { "Text": "Total", "Confidence": 0.98, "Rectangle": { "X": 10, "Y": 15, "Width": 50, "Height": 12 } },
    { "Text": "$12.34", "Confidence": 0.96, "Rectangle": { "X": 70, "Y": 15, "Width": 45, "Height": 12 } }
    // … more words …
  ]
}
```

*Perché JSON?* È indipendente dal linguaggio, facile da deserializzare e conserva i metadati OCR dettagliati che potresti necessitare per la validazione a valle.

---

## Passo 4: Programma completo e eseguibile

Mettendo insieme i pezzi, ecco l'app console completa. Copia‑incolla, ripristina i pacchetti NuGet e premi **F5**.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Export;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Configuration – adjust these paths as needed
        // -------------------------------------------------
        string inputPath  = Path.Combine("Resources", "input.png");
        string outputPath = Path.Combine("Resources", "output.json");

        // -------------------------------------------------
        // Validate input file
        // -------------------------------------------------
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"❌ Image not found at {inputPath}");
            return;
        }

        // -------------------------------------------------
        // Load image (load image file c#)
        // -------------------------------------------------
        using (Image receiptImage = Image.FromFile(inputPath))
        {
            // -------------------------------------------------
            // Initialize OCR engine and recognize text
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();
            OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("⚠️ No text detected. Try a clearer image.");
                return;
            }

            Console.WriteLine("✅ OCR succeeded. Sample output:");
            Console.WriteLine(ocrResult.Text.Substring(0, Math.Min(100, ocrResult.Text.Length)) + "...");

            // -------------------------------------------------
            // Convert result to JSON (write json in c#)
            // -------------------------------------------------
            string jsonResult = JsonExport.ToJson(ocrResult);
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"💾 JSON written to {outputPath}");
        }
    }
}
```

Esegui il programma e apri `Resources/output.json`—dovresti vedere una rappresentazione JSON ben strutturata di tutto ciò che il motore ha riconosciuto.

---

## Gestione dei casi limite comuni

| Situazione | Cosa fare | Perché |
|-----------|------------|-----|
| **Image is null or corrupted** | Avvolgi `Image.FromFile` in un try/catch e registra l'eccezione. | Previene il crash dell'app e fornisce un messaggio di errore chiaro. |
| **Low confidence scores** | Controlla `ocrResult.Words[i].Confidence`. Se è inferiore a 0.75, considera il preprocessing (aumenta DPI, nitidezza). | Migliora l'affidabilità per i processi a valle come l'estrazione dell'importo. |
| **Large files (>10 MB)** | Ridimensiona l'immagine prima dell'OCR (`receiptImage = new Bitmap(receiptImage, new Size(width/2, height/2))`). | Riduce la pressione sulla memoria e velocizza il riconoscimento. |
| **Multi‑language documents** | Imposta `ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;` | Consente al motore di rilevare caratteri di entrambe le lingue. |

---

## Bonus: Visualizzare il risultato OCR (opzionale)

Se vuoi vedere dove ogni parola si trova sull'immagine, puoi disegnare le bounding box:

```csharp
using (Graphics g = Graphics.FromImage(receiptImage))
{
    foreach (var word in ocrResult.Words)
    {
        var rect = new Rectangle(word.Rectangle.X, word.Rectangle.Y,
                                 word.Rectangle.Width, word.Rectangle.Height);
        g.DrawRectangle(Pens.Red, rect);
    }
    receiptImage.Save(Path.Combine("Resources", "annotated.png"));
}
```

Il `annotated.png` risultante mostrerà rettangoli rossi attorno a ogni parola riconosciuta—utile per il debugging.

---

## Conclusione

Abbiamo appena **recognize image text** in C# dall'inizio alla fine: caricamento del file immagine, invocazione di Aspose OCR per **how to extract text**, e infine **write json in c#** così i dati possono viaggiare ovunque. L'esempio completo funziona subito, e i consigli aggiuntivi ti aiutano a gestire ricevute sfocate, file di grandi dimensioni o scansioni multilingue.

Cosa fare dopo? Prova a sostituire Aspose con un altro motore (Tesseract, Microsoft OCR) e confronta i punteggi di confidenza, oppure inserisci il JSON in un database per la rendicontazione delle spese. Potresti anche espandere l'app console in un'ASP .NET Core Web API che accetta upload di immagini e restituisce JSON immediatamente.

Hai domande su scaling, gestione degli errori o integrazione con Azure Functions? Lascia un commento o contattami su GitHub. Buona programmazione, e che il tuo OCR sia sempre nitido! 

---

![Screenshot dell'output JSON OCR – esempio di recognize image text](https://example.com/ocr-example.png "esempio di recognize image text")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}