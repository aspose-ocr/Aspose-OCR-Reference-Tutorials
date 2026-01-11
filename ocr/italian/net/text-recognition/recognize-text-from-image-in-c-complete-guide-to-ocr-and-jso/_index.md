---
category: general
date: 2026-01-10
description: Scopri come riconoscere il testo da un'immagine, estrarre le coordinate
  del testo e convertire la ricevuta in JSON usando Aspose OCR in C#. Tutorial passo‑passo.
draft: false
keywords:
- recognize text from image
- how to extract text
- extract text coordinates
- convert receipt to json
language: it
og_description: Riconosci il testo da un'immagine in C# usando Aspose OCR. Questa
  guida mostra come estrarre il testo, ottenere le coordinate e convertire lo scontrino
  in JSON.
og_title: Riconosci il testo da un'immagine – Tutorial completo OCR in C#
tags:
- OCR
- C#
- Aspose
title: Riconoscere il testo da un'immagine in C# – Guida completa a OCR e JSON
url: /it/net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# riconoscere testo da immagine – Tutorial completo C# OCR

Hai mai avuto bisogno di riconoscere testo da un’immagine ma non sapevi quale libreria scegliere? Non sei solo. In molte app del mondo reale—tracker di spese, scanner di ricevute o archiviatori di documenti—estrarre testo in modo affidabile è il primo ostacolo.  

In questo tutorial vedremo **come estrarre testo**, otterremo i relativi bounding box e infine **convertire la ricevuta in JSON** usando Aspose.OCR per .NET. Alla fine avrai un progetto C# autonomo che prende una foto di una ricevuta e genera un file JSON ordinato con punteggi di confidenza e coordinate.

## Cosa ti servirà

Prima di immergerci, assicurati di avere quanto segue sulla tua macchina:

- **.NET 6.0 SDK** (o qualsiasi versione successiva). Anche i framework più vecchi funzionano, ma .NET 6 è il punto di equilibrio per le librerie moderne.
- **Visual Studio 2022** o VS Code con l’estensione C#.
- **Aspose.OCR for .NET** pacchetto NuGet (`Aspose.OCR` e `Aspose.OCR.Output`). Puoi installarlo tramite la Package Manager Console:

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Output
```

- Un’immagine di esempio di ricevuta (ad es. `receipt.jpg`) collocata in una cartella che farai riferimento più tardi.

Tutto qui—nessun SDK aggiuntivo, nessun binario nativo, solo codice gestito puro.

## Passo 1: Crea un nuovo progetto console

Prima di tutto, avvia un’app console. È il modo più rapido per testare l’OCR senza overhead dell’interfaccia utente.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in later.
        }
    }
}
```

> **Suggerimento:** Mantieni ordinata la cartella del progetto; crea una sottocartella chiamata `Resources` e inserisci `receipt.jpg` lì. Renderà la gestione dei percorsi indolore.

## Passo 2: Carica l’immagine della ricevuta

Ora riconosciamo effettivamente **testo da immagine**. Il primo passo è puntare il motore OCR al file.

```csharp
// Inside Main()
string imagePath = @"Resources/receipt.jpg";
if (!System.IO.File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// Initialise the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    Image = ImageStream.FromFile(imagePath)
};

Console.WriteLine("✅ Image loaded successfully.");
```

Perché avvolgiamo il caricamento in un semplice controllo di esistenza? Perché in produzione spesso si gestiscono upload di utenti che potrebbero mancare o essere corrotti. Catturare il problema subito ti salva da eccezioni criptiche più tardi.

## Passo 3: Esegui OCR – **testo da immagine**

Con l’immagine in memoria, chiediamo ad Aspose di **riconoscere testo da immagine**. Questa operazione è sincrona e restituisce un ricco set di risultati.

```csharp
// Still inside Main()
try
{
    ocrEngine.Recognize();
    Console.WriteLine("🧠 OCR completed.");
}
catch (Exception ex)
{
    Console.WriteLine($"❗ OCR failed: {ex.Message}");
    return;
}
```

Dietro le quinte Aspose esegue una rete neurale addestrata su milioni di caratteri. Il motore popola `ocrEngine.Text`, `ocrEngine.RecognitionResult` e una collezione di oggetti `OcrRegion` che contengono le coordinate. È esattamente ciò che ci serve per il passo successivo.

## Passo 4: **come estrarre testo** – Ottenere la stringa grezza

Se ti interessa solo il testo semplice (magari per una ricerca veloce), puoi prelevarlo direttamente dal motore:

```csharp
string plainText = ocrEngine.Text;
Console.WriteLine("\n--- Extracted Text ---");
Console.WriteLine(plainText);
```

Noterai interruzioni di riga dove l’OCR ha rilevato i confini dei paragrafi. In molti scenari di scansione di ricevute la stringa grezza è sufficiente per estrarre totali, date o nomi dei fornitori usando semplici regex.

## Passo 5: **estrarre coordinate del testo** – Bounding box per ogni parola

Spesso è necessario sapere *dove* sull’immagine si trova un determinato pezzo di testo—ad esempio per evidenziare l’importo totale in una UI. Aspose ci fornisce queste informazioni tramite gli oggetti `OcrRegion`.

```csharp
Console.WriteLine("\n--- Text Coordinates (extract text coordinates) ---");
foreach (var region in ocrEngine.RecognitionResult.Regions)
{
    // Each region represents a word or a line depending on the engine settings.
    string word = region.Text;
    var bounds = region.BoundingBox; // X, Y, Width, Height
    Console.WriteLine($"Word: \"{word}\" | Box: X={bounds.X}, Y={bounds.Y}, W={bounds.Width}, H={bounds.Height}");
}
```

Nota che stiamo iterando su **estrarre coordinate del testo** per ogni segmento riconosciuto. Le coordinate sono relative all’immagine originale, così puoi sovrapporle su una canvas grafica o su un elemento HTML `<canvas>`.

## Passo 6: **convertire la ricevuta in JSON** – Salvataggio dei risultati dettagliati

Ora arriva la parte che lega tutto insieme: vogliamo una struttura leggibile da macchine che includa testo, punteggi di confidenza e i bounding box. Aspose fornisce `JsonSaveOptions` che rendono tutto questo un gioco da ragazzi.

```csharp
// Define where the JSON will be saved
string jsonPath = @"Resources/receipt.json";

// Configure JSON options to keep confidence and bounding boxes
JsonSaveOptions jsonOptions = new JsonSaveOptions
{
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};

// Save the OCR result
ocrEngine.Save(jsonPath, jsonOptions);
Console.WriteLine($"\n💾 Detailed OCR results saved to {jsonPath}");
```

Il file risultante appare più o meno così (troncato per brevità):

```json
{
  "Regions": [
    {
      "Text": "Store",
      "Confidence": 0.99,
      "BoundingBox": { "X": 45, "Y": 120, "Width": 80, "Height": 20 }
    },
    {
      "Text": "Total",
      "Confidence": 0.97,
      "BoundingBox": { "X": 300, "Y": 560, "Width": 70, "Height": 22 }
    }
    // ... more regions ...
  ]
}
```

Ora disponi di un artefatto **convertire la ricevuta in JSON** che può essere inviato a servizi downstream—pensa a API di report spese, pipeline di analisi o anche a una semplice UI che disegna rettangoli attorno a ogni parola.

## Esempio completo funzionante

Riunendo tutti i pezzi, ecco il `Program.cs` completo che puoi copiare‑incollare nel tuo progetto:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image
            // -------------------------------------------------
            string imagePath = @"Resources/receipt.jpg";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found at {imagePath}");
                return;
            }

            OcrEngine ocrEngine = new OcrEngine
            {
                Image = ImageStream.FromFile(imagePath)
            };
            Console.WriteLine("✅ Image loaded.");

            // -------------------------------------------------
            // 2️⃣ Run OCR – recognize text from image
            // -------------------------------------------------
            try
            {
                ocrEngine.Recognize();
                Console.WriteLine("🧠 OCR completed.");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❗ OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 3️⃣ Extract plain text (how to extract text)
            // -------------------------------------------------
            Console.WriteLine("\n--- Extracted Text ---");
            Console.WriteLine(ocrEngine.Text);

            // -------------------------------------------------
            // 4️⃣ Get coordinates (extract text coordinates)
            // -------------------------------------------------
            Console.WriteLine("\n--- Text Coordinates ---");
            foreach (var region in ocrEngine.RecognitionResult.Regions)
            {
                var box = region.BoundingBox;
                Console.WriteLine($"Word: \"{region.Text}\" | Box: X={box.X}, Y={box.Y}, W={box.Width}, H={box.Height}");
            }

            // -------------------------------------------------
            // 5️⃣ Save detailed JSON (convert receipt to json)
            // -------------------------------------------------
            string jsonPath = @"Resources/receipt.json";
            JsonSaveOptions jsonOptions = new JsonSaveOptions
            {
                IncludeConfidence = true,
                IncludeBoundingBoxes = true
            };
            ocrEngine.Save(jsonPath, jsonOptions);
            Console.WriteLine($"\n💾 JSON saved at {jsonPath}");
        }
    }
}
```

Esegui il programma (`dotnet run`) e osserva l’output della console. Apri `Resources/receipt.json` per verificare la struttura.

## Domande comuni e casi particolari

- **E se l’immagine è sfocata?**  
  Aspose OCR funziona al meglio con 300 dpi o più. Se ottieni punteggi di confidenza bassi, considera di applicare un filtro di nitidezza prima di passare l’immagine al motore.

- **Posso riconoscere più lingue?**  
  Sì. Imposta `ocrEngine.Language = Language.English | Language.Spanish;` prima di chiamare `Recognize()`.

- **Come limitare l’output solo ai numeri (ad es. totali)?**  
  Dopo aver ottenuto il testo semplice, esegui una regex come `\d+\.\d{2}` su `ocrEngine.Text`. Poiché abbiamo già le coordinate, puoi mappare la stringa trovata alla sua regione per evidenziare visivamente.

- **Il formato JSON è personalizzabile?**  
  La classe `JsonSaveOptions` espone diverse opzioni. Se ti serve uno schema completamente personalizzato, puoi iterare su `ocrEngine.RecognitionResult.Regions` e serializzare gli oggetti manualmente con `System.Text.Json`.

## Conclusione

Abbiamo appena dimostrato come **riconoscere testo da immagine** in C# usando Aspose.OCR, **come estrarre testo**, ottenere **estrarre coordinate del testo**, e infine **convertire la ricevuta in JSON**. L’intero flusso vive in una singola app console facile da eseguire, perfetta per prototipi o come blocco costruttivo in sistemi più grandi.

Prossimi passi? Prova a inviare il JSON a un front‑end che disegna i bounding box, oppure collega l’output a un servizio di report spese. Puoi anche sperimentare con formati immagine diversi (PNG, TIFF) o processare in batch una cartella di ricevute.

Hai altre domande su OCR, Aspose o la gestione del JSON? Lascia un commento qui sotto, e buona programmazione! 

![Esempio di immagine di ricevuta per riconoscere testo da immagine](receipt.jpg "Esempio di immagine di ricevuta")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}