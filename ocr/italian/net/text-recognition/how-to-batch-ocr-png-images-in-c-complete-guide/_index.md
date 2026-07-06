---
category: general
date: 2026-04-26
description: Come eseguire OCR batch di immagini PNG rapidamente. Impara a estrarre
  il testo da PNG, convertire le immagini in testo, scrivere il testo riconosciuto
  e leggere la directory PNG con Aspose OCR.
draft: false
keywords:
- how to batch OCR
- extract text from png
- convert images to text
- write recognized text
- read png directory
language: it
og_description: Come eseguire l'OCR batch di immagini PNG in C# con Aspose OCR. Questa
  guida mostra come estrarre il testo da PNG, convertire le immagini in testo e scrivere
  il testo riconosciuto in modo efficiente.
og_title: Come eseguire OCR batch su immagini PNG in C# – Passo dopo passo
tags:
- OCR
- C#
- Aspose
title: Come eseguire OCR in batch di immagini PNG in C# – Guida completa
url: /it/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR batch di immagini PNG in C# – Guida completa

Ti sei mai chiesto **come eseguire OCR batch** su un'intera cartella di file PNG senza dover scrivere un programma separato per ogni immagine? Non sei l'unico a gestire decine di screenshot, ricevute scannerizzate o grafiche che devono essere trasformate in testo ricercabile. In questo tutorial vedremo una soluzione pratica che **estrae testo da PNG**, **converte le immagini in testo** e **scrive il testo riconosciuto** in file individuali—tutto leggendo automaticamente la directory dei PNG.

Al termine di questa guida avrai un'app console C# pronta all'uso che elabora qualsiasi numero di immagini in un solo colpo. Nessuno script aggiuntivo, nessun copia‑incolla manuale—solo codice puro che fa il lavoro pesante per te.

## Cosa ti serve

- **.NET 6.0** o successivo (il codice funziona anche su .NET Framework).  
- Pacchetto NuGet **Aspose.OCR for .NET** (la versione di prova gratuita è sufficiente per i test).  
- Una cartella con un certo numero di file *.png* da sottoporre a OCR.  
- Visual Studio 2022 o qualsiasi IDE C# tu preferisca.

Se hai tutto questo, possiamo passare subito all'implementazione.

## Passo 1 – Prepara le cartelle di input e output *(Leggi la directory PNG)*

La prima cosa da fare è indicare al programma la cartella che contiene le immagini e decidere dove verranno salvati i file *.txt* risultanti. Usare `Directory.GetFiles` ci fornisce un enumerabile pulito di tutti i PNG nella directory.

```csharp
using System;
using System.Collections.Generic;
using System.IO;

// Define where the source PNGs are and where the OCR results will be saved
string inputFolder = @"C:\MyProject\BatchImages";   // <-- change to your path
string outputFolder = @"C:\MyProject\BatchOutput";

// Ensure the output folder exists; create it if it doesn’t
if (!Directory.Exists(outputFolder))
{
    Directory.CreateDirectory(outputFolder);
}

// Grab every *.png* file – this is the “read png directory” part
IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
```

**Perché è importante:**  
- L'uso di un wildcard (`*.png`) garantisce che vengano elaborate solo le immagini, ignorando eventuali documenti sparsi.  
- Creare la cartella di output al volo evita una `DirectoryNotFoundException` in seguito.

> **Consiglio esperto:** Se devi supportare altri formati (JPEG, BMP), estendi semplicemente il pattern di ricerca o chiama `Directory.EnumerateFiles` con più estensioni.

## Passo 2 – Inizializza il motore OCR *(Converti le immagini in testo)*

Aspose.OCR fornisce due tipi di motore: un `OcrEngine` basato su CPU e un `GpuOcrEngine` accelerato da GPU. Per la maggior parte dei batch il motore CPU è più che sufficiente, ma puoi cambiare il nome della classe se disponi di una GPU adeguata.

```csharp
using Aspose.OCR;

// Initialise the OCR engine – CPU version
OcrEngine ocrEngine = new OcrEngine();   // Use new GpuOcrEngine() for GPU acceleration

// Set the language to Latin (covers English, French, Spanish, etc.)
ocrEngine.Language = Language.Latin;
```

**Perché è importante:**  
- Specificare la lingua migliora notevolmente l'accuratezza perché il motore sa quale set di caratteri aspettarsi.  
- Passare a `GpuOcrEngine` è una modifica di una sola riga se incontri colli di bottiglia di prestazioni su batch di grandi dimensioni.

## Passo 3 – Crea un Batch Recogniser

Aspose mette a disposizione un comodo `BatchRecognizer` che accetta un enumerabile di percorsi file e restituisce i risultati uno alla volta. Questo evita di caricare tutte le immagini in memoria contemporaneamente—un dettaglio cruciale per cartelle molto grandi.

```csharp
// Build a batch recogniser that will use the previously configured engine
BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);
```

**Perché è importante:**  
- Il batch recogniser incapsula la logica del ciclo, permettendoci di concentrarci su cosa fare con ogni risultato anziché su come iterare in modo sicuro.

## Passo 4 – Esegui OCR su tutte le immagini e scrivi l'output *(Scrivi il testo riconosciuto)*

Ora eseguiamo effettivamente l'OCR. Il metodo `Recognize` restituisce un `IEnumerable<RecognitionResult>` dove ogni risultato contiene il testo estratto e altri metadati.

```csharp
// Perform OCR on the entire collection of PNG files
IEnumerable<RecognitionResult> recognitionResults = batchRecognizer.Recognize(inputImageFiles);

// Write each recognised text to a separate *.txt* file
int fileIndex = 0;
foreach (RecognitionResult result in recognitionResults)
{
    // Build a unique output filename – out_0.txt, out_1.txt, …
    string outputPath = Path.Combine(outputFolder, $"out_{fileIndex++}.txt");

    // Save the plain text to disk
    File.WriteAllText(outputPath, result.Text);
}
```

**Perché è importante:**  
- Usare `File.WriteAllText` garantisce che il testo venga salvato con codifica UTF‑8 per impostazione predefinita, preservando i caratteri speciali.  
- La numerazione incrementale (`out_0.txt`, `out_1.txt`) corrisponde all'ordine di elaborazione, utile per il debug.

> **Caso limite:** Se qualche immagine non riesce a passare l'OCR (ad es. file corrotto), `RecognitionResult.Text` sarà vuoto. Puoi aggiungere un semplice controllo all'interno del ciclo per registrare i fallimenti:

```csharp
if (string.IsNullOrWhiteSpace(result.Text))
{
    Console.WriteLine($"Warning: No text extracted from {inputImageFiles.ElementAt(fileIndex - 1)}");
}
```

## Passo 5 – Metti tutto insieme – Esempio completo funzionante

Di seguito trovi il programma completo da copiare‑incollare in un nuovo progetto console. Include le direttive `using`, la validazione delle cartelle e una piccola UI console così sai quando il batch è terminato.

```csharp
// ---------------------------------------------------------------
// Batch OCR for PNG files using Aspose.OCR
// ---------------------------------------------------------------
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Define input & output directories
        string inputFolder = @"C:\MyProject\BatchImages";   // <-- adjust
        string outputFolder = @"C:\MyProject\BatchOutput";

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"Error: Input folder does not exist -> {inputFolder}");
            return;
        }

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ Gather all PNG files
        IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
        Console.WriteLine($"Found {inputImageFiles?.Count() ?? 0} PNG files to process.");

        // 3️⃣ Initialise OCR engine (CPU) and set language
        OcrEngine ocrEngine = new OcrEngine();   // Swap with GpuOcrEngine() if needed
        ocrEngine.Language = Language.Latin;

        // 4️⃣ Create batch recogniser
        BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);

        // 5️⃣ Run OCR and write results
        IEnumerable<RecognitionResult> results = batchRecognizer.Recognize(inputImageFiles);
        int index = 0;
        foreach (RecognitionResult result in results)
        {
            string outPath = Path.Combine(outputFolder, $"out_{index++}.txt");
            File.WriteAllText(outPath, result.Text);
        }

        Console.WriteLine($"✅ OCR complete! Text files saved to {outputFolder}");
    }
}
```

**Output previsto:**  
L'esecuzione del programma stampa qualcosa del genere:

```
Found 12 PNG files to process.
✅ OCR complete! Text files saved to C:\MyProject\BatchOutput
```

E vedrai `out_0.txt` … `out_11.txt` nella cartella di output, ognuno contenente la versione di testo semplice dell'immagine corrispondente.

## Domande frequenti & Suggerimenti

| Domanda | Risposta |
|----------|----------|
| *Posso eseguire OCR anche su sottocartelle?* | Sì—sostituisci `Directory.GetFiles` con `Directory.EnumerateFiles(inputFolder, "*.png", SearchOption.AllDirectories)`. |
| *E se ho bisogno di un'altra lingua?* | Imposta `ocrEngine.Language = Language.Spanish;` (o qualsiasi enum supportato). |
| *Come gestire batch enormi (migliaia di file)?* | Considera di elaborare a blocchi o usa `Parallel.ForEach` con un grado di parallelismo limitato per evitare di esaurire la memoria. |
| *L'output è sempre UTF‑8?* | `File.WriteAllText` usa UTF‑8 senza BOM di default, il che funziona per la maggior parte delle lingue latine. Per script asiatici potresti dover impostare esplicitamente `Encoding.UTF8`. |
| *Posso ottenere i punteggi di confidenza?* | `RecognitionResult` espone `Confidence`—puoi registrarlo insieme al testo per il controllo di qualità. |

## Panoramica visiva *(Come eseguire OCR batch – Diagramma)*

![Diagramma del flusso di lavoro OCR batch che mostra cartella di input → motore OCR → batch recogniser → file txt di output](https://example.com/diagram-how-to-batch-ocr.png "Come eseguire OCR batch")

*Il testo alternativo contiene la parola chiave principale, soddisfacendo i requisiti SEO per le immagini.*

## Conclusioni

Abbiamo appena coperto **come eseguire OCR batch** su una directory di file PNG usando Aspose.OCR, dalla lettura della directory PNG alla scrittura di ogni file di testo riconosciuto. La soluzione è completamente autonoma, funziona su qualsiasi runtime .NET moderno e può essere estesa per accelerazione GPU, supporto multilingua o elaborazione parallela.

Pronto per il passo successivo? Prova a sostituire `Language.Latin` con un'altra lingua, oppure integra l'output in un indice di ricerca così i tuoi documenti diventano immediatamente ricercabili. Il cielo è il limite una volta che hai padroneggiato l'OCR batch.

Buon coding, e fammi sapere nei commenti se incontri difficoltà!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}