---
category: general
date: 2026-01-02
description: Esegui OCR su PNG rapidamente usando Aspose OCR e il supporto GPU. Scopri
  come riconoscere il testo da un'immagine, estrarre il testo dall'immagine e impostare
  il limite di memoria GPU.
draft: false
keywords:
- run OCR on PNG
- recognize text from image
- extract text from image
- how to extract text
- set GPU memory limit
language: it
og_description: Esegui OCR su PNG in modo efficiente sfruttando Aspose OCR e l'accelerazione
  GPU. Questo tutorial mostra come riconoscere il testo da un'immagine, estrarre il
  testo dall'immagine e controllare l'uso della memoria GPU.
og_title: Esegui OCR su PNG con GPU – Guida completa C#
tags:
- OCR
- C#
- GPU
title: Esegui OCR su PNG con GPU – Guida completa C#
url: /it/net/ocr-optimization/run-ocr-on-png-with-gpu-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# eseguire OCR su PNG con GPU – Guida completa in C#

Hai mai dovuto **eseguire OCR su PNG** ma ti sei bloccato per le prestazioni? Non sei l’unico. In molte pipeline reali un singolo PNG ad alta risoluzione può rallentare un motore OCR solo CPU, trasformando quello che dovrebbe essere una rapida ricerca in un’attesa di minuti.  

La buona notizia è che Aspose OCR include estensioni GPU che ti permettono di **riconoscere testo da immagini** in una frazione del tempo. In questo tutorial vedremo un esempio pratico che mostra esattamente come **eseguire OCR su PNG** usando C#, come **estrarre testo da immagine**, e anche come **impostare il limite di memoria GPU** per rimanere entro il budget hardware.

Tratteremo anche il “come” e il “perché” di ogni passaggio, così avrai un modello mentale solido – non solo uno snippet da copiare‑incollare.

## Cosa imparerai

- I prerequisiti per usare il supporto GPU di Aspose OCR.  
- Come caricare un PNG in un `Bitmap` e passarlo al motore OCR.  
- Come configurare `GpuDevice` e `GpuMemoryLimitMb` per prestazioni ottimali.  
- Come **riconoscere testo da immagine** e recuperare il risultato in plain‑text.  
- Suggerimenti per gestire casi particolari come GPU a bassa memoria o PNG multi‑pagina.  

Al termine di questa guida sarai in grado di **eseguire OCR su PNG** a velocità GPU e controllare con sicurezza l’impronta di memoria dei tuoi job OCR.

![Diagramma che mostra l'esecuzione di OCR su PNG con accelerazione GPU](run-ocr-on-png-diagram.png "esempio di OCR su PNG")

## Prerequisiti

Prima di immergerci, assicurati di avere:

1. .NET 6.0 o successivo (il codice funziona anche con .NET Core e .NET Framework).  
2. Una GPU NVIDIA con supporto CUDA (l’esempio utilizza l’indice dispositivo 0).  
3. Il pacchetto NuGet Aspose.OCR e le sue estensioni GPU (`Aspose.OCR.Extensions`).  
4. Un PNG di esempio (`input.png`) posizionato in una cartella a cui il progetto può fare riferimento.  

Se qualcuno di questi punti ti è sconosciuto, non preoccuparti—indicheremo alternative dove necessario.

---

## Passo 1 – Installare Aspose OCR e le estensioni GPU

Prima di tutto. Senza le librerie corrette il resto del codice non compila.

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Extensions
```

Il pacchetto `Aspose.OCR.Extensions` include i binari CUDA nativi necessari per l’accelerazione GPU.  
*Consiglio:* Se lavori su una macchina senza GPU, puoi comunque compilare il progetto; basta impostare `PreferGpu = false` più avanti.

---

## Passo 2 – Caricare il PNG da elaborare

Ora **eseguiamo OCR su PNG** caricandolo in un `Bitmap`. Questo passaggio è semplice ma merita una nota rapida: `Bitmap` si aspetta un percorso file, quindi assicurati che il percorso sia corretto rispetto all’eseguibile.

```csharp
using System.Drawing;        // Bitmap handling
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

// ...

// Step 2: Load the PNG image
string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "YOUR_DIRECTORY", "input.png");
Bitmap imageBitmap = new Bitmap(imagePath);
```

Se il PNG è insolitamente grande (ad esempio > 5000 px per lato), potresti voler ridimensionarlo prima per evitare di esaurire la memoria GPU. È qui che l’opzione **impostare il limite di memoria GPU** diventa utile più avanti.

---

## Passo 3 – Creare e configurare il motore OCR per l’uso della GPU

Ecco il cuore del tutorial: configurare il motore OCR per **riconoscere testo da immagine** usando la GPU. Due proprietà sono fondamentali:

- `GpuDevice` – seleziona quale dispositivo CUDA utilizzare.  
- `GpuMemoryLimitMb` – imposta il limite di memoria GPU che il motore può allocare.

```csharp
// Step 3: Initialize OCR engine with GPU settings
OcrEngine ocrEngine = new OcrEngine()
{
    // Pick the first CUDA device (index 0)
    GpuDevice = GpuDeviceInfo.GetDevice(0),

    // Optional: limit GPU memory consumption (in MB)
    GpuMemoryLimitMb = 2048   // Adjust based on your GPU's VRAM
};
```

**Perché impostare un limite di memoria?** Alcune GPU condividono la memoria con il display o eseguono più carichi di lavoro contemporaneamente. Limitando l’allocazione eviti crash per out‑of‑memory, soprattutto quando elabori molti PNG in parallelo.

---

## Passo 4 – Definire le opzioni di riconoscimento (lingua e preferenza GPU)

L’oggetto `RecognitionOptions` indica al motore quale lingua cercare e se **preferire la GPU** anche per immagini piccole. Per la maggior parte dei documenti in inglese è sufficiente, ma puoi sostituire `Language.English` con altre locale supportate.

```csharp
// Step 4: Set recognition options
RecognitionOptions recognitionOptions = new RecognitionOptions
{
    Language = Language.English,
    PreferGpu = true // Force GPU path even for smaller images
};
```

Se devi **estrarre testo da immagine** in una lingua diversa dall’inglese, cambia semplicemente l’enum `Language`. La libreria supporta decine di lingue pronte all’uso.

---

## Passo 5 – Eseguire l’OCR e recuperare il risultato

Con tutto collegato, la chiamata finale è una singola riga che effettivamente **esegue OCR su PNG** e restituisce un ricco oggetto risultato.

```csharp
// Step 5: Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

// Output the extracted text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

L’`OcrResult` contiene non solo il plain text (`ocrResult.Text`) ma anche punteggi di confidenza, bounding box e persino l’immagine originale con le parole evidenziate—utile se devi fare debug o visualizzare l’estrazione.

**Output previsto** (per un PNG di esempio che dice “Hello World”):

```
=== OCR Output ===
Hello World
```

Se il testo appare distorto, verifica che il PNG non sia corrotto e che il limite di memoria GPU non sia troppo basso per le dimensioni dell’immagine.

---

## Passo 6 – Gestire casi particolari e consigli di best‑practice

### GPU a bassa memoria

Se ricevi un’eccezione come `CudaException: out of memory`, riduci `GpuMemoryLimitMb` o suddividi il PNG in tasselli prima dell’elaborazione. Il tiling può essere fatto con `Graphics.DrawImage` su una copia di `Bitmap`.

### Più PNG in batch

Quando elabori una cartella di PNG, riutilizza la stessa istanza di `OcrEngine`—inizializzarla una sola volta riduce i cambi di contesto GPU.

```csharp
foreach (var file in Directory.GetFiles("images", "*.png"))
{
    using var bmp = new Bitmap(file);
    var result = ocrEngine.Recognize(bmp, recognitionOptions);
    Console.WriteLine($"{Path.GetFileName(file)}: {result.Text}");
}
```

### Fallback alla CPU

Se non è disponibile una GPU, imposta semplicemente `PreferGpu = false`. Il motore tornerà automaticamente alla CPU senza modifiche al codice.

```csharp
recognitionOptions.PreferGpu = false; // Safe CPU path
```

---

## Esempio completo funzionante

Di seguito trovi il programma completo da copiare‑incollare in un nuovo progetto console. Include tutti i passaggi sopra, più alcuni controlli di sicurezza.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

class GpuExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the PNG image
        // -------------------------------------------------
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory,
                                         "YOUR_DIRECTORY", "input.png");

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"File not found: {imagePath}");
            return;
        }

        using Bitmap imageBitmap = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2: Initialize OCR engine with GPU settings
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine()
        {
            GpuDevice = GpuDeviceInfo.GetDevice(0), // First CUDA device
            GpuMemoryLimitMb = 2048                  // Adjust as needed
        };

        // -------------------------------------------------
        // Step 3: Set recognition options
        // -------------------------------------------------
        RecognitionOptions recognitionOptions = new RecognitionOptions
        {
            Language = Language.English,
            PreferGpu = true // Force GPU even for small images
        };

        // -------------------------------------------------
        // Step 4: Perform OCR
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

        // -------------------------------------------------
        // Step 5: Output the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Salva il file come `Program.cs`, esegui `dotnet run` e dovresti vedere il testo estratto stampato sulla console.

---

## Conclusione

Abbiamo appena dimostrato come **eseguire OCR su PNG** usando le estensioni GPU di Aspose OCR, come **riconoscere testo da immagine** e come **estrarre testo da immagine** controllando il **limite di memoria GPU**. Configurando `GpuDevice` e `GpuMemoryLimitMb` mantieni la tua applicazione veloce e stabile, anche su GPU modeste.

Da qui potresti:

- Sperimentare con altre lingue (`Language.French`, `Language.Spanish`).  
- Integrare il passo OCR in una pipeline di elaborazione documenti più ampia.  
- Aggiungere post‑processing come spell‑checking o estrazione di entità per rifinire il testo grezzo.  

Ricorda, la chiave non è solo il codice ma capire perché ogni impostazione è importante. Quando sai come **impostare il limite di memoria GPU** e quando ricorrere alla CPU, costruirai soluzioni OCR che scalano con eleganza.

Hai domande su una dimensione PNG specifica, TIFF multi‑pagina o errori GPU? Lascia un commento qui sotto, e buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}