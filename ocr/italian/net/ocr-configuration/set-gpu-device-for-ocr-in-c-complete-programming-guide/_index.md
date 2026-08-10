---
category: general
date: 2026-03-18
description: Imposta il dispositivo GPU in Aspose OCR per estrarre rapidamente il
  testo dall'immagine. Scopri come caricare l'immagine per l'OCR, riconoscere l'immagine
  di una ricevuta e ottenere risultati accurati.
draft: false
keywords:
- set GPU device
- extract text from image
- how to extract text
- load image for OCR
- recognize receipt image
language: it
og_description: Imposta il dispositivo GPU in Aspose OCR per estrarre rapidamente
  il testo dall'immagine. Segui questa guida passo‑passo per caricare l'immagine per
  l'OCR e riconoscere l'immagine della ricevuta.
og_title: Imposta il dispositivo GPU per OCR in C# – Guida completa alla programmazione
tags:
- OCR
- C#
- GPU
- Aspose
title: Imposta il dispositivo GPU per OCR in C# – Guida completa alla programmazione
url: /it/net/ocr-configuration/set-gpu-device-for-ocr-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Imposta il dispositivo GPU per OCR in C# – Guida completa di programmazione

Hai bisogno di **impostare il dispositivo GPU** per una più rapida elaborazione OCR? In questa guida ti mostreremo passo passo come impostare il dispositivo GPU usando Aspose OCR, quindi estrarre il testo da un’immagine di una ricevuta in poche righe di codice.  

Se hai mai faticato a **caricare l’immagine per OCR** o ti sei chiesto *come estrarre testo* da scansioni ad alta risoluzione, sei nel posto giusto. Alla fine avrai un programma eseguibile che riconosce l’immagine di una ricevuta, stampa il testo semplice e torna in modalità CPU in modo elegante se la GPU non è disponibile.

## Cosa copre questo tutorial

Tratteremo tutto ciò che devi sapere:

* Installare il pacchetto NuGet Aspose OCR (l’unica dipendenza esterna).  
* Impostare il dispositivo GPU (`set GPU device`) e, opzionalmente, scegliere un indice GPU diverso.  
* Caricare un file immagine per OCR – sì, include anche il temuto passaggio “carica immagine per OCR” che blocca molti principianti.  
* Eseguire il motore di riconoscimento per **riconoscere l’immagine della ricevuta**.  
* Estrarre la stringa risultante così da poter **estrarre testo dall’immagine** e usarlo nella tua app.  

Niente magie, niente link a documenti nascosti – solo una soluzione completa e autonoma che puoi copiare‑incollare in Visual Studio e farla girare subito.

## Prerequisiti

* .NET 6.0 o successivo (il codice funziona anche su .NET Core e .NET Framework).  
* Una macchina con GPU e i driver appropriati installati – altrimenti la libreria passerà automaticamente alla modalità CPU.  
* Un’immagine di esempio di una ricevuta (ad es., `receipt_highres.png`) posizionata in un percorso a cui puoi fare riferimento con il percorso completo.  

Questo è tutto. Se ti manca il pacchetto NuGet, esegui `dotnet add package Aspose.OCR` nella cartella del progetto.

---

## Passo 1 – Imposta il dispositivo GPU in Aspose OCR

La prima cosa da fare è **impostare il dispositivo GPU** sul motore OCR. Questo indica ad Aspose di delegare il lavoro pesante alla scheda grafica invece che alla CPU.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class GpuDemo
{
    static void Main()
    {
        // Create the OCR engine instance
        var ocrEngine = new OcrEngine();

        // Enable GPU processing – this is where we set the GPU device
        ocrEngine.Settings.ProcessingMode = ProcessingMode.Gpu;

        // (Optional) Choose a specific GPU if you have more than one.
        // The default is device 0, but you can set it to 1, 2, etc.
        ocrEngine.Settings.GpuDeviceId = 0;
```

**Perché è importante:**  
Quando il motore gira in `ProcessingMode.Gpu`, i kernel CUDA sottostanti possono accelerare la segmentazione dei caratteri e l’inferenza della rete neurale in modo notevole. Su una moderna RTX 3080 vedrai i tempi di OCR scendere da secondi a sotto‑secondi per ricevute ad alta risoluzione.

> **Suggerimento:** Se non sei sicuro di quale indice GPU usare, chiama `OcrEngine.GetAvailableGpuDevices()` (disponibile nelle versioni più recenti) e scegli quello con più memoria libera.

---

## Passo 2 – Carica l’immagine per OCR

Ora che il motore è configurato, dobbiamo **caricare l’immagine per OCR**. Aspose fornisce un comodo wrapper `ImageStream` che astrae l’I/O dei file e supporta stream da memoria, rete o disco.

```csharp
        // Load the receipt image you want to recognize
        var imagePath = @"C:\OCR\Samples\receipt_highres.png";
        var imageStream = ImageStream.FromFile(imagePath);
```

**Cosa potrebbe andare storto?**  
Se il percorso del file è errato o l’immagine è corrotta, `FromFile` lancerà una `FileNotFoundException`. Un rapido controllo `File.Exists(imagePath)` prima di creare lo stream ti salva da un crash brutale.

---

## Passo 3 – Riconosci l’immagine della ricevuta

Con l’immagine a disposizione, chiamiamo `Recognize`. Questo è il passaggio che effettivamente **riconosce l’immagine della ricevuta** usando la pipeline accelerata dalla GPU che abbiamo impostato prima.

```csharp
        // Perform OCR – this returns an OcrResult object
        var ocrResult = ocrEngine.Recognize(imageStream);
```

**Dietro le quinte:**  
Il motore prima converte l’immagine in una bitmap in scala di grigi normalizzata, poi esegue un modello di deep‑learning che prevede le probabilità dei caratteri. Poiché siamo su GPU, il modello elabora l’intera bitmap in parallelo, ed è per questo che le grandi ricevute terminano rapidamente.

---

## Passo 4 – Estrai testo dall’immagine e verifica l’output

Infine, estraiamo il risultato in testo semplice dall’`OcrResult` e lo scriviamo sulla console. Questo è il momento in cui **estrai testo dall’immagine** e lo puoi passare alla logica successiva (ad es., parsing delle voci).

```csharp
        // Output the recognized plain text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("==================");
    }
}
```

**Output previsto:**  

```
=== OCR Result ===
Store Name
Date: 03/15/2026
Item A   $12.99
Item B   $5.49
Total    $18.48
==================
```

Se il testo appare distorto, verifica che l’immagine sia ad alta risoluzione e che il driver della GPU sia aggiornato. Puoi anche alternare `ocrEngine.Settings.PreprocessMode` per migliorare il contrasto di ricevute poco illuminate.

---

## Passo 5 – Fallback alla CPU (Gestione dei casi limite)

E se la macchina di destinazione non ha una GPU compatibile? Invece di andare in crash, puoi rilevare la situazione e passare all’elaborazione CPU.

```csharp
        // Detect GPU availability – fallback if needed
        if (!ocrEngine.IsGpuAvailable)
        {
            Console.WriteLine("GPU not detected, falling back to CPU mode.");
            ocrEngine.Settings.ProcessingMode = ProcessingMode.Cpu;
        }
```

**Perché includerlo?**  
Nei pipeline CI o nei container cloud spesso si lavora su server headless senza GPU. Una degradazione elegante garantisce che lo stesso codice funzioni ovunque.

---

## Problemi comuni e consigli pratici

| Problema | Come evitarlo |
|----------|---------------|
| Dimenticare di impostare `ProcessingMode` prima di caricare l’immagine. | Configura sempre il motore per primo (Passo 1). |
| Usare l’indice GPU sbagliato (`GpuDeviceId`). | Interroga i dispositivi disponibili o usa il valore predefinito `0`. |
| Caricare un’immagine a bassa risoluzione, che riduce la precisione OCR. | Puntare ad almeno 300 DPI per le ricevute. |
| Non rilasciare `ImageStream` – provoca blocchi sui file. | Avvolgi lo stream in un blocco `using` o chiama `Dispose()` manualmente. |
| Ignorare il flag `IsGpuAvailable` su macchine senza CUDA. | Aggiungi la logica di fallback dal Passo 5. |

---

## Esempio completo funzionante (pronto da copiare‑incollare)

Di seguito trovi l’intero programma, pronto per la compilazione. Salvalo come `Program.cs`, aggiungi il pacchetto NuGet Aspose OCR e avvialo.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class GpuDemo
{
    static void Main()
    {
        // ---------- Step 1: Set GPU device ----------
        var ocrEngine = new OcrEngine();
        ocrEngine.Settings.ProcessingMode = ProcessingMode.Gpu; // set GPU device
        ocrEngine.Settings.GpuDeviceId = 0; // use the first GPU (change if needed)

        // Optional: fallback if GPU isn't present
        if (!ocrEngine.IsGpuAvailable)
        {
            Console.WriteLine("GPU not detected, switching to CPU.");
            ocrEngine.Settings.ProcessingMode = ProcessingMode.Cpu;
        }

        // ---------- Step 2: Load image for OCR ----------
        var imagePath = @"C:\OCR\Samples\receipt_highres.png";
        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"File not found: {imagePath}");
            return;
        }
        var imageStream = ImageStream.FromFile(imagePath);

        // ---------- Step 3: Recognize receipt image ----------
        var ocrResult = ocrEngine.Recognize(imageStream);

        // ---------- Step 4: Extract text from image ----------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("==================");
    }
}
```

Eseguendo il programma verrà stampato il testo estratto dalla ricevuta sulla console, esattamente come mostrato in precedenza. Ora puoi inoltrare quella stringa a un parser, a un database o a qualsiasi altra logica di business di cui hai bisogno.

---

## Conclusione

Ti abbiamo mostrato come **impostare il dispositivo GPU** in Aspose OCR, **caricare l’immagine per OCR** e **riconoscere l’immagine della ricevuta** così da **estrarre testo dall’immagine** con una velocità impressionante. L’esempio completo e eseguibile dimostra sia il “come” sia il “perché”, fornendoti una solida base per qualsiasi progetto C# OCR che richieda accelerazione GPU.

Pronto per il passo successivo? Prova a sperimentare con:

* Elaborare più immagini in parallelo usando `Parallel.ForEach`.  
* Regolare `ocrEngine.Settings.PreprocessMode` per migliorare i risultati su scansioni a basso contrasto.  
* Esportare l’output OCR in JSON per analisi successive.  

Sentiti libero di lasciare un commento se incontri difficoltà, e buona programmazione!

![Diagramma che mostra come impostare il dispositivo GPU per l'elaborazione OCR](set-gpu-device.png "imposta dispositivo GPU")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}