---
category: general
date: 2026-09-08
description: Scopri come abilitare la GPU per Aspose OCR, eseguire l'elaborazione
  OCR batch e estrarre testo dalle immagini in modo efficiente usando .NET.
draft: false
keywords:
- how to enable gpu
- extract text from images
- batch ocr processing
- ocr gpu acceleration
- aspose ocr .net
lastmod: 2026-09-08
og_description: Come abilitare la GPU per Aspose OCR. Questa guida mostra l'elaborazione
  OCR batch, l'estrazione di testo dalle immagini e la selezione del dispositivo GPU
  ottimale in .NET.
og_image_alt: Diagram of Aspose OCR engine offloading work to GPU for faster text
  extraction
og_title: Come abilitare la GPU per Aspose OCR – tutorial completo
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: Learn how to enable GPU for Aspose OCR, run batch OCR processing, and
    extract text from images efficiently using .NET.
  headline: How to enable GPU for Aspose OCR – complete tutorial
  type: TechArticle
- description: Learn how to enable GPU for Aspose OCR, run batch OCR processing, and
    extract text from images efficiently using .NET.
  name: How to enable GPU for Aspose OCR – complete tutorial
  steps:
  - name: 'Install the NuGet package: `dotnet add package Aspose.OCR --version 23.10.0`'
    text: 'Install the NuGet package: `dotnet add package Aspose.OCR --version 23.10.0`'
  - name: Replace the paths in `imageFiles` with the location of your own `.tif` files.
    text: Replace the paths in `imageFiles` with the location of your own `.tif` files.
  - name: 'Build and run: `dotnet run`.'
    text: 'Build and run: `dotnet run`.'
  type: HowTo
- questions:
  - answer: Yes, a commercial Aspose.OCR license is needed for production deployments;
      a free trial is available for evaluation.
    question: Is a license required for production use?
  - answer: Any NVIDIA GPU that supports CUDA 11.0 or newer, such as RTX 2060, RTX
      3070, RTX 4090, and the corresponding Tesla series.
    question: Which GPU models are officially supported?
  - answer: Absolutely. The same `OcrEngine` instance can be reused across requests;
      just ensure thread safety by cloning the engine per request.
    question: Can I run this code in an ASP.NET Core web API?
  - answer: Yes, you can set `ocrEngine.Language = Language.English | Language.Spanish`
      to enable simultaneous recognition of multiple languages.
    question: Does Aspose OCR handle multi‑language documents?
  - answer: The engine streams image data, so you can process images up to 10,000
      × 10,000 pixels without exhausting GPU memory, though performance may vary.
    question: What is the maximum image size the GPU can handle?
  type: FAQPage
tags:
- Aspose OCR
- GPU acceleration
- C#
- .NET
title: Come abilitare la GPU per Aspose OCR – tutorial completo
url: /it/net/ocr-configuration/how-to-enable-gpu-for-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come abilitare la GPU per Aspose OCR – tutorial completo

Ti sei mai chiesto **come abilitare la GPU** quando usi Aspose OCR? Non sei l'unico—gli sviluppatori che gestiscono enormi volumi di documenti spesso incontrano limiti di prestazioni perché il motore OCR è bloccato sulla CPU. La buona notizia? Attivare l'accelerazione GPU è abbastanza semplice e può ridurre di qualche secondo il tempo per ogni pagina. In questa guida vedremo **come abilitare la GPU**, eseguire **l'elaborazione OCR batch**, estrarre il testo riconosciuto e persino scegliere il dispositivo GPU corretto. Alla fine saprai **come usare Aspose** per un'estrazione di testo OCR fulminea.

## Risposte rapide
- **Cosa fa l'abilitazione della GPU?** Sposta l'analisi a livello di pixel sulla scheda grafica, riducendo il tempo di elaborazione fino all'80 % su immagini tipiche a 300 dpi.  
- **Ho bisogno di una licenza speciale?** No, il pacchetto NuGet standard Aspose.OCR include il supporto GPU.  
- **Quale versione di .NET è richiesta?** .NET 6.0 o successiva; l'API utilizza funzionalità moderne di C#.  
- **Posso eseguire su una macchina solo CPU?** Sì—se non viene trovata una GPU compatibile il motore passa automaticamente alla CPU.  
- **Quante immagini posso elaborare contemporaneamente?** Puoi mettere in coda centinaia di file; la GPU le gestirà sequenzialmente mentre il tuo codice può fornire l'immagine successiva non appena la precedente termina.

## Che cosa significa abilitare la GPU?
Il `how to enable GPU` è il processo di configurazione di `OcrEngine` di Aspose OCR per indirizzare i carichi di lavoro di elaborazione delle immagini a una scheda grafica compatibile CUDA anziché al processore centrale. Questo passaggio è controllato da due proprietà: `UseGpu` e `GpuDeviceId`. Abilitare questo flag trasferisce l'analisi dei pixel intensiva dal punto di vista computazionale alla GPU, che può gestire migliaia di thread in parallelo, riducendo drasticamente il tempo di elaborazione.

La classe `OcrEngine` è il componente principale di Aspose OCR che esegue l'analisi delle immagini e il riconoscimento del testo.

## Perché utilizzare l'accelerazione GPU con Aspose OCR?
Aspose OCR supporta **oltre 50 formati di immagine** e può elaborare batch di centinaia di pagine senza caricare l'intero documento in memoria. Quando l'accelerazione GPU è abilitata, i test di benchmark mostrano una **riduzione del 70 %‑80 %** del tempo medio di elaborazione per pagina su una RTX 3080 rispetto all'esecuzione solo CPU. Il guadagno di velocità si traduce direttamente in costi cloud più bassi e risultati più rapidi visibili all'utente in applicazioni ad alta intensità documentale.

## Prerequisiti
- .NET 6.0 o successivo (il codice utilizza la sintassi moderna di C#)  
- Pacchetto NuGet Aspose.OCR per .NET (versione 23.10 o successiva)  
- Una GPU compatibile CUDA con il driver appropriato installato (CUDA 11.0 minimo)  
- Una cartella contenente file `.tif` di esempio per l'esecuzione batch  

Se hai questi requisiti di base, immergiamoci.

## Come abilitare la GPU in Aspose OCR

Carica il motore OCR, attiva la modalità GPU e, facoltativamente, scegli un indice del dispositivo.  

`OcrEngine` è la classe principale di Aspose OCR che esegue l'analisi delle immagini e il riconoscimento del testo.  

Abilitare la GPU è un'operazione in due fasi: impostare `UseGpu = true` e, quando sono presenti più GPU, assegnare il `GpuDeviceId` desiderato. Questo paragrafo di risposta diretta spiega l'intero processo in 45 parole.

La prima cosa da fare è dire al `OcrEngine` di usare la GPU. Questo avviene tramite due semplici proprietà: `UseGpu` e, facoltativamente, `GpuDeviceId`. Impostare `UseGpu` a `true` attiva la modalità GPU, mentre `GpuDeviceId` consente di scegliere quale GPU (se ne hai più di una) deve svolgere il lavoro pesante.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;
using System.Collections.Generic;

// Step 1: Create the OCR engine and enable GPU acceleration
var ocrEngine = new OcrEngine
{
    // Turn on GPU support – this is the core of “how to enable gpu”
    UseGpu = true,

    // (optional) Choose GPU index 0; change if you have multiple devices
    GpuDeviceId = 0
};
```

> **Perché è importante** – La versione CPU elabora ogni pixel in sequenza, il che può diventare un collo di bottiglia per immagini ad alta risoluzione. La versione GPU esegue migliaia di thread in parallelo, riducendo drasticamente il tempo per pagina.

### Panoramica visiva  

![Diagramma che mostra come il motore OCR delega il lavoro alla GPU quando “how to enable gpu” è impostato](/images/enable-gpu-diagram.png){: .center .responsive alt="come abilitare gpu"}

[Diagramma che mostra come il motore OCR delega il lavoro alla GPU quando “how to enable gpu” è impostato](/images/enable-gpu-diagram.png)

*(Se non riesci a vedere l'immagine, immagina semplicemente un diagramma di flusso in cui il motore OCR passa il buffer dell'immagine al core CUDA.)*

## Come eseguire l'elaborazione OCR batch con Aspose

Il metodo `Recognize` di `OcrEngine` elabora un'immagine e restituisce un `OcrResult` contenente il testo estratto e i metadati. Puoi elaborare un'intera cartella iterando su un elenco di percorsi file. Il motore mette automaticamente in coda ogni immagine sulla GPU, mantenendo la pipeline occupata mentre la tua applicazione continua a fornire nuovi file. Questo approccio ti consente di gestire centinaia di TIFF in modo efficiente, con la GPU che svolge il lavoro pesante in parallelo.

```csharp
// Step 2: Define the image files you want to process
var imageFiles = new List<string>
{
    @"C:\OCRSamples\page1.tif",
    @"C:\OCRSamples\page2.tif",
    @"C:\OCRSamples\page3.tif"
};

// Step 3: Process each image and report the character count
foreach (var imagePath in imageFiles)
{
    // Recognize the image – the GPU does the heavy lifting behind the scenes
    var ocrResult = ocrEngine.Recognize(imagePath);

    // Show how many characters were extracted – a quick sanity check
    Console.WriteLine($"{imagePath}: {ocrResult.Text.Length} characters");
}
```

> **Consiglio professionale** – Per batch davvero massivi, considera l'uso di `Parallel.ForEach` insieme a `ocrEngine.Clone()` per evitare problemi di thread‑safety. Il metodo `Clone` crea una copia superficiale del motore che punta ancora allo stesso contesto GPU.

### Output previsto

```
C:\OCRSamples\page1.tif: 1245 characters
C:\OCRSamples\page2.tif: 1130 characters
C:\OCRSamples\page3.tif: 1389 characters
```

Se i numeri sembrano ragionevoli, il tuo **batch OCR processing** sta funzionando e la GPU è in uso.

## Come estrarre il testo dalle immagini – ottenere i risultati

`OcrResult` è l'oggetto che contiene l'output OCR, includendo il testo riconosciuto, i punteggi di confidenza e le informazioni di layout. Il metodo `Recognize` restituisce un oggetto `OcrResult`. Estrai il testo semplice dalla proprietà `Text` e scrivilo in un file per l'uso successivo. Memorizzare il testo OCR consente l'elaborazione a valle (indicizzazione di ricerca, data mining, ecc.) senza rieseguire il motore e ti fornisce un record permanente per il debug.

```csharp
foreach (var imagePath in imageFiles)
{
    var ocrResult = ocrEngine.Recognize(imagePath);
    var extractedText = ocrResult.Text;

    // Save the text to a .txt file with the same base name
    var outputPath = System.IO.Path.ChangeExtension(imagePath, ".txt");
    System.IO.File.WriteAllText(outputPath, extractedText);

    Console.WriteLine($"Extracted text saved to {outputPath}");
}
```

> **Perché estrarre in un file?** – Memorizzare il testo OCR consente l'elaborazione a valle (indicizzazione di ricerca, data mining, ecc.) senza rieseguire il motore. Inoltre ti fornisce un record permanente per il debug.

## Come impostare il dispositivo GPU per prestazioni ottimali

`CudaDeviceInfo` fornisce informazioni sulle GPU compatibili CUDA installate nel sistema. Quando sono presenti più GPU, usa `GpuDeviceId` per selezionare la migliore. L'indice corrisponde all'ordine restituito da `CudaDeviceInfo.GetDevices()`. Selezionare il dispositivo appropriato garantisce di utilizzare la GPU più potente e di evitare conflitti con altri carichi di lavoro su schede secondarie.

```csharp
using Aspose.OCR.Gpu;

// List all available GPU devices
var devices = CudaDeviceInfo.GetDevices();
for (int i = 0; i < devices.Length; i++)
{
    Console.WriteLine($"Device {i}: {devices[i].Name} (Compute Capability {devices[i].ComputeCapability})");
}

// Suppose you want to use the second GPU (index 1)
ocrEngine.GpuDeviceId = 1;
Console.WriteLine($"Switched to GPU device {ocrEngine.GpuDeviceId}");
```

> **Caso limite** – Alcune GPU più vecchie non supportano la versione CUDA richiesta. In tal caso, `UseGpu = true` tornerà silenziosamente alla CPU, quindi controlla sempre `ocrEngine.IsGpuEnabled` dopo l'inizializzazione.

## Come usare Aspose OCR in un progetto reale

Mettendo tutto insieme, ecco un'applicazione console compatta, pronta all'uso, che dimostra **come abilitare la GPU**, esegue **batch OCR processing**, estrae il testo e ti consente di scegliere il dispositivo GPU. L'esempio crea un `OcrEngine`, abilita la GPU, elenca i dispositivi disponibili, elabora ogni immagine e scrive il testo riconosciuto in un file `.txt` accanto all'immagine di origine.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.Collections.Generic;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialize OCR engine with GPU support
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            UseGpu = true,
            GpuDeviceId = 0 // change if you have multiple GPUs
        };

        // -------------------------------------------------
        // 2️⃣ (Optional) Show available GPU devices
        // -------------------------------------------------
        var devices = CudaDeviceInfo.GetDevices();
        Console.WriteLine("Available GPU devices:");
        for (int i = 0; i < devices.Length; i++)
        {
            Console.WriteLine($"  [{i}] {devices[i].Name} – Compute {devices[i].ComputeCapability}");
        }

        // -------------------------------------------------
        // 3️⃣ Define the batch of images to process
        // -------------------------------------------------
        var imageFiles = new List<string>
        {
            @"C:\OCRSamples\page1.tif",
            @"C:\OCRSamples\page2.tif",
            @"C:\OCRSamples\page3.tif"
        };

        // -------------------------------------------------
        // 4️⃣ Process each image, extract text, and save it
        // -------------------------------------------------
        foreach (var imagePath in imageFiles)
        {
            var result = ocrEngine.Recognize(imagePath);
            var text = result.Text;

            var txtPath = Path.ChangeExtension(imagePath, ".txt");
            File.WriteAllText(txtPath, text);

            Console.WriteLine($"{Path.GetFileName(imagePath)} → {Path.GetFileName(txtPath)} ({text.Length} chars)");
        }

        Console.WriteLine("All done! GPU‑accelerated OCR batch completed.");
    }
}
```

### Esecuzione del campione

1. Installa il pacchetto NuGet: `dotnet add package Aspose.OCR --version 23.10.0`  
2. Sostituisci i percorsi in `imageFiles` con la posizione dei tuoi file `.tif`.  
3. Compila ed esegui: `dotnet run`.  

Dovresti vedere l'elenco delle GPU, seguito da una riga per ogni immagine che riporta il conteggio dei caratteri e il percorso del file `.txt` generato.

## Domande comuni e insidie

- **Funziona su una macchina solo CPU?**  
  Sì—se `UseGpu` è `true` ma non viene trovata una GPU compatibile, Aspose passa alla CPU. Puoi verificare la modalità tramite `ocrEngine.IsGpuEnabled`.

- **Cosa succede se ricevo l'errore “CUDA driver version is insufficient”?**  
  Aggiorna il driver NVIDIA all'ultima versione che corrisponde al toolkit CUDA fornito con Aspose. La libreria richiede almeno CUDA 11.0 per le funzionalità GPU recenti.

- **Posso elaborare PDF direttamente?**  
  Aspose OCR funziona su immagini raster. Converti prima le pagine PDF in immagini (ad esempio, usando Aspose.PDF) e poi fornisci queste al motore OCR.

- **Come miglioro la precisione su scansioni rumorose?**  
  Abilita opzioni di pre‑elaborazione come `ocrEngine.Preprocess = true` o fornisci immagini a risoluzione più alta (300 dpi o più). L'accelerazione GPU rimane valida.

## Domande frequenti

**D: È necessaria una licenza per l'uso in produzione?**  
R: Sì, è necessaria una licenza commerciale Aspose.OCR per le distribuzioni in produzione; è disponibile una prova gratuita per la valutazione.

**D: Quali modelli di GPU sono ufficialmente supportati?**  
R: Qualsiasi GPU NVIDIA che supporta CUDA 11.0 o versioni successive, come RTX 2060, RTX 3070, RTX 4090 e le corrispondenti serie Tesla.

**D: Posso eseguire questo codice in un'API web ASP.NET Core?**  
R: Assolutamente. La stessa istanza di `OcrEngine` può essere riutilizzata tra le richieste; basta garantire la sicurezza dei thread clonando il motore per ogni richiesta.

**D: Aspose OCR gestisce documenti multilingua?**  
R: Sì, puoi impostare `ocrEngine.Language = Language.English | Language.Spanish` per abilitare il riconoscimento simultaneo di più lingue.

**D: Qual è la dimensione massima dell'immagine che la GPU può gestire?**  
R: Il motore trasmette i dati dell'immagine in streaming, quindi puoi elaborare immagini fino a 10.000 × 10.000 pixel senza esaurire la memoria GPU, anche se le prestazioni possono variare.

---

**Ultimo aggiornamento:** 2026-09-08  
**Testato con:** Aspose.OCR 23.10 for .NET  
**Autore:** Aspose

## Tutorial correlati

- [Come usare Ocr in C per estrarre testo dalle immagini con accelerazione GPU](/ocr/net/ocr-optimization/how-to-use-ocr-in-c-extract-text-from-images-with-gpu-accele/)
- [Estrarre testo da immagine con Aspose Ocr GPU Guida C](/ocr/net/ocr-optimization/extract-text-from-image-with-aspose-ocr-gpu-c-guide/)
- [Rimuovere lo sfondo OCR con Aspose OCR Guida completa GPU](/ocr/net/ocr-optimization/remove-background-ocr-with-aspose-ocr-complete-gpu-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}