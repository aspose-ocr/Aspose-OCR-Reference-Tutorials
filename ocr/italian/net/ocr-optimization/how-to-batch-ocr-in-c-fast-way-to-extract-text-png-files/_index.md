---
category: general
date: 2026-04-03
description: Impara come eseguire l'OCR in batch con Aspose.OCR in C#. Questa guida
  ti mostra come estrarre testo da immagini PNG e convertire le immagini in testo
  in modo efficiente.
draft: false
keywords:
- how to batch ocr
- extract text png
- convert images to text
- Aspose OCR
- C# parallel processing
language: it
og_description: Scopri come eseguire OCR batch in C# per estrarre testo da immagini
  PNG e convertire le immagini in testo usando Aspose.OCR. Codice completo incluso.
og_title: Come eseguire OCR in batch in C# – Guida rapida
tags:
- OCR
- C#
- Aspose
title: Come eseguire OCR in batch in C# – Metodo veloce per estrarre testo da file
  PNG
url: /it/net/ocr-optimization/how-to-batch-ocr-in-c-fast-way-to-extract-text-png-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR batch in C# – Metodo veloce per estrarre testo da file PNG

Ti sei mai chiesto **come eseguire OCR batch** su un’intera cartella di screenshot senza scrivere un ciclo per ogni file? Non sei l’unico. In molti progetti—pensa alla digitalizzazione di fatture o all’archiviazione di ricevute scannerizzate—ti ritrovi con decine, a volte centinaia, di file PNG a cui è necessario estrarre il testo. La buona notizia? Con Aspose.OCR puoi **estrarre testo da immagini PNG** in parallelo, e l’intero processo può essere racchiuso in poche righe di C#.

In questo tutorial percorreremo un esempio completo, pronto‑all‑uso, che mostra **come convertire immagini in testo** usando un processore batch. Copriremo i prerequisiti, spiegheremo perché ogni riga è importante e inseriremo anche qualche pro‑tip per evitare gli errori più comuni.

## Prerequisiti

Prima di iniziare, assicurati di avere:

- **.NET 6.0** (o successivo) installato sulla tua macchina. I runtime più vecchi funzionano, ma l’ultima versione offre migliori prestazioni e supporto async.
- Pacchetto **Aspose.OCR for .NET**. Puoi ottenerlo via NuGet: `dotnet add package Aspose.OCR`.
- Una cartella piena di immagini **PNG** che desideri elaborare. La chiameremo `YOUR_DIRECTORY` per tutto il tutorial.
- Una quantità moderata di RAM—l’OCR batch può consumare molta memoria se aumenti troppo il parallelismo, ma usando `Environment.ProcessorCount` rimane sotto controllo.

> **Pro tip:** Se lavori su una pipeline CI/CD, aggiungi il file di licenza Aspose come secret per evitare il limite di 20 pagine della valutazione gratuita.

Ora, mettiamoci al lavoro.

## Step 1: Set Up the Batch OCR Processor (Primary Keyword in Header)

La prima cosa di cui hai bisogno è un’istanza di `BatchOcrProcessor`. Questa classe astrae la logica di threading e ti permette di concentrarti su cosa fare con ogni immagine.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Create a batch OCR processor and tell it to use all CPU cores
        var ocrBatch = new BatchOcrProcessor
        {
            Engine = new OcrEngine(),
            MaxDegreeOfParallelism = Environment.ProcessorCount
        };
```

**Perché è importante:**  
- `Engine = new OcrEngine()` ti fornisce un motore OCR nuovo per ogni thread, evitando conflitti.  
- `MaxDegreeOfParallelism = Environment.ProcessorCount` scala automaticamente al numero di core, garantendo il massimo throughput senza doverlo regolare manualmente.

## Step 2: Hook Into Progress Events (Helps Track Extraction)

Vedere l’avanzamento è essenziale quando si elaborano centinaia di file. L’evento `ProgressChanged` viene sollevato dopo il completamento di ciascun file, permettendoti di registrare lo stato.

```csharp
        // Subscribe to progress updates so we know which file is being processed
        ocrBatch.ProgressChanged += (s, e) =>
            Console.WriteLine($"Processed {e.Current}/{e.Total}: {e.FilePath}");
```

**Perché lo adorerai:**  
- Un feedback in tempo reale ti impedisce di chiederti se l’applicazione si è bloccata.  
- Se mai dovessi mettere in pausa o annullare l’operazione, hai già un hook per confrontare `e.Current` con `e.Total`.

## Step 3: Define the Folder Scan and File Pattern (Extract Text PNG)

Ora indichiamo al processore dove cercare e che tipo di file raccogliere. Il pattern `"*.png"` assicura che vengano gestite solo le immagini PNG.

```csharp
        // Run OCR on every PNG image in the target folder
        ocrBatch.ProcessFolder(
            @"YOUR_DIRECTORY",          // folder containing the images
            "*.png",                    // file pattern
            (imagePath, ocrText) =>     // callback for each processed file
            {
                // Step 4 is inside this callback – see next section
            });
```

**Perché è fondamentale:**  
- L’uso di un pattern glob mantiene il codice flessibile; basta cambiare `*.png` in `*.jpg` se in seguito dovrai gestire JPEG.  
- Il callback riceve sia il percorso dell’immagine sia il testo riconosciuto, dandoti pieno controllo su cosa fare dopo.

## Step 4: Save Recognized Text Next to the Source (Convert Images to Text)

All’interno del callback scriveremo l’output OCR in un file `.txt` posizionato accanto al PNG originale. Questo è il modo più semplice per **convertire immagini in testo** per ulteriori elaborazioni.

```csharp
                // Save the recognized text next to the image as a .txt file
                string txtPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(txtPath, ocrText);
```

**Perché scegliamo un file `.txt` affiancato:**  
- Mantiene la relazione evidente—apri il PNG, apri il TXT, confronta.  
- Non serve un database o uno strato di storage aggiuntivo in progetti di piccola scala.

## Step 5: Wrap Up with a Friendly Completion Message

Un messaggio di console pulito ti informa quando tutto è terminato.

```csharp
        // Indicate that batch processing has finished
        Console.WriteLine("Batch processing completed.");
    }
}
```

Quando esegui il programma, vedrai un output simile a:

```
Processed 1/27: C:\Images\invoice1.png
Processed 2/27: C:\Images\invoice2.png
...
Batch processing completed.
```

Ogni PNG ora ha un file `.txt` gemello contenente il testo estratto.

## Full Working Example (All Steps Combined)

Di seguito trovi l’intero programma che puoi copiare‑incollare in un nuovo progetto console. Nessuna parte è mancante—basta sostituire `YOUR_DIRECTORY` con il percorso assoluto delle tue immagini.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create a batch OCR processor and configure it to use all CPU cores
        var ocrBatch = new BatchOcrProcessor
        {
            Engine = new OcrEngine(),
            MaxDegreeOfParallelism = Environment.ProcessorCount
        };

        // Step 2: Subscribe to progress updates to see which file is being processed
        ocrBatch.ProgressChanged += (s, e) =>
            Console.WriteLine($"Processed {e.Current}/{e.Total}: {e.FilePath}");

        // Step 3: Run OCR on every PNG image in the target folder
        ocrBatch.ProcessFolder(
            @"C:\MyImages",          // folder containing the images
            "*.png",                // file pattern
            (imagePath, ocrText) => // callback for each processed file
            {
                // Step 4: Save the recognized text next to the image as a .txt file
                string txtPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(txtPath, ocrText);
            });

        // Step 5: Indicate that batch processing has finished
        Console.WriteLine("Batch processing completed.");
    }
}
```

### Expected Result

- Per ogni `image.png` in `C:\MyImages`, appare un `image.txt` accanto.
- La console stampa le righe di avanzamento, facilitando il monitoraggio di batch di grandi dimensioni.
- Nessun ciclo manuale o gestione di thread—`BatchOcrProcessor` si occupa di tutto.

## Common Questions & Edge Cases

### What if my images are not PNGs?

Basta cambiare il secondo argomento in `ProcessFolder` in `"*.jpg"` o `"*.*"` per includere tutti i file. Il motore OCR funziona con la maggior parte dei formati raster.

### How much memory does this consume?

`BatchOcrProcessor` carica un’immagine per thread. Con `Environment.ProcessorCount` impostato, ad esempio, a 8 core, avrai otto immagini in memoria contemporaneamente. Se incontri eccezioni OutOfMemory, riduci il parallelismo:

```csharp
MaxDegreeOfParallelism = 4; // or any number that fits your machine
```

### Can I customize the OCR language?

Assolutamente. Dopo aver creato il motore, imposta la sua proprietà `Language`:

```csharp
Engine = new OcrEngine { Language = Language.English };
```

Aspose supporta molte lingue; aggiungi il pacchetto NuGet appropriato se necessario.

### What about error handling?

Avvolgi il callback in un blocco try/catch e registra i fallimenti. Il processore continuerà con il file successivo, evitando che un’immagine corrotta interrompa l’intera esecuzione.

```csharp
(imagePath, ocrText) =>
{
    try
    {
        string txtPath = Path.ChangeExtension(imagePath, ".txt");
        File.WriteAllText(txtPath, ocrText);
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Failed on {imagePath}: {ex.Message}");
    }
}
```

## Pro Tips for Scaling Up

- **Chunk the folder**: Se hai decine di migliaia di file, dividili in sottocartelle e avvia più job batch in sequenza.  
- **Use a cloud VM**: Una macchina con più core (es. 32‑core) terminerà molto più velocemente. Ricorda solo di adeguare i limiti della licenza.  
- **Post‑process the text**: Dopo l’estrazione, potresti voler eseguire regex per estrarre numeri di fattura o date. I file `.txt` sono l’input perfetto per queste pipeline.

## Conclusion

Ora disponi di una ricetta solida, pronta per la produzione, su **come eseguire OCR batch** su una directory di PNG, **estrarre testo da file PNG** e **convertire immagini in testo** usando Aspose.OCR in C#. L’esempio è autonomo, spiega il “perché” di ogni riga e include consigli per gestire carichi di lavoro più grandi o tipi di file diversi.

Pronto per il passo successivo? Prova a modificare il callback per inserire i risultati in un database, o aggiungi una pre‑elaborazione dell’immagine (es. deskew) prima dell’OCR. Il pattern scala bene, così potrai adattarlo a qualsiasi scenario di elaborazione batch.

Buona programmazione, e che le tue pipeline OCR siano veloci e prive di errori!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}