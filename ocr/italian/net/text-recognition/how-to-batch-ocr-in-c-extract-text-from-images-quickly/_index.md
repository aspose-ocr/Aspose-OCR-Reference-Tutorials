---
category: general
date: 2026-02-19
description: Scopri come eseguire l'OCR in batch con Aspose.OCR in C#. Questa guida
  ti mostra come estrarre il testo dalle immagini e convertire le immagini in txt
  in modo efficiente.
draft: false
keywords:
- how to batch ocr
- extract text from images
- convert images to txt
- Aspose OCR batch processing
- C# image to text conversion
language: it
og_description: Come eseguire OCR batch con Aspose.OCR in C#. Estrai il testo dalle
  immagini e converti le immagini in txt in pochi semplici passaggi.
og_title: Come eseguire OCR batch in C# – Conversione rapida da immagine a testo
tags:
- OCR
- C#
- Aspose
title: Come eseguire OCR in batch con C# – Estrarre rapidamente testo dalle immagini
url: /it/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-images-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR batch in C# – Guida completa passo‑passo

Ti sei mai chiesto **come eseguire OCR batch** su un’intera cartella di immagini senza scrivere un programma separato per ogni file? Non sei il solo. Molti sviluppatori si trovano in difficoltà quando devono estrarre testo da decine—o addirittura migliaia—di pagine scansionate, ricevute o screenshot. La buona notizia? Con Aspose.OCR puoi automatizzare l’intero flusso, **estrarre testo dalle immagini** e **convertire immagini in txt** con poche righe di codice.

In questo tutorial vedremo un esempio completo, pronto‑da‑eseguire, che mostra esattamente come configurare un processore OCR batch, regolare il preprocessing, gestire il parallelismo e scrivere ogni risultato in un file `.txt`. Alla fine avrai un’app console autonoma che potrai inserire in qualsiasi progetto .NET.

## Cosa ti serve

- .NET 6.0 o successivo (il codice funziona anche su .NET Core e .NET Framework)  
- Pacchetto NuGet Aspose.OCR per .NET (`Aspose.OCR`)  
- Una cartella piena di file immagine (`.png`, `.jpg`, ecc.) da elaborare  
- Una quantità modesta di RAM; la demo utilizza 4 thread paralleli ma puoi regolarli

Nessun servizio esterno, nessun file di configurazione nascosto—solo puro codice C# che puoi compilare ed eseguire subito.

![Diagram illustrating how to batch ocr processing flow](/images/how-to-batch-ocr-flow.png "how to batch ocr flow diagram")

## Passo 1: Installa Aspose.OCR e configura il progetto

Per prima cosa, aggiungi il pacchetto Aspose.OCR al tuo progetto:

```bash
dotnet add package Aspose.OCR
```

Perché è importante: Aspose.OCR include il motore OCR, i dati linguistici e le utility di preprocessing, quindi non avrai bisogno di binari di terze parti. Una volta installato il pacchetto, crea una nuova app console (o aggiungi il codice a una esistente) e importa gli spazi dei nomi necessari:

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
```

Queste istruzioni `using` ti danno accesso alle classi del processore batch e a utili helper I/O.

## Passo 2: Configura il processore OCR batch

Ora istanzieremo `OcrBatchProcessor` e gli diremo quale lingua cercare, come pulire le immagini e quanti thread eseguire in parallelo. Questo è il cuore di **come eseguire OCR batch** in modo efficiente.

```csharp
// Step 2: Create and configure the OCR batch processor
var ocrBatch = new OcrBatchProcessor
{
    // Language selection – English is the most common, but you can change it
    Language = Language.English,

    // Preprocessing improves accuracy; Deskew removes rotation
    Preprocessing = new PreprocessingOptions
    {
        Deskew = DeskewAdvanced.Enable()
    },

    // Parallelism – adjust based on your CPU/GPU capabilities
    MaxDegreeOfParallelism = 4
};
```

**Perché abilitare Deskew?** Molti documenti scansionati non sono perfettamente allineati; l’algoritmo di deskew li ruota nuovamente su una linea di base dritta, migliorando spesso i tassi di riconoscimento del 10‑15 %.

## Passo 3: Collega un callback per salvare i file di testo

Il processore batch solleva un evento per ogni immagine completata. Ci iscriveremo a `ResultProcessed` così da scrivere ogni risultato OCR in un file `.txt`—convertendo **immagini in txt** al volo.

```csharp
// Step 3: Register a callback to save each OCR result as a text file
ocrBatch.ResultProcessed += (sender, args) =>
{
    // Change the original file extension to .txt
    string txtPath = Path.ChangeExtension(args.ImagePath, ".txt");

    // Write the recognized text to the new file
    File.WriteAllText(txtPath, args.Result.Text);

    // Inform the console for debugging / progress monitoring
    Console.WriteLine($"Processed: {args.ImagePath}");
};
```

Un suggerimento rapido: se devi preservare la struttura originale delle cartelle, puoi modificare `txtPath` includendo sottocartelle o una directory di output separata.

## Passo 4: Esegui il batch sulla tua cartella di immagini

L’unica cosa che resta da fare è puntare il processore alla cartella che contiene le foto da **estrarre testo dalle immagini**. Il metodo `ProcessFolder` scansiona ricorsivamente le sottocartelle, così puoi inserire un intero albero di scansioni e lasciare che la libreria gestisca il resto.

```csharp
// Step 4: Run the batch on all image files in the target folder
ocrBatch.ProcessFolder(@"C:\Path\To\Your\Images");
```

Quando avvii il programma, vedrai un output console simile a:

```
Processed: C:\Path\To\Your\Images\invoice1.png
Processed: C:\Path\To\Your\Images\receipt_2024.jpg
...
```

Ogni immagine avrà ora un file `.txt` gemello contenente il testo estratto.

## Esempio completo funzionante

Mettendo tutto insieme, ecco il programma completo che puoi copiare‑incollare in `Program.cs`:

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create and configure the OCR batch processor
        var ocrBatch = new OcrBatchProcessor
        {
            Language = Language.English,
            Preprocessing = new PreprocessingOptions
            {
                Deskew = DeskewAdvanced.Enable()
            },
            // Step 2: Define the level of parallelism (adjust for your CPU/GPU)
            MaxDegreeOfParallelism = 4
        };

        // Step 3: Register a callback to save each OCR result as a text file
        ocrBatch.ResultProcessed += (sender, args) =>
        {
            string txtPath = Path.ChangeExtension(args.ImagePath, ".txt");
            File.WriteAllText(txtPath, args.Result.Text);
            Console.WriteLine($"Processed: {args.ImagePath}");
        };

        // Step 4: Run the batch on all image files in the target folder
        ocrBatch.ProcessFolder(@"C:\Path\To\Your\Images");
    }
}
```

### Output previsto

- Per ogni `*.png` o `*.jpg` nella directory di origine, appare un file `*.txt` corrispondente accanto.
- La console stampa una riga per file, fornendoti un feedback in tempo reale.
- Se un’immagine non può essere letta (file corrotto, formato non supportato), Aspose.OCR registra un errore ma continua a elaborare il resto—grazie alla robustezza integrata del motore batch.

## Domande frequenti e casi particolari

### E se devo elaborare PDF invece di immagini?

Aspose.OCR può accettare pagine PDF come immagini internamente, ma dovrai prima convertire il PDF in immagini raster (ad es., usando Aspose.PDF). Una volta ottenuti i PNG, lo stesso codice batch funziona senza modifiche.

### Posso cambiare lingua al volo?

Sì. La proprietà `Language` accetta qualsiasi valore dell’enum `Language` (Spanish, French, Chinese, ecc.). Se hai documenti multilingue, considera di eseguire due passaggi—uno per lingua—oppure usa `Language.AutoDetect`.

### Come limitare il batch a tipi di file specifici?

`ProcessFolder` accetta un `SearchOption` opzionale e un array `string[] extensions`. Esempio:

```csharp
ocrBatch.ProcessFolder(@"C:\Images", new[] { ".png", ".tif" });
```

### E l’accelerazione GPU?

Aspose.OCR supporta la GPU tramite la configurazione di `OcrEngine`, ma il parametro `MaxDegreeOfParallelism` del processore batch rimane il principale controllo del parallelismo. Se disponi di una GPU compatibile, abilitala nelle impostazioni del motore prima di creare `OcrBatchProcessor`.

### Come gestire cartelle molto grandi (decine di migliaia di file)?

- Aumenta `MaxDegreeOfParallelism` con cautela; troppi thread possono esaurire la memoria.  
- Usa una cartella di output dedicata per evitare confusione.  
- Svuota periodicamente i log su disco per prevenire l’accumulo di memoria.

## Pro Tips per OCR di alta qualità

- **DPI è importante**: immagini a 300 DPI o più garantiscono la massima precisione. Se le tue scansioni sono a risoluzione inferiore, considera di ingrandirle con un filtro bicubico prima dell’elaborazione.  
- **Riduzione del rumore**: attiva `Preprocessing.NoiseRemoval` se le immagini di origine sono granulose.  
- **Naming dei file**: mantieni i nomi brevi e alfanumerici; i caratteri speciali possono confondere la logica del percorso nel callback.  
- **Logging**: sostituisci `Console.WriteLine` con un logger adeguato (ad es., `Serilog`) per carichi di lavoro di produzione.

## Prossimi passi

Ora che hai padroneggiato **come eseguire OCR batch**, potresti voler:

- **Estrarre testo dalle immagini** e inviare l’output a un indice di ricerca (ad es., Elasticsearch) per ricerche full‑text.  
- **Convertire immagini in txt** e poi eseguire elaborazione del linguaggio naturale (NLP) per classificare automaticamente i documenti.  
- Sperimentare con **pacchetti linguistici diversi** o dizionari personalizzati per terminologia specifica di settore.

Se sei curioso del post‑processing, dai un’occhiata ai tutorial “Parsing OCR output with regular expressions” o “Storing OCR results in a SQL database”.

---

**Buon coding!** Sentiti libero di regolare il parallelismo, aggiungere altri passaggi di preprocessing o racchiudere il tutto in un servizio Windows per monitoraggio continuo. Il cielo è il limite quando combini le capacità batch di Aspose.OCR con un po’ di ingegnosità .NET.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}