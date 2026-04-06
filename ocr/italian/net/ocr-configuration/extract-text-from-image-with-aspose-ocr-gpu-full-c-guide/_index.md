---
category: general
date: 2026-04-06
description: Estrai il testo da un'immagine usando Aspose OCR GPU in C#. Impara a
  caricare l'immagine da file e impostare il limite di memoria GPU in questa guida
  passo‑passo.
draft: false
keywords:
- extract text from image
- load image from file
- set gpu memory limit
- aspose ocr example
- aspose ocr gpu
language: it
og_description: Estrai il testo da un'immagine usando Aspose OCR GPU in C#. Impara
  a caricare l'immagine da file e impostare il limite di memoria GPU in questa guida
  passo‑passo.
og_title: Estrai il testo dall'immagine con Aspose OCR GPU – Guida completa C#
tags:
- Aspose OCR
- C#
- GPU
- OCR
title: Estrai il testo da un'immagine con Aspose OCR GPU – Guida completa C#
url: /it/net/ocr-configuration/extract-text-from-image-with-aspose-ocr-gpu-full-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrarre testo da immagine con Aspose OCR GPU – Guida completa C#

Ti è mai capitato di **estrarre testo da un'immagine** ma di rimanere bloccato quando le prestazioni diventano cruciali? Non sei solo: molti sviluppatori incontrano lo stesso ostacolo quando l'OCR diventa un collo di bottiglia. In questo tutorial ti mostreremo esattamente come estrarre testo da un'immagine usando il runtime GPU di Aspose OCR, caricare l'immagine da file e persino impostare un limite di memoria GPU per un controllo più preciso delle risorse.

Percorreremo un esempio completo, pronto‑da‑eseguire in C#, spiegheremo perché ogni riga è importante e indicheremo le insidie più comuni. Alla fine avrai una solida base per costruire pipeline OCR veloci e scalabili che girano sulla GPU.

## Cosa copre questa guida

- **Prerequisiti**: .NET 6+ (o .NET Framework 4.6+), pacchetto NuGet Aspose.OCR, driver GPU compatibile.  
- **Codice passo‑passo** che carica un'immagine da file, configura il motore GPU di Aspose OCR ed estrae il testo.  
- **Perché** potresti voler impostare un limite di memoria GPU e come farlo in modo sicuro.  
- **Gestione dei casi limite**: immagini a bassa risoluzione, GPU assente e risoluzione di problemi con i punteggi di confidenza.  
- **Passi successivi**: elaborazione batch, integrazione con ASP.NET Core e ritorno alla CPU se necessario.

> **Consiglio professionale:** se non sei sicuro che la GPU venga effettivamente usata, controlla il monitor di attività GPU (ad esempio NVIDIA‑SMI) mentre l'OCR è in esecuzione. Vedrai un picco di utilizzo della memoria corrispondente al limite impostato.

---

![Diagramma che mostra il flusso di estrazione del testo da immagine usando il motore Aspose OCR GPU engine](extract-text-from-image-aspose-ocr-gpu.png "estrarre testo da immagine usando Aspose OCR GPU")

## Passo 1: Inizializzare il motore Aspose OCR per l'elaborazione GPU

La prima cosa di cui hai bisogno è un'istanza di `OcrEngine` che sappia di dover girare sulla GPU. Aspose fornisce un oggetto `OcrEngineSettings` pulito dove puoi specificare il runtime.

```csharp
using Aspose.OCR;
using Aspose.OCR.Runtime;
using System;
using System.Drawing;

// Create the OCR engine and tell it to use the GPU runtime
var ocrEngine = new OcrEngine(new OcrEngineSettings
{
    Runtime = OcrRuntime.Gpu   // Switches processing to the GPU
});
```

**Perché è importante:** per impostazione predefinita Aspose OCR ricade sulla CPU, il che è accettabile per immagini piccolissime ma può diventare dolorosamente lento per foto ad alta risoluzione. Impostare esplicitamente `Runtime = OcrRuntime.Gpu` sposta il lavoro pesante sulla scheda grafica, garantendo un notevole aumento di velocità.

## Passo 2: (Opzionale) Impostare un limite di memoria GPU

Se lavori su una workstation condivisa o in un container con risorse GPU limitate, puoi porre un tetto alla quantità di memoria che il motore OCR consuma. Questo evita crash per out‑of‑memory e mantiene felici gli altri processi.

```csharp
// Limit the GPU memory usage to 1024 MB (1 GB)
ocrEngine.Settings.GpuMemoryLimit = 1024;
```

**Quando usarlo:**  
- **Ambienti multi‑tenant** in cui diversi servizi condividono la stessa GPU.  
- **Pipeline CI/CD** che assegnano una quantità fissa di memoria GPU per job.  

Se ometti questa riga, Aspose utilizzerà tutta la memoria necessaria, il che è accettabile su una workstation dedicata.

## Passo 3: Caricare l'immagine da file

Ora dobbiamo portare l'immagine in memoria. Aspose OCR lavora con `System.Drawing.Image`, quindi useremo `Image.FromFile`. Assicurati che il percorso punti a un file reale; altrimenti verrà sollevata un'eccezione.

```csharp
// Replace with the actual path to your high‑resolution image
string imagePath = @"YOUR_DIRECTORY/high_res_photo.png";

using (var image = Image.FromFile(imagePath))
{
    // The image is now ready for OCR processing
    // (the next step will happen inside this using block)
}
```

**Perché il caricamento da file è importante:** molti sviluppatori provano a fornire direttamente un array di byte, cosa che funziona ma aggiunge un passaggio di conversione non necessario. Usare `Image.FromFile` è diretto, e la dichiarazione `using` garantisce che il handle del file venga rilasciato prontamente.

## Passo 4: Eseguire l'OCR e recuperare il risultato

Con il motore configurato e l'immagine caricata, possiamo finalmente estrarre il testo. Il metodo `Recognize` restituisce un `OcrResult` contenente sia il testo grezzo sia un punteggio di confidenza.

```csharp
using (var image = Image.FromFile(imagePath))
{
    // Perform OCR on the loaded image
    var ocrResult = ocrEngine.Recognize(image);

    // Display the confidence and the extracted text
    Console.WriteLine($"GPU OCR confidence: {ocrResult.Confidence:P2}");
    Console.WriteLine("Extracted text:");
    Console.WriteLine(ocrResult.Text);
}
```

**Comprendere l'output:**  
- `Confidence` è un valore compreso tra 0 e 1. Una confidenza di 0,95 (o 95 %) indica solitamente che l'OCR è preciso.  
- `Text` contiene i ritorni a capo così come appaiono nell'immagine, utile per ulteriori elaborazioni.

## Passo 5: Verificare l'output e gestire i casi limite

### Controllare i livelli di confidenza

Se la confidenza scende sotto, ad esempio, l'80 %, potresti voler tornare all'elaborazione CPU o applicare una pre‑elaborazione dell'immagine (es. binarizzazione).

```csharp
if (ocrResult.Confidence < 0.80)
{
    Console.WriteLine("Low confidence detected – consider preprocessing or CPU fallback.");
    // Example fallback: switch to CPU runtime temporarily
    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
    var cpuResult = ocrEngine.Recognize(image);
    Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
    Console.WriteLine(cpuResult.Text);
}
```

### Gestire l'assenza di GPU

Non tutte le macchine dispongono di una GPU compatibile. Aspose lancerà un `OcrException` se non riesce a inizializzare il runtime GPU.

```csharp
try
{
    var ocrResult = ocrEngine.Recognize(image);
    // Normal processing...
}
catch (OcrException ex) when (ex.Message.Contains("GPU"))
{
    Console.WriteLine("GPU not available – falling back to CPU.");
    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
    var cpuResult = ocrEngine.Recognize(image);
    Console.WriteLine(cpuResult.Text);
}
```

### Immagini ad alta risoluzione

Immagini molto grandi (es. > 4000 px di larghezza) possono consumare molta memoria GPU. Se raggiungi il limite impostato in precedenza, Aspose troncherà l'elaborazione. In questi casi, ridimensiona prima l'immagine:

```csharp
using (var original = Image.FromFile(imagePath))
{
    int maxWidth = 2000;
    var resized = new Bitmap(original, new Size(maxWidth, original.Height * maxWidth / original.Width));
    var ocrResult = ocrEngine.Recognize(resized);
    // Continue as before
}
```

## Esempio completo funzionante

Di seguito trovi il programma completo da copiare‑incollare in un nuovo progetto console. Include tutti i passaggi, la gestione degli errori e la logica opzionale di fallback.

```csharp
// Program.cs
using Aspose.OCR;
using Aspose.OCR.Runtime;
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Initialize OCR engine to use GPU
        var ocrEngine = new OcrEngine(new OcrEngineSettings
        {
            Runtime = OcrRuntime.Gpu   // Switches processing to the GPU
        });

        // Step 2: (Optional) Limit GPU memory usage to 1 GB
        ocrEngine.Settings.GpuMemoryLimit = 1024;

        // Path to the image you want to process
        string imagePath = @"YOUR_DIRECTORY/high_res_photo.png";

        // Step 3: Load image from file
        using (var image = Image.FromFile(imagePath))
        {
            try
            {
                // Step 4: Run OCR on the image
                var ocrResult = ocrEngine.Recognize(image);

                // Step 5: Output confidence and extracted text
                Console.WriteLine($"GPU OCR confidence: {ocrResult.Confidence:P2}");
                Console.WriteLine("Extracted text:");
                Console.WriteLine(ocrResult.Text);

                // Edge‑case: low confidence handling
                if (ocrResult.Confidence < 0.80)
                {
                    Console.WriteLine("\nLow confidence detected – trying CPU fallback...");
                    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
                    var cpuResult = ocrEngine.Recognize(image);
                    Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
                    Console.WriteLine(cpuResult.Text);
                }
            }
            catch (OcrException ex) when (ex.Message.Contains("GPU"))
            {
                Console.WriteLine("GPU not available – falling back to CPU runtime.");
                ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
                var cpuResult = ocrEngine.Recognize(image);
                Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
                Console.WriteLine(cpuResult.Text);
            }
        }
    }
}
```

### Output previsto

```
GPU OCR confidence: 96.45%
Extracted text:
This is the text that was
found in the high‑resolution
image you supplied.

```

Se la confidenza scende sotto la soglia, vedrai i messaggi aggiuntivi di fallback alla CPU.

---

## Conclusione

Ora sai **come estrarre testo da immagine** usando il motore GPU di Aspose OCR, **come caricare l'immagine da file** e perché potresti voler **impostare un limite di memoria GPU** per carichi di lavoro di produzione. L'esempio sopra è una soluzione pienamente funzionante e citabile che puoi inserire in qualsiasi progetto .NET.

Quali sono i prossimi passi? Considera:

- **Elaborazione batch**: cicla su una cartella di immagini e scrivi i risultati in un CSV.  
- **Integrazione ASP.NET Core**: espone un endpoint API che accetta un'immagine caricata e restituisce il testo OCR.  
- **Ottimizzazione delle prestazioni**: sperimenta con valori diversi di `GpuMemoryLimit` e monitora l'utilizzo della GPU per trovare il punto ottimale.

Sentiti libero di adattare il codice al tuo scenario—che tu stia costruendo una pipeline di digitalizzazione documenti, un'app di traduzione in tempo reale o un servizio di scansione ricevute. I principi rimangono gli stessi: inizializzare il motore GPU, gestire saggiamente la memoria e verificare sempre la confidenza.

Hai domande o incontri un problema? Lascia un commento qui sotto e risolviamo insieme. Buon coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}