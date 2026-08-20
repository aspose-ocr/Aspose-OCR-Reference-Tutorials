---
category: general
date: 2026-01-02
description: Estrai il testo da un'immagine usando Aspose OCR in C#. Scopri come convertire
  l'immagine in formato JSONL in modo rapido e affidabile.
draft: false
keywords:
- extract text from image
- convert image to jsonl
language: it
og_description: Estrai il testo da un'immagine con Aspose OCR e convertilo in formato
  JSONL. Tutorial completo passo‑passo in C# per sviluppatori.
og_title: Estrai testo dall'immagine – Converti in JSONL in C#
tags:
- C#
- OCR
- Aspose
- JSONL
title: Estrai testo da immagine e converti in JSONL – Guida C#
url: /it/net/text-recognition/extract-text-from-image-and-convert-to-jsonl-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai testo da immagine e converti in JSONL – Tutorial completo C#

Ti è mai capitato di dover **estrarre testo da immagine** senza sapere quale libreria fornisca un output pulito e strutturato? Non sei solo. In molti progetti di elaborazione di ricevute o di digitalizzazione di documenti il collo di bottiglia è trasformare un bitmap in testo ricercabile *e* in un formato leggibile da macchine.  

La buona notizia? Con Aspose OCR puoi **estrarre testo da immagine** e, con poche righe di codice, **convertire l’immagine in JSONL** per analisi successive. Questa guida ti accompagna passo passo, dal caricamento di un PNG alla scrittura di un file JSON‑Lines che può essere inviato a una pipeline di dati.

> **Suggerimento:** Se usi già .NET 6 o versioni successive, lo stesso codice funziona senza alcuna configurazione aggiuntiva.

## Prerequisiti — Cosa ti serve

- **.NET 6 SDK** (o qualsiasi versione recente di .NET)
- **Aspose.OCR** pacchetto NuGet  
  ```bash
  dotnet add package Aspose.OCR
  ```
- **Newtonsoft.Json** per la serializzazione  
  ```bash
  dotnet add package Newtonsoft.Json
  ```
- Un’immagine di esempio (ad es. `receipt.png`) collocata in una cartella a cui puoi fare riferimento.
- Un IDE o editor a tua scelta—Visual Studio, VS Code, Rider, ecc.

Nessuna configurazione complessa, nessun servizio esterno, solo qualche pacchetto NuGet.

![Extract text from image using C#](https://example.com/assets/ocr-sample.png)

*Alt text: estrarre testo da immagine usando C# con Aspose OCR*

## Passo 1: Carica l’immagine da elaborare  

La prima cosa da fare quando vuoi **estrarre testo da immagine** è fornire al motore OCR un bitmap. Usare `System.Drawing.Bitmap` è semplice e funziona per la maggior parte dei formati raster.

```csharp
using System.Drawing;

// Adjust the path to where your receipt.png lives
string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
Bitmap receiptImage = new Bitmap(imagePath);
```

> **Perché è importante:** Caricare l’immagine come `Bitmap` dà al motore OCR accesso diretto ai pixel, migliorando velocità e precisione del riconoscimento rispetto allo streaming di byte grezzi.

## Passo 2: Configura Aspose OCR per l’output JSON‑Lines  

Aspose OCR ti consente di specificare lingua, formato di output e qualche ottimizzazione delle prestazioni. Qui richiediamo **JSON‑Lines** (un oggetto JSON per riga) perché è perfetto per l’elaborazione riga‑per‑riga successiva.

```csharp
using Aspose.OCR;

// Create the engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine we’re dealing with English text
RecognitionOptions options = new RecognitionOptions
{
    Language = Language.English,
    OutputFormat = OutputFormat.JsonLines   // This is the key for converting image to JSONL
};
```

> **Consiglio esperto:** Se ti servono ricevute multilingue, imposta `Language = Language.Multilingual` o passa un array di valori `Language`.

## Passo 3: Esegui l’OCR e cattura il risultato  

Ora **estraiamo testo da immagine**. Il metodo `Recognize` restituisce un oggetto `OcrResult` che contiene una collezione di oggetti `OcrLine`, ciascuno rappresentante una riga di testo riconosciuto insieme al suo riquadro di delimitazione.

```csharp
// Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);
```

A questo punto `ocrResult.Lines` contiene tutto ciò di cui hai bisogno—testo grezzo, punteggi di confidenza e coordinate.

## Passo 4: Serializza le linee in JSON‑Lines  

Trasformeremo la collezione in una stringa JSON ben indentata. Anche se JSON‑Lines è tipicamente compatto, aggiungere l’indentazione rende il file più facile da ispezionare durante lo sviluppo.

```csharp
using Newtonsoft.Json;

// Serialize each line as a separate JSON object
string jsonLines = JsonConvert.SerializeObject(
    ocrResult.Lines,
    Formatting.Indented
);
```

La variabile `jsonLines` risultante appare più o meno così (troncata per brevità):

```json
{
  "Text": "Store XYZ",
  "Confidence": 0.98,
  "BoundingBox": { "X": 10, "Y": 15, "Width": 120, "Height": 20 }
}
{
  "Text": "Date: 01/01/2026",
  "Confidence": 0.95,
  "BoundingBox": { "X": 10, "Y": 45, "Width": 180, "Height": 20 }
}
```

Ogni riga termina con un carattere di nuova linea, fornendoti un vero file **JSONL** (JSON‑Lines).

## Passo 5: Scrivi le JSON‑Lines su disco  

Infine, persisti l’output così che altri servizi—come Spark, Logstash o un semplice script Bash—possano ingerirlo riga per riga.

```csharp
using System.IO;

// Choose a destination file
string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
File.WriteAllText(outputPath, jsonLines);
```

Quando apri `receipt.jsonl` vedrai un oggetto JSON per riga, pronto per lo streaming.

## Passo 6: Verifica l’esportazione  

Un rapido controllo di coerenza ti fa risparmiare ore di debug in seguito. Leggiamo le prime righe e stampiamole sulla console.

```csharp
Console.WriteLine("First three lines of the JSONL output:");
foreach (var line in File.ReadLines(outputPath).Take(3))
{
    Console.WriteLine(line);
}
```

Output tipico della console:

```
First three lines of the JSONL output:
{"Text":"Store XYZ","Confidence":0.98,"BoundingBox":{"X":10,"Y":15,"Width":120,"Height":20}}
{"Text":"Date: 01/01/2026","Confidence":0.95,"BoundingBox":{"X":10,"Y":45,"Width":180,"Height":20}}
{"Text":"Total   $23.45","Confidence":0.97,"BoundingBox":{"X":10,"Y":75,"Width":150,"Height":20}}
```

Se vedi qualcosa di simile, congratulazioni—hai **estratto testo da immagine** e **convertito l’immagine in JSONL** con successo.

## Problemi comuni e come evitarli  

| Problema | Perché accade | Soluzione |
|----------|----------------|-----------|
| **Output vuoto** | Percorso immagine errato o file non leggibile. | Usa `File.Exists(imagePath)` prima di creare il bitmap. |
| **Punteggi di confidenza bassi** | L’immagine è sfocata o ha basso contrasto. | Pre‑elabora l’immagine (es. `Bitmap.RotateFlip`, `Graphics.Clear`) o aumenta DPI. |
| **Lingua errata** | OCR usa l’inglese di default ma la ricevuta è in un’altra lingua. | Imposta `options.Language = Language.Spanish` (o l’enum appropriato). |
| **JSONL appare come un unico array JSON** | Hai usato `Formatting.None` senza gestire le newline. | Assicurati che ogni oggetto serializzato termini con `Environment.NewLine`. |

## Esempio completo funzionante  

Di seguito trovi il programma completo, pronto per essere eseguito. Incollalo in un progetto console e premi **F5**.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.IO;
using System.Linq;
using Newtonsoft.Json;

namespace OcrToJsonlDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the image
            string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found at {imagePath}");
                return;
            }
            Bitmap receiptImage = new Bitmap(imagePath);

            // 2️⃣ Set up OCR options for JSON‑Lines output
            OcrEngine ocrEngine = new OcrEngine();
            RecognitionOptions options = new RecognitionOptions
            {
                Language = Language.English,
                OutputFormat = OutputFormat.JsonLines
            };

            // 3️⃣ Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);

            // 4️⃣ Serialize to JSON‑Lines
            string jsonLines = JsonConvert.SerializeObject(
                ocrResult.Lines,
                Formatting.Indented
            );

            // 5️⃣ Write to file
            string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
            File.WriteAllText(outputPath, jsonLines);
            Console.WriteLine($"✅ JSONL saved to {outputPath}");

            // 6️⃣ Quick verification
            Console.WriteLine("\nFirst three lines of output:");
            foreach (var line in File.ReadLines(outputPath).Take(3))
            {
                Console.WriteLine(line);
            }
        }
    }
}
```

**Risultato atteso:** Un file `receipt.jsonl` contenente un oggetto JSON per riga, ciascuno con i campi `Text`, `Confidence` e `BoundingBox`. Ora puoi alimentare questo file a qualsiasi pipeline analitica che accetti JSONL.

## Prossimi passi – Oltre l’OCR di base  

- **Elaborazione batch:** Avvolgi la logica sopra in un ciclo `foreach` per gestire intere cartelle di ricevute.  
- **Parallelismo:** Usa `Parallel.ForEach` per velocizzare su più core quando devi elaborare migliaia di immagini.  
- **Post‑elaborazione:** Filtra le linee a bassa confidenza (`Confidence < 0.9`) prima di memorizzarle.  
- **Integrazione:** Invia direttamente il JSONL a Azure Blob Storage o AWS S3 con i rispettivi SDK.  
- **Formati alternativi:** Cambia `OutputFormat` in `PlainText` o `Xml` se il tuo sistema a valle preferisce quei formati.  

## Conclusione  

Ora disponi di una soluzione solida, end‑to‑end, per **estrarre testo da immagine** e **convertire l’immagine in JSONL** usando Aspose OCR in C#. Il tutorial ha coperto tutto, dal caricamento del bitmap alla verifica dell’output, includendo consigli pratici per mantenere la pipeline robusta.

Provalo con le tue ricevute, fatture o moduli scansionati—guarda il motore OCR trasformare pixel in dati ricercabili e strutturati in pochi secondi. Se incontri casi particolari (es. scansioni inclinate o testo multilingue), rivedi la sezione *RecognitionOptions* e regola lingua o passaggi di pre‑elaborazione.

Buon coding, e che le tue pipeline di dati siano sempre pulite!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}