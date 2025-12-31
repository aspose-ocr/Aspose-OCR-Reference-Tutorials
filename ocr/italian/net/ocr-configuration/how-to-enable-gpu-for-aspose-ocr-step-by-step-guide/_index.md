---
category: general
date: 2025-12-30
description: Come abilitare la GPU in Aspose OCR per l'elaborazione batch OCR e l'estrazione
  del testo OCR. Scopri come impostare il dispositivo GPU e come utilizzare Aspose
  in modo efficiente.
draft: false
keywords:
- how to enable gpu
- batch ocr processing
- ocr text extraction
- set gpu device
- how to use aspose
language: it
og_description: Come abilitare la GPU in Aspose OCR. Segui questa guida per l'elaborazione
  OCR batch, l'estrazione del testo OCR, impostare il dispositivo GPU e imparare come
  utilizzare Aspose.
og_title: Come abilitare la GPU per Aspose OCR – Tutorial completo
tags:
- Aspose
- OCR
- GPU
- C#
title: Come abilitare la GPU per Aspose OCR – Guida passo passo
url: /it/net/ocr-configuration/how-to-enable-gpu-for-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come abilitare la GPU per Aspose OCR – Tutorial completo

Ti sei mai chiesto **come abilitare la GPU** quando usi Aspose OCR? Non sei l'unico—gli sviluppatori che gestiscono enormi volumi di documenti spesso incontrano colli di bottiglia di prestazioni perché il motore OCR è bloccato sulla CPU. La buona notizia? Attivare l'accelerazione GPU è piuttosto semplice e può far risparmiare secondi per ogni pagina. In questa guida vedremo **come abilitare la GPU**, eseguire **elaborazione OCR batch**, estrarre il testo riconosciuto e persino scegliere il dispositivo GPU corretto. Alla fine saprai **come usare Aspose** per un'estrazione di testo OCR fulminea.

## Cosa copre questo tutorial

Inizieremo configurando la libreria Aspose OCR, poi abiliteremo il supporto GPU e infine eseguiremo un batch di immagini TIFF attraverso il motore. Lungo il percorso spiegheremo perché potresti voler **impostare manualmente il dispositivo GPU**, quali insidie osservare e come verificare che l'estrazione del testo abbia effettivamente funzionato. Nessuna documentazione esterna, solo una soluzione completa, pronta da copiare‑incollare che puoi eseguire subito.

> **Prerequisiti**  
> - .NET 6.0 o successivo (il codice usa la sintassi moderna di C#)  
> - Pacchetto NuGet Aspose.OCR per .NET (versione 23.10 o più recente)  
> - Una GPU compatibile con CUDA con il driver appropriato installato  
> - Una cartella con alcuni file di esempio `.tif` per l'esecuzione batch  

Se hai questi requisiti di base, immergiamoci.

## Come abilitare la GPU in Aspose OCR

La prima cosa da fare è indicare al `OcrEngine` di usare la GPU. Questo avviene tramite due semplici proprietà: `UseGpu` e, opzionalmente, `GpuDeviceId`. Impostare `UseGpu` a `true` attiva la modalità GPU, mentre `GpuDeviceId` ti permette di scegliere quale GPU (se ne hai più di una) deve svolgere il lavoro pesante.

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

> **Perché è importante** – La versione CPU elabora ogni pixel in modo sequenziale, il che può diventare un collo di bottiglia per immagini ad alta risoluzione. La versione GPU esegue migliaia di thread in parallelo, riducendo drasticamente il tempo per pagina.

### Panoramica visiva  

![Diagramma che mostra come il motore OCR delega il lavoro alla GPU quando “come abilitare gpu” è impostato](/images/enable-gpu-diagram.png){: .center .responsive alt="come abilitare gpu"}

*(Se non riesci a vedere l'immagine, immagina semplicemente un diagramma di flusso in cui il motore OCR passa il buffer dell'immagine al core CUDA.)*

## Elaborazione OCR batch con Aspose

Ora che il motore è pronto per la GPU, forniamogli un elenco di file. L'elaborazione batch è semplice come iterare su una `List<string>` che contiene i percorsi delle tue immagini. Poiché usiamo la GPU, il motore accoderà automaticamente ogni immagine al dispositivo, mantenendo la pipeline occupata.

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

> **Consiglio professionale** – Per batch davvero enormi, considera l'uso di `Parallel.ForEach` insieme a `ocrEngine.Clone()` per evitare problemi di thread‑safety. Il metodo `Clone` crea una copia superficiale del motore che punta ancora allo stesso contesto GPU.

### Output previsto

```
C:\OCRSamples\page1.tif: 1245 characters
C:\OCRSamples\page2.tif: 1130 characters
C:\OCRSamples\page3.tif: 1389 characters
```

Se i numeri sembrano ragionevoli, il tuo **batch OCR processing** sta funzionando e la GPU è in uso.

## Estrazione del testo OCR – Ottenere i risultati

Il metodo `Recognize` restituisce un oggetto `OcrResult` che contiene il testo grezzo, i punteggi di confidenza e persino le bounding box se ti servono. Estraiamo il testo semplice e scriviamolo in un file così potrai verificare l'estrazione.

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

> **Perché estrarre in un file?** – Salvare il testo OCR consente l'elaborazione a valle (indicizzazione di ricerca, data mining, ecc.) senza dover rieseguire il motore. Fornisce anche un record permanente per il debug.

## Imposta il dispositivo GPU per prestazioni ottimali

Se la tua workstation dispone di più GPU—ad esempio, una RTX dedicata per il ML e una scheda grafica integrata—vuoi assicurarti di utilizzare quella giusta. La proprietà `GpuDeviceId` accetta un intero che corrisponde all'indice del dispositivo riportato da `CudaDeviceInfo.GetDevices()`.

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

Mettendo tutto insieme, ecco un'applicazione console compatta, pronta da eseguire, che dimostra **come abilitare la GPU**, esegue **batch OCR processing**, estrae il testo e ti permette di scegliere il dispositivo GPU.

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

## Domande comuni e problemi

- **Funziona su una macchina solo CPU?**  
  Sì—se `UseGpu` è `true` ma non viene trovata una GPU compatibile, Aspose torna alla CPU. Puoi verificare la modalità tramite `ocrEngine.IsGpuEnabled`.

- **Cosa succede se ricevo un errore “CUDA driver version is insufficient”?**  
  Aggiorna il driver NVIDIA all'ultima versione che corrisponde al toolkit CUDA fornito con Aspose. La libreria richiede almeno CUDA 11.0 per le recenti funzionalità GPU.

- **Posso elaborare direttamente i PDF?**  
  Aspose OCR funziona su immagini raster. Converti prima le pagine PDF in immagini (ad esempio, usando Aspose.PDF) e poi passale al motore OCR.

- **Come migliorare la precisione su scansioni rumorose?**  
  Abilita opzioni di pre‑elaborazione come `ocrEngine.Preprocess = true` o utilizza immagini a risoluzione più alta (300 dpi o più). L'accelerazione GPU rimane valida.

## Conclusione

Abbiamo coperto **come abilitare la GPU** per Aspose OCR, illustrato **l'elaborazione OCR batch**, dimostrato **l'estrazione del testo OCR** e mostrato come **impostare il dispositivo GPU** per prestazioni ottimali. Seguendo il campione di codice completo, ora puoi integrare un OCR veloce, alimentato dalla GPU, in qualsiasi progetto .NET e rispondere con sicurezza alla perenne domanda “come usare Aspose”.

Pronto per il passo successivo? Prova ad aggiungere il rilevamento della lingua, a inserire il testo estratto in un indice di ricerca, o a sperimentare il scaling multi‑GPU per archivi documentali massivi. Il cielo è il limite quando combini l'API robusta di Aspose con la potenza grezza delle GPU moderne.

Buon coding, e che i tuoi job OCR girino veloci quanto la tua GPU può gestire!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}