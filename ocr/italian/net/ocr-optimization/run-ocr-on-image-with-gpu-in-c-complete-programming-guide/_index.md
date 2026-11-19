---
category: general
date: 2026-03-26
description: Esegui OCR su un'immagine usando il supporto GPU di Aspose OCR in C#.
  Scopri come caricare l'immagine per l'OCR, impostare l'ID del dispositivo GPU e
  estrarre rapidamente il testo dall'immagine.
draft: false
keywords:
- run OCR on image
- extract text from image
- load image for OCR
- recognize text from document
- set GPU device ID
language: it
og_description: Esegui OCR su un'immagine usando Aspose OCR GPU in C#. Questa guida
  mostra come caricare l'immagine per l'OCR, impostare l'ID del dispositivo GPU e
  estrarre il testo dall'immagine in modo efficiente.
og_title: Esegui OCR su immagine con GPU in C# – Guida completa
tags:
- C#
- OCR
- GPU
- Aspose
title: Esegui OCR su immagine con GPU in C# – Guida completa alla programmazione
url: /it/net/ocr-optimization/run-ocr-on-image-with-gpu-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esegui OCR su Immagine con GPU in C# – Guida Completa di Programmazione

Hai mai avuto bisogno di **run OCR on image** ma hai trovato la versione CPU dolorosamente lenta? Non sei solo. In molte app reali—pensa a scanner di fatture o archivi di documenti su larga scala—il collo di bottiglia è il motore OCR stesso.  

In questo tutorial percorreremo un **complete, runnable example** che mostra come **load image for OCR**, opzionalmente **set GPU device ID**, e infine **extract text from image** usando l'API GPU‑accelerated di Aspose OCR. Alla fine sarai in grado di **recognize text from document** immagini in una frazione del tempo che richiederebbe un approccio puro‑CPU.

## Cosa Imparerai

- Come installare e referenziare i pacchetti Aspose.OCR e Aspose.OCR.Gpu.  
- I passaggi esatti per **run OCR on image** con accelerazione GPU.  
- Perché selezionare il corretto **GPU device ID** è importante su macchine multi‑GPU.  
- Suggerimenti per gestire file di grandi dimensioni, strategie di fallback e problemi comuni.  

### Prerequisiti

| Requisito | Motivo |
|-------------|--------|
| .NET 6.0 o successivo | Funzionalità del linguaggio moderne e migliori prestazioni |
| Visual Studio 2022 (o qualsiasi IDE C#) | Per una facile configurazione del progetto |
| GPU NVIDIA con supporto CUDA (opzionale) | Necessario solo se desideri l'accelerazione GPU |
| Pacchetti NuGet Aspose.OCR & Aspose.OCR.Gpu | Fornisce la classe `GpuOcrEngine` |

Se non hai una GPU, non preoccuparti—il codice ricade elegantemente sul motore CPU, che tratteremo più avanti.

---

## Passo 1: Installa i Pacchetti Aspose OCR

Prima di poter **run OCR on image**, hai bisogno delle librerie. Apri il tuo terminale (o la Console del Package Manager) ed esegui:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

Questi due pacchetti includono il motore OCR core e le estensioni specifiche per GPU. Dopo l'installazione, vedrai i seguenti riferimenti nel tuo `.csproj`:

```xml
<ItemGroup>
  <PackageReference Include="Aspose.OCR" Version="23.10.0" />
  <PackageReference Include="Aspose.OCR.Gpu" Version="23.10.0" />
</ItemGroup>
```

> **Pro tip:** Mantieni le versioni dei pacchetti sincronizzate; versioni non corrispondenti possono causare errori a runtime.

---

## Passo 2: Crea un Motore OCR Abilitato alla GPU

Ora che le librerie sono al loro posto, facciamo **run OCR on image** usando la GPU. La classe `GpuOcrEngine` è il punto di ingresso per l'elaborazione accelerata.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // Namespace for GPU support

class GpuExample
{
    static void Main()
    {
        // Step 2.1: Instantiate the GPU OCR engine
        var gpuEngine = new GpuOcrEngine();

        // Step 2.2 (optional): Choose which GPU to use – 0 = first GPU
        // This is where the "set GPU device ID" keyword comes into play.
        gpuEngine.DeviceId = 0;

        // The rest of the workflow continues in the following steps...
```

**Perché una GPU?**  
I core della GPU eccellono nelle operazioni pixel in parallelo, che è esattamente ciò di cui l'OCR ha bisogno quando scansiona immagini ad alta risoluzione. Impostando `DeviceId`, indichi alla libreria quale scheda fisica usare—utile su workstation con più GPU.

---

## Passo 3: Carica l'Immagine per l'OCR

Prima del riconoscimento, devi **load image for OCR**. Aspose fornisce un comodo metodo statico factory che supporta molti formati (JPEG, PNG, TIFF, ecc.).

```csharp
        // Step 3: Load the image you want to recognize
        // Replace the path with your actual file location.
        var ocrImage = OcrImage.FromFile(@"C:\Images\large_document.jpg");

        // Quick sanity check – ensure the image was loaded.
        if (ocrImage == null)
        {
            Console.WriteLine("Failed to load image. Check the file path.");
            return;
        }
```

> **Caso limite:** Se l'immagine è più grande di 10 MB, considera di ridimensionarla prima per evitare l'esaurimento della memoria GPU. Puoi farlo con `ocrImage.Resize(width, height)` prima del riconoscimento.

---

## Passo 4: Riconosci Testo dal Documento

Con il motore pronto e l'immagine caricata, è il momento di **recognize text from document**. Il metodo `Recognize` restituisce un oggetto `OcrResult` contenente l'output di testo semplice e metadati aggiuntivi.

```csharp
        // Step 4: Run the OCR process on the image
        OcrResult ocrResult = gpuEngine.Recognize(ocrImage);

        // Verify that OCR succeeded
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("OCR failed or returned empty result.");
            return;
        }
```

**Cosa succede dietro le quinte?**  
Il motore GPU invia i dati pixel ai kernel CUDA, che eseguono binarizzazione, segmentazione dei caratteri e inferenza di rete neurale—tutto in parallelo. Questo è il motivo per cui puoi **run OCR on image** file che altrimenti richiederebbero secondi sulla CPU.

---

## Passo 5: Estrai Testo dall'Immagine e Output

Infine, **extract text from image** e lo visualizziamo. Puoi anche scrivere il risultato su un file, un database, o alimentarlo in pipeline NLP successive.

```csharp
        // Step 5: Output the recognized plain‑text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);

        // Optional: Save to a .txt file for later processing
        System.IO.File.WriteAllText(@"C:\Output\ocr_result.txt", ocrResult.Text);
    }
}
```

**Output previsto** (troncato per brevità):

```
=== OCR Result ===
Invoice #12345
Date: 03/15/2026
Total: $1,234.56
...
```

Se esegui il programma e vedi un blocco simile, congratulazioni—hai eseguito con successo **run OCR on image** usando l'accelerazione GPU!

---

## Gestione delle Situazioni Senza GPU (Fallback)

E se la macchina su cui distribuisci non ha una GPU compatibile? Il costruttore `GpuOcrEngine` lancerà una `GpuNotSupportedException`. Avvolgi l'inizializzazione in un try‑catch e ricadi su `OcrEngine` (CPU) così:

```csharp
        try
        {
            var gpuEngine = new GpuOcrEngine { DeviceId = 0 };
            // Continue with GPU workflow...
        }
        catch (GpuNotSupportedException)
        {
            Console.WriteLine("GPU not available – switching to CPU OCR.");
            var cpuEngine = new OcrEngine();
            OcrResult result = cpuEngine.Recognize(ocrImage);
            Console.WriteLine(result.Text);
        }
```

Questo schema garantisce che la tua app rimanga funzionale indipendentemente dall'hardware, una considerazione cruciale per le distribuzioni cloud.

---

## Esempio Completo Funzionante (Pronto per Copia‑Incolla)

Di seguito trovi il **entire program**—senza parti mancanti, basta sostituire i percorsi dei file con i tuoi.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // Namespace for GPU support

class GpuExample
{
    static void Main()
    {
        // 1️⃣ Create a GPU‑enabled OCR engine
        GpuOcrEngine gpuEngine;
        try
        {
            gpuEngine = new GpuOcrEngine { DeviceId = 0 }; // set GPU device ID
        }
        catch (GpuNotSupportedException)
        {
            Console.WriteLine("GPU not detected. Falling back to CPU engine.");
            var cpuEngine = new OcrEngine();
            RunCpuOcr(cpuEngine);
            return;
        }

        // 2️⃣ Load image for OCR
        var ocrImage = OcrImage.FromFile(@"C:\Images\large_document.jpg");
        if (ocrImage == null)
        {
            Console.WriteLine("Unable to load image – check the path.");
            return;
        }

        // 3️⃣ Recognize text from document
        OcrResult ocrResult = gpuEngine.Recognize(ocrImage);
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("OCR returned no text.");
            return;
        }

        // 4️⃣ Extract text from image and output
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
        System.IO.File.WriteAllText(@"C:\Output\ocr_result.txt", ocrResult.Text);
    }

    // Helper for CPU fallback
    static void RunCpuOcr(OcrEngine cpuEngine)
    {
        var img = OcrImage.FromFile(@"C:\Images\large_document.jpg");
        var result = cpuEngine.Recognize(img);
        Console.WriteLine("=== CPU OCR Result ===");
        Console.WriteLine(result.Text);
    }
}
```

> **Nota:** Il codice sopra estrae automaticamente **extract text from image** e lo scrive in `ocr_result.txt`. Regola i percorsi secondo necessità.

---

## Domande Frequenti & Suggerimenti

| Domanda | Risposta |
|----------|--------|
| *Devo avere un driver NVIDIA specifico?* | Sì—si consiglia CUDA 11.x o versioni più recenti. Controlla le note di rilascio di Aspose per la compatibilità esatta. |
| *Posso elaborare più immagini contemporaneamente?* | Assolutamente. Avvolgi la chiamata OCR in un ciclo `Parallel.ForEach`, ma fai attenzione ai limiti di memoria GPU. |
| *E se il risultato OCR contiene caratteri illeggibili?* | Prova a modificare la pre‑elaborazione dell'immagine: `ocrImage.Binarize()` o `ocrImage.Deskew()` prima del riconoscimento. |
| *C’è un modo per limitare il modello linguistico?* | Imposta `gpuEngine.Language = OcrLanguage.English;` per velocizzare l'elaborazione se ti serve solo l'inglese. |

---

## Conclusione

Ora hai una **complete, end‑to‑end solution** per **run OCR on image**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}