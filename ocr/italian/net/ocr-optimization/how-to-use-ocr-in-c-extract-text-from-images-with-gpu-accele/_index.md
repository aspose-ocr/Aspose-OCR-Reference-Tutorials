---
category: general
date: 2025-12-29
description: Come utilizzare l'OCR in C# per estrarre testo dalle immagini, visualizzare
  il conteggio dei caratteri e migliorare le prestazioni con l'accelerazione GPU usando
  Aspose OCR.
draft: false
keywords:
- how to use OCR
- extract text image
- display character count
- gpu acceleration ocr
- c# ocr aspose
language: it
og_description: Come utilizzare OCR in C# per estrarre testo dalle immagini, visualizzare
  il conteggio dei caratteri e accelerare l'elaborazione con GPU usando Aspose OCR.
og_title: Come usare OCR in C# – Estrazione rapida del testo con GPU
tags:
- OCR
- C#
- Aspose
- GPU
title: Come usare l'OCR in C# – Estrarre testo dalle immagini con accelerazione GPU
url: /it/net/ocr-optimization/how-to-use-ocr-in-c-extract-text-from-images-with-gpu-accele/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come usare l'OCR in C# – Guida completa

Ti sei mai chiesto **come usare l'OCR** in un progetto .NET senza scrivere migliaia di righe di codice? Forse hai scansionato un enorme file TIFF e hai bisogno del testo rapidamente, oppure vuoi semplicemente contare i caratteri per una dashboard di report. In entrambi i casi sei nel posto giusto. In questo tutorial vedremo come estrarre testo da un'immagine, visualizzare il conteggio dei caratteri e potenziare il processo con **GPU acceleration OCR** – il tutto con la libreria **C# Aspose OCR**.

Inseriremo anche gli argomenti secondari che potresti cercare: **extract text image**, **display character count**, e trucchi **c# ocr aspose**. Alla fine avrai un'app console pronta all'uso che può elaborare grandi scansioni in un lampo.

---

## Cosa imparerai

- Configurare Aspose OCR in un progetto C# (senza misteri NuGet).  
- Abilitare **GPU acceleration OCR** per file di grandi dimensioni.  
- Caricare un'immagine e **estrarre testo dall'immagine**.  
- **Visualizzare il conteggio dei caratteri** e il tempo di elaborazione.  
- Gestire le difficoltà comuni come driver GPU mancanti o formati immagine non supportati.

> **Prerequisito:** .NET 6+ (o .NET Framework 4.7.2) e una GPU compatibile. Se non disponi di una GPU, il codice tornerà elegantemente alla modalità CPU.

---

![Come usare l'OCR con accelerazione GPU in C#](ocr-gpu.png "esempio di utilizzo dell'OCR che mostra l'uso della GPU")

*Testo alternativo immagine: illustrazione su come usare l'OCR con accelerazione GPU*

---

## Passo 1: Installa Aspose OCR e prepara il progetto

### Perché è importante

Prima di poter **usare l'OCR**, la libreria deve essere referenziata. Aspose OCR viene fornito come unico pacchetto NuGet che include i binari nativi sia per CPU che per GPU, così non dovrai cercare manualmente le DLL.

```csharp
// In your terminal or Package Manager Console
dotnet add package Aspose.OCR
```

> **Consiglio:** Se punti a .NET Framework, usa l'interfaccia NuGet in Visual Studio per evitare conflitti di versione.

### Scheletro completo del progetto

Crea una nuova app console e incolla il seguente `Program.cs`. Include tutte le istruzioni `using` necessarie, così non dovrai indovinare cosa importare.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;
using Aspose.OCR.ImageProcessing; // optional, for advanced pre‑processing

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Call the helper that does the heavy lifting
            RunOcr(@"YOUR_DIRECTORY/large_scanned_page.tif");
        }

        static void RunOcr(string imagePath)
        {
            // Step 2: Create and configure the OCR engine (see next section)
        }
    }
}
```

Salva il file, ripristina i pacchetti e sei pronto per il passo successivo.

---

## Passo 2: Come usare il motore OCR con accelerazione GPU

### Perché abilitare la GPU?

Elaborare un TIFF multi‑megapixel su CPU può richiedere secondi o addirittura minuti. Il percorso **GPU acceleration OCR** scarica le operazioni pixel‑wise sulla tua scheda grafica, riducendo drasticamente i tempi — spesso a una frazione di quelli originali.

```csharp
static void RunOcr(string imagePath)
{
    // Create an OCR engine instance
    var ocrEngine = new OcrEngine();

    // Enable GPU acceleration – if a compatible device is found
    ocrEngine.UseGpu = true;
    ocrEngine.GpuDeviceId = 0; // 0 = first GPU; change if you have multiple

    // Optional sanity check – fall back to CPU if GPU init fails
    try
    {
        // This call forces the engine to initialize GPU resources
        ocrEngine.InitializeGpu();
        Console.WriteLine("✅ GPU acceleration enabled.");
    }
    catch (Exception ex)
    {
        Console.WriteLine($"⚠️ GPU init failed ({ex.Message}), switching to CPU.");
        ocrEngine.UseGpu = false;
    }

    // Load the image (this also validates format)
    var inputImage = Image.Load(imagePath);
    
    // Perform OCR – the heavy lifting happens here
    var ocrResult = ocrEngine.Recognize(inputImage);

    // Step 3: Display results (character count & processing time)
    DisplayResult(ocrResult);
}
```

> **Perché funziona:** `UseGpu` attiva la pipeline interna. `InitializeGpu()` forza una validazione anticipata così puoi intercettare problemi di driver prima della chiamata a lungo termine `Recognize`.

---

## Passo 3: Estrarre testo dall'immagine e visualizzare il conteggio dei caratteri

Ora che il motore è in funzione, **estraiamo il testo dall'immagine** e mostriamo quanti caratteri sono stati riconosciuti. Questa è la parte che la maggior parte degli sviluppatori salta, ma è fondamentale per la validazione e le analisi successive.

```csharp
static void DisplayResult(OcrResult ocrResult)
{
    // The raw OCR text
    string extractedText = ocrResult.Text;

    // Character count – includes spaces and line breaks
    int charCount = extractedText.Length;

    // Processing time in milliseconds (provided by Aspose)
    long processingMs = ocrResult.ProcessingTime;

    // Output to console – easy to pipe to a file or logger
    Console.WriteLine($"🖋️ Extracted {charCount} characters in {processingMs} ms");
    Console.WriteLine("----- Begin OCR Text -----");
    Console.WriteLine(extractedText);
    Console.WriteLine("------ End OCR Text ------");
}
```

**Output previsto** (esempio per una scansione di 2 pagine):

```
✅ GPU acceleration enabled.
🖋️ Extracted 12,345 characters in 842 ms
----- Begin OCR Text -----
Lorem ipsum dolor sit amet, consectetur...
... (rest of the page) ...
------ End OCR Text ------
```

Se la GPU non è disponibile, vedrai un avviso e otterrai lo stesso risultato, solo più lentamente.

---

## Passo 4: Gestire file di grandi dimensioni e casi limite

### E se l'immagine è enorme?

Aspose OCR può streammare le pagine, ma hai comunque bisogno di RAM sufficiente. Una buona pratica è ridimensionare il DPI non essenziale prima del riconoscimento:

```csharp
// Optional pre‑processing: downscale to 300 DPI if original > 600 DPI
if (inputImage.DpiX > 600 || inputImage.DpiY > 600)
{
    inputImage = inputImage.Resize(0.5, 0.5); // 50% reduction
    Console.WriteLine("🔎 Image downscaled for faster OCR.");
}
```

### Driver GPU mancanti?

Il blocco `try/catch` attorno a `InitializeGpu()` intercetta già la maggior parte dei problemi, ma puoi anche interrogare i dispositivi disponibili:

```csharp
var gpuInfo = GpuDeviceManager.GetDevices();
if (gpuInfo.Count == 0)
{
    Console.WriteLine("⚡ No GPU detected – defaulting to CPU.");
    ocrEngine.UseGpu = false;
}
```

### Formati immagine non supportati?

Aspose supporta TIFF, PNG, JPEG, BMP e alcuni formati esotici. Se ricevi un `UnsupportedFormatException`, converti il file prima con uno strumento come ImageMagick o il metodo integrato `Image.Save` in PNG.

---

## Passo 5: Conclusione – Esempio completo funzionante

Copia‑incolla l'intero programma qui sotto in `Program.cs`. È una demo autonoma che puoi eseguire subito (basta sostituire il percorso).

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;
using Aspose.OCR.ImageProcessing;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust the path to point at your scanned TIFF or JPEG
            RunOcr(@"YOUR_DIRECTORY/large_scanned_page.tif");
        }

        static void RunOcr(string imagePath)
        {
            var ocrEngine = new OcrEngine
            {
                UseGpu = true,
                GpuDeviceId = 0
            };

            try
            {
                ocrEngine.InitializeGpu();
                Console.WriteLine("✅ GPU acceleration enabled.");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"⚠️ GPU init failed ({ex.Message}), switching to CPU.");
                ocrEngine.UseGpu = false;
            }

            var inputImage = Image.Load(imagePath);

            // Optional downscale for gigantic files
            if (inputImage.DpiX > 600 || inputImage.DpiY > 600)
            {
                inputImage = inputImage.Resize(0.5, 0.5);
                Console.WriteLine("🔎 Image downscaled for faster OCR.");
            }

            var ocrResult = ocrEngine.Recognize(inputImage);
            DisplayResult(ocrResult);
        }

        static void DisplayResult(OcrResult ocrResult)
        {
            string extractedText = ocrResult.Text;
            int charCount = extractedText.Length;
            long processingMs = ocrResult.ProcessingTime;

            Console.WriteLine($"🖋️ Extracted {charCount} characters in {processingMs} ms");
            Console.WriteLine("----- Begin OCR Text -----");
            Console.WriteLine(extractedText);
            Console.WriteLine("------ End OCR Text ------");
        }
    }
}
```

Eseguilo con `dotnet run` e osserva la console stampare il **conteggio dei caratteri** e il testo OCR. Questo è l'intero ciclo **come usare l'OCR** dall'inizio alla fine.

---

## Conclusione

Abbiamo appena coperto **come usare l'OCR** in C# per **estrarre testo dalle immagini**, **visualizzare il conteggio dei caratteri**, e accelerare l'intera pipeline con **GPU acceleration OCR** usando la libreria **c# ocr aspose**. I punti chiave:

1. Installa Aspose OCR via NuGet e riferisci gli spazi dei nomi corretti.  
2. Attiva la GPU, ma mantieni sempre un fallback CPU.  
3. Carica l'immagine, opzionalmente ridimensiona, poi chiama `Recognize`.  
4. Recupera `ocrResult.Text` e `ocrResult.ProcessingTime` per **visualizzare il conteggio dei caratteri** e le metriche di performance.  

Da qui puoi espandere — salvare il testo in un database, indicizzarlo per la ricerca, o eseguire il rilevamento della lingua sulla stringa estratta. Se devi elaborare PDF, basta trasformare ogni pagina in immagine; lo stesso codice funziona.

**Prossimi passi** da esplorare:

- Usare **extract text image** da PDF multi‑pagina con `PdfConverter`.  
- Regolare le impostazioni OCR (pacchetti lingua, riduzione rumore) per una maggiore precisione.  
- Scalare la soluzione in Azure Functions o AWS Lambda con istanze abilitate alla GPU.  

Provalo, rompi il codice, e poi miglioralo. È così che nascono i progetti OCR nel mondo reale. Buona programmazione, e che le tue scansioni siano sempre leggibili!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}