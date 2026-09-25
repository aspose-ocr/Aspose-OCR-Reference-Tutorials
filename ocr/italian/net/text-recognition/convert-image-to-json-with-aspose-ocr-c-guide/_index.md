---
category: general
date: 2026-01-15
description: Converti l'immagine in JSON usando Aspose OCR in C#. Scopri come estrarre
  il testo dall'immagine, ottenere i riquadri di delimitazione in JSON e riconoscere
  l'immagine della ricevuta.
draft: false
keywords:
- convert image to json
- extract text from image
- aspose ocr c# example
- recognize receipt image
- json bounding boxes
language: it
og_description: Converti l'immagine in JSON usando Aspose OCR in C#. Guida passo‑passo
  per estrarre il testo dall'immagine, riconoscere l'immagine della ricevuta e ottenere
  i riquadri di delimitazione in JSON.
og_title: Converti immagine in JSON con la guida Aspose OCR C#
tags:
- Aspose OCR
- C#
- JSON
- Image Processing
title: Converti immagine in JSON con la Guida Aspose OCR C#
url: /it/net/text-recognition/convert-image-to-json-with-aspose-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Converti immagine in JSON con Aspose OCR C# Guida

Hai mai avuto bisogno di **convertire immagine in JSON** ma non eri sicuro quale libreria potesse darti sia il testo grezzo sia le coordinate esatte delle parole? Non sei solo. Molti sviluppatori si trovano di fronte a questo ostacolo quando cercano di estrarre testo da file immagine—specialmente ricevute—avendo anche bisogno di un payload JSON leggibile da macchine per l'elaborazione a valle.

In questo tutorial percorreremo un esempio completo di **Aspose OCR C#** che mostra come estrarre testo da un'immagine, riconoscere l'immagine di una ricevuta e generare **JSON bounding boxes** per ogni parola. Alla fine avrai un'app console pronta all'uso che stampa una stringa JSON formattata bene che puoi inviare a qualsiasi API, database o pipeline di analisi.

> **Cosa otterrai**  
> • Un progetto C# completamente funzionale che **converte immagine in JSON**  
> Comprensione del motivo per cui abilitiamo `IncludeBoundingBoxes` (è la chiave per i `json bounding boxes`)  
> • Suggerimenti per gestire diversi formati di immagine e lingue  

Cominciamo.

---

## Cosa ti serve

- **.NET 6.0 SDK** (o qualsiasi versione successiva) – il codice è destinato a .NET 6 ma funziona anche su .NET Framework 4.7+.  
- **Aspose.OCR for .NET** pacchetto NuGet – puoi installarlo tramite `dotnet add package Aspose.OCR`.  
- Un'immagine di esempio di ricevuta (`receipt.jpg`) posizionata in una cartella a cui puoi fare riferimento dal tuo progetto.  
- Visual Studio 2022, VS Code, o qualsiasi IDE tu preferisca.

Non sono richiesti altri servizi esterni; tutto gira localmente.

## Converti imm in JSON – Panoramica

L'idea di base è semplice: caricare un'immagine, dire ad Aspose OCR di riconoscere l'inglese (o qualsiasi lingua supportata), chiedere di includere le bounding box e infine richiedere il risultato in formato **JSON**. La libreria si occupa di tutto il lavoro pesante—OCR, analisi del layout e serializzazione JSON.

Ecco un diagramma del flusso (immagina una piccola immagine):

```
[Image File] → Aspose OCR Engine → Recognition Options (JSON + Bounding Boxes) → JSON Output
```

Quel piccolo diagramma cattura l'intera pipeline che implementeremo.

## Passo 1: Configura il Progetto e Installa Aspose OCR

Per prima cosa, crea un nuovo progetto console e aggiungi il pacchetto Aspose OCR.

```bash
dotnet new console -n JsonOutputDemo
cd JsonOutputDemo
dotnet add package Aspose.OCR
```

> **Consiglio pro:** Se usi Visual Studio, fai clic con il tasto destro sul progetto → *Gestisci Pacchetti NuGet* → cerca **Aspose.OCR** e installa l'ultima versione stabile (attualmente .).

## Passo 2: Carica l'Immagine da Riconoscere

Useremo il metodo `OcrImage.FromFile` per leggere l'immagine della ricevuta. Assicurati che il percorso punti a un file reale; altrimenti otterrai una `FileNotFoundException`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // Step 2: Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

Se la tua immagine si trova accanto al file `.csproj`, puoi semplicemente usare `"receipt.jpg"`.

## Passo 3: Configura le Opzioni OCR per le Bounding Box JSON

La magia avviene quando abilitiamo `OutputFormat = OutputFormat.Json` **e** `IncludeBoundingBoxes = true`. Il primo indica ad Aspose di serializzare il risultato come JSON, mentre il secondo aggiunge `x`, `y`, `width` e `height` per ogni parola—esattamente ciò di cui hai bisogno per i `json bounding boxes`.

```csharp
        // Step 3: Configure OCR options
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };
```

Puoi anche modificare `ocrOptions.Dpi` o `ocrOptions.Language` se ti serve una risoluzione più alta o una lingua diversa.

## Passo 4: Esegui il Riconoscimento – Estrai il Testo dall'Immagine

Ora chiamiamo `Recognize`. Il metodo restituisce un oggetto `OcrResult` che contiene la stringa JSON, il testo grezzo e altro.

```csharp
        // Step 4: Perform recognition using English language and the configured options
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);
```

Se devi gestire altre lingue, sostituisci `Language.English` con `Language.Spanish`, `Language.French`, ecc. Aspose supporta più di 30 lingue pronte all'uso.

## Passo 5: Output del Risultato – Il Tuo Payload JSON

Infine, stampiamo il JSON sulla console. In un'app reale probabilmente lo scriveresti su un file o lo invieresti a un servizio.

```csharp
        // Step 5: Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

Eseguendo il programma dovrebbe produrre un documento JSON simile allo snippet qui sotto.

```json
{
  "Text": "Total $12.34\nDate 01/01/2024",
  "Words": [
    {
      "Text": "Total",
      "BoundingBox": { "X": 45, "Y": 112, "Width": 60, "Height": 20 }
    },
    {
      "Text": "$12.34",
      "BoundingBox": { "X": 110, "Y": 112, "Width": 70, "Height": 20 }
    },
    {
      "Text": "Date",
      "BoundingBox": { "X": 45, "Y": 140, "Width": 50, "Height": 20 }
    },
    {
      "Text": "01/01/2024",
      "BoundingBox": { "X": 100, "Y": 140, "Width": 120, "Height": 20 }
    }
  ]
}
```

Nota come ogni parola ora porta la sua **JSON bounding box**—perfetta da inserire in un overlay UI o in un parser a valle.

## Esempio Completo Funzionante

Di seguito trovi il programma completo, pronto per il copia‑incolla. Nessuna parte nascosta, nessuna chiamata esterna—solo puro C#.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");

        // 3️⃣ Configure OCR options to get detailed JSON output with word positions
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };

        // 4️⃣ Perform recognition using English language and the configured options
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);

        // 5️⃣ Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

> **Attenzione a:**  
> • **Errori di percorso file** – verifica nuovamente la posizione dell'immagine.  
> • **Pacchetto NuGet mancante** – assicurati che `Aspose.OCR` sia referenziato.  
> • **Formati immagine non supportati** – usa JPEG, PNG, BMP o TIFF per i migliori risultati.

## Domande Frequenti & Casi Limite

### Posso convertire una **pagina PDF** in JSON invece di un JPEG?

Sì. Converti prima la pagina PDF in un'immagine (ad es., usando `Aspose.PDF`), poi passa quell'immagine nella stessa pipeline OCR. L'output JSON sarà identico perché il passo OCR si occupa solo di dati raster.

### Cosa succede se la ricevuta è sfocata?

Aumenta il DPI in `ocrOptions`. Per esempio:

```csharp
ocrOptions.Dpi = 300; // higher DPI improves accuracy on low‑quality scans
```

Un DPI più alto può aumentare l'uso di memoria, quindi bilancia qualità e prestazioni.

### Ho bisogno di **più lingue** sulla stessa ricevuta (ad es., Inglese + Spagnolo).

Puoi passare un array di lingue:

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, new[] { Language.English, Language.Spanish }, ocrOptions);
```

Aspose cercherà di riconoscere ogni lingua nell'ordine specificato.

### Come scrivo il JSON su un file?

Basta sostituire la riga `Console.WriteLine` con:

```csharp
System.IO.File.WriteAllText("receipt.json", ocrResult.Json);
```

Ora hai un file persistente che puoi inviare ad altri servizi.

## Riepilogo Visivo

![esempio di conversione immagine in json](convert-image-to-json.png "esempio di conversione immagine in json")

*Lo screenshot mostra l'output della console del payload JSON dopo aver eseguito la demo.*

## Conclusione

Ti abbiamo appena mostrato come **convertire immagine in JSON** usando Aspose OCR in C#. Configurando `OutputFormat` e `IncludeBoundingBoxes`, puoi **estrarre testo dall'immagine**, **riconoscere l'immagine della ricevuta**, e ottenere precise **JSON bounding boxes** per ogni parola. Il codice completo e eseguibile è nello snippet sopra, così puoi inserirlo in qualsiasi progetto .NET subito.

Cosa fare dopo? Prova a inviare il JSON a un visualizzatore front‑end che evidenzia ogni parola, o invia i dati a un modello di machine‑learning che classifica le voci di spesa sulle ricevute. Puoi anche sperimentare con altre lingue, impostazioni DPI più alte, o elaborare più immagini in batch in un ciclo.

Se incontri problemi, ricorda i consigli su percorsi file, DPI e array di lingue. Sentiti libero di lasciare un commento o aprire un issue sul repository GitHub che crei per questa demo. Buon coding e divertiti a trasformare le immagini in JSON strutturato!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}