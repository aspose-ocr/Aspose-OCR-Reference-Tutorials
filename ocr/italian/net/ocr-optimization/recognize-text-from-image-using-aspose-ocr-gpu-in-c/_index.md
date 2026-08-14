---
category: general
date: 2026-02-20
description: Riconosci il testo da un'immagine rapidamente con l'accelerazione GPU
  di Aspose OCR. Scopri come estrarre il testo da una scansione in C# con un esempio
  completo e eseguibile.
draft: false
keywords:
- recognize text from image
- extract text from scan
- Aspose OCR GPU
- C# OCR tutorial
- image to text conversion
language: it
og_description: Riconosci il testo da un'immagine con accelerazione GPU. Questo tutorial
  ti mostra come estrarre il testo da una scansione in C# usando Aspose OCR, completo
  di codice e consigli.
og_title: Riconoscere il testo da un'immagine usando Aspose OCR GPU – Guida C#
tags:
- Aspose
- OCR
- C#
- GPU
title: Riconoscere il testo da un'immagine usando Aspose OCR GPU in C#
url: /it/net/ocr-optimization/recognize-text-from-image-using-aspose-ocr-gpu-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# riconoscere testo da immagine usando Aspose OCR GPU in C#

Hai mai dovuto **riconoscere testo da immagine** ma il file era enorme e la tua CPU si bloccava? Forse hai provato una vecchia libreria OCR e ci è voluto un tempo infinito, o i risultati erano scarsi. La buona notizia? Con l’accelerazione GPU di Aspose OCR puoi trasformare un TIFF scansionato di grandi dimensioni in testo pulito e ricercabile in pochi secondi.

In questa guida percorreremo un esempio completo, pronto per il copia‑incolla, che mostra come **estrarre testo da file di scansione** su una macchina con GPU abilitata. Nessun riferimento vago, solo il codice necessario, perché ogni riga è importante, e qualche avvertimento per non impazzire.

## Cosa ti serve

- **.NET 6+** (o .NET Framework 4.7+ – l’API funziona allo stesso modo)
- Pacchetto NuGet **Aspose.OCR for .NET** (versione 23.12 o successiva)
- Una **GPU** con supporto CUDA (opzionale, ma notevolmente più veloce)
- Un’immagine scansionata ad alta risoluzione (es. `large_doc.tif`)

Se non hai una GPU, il motore tornerà automaticamente alla CPU – quindi potrai comunque eseguire l’esempio, solo un po’ più lentamente.

## Passo 1 – Installa il pacchetto Aspose.OCR

Apri il terminale o la Package Manager Console ed esegui:

```bash
dotnet add package Aspose.OCR
```

Oppure, nell’interfaccia NuGet di Visual Studio, cerca **Aspose.OCR** e fai clic su *Installa*. Questo scaricherà la libreria OCR di base più l’assembly opzionale per l’accelerazione GPU.

> **Consiglio esperto:** Dopo l’installazione, controlla la cartella `packages` per `Aspose.OCR.Acceleration.dll`. È necessario per il supporto GPU; se sei su un server headless, puoi ometterlo e il codice compilerà comunque.

## Passo 2 – Inizializza il motore OCR accelerato dalla GPU

La classe `GpuOcrEngine` rileva automaticamente qualsiasi GPU compatibile. Se ne hai più di una, puoi scegliere una specifica, ma la maggior parte degli sviluppatori lascia che sia il motore a decidere.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Acceleration;   // <-- enables GPU support

class GpuExample
{
    static void Main()
    {
        // Step 2.1: Create the OCR engine. It will look for a CUDA‑compatible GPU.
        GpuOcrEngine ocrEngine = new GpuOcrEngine();

        // Step 2.2 (optional): Force a particular GPU device.
        // Uncomment the line below if you know the device ID you want to use.
        // ocrEngine.Device = GpuDevice.GetById(0);
```

**Perché è importante:** Inizializzare il motore GPU una sola volta mantiene basso l’overhead. Se crei e distruggi ripetutamente il motore all’interno di un ciclo, perderai i guadagni di prestazioni.

## Passo 3 – Carica la tua immagine scansionata ad alta risoluzione

Aspose OCR lavora con `System.Drawing.Image`. Assicurati che il percorso del file punti a un’immagine reale; altrimenti otterrai una `FileNotFoundException`.

```csharp
        // Step 3: Load the image you want to process.
        // Replace YOUR_DIRECTORY with the actual folder on your machine.
        var scannedImage = Image.FromFile(@"YOUR_DIRECTORY/large_doc.tif");
```

> **Caso limite:** Se l’immagine è più grande di 10 000 × 10 000 px, considera di ridurla prima. La memoria della GPU è limitata e caricare un bitmap enorme può provocare una `OutOfMemoryException`.

## Passo 4 – Esegui l’OCR con le impostazioni predefinite (lingua latina)

Il metodo `Recognize` restituisce una stringa semplice. Puoi passare un oggetto `OcrOptions` se ti serve una lingua diversa o una pre‑elaborazione personalizzata.

```csharp
        // Step 4: Run OCR. By default it assumes Latin script.
        string recognizedText = ocrEngine.Recognize(scannedImage);
```

**Perché le impostazioni predefinite funzionano:** La maggior parte dei documenti scansionati – contratti, fatture, report – utilizza alfabeti basati sul latino. Se ti servono cirillico, arabo o cinese, imposta `ocrEngine.Language = "ru"` (o il codice ISO appropriato) prima di chiamare `Recognize`.

## Passo 5 – Visualizza o salva il testo estratto

Per un rapido controllo scriveremo semplicemente il risultato sulla console. In un’app reale potresti salvarlo in un database, in un file `.txt` o inviarlo a un indice di ricerca.

```csharp
        // Step 5: Output the OCR result.
        Console.WriteLine(recognizedText);

        // Optional: Save to a file.
        // File.WriteAllText(@"output.txt", recognizedText);
    }
}
```

### Output previsto

Se `large_doc.tif` contiene un semplice paragrafo come “Hello, world!”, vedrai:

```
Hello, world!
```

Per scansioni multi‑pagina il motore concatena il testo nell’ordine di lettura. Puoi suddividerlo successivamente usando i ritorni a capo (`\n`) se ti servono i confini di pagina.

## Gestione delle difficoltà comuni

| Problema | Sintomo | Soluzione |
|----------|---------|-----------|
| **Nessuna GPU rilevata** | `ocrEngine.Device` è `null` e l’elaborazione è lenta. | Installa l’ultimo driver NVIDIA e il CUDA Toolkit (v11+). Verifica con `nvidia-smi`. |
| **Ritardi nella garbage collection** | Picchi di memoria dopo l’elaborazione di molte immagini. | Chiama `scannedImage.Dispose()` dopo l’OCR, o avvolgi l’immagine in un blocco `using`. |
| **Lingua errata** | Caratteri incomprensibili per testo non latino. | Imposta `ocrEngine.Language` sul codice ISO 639‑1 corretto prima di `Recognize`. |
| **File molto grandi** | `OutOfMemoryException`. | Ridimensiona con `Image.GetThumbnailImage` o dividi la scansione in tasselli. |

## Esempio completo, pronto per l’esecuzione

Di seguito trovi l’intero programma – inclusi i `using`, la gestione degli errori e un blocco `using` ordinato per l’immagine:

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Acceleration; // GPU support

class GpuOcrDemo
{
    static void Main()
    {
        try
        {
            // Initialize the GPU‑accelerated OCR engine.
            GpuOcrEngine ocrEngine = new GpuOcrEngine();

            // OPTIONAL: Choose a specific GPU device.
            // ocrEngine.Device = GpuDevice.GetById(0);

            // Load the high‑resolution scanned image.
            string imagePath = @"YOUR_DIRECTORY/large_doc.tif";
            if (!File.Exists(imagePath))
                throw new FileNotFoundException($"Image not found: {imagePath}");

            using (Image scannedImage = Image.FromFile(imagePath))
            {
                // Perform OCR (defaults to Latin script).
                string text = ocrEngine.Recognize(scannedImage);

                // Output the extracted text.
                Console.WriteLine("=== OCR Result ===");
                Console.WriteLine(text);

                // Save to a text file (optional).
                string outputPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(outputPath, text);
                Console.WriteLine($"Text saved to {outputPath}");
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

### Cosa fa questo codice

1. **Crea** un `GpuOcrEngine` che seleziona automaticamente la GPU migliore.
2. **Carica** il TIFF di destinazione all’interno di un blocco `using` per garantire lo smaltimento.
3. **Chiama** `Recognize` per convertire il bitmap in una stringa.
4. **Scrive** il risultato sia sulla console sia in un file `.txt` accanto all’immagine sorgente.
5. **Gestisce** eventuali eccezioni stampando un messaggio di errore amichevole.

## Approfondimenti – Da “riconoscere testo da immagine” a pipeline documentali complete

Ora che sai **estrarre testo da file di scansione**, considera i prossimi passi:

- **Elaborazione batch:** cicla su una cartella di TIFF e aggrega i risultati in un unico indice ricercabile.
- **Rilevamento lingua:** usa `ocrEngine.DetectLanguage()` (se disponibile) per cambiare lingua automaticamente.
- **Post‑processing:** passa l’output attraverso un correttore ortografico o un filtro regex per pulire gli artefatti OCR.
- **Integrazione con Azure Cognitive Search:** invia il testo estratto a un indice cloud ricercabile per lookup istantanei.

Ognuno di questi si basa sullo stesso modello di base che hai appena visto – inizializza una volta, alimenta le immagini, raccogli il testo.

## Conclusione

Hai appena imparato come **riconoscere testo da immagine** usando il motore OCR accelerato da GPU di Aspose OCR in C#. L’esempio completo e funzionante mostra come configurare il motore, caricare una scansione ad alta risoluzione, eseguire l’OCR e gestire l’output. Seguendo i consigli e le indicazioni per i casi limite sopra, eviterai le difficoltà più comuni e otterrai risultati affidabili sia su un laptop da sviluppatore sia su un server di produzione.

Pronto a trasformare altre scansioni in dati ricercabili? Prova a processare un’intera cartella, sperimenta con lingue non latine, o invia i risultati a un motore di ricerca full‑text. Il cielo è il limite, e il codice che hai appena scritto è la solida base di cui hai bisogno.

Buon coding! 🚀

![esempio di riconoscimento testo da immagine](/images/ocr-gpu

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}