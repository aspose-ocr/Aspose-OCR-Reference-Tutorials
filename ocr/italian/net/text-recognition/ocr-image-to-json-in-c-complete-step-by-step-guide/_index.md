---
category: general
date: 2026-02-11
description: Converti un'immagine OCR in JSON in C#. Impara a estrarre il testo dall’immagine,
  leggere il file immagine in C#, formattare l’output JSON e stampare il JSON in modo
  leggibile in C# con Aspose.OCR.
draft: false
keywords:
- ocr image to json
- extract text from image
- read image file c#
- format json output
- pretty print json c#
language: it
og_description: Converti un'immagine OCR in JSON in C#. Questa guida mostra come estrarre
  il testo dall’immagine, leggere il file immagine in C#, formattare l’output JSON
  e stampare il JSON in modo leggibile in C# usando Aspose.OCR.
og_title: OCR immagine in JSON in C# – Guida completa passo‑passo
tags:
- OCR
- C#
- JSON
title: OCR immagine in JSON in C# – Guida completa passo passo
url: /it/net/text-recognition/ocr-image-to-json-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ocr image to json in C# – Guida completa passo‑per‑passo

Ti è mai capitato di dover **ocr image to json** ma non eri sicuro quale libreria scegliere o come ottenere un risultato ben formattato? Non sei solo. In molte applicazioni reali—scansione di ricevute, verifica di ID o semplice archiviazione di documenti—vorrai estrarre il testo da un'immagine e ottenere un payload JSON pulito che i servizi a valle possano consumare.

Nel tutorial percorreremo l'intero flusso: dalla lettura di un file immagine in C# all'estrazione del testo con Aspose.OCR, poi richiedendo al motore un output JSON strutturato, e infine formattando quel JSON in modo leggibile. Alla fine avrai uno snippet autonomo, pronto per la produzione, che potrai inserire in qualsiasi progetto .NET.

Tratteremo anche le insidie comuni (come pacchetti linguistici mancanti) e mostreremo alcune rapide variazioni—ad esempio, passare a output XML o gestire PDF multi‑pagina. Nessuna documentazione esterna necessaria; tutto quello che ti serve è qui.

## Cosa ti servirà

- **.NET 6+** (il codice funziona anche con .NET Framework 4.7+)
- **Aspose.OCR for .NET** – installa tramite NuGet (`Install-Package Aspose.OCR`)
- Un'immagine di esempio (ad es., `receipt.png`) posizionata in un percorso accessibile
- Familiarità di base con la sintassi C# (se hai già scritto un “Hello World”, sei a posto)

> *Suggerimento:* Se sei su un server CI, imposta `AutomaticResourceDownload = true` così Aspose scarica i dati linguistici al volo—senza dover gestire manualmente le DLL.

## Passo 1: Leggere il file immagine C# e creare il motore OCR  

La prima cosa che facciamo è caricare l'immagine dal disco. Usare `System.Drawing.Image` mantiene il codice breve e funziona per PNG, JPEG, BMP e anche TIFF multi‑pagina (il motore seleziona la prima pagina per impostazione predefinita).

```csharp
using System.Drawing;          // For Image
using Aspose.OCR;              // Core OCR classes
using Aspose.OCR.Models;       // Language and output enums
using System.Text.Json;        // JSON parsing & pretty‑print

// 1️⃣ Configure the OCR engine – this is where we tell Aspose what language we expect
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,          // extract text from image in English
    AutomaticResourceDownload = true,        // auto‑download language packs if missing
    OutputFormat = OcrOutputFormat.Json      // ask for JSON rather than plain text
};
```

**Perché è importante:**  
- `AutomaticResourceDownload` previene crash a runtime quando il file della lingua inglese non è presente localmente.  
- Impostare `OutputFormat` su `Json` significa che il motore esegue già la conversione dei risultati OCR grezzi in un oggetto strutturato—nessuna analisi manuale di stringhe necessaria.

## Passo 2: Eseguire l'OCR e ottenere l'output JSON  

Ora passiamo il bitmap caricato al motore. Il metodo `Recognize` restituisce un `OcrResult` che contiene una proprietà `Text` con la stringa JSON.

```csharp
// 2️⃣ Load the image you want to process
using (var receiptImage = Image.FromFile(@"C:\Images\receipt.png"))
{
    // 3️⃣ Perform OCR – this call blocks until the engine finishes
    var ocrResult = ocrEngine.Recognize(receiptImage);

    // 4️⃣ The OCR engine gave us JSON straight away
    string rawJson = ocrResult.Text;
    
    // Optional: write the raw JSON to a file for debugging
    System.IO.File.WriteAllText(@"C:\Temp\ocr_raw.json", rawJson);
}
```

**Caso limite:** Se l'immagine è corrotta o il percorso è errato, `Image.FromFile` genera una `FileNotFoundException`. Avvolgi il blocco in un `try/catch` se ti aspetti input non affidabili.

## Passo 3: Analizzare e formattare il JSON – pretty‑print JSON C#  

Il JSON grezzo prodotto dal motore OCR è compatto e poco leggibile. Usando `System.Text.Json` possiamo deserializzarlo in un `JsonDocument`, poi riserializzarlo con indentazione.

```csharp
// 5️⃣ Parse the JSON string into a DOM-like structure
using var jsonDoc = JsonDocument.Parse(rawJson);

// 6️⃣ Pretty‑print with indentation (2 spaces by default)
string prettyJson = JsonSerializer.Serialize(
    jsonDoc.RootElement,
    new JsonSerializerOptions { WriteIndented = true });

// 7️⃣ Output to console – you could also send this to an API or a file
Console.WriteLine(prettyJson);

// 8️⃣ Save the pretty JSON for later use
System.IO.File.WriteAllText(@"C:\Temp\ocr_pretty.json", prettyJson);
```

**Cosa vedrai:**  

```json
{
  "Lines": [
    {
      "Text": "Store Name",
      "BoundingBox": { "X": 12, "Y": 5, "Width": 150, "Height": 20 }
    },
    {
      "Text": "Total: $23.45",
      "BoundingBox": { "X": 12, "Y": 200, "Width": 100, "Height": 20 }
    }
  ],
  "Language": "English",
  "Confidence": 0.96
}
```

Il JSON ora include testo riga per riga, bounding box, lingua rilevata e un punteggio di confidenza—perfetto per alimentare analisi a valle o un componente UI.

## Passo 4: Bonus – Cambiare formato di output o lingua  

Se mai avrai bisogno di **format json output** come XML o vuoi fare OCR su una ricevuta spagnola, basta modificare la configurazione del motore:

```csharp
ocrEngine.Language = OcrLanguage.Spanish;          // extract text from image in Spanish
ocrEngine.OutputFormat = OcrOutputFormat.Xml;     // ask for XML instead of JSON
```

Il resto del codice rimane identico; cambi solo la fase di deserializzazione (usa `XmlDocument` per XML).

## Esempio completo funzionante  

Mettiamo tutto insieme, ecco un unico file che puoi copiare‑incollare in un'app console:

```csharp
// ---------------------------------------------------------------
// ocr_image_to_json_demo.cs
// ---------------------------------------------------------------
using System;
using System.Drawing;
using System.Text.Json;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Configure OCR engine
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            AutomaticResourceDownload = true,
            OutputFormat = OcrOutputFormat.Json
        };

        // Path to your image – adjust as needed
        string imagePath = @"C:\Images\receipt.png";

        try
        {
            using (var receiptImage = Image.FromFile(imagePath))
            {
                var ocrResult = ocrEngine.Recognize(receiptImage);
                string rawJson = ocrResult.Text;

                // Parse & pretty‑print
                using var jsonDoc = JsonDocument.Parse(rawJson);
                string prettyJson = JsonSerializer.Serialize(
                    jsonDoc.RootElement,
                    new JsonSerializerOptions { WriteIndented = true });

                Console.WriteLine("=== Pretty‑Printed OCR JSON ===");
                Console.WriteLine(prettyJson);

                // Optional: write to file
                System.IO.File.WriteAllText(@"C:\Temp\ocr_pretty.json", prettyJson);
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Error processing image: {ex.Message}");
        }
    }
}
```

Eseguendo questo programma stampa un payload JSON ben indentato sulla console e lo salva in `C:\Temp\ocr_pretty.json`. Il blocco `try/catch` garantisce che, anche se l'immagine non può essere letta, otterrai un messaggio di errore chiaro invece di un crash silenzioso.

## Domande comuni e insidie  

- **E se l'OCR restituisce testo vuoto?**  
  Di solito significa che l'immagine è troppo rumorosa o la lingua non corrisponde. Prova ad aumentare il contrasto dell'immagine o a impostare `Language` su `AutoDetect`.  

- **Posso elaborare più immagini in un ciclo?**  
  Assolutamente. Avvolgi il blocco `using (var img = Image.FromFile(...))` dentro un ciclo `foreach (var file in Directory.GetFiles(...))` e raccogli ogni `prettyJson` in una lista o scrivili in file separati.  

- **Lo schema JSON è stabile?**  
  Aspose garantisce la retrocompatibilità per il formato di output `Json`, ma controlla sempre l'attributo `Version` nella risposta se stai puntando a una versione specifica dell'API.  

- **È necessaria una licenza per Aspose.OCR?**  
  Una chiave di valutazione gratuita funziona fino a 100 pagine. Per la produzione, acquista una licenza e impostala con `License license = new License(); license.SetLicense("Aspose.OCR.lic");`.  

## Conclusione  

Ora hai una **soluzione completa e autonoma per ocr image to json** in C#. Leggendo il file immagine, configurando il motore OCR, richiedendo l'output JSON e formattandolo, puoi integrare l'estrazione del testo in qualsiasi servizio .NET senza ricorrere a trucchi con le stringhe.

Da qui potresti esplorare **extract text from image** per altri tipi di file (PDF, TIFF multi‑pagina), sperimentare con lingue diverse, o inviare il JSON a un archivio NoSQL per analisi. Il cielo è il limite—ricorda solo di gestire gli errori in modo corretto e di tenere d'occhio le licenze se scala.

Buona programmazione, e che le tue pipeline OCR siano sempre accurate!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}