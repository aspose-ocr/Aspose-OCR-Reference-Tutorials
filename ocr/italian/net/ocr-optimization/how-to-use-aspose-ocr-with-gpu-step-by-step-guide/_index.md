---
category: general
date: 2026-02-09
description: Come usare Aspose OCR con accelerazione GPU in C#. Impara a riconoscere
  il testo da JPG, estrarre il testo dall'immagine e abilitare la GPU in pochi minuti.
draft: false
keywords:
- how to use aspose
- recognize text from jpg
- extract text from image
- how to enable gpu
- how to set gpu
language: it
og_description: Come utilizzare Aspose OCR con GPU in C#. Questa guida ti mostra come
  riconoscere il testo da un JPG ed estrarre il testo dall'immagine usando l'accelerazione
  GPU.
og_title: Come utilizzare Aspose OCR con GPU – Guida completa alla programmazione
tags:
- Aspose
- OCR
- C#
- GPU Acceleration
title: Come utilizzare Aspose OCR con GPU – Guida passo passo
url: /it/net/ocr-optimization/how-to-use-aspose-ocr-with-gpu-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come utilizzare Aspose OCR con GPU – Guida completa di programmazione

Ti è mai capitato di dover elaborare una pila di fatture scannerizzate in un lampo, ma la CPU continuava a impantanarsi? È un classico punto dolente quando si cerca di **how to use aspose** per OCR su larga scala. In questo tutorial ti guideremo attraverso un esempio reale che mostra **how to use aspose** per riconoscere testo da file jpg, estrarre testo dall’immagine e sfruttare al massimo la tua GPU.

Pensalo come una dimostrazione da pausa caffè—senza fronzoli, solo i passaggi che puoi copiare‑incollare in Visual Studio e vedere la magia accadere. Alla fine avrai un’app console C# autonoma che gira su qualsiasi PC Windows moderno con GPU NVIDIA o AMD.

![how to use aspose OCR with GPU](/images/aspose-gpu-example.png)

## Cosa ti servirà

- **.NET 6.0** (o versioni successive) – il codice è destinato a .NET 6 ma funziona con .NET 5 e .NET Framework 4.8 con piccole modifiche.  
- **Aspose.OCR for .NET** pacchetto NuGet – installalo con `dotnet add package Aspose.OCR`.  
- Una **macchina con GPU** – il tutorial mostra come **how to enable gpu** e **how to set gpu** i limiti di memoria, ma il codice tornerà automaticamente alla CPU se non viene trovata una GPU compatibile.  
- Un’immagine come `invoice_01.jpg` posizionata in una cartella a cui puoi fare riferimento.

Li hai? Ottimo, immergiamoci.

## Come utilizzare Aspose OCR con GPU – Configurazione iniziale

La prima cosa da fare è creare un’istanza del motore OCR e indicargli di usare la GPU. Questo passaggio è cruciale perché senza il flag, Aspose utilizzerà la CPU per impostazione predefinita, vanificando lo scopo del nostro boost di prestazioni.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

// Step 1: Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Enable GPU acceleration – this is the core of **how to use aspose** with a graphics card
ocrEngine.Configuration.UseGpu = true;

// Optional: limit GPU memory to avoid OOM on low‑end cards
ocrEngine.Configuration.GpuMemoryLimit = 1024; // in MB
```

**Perché è importante:** Abilitare la GPU sposta i kernel di elaborazione immagine pesanti sul processore grafico, che può essere 10‑20× più veloce della CPU per immagini di grandi dimensioni. `GpuMemoryLimit` è una valvola di sicurezza; impostarla a 1024 MB funziona per la maggior parte delle schede di fascia media mantenendo l’app reattiva.

> **Consiglio esperto:** Se esegui l’app su una macchina senza GPU compatibile, Aspose tornerà automaticamente alla modalità CPU e registrerà un avviso. Nessun crash, solo un’esecuzione più lenta.

## Riconoscere testo da JPG – Caricamento dell’immagine

Ora che il motore è pronto, dobbiamo fornirgli un’immagine. L’esempio utilizza un JPEG perché **recognize text from jpg** è uno scenario comune per fatture, ricevute e passaporti.

```csharp
// Step 2: Load the JPEG image you want to process
// Replace the path with the location of your own image
var inputImage = ImageStream.FromFile(@"C:\OCR\Samples\invoice_01.jpg");

// Verify that the file exists (helps avoid a FileNotFoundException)
if (!System.IO.File.Exists(@"C:\OCR\Samples\invoice_01.jpg"))
{
    Console.WriteLine("Image file not found. Check the path and try again.");
    return;
}
```

**Perché controlliamo il file:** Un file mancante è la causa più frequente di errori a runtime nei demo veloci. Gestendolo subito, il tutorial rimane adatto ai principianti.

## Estrarre testo dall’immagine – Esecuzione del motore OCR

Con l’immagine a disposizione, il passo successivo è avviare effettivamente il processo OCR. Qui Aspose fa il lavoro pesante e restituisce un oggetto `OcrResult` che contiene il testo semplice, i punteggi di confidenza e persino le bounding box se ti servono in seguito.

```csharp
// Step 3: Perform OCR on the loaded image
OcrResult ocrResult = ocrEngine.Recognize(inputImage);

// Step 4: Output the extracted plain‑text
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(ocrResult.PlainText);
```

**Ciò che vedrai:** La console stampa i caratteri grezzi rilevati da Aspose. Per una fattura pulita, potresti ottenere qualcosa del tipo:

```
=== Extracted Text ===
Invoice #: 2023‑00123
Date: 02/08/2023
Total: $1,245.67
...
```

Se l’output appare confuso, probabilmente dovrai migliorare la qualità dell’immagine o abilitare opzioni di pre‑elaborazione aggiuntive (es. deskew, binarizzazione). Queste vanno oltre lo scopo di questa breve guida ma sono documentate nella reference API di Aspose.

## Come abilitare GPU – Configurazione del motore

Ti starai chiedendo **how to enable gpu** per Aspose se ti sei perso il primo passaggio. La risposta è semplicemente attivare il flag `UseGpu` sull’oggetto di configurazione del motore, come mostrato in precedenza. Ecco uno snippet condensato che puoi inserire in qualsiasi progetto esistente:

```csharp
ocrEngine.Configuration.UseGpu = true;   // Enables GPU
```

Dietro le quinte, Aspose carica le librerie native CUDA/OpenCL corrispondenti al tuo hardware. Se il runtime non riesce a trovarle, registra un avviso e torna alla CPU. Non sono richiesti passaggi di installazione aggiuntivi per la maggior parte delle configurazioni Windows.

## Come impostare GPU – Ottimizzazione dell’uso della memoria

A volte si verifica un errore “out of memory” su una GPU di fascia bassa. È qui che **how to set gpu** i limiti di memoria risultano utili. La proprietà `GpuMemoryLimit` accetta un intero che rappresenta i megabyte.

```csharp
// Example: restrict GPU usage to 512 MB
ocrEngine.Configuration.GpuMemoryLimit = 512;
```

**Quando regolare:** Se elabori molte immagini in parallelo, abbassa il limite per evitare che la scheda si saturi. Al contrario, su una workstation con 8 GB di VRAM puoi aumentarlo tranquillamente a 4096 MB per una più rapida elaborazione batch.

## Esempio completo, eseguibile

Di seguito trovi il programma completo che puoi copiare in un nuovo progetto console (`dotnet new console`). Include tutti i pezzi discussi, più una piccola gestione degli errori per renderlo robusto.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

class GpuExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Create the OCR engine and enable GPU
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.Configuration.UseGpu = true;            // how to enable gpu
        ocrEngine.Configuration.GpuMemoryLimit = 1024;   // how to set gpu

        // -------------------------------------------------
        // Step 2: Load the JPEG image you want to process
        // -------------------------------------------------
        string imagePath = @"C:\OCR\Samples\invoice_01.jpg";

        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"File not found: {imagePath}");
            return;
        }

        var inputImage = ImageStream.FromFile(imagePath);

        // -------------------------------------------------
        // Step 3: Run the OCR engine
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(inputImage);

        // -------------------------------------------------
        // Step 4: Display the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.PlainText);
    }
}
```

**Output previsto:** Dopo aver eseguito `dotnet run`, la console stamperà il testo grezzo estratto da `invoice_01.jpg`. Se l’immagine contiene testo stampato chiaramente, il risultato sarà quasi identico al documento originale.

## Problemi comuni e come evitarli

| Problema | Perché accade | Soluzione rapida |
|----------|----------------|------------------|
| **GPU non rilevata** | Driver CUDA mancanti o GPU non supportata | Installa l’ultimo driver NVIDIA/AMD; verifica con `nvidia-smi` o equivalente |
| **Errore out‑of‑memory** | `GpuMemoryLimit` troppo alto per la scheda | Riduci il limite a 512 MB o meno |
| **Output incomprensibile** | JPG a bassa risoluzione o compressione eccessiva | Usa un’immagine sorgente di qualità superiore o abilita `ocrEngine.Preprocessing.Deskew = true` |
| **`ocrResult` nullo** | Impossibile caricare lo stream dell’immagine | Controlla il percorso del file e assicurati che non sia bloccato |

Affrontare questi aspetti in anticipo ti salva da tracciati di stack criptici in seguito.

## Prossimi passi

Ora che hai padroneggiato **how to use aspose** per OCR veloce, potresti voler esplorare:

- **Elaborazione batch** – cicla su una cartella di JPG e scrivi ogni risultato in un file `.txt`.  
- **Estrazione strutturata** – usa `ocrResult.Regions` per ottenere le bounding box e ricavare campi specifici come i numeri di fattura.  
- **Modalità ibrida CPU/GPU** – usa la CPU per immagini piccole e passa alla GPU solo per file grandi, bilanciando velocità e memoria.

Tutte queste estensioni si basano sulla stessa fondazione che hai appena impostato, e sono argomenti perfetti per la tua prossima avventura tutorial.

---

*Buona programmazione! Se incontri difficoltà, lascia un commento qui sotto o contatta i forum della community Aspose. La GPU è pronta—rendiamo l’OCR fulmineo.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}