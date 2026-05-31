---
category: general
date: 2026-05-31
description: Impara a riconoscere il testo dalle immagini in C# con Aspose OCR, incluso
  come estrarre il testo dai file TIFF e caricare l'immagine per l'OCR in modo efficiente.
draft: false
keywords:
- recognize text from image
- extract text from tiff
- load image for OCR
- Aspose OCR C#
- GPU accelerated OCR
language: it
og_description: Guida passo passo per riconoscere il testo da un'immagine con Aspose
  OCR, che copre l'estrazione da file TIFF e il corretto caricamento dell'immagine
  per l'OCR.
og_title: Riconosci il testo da un'immagine in C# usando Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to recognize text from image in C# with Aspose OCR, including
    how to extract text from tiff files and load image for OCR efficiently.
  headline: recognize text from image in C# using Aspose OCR
  type: TechArticle
- questions:
  - answer: Reduce its resolution before feeding it to the engine, or increase `GpuMemoryLimit`
      if you have enough VRAM.
    question: What if the image is huge (over 10 MB)?
  - answer: Absolutely. Just reuse the same `OcrEngine` instance and assign a new
      `ImageStream` each iteration.
    question: Can I process multiple images in a loop?
  - answer: '`OcrEngine` implements `IDisposable`. Wrap it in a `using` block for
      clean resource management, especially when working with GPU resources.'
    question: Do I need to dispose of anything?
  - answer: Set `engine.Language = OcrLanguage.Spanish` (or any supported language)
      before calling `Recognize()`.
    question: What about languages other than English?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
title: Riconoscere il testo da un'immagine in C# usando Aspose OCR
url: /it/net/text-recognition/recognize-text-from-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# riconoscere testo da immagine in C# usando Aspose OCR

Ti è mai capitato di dover **recognize text from image** ma non sapevi da dove cominciare in C#? Non sei solo—molti sviluppatori si trovano di fronte a questo ostacolo quando lavorano con documenti scansionati o TIFF multi‑pagina. In questa guida ti accompagneremo passo passo con un esempio completo, pronto‑all'uso, che **recognize text from image** usando la libreria Aspose OCR, e ti mostreremo anche come **extract text from tiff** e il modo migliore per **load image for OCR** senza impazzire.

Copriamo tutto, dall'installazione del pacchetto NuGet alla gestione dell'accelerazione GPU e al fallback sulla CPU quando necessario. Alla fine di questo tutorial avrai un'app console che stampa il testo riconosciuto e il tempo di elaborazione—senza parti mancanti, senza riferimenti vaghi.

## Cosa Costruirai

- Una semplice applicazione console .NET che carica un'immagine (inclusi TIFF multi‑pagina)  
- Un motore OCR configurato per l'uso della GPU, con fallback elegante alla CPU  
- Estrazione del testo semplice dall'immagine, stampato sulla console  
- Informazioni sul tempo di esecuzione così da poter vedere l'impatto delle prestazioni GPU vs CPU  

**Prerequisiti**

- .NET 6 SDK o successivo (il codice funziona con .NET Core e .NET Framework)  
- Familiarità di base con C# e la riga di comando  
- Accesso a Internet per scaricare il pacchetto NuGet Aspose.OCR  

Se li hai, immergiamoci.

![Codice C# per riconoscere testo da immagine usando Aspose OCR](image.png "Codice C# per riconoscere testo da immagine usando Aspose OCR")

## Passo 1 – Recognize text from image: Configura il motore OCR

Prima di tutto, ci serve un'istanza di `OcrEngine`. Aspose OCR ti permette di scegliere il dispositivo di elaborazione—GPU per la velocità, CPU come rete di sicurezza. Il motore accetta anche un suggerimento di limite di memoria, utile su macchine condivise.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Create the OCR engine and request GPU acceleration.
        // If no compatible GPU is found, Aspose silently falls back to CPU.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,      // Try GPU first
            GpuMemoryLimit = 1024        // Optional: cap GPU memory usage (MB)
        };
```

**Perché è importante:**  
Scegliere `OcrDevice.Gpu` può ridurre di alcuni secondi il tempo di riconoscimento per immagini grandi, specialmente TIFF multi‑pagina. `GpuMemoryLimit` impedisce alla tua app di monopolizzare tutta la memoria GPU su una workstation condivisa.

## Passo 2 – Load image for OCR (incluso il supporto TIFF)

Ora forniamo al motore un'immagine. `ImageStream.FromFile` di Aspose accetta **qualsiasi** formato supportato dalla libreria—TIFF, PNG, JPEG, quello che vuoi. Questo passaggio soddisfa direttamente il requisito **load image for OCR**.

```csharp
        // Load the image you want to process.
        // Replace the path with the actual location of your TIFF or other image.
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");
```

**Suggerimento:** Se lavori con un TIFF multi‑pagina, Aspose tratta automaticamente ogni pagina come un frame separato, e il motore le elaborerà sequenzialmente. Nessun codice aggiuntivo necessario.

## Passo 3 – Run the recognition and **extract text from tiff**

Con il motore pronto e l'immagine caricata, avviamo l'operazione OCR. Il metodo `Recognize` restituisce un `OcrResult` che contiene il testo semplice, i punteggi di confidenza e i dettagli temporali.

```csharp
        // Perform the OCR operation.
        OcrResult result = engine.Recognize();
```

**Gestione dei casi limite:**  
Se la GPU non è disponibile, `engine.Recognize()` funziona comunque perché il motore passa silenziosamente alla CPU. Puoi controllare `engine.Device` dopo il riconoscimento se devi registrare quale dispositivo è stato effettivamente usato.

## Passo 4 – Recupera il testo semplice riconosciuto

Estrarre il testo è semplice—basta leggere la proprietà `Text`. Qui è dove finalmente **extract text from tiff** (o qualsiasi altra immagine) e lo presentiamo all'utente.

```csharp
        // Output the plain text that was extracted.
        Console.WriteLine($"Text:\n{result.Text}");
```

Vedrai i caratteri grezzi, con le interruzioni di riga preservate così come appaiono nell'immagine di origine. Per un output più strutturato (come JSON o CSV), puoi approfondire `result.Regions` e `result.Lines`, ma il testo semplice è di solito sufficiente per script veloci.

## Passo 5 – Misura il tempo di elaborazione e gestisci il fallback GPU

Le prestazioni sono importanti, soprattutto quando elabori decine di pagine. La proprietà `ProcessingTime` ti indica esattamente quanto tempo ha impiegato l'OCR, indipendentemente dal fatto che sia stato eseguito su GPU o CPU.

```csharp
        // Show how long the recognition took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**Perché dovresti interessartene:**  
Se noti che il tempo aumenta notevolmente, potresti voler regolare `GpuMemoryLimit` o passare esplicitamente alla CPU (`Device = OcrDevice.Cpu`). Al contrario, un risultato inferiore al secondo su un TIFF grande indica che l'accelerazione GPU sta facendo il suo lavoro.

## Esempio completo, pronto‑all'uso

Copia il codice qui sotto in un nuovo progetto console (`dotnet new console -n OcrDemo`) ed esegui `dotnet add package Aspose.OCR`. Poi sostituisci `YOUR_DIRECTORY/sample_multi_page.tif` con il percorso della tua immagine.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine with GPU preference.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,
            GpuMemoryLimit = 1024
        };

        // Step 2: Load image for OCR (supports TIFF, PNG, JPEG, etc.).
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");

        // Step 3: Run recognition – this will also **extract text from tiff**.
        OcrResult result = engine.Recognize();

        // Step 4: Retrieve and display the recognized plain text.
        Console.WriteLine($"Text:\n{result.Text}");

        // Step 5: Display how long the operation took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**Output previsto (troncato per brevità):**

```
Text:
Invoice #12345
Date: 2026-05-01
Total: $1,250.00
...
Time elapsed: 1.42s
```

Se la tua macchina non dispone di una GPU adeguata, il tempo trascorso potrebbe essere qualche secondo più lungo, ma il testo verrà comunque estratto correttamente.

## Domande comuni e insidie

- **E se l'immagine è enorme (oltre 10 MB)?**  
  Riduci la sua risoluzione prima di passarla al motore, oppure aumenta `GpuMemoryLimit` se hai abbastanza VRAM.  
- **Posso elaborare più immagini in un ciclo?**  
  Assolutamente. Riutilizza la stessa istanza di `OcrEngine` e assegna un nuovo `ImageStream` a ogni iterazione.  
- **Devo liberare qualche risorsa?**  
  `OcrEngine` implementa `IDisposable`. Avvolgilo in un blocco `using` per una gestione pulita delle risorse, specialmente quando lavori con risorse GPU.  

```csharp
using (OcrEngine engine = new OcrEngine { Device = OcrDevice.Gpu })
{
    // ... same steps as before
}
```

- **E per le lingue diverse dall'inglese?**  
  Imposta `engine.Language = OcrLanguage.Spanish` (o qualsiasi lingua supportata) prima di chiamare `Recognize()`.

## Conclusione

Ora disponi di una soluzione completa, end‑to‑end, che **recognize text from image** in C# usando Aspose OCR. Il tutorial ha coperto come **load image for OCR**, come **extract text from tiff**, e come misurare le prestazioni gestendo elegantemente il fallback GPU.

Da qui potresti:

- Sperimentare con diversi formati immagine (BMP, PDF) per vedere come li gestisce Aspose.  
- Approfondire `result.Regions` per i dati delle bounding‑box se ti serve la consapevolezza del layout

## Cosa dovresti imparare dopo?

- [Come usare Aspose per riconoscere l'immagine dallo stream in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Estrarre testo da immagine – Ottimizzazione OCR con Aspose.OCR per .NET](/ocr/english/net/ocr-optimization/)
- [Estrarre testo da immagine – Riconoscere la linea con Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}