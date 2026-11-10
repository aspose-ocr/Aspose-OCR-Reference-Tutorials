---
category: general
date: 2026-03-17
description: Come eseguire OCR batch di immagini PNG in C# rapidamente. Impara a estrarre
  testo da file PNG, convertire PNG in testo e leggere le immagini da una directory
  con uno script semplice.
draft: false
keywords:
- how to batch OCR
- extract text png
- convert png to text
- read images from directory
language: it
og_description: Come eseguire OCR batch di immagini PNG in C# con codice passo‑passo.
  Estrai testo da file PNG, converti PNG in testo e leggi le immagini dalla directory
  senza sforzo.
og_title: Come eseguire OCR batch di immagini PNG in C# – Guida completa
tags:
- OCR
- C#
- Image Processing
title: Come eseguire OCR batch di immagini PNG in C# – Guida completa
url: /it/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR batch di immagini PNG in C# – Guida completa

Ti sei mai chiesto **come eseguire OCR batch** su una cartella piena di screenshot senza aprire manualmente ogni file? Non sei l'unico—gli sviluppatori chiedono continuamente come eseguire OCR batch su grandi collezioni di PNG, soprattutto quando l'obiettivo è estrarre file PNG di testo per analisi successive.  

In questo tutorial vedremo un esempio pronto‑all'uso in C# che **estrae file PNG di testo**, **converte PNG in testo**, e ti mostra il modo migliore per **leggere immagini da directory**. Alla fine avrai uno script unico che crea un `.txt` accanto a ogni immagine, risparmiandoti ore di copia‑incolla manuale.

## Cosa otterrai

- Inizializzare un motore OCR una sola volta e riutilizzarlo per l'intero batch.  
- Scansionare ogni `*.png` in una cartella specificata senza scrivere un ciclo manualmente.  
- Scrivere ogni risultato OCR in un proprio file di testo, preservando il nome originale del file.  
- Gestire i casi limite comuni, come cartelle vuote o file non‑immagine, in modo corretto.

### Prerequisiti

- .NET 6.0 o successivo (il codice funziona anche su .NET Core e .NET Framework).  
- Una libreria OCR che espone i tipi `OcrEngine`, `ImageStream` e `OcrResult` (ad esempio, il fittizio SDK **FastOCR** usato negli esempi).  
- Conoscenze di base di C#—non sono richiesti pattern avanzati.

---

## Come eseguire OCR batch di immagini PNG – Panoramica

Di seguito trovi il **programma completo e eseguibile**. Sentiti libero di copiarlo‑incollarlo in un nuovo progetto console, sostituire i percorsi segnaposto e premere **F5**.

```csharp
using System;
using System.IO;
using System.Linq;
using FastOCR;               // <-- Replace with your actual OCR namespace

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize the OCR engine (language = English)
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();
        ocrEngine.Config.Language = Language.English;

        // -------------------------------------------------
        // Step 2: Locate every PNG file in the input folder
        // -------------------------------------------------
        string inputFolder = @"YOUR_DIRECTORY\images";
        string[] imagePaths = Directory.GetFiles(inputFolder, "*.png");

        if (imagePaths.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to process.");
            return;
        }

        // -------------------------------------------------
        // Step 3: Convert file paths to ImageStream objects
        // -------------------------------------------------
        var imageStreams = imagePaths
            .Select(path => ImageStream.FromFile(path))
            .ToList();

        // -------------------------------------------------
        // Step 4: Recognize text in the entire batch
        // -------------------------------------------------
        IReadOnlyList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // -------------------------------------------------
        // Step 5: Write each result to a .txt file next to the image
        // -------------------------------------------------
        string outputFolder = @"YOUR_DIRECTORY\output";
        Directory.CreateDirectory(outputFolder); // ensures the folder exists

        for (int i = 0; i < ocrResults.Count; i++)
        {
            string originalFileName = Path.GetFileNameWithoutExtension(imagePaths[i]);
            string outputPath = Path.Combine(outputFolder, $"{originalFileName}.txt");
            File.WriteAllText(outputPath, ocrResults[i].Text);
            Console.WriteLine($"✅ {originalFileName}.txt created");
        }

        Console.WriteLine("All done! Check the output folder for your text files.");
    }
}
```

> **Output previsto:** Per ogni `image01.png` troverai un `image01.txt` contenente i caratteri riconosciuti. La console elencherà ogni file man mano che viene scritto.

![Diagramma di come eseguire OCR batch](how-to-batch-ocr-diagram.png "Diagramma che illustra come eseguire OCR batch di immagini PNG usando C#")

---

## Spiegazione passo‑passo

### 1. Inizializzare il motore OCR – il cuore del processo  

La riga `var ocrEngine = new OcrEngine();` crea un'unica istanza del motore che verrà riutilizzata per l'intero batch. Riutilizzare il motore è **cruciale** perché la maggior parte delle librerie OCR allocano risorse pesanti (come i modelli linguistici) al momento della costruzione. Inizializzare una sola volta migliora drasticamente le prestazioni—soprattutto quando hai decine o centinaia di PNG.

> **Consiglio professionale:** Se hai bisogno di una lingua diversa dall'inglese, imposta `ocrEngine.Config.Language = Language.Spanish;` (o qualsiasi enum supportato).  

### 2. Leggere immagini da directory – individuare ogni PNG  

`Directory.GetFiles(@"YOUR_DIRECTORY\images", "*.png")` fa esattamente ciò che promette la keyword secondaria *leggere immagini da directory*. Restituisce un array di percorsi assoluti, che successivamente passiamo al motore OCR.  

> **Perché non usare `SearchOption.AllDirectories`?** Se le tue immagini sono annidate, puoi passare a `GetFiles(path, "*.png", SearchOption.AllDirectories)`. Ricorda solo che scansioni più profonde potrebbero includere file indesiderati, quindi filtra di conseguenza.

### 3. Convertire i percorsi dei file in oggetti ImageStream  

La maggior parte degli SDK OCR si aspetta uno stream anziché un percorso grezzo. L'espressione LINQ `Select(path => ImageStream.FromFile(path)).ToList()` crea una **lista di stream** che il riconoscitore batch può consumare in una sola chiamata. Questo passaggio garantisce anche che i handle dei file vengano aperti una sola volta, riducendo l'overhead I/O.

> **Caso limite:** Se un file è corrotto, `ImageStream.FromFile` può generare un'eccezione. Avvolgi la conversione in un `try/catch` se hai bisogno di resilienza.

### 4. Riconoscere il testo nell'intero batch  

`ocrEngine.RecognizeBatch(imageStreams)` è il punto ideale per *come eseguire OCR batch*. Invece di iterare su ogni immagine e chiamare un metodo per immagine singola, passiamo l'intera collezione al motore. Internamente la libreria può parallelizzare il lavoro, offrendoti un aumento di velocità su macchine multi‑core.

> **Suggerimento:** Se la tua libreria OCR non espone un metodo batch, puoi comunque ottenere prestazioni simili usando `Parallel.ForEach` attorno alla chiamata `Recognize` per immagine singola.

### 5. Scrivere ogni risultato OCR – convertire PNG in testo  

L'ultimo ciclo `for` scrive `ocrResults[i].Text` in un file `.txt` il cui nome rispecchia il PNG originale. Questo è esattamente ciò che descrive la keyword secondaria *convertire PNG in testo*. La chiamata `Path.Combine` garantisce che la cartella di output esista e previene bug di traversal del percorso.

> **Errore comune:** Dimenticare di creare prima la cartella di output causerà una `DirectoryNotFoundException`. La riga `Directory.CreateDirectory(outputFolder);` risolve preventivamente il problema.

## Gestire variazioni nel mondo reale

| Situazione | Cosa cambiare | Perché |
|------------|---------------|--------|
| **Cartella di input vuota** | Mantieni il controllo iniziale `if (imagePaths.Length == 0)` | Previene una chiamata OCR inutile e fornisce un messaggio amichevole |
| **Tipi di file misti** | Use `Directory.EnumerateFiles(..., "*.*", SearchOption.TopDirectoryOnly).Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase))` | Garantisce di processare solo PNG, soddisfacendo *extract text png* senza errori |
| **Immagini molto grandi ( > 5 MB )** | Downscale before feeding to OCR: `ImageStream.FromFile(path).Resize(1920, 1080)` (if API supports) | Riduce la pressione sulla memoria e spesso migliora l'accuratezza del riconoscimento |
| **Lingua OCR diversa** | Set `ocrEngine.Config.Language = Language.French;` | Allinea il motore alla lingua delle immagini di origine |

## Domande frequenti (FAQ)

**D: Questo funziona con file JPEG o TIFF?**  
R: La logica di base rimane la stessa; basta cambiare il pattern di ricerca in `"*.jpg"` o `"*.tif"` e assicurarsi che la libreria OCR possa decodificare quei formati.

**D: Come posso elaborare migliaia di immagini senza esaurire la memoria?**  
R: Sostituisci la chiamata batch con un approccio di streaming—elabora un blocco di, ad esempio, 50 immagini alla volta, poi rilascia gli stream prima di caricare il blocco successivo.

**D: Ho bisogno del punteggio di confidenza OCR. Dove lo trovo?**  
R: La maggior parte degli oggetti `OcrResult` espone una proprietà `Confidence`. Puoi estendere la fase di scrittura:

```csharp
var result = ocrResults[i];
string content = $"Confidence: {result.Confidence:P2}\n{result.Text}";
File.WriteAllText(outputPath, content);
```

## Conclusione

Abbiamo appena coperto **come eseguire OCR batch** di immagini PNG in C# dall'inizio alla fine. Inizializzando un unico motore, leggendo immagini da directory, convertendole in stream, riconoscendo l'intero batch e infine scrivendo ogni risultato in un file di testo, ora disponi di un modello solido e pronto per la produzione per le attività di **estrarre testo PNG**, **convertire PNG in testo** e **leggere immagini da directory**.

Cosa fare dopo? Prova a cambiare il provider OCR, aggiungi post‑processing multithread (ad esempio, correzione ortografica), o alimenta i file `.txt` in un indice di ricerca. Il cielo è il limite una volta che hai padroneggiato il flusso batch.

Hai un trucco da condividere? Lascia un commento, e buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}