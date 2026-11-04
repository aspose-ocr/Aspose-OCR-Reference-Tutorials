---
category: general
date: 2026-04-01
description: Scopri come riconoscere rapidamente il testo da file PNG impostando l'ID
  del dispositivo GPU e abilitando l'accelerazione GPU in Aspose OCR. Guida passo‑passo
  in C#.
draft: false
keywords:
- recognize text from png
- set gpu device id
- Aspose OCR GPU
- batch OCR C#
- OCR performance tips
language: it
og_description: Riconosci il testo dai file PNG rapidamente impostando l'ID del dispositivo
  GPU. Segui questa guida completa in C# per abilitare l'accelerazione GPU con Aspose
  OCR.
og_title: Riconoscere il testo da PNG – Tutorial OCR Aspose accelerato GPU
tags:
- C#
- OCR
- GPU
- Aspose
title: Riconoscere il testo da PNG con Aspose OCR – Demo batch accelerata GPU
url: /it/net/ocr-optimization/recognize-text-from-png-with-aspose-ocr-gpu-accelerated-batc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# riconoscere testo da png – Tutorial completo batch accelerato da GPU in C#

Hai mai avuto bisogno di **riconoscere testo da png** immagini ma hai trovato il processo dolorosamente lento? Non sei solo. La maggior parte degli sviluppatori inizia con una semplice chiamata OCR, poi fissa una console che avanza come una lumaca quando una cartella contiene decine di screenshot.  

Buone notizie? Aspose OCR può delegare il lavoro pesante alla tua scheda grafica, e con solo un paio di righe puoi **set gpu device id** per scegliere la GPU esatta che desideri. In questa guida percorreremo un esempio completo e eseguibile che preleva tutti i PNG da una cartella, attiva l'accelerazione GPU, seleziona la prima GPU e stampa il conteggio dei caratteri per ogni file.

Alla fine avrai un programma autonomo che potrai inserire in qualsiasi progetto .NET, e comprenderai perché abilitare la GPU è importante, come gestire i casi limite e cosa modificare per ottenere prestazioni ancora migliori.

## Di cosa avrai bisogno

- **.NET 6.0** o successivo (il codice si compila anche con .NET Core).  
- Il pacchetto **Aspose.OCR** NuGet – installalo con `dotnet add package Aspose.OCR`.  
- Una macchina con una GPU compatibile CUDA (NVIDIA è tipica) e il driver appropriato.  
- Una cartella piena di immagini **PNG** che desideri elaborare.  

Se qualcuno di questi ti è sconosciuto, non preoccuparti. I passaggi seguenti includono i comandi esatti di cui hai bisogno, e discuteremo anche cosa fare quando una GPU non è presente.

## Passo 1: Inizializzare il motore OCR e abilitare l'accelerazione GPU  

La prima cosa da fare è creare un'istanza di `OcrEngine` e attivare il supporto GPU. Questa opzione indica ad Aspose di utilizzare le librerie native CUDA sottostanti.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // Enable GPU acceleration – huge speed boost for large batches
        ocrEngine.UseGpuAcceleration = true;
```

**Perché è importante:** Senza `UseGpuAcceleration`, ogni immagine viene elaborata sulla CPU, il che può essere di ordini di grandezza più lento, soprattutto per PNG ad alta risoluzione. Abilitare l'opzione prepara anche il motore ad accettare un dispositivo GPU specifico in seguito.

## Passo 2: Impostare l'ID del dispositivo GPU (Opzionale ma consigliato)  

Se la tua workstation ha più di una GPU, puoi decidere quale utilizzare. Gli ID dei dispositivi partono da **0**, quindi `0` sceglie la prima GPU, `1` la seconda, e così via.

```csharp
        // Optional: Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id
```

**Consiglio professionale:** Quando si esegue su un server condiviso, impostare esplicitamente l'ID del dispositivo GPU può impedire al tuo lavoro di rubare risorse ad altri processi. Se ometti questa riga, Aspose sceglierà il dispositivo predefinito, il che di solito è accettabile per una configurazione a singola GPU.

## Passo 3: Raccogliere tutti i file PNG dalla tua cartella batch  

Ora dobbiamo individuare tutti i PNG su cui eseguire l'OCR. Il metodo `Directory.GetFiles` fa il lavoro pesante.

```csharp
        // Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // <-- replace with your path
            "*.png",                  // only PNG files
            System.IO.SearchOption.TopDirectoryOnly);
```

**Caso limite:** Se la cartella è vuota, `imageFiles` sarà un array vuoto. Lo gestiremo più tardi con un messaggio amichevole.

## Passo 4: Elaborare ogni immagine e stampare il conteggio dei caratteri riconosciuti  

Ora il ciclo principale. Per ogni PNG chiamiamo `Recognize`, poi stampiamo il nome del file e la lunghezza del testo estratto.

```csharp
        // Verify we actually found files
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

**Cosa vedrai:**  
```
invoice1.png → 342 chars
receipt_2023.png → 127 chars
screenshot.png → 0 chars
```

Se un'immagine non contiene testo, il conteggio sarà `0`. È perfettamente normale per screenshot puramente grafici.

## Passo 5: Eseguire il programma e verificare l'uso della GPU  

Compila il file (`dotnet build`) ed eseguilo (`dotnet run`). Mentre la console scorre, puoi aprire lo strumento di monitoraggio GPU (come NVIDIA Smi) per vedere il picco di utilizzo della GPU brevemente per ogni immagine. Se non vedi alcuna attività, ricontrolla che:

1. Il driver CUDA è installato.  
2. `UseGpuAcceleration` è impostato su `true`.  
3. Il corretto `GpuDeviceId` corrisponde a una GPU fisica.

Se la GPU non è disponibile, Aspose tornerà automaticamente alla CPU, ma perderai il vantaggio di velocità.

## Variazioni comuni e consigli

| Situazione | Cosa cambiare |
|-----------|----------------|
| **Formato immagine diverso** (es., JPEG) | Modifica il pattern di ricerca in `*.jpg` o `*.*` e Aspose riconoscerà comunque il testo. |
| **La dimensione del batch è enorme** (migliaia di file) | Elabora a blocchi per evitare pressione di memoria: dividi `imageFiles` in array più piccoli. |
| **Hai bisogno del testo reale, non solo della lunghezza** | Sostituisci `ocrResult.Text.Length` con `ocrResult.Text` nella `WriteLine`. |
| **Esecuzione su server headless** | Assicurati che il server abbia un driver GPU; altrimenti, imposta `UseGpuAcceleration = false` per evitare errori non necessari. |
| **GPU multiple, vuoi bilanciare il carico** | Esegui un ciclo su `ocrEngine.GpuDeviceId = i % gpuCount` all'interno del `foreach` per ruotare i dispositivi. |

## Output previsto e verifica  

Quando tutto funziona, la console stampa ogni nome file seguito dal conteggio dei caratteri, come mostrato in precedenza. Per ricontrollare l'output OCR reale, puoi temporaneamente stampare il testo:

```csharp
Console.WriteLine($"{Path.GetFileName(imagePath)} → {ocrResult.Text}");
```

Ricorda solo di rimuovere o commentare quella riga per batch grandi; stampare migliaia di linee può sovraccaricare il tuo terminale.

## Esempio completo funzionante (pronto per copia‑incolla)

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine and enable GPU acceleration
        var ocrEngine = new OcrEngine();
        ocrEngine.UseGpuAcceleration = true;

        // Step 2: (Optional) Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id

        // Step 3: Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // replace with your folder path
            "*.png",
            System.IO.SearchOption.TopDirectoryOnly);

        // Guard clause if no files are found
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Step 4: Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

Salva questo come `GpuBatchDemo.cs`, esegui `dotnet add package Aspose.OCR`, poi `dotnet run`. Dovresti vedere i conteggi dei caratteri apparire quasi istantaneamente per ogni PNG, grazie all'accelerazione GPU.

## Conclusione  

Ora sai come **recognize text from png** file in modo efficiente abilitando l'accelerazione GPU e impostando esplicitamente **set gpu device id** in Aspose OCR. Il programma completo, pronto per copia‑incolla, gestisce la scoperta della cartella, i controlli dei casi limite e ti fornisce un feedback immediato sulle prestazioni OCR.  

Prossimi passi? Prova a sostituire la chiamata `Recognize` con `ocrEngine.RecognizeAsync` se ti serve un'elaborazione non bloccante, o sperimenta diverse opzioni di pre‑elaborazione immagine (es., binarizzazione) offerte da Aspose. Potresti anche inviare i risultati OCR a un database o a un indice di ricerca per una soluzione di ricerca full‑text.  

Hai domande sulla gestione di PDF multi‑pagina, o vuoi confrontare Aspose OCR con Tesseract? Lascia un commento o esplora i nostri altri tutorial su **batch OCR C#**, **OCR performance tips**, e **GPU‑driven image processing**. Buon coding!  

![Output della console che mostra i conteggi dei caratteri riconosciuti per i file PNG – riconoscere testo da png usando accelerazione GPU](image-placeholder.png "esempio output riconoscimento testo da png")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}