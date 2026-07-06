---
category: general
date: 2026-02-17
description: Come eseguire l'OCR batch di più PDF e immagini in C# usando Aspose OCR.
  Impara a estrarre testo da PDF, convertire PDF in testo e riconoscere testo dalle
  immagini.
draft: false
keywords:
- how to batch OCR
- extract text from pdf
- convert pdf to text
- recognize text from images
- extract text scanned pdf
language: it
og_description: Come eseguire l'OCR batch su più documenti in C# con Aspose OCR. Ottieni
  il codice passo‑passo per estrarre il testo da PDF, convertire PDF in testo e riconoscere
  il testo dalle immagini.
og_title: Come eseguire OCR su file in batch in C# – Guida completa
tags:
- OCR
- C#
- Aspose
- PDF
- Text Extraction
title: Come eseguire OCR di file in batch in C# – Esempio di codice completo
url: /it/net/text-recognition/how-to-batch-ocr-files-in-c-full-code-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire l'OCR batch di file in C# – Guida completa

Ti sei mai chiesto **come eseguire l'OCR batch** su una pila di PDF e scansioni di immagini senza scrivere un ciclo separato per ogni file? Non sei solo. La maggior parte degli sviluppatori si imbatte in questo ostacolo quando deve estrarre testo da decine di pagine in un'unica operazione. La buona notizia? Con Aspose OCR puoi fornire una collezione di file a un unico motore e lasciarlo fare il lavoro pesante.  

In questo tutorial percorreremo una soluzione pratica che ti permette di **estrarre testo da pdf**, **convertire pdf in testo** e **riconoscere testo da immagini** tutto in un'unica esecuzione batch. Alla fine avrai un'app console pronta all'uso che stampa il risultato OCR per ogni pagina, e comprenderai il perché di ogni passaggio così da poterlo adattare ai tuoi progetti.

## Prerequisiti – Cosa serve prima di iniziare

- **.NET 6.0 o successivo** (il codice funziona anche su .NET Framework, ma .NET 6+ è consigliato)
- **Pacchetto NuGet Aspose.OCR** – installalo con `dotnet add package Aspose.OCR`
- Un paio di file di esempio: un PDF multipagina (`doc1.pdf`) e un TIFF scansionato (`doc2.tif`). Posizionali in una cartella a cui puoi fare riferimento, ad esempio `C:\OCRSamples`.
- Conoscenze di base di C# – dovresti sentirti a tuo agio con le istruzioni `using` e le collezioni.

> Pro tip: Se non hai una licenza, Aspose offre una chiave temporanea gratuita che rimuove il limite di 100 pagine durante lo sviluppo.

## Passo 1: Configurare il progetto e importare i namespace

Per prima cosa, crea un nuovo progetto console (o aggiungilo a uno esistente) e importa i namespace necessari.

```csharp
// Program.cs
using System;
using System.Collections.Generic;
using Aspose.OCR;          // Aspose OCR core library
using Aspose.OCR.Image;   // ImageStream helper class
```

> **Perché è importante:** Importare `Aspose.OCR.Image` ti fornisce il comodo metodo `ImageStream.FromFile`, che suddivide automaticamente le pagine PDF in stream di immagine separati. Questo è il segreto che rende la lavorazione batch indolore.

## Passo 2: Inizializzare il motore OCR

Il motore è il cavallo di battaglia che comunica con il motore OCR sottostante. Hai bisogno di una sola istanza per l'intero batch.

```csharp
// Step 2: Create a single OcrEngine instance
OcrEngine ocrEngine = new OcrEngine();
```

> **Spiegazione:** Riutilizzare lo stesso `OcrEngine` riduce il churn di memoria e velocizza l'elaborazione perché le librerie native rimangono caricate tra le pagine.

## Passo 3: Costruire una lista di stream di immagine

Qui raccogliamo tutti i documenti che vogliamo elaborare. `ImageStream.FromFile` è sufficientemente intelligente da suddividere un PDF in pagine individuali, così un PDF a tre pagine diventa tre stream separati dietro le quinte.

```csharp
// Step 3: Assemble the collection of image streams
List<ImageStream> imageStreams = new List<ImageStream>
{
    ImageStream.FromFile(@"C:\OCRSamples\doc1.pdf"),
    ImageStream.FromFile(@"C:\OCRSamples\doc2.tif")
};
```

> **Caso limite:** Se hai una combinazione di PDF, TIFF, JPEG o PNG, aggiungili semplicemente alla stessa lista – Aspose gestisce automaticamente il rilevamento del formato.

## Passo 4: Eseguire l'operazione OCR batch

Ora passiamo la lista al motore. `RecognizeBatch` restituisce una collezione di oggetti `OcrResult`, uno per pagina.

```csharp
// Step 4: Perform batch OCR on the supplied streams
IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

> **Perché batch?** Eseguire l'OCR pagina per pagina in un ciclo manuale costringe il motore a reinizializzarsi ogni volta, il che può raddoppiare i tempi di elaborazione. `RecognizeBatch` mantiene il motore “caldo” e restituisce i risultati man mano che sono disponibili.

## Passo 5: Stampare il testo riconosciuto

Infine, cicliamo sui risultati e scriviamo il testo di ogni pagina sulla console. Qui puoi sostituire `Console.WriteLine` con scritture su file, inserimenti in database o qualsiasi altra azione a valle.

```csharp
// Step 5: Display the OCR output for each page
for (int pageIndex = 0; pageIndex < ocrResults.Count; pageIndex++)
{
    Console.WriteLine($"--- Page {pageIndex + 1} ---");
    Console.WriteLine(ocrResults[pageIndex].Text);
}
```

### Output console previsto

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore...
--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation...
```

Se esegui il programma con i file di esempio, dovresti vedere un blocco di testo per ogni pagina, dimostrando che hai **estratto testo da pdf scansionato** con successo in un'unica passata.

## Gestione dei problemi comuni

| Problema | Perché accade | Soluzione rapida |
|----------|----------------|-------------------|
| **Errori di out‑of‑memory** | I PDF di grandi dimensioni generano molte immagini ad alta risoluzione. | Limita il DPI durante il caricamento dei PDF: `ocrEngine.Settings.ImageDpi = 200;` |
| **Caratteri spazzatura** | La scansione di origine è di bassa qualità o usa una lingua non supportata. | Imposta esplicitamente la lingua: `ocrEngine.Language = Language.English;` |
| **Risultati parziali** | La lista batch contiene un file corrotto. | Avvolgi `RecognizeBatch` in un try/catch e registra `e.Message` per il file problematico. |
| **Collo di bottiglia delle prestazioni** | Esecuzione su thread singolo su una macchina multicore. | Usa `Parallel.ForEach` con istanze separate di `OcrEngine` per thread (avanzato). |

## Bonus: Salvare i risultati OCR in file di testo

Se preferisci mantenere un file `.txt` separato per pagina, aggiungi un piccolo blocco di scrittura all'interno del ciclo:

```csharp
string outputPath = @"C:\OCRResults";
System.IO.Directory.CreateDirectory(outputPath);

for (int i = 0; i < ocrResults.Count; i++)
{
    string fileName = System.IO.Path.Combine(outputPath, $"Page_{i + 1}.txt");
    System.IO.File.WriteAllText(fileName, ocrResults[i].Text);
}
```

Ora hai trasformato **convertire pdf in testo** in una cartella ordinata di file di testo semplice—perfetta per indicizzazione o ricerca successive.

## Esempio completo funzionante

Di seguito trovi il programma completo, pronto per il copia‑incolla. Nessuna dipendenza nascosta, nessuno script esterno.

```csharp
// FullProgram.cs
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // Initialise OCR engine (reuse for the whole batch)
        OcrEngine ocrEngine = new OcrEngine();

        // Optional: tweak settings for speed or accuracy
        ocrEngine.Settings.ImageDpi = 200;          // lower memory usage
        ocrEngine.Language = Language.English;     // set language explicitly

        // Build the list of image streams (PDF pages auto‑split)
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"C:\OCRSamples\doc1.pdf"),
            ImageStream.FromFile(@"C:\OCRSamples\doc2.tif")
        };

        // Perform batch OCR
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Output each page's text to console
        for (int pageIndex = 0; pageIndex < ocrResults.Count; pageIndex++)
        {
            Console.WriteLine($"--- Page {pageIndex + 1} ---");
            Console.WriteLine(ocrResults[pageIndex].Text);
        }

        // (Optional) Save each page to a .txt file
        string outputFolder = @"C:\OCRResults";
        System.IO.Directory.CreateDirectory(outputFolder);
        for (int i = 0; i < ocrResults.Count; i++)
        {
            string txtPath = System.IO.Path.Combine(outputFolder, $"Page_{i + 1}.txt");
            System.IO.File.WriteAllText(txtPath, ocrResults[i].Text);
        }
    }
}
```

Esegui `dotnet run` dalla cartella del progetto e osserva la console riempirsi del testo estratto. Questo è **come eseguire l'OCR batch** su una collezione di documenti in poche righe di C#.

## Cosa abbiamo coperto – Riepilogo veloce

- Configurare un'app console .NET e installare Aspose.OCR.  
- Creare un'unica istanza di `OcrEngine` per mantenere il processo efficiente.  
- Costruire una lista di oggetti `ImageStream` che suddividono automaticamente i PDF in pagine.  
- Eseguire `RecognizeBatch` per **estrarre testo da pdf** e altri formati immagine in un'unica operazione.  
- Stampare i risultati e, facoltativamente, salvarli come file `.txt` individuali, completando il flusso di lavoro **convertire pdf in testo**.  

## Prossimi passi e argomenti correlati

- **Scalare**: Usa `Parallel.ForEach` con un pool di oggetti `OcrEngine` per processare centinaia di file in parallelo.  
- **Pacchetti lingua**: Sostituisci `Language.English` con `Language.French` o carica un dizionario personalizzato quando devi **riconoscere testo da immagini** in altre lingue.  
- **Post‑processing**: Invia l'output OCR a un correttore ortografico o a un parser di linguaggio naturale per migliorare l'accuratezza su contratti scansionati.  
- **Librerie alternative**: Confronta Aspose OCR con Tesseract.NET se cerchi un'opzione open‑source—entrambi possono **estrarre testo da pdf scansionato** ma differiscono per licenza e precisione out‑of‑the‑box.

---

![how to batch OCR example](alt="how to batch OCR example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}