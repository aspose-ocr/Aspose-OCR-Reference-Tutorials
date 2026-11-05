---
category: general
date: 2026-02-14
description: Come utilizzare l'OCR in C# per estrarre rapidamente il testo da file
  PNG. Impara a fare OCR batch su immagini, a elaborare più immagini e a usare Aspose
  OCR C# in una guida unica.
draft: false
keywords:
- how to use OCR
- extract text png
- batch OCR images
- process multiple images
- aspose OCR c#
language: it
og_description: Come utilizzare l'OCR in C# con Aspose OCR C#. Questo tutorial mostra
  come estrarre testo da file PNG, eseguire OCR in batch su immagini e gestire più
  immagini in modo efficiente.
og_title: Come utilizzare l'OCR in C# – Estrazione di testo da PNG in batch
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Come utilizzare l'OCR in C# – Elaborazione batch di immagini PNG con Aspose
  OCR
url: /it/net/text-recognition/how-to-use-ocr-in-c-batch-process-png-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come usare l'OCR in C# – Elaborazione batch di immagini PNG con Aspose OCR

Ti sei mai chiesto **come usare l'OCR** per estrarre testo da un sacco di file PNG senza dover scrivere una routine separata per ciascuno? Non sei l'unico. Molti sviluppatori si trovano in difficoltà quando devono **estrarre testo da PNG** su larga scala, soprattutto quando le immagini sono in una cartella e devi avviare il motore OCR per ogni file.  

In questa guida percorreremo una soluzione completa, pronta‑da‑eseguire, che **esegue OCR batch sulle immagini**, **elabora più immagini** in parallelo e sfrutta la potente libreria **Aspose OCR C#**. Alla fine avrai un unico eseguibile che legge un numero qualsiasi di PNG, ne estrae il testo e stampa i risultati sulla console—tutto con poche righe di codice.

## Prerequisiti

- .NET 6.0 o successivo (il codice funziona anche con .NET Core e .NET Framework)  
- Una licenza valida di Aspose.OCR per .NET (o la versione di prova) – puoi ottenerla dal sito web di Aspose.  
- Una cartella contenente i file PNG che desideri leggere.  
- Visual Studio 2022 (o qualsiasi IDE compatibile con C#).  

Non sono richiesti pacchetti NuGet aggiuntivi oltre a `Aspose.OCR`.

## Passo 1: Come usare l'OCR – Inizializzare il motore Aspose OCR

La prima cosa di cui hai bisogno è un'istanza della classe `Engine`. Questo oggetto astrae la tecnologia OCR sottostante e può funzionare su CPU o GPU, a seconda dell'hardware e della licenza.

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

// Create an OCR engine (CPU by default; GPU can be enabled via EngineSettings if licensed)
var ocrEngine = new Engine();
```

*Perché è importante:* Inizializzare il motore una sola volta e riutilizzarlo tra i thread consente di risparmiare memoria ed evita il sovraccarico di caricare ripetutamente i modelli OCR. Garantisce inoltre impostazioni coerenti per tutte le immagini.

## Passo 2: Estrarre testo da PNG – Raccogliere i percorsi delle immagini

Successivamente, abbiamo bisogno di una raccolta di percorsi file. In un progetto reale potresti leggere la directory in modo dinamico, ma per chiarezza elencheremo alcuni file di esempio.

```csharp
// List the PNG files you want to process
var imagePaths = new List<string>
{
    "YOUR_DIRECTORY/img1.png",
    "YOUR_DIRECTORY/img2.png",
    "YOUR_DIRECTORY/img3.png"
};
```

*Consiglio:* Sostituisci `YOUR_DIRECTORY` con il percorso assoluto o relativo alle tue immagini. Se hai dozzine di file, puoi sostituire l'elenco manuale con `Directory.GetFiles("YOUR_DIRECTORY", "*.png")`.

## Passo 3: OCR batch delle immagini – Eseguire il riconoscimento in parallelo

Elaborare le immagini una dopo l'altra è semplice ma lento. Utilizzando `Parallel.ForEach` possiamo **elaborare più immagini** simultaneamente, sfruttando le CPU multi‑core.

```csharp
// Helper method that performs the parallel recognition
static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
{
    var resultsBag = new ConcurrentBag<OcrResult>();

    Parallel.ForEach(paths, path =>
    {
        // Load the image stream (Aspose handles various formats)
        var image = ImageStream.FromFile(path);
        // Perform OCR
        OcrResult result = engine.Recognize(image);
        // Store the result safely for later use
        resultsBag.Add(result);
    });

    return resultsBag.ToArray();
}

// Execute the parallel OCR
var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);
```

*Perché in parallelo?* Ogni chiamata OCR è intensiva per la CPU ma indipendente, quindi eseguirle contemporaneamente può ridurre drasticamente il tempo totale, soprattutto su una macchina a 4 core o più.

## Passo 4: Elaborare più immagini – Visualizzare il testo estratto

Ora che disponiamo di una collezione di oggetti `OcrResult`, possiamo iterare su di essi e stampare il testo riconosciuto. Qui normalmente salveresti l'output in un database o in file, ma l'output su console mantiene l'esempio conciso.

```csharp
int index = 1;
foreach (var result in ocrResults)
{
    Console.WriteLine($"--- Image {index++} ---");
    Console.WriteLine(result.Text);
}
```

**Output console previsto (esempio):**

```
--- Image 1 ---
Hello world! This is the first image.
--- Image 2 ---
Invoice #12345
Total: $250.00
--- Image 3 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
```

Se qualche immagine non dovesse caricarsi, Aspose genera un'eccezione; puoi avvolgere la chiamata `engine.Recognize` in un blocco try/catch per registrare gli errori senza interrompere l'intero batch.

## Passo 5: Esempio completo – Tutti i pezzi insieme

Di seguito trovi il programma completo che puoi copiare‑incollare in un nuovo progetto console C#. Include tutto, dalle istruzioni `using` al ciclo finale di output.

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new Engine();

        // Step 2: Define the PNG files to process
        var imagePaths = new List<string>
        {
            "YOUR_DIRECTORY/img1.png",
            "YOUR_DIRECTORY/img2.png",
            "YOUR_DIRECTORY/img3.png"
        };

        // Step 3: Run OCR in parallel
        var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);

        // Step 4: Output the recognized text
        int index = 1;
        foreach (var result in ocrResults)
        {
            Console.WriteLine($"--- Image {index++} ---");
            Console.WriteLine(result.Text);
        }
    }

    // Helper method for parallel OCR
    static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
    {
        var resultsBag = new ConcurrentBag<OcrResult>();

        Parallel.ForEach(paths, path =>
        {
            try
            {
                var image = ImageStream.FromFile(path);
                OcrResult result = engine.Recognize(image);
                resultsBag.Add(result);
            }
            catch (Exception ex)
            {
                // Log the error but keep the batch running
                Console.Error.WriteLine($"Error processing {path}: {ex.Message}");
            }
        });

        return resultsBag.ToArray();
    }
}
```

### Eseguire l'esempio

1. Crea un nuovo progetto **Console App** in Visual Studio.  
2. Aggiungi il pacchetto NuGet **Aspose.OCR** (`Install-Package Aspose.OCR`).  
3. Sostituisci `YOUR_DIRECTORY` con il percorso che contiene i tuoi file PNG.  
4. Compila ed esegui – dovresti vedere il testo estratto stampato sulla console.

## Suggerimenti avanzati & casi particolari

- **Accelerazione GPU:** Se disponi di una GPU compatibile e di una licenza Aspose OCR, abilitala tramite `EngineSettings` prima di creare il motore. Questo può ridurre di alcuni secondi il tempo per ogni immagine.  
- **File di grandi dimensioni:** Per immagini superiori a 10 MB, considera di ridimensionarle prima per diminuire la pressione sulla memoria.  
- **Supporto linguistico:** Per impostazione predefinita il motore assume l'inglese. Imposta `engine.Language = Language.French;` (o qualsiasi lingua supportata) per migliorare la precisione su testi non inglesi.  
- **Gestione degli errori:** Il `try/catch` all'interno del ciclo parallelo garantisce che un file corrotto non interrompa l'intero batch. Puoi anche registrare i fallimenti in un file per una revisione successiva.  
- **Memorizzazione dei risultati:** Invece di stampare, potresti scrivere `result.Text` in un file `.txt` usando `File.WriteAllText(Path.ChangeExtension(path, ".txt"))`.

## Conclusione

Ora sai **come usare l'OCR** in C# per **estrarre testo da file PNG**, **eseguire OCR batch sulle immagini** e **elaborare più immagini** in modo efficiente con Aspose OCR C#. La soluzione è completamente autonoma, gira in parallelo e può essere estesa per gestire centinaia o migliaia di file con minime modifiche.

Pronto per il passo successivo? Prova a sostituire l'output console con un report CSV, sperimenta l'accelerazione GPU, o alimenta il testo OCR in un indice di ricerca. Le possibilità sono infinite, e il modello di base—inizializzare una volta, eseguire in parallelo, gestire gli errori con cura—ti sarà utile in qualsiasi pipeline di elaborazione immagini.

Buon coding, e che i tuoi job OCR siano rapidi e privi di errori!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}