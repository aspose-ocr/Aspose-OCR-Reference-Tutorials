---
category: general
date: 2026-05-21
description: Aspose OCR GPU ti consente di riconoscere rapidamente le immagini di
  testo. Scopri come caricare un'immagine per l'OCR, estrarre il testo da un TIFF
  e migliorare le prestazioni.
draft: false
keywords:
- aspose ocr gpu
- recognize text image
- ocr tiff image
- load image for ocr
- extract text from tiff
language: it
og_description: Aspose OCR GPU accelera l'estrazione del testo. Questa guida mostra
  come caricare un'immagine per l'OCR, riconoscere il testo nell'immagine ed estrarre
  il testo da un TIFF in modo efficiente.
og_title: Aspose OCR GPU – Riconosci il testo da un'immagine TIFF in C#
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Aspose OCR GPU lets you recognize text image quickly. Learn how to
    load image for OCR, extract text from TIFF and boost performance.
  headline: 'Aspose OCR GPU: Recognize Text Image from TIFF with C#'
  type: TechArticle
- description: Aspose OCR GPU lets you recognize text image quickly. Learn how to
    load image for OCR, extract text from TIFF and boost performance.
  name: 'Aspose OCR GPU: Recognize Text Image from TIFF with C#'
  steps:
  - name: Enables GPU acceleration (optional, with automatic CPU fallback).
    text: Enables GPU acceleration (optional, with automatic CPU fallback).
  - name: Creates an `OcrEngine` configured for English.
    text: Creates an `OcrEngine` configured for English.
  - name: Loads a large **OCR TIFF image** from disk.
    text: Loads a large **OCR TIFF image** from disk.
  - name: Runs the recognition and prints the result.
    text: Runs the recognition and prints the result.
  type: HowTo
tags:
- aspose
- ocr
- csharp
title: 'Aspose OCR GPU: Riconosci l''immagine di testo da TIFF con C#'
url: /it/net/ocr-optimization/aspose-ocr-gpu-recognize-text-image-from-tiff-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR GPU: Riconoscere Immagine di Testo da TIFF con C#

Ti sei mai chiesto come **riconoscere un'immagine di testo** da un enorme file TIFF senza bloccare la tua CPU? Non sei l'unico. In molte pipeline di elaborazione documenti il collo di bottiglia è il passaggio OCR, soprattutto quando si inviano gigabyte di pagine scansionate a un motore standard.  

La buona notizia? **Aspose OCR GPU** può turbo‑caricare il processo, e il campione di codice qui sotto mostra esattamente come **caricare l'immagine per OCR**, **estrarre testo da TIFF**, e tornare indietro in modo elegante se una GPU non è presente. Immergiamoci.

## Cosa Copre Questo Tutorial

Esamineremo un programma C# completo, pronto per il copia‑incolla, che:

1. Abilita l'accelerazione GPU (opzionale, con fallback automatico alla CPU).  
2. Crea un `OcrEngine` configurato per l'inglese.  
3. Carica una grande **immagine OCR TIFF** dal disco.  
4. Esegue il riconoscimento e stampa il risultato.  

Alla fine comprenderai **perché** ogni passaggio è importante, come gestire i casi limite comuni, e avrai un esempio eseguibile che potrai adattare a PDF, TIFF multi‑pagina o persino flussi di telecamere in tempo reale.

> **Prerequisiti** – .NET 6+ (o .NET Framework 4.7+), il pacchetto NuGet Aspose.OCR, e una macchina con GPU abilitata se vuoi vedere l’aumento di velocità. Non è necessario hardware speciale; il codice utilizzerà semplicemente la CPU quando una GPU non viene rilevata.

---

![Aspose OCR GPU processing diagram showing CPU fallback](/images/aspose-ocr-gpu-diagram.png){: .align-center alt="aspose ocr gpu"}

## Passo 1: Abilitare l'Accelerazione GPU (Opzionale)

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // adds GPU support

// Enable GPU if a compatible device is present.
// The call is safe – if no GPU is found Aspose falls back to CPU.
OcrEngine.EnableGpu(true);
```

**Perché è importante:**  
I core GPU eccellono nel massiccio parallelismo richiesto per il pre‑processamento delle immagini (binarizzazione, rimozione del rumore) e l’inferenza delle reti neurali. Attivando `EnableGpu(true)` si dà al motore il via libera per delegare questi compiti. Se la macchina non dispone di una scheda compatibile CUDA, Aspose passa silenziosamente alla CPU, così non si verifica alcun crash.

**Consiglio professionale:**  
Su Windows potresti aver bisogno dell'ultimo driver NVIDIA e del toolkit CUDA installati. Su Linux, assicurati che `nvidia‑driver` e `libcuda.so` siano nel tuo percorso di libreria.

## Passo 2: Creare e Configurare il Motore OCR

```csharp
// Step 2: Instantiate the OCR engine and set the language.
var ocrEngine = new OcrEngine
{
    // English works for most scanned docs; you can pick other languages here.
    Language = OcrLanguage.English
};
```

**Perché è importante:**  
`OcrEngine` è il cuore di **Aspose OCR GPU**. Impostare `Language` indica al modello neurale sottostante quale set di caratteri aspettarsi, migliorando drasticamente l'accuratezza. È inoltre possibile regolare `Resolution`, `PreprocessOptions` o `RecognitionMode` per documenti più difficili.

## Passo 3: Caricare l'Immagine per OCR

```csharp
// Step 3: Load a large TIFF image from disk.
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/large_doc.tif");
```

**Perché è importante:**  
Un TIFF può contenere più pagine, alta risoluzione e compressione lossless—perfetto per scansioni d'archivio ma pesante per la memoria. `ImageStream.FromFile` trasmette il file in streaming, evitando un caricamento completo in memoria per immagini molto grandi.  

**Caso limite:** Se devi elaborare un TIFF multi‑pagina, chiama `ocrEngine.Image = ImageStream.FromFile(path, pageIndex);` all'interno di un ciclo, incrementando `pageIndex` finché `ocrEngine.Image.IsNull` restituisce `true`.

## Passo 4: Eseguire il Riconoscimento

```csharp
// Step 4: Run the OCR process.
ocrEngine.Recognize();
```

**Perché è importante:**  
`Recognize()` esegue tutto il lavoro pesante: pre‑processamento, analisi del layout, segmentazione dei caratteri e infine inferenza della rete neurale. Quando la GPU è attiva, il passo di inferenza viene eseguito sulla GPU, spesso riducendo del 50‑80 % il tempo di elaborazione per TIFF di grandi dimensioni.

## Passo 5: Restituire i Risultati

```csharp
// Step 5: Show how many characters were extracted and how long it took.
Console.WriteLine($"Recognized {ocrEngine.Text.Length} characters in {ocrEngine.ProcessingTime} ms");

// Optional: print the extracted text (be careful with huge strings!)
Console.WriteLine("--- Extracted Text Start ---");
Console.WriteLine(ocrEngine.Text);
Console.WriteLine("--- Extracted Text End ---");
```

**Perché è importante:**  
`ocrEngine.Text` contiene la stringa completamente concatenata dall'immagine, mentre `ProcessingTime` fornisce una rapida metrica per confrontare le esecuzioni CPU vs. GPU. L'output della console è utile per il debug veloce; in produzione probabilmente scriveresti il testo in un database o in un file.

**Output previsto (esempio per una fattura a 2 pagine):**

```
Recognized 1342 characters in 842 ms
--- Extracted Text Start ---
Invoice #12345
Date: 2026‑04‑30
...
Total: $1,234.56
--- Extracted Text End ---
```

Se la GPU non è disponibile, il tempo potrebbe salire a ~1800 ms sullo stesso hardware, dimostrando chiaramente il vantaggio di **aspose ocr gpu**.

---

## Gestire le Trappole Comuni

| Situazione | Cosa Controllare | Come Risolvere |
|-----------|-------------------|------------|
| **GPU non rilevata** | `EnableGpu(true)` passa silenziosamente al fallback, ma potresti pensare che stia ancora usando la GPU. | Controlla `OcrEngine.IsGpuEnabled` dopo la chiamata; registra il risultato. |
| **Out‑of‑memory su TIFF enorme** | Caricare un'immagine di 10 000 × 10 000 pixel può superare la RAM. | Usa `ImageStream.FromFile(path, pageIndex, maxResolution: 300)` per ridurre la risoluzione al caricamento. |
| **Lingua errata** | Il modello inglese su un documento francese produce output confuso. | Imposta `Language = OcrLanguage.French` o abilita la modalità multilingue. |
| **TIFF multi‑pagina** | Viene elaborata solo la prima pagina. | Cicla sulle pagine usando `ImageStream.FromFile(path, pageNumber)`. |

---

## Esempio Completo Funzionante

Di seguito trovi il programma completo che puoi inserire in un'app console. Include la gestione degli errori, il logging dello stato della GPU e un semplice timer per i tuoi benchmark.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // adds GPU support

namespace AsposeOcrGpuDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Enable GPU acceleration (if available)
            OcrEngine.EnableGpu(true);
            Console.WriteLine($"GPU enabled: {OcrEngine.IsGpuEnabled}");

            // 2️⃣ Create the OCR engine and set language
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.English
            };

            // 3️⃣ Load the TIFF image (replace with your actual path)
            string imagePath = @"YOUR_DIRECTORY\large_doc.tif";
            try
            {
                ocrEngine.Image = ImageStream.FromFile(imagePath);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Failed to load image: {ex.Message}");
                return;
            }

            // 4️⃣ Perform recognition
            try
            {
                ocrEngine.Recognize();
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Recognition error: {ex.Message}");
                return;
            }

            // 5️⃣ Output results
            Console.WriteLine($"Recognized {ocrEngine.Text.Length} characters in {ocrEngine.ProcessingTime} ms");
            Console.WriteLine("--- Extracted Text Start ---");
            Console.WriteLine(ocrEngine.Text);
            Console.WriteLine("--- Extracted Text End ---");
        }
    }
}
```

Copia, incolla, premi **F5**, e guarda la console stampare il conteggio dei caratteri e il testo estratto. Sostituisci `OcrLanguage.English` con qualsiasi altra lingua supportata da Aspose se hai bisogno di **riconoscere un'immagine di testo** in spagnolo, tedesco, ecc.

## Riepilogo & Prossimi Passi

Abbiamo appena coperto come **aspose ocr gpu** per **riconoscere un'immagine di testo** da una **immagine OCR TIFF**, come **caricare l'immagine per OCR**, e come **estrarre testo da TIFF** in modo efficiente. Le idee fondamentali—abilitare la GPU, configurare la lingua, fare lo streaming del TIFF e leggere il risultato—sono trasferibili ad altri formati di file come JPEG o PNG.

### Cosa Provare Dopo

- **Elaborazione batch**: Scorri una cartella di TIFF, scrivi ogni `ocrEngine.Text` in un file `.txt`.  
- **Gestione multi‑pagina**: Usa `ImageStream.FromFile(path, pageIndex)` all'interno di un ciclo `while` per elaborare ogni pagina di un documento multi‑pagina.  
- **Pre‑processamento personalizzato**: Regola `ocrEngine.PreprocessOptions` (ad esempio `Denoise`, `Deskew`) per scansioni rumorose.  
- **Benchmark GPU**: Registra `ProcessingTime` con e senza `EnableGpu(true)` sulla stessa macchina per quantificare l'accelerazione.  

Sentiti libero di sperimentare—l'accelerazione GPU brilla soprattutto su TIFF ad alta risoluzione e multi‑pagina, ma anche una modesta 1080 Ti ridurrà drasticamente il tempo di riconoscimento.

Hai domande su un tipo di documento specifico o hai bisogno di aiuto per integrare l'output in un database? Lascia un commento qui sotto, e buona programmazione!

## Tutorial Correlati

- [Estrai Testo da Immagine – Ottimizzazione OCR con Aspose.OCR per .NET](/ocr/english/net/ocr-optimization/)
- [Come Estrarre Testo da Immagine Preparando Rettangoli in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Estrai Testo da Immagine – Riconoscere Linea con Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}