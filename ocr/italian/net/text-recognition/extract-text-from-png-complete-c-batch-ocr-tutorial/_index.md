---
category: general
date: 2026-04-26
description: Estrai rapidamente testo da file PNG con C#. Scopri come convertire le
  immagini in testo, leggere i file PNG, iterare le immagini ed eseguire OCR batch
  in pochi minuti.
draft: false
keywords:
- extract text from png
- convert images to text
- read png files
- loop through images
- batch ocr images
language: it
og_description: Estrai testo da file PNG rapidamente con C#. Questa guida mostra come
  convertire le immagini in testo, leggere i file PNG, scorrere le immagini ed eseguire
  OCR di immagini in batch.
og_title: Estrai testo da PNG – Tutorial completo di OCR batch in C#
tags:
- C#
- OCR
- Aspose
title: Estrai testo da PNG – Tutorial completo OCR batch in C#
url: /it/net/text-recognition/extract-text-from-png-complete-c-batch-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai Testo da PNG – Tutorial Completo OCR Batch in C#

Hai mai dovuto **estrarre testo da file PNG** ma non sapevi da dove cominciare? Non sei solo: molti sviluppatori si trovano di fronte a questo ostacolo al loro primo tentativo di OCR su una cartella di screenshot. La buona notizia è che, con poche righe di C# e Aspose OCR, puoi convertire le immagini in testo, leggere i file PNG, scorrere le immagini e processare tutto in batch in un unico passaggio.  

In questo tutorial ti guideremo passo passo attraverso un’app console pronta all’uso che fa esattamente questo. Alla fine avrai una soluzione autonoma che estrae il testo da ogni PNG in una directory e crea un file `.txt` corrispondente accanto a ciascuna immagine. Nessuno script aggiuntivo, nessun copia‑incolla manuale—solo puro codice.

## Di cosa avrai bisogno

- **.NET 6 SDK** (o qualsiasi versione più recente di .NET). È gratuito, veloce e funziona ovunque.
- **Aspose.OCR for .NET** (il pacchetto NuGet). La libreria include l’accelerazione GPU se disponi di una GPU compatibile, ma torna automaticamente alla CPU se necessario.
- Una cartella con una manciata di **immagini PNG** che desideri processare.  
- Un editor di testo o IDE—Visual Studio, VS Code, Rider—quello che preferisci.

Tutto qui. Se hai già tutto, sei pronto a partire.

![extract text from png example](image.png "extract text from png demo screenshot")

*Testo alternativo dell'immagine: “estrarre testo da png usando OCR batch C#”*

## Passo 1 – Configura il Progetto e Installa Aspose.OCR

Prima, crea un nuovo progetto console e aggiungi il pacchetto Aspose OCR.

```bash
dotnet new console -n PngOcrBatch
cd PngOcrBatch
dotnet add package Aspose.OCR
```

Perché usiamo un’app console? È l’host più semplice per i job batch, e puoi eseguirla da riga di comando o programmarla con un task runner. Se in seguito avrai bisogno di un’interfaccia UI, potrai spostare la logica principale in una libreria di classi.

## Passo 2 – Inizializza un Motore OCR Accelerato GPU (o fallback CPU)

Aspose offre un `GpuOcrEngine` che rileva automaticamente una GPU supportata. Se non ne trova alcuna, ritorna al motore CPU standard—senza codice aggiuntivo.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Create the OCR engine – GPU if available, otherwise CPU
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;   // Latin covers most Western alphabets

        // The rest of the code lives in a separate method for clarity
        ProcessFolder(ocrEngine, @"C:\MyPngFolder");
    }

    // …
}
```

**Consiglio professionale:** Se sei su un server headless senza GPU, puoi sostituire `GpuOcrEngine` con `OcrEngine` e il codice si comporterà esattamente allo stesso modo.

## Passo 3 – Scorri le Immagini nella Directory di Destinazione

Dobbiamo **scorrere le immagini** e selezionare solo i file PNG. Il metodo `Directory.GetFiles` fa il lavoro pesante, e noi gestiremo il caso di una cartella vuota.

```csharp
static void ProcessFolder(OcrEngine engine, string folderPath)
{
    if (!Directory.Exists(folderPath))
    {
        Console.WriteLine($"❌ Folder not found: {folderPath}");
        return;
    }

    // Grab every *.png file – this is the “read png files” part
    string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

    if (pngFiles.Length == 0)
    {
        Console.WriteLine("⚠️ No PNG files found. Make sure the folder contains .png images.");
        return;
    }

    foreach (var pngPath in pngFiles)
    {
        Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
        ExtractAndSave(engine, pngPath);
    }
}
```

Nota l’uso di `SearchOption.TopDirectoryOnly`. Se in seguito avrai bisogno di ricorsione nelle sottocartelle, basta passare a `AllDirectories`. Questa piccola modifica ti permette di **convertire le immagini in testo** in un intero albero con una sola riga.

## Passo 4 – Esegui OCR e Salva il Risultato

Ora arriva il cuore del workflow **batch OCR images**. Carichiamo ogni PNG, eseguiamo `Recognize()` e scriviamo la stringa estratta in un file `.txt` che condivide lo stesso nome base.

```csharp
static void ExtractAndSave(OcrEngine engine, string imagePath)
{
    try
    {
        // Load the PNG into the engine
        engine.Image = ImageStream.FromFile(imagePath);

        // Run recognition – this returns a RecognitionResult object
        RecognitionResult result = engine.Recognize();

        // Build the output path (same name, .txt extension)
        string txtPath = Path.ChangeExtension(imagePath, ".txt");

        // Write the OCR text to disk
        File.WriteAllText(txtPath, result.Text);

        Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
    }
    catch (Exception ex)
    {
        // Edge case: corrupted PNG or unsupported format
        Console.WriteLine($"❗ Error processing {Path.GetFileName(imagePath)}: {ex.Message}");
    }
}
```

**Perché avvolgerlo in try/catch?** I batch di immagini reali spesso contengono file corrotti o PNG con profili colore non comuni. Catturare l’eccezione impedisce il crash dell’intera esecuzione e ti permette di continuare con i file rimanenti.

## Passo 5 – Esegui l’Applicazione e Verifica l’Uscita

Compila e avvia l’app:

```bash
dotnet run
```

Dovresti vedere un log della console simile a:

```
🔎 Processing: invoice1.png
✅ Saved: invoice1.txt
🔎 Processing: screenshot_2024.png
✅ Saved: screenshot_2024.txt
...
```

Apri uno dei file `.txt` generati—ecco il testo estratto. Se un file è vuoto, ricontrolla la qualità dell’immagine; l’OCR funziona al meglio con testo chiaro e ad alto contrasto.

### Script di Verifica Rapida (opzionale)

Se vuoi assicurarti che ogni PNG abbia un file di testo corrispondente, esegui questa piccola riga PowerShell:

```powershell
Get-ChildItem -Path "C:\MyPngFolder" -Filter *.png |
  ForEach-Object { 
    $txt = $_.BaseName + ".txt"
    if (-Not (Test-Path $txt)) { Write-Host "Missing: $txt" }
  }
```

## Variazioni Comuni & Casi Limite

| Situazione | Cosa Cambiare |
|------------|---------------|
| **Lingue non latine** (es. cirillico) | Imposta `ocrEngine.Language = Language.Cyrillic;` |
| **Set di immagini molto grande (>10 000 file)** | Usa `Parallel.ForEach` per velocizzare l’elaborazione, ma controlla l’utilizzo della memoria GPU. |
| **Mantenere l’ordine originale delle immagini** | Ordina `pngFiles` prima del `foreach` (`Array.Sort(pngFiles);`). |
| **Esecuzione su server CI senza GPU** | Sostituisci `GpuOcrEngine` con `OcrEngine` per evitare errori di inizializzazione GPU. |
| **Processare solo file che contengono una parola chiave specifica** | Dopo aver ottenuto `result.Text`, verifica `result.Text.Contains("Invoice")` prima di scrivere il file. |

Queste modifiche ti consentono di adattare la pipeline **convert images to text** a quasi ogni scenario possibile.

## Codice Sorgente Completo (Pronto per Copia‑Incolla)

```csharp
// ------------------------------------------------------------
// Extract Text from PNG – Batch OCR using Aspose.OCR (C#)
// ------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine (GPU if possible)
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;

        // 2️⃣ Define the folder that holds your PNG files
        string targetFolder = @"C:\MyPngFolder";   // <-- change to your path

        // 3️⃣ Process every PNG in the folder
        ProcessFolder(ocrEngine, targetFolder);
    }

    static void ProcessFolder(OcrEngine engine, string folderPath)
    {
        if (!Directory.Exists(folderPath))
        {
            Console.WriteLine($"❌ Folder not found: {folderPath}");
            return;
        }

        string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

        if (pngFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No PNG files found.");
            return;
        }

        foreach (var pngPath in pngFiles)
        {
            Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
            ExtractAndSave(engine, pngPath);
        }
    }

    static void ExtractAndSave(OcrEngine engine, string imagePath)
    {
        try
        {
            engine.Image = ImageStream.FromFile(imagePath);
            RecognitionResult result = engine.Recognize();

            string txtPath = Path.ChangeExtension(imagePath, ".txt");
            File.WriteAllText(txtPath, result.Text);

            Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❗ Error on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

Salva questo come `Program.cs`, esegui `dotnet run` e osserva la magia.

## Conclusione

Ora disponi di un **metodo completo e pronto per la produzione per estrarre testo da file PNG** usando C#. Il tutorial ha coperto tutto—dalla configurazione del progetto, all’inizializzazione di un motore OCR accelerato GPU, **scorrendo le immagini**, fino al **batch OCR images** e al salvataggio dei risultati in testo semplice.  

Se sei curioso dei prossimi passi, prova a:

- **Convertire le immagini in testo** per altri formati (JPG, BMP

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}