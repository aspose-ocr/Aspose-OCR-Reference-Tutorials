---
category: general
date: 2026-02-22
description: Come eseguire OCR batch di immagini JPEG in C# con Aspose.OCR. Impara
  a estrarre testo da JPG, convertire JPG in TXT e processare le immagini in batch
  in modo efficiente.
draft: false
keywords:
- how to batch ocr
- extract text from jpg
- convert jpg to txt
- batch process images
- c# ocr example
language: it
og_description: Come eseguire l'OCR batch di immagini JPEG in C# usando Aspose.OCR.
  Questo tutorial ti mostra come estrarre il testo da JPG, convertire JPG in TXT e
  processare le immagini in batch in pochi minuti.
og_title: Come eseguire OCR in batch di immagini JPEG in C# – Guida completa
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Come eseguire OCR batch di immagini JPEG in C# – Guida completa
url: /it/net/text-recognition/how-to-batch-ocr-jpeg-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR batch di immagini JPEG in C# – Guida completa

Ti sei mai chiesto **come eseguire OCR batch** su una cartella piena di immagini senza dover scrivere un programma separato per ogni file? In questa guida ti mostreremo esattamente **come eseguire OCR batch** sui file JPEG usando Aspose.OCR, così potrai **estrarre testo da jpg** e **convertire jpg in txt** con poche righe di codice.  

Se ti sei mai trovato davanti a una cartella di fatture scannerizzate e hai pensato “Deve esserci un modo più veloce”, sei nel posto giusto. Ti guideremo passo passo, spiegheremo perché ogni elemento è importante e inseriremo anche qualche consiglio professionale per gestire batch di grandi dimensioni.

## Cosa Costruirai

* Scansiona una directory specificata alla ricerca di file `*.jpg`.  
* Invia ogni immagine attraverso il motore OCR di Aspose (accelerato GPU se disponi di una scheda adeguata).  
* Scrive il testo riconosciuto in un file `.txt` posizionato accanto all'immagine originale.  

Nessun servizio esterno, nessun copia‑incolla manuale—solo puro C# e una libreria OCR affidabile.

### Prerequisiti

* .NET 6.0 o successivo (il codice funziona anche su .NET Framework 4.8).  
* Visual Studio 2022 o qualsiasi editor che supporti C#.  
* Un pacchetto NuGet Aspose.OCR (la versione di prova gratuita funziona per i test).  

Se ti manca qualcuno di questi, fermati ora e installalo; il resto della guida presume che siano già presenti.

![Esempio di OCR batch](/images/how-to-batch-ocr.png "diagramma OCR batch")

## Passo 1: Installa il pacchetto NuGet Aspose.OCR

Prima di tutto—il tuo progetto ha bisogno della libreria OCR. Apri un terminale nella cartella della soluzione ed esegui:

```bash
dotnet add package Aspose.OCR
```

Oppure usa l’interfaccia UI del NuGet Package Manager in Visual Studio. Questo scarica tutto il necessario, incluse le librerie abilitate per GPU se la tua macchina le supporta.

> **Consiglio professionale:** Se prevedi di eseguire questo su un server senza GPU, imposta `UseGpu = false` più tardi; il motore tornerà automaticamente alla CPU.

## Passo 2: Configura il motore OCR

Creare e configurare l'`OcrEngine` è dove inizia la magia. Indicherai al motore quale lingua aspettarsi, se usare la GPU e in quale formato deve essere l'output.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// ...

// Step 2: Initialize and configure the OCR engine
var ocrEngine = new OcrEngine
{
    // English works for most documents; change if you need another language.
    Language = Language.English,

    // Enable GPU for faster processing on supported hardware.
    UseGpu = true,

    // We only need plain text for our .txt files.
    OutputFormat = OutputFormat.Text
};
```

**Perché è importante:** Impostare `Language` migliora l'accuratezza perché il motore può restringere i set di caratteri. Abilitare `UseGpu` può dimezzare i tempi di elaborazione su una scheda grafica moderna, il che è un vero vantaggio quando si esegue **elaborazione batch di immagini**.

## Passo 3: Riconosci tutti i file JPEG in una cartella

Ora lasciamo che Aspose faccia il lavoro pesante. Il metodo statico `BatchProcessor.RecognizeFolder` attraversa la directory, esegue l'OCR su ogni file corrispondente e restituisce una collezione di risultati.

```csharp
using System.Collections.Generic;

// ...

// Step 3: Run OCR on every *.jpg in the target directory
IList<OcrResult> ocrResults = BatchProcessor.RecognizeFolder(
    ocrEngine,
    @"C:\Images\Invoices",   // <-- replace with your folder path
    searchPattern: "*.jpg"); // Only JPEG files are processed
```

**Gestione dei casi limite:** Se la cartella contiene sottocartelle, puoi aggiungere un overload `SearchOption.AllDirectories` (o ricorsione manuale) per assicurarti di non perdere alcun file.

## Passo 4: Scrivi ogni risultato in un file `.txt` corrispondente

Gli oggetti `OcrResult` contengono il percorso del file originale e il testo riconosciuto. Scorri l'elenco, cambia l'estensione e scrivi l'output.

```csharp
using System.IO;

// ...

// Step 4: Persist OCR results as .txt files next to the source images
foreach (var result in ocrResults)
{
    // Change "image.jpg" → "image.txt"
    string txtFilePath = Path.ChangeExtension(result.SourceFilePath, ".txt");

    // Save the extracted text
    File.WriteAllText(txtFilePath, result.Text);
}
```

È tutto—ogni JPEG ora ha un file di testo associato che puoi inviare a processi successivi, indici di ricerca o semplicemente archiviare.

## Passo 5: Esegui l'applicazione e verifica l'output

Compila ed esegui il programma:

```bash
dotnet run
```

Supponendo che la cartella contenga `invoice1.jpg` e `receipt2.jpg`, dovresti vedere comparire `invoice1.txt` e `receipt2.txt` accanto a loro. Apri uno dei file `.txt`; troverai l'output OCR grezzo, ad esempio:

```
Invoice #12345
Date: 02/15/2026
Total: $1,234.56
Thank you for your business!
```

Se il testo appare illeggibile, verifica che le immagini di origine siano ad alto contrasto e che la proprietà `Language` corrisponda alla lingua del documento.

## Passo 6: Ottimizzazioni Avanzate (Opzionale)

### a) Gestione di scansioni a bassa qualità

A volte i JPEG sono rumorosi. Puoi pre‑elaborare le immagini con Aspose.Imaging o qualsiasi altra libreria:

```csharp
using Aspose.Imaging;
using Aspose.Imaging.ImageOptions;

// Example: increase contrast before OCR
using (var image = Image.Load(result.SourceFilePath))
{
    image.Contrast = 30; // boost contrast
    image.Save(result.SourceFilePath); // overwrite or save to temp file
}
```

### b) Parallelizzare il batch

Se hai molti file e una CPU multi‑core, avvolgi il ciclo in `Parallel.ForEach`:

```csharp
Parallel.ForEach(ocrResults, result =>
{
    string txtFilePath = Path.ChangeExtension(result.SourceFilePath, ".txt");
    File.WriteAllText(txtFilePath, result.Text);
});
```

Tieni presente che il motore OCR di Aspose non è thread‑safe; avresti bisogno di un'istanza `OcrEngine` separata per thread o di utilizzare una coda concorrente.

### c) Logging e gestione degli errori

Una soluzione robusta registra i fallimenti in modo da poterli riprovare in seguito:

```csharp
try
{
    // OCR and write logic here
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed on {result.SourceFilePath}: {ex.Message}");
    // Optionally write to a log file
}
```

## Esempio Completo Funzionante

Mettendo tutto insieme, ecco il programma completo che puoi copiare‑incollare in una nuova Console App:

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;
using System.Collections.Generic;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create and configure the OCR engine
        var ocrEngine = new OcrEngine
        {
            Language = Language.English,
            UseGpu = true,
            OutputFormat = OutputFormat.Text
        };

        // 2️⃣ Recognize all JPEG images in the target folder
        IList<OcrResult> ocrResults = BatchProcessor.RecognizeFolder(
            ocrEngine,
            @"C:\Images\Invoices",   // <-- change to your directory
            searchPattern: "*.jpg");

        // 3️⃣ Write each OCR result to a matching .txt file
        foreach (var result in ocrResults)
        {
            string txtFilePath = Path.ChangeExtension(result.SourceFilePath, ".txt");
            File.WriteAllText(txtFilePath, result.Text);
        }

        Console.WriteLine("Batch OCR complete. Check the folder for .txt files.");
    }
}
```

Eseguilo, osserva l'output della console, e poi apri alcuni file `.txt` per confermare che il passaggio **estrarre testo da jpg** sia riuscito.  

---

## Conclusione

Abbiamo appena illustrato **come eseguire OCR batch** su una collezione di immagini JPEG in C# usando Aspose.OCR, trasformando ogni immagine in un file `.txt` ricercabile. La soluzione è compatta, consapevole della GPU e facile da estendere per la gestione degli errori, la pre‑elaborazione delle immagini o l'esecuzione parallela.  

Se sei pronto a proseguire, considera i seguenti passi successivi:

* **Elabora in batch immagini** di altri formati (`*.png`, `*.tif`) modificando il `searchPattern`.  
* Combina l'output con un motore di ricerca full‑text come Lucene.NET per una ricerca istantanea dei documenti.  
* Esplora le funzionalità di conversione PDF di Aspose per generare PDF ricercabili direttamente dai risultati OCR.  

Sentiti libero di sperimentare—cambia la lingua, disattiva la GPU o invia il testo a un database. Il modello di base rimane lo stesso, e ora hai una solida base su cui costruire.

Buon coding, e che le tue pipeline OCR siano sempre veloci e accurate!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}