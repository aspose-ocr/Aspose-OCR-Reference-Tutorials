---
category: general
date: 2026-03-21
description: Come eseguire OCR batch in C# in modo semplice—impara a estrarre testo
  dalle immagini, convertire le immagini in testo e salvare l'OCR come testo con le
  impostazioni della lingua.
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert images to text
- save OCR as text
- set OCR language
language: it
og_description: Come eseguire OCR batch in C# ti permette di estrarre testo dalle
  immagini, convertire le immagini in testo e salvare l'OCR come testo impostando
  facilmente la lingua dell'OCR.
og_title: Come eseguire OCR in batch con C# – Guida rapida
tags:
- OCR
- C#
- Aspose
title: Come eseguire OCR batch in C# – Estrarre testo dalle immagini rapidamente
url: /it/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-images-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR in batch con C# – Estrarre testo dalle immagini rapidamente

Ti sei mai chiesto **come fare OCR in batch** quando hai centinaia di foto in una cartella? Non sei l'unico: gli sviluppatori chiedono continuamente come estrarre testo dalle immagini senza scrivere un ciclo per ogni file. La buona notizia è che Aspose.OCR ti offre un modo pulito e pronto per il parallelismo per **convertire le immagini in testo** in poche righe di C#.

In questo tutorial vedremo un esempio completo, pronto all'uso, che mostra come **salvare l'OCR come testo**, scegliere la lingua corretta e aumentare la velocità con l'elaborazione parallela. Alla fine avrai una soluzione autonoma da inserire in qualsiasi progetto .NET.

## Cosa ti serve

- .NET 6 o versioni successive (l'API funziona con .NET Core e .NET Framework)
- Aspose.OCR per .NET (pacchetto NuGet `Aspose.OCR`)
- Una cartella di immagini da elaborare (PNG, JPEG, TIFF, ecc.)
- Un po' di curiosità sulla programmazione parallela (opzionale, ma utile)

Nessun servizio aggiuntivo, nessuna chiave cloud—solo puro codice C# che gira in locale.

---

![how to batch OCR workflow](placeholder.png){alt="diagramma del flusso di lavoro per batch OCR"}

## Passo 1: Configura il progetto e installa Aspose.OCR

Per prima cosa, crea un'app console (o riutilizza una esistente) e aggiungi il pacchetto Aspose.OCR:

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

> **Pro tip:** Se usi Visual Studio, fai clic destro sul progetto → *Manage NuGet Packages* → cerca *Aspose.OCR* e installa l'ultima versione stabile.

Questo ti dà accesso a `OcrBatchProcessor`, `OcrEngineSettings` e all'enumerazione `Language`.

## Passo 2: Definisci le cartelle di input e output

Il processore batch deve sapere dove si trovano le immagini sorgente e dove scrivere i file di testo estratti. Usa percorsi assoluti o relativi alla radice del progetto—assicurati solo che le cartelle esistano prima di eseguire il codice.

```csharp
var inputPath  = @"C:\MyImages\BatchInput";
var outputPath = @"C:\MyImages\BatchResults";

// Ensure the output directory exists
if (!Directory.Exists(outputPath))
    Directory.CreateDirectory(outputPath);
```

> **Perché è importante:** Se la cartella di output manca, il processore lancerà un'eccezione, interrompendo l'intero batch. Crearla in anticipo garantisce un'esecuzione fluida.

## Passo 3: Configura le impostazioni OCR (inclusa la lingua)

Qui è dove **imposti la lingua OCR** per l'intero batch. Aspose.OCR supporta decine di lingue; l'inglese è il valore predefinito, ma puoi passare al francese, spagnolo, ecc., modificando il valore dell'enumerazione `Language`.

```csharp
var ocrSettings = new OcrEngineSettings
{
    Language = Language.English   // Change to Language.French, Language.Spanish, etc.
};
```

Se in futuro dovrai elaborare lingue diverse per immagine, potrai sovrascrivere questa impostazione per file specifici—ne parleremo più avanti.

## Passo 4: Crea l'oggetto `OcrBatchProcessor`

Ora uniamo tutto. `OcrBatchProcessor` ti permette di specificare la cartella di input, la cartella di output, il formato di output, le opzioni di parallelismo e le impostazioni condivise appena create.

```csharp
using Aspose.OCR.Batch;
using Aspose.OCR.Settings;
using System.Threading.Tasks;

var batch = new OcrBatchProcessor
{
    InputFolder   = inputPath,
    OutputFolder  = outputPath,
    OutputFormat  = OcrOutputFormat.PlainText, // **save OCR as text** in .txt files
    ParallelOptions = new ParallelOptions { MaxDegreeOfParallelism = 4 }, // up to 4 threads
    Settings = ocrSettings
};
```

> **Perché il parallelismo?** Quando hai decine o centinaia di immagini, elaborarli uno alla volta può essere estremamente lento. Impostare `MaxDegreeOfParallelism` a 4 consente al runtime di usare quattro core CPU contemporaneamente, riducendo drasticamente il tempo totale su una workstation tipica.

## Passo 5: Esegui l'operazione batch

Con il processore configurato, l'esecuzione è una singola chiamata di metodo. La libreria gestisce l'enumerazione dei file, l'OCR e la scrittura dei risultati automaticamente.

```csharp
batch.Execute();
Console.WriteLine("Batch OCR completed.");
```

Quando la console stampa *“Batch OCR completed.”* troverai un file `.txt` accanto a ciascuna immagine originale nella cartella `BatchResults`. Ogni file di testo contiene i caratteri grezzi estratti dall'immagine di origine—esattamente ciò che ti serve per **estrarre testo dalle immagini** per ulteriori elaborazioni.

### Output previsto

```
C:\MyImages\BatchResults\image1.txt
C:\MyImages\BatchResults\image2.txt
...
```

Apri uno di questi file e vedrai la rappresentazione in testo semplice del contenuto dell'immagine.

## Passo 6: Verifica i risultati (opzionale)

È buona pratica controllare qualche file per assicurarsi che l'OCR abbia funzionato correttamente. Un modo rapido è leggere la prima riga di ogni file generato e stamparla sulla console:

```csharp
foreach (var txtFile in Directory.GetFiles(outputPath, "*.txt"))
{
    var firstLine = File.ReadLines(txtFile).FirstOrDefault();
    Console.WriteLine($"{Path.GetFileName(txtFile)} → {firstLine}");
}
```

Se noti caratteri illeggibili, considera di cambiare l'impostazione `Language` o di migliorare la qualità dell'immagine (ad esempio, aumentare i DPI, convertire in scala di grigi).

## Varianti avanzate e casi limite

### 1. Sovrascritture della lingua per file
A volte un batch contiene documenti multilingue. Puoi ispezionare il nome di ciascuna immagine e assegnare una lingua al volo:

```csharp
batch.Settings = new OcrEngineSettings(); // default settings

batch.FileProcessing += (sender, args) =>
{
    if (args.FileName.Contains("_fr"))
        args.Settings.Language = Language.French;
    else if (args.FileName.Contains("_es"))
        args.Settings.Language = Language.Spanish;
    // otherwise keep the default (English)
};
```

### 2. Formati di output diversi
Se ti servono PDF ricercabili invece di testo semplice, cambia `OutputFormat`:

```csharp
batch.OutputFormat = OcrOutputFormat.SearchablePdf;
```

In questo modo **converti le immagini in testo** all'interno di un contenitore PDF, preservando il layout originale.

### 3. Gestione di immagini di grandi dimensioni
Immagini ad altissima risoluzione possono consumare molta memoria. Per mantenere il processo leggero, abilita il down‑sampling dell'immagine:

```csharp
batch.Settings.Dpi = 300; // lowers internal processing DPI
```

### 4. Registrazione degli errori
Il processore lancia eccezioni per file illeggibili. Avvolgi `Execute` in un try/catch e registra i nomi dei file problematici:

```csharp
try
{
    batch.Execute();
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed on {ex.Data["FileName"]}: {ex.Message}");
}
```

## Esempio completo funzionante

Mettendo tutto insieme, ecco il programma completo, pronto per il copia‑incolla:

```csharp
using Aspose.OCR.Batch;
using Aspose.OCR.Settings;
using System;
using System.IO;
using System.Linq;
using System.Threading.Tasks;

class Program
{
    static void Main()
    {
        // 1️⃣ Input & output locations
        var inputFolder  = @"C:\MyImages\BatchInput";
        var outputFolder = @"C:\MyImages\BatchResults";

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ OCR settings – set OCR language
        var ocrSettings = new OcrEngineSettings
        {
            Language = Language.English // change as needed
        };

        // 3️⃣ Configure the batch processor
        var batch = new OcrBatchProcessor
        {
            InputFolder    = inputFolder,
            OutputFolder   = outputFolder,
            OutputFormat   = OcrOutputFormat.PlainText, // **save OCR as text**
            ParallelOptions = new ParallelOptions { MaxDegreeOfParallelism = 4 },
            Settings       = ocrSettings
        };

        // 4️⃣ Run the batch job
        batch.Execute();

        // 5️⃣ Confirmation message
        Console.WriteLine("Batch OCR completed.");

        // 6️⃣ (Optional) Quick verification of a few results
        foreach (var txtFile in Directory.GetFiles(outputFolder, "*.txt").Take(5))
        {
            var firstLine = File.ReadLines(txtFile).FirstOrDefault();
            Console.WriteLine($"{Path.GetFileName(txtFile)} → {firstLine}");
        }
    }
}
```

Salva questo file come `Program.cs`, compila il progetto e avvia `dotnet run`. Vedrai l'output della console che conferma il completamento, seguito da un breve anteprima del testo estratto.

---

## Conclusione

Abbiamo appena visto **come fare OCR in batch** in C# usando Aspose.OCR, mostrando come **estrarre testo dalle immagini**, **convertire le immagini in testo** e **salvare l'OCR come testo** impostando la **lingua OCR** adeguata al contenuto. L'esempio è pienamente funzionante, include il parallelismo per la velocità e offre punti di estensione per scenari avanzati come sovrascritture della lingua per file o output PDF.

Pronto per il passo successivo? Prova a sostituire `OcrOutputFormat.PlainText` con `SearchablePdf` e scopri quanto è semplice generare PDF ricercabili. Oppure sperimenta con valori diversi di `MaxDegreeOfParallelism` per spremere ogni millisecondo su una macchina multicore.

Se incontri problemi, ricontrolla i percorsi delle cartelle, assicurati che le immagini siano leggibili e verifica che l'enumerazione della lingua corrisponda al testo presente nelle tue foto. Buona programmazione, e che i tuoi batch OCR siano rapidi e precisi!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}