---
category: general
date: 2026-04-17
description: Impara un esempio di Aspose OCR per leggere un file immagine in C#, estrarre
  il testo dall’immagine in C# e scrivere un file JSON in C#. Tutorial completo passo‑passo
  di OCR in C#.
draft: false
keywords:
- aspose ocr example
- write json file c#
- read image file c#
- extract text image c#
- c# ocr tutorial
language: it
og_description: Padroneggia un esempio di Aspose OCR per leggere un'immagine, estrarre
  il testo e scrivere un file JSON usando C#. Segui questo conciso tutorial OCR in
  C#.
og_title: esempio aspose ocr – Converti il testo dell'immagine in JSON in C#
tags:
- Aspose
- OCR
- C#
- JSON
title: esempio di aspose ocr – Converti il testo dell'immagine in JSON in C#
url: /it/net/text-recognition/aspose-ocr-example-convert-image-text-to-json-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# esempio aspose ocr – Converti il testo dell'immagine in JSON in C#

Hai mai avuto bisogno di un **aspose ocr example** che non solo legga un'immagine ma produca anche un JSON ordinato per l'elaborazione successiva? Non sei solo. In molti progetti—automazione delle fatture, scansione di ricevute o anche semplice archiviazione di documenti—gli sviluppatori si imbattono nello stesso ostacolo: “Come ottengo il risultato OCR in un formato che la mia API ama?”  

La buona notizia? Con Aspose.OCR puoi farlo in poche righe, e ti mostrerò esattamente come. Alla fine di questa guida saprai come **read image file C#**, **extract text image C#**, e **write JSON file C#**—tutto racchiuso in un tutorial OCR C# pulito e riutilizzabile.

## Cosa ti serve

- .NET 6.0 o versioni successive (il codice si compila anche con .NET Core)  
- Pacchetto NuGet Aspose.OCR per .NET (`Install-Package Aspose.OCR`)  
- Un'immagine (`input.jpg`) contenente testo chiaro e leggibile da macchina  
- Un editor di testo o Visual Studio (qualsiasi IDE va bene)

Nessun file di configurazione extra, nessuna magia nascosta—solo l'SDK e un'immagine.

## Passo 1 – Leggi il file immagine C# con Aspose.OCR

Prima di tutto: devi fornire al motore OCR un'immagine valida. Aspose.OCR si aspetta un oggetto `OcrImage`, che puoi creare direttamente da un percorso file.

```csharp
using Aspose.OCR;
using System.IO;

// Path to the source picture
string imagePath = @"C:\MyProject\Images\input.jpg";

// Load the image – this is the “read image file C#” part
OcrImage ocrImage = OcrImage.FromFile(imagePath);
```

*Perché è importante:* Caricare l'immagine in anticipo ti consente di verificare l'esistenza del file e di intercettare problemi di formato prima che il motore inizi a elaborare i pixel. Se il file manca, `FromFile` lancia un'eccezione chiara che puoi gestire a valle.

## Passo 2 – Inizializza il motore Aspose OCR

Creare il motore è poco costoso, ma dovresti avvolgerlo in un'istruzione `using` affinché le risorse vengano rilasciate prontamente.

```csharp
// Create the OCR engine – it holds all the recognition settings
using var ocrEngine = new OcrEngine();
```

*Consiglio professionale:* Il motore predefinito funziona bene per la maggior parte dei testi basati su alfabeto latino. Se ti serve una lingua diversa, puoi impostare `ocrEngine.Language = Language.YourLanguage;` prima di chiamare `Recognize`.

## Passo 3 – Estrai il testo dall'immagine C# – Esegui il riconoscimento

Ora avviene il lavoro pesante. Il metodo `Recognize` restituisce un oggetto `OcrResult` che contiene il testo grezzo, i punteggi di confidenza e le bounding box per ogni parola.

```csharp
// Run OCR – this is the “extract text image C#” step
OcrResult ocrResult = ocrEngine.Recognize(ocrImage);
```

Noterai che `ocrResult.Text` contiene la stringa semplice, mentre `ocrResult.Regions` ti fornisce dati posizionali se mai dovessi evidenziare parole in un'interfaccia utente.

## Passo 4 – Scrivi il file JSON C# – Serializza il risultato

Serializzare in JSON è semplice con `System.Text.Json`. Formatteremo l'output in modo leggibile per gli esseri umani.

```csharp
using System.Text.Json;

// Convert the OCR result to nicely formatted JSON
string json = JsonSerializer.Serialize(
    ocrResult,
    new JsonSerializerOptions { WriteIndented = true });
```

*Perché usiamo `System.Text.Json`*: È integrato in .NET, veloce e non richiede dipendenze aggiuntive. Se preferisci Newtonsoft, il codice cambia solo poche righe.

## Passo 5 – Salva il JSON su disco

Infine, scrivi la stringa su un file. Questo completa la sezione **write json file c#**.

```csharp
// Destination path for the JSON output
string jsonOutputPath = @"C:\MyProject\Output\ocrResult.json";

// Save the JSON – now you have a portable data file
File.WriteAllText(jsonOutputPath, json);

Console.WriteLine("OCR data saved as JSON.");
```

### Output JSON previsto (esempio)

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑01\nTotal: $1,234.56",
  "Regions": [
    {
      "BoundingBox": { "X": 10, "Y": 20, "Width": 200, "Height": 30 },
      "Confidence": 0.98,
      "Text": "Invoice #12345"
    },
    {
      "BoundingBox": { "X": 10, "Y": 60, "Width": 150, "Height": 30 },
      "Confidence": 0.96,
      "Text": "Date: 2024‑03‑01"
    },
    {
      "BoundingBox": { "X": 10, "Y": 100, "Width": 180, "Height": 30 },
      "Confidence": 0.99,
      "Text": "Total: $1,234.56"
    }
  ]
}
```

*Nota:* I numeri esatti varieranno in base alla tua immagine, ma la struttura rimane la stessa—perfetta per alimentare API, database o visualizzatori front‑end.

## Tutorial OCR completo in C# – Tutti i passaggi combinati

Di seguito trovi il programma completo, pronto per il copia‑incolla, che unisce tutto. Nessun pezzo mancante, nessuna scorciatoia “vedi la documentazione”.

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the image you want to process
        // -------------------------------------------------
        string imagePath = @"C:\MyProject\Images\input.jpg";
        var ocrImage = OcrImage.FromFile(imagePath);

        // -------------------------------------------------
        // Step 2: Create and configure the OCR engine
        // -------------------------------------------------
        using var ocrEngine = new OcrEngine();
        // Example: ocrEngine.Language = Language.English; // optional

        // -------------------------------------------------
        // Step 3: Perform OCR recognition
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(ocrImage);

        // -------------------------------------------------
        // Step 4: Serialize the result to indented JSON
        // -------------------------------------------------
        string json = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true });

        // -------------------------------------------------
        // Step 5: Write the JSON to a file
        // -------------------------------------------------
        string jsonOutputPath = @"C:\MyProject\Output\output.json";
        File.WriteAllText(jsonOutputPath, json);

        // -------------------------------------------------
        // Step 6: Let the user know we’re done
        // -------------------------------------------------
        Console.WriteLine("OCR data saved as JSON.");
    }
}
```

### Esecuzione del codice

1. Sostituisci i due percorsi `@"C:\MyProject\…"` con le tue directory effettive.  
2. Compila il progetto (`dotnet build`) ed eseguilo (`dotnet run`).  
3. Apri `output.json`—dovresti vedere una rappresentazione ben strutturata del testo dell'immagine.

## Domande comuni e casi particolari

**E se la mia immagine è sfocata?**  
Aspose.OCR offre opzioni di pre‑elaborazione come `ocrEngine.ImagePreprocessOptions.Deskew = true;`. Abilitalo prima di chiamare `Recognize` per migliorare l'accuratezza.

**Posso limitare l'output solo al testo semplice?**  
Certo—basta serializzare `ocrResult.Text` invece dell'intero oggetto:

```csharp
string plainJson = JsonSerializer.Serialize(
    new { Text = ocrResult.Text },
    new JsonSerializerOptions { WriteIndented = true });
```

**Devo gestire PDF multi‑pagina?**  
L'esempio si concentra su una singola immagine, ma puoi iterare su ogni immagine di pagina, eseguire gli stessi passaggi e aggregare i risultati in un array JSON.

## Consigli professionali e avvertenze

- **Percorsi file:** Usa `Path.Combine` per evitare backslash hard‑coded, soprattutto se dovessi passare a Linux.  
- **Memoria:** Per batch massivi, riutilizza una singola istanza di `OcrEngine` invece di crearne una nuova per ogni immagine.  
- **Dimensione JSON:** Se ti serve solo il testo, elimina la proprietà `Regions` per mantenere il payload piccolo.  
- **Controllo versione:** Questo tutorial è stato testato con Aspose.OCR 23.9.0; le versioni più recenti mantengono la stessa interfaccia API, ma controlla sempre le note di rilascio per eventuali cambiamenti incompatibili.

![Esempio di output JSON OCR – esempio aspose ocr](https://example.com/sample-ocr-json.png "anteprima JSON esempio aspose ocr")

## Conclusione

Abbiamo esaminato un **aspose ocr example** completo che legge un'immagine, ne estrae il testo e scrive il risultato in un file JSON usando puro C#. La soluzione è autonoma, pronta per la produzione e facile da estendere—che tu voglia aggiungere il supporto per nuove lingue, modificare le soglie di confidenza o inviare il JSON a un servizio downstream.

Se cerchi il passo successivo, prova a concatenare questo tutorial con un **C# OCR tutorial** che carica il JSON su Azure Cognitive Search, o sperimenta l'estrazione di tabelle dalle fatture. Il cielo è il limite una volta che hai il JSON in mano.

Hai un'idea da condividere? Lascia un commento, fork del repository o contattami su GitHub. Buon coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}