---
category: general
date: 2026-02-25
description: Riconosci rapidamente il testo da un'immagine usando OCR accelerato da
  GPU. Impara a impostare la modalità GPU, caricare l'immagine per l'OCR ed estrarre
  il testo da un TIFF.
draft: false
keywords:
- recognize text from image
- set gpu mode
- gpu accelerated ocr
- load image for ocr
- extract text from tiff
language: it
og_description: Riconosci il testo da un'immagine istantaneamente usando OCR accelerato
  da GPU. Tutorial passo‑passo in C# che copre l'impostazione della modalità GPU,
  il caricamento dell'immagine per l'OCR e l'estrazione del testo da un TIFF.
og_title: Riconosci il testo da un'immagine con OCR accelerato da GPU – Guida C#
tags:
- Aspose OCR
- C#
- GPU computing
title: Riconoscere il testo da un'immagine con OCR accelerato da GPU in C#
url: /it/net/ocr-optimization/recognize-text-from-image-using-gpu-accelerated-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# riconoscere testo da immagine usando OCR accelerato da GPU in C#

Hai mai avuto bisogno di **riconoscere testo da immagine** ma la tua CPU si soffocava con una scansione ad alta risoluzione? Non sei solo. In molti progetti reali—pensa alla digitalizzazione di fatture o all'archiviazione di vecchi giornali—un singolo file TIFF può bloccare la tua pipeline per minuti. La buona notizia? Aspose.OCR ti permette di attivare un interruttore e affidare il lavoro pesante alla tua GPU, trasformando un'operazione lenta in quasi un'istantanea.

In questo tutorial percorreremo l'intero processo: come **impostare la modalità GPU**, come **caricare l'immagine per OCR**, e come **estrarre testo da file TIFF**. Alla fine avrai un esempio autonomo, pronto per la produzione, che potrai inserire in qualsiasi progetto .NET 6+.

## Prerequisiti

- .NET 6 SDK (o successivo) installato.
- Visual Studio 2022 o qualsiasi editor tu preferisca.
- Un pacchetto NuGet Aspose.OCR (`Aspose.OCR`) aggiunto al tuo progetto.
- Una GPU che supporta DirectX 11 o successivo (la maggior parte delle GPU moderne ne è idonea).  
  *Se non hai una GPU, puoi comunque eseguire il codice con `GpuMode.Auto`—la libreria tornerà automaticamente alla CPU.*

> **Consiglio professionale:** Verifica che il driver della tua GPU sia aggiornato; driver obsoleti possono causare errori di inizializzazione poco chiari.

## Passo 1 – Crea il motore OCR e imposta la modalità GPU

La prima cosa di cui hai bisogno è un'istanza di `OcrEngine`. Questo oggetto contiene tutta la configurazione, inclusa l'opzione se il motore deve usare la GPU.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace GpuOcrDemo
{
    public class Program
    {
        public static void Main()
        {
            // Step 1: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Enable GPU acceleration.
            // Use GpuMode.Auto if you want the library to pick CPU when a GPU isn’t available.
            ocrEngine.Config.SetGpuMode(GpuMode.Enabled);

            // The rest of the workflow continues below…
        }
    }
}
```

**Perché è importante:** Abilitare la modalità GPU sposta la pre‑elaborazione delle immagini, computazionalmente intensiva (binarizzazione, rimozione del rumore, ecc.), sulla scheda grafica. Su una RTX 3060 di fascia media, puoi vedere un **incremento di velocità di 3‑5×** rispetto all'elaborazione esclusivamente CPU.

## Passo 2 – Carica l'immagine per OCR (esempio TIFF)

Aspose.OCR accetta molti formati, ma il TIFF è comune per i documenti scansionati perché preserva la qualità senza perdita. Usa `ImageStream.FromFile` per leggere il file in memoria.

```csharp
// Step 2: Load the high‑resolution TIFF you want to process
ocrEngine.Image = ImageStream.FromFile(@"C:\Data\high_res_scan.tif");

// Optional: If you need to work with a stream (e.g., from a web API), use:
// ocrEngine.Image = ImageStream.FromStream(yourInputStream);
```

**Caso limite:** Alcuni file TIFF contengono più pagine. `ImageStream.FromFile` leggerà solo la prima pagina. Se devi elaborare ogni pagina, itera su `ImageInfo.Pages` e passa ciascuna al motore separatamente.

## Passo 3 – Esegui il riconoscimento

Ora che il motore è configurato e l'immagine è caricata, chiama `Recognize()`. Il metodo restituisce un oggetto `OcrResult` contenente l'output di testo semplice e metadati aggiuntivi.

```csharp
// Step 3: Run OCR
OcrResult result = ocrEngine.Recognize();

// The result may include confidence scores per line, if you enable them in the config.
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(result.Text);
```

**Cosa fare se il testo appare confuso?**  
- Assicurati che l'immagine sia in un'orientazione leggibile (ruota se necessario).  
- Regola le opzioni di pre‑elaborazione come `ocrEngine.Config.DeskewEnabled = true;`.  
- Per documenti multilingue, imposta `ocrEngine.Config.Language = Language.English;` o l'enumerazione appropriata.

## Passo 4 – Verifica l'output e gestisci gli errori

Un'implementazione robusta verifica risultati null e intercetta potenziali eccezioni (ad esempio, driver GPU mancanti).

```csharp
try
{
    OcrResult result = ocrEngine.Recognize();

    if (result?.Text == null)
    {
        Console.WriteLine("No text detected – double‑check the image quality.");
    }
    else
    {
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);
    }
}
catch (Exception ex)
{
    Console.WriteLine($"OCR failed: {ex.Message}");
    // You might want to fallback to CPU mode here:
    // ocrEngine.Config.SetGpuMode(GpuMode.Disabled);
}
```

**Perché avvolgerlo?** L'inizializzazione della GPU può lanciare `DllNotFoundException` se le librerie native richieste non sono presenti. Il blocco catch ti offre un percorso di degradazione elegante.

## Esempio completo, eseguibile

Mettendo tutto insieme, ecco un programma completo che puoi compilare ed eseguire subito. Sostituisci il percorso del file con un TIFF reale sul tuo computer.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace GpuOcrDemo
{
    public class Program
    {
        public static void Main()
        {
            // 1️⃣ Create OCR engine and enable GPU acceleration
            var ocrEngine = new OcrEngine();
            ocrEngine.Config.SetGpuMode(GpuMode.Enabled); // or GpuMode.Auto for fallback

            // 2️⃣ Load the image you want to process
            string imagePath = @"C:\Data\high_res_scan.tif";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Optional: tweak preprocessing (helps with noisy scans)
            ocrEngine.Config.DeskewEnabled = true;
            ocrEngine.Config.RemoveNoiseEnabled = true;

            // 4️⃣ Run recognition and handle the result
            try
            {
                OcrResult result = ocrEngine.Recognize();

                if (string.IsNullOrWhiteSpace(result?.Text))
                {
                    Console.WriteLine("No text found – consider improving image quality.");
                }
                else
                {
                    Console.WriteLine("=== Recognized Text ===");
                    Console.WriteLine(result.Text);
                }
            }
            catch (Exception e)
            {
                Console.WriteLine($"Error during OCR: {e.Message}");
                // Fallback to CPU if GPU failed
                ocrEngine.Config.SetGpuMode(GpuMode.Disabled);
                // You could retry here…
            }
        }
    }
}
```

**Output previsto**

Se il TIFF contiene testo inglese leggibile, vedrai qualcosa del genere:

```
=== Recognized Text ===
Invoice #12345
Date: 2024‑11‑08
Total Amount: $1,235.00
...
```

Se l'immagine è vuota o illeggibile, la console ti consiglierebbe di controllare il file di origine.

## Domande comuni & variazioni

| Domanda | Risposta |
|----------|--------|
| **Posso elaborare JPEG o PNG invece di TIFF?** | Assolutamente. `ImageStream.FromFile` funziona con qualsiasi formato supportato da Aspose.OCR (PNG, JPEG, BMP, ecc.). |
| **E se ho più pagine in un unico TIFF?** | Itera su `ImageInfo.Pages` e assegna ogni pagina a `ocrEngine.Image` prima di chiamare `Recognize()`. |
| **Ho bisogno di una licenza per Aspose.OCR?** | Una valutazione gratuita funziona fino a 100 pagine. Per la produzione, acquista una licenza per rimuovere il watermark di valutazione. |
| **Come cambio il modello linguistico?** | Imposta `ocrEngine.Config.Language = Language.Spanish;` (o qualsiasi enum supportato). |
| **C'è un modo per ottenere i punteggi di confidenza?** | Abilita `ocrEngine.Config.EnableConfidence = true;` e ispeziona `result.Confidence` per riga. |

## Conclusione

Ora sai come **recognize text from image** usando una pipeline **OCR accelerata da GPU** in C#. Impostando la **modalità GPU**, **caricando un'immagine per OCR**, e **estrarre testo da file TIFF**, hai costruito una soluzione veloce e scalabile pronta per carichi di lavoro reali.

Prossimi passi? Prova a concatenare questo codice con un generatore PDF per creare PDF ricercabili, oppure alimenta le stringhe estratte in una pipeline di elaborazione del linguaggio naturale. Puoi anche sperimentare con `GpuMode.Auto` per rendere la tua app adattabile a ambienti senza GPU.

Buon coding, e che le tue esecuzioni OCR siano fulminee! 

![esempio di riconoscimento testo da immagine](https://example.com/ocr-demo.png "riconoscere testo da immagine usando OCR accelerato da GPU")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}