---
category: general
date: 2026-02-17
description: Come eseguire OCR in C# e convertire rapidamente un'immagine in JSON.
  Segui questo tutorial OCR in C# per estrarre il testo dalle immagini e salvare il
  layout come JSON.
draft: false
keywords:
- how to perform OCR
- convert image to json
- c# ocr tutorial
- extract text image c#
- load image file c#
language: it
og_description: Come eseguire l'OCR in C#? Questa guida ti mostra come convertire
  un'immagine in JSON, estrarre il testo dall'immagine in C# e caricare il file immagine
  per l'OCR.
og_title: Come eseguire OCR in C# – Converti immagine in JSON
tags:
- OCR
- C#
- Aspose
title: Come eseguire OCR in C# – Guida alla conversione di immagini in JSON
url: /it/net/text-recognition/how-to-perform-ocr-in-c-convert-image-to-json-guide/
---

un terminale."

Make sure to keep markdown formatting.

Now produce final translation.

Let's craft.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR in C# – Guida alla conversione di un'immagine in JSON

Ti sei mai chiesto **come eseguire OCR** su una ricevuta, fattura o qualsiasi documento scansionato usando C#? Non sei il solo. Molti sviluppatori si trovano bloccati quando devono estrarre testo *e* preservare il layout senza passare ore a scrivere parser personalizzati.  

In questo tutorial percorreremo un **c# ocr tutorial** completo che mostra esattamente come eseguire OCR, **convertire immagine in json**, e salvare il risultato per analisi successive. Alla fine avrai un'app console pronta‑da‑eseguire che carica un file immagine in C#, estrae il testo e scrive un file JSON dettagliato contenente coordinate, punteggi di confidenza e il testo grezzo.

## Prerequisiti — Cosa ti serve

- .NET 6 SDK o successivo (il codice funziona anche su .NET Core)  
- Visual Studio 2022 o qualsiasi editor tu preferisca  
- Una licenza Aspose OCR (puoi iniziare con una prova gratuita)  
- Un’immagine di esempio, ad es. `receipt.png`, posizionata in una cartella a cui puoi fare riferimento  

Questo è tutto—nessun pacchetto NuGet aggiuntivo oltre a `Aspose.OCR`. Se hai questi elementi, sei pronto per partire.

## Come eseguire OCR e ottenere l'output JSON

Il cuore di **come eseguire OCR** con Aspose è semplice: crea un `OcrEngine`, fornisci uno stream immagine, chiama `Recognize`, e poi serializza l'`OcrResult` in JSON. Vediamolo passo passo.

### Passo 1: Installa il pacchetto NuGet Aspose OCR

Apri il terminale nella cartella del progetto ed esegui:

```bash
dotnet add package Aspose.OCR
```

> **Consiglio:** Usa il flag `--version` per bloccare alla versione stabile più recente (es. `23.9.0`). Questo rende la tua build riproducibile.

### Passo 2: Crea lo scheletro del progetto console

Se non hai ancora un progetto, creane uno:

```bash
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo
```

Ora hai un file `Program.cs` pronto per il codice che **caricherà il file immagine c#** e avvierà il processo OCR.

### Passo 3: Scrivi il codice completo OCR‑to‑JSON

Di seguito trovi il programma completo, pronto‑da‑eseguire. Copialo e incollalo in `Program.cs`. Ogni riga è commentata così puoi capire *perché* ogni parte è importante.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonOutput
{
    static void Main()
    {
        // ---------------------------------------------------------
        // 1️⃣  Initialize the OCR engine – this object holds
        //     language settings, recognition options, etc.
        // ---------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---------------------------------------------------------
        // 2️⃣  Load the image you want to analyze.
        //     This demonstrates **load image file c#** in a clean way.
        // ---------------------------------------------------------
        // Replace the path with the actual location of your receipt.png
        string imagePath = Path.Combine(
            Environment.CurrentDirectory, "receipt.png");
        ImageStream image = ImageStream.FromFile(imagePath);

        // ---------------------------------------------------------
        // 3️⃣  Perform the recognition.
        //     The engine returns an OcrResult containing text,
        //     confidence scores, and layout information.
        // ---------------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // ---------------------------------------------------------
        // 4️⃣  Convert the result to a detailed JSON string.
        //     This is the heart of **convert image to json**.
        // ---------------------------------------------------------
        string jsonResult = ocrResult.ToJson();

        // ---------------------------------------------------------
        // 5️⃣  Save the JSON to disk – you can later import this into
        //     databases, analytics pipelines, or UI components.
        // ---------------------------------------------------------
        string jsonPath = Path.Combine(
            Environment.CurrentDirectory, "receipt.json");
        File.WriteAllText(jsonPath, jsonResult);

        // ---------------------------------------------------------
        // 6️⃣  Let the user know we’re done.
        // ---------------------------------------------------------
        Console.WriteLine("JSON with layout saved to " + jsonPath);
    }
}
```

#### Cosa fa il codice

| Passo | Perché è importante |
|------|----------------------|
| **Initialize OcrEngine** | Imposta la lingua predefinita (English) e prepara i modelli interni. |
| **Load image file** | L'uso di `ImageStream.FromFile` garantisce che l'immagine sia letta nel formato atteso da Aspose. |
| **Recognize** | Il lavoro pesante—analisi dei pixel, segmentazione dei caratteri e ricerca nel dizionario. |
| **ToJson** | Produce un output strutturato che include bounding box, confidenza e testo grezzo. |
| **WriteAllText** | Persiste il JSON così puoi condividerlo con altri servizi. |
| **Console.WriteLine** | Fornisce un feedback immediato—utile quando si esegue da un terminale. |

> **Attenzione:** Se la tua immagine è grande, considera di ridimensionarla prima per migliorare velocità e consumo di memoria. Aspose fornisce metodi `Resize` che puoi chiamare su `ImageStream`.

### Passo 4: Esegui l'applicazione e verifica l'output

Dal terminale:

```bash
dotnet run
```

Dovresti vedere:

```
JSON with layout saved to C:\Path\To\OcrJsonDemo\receipt.json
```

Apri `receipt.json` in qualsiasi editor; troverai qualcosa di simile:

```json
{
  "Pages": [
    {
      "Blocks": [
        {
          "Text": "Total: $12.34",
          "Confidence": 0.98,
          "BoundingBox": { "X": 120, "Y": 340, "Width": 150, "Height": 30 }
        }
      ]
    }
  ]
}
```

Quel JSON cattura **extract text image c#** più i metadati di layout, perfetto per l'elaborazione a valle.

## Converti immagine in JSON – Oltre le basi

Ora che sai **come eseguire OCR**, esploriamo un paio di varianti che potresti necessitare nei progetti reali.

### Gestione di più pagine

Se la tua sorgente è un PDF o TIFF multi‑pagina, basta iterare su ogni pagina:

```csharp
foreach (var pageStream in multiPageImageStreams)
{
    OcrResult result = ocrEngine.Recognize(pageStream);
    // Append each page's JSON to a master list
}
```

### Personalizzare lingua e accuratezza

Aspose supporta oltre 40 lingue. Per passare allo spagnolo:

```csharp
ocrEngine.Language = Language.Spanish;
```

Puoi anche modificare `ocrEngine.Settings` per abilitare **auto‑rotate**, **rimozione rumore**, o **correzione basata su dizionario**—tutte funzionalità che migliorano la qualità del JSON ottenuto.

### Salvataggio del JSON in formato “pretty‑printed”

Se preferisci un JSON indentato per una migliore leggibilità:

```csharp
string prettyJson = ocrResult.ToJson(true); // true = formatted
File.WriteAllText(jsonPath, prettyJson);
```

## Caricare file immagine C# – Problemi comuni e consigli

Quando **carichi file immagine c#**, potresti incontrare:

- **File non trovato** – Assicurati che il percorso sia assoluto o usa `Path.Combine` con `Environment.CurrentDirectory`.  
- **Formato non supportato** – Aspose gestisce PNG, JPEG, BMP, TIFF e PDF. Per formati RAW, convertili prima.  
- **Elevata pressione di memoria su file grandi** – Usa `ImageStream.FromFile(path, maxSizeInKB)` per ridimensionare al caricamento.

Affrontare questi problemi fin da subito ti salva da eccezioni criptiche più tardi nella pipeline OCR.

## Estrarre testo da immagine C# – Verifica dei risultati

Dopo aver ottenuto il JSON, potresti volere solo il testo semplice:

```csharp
var ocrResult = ocrEngine.Recognize(image);
string plainText = ocrResult.Text; // Simple string with line breaks
Console.WriteLine(plainText);
```

Questo snippet dimostra **extract text image c#** senza i dettagli di layout—utile per ricerche rapide o logging.

---

![Diagramma che mostra il flusso di lavoro OCR – come eseguire OCR, convertire immagine in JSON e estrarre testo immagine c#](/images/ocr-workflow.png "flusso di lavoro come eseguire OCR")

*Testo alternativo immagine: "diagramma del flusso di lavoro OCR che illustra la conversione di immagine in JSON e l'estrazione di testo immagine c#"*  

*(L'immagine è un segnaposto; sostituiscila con un diagramma reale quando pubblichi.)*

---

## Conclusione

Abbiamo coperto **come eseguire OCR** in C# dall'inizio alla fine, mostrato come **convertire immagine in JSON**, e spiegato le sfumature di **load image file c#** e **extract text image c#**. L'esempio di codice completo è pronto per essere inserito in qualsiasi progetto .NET, e l'output JSON ti fornisce sia il testo grezzo sia dati di layout precisi per analisi successive.

Qual è il prossimo passo? Prova a inserire il JSON in un database, visualizzare le bounding box in un'interfaccia UI, o concatenare più esecuzioni OCR per elaborazioni batch. Puoi anche sperimentare altre funzionalità Aspose come il riconoscimento della scrittura a mano o il rilevamento di codici a barre—entrambi si integrano naturalmente nello stesso flusso.

Se incontri difficoltà, ricontrolla i consigli di risoluzione problemi nella sezione “Load Image File C#”, o esplora la documentazione completa di Aspose per impostazioni avanzate. Buon coding e divertiti a trasformare le immagini in dati strutturati!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}