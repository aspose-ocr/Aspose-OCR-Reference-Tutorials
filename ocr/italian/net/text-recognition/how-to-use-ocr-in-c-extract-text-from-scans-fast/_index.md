---
category: general
date: 2026-03-13
description: Come utilizzare l'OCR in C# per estrarre testo dalle scansioni. Impara
  a convertire TIFF in testo con Aspose OCR, accelerazione GPU e codice passo‑passo.
draft: false
keywords:
- how to use OCR
- extract text from scans
- convert tiff to text
- c# ocr tutorial
language: it
og_description: Come utilizzare l'OCR in C# per estrarre testo da scansioni. Questa
  guida ti mostra come convertire i file TIFF in testo con Aspose OCR e accelerazione
  GPU.
og_title: Come usare l'OCR in C# – Estrai il testo dalle scansioni rapidamente
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Come usare l'OCR in C# – Estrai il testo dalle scansioni rapidamente
url: /it/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-scans-fast/
---

Should we translate? The instruction says translate all text content naturally to Italian, but keep technical terms in English. "how to use OCR" is phrase, but "OCR" is technical term, "how to use" could be translated. However it's inside bold, we can translate the phrase but keep OCR. So maybe **come usare OCR**. Let's do that.

Proceed.

We'll translate each paragraph.

Make sure not to translate code block placeholders.

Also tables: need translate column headers and content.

Let's rewrite.

I'll produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come usare OCR in C# – Estrarre testo da scansioni velocemente

Ti sei mai chiesto **come usare OCR** per estrarre testo leggibile da una pila di file TIFF scansionati? Non sei il solo. In molti progetti reali—pensa alla digitalizzazione di fatture, all'archiviazione di documenti storici o semplicemente a rendere i PDF ricercabili—gli sviluppatori hanno bisogno di un modo affidabile per **estrarre testo da scansioni** senza sforzi.

La buona notizia? Con Aspose OCR e poche righe di C# puoi convertire TIFF in testo in pochi secondi, anche su una workstation modesta. Di seguito trovi un esempio completo, pronto all'uso, più le motivazioni dietro ogni scelta così da poterlo adattare al tuo flusso di lavoro.

## Cosa ti serve

Prima di immergerci, assicurati di avere a disposizione quanto segue:

| Prerequisito | Perché è importante |
|--------------|----------------------|
| .NET 6+ (o .NET Framework 4.7+) | Il pacchetto NuGet Aspose OCR è destinato a runtime .NET moderni. |
| Visual Studio 2022 (o qualsiasi IDE tu preferisca) | Ti offre IntelliSense e debug semplificato. |
| Una GPU compatibile CUDA & driver (opzionale) | Consente `ocrEngine.UseGpu = true` per un notevole aumento di velocità su grandi batch. |
| Una cartella di immagini TIFF da elaborare | Questo tutorial usa file `*.tif`, ma puoi adattare il pattern. |
| Pacchetto NuGet Aspose.OCR (`Install-Package Aspose.OCR`) | La libreria core che esegue il lavoro pesante. |

Se ti manca qualcosa, procuratelo subito—non ha senso continuare la lettura per poi incappare in una dipendenza mancante.

## Panoramica della soluzione

A livello alto il programma fa tre cose:

1. **Crea un motore OCR** e, facoltativamente, attiva l'accelerazione GPU.  
2. **Itera su ogni file TIFF** in una directory, esegue il riconoscimento e cattura il testo plain‑text risultante.  
3. **Scrive il testo** in un file `.txt` posizionato accanto all'immagine originale.

Tutto qui. Il codice è deliberatamente piccolo, ma dimostra le best practice come la selezione esplicita della lingua, il corretto smaltimento delle risorse e la gestione degli errori per i casi limite più comuni.

![How to use OCR in C# example](/images/how-to-use-ocr-csharp.png "Illustration of how to use OCR in C# to extract text from scans")

## Passo 1: Inizializzare il motore OCR (How to Use OCR)

La prima cosa di cui hai bisogno è un'istanza di `OcrEngine`. Questo oggetto è il gateway a tutte le funzionalità di Aspose OCR. Per impostazione predefinita funziona sulla CPU, ma impostare `UseGpu = true` indica alla libreria di delegare i calcoli matriciali pesanti alla tua scheda grafica—purché tu abbia installato un driver compatibile CUDA.

```csharp
using Aspose.OCR;
using System.IO;

// Initialise the engine ----------------------------------------------------
OcrEngine ocrEngine = new OcrEngine
{
    // Enable GPU acceleration if a compatible card is present.
    // If you don’t have a GPU, just leave this as false – the code will still run.
    UseGpu = true,

    // Choose English as the recognition language. Change this if you need
    // another language pack (e.g., Language.French, Language.Spanish, etc.).
    Language = Language.English
};
```

**Perché è importante:**  
- **Accelerazione GPU** può ridurre i tempi di elaborazione fino al 70 % per scansioni ad alta risoluzione.  
- **Selezione esplicita della lingua** evita che il motore indovini e migliora la precisione, soprattutto per script non latini.

## Passo 2: Puntare il motore alle tue scansioni (Convert TIFF to Text)

Successivamente indichiamo al programma dove cercare le immagini. Usare `Directory.GetFiles` con un filtro `*.tif` mantiene la logica semplice ed evita di includere file non correlati come `.jpg` o `.png`.

```csharp
// Define the folder that contains the scanned TIFF images -----------------
string inputFolder = @"C:\ScannedDocs"; // <-- replace with your actual path

// Verify the folder exists before we start looping
if (!Directory.Exists(inputFolder))
{
    Console.WriteLine($"❌ Folder not found: {inputFolder}");
    return;
}
```

**Nota caso limite:** Se la directory è vuota, il ciclo sottostante semplicemente non verrà mai eseguito, il che è perfettamente accettabile. Vedrai più tardi un messaggio amichevole “No files found”.

## Passo 3: Elaborare ogni file TIFF (Extract Text from Scans)

Ora il cuore del programma: caricare ogni immagine, eseguire OCR e salvare l'output. L'helper `ImageStream.FromFile` trasmette il file direttamente in memoria, risultando più efficiente rispetto al caricamento preliminare di un `Bitmap`.

```csharp
// Step 3: Iterate over every .tif file in the folder --------------------
string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

if (tiffFiles.Length == 0)
{
    Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
}
else
{
    foreach (var imagePath in tiffFiles)
    {
        try
        {
            // Load the current image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR on the image
            ocrEngine.Recognize();

            // Build the output .txt file path (same name, different extension)
            string textPath = Path.ChangeExtension(imagePath, ".txt");

            // Save the extracted text
            File.WriteAllText(textPath, ocrEngine.Text);

            Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
        }
        catch (Exception ex)
        {
            // Log the error but continue with the next file
            Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

**Perché avvolgere ogni iterazione in un `try/catch`:**  
Elaborare un batch di documenti è disordinato; un TIFF corrotto o un intoppo di out‑of‑memory non dovrebbe abortire l'intera esecuzione. Il blocco catch registra il problema e prosegue, mantenendo la pipeline robusta.

### Output previsto

Per ogni `example.tif` troverai un file `example.txt` gemello contenente qualcosa di simile a:

```
Invoice #12345
Date: 2024‑01‑15
Total: $1,250.00
Thank you for your business!
```

Se il motore OCR non riesce a leggere una riga, lascerà semplicemente una riga vuota o un carattere illeggibile—niente crash.

## Passo 4: Pulizia e smaltimento (Best Practice)

`OcrEngine` implementa `IDisposable`, quindi è buona norma liberare le risorse native quando hai finito. In una piccola app console potresti fare affidamento sul GC, ma lo smaltimento esplicito è un'abitudine che vale la pena coltivare.

```csharp
// Dispose the engine when everything is finished -------------------------
ocrEngine.Dispose();
Console.WriteLine("🎉 All done! OCR engine released.");
```

## Esempio completo funzionante (Pronto da copiare‑incollare)

Di seguito trovi il programma completo da incollare in un nuovo progetto Console App. Compila così com'è, a patto che tu abbia aggiunto il pacchetto NuGet Aspose.OCR.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // --------------------------------------------------------------------
        // Step 1: Initialise the OCR engine (how to use OCR)
        // --------------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            UseGpu = true,               // Enable GPU if available
            Language = Language.English  // Set language for recognition
        };

        // --------------------------------------------------------------------
        // Step 2: Define the folder containing TIFF scans (convert TIFF to text)
        // --------------------------------------------------------------------
        string inputFolder = @"C:\ScannedDocs"; // <-- adjust this path

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"❌ Folder not found: {inputFolder}");
            return;
        }

        // --------------------------------------------------------------------
        // Step 3: Process each TIFF file (extract text from scans)
        // --------------------------------------------------------------------
        string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

        if (tiffFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
        }
        else
        {
            foreach (var imagePath in tiffFiles)
            {
                try
                {
                    // Load image
                    ocrEngine.Image = ImageStream.FromFile(imagePath);

                    // Run OCR
                    ocrEngine.Recognize();

                    // Save result next to source image
                    string textPath = Path.ChangeExtension(imagePath, ".txt");
                    File.WriteAllText(textPath, ocrEngine.Text);

                    Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
                }
            }
        }

        // --------------------------------------------------------------------
        // Step 4: Clean‑up (c# OCR tutorial best practice)
        // --------------------------------------------------------------------
        ocrEngine.Dispose();
        Console.WriteLine("🎉 All done! OCR engine released.");
    }
}
```

### Checklist veloce

- **Flag GPU** – rimuovi o imposta a `false` se non hai un driver CUDA.  
- **Lingua** – sostituisci `Language.English` con qualsiasi altra lingua supportata.  
- **Pattern di file** – cambia `"*.tif"` in `"*.png"` o `"*.*"` se le tue scansioni sono in un altro formato.  

## Problemi comuni & Pro Tips (c# OCR tutorial)

| Problema | Come evitarlo |
|----------|---------------|
| **Errori di out‑of‑memory** su batch enormi | Elabora i file in blocchi più piccoli o chiama `GC.Collect()` dopo ogni 50 file (raramente necessario). |
| **GPU non rilevata** ma `UseGpu = true` | Il motore ricade silenziosamente sulla CPU, ma puoi verificare `ocrEngine.IsGpuAvailable` dopo la costruzione. |
| **Pacchetto lingua errato** porta a output illeggibile | Imposta sempre `ocrEngine.Language` esplicitamente; il valore predefinito può essere `Language.Unknown`. |
| **Il percorso del file contiene caratteri Unicode** | Usa `Path.GetFullPath` per normalizzare, o aggiungi il prefisso `@"\\?\"` su Windows se i percorsi superano |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}