---
category: general
date: 2026-02-11
description: Impara come eseguire l'OCR su un'immagine usando GPU OCR in C#. Questo
  tutorial passo‑passo copre l'installazione, il codice e le migliori pratiche.
draft: false
keywords:
- perform OCR on image
- use GPU OCR
- Aspose OCR C#
- GPU acceleration OCR
- OCR performance tuning
language: it
og_description: Esegui OCR su un'immagine usando GPU OCR in C#. Segui questa guida
  per una soluzione veloce e affidabile con Aspose OCR.
og_title: Esegui OCR su immagine con GPU – Implementazione completa in C#
tags:
- OCR
- C#
- Aspose
- GPU Computing
title: Eseguire OCR su immagine con accelerazione GPU – Guida completa C#
url: /it/net/ocr-optimization/perform-ocr-on-image-with-gpu-acceleration-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esegui OCR su Immagine con Accelerazione GPU – Guida Completa C#

Hai mai dovuto **perform OCR on image** ma la tua CPU si bloccava su enormi file TIFF? Non sei solo. In molti progetti reali, l'elaborazione di grandi documenti può trasformare pochi secondi in minuti, e questo rallentamento penalizza sia gli utenti sia i budget.  

La buona notizia? Sfruttando una GPU puoi ridurre drasticamente i tempi di elaborazione. In questo tutorial ti guideremo attraverso un esempio pratico che mostra esattamente **how to perform OCR on image** usando il motore GPU‑accelerated di Aspose, oltre a una serie di consigli pratici che non troverai nella documentazione generica.

> **What you’ll get:** un'app console C# pronta‑all'uso, spiegazioni di ogni riga e indicazioni per risolvere i problemi comuni. Nessun riferimento esterno necessario—tutto ciò che ti serve è qui.

## Cosa Ti Serve

Prima di iniziare, assicurati di avere installato quanto segue sulla tua macchina di sviluppo:

| Prerequisito | Versione minima |
|--------------|-----------------|
| .NET 6.0 SDK or later | 6.0 |
| Visual Studio 2022 (or any IDE you like) | 17.0 |
| Aspose.OCR for .NET (NuGet package) | 23.11 or newer |
| A GPU that supports CUDA (NVIDIA) | Compute Capability 3.5+ |
| A sample image – e.g., `large_document.tif` | any size |

Se qualcuno di questi ti è sconosciuto, non preoccuparti. La funzionalità **use GPU OCR** funziona anche su GPU modeste, e il pacchetto NuGet scaricherà tutte le binarie native necessarie per te.

## Passo 1: Esegui OCR su Immagine con Accelerazione GPU

La prima cosa di cui abbiamo bisogno è un'istanza del motore OCR abilitato GPU. Questo oggetto gestisce il lavoro pesante sulla scheda grafica, mantenendo comunque un'API pulita e sincrona.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System.Drawing;

// Create a GPU‑accelerated OCR engine and configure it
var ocrEngine = new GpuOcrEngine
{
    // Select the first GPU in the system (device index 0)
    DeviceId = 0,
    // Let the engine download language packs automatically if they’re missing
    AutomaticResourceDownload = true,
    // Specify the language you want to recognize – English in this case
    Language = OcrLanguage.English
};
```

**Perché è importante:**  
- `DeviceId = 0` indica alla libreria di usare la GPU primaria; puoi cambiarlo se hai più schede.  
- `AutomaticResourceDownload = true` previene un errore a runtime quando i dati della lingua inglese non sono presenti localmente.  
- Impostare `Language` esplicitamente evita il fallback predefinito del motore a un modello più lento e generico.

> **Pro tip:** Se stai eseguendo su un server headless, assicurati che il driver NVIDIA sia installato e che il comando `nvidia-smi` segnali la GPU come “Online”. Altrimenti il motore tornerà silenziosamente alla CPU.

## Passo 2: Carica il File Immagine

Successivamente, carica l'immagine su cui eseguire l'OCR. Aspose funziona con qualsiasi `System.Drawing.Image`, quindi puoi fornire JPEG, PNG, TIFF o anche PDF multi‑pagina (dopo la conversione).

```csharp
// Load the image from disk – replace the path with your own file location
using var image = Image.FromFile(@"C:\OCR\Samples\large_document.tif");
```

**Perché è importante:**  
- Usare una dichiarazione `using` garantisce che le risorse non gestite dell'immagine vengano rilasciate tempestivamente, il che è cruciale quando si elaborano molti file in un ciclo.  
- Se la tua immagine è eccezionalmente grande (ad esempio > 500 MB), considera di ridimensionarla prima per mantenere sotto controllo l'uso della memoria GPU.

## Passo 3: Riconosci il Testo Usando il Motore OCR GPU

Ora passiamo l'immagine al motore GPU e attendiamo il risultato. Il metodo `Recognize` restituisce un oggetto `OcrResult` contenente il testo estratto e le metriche di prestazione.

```csharp
// Perform OCR – this call runs on the GPU
var ocrResult = ocrEngine.Recognize(image);
```

**Perché è importante:**  
- La chiamata è sincrona, il che significa che il thread si blocca finché la GPU non termina. In un'app UI vorresti eseguirla su un thread in background per mantenere l'interfaccia reattiva.  
- `ocrResult.ProcessingTime` fornisce il tempo trascorso in millisecondi, ideale per confrontare le prestazioni **use GPU OCR** rispetto alle alternative solo CPU.

## Passo 4: Visualizza i Risultati e le Statistiche

Infine, stampiamo la lunghezza del testo riconosciuto e il tempo impiegato dall'operazione. In un'applicazione reale probabilmente scriveresti `ocrResult.Text` su un file o in un database.

```csharp
// Show a quick summary on the console
Console.WriteLine($"Recognized {ocrResult.Text.Length} characters in {ocrResult.ProcessingTime} ms");

// Optionally, dump the full text (commented out for brevity)
// Console.WriteLine(ocrResult.Text);
```

**Output previsto (esempio):**

```
Recognized 12457 characters in 312 ms
```

Nota come il tempo di elaborazione sia misurato in poche centinaia di millisecondi per un TIFF multi‑megabyte—esattamente l'accelerazione che ti aspetti quando **use GPU OCR**.

![perform OCR on image example](/images/perform-ocr-on-image.png "Screenshot showing console output after performing OCR on image")

*Lo screenshot sopra illustra l'output della console dopo aver eseguito OCR su immagine con accelerazione GPU.*

## Come Utilizzare GPU OCR Efficientemente

Anche se il codice sopra funziona subito, le distribuzioni in produzione spesso incontrano qualche problema. Di seguito i problemi più comuni e come risolverli.

| Problema | Causa | Soluzione |
|----------|-------|-----------|
| **Out‑of‑memory (GPU)** | Immagine troppo grande per la VRAM della GPU | Ridimensiona l'immagine (`Bitmap` resize) prima di chiamare `Recognize`. |
| **Language pack not found** | `AutomaticResourceDownload` disabilitato o nessuna connessione internet | Pre‑scarica il language pack tramite `ocrEngine.DownloadResources(OcrLanguage.English)`. |
| **Slow first run** | Compilazione JIT del driver GPU | Riscalda il motore eseguendo una piccola immagine dummy una volta all'avvio. |
| **Incorrect character set** | Proprietà `Language` errata | Imposta `Language` sull'enum corretto (ad esempio `OcrLanguage.French`). |

**Pro tip:** Quando elabori in batch decine di file, riutilizza la stessa istanza `GpuOcrEngine`. Creare un nuovo motore per ogni file comporta un costoso cambio di contesto GPU.

## Esempio Completo Funzionante

Ecco l'intero programma assemblato in un unico file che puoi copiare‑incollare in un nuovo progetto console.

```csharp
// File: Program.cs
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.Drawing;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize GPU OCR engine
            var ocrEngine = new GpuOcrEngine
            {
                DeviceId = 0,
                AutomaticResourceDownload = true,
                Language = OcrLanguage.English
            };

            // 2️⃣ Load the image (adjust the path to your file)
            using var image = Image.FromFile(@"C:\OCR\Samples\large_document.tif");

            // 3️⃣ Run recognition on the GPU
            var ocrResult = ocrEngine.Recognize(image);

            // 4️⃣ Output statistics
            Console.WriteLine($"Recognized {ocrResult.Text.Length} characters in {ocrResult.ProcessingTime} ms");

            // Optional: write the extracted text to a file
            // System.IO.File.WriteAllText("output.txt", ocrResult.Text);
        }
    }
}
```

Salva il file, esegui `dotnet run` e dovresti vedere il conteggio dei caratteri e il tempo di elaborazione stampati sulla console. Se apri `output.txt` (decommenta la riga), vedrai il testo OCR grezzo pronto per l'elaborazione successiva.

## Conclusione

Ti abbiamo appena mostrato **how to perform OCR on image** usando il motore GPU‑accelerated di Aspose, dalla configurazione di `GpuOcrEngine` alla gestione del risultato e alla risoluzione dei problemi comuni. Delegando il lavoro pesante alla scheda grafica, ottieni miglioramenti di velocità di ordine di grandezza—esattamente ciò di cui hai bisogno quando lavori con documenti di grandi dimensioni o scenari di scansione in tempo reale.

> **Takeaway:** La combinazione di `GpuOcrEngine`, gestione automatica delle risorse e dimensionamento attento delle immagini ti fornisce una pipeline robusta e ad alte prestazioni per qualsiasi progetto C# che necessita di **use GPU OCR**.

### Cosa Viene Dopo?

- **Batch processing:** Avvolgi la logica principale in un ciclo `foreach` per gestire cartelle di immagini.  
- **Parallelism:** Combina GPU OCR con `Parallel.ForEach` per server multi‑GPU.  
- **Post‑processing:** Fornisci `ocrResult.Text` a un correttore ortografico o a un estrattore di entità per analisi più intelligenti a valle.  

Sentiti libero di sperimentare—sostituisci `OcrLanguage.English` con un'altra lingua, prova formati immagine diversi o integra il motore in un'API ASP.NET. Il cielo è il limite quando **use GPU OCR** in modo responsabile.

Buona programmazione, e che i tuoi job OCR girino a velocità della luce!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}