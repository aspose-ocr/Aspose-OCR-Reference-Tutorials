---
category: general
date: 2026-05-25
description: Converti TIFF in testo usando Aspose.OCR in C#. Impara la conversione
  batch di immagini in testo ed estrai il testo dai file TIFF in modo efficiente.
draft: false
keywords:
- convert tiff to text
- extract text from tiff
- batch image to text conversion
- convert scanned images txt
language: it
og_description: Converti TIFF in testo con Aspose.OCR. Questa guida mostra la conversione
  batch di immagini in testo e come estrarre il testo da file TIFF in poche righe
  di C#.
og_title: Converti TIFF in testo in C# – Guida completa all'OCR batch
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Convert TIFF to text using Aspose.OCR in C#. Learn batch image to text
    conversion and extract text from TIFF files efficiently.
  headline: Convert TIFF to Text in C# – Complete Batch OCR Guide
  type: TechArticle
- description: Convert TIFF to text using Aspose.OCR in C#. Learn batch image to text
    conversion and extract text from TIFF files efficiently.
  name: Convert TIFF to Text in C# – Complete Batch OCR Guide
  steps:
  - name: '**Create** an OCR engine set for English.'
    text: '**Create** an OCR engine set for English.'
  - name: '**Collect** every TIFF file from the target folder.'
    text: '**Collect** every TIFF file from the target folder.'
  - name: '**Run** `BatchOcr.RecognizeAll` with four threads, turning each image into
      a string.'
    text: '**Run** `BatchOcr.RecognizeAll` with four threads, turning each image into
      a string.'
  - name: '**Loop** over the results, swapping the `.tif` extension for `.txt` and
      writing the string to disk.'
    text: '**Loop** over the results, swapping the `.tif` extension for `.txt` and
      writing the string to disk.'
  type: HowTo
tags:
- C#
- OCR
- Aspose
- TIFF
title: Converti TIFF in Testo con C# – Guida Completa all'OCR Batch
url: /it/net/text-recognition/convert-tiff-to-text-in-c-complete-batch-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertire TIFF in Testo in C# – Guida Completa all'OCR in Batch

Ti è mai capitato di dover **convertire TIFF in testo** ma non sapevi da dove cominciare? Non sei solo—molti sviluppatori si imbattono nell'OCR batch quando lavorano con documenti scansionati. In questo tutorial ti guideremo passo passo attraverso una soluzione pratica che **estrae testo da file TIFF** usando Aspose.OCR, e lo faremo in parallelo così le cartelle grandi terminano in pochi secondi.

Tratteremo anche le migliori pratiche per la **conversione batch di immagini in testo**, così alla fine avrai uno snippet riutilizzabile che trasforma un'intera directory di immagini scansionate in ordinati file *.txt*—perfetti per indicizzare, cercare o alimentare analisi successive.

## Cosa Ti Serve

- **.NET 6.0** o versioni successive (il codice compila anche su .NET Framework)  
- **Aspose.OCR for .NET** NuGet package (`Install-Package Aspose.OCR`)  
- Una cartella contenente uno o più file *.tif* (il classico formato di scansione TIFF)  
- Il tuo IDE preferito (Visual Studio, VS Code, Rider—quello che preferisci)

È tutto. Nessun servizio esterno, nessuna chiave API, solo puro C# e Aspose.

![Screenshot di un file TIFF in elaborazione e del file di testo risultante](/images/ocr-result.png "Risultato OCR che mostra l'output del TIFF convertito in testo")

*(Testo alternativo: Screenshot che mostra l'output del TIFF convertito in testo sullo schermo)*

## Passo 1: Configurare il Motore OCR – Convertire TIFF in Testo

Prima di tutto, abbiamo bisogno di un'istanza di `OcrEngine` che sappia leggere caratteri inglesi. Il motore è il cuore della conversione; configurarlo correttamente garantisce risultati affidabili.

```csharp
using Aspose.OCR;
using System.IO;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Create an OCR engine configured for English – this is the core of convert TIFF to text
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English
        };
```

*Perché è importante:*  
Aspose.OCR supporta decine di lingue. Se lavori con scansioni multilingue, basta cambiare `OcrLanguage.English` con il valore enum appropriato. Lasciare la lingua non definita costringe il motore in modalità auto‑rilevamento, che può essere più lenta e meno accurata.

## Passo 2: Raccogliere Tutti i File TIFF – Estrarre Testo da TIFF in Modo Efficiente

Successivamente raccogliamo tutti i file *.tif* da una cartella specificata. Usare `Directory.GetFiles` ci fornisce un array pulito da passare al processore batch.

```csharp
        // Locate every TIFF in the input folder – adjust the path to your own directory
        string inputFolder = @"C:\Scans\Batch";
        string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif", SearchOption.TopDirectoryOnly);

        if (tiffFiles.Length == 0)
        {
            System.Console.WriteLine("No TIFF files found. Check the folder path.");
            return;
        }
```

*Consiglio professionale:* Il flag `SearchOption.AllDirectories` può essere usato se le tue scansioni sono annidate in sottocartelle. Ricorda solo che una ricorsione più profonda può aumentare l'uso di memoria durante il passaggio batch.

## Passo 3: Eseguire OCR in Parallelo – Conversione Batch di Immagini in Testo

Ora la parte divertente. Aspose.OCR fornisce un helper statico `BatchOcr.RecognizeAll` che accetta un array di percorsi file, un motore e un suggerimento `parallelism`. Avvieremo quattro thread, che su un laptop moderno quad‑core offrono un'accelerazione quasi lineare.

```csharp
        // Run OCR on all files in parallel (4 threads by default)
        // The result is a dictionary where Key = file path, Value = extracted text
        Dictionary<string, string> ocrResults = BatchOcr.RecognizeAll(tiffFiles, ocrEngine, parallelism: 4);
```

*Perché il parallelismo?*  
Scansionare un batch di TIFF ad alta risoluzione può richiedere molta CPU. Distribuendo il lavoro su più thread manteniamo tutti i core occupati, riducendo drasticamente il tempo totale di esecuzione. Se lo esegui su un server con più core, aumenta di conseguenza il valore `parallelism`.

## Passo 4: Scrivere l'Output – Convertire le Immagini Scansionate in File TXT

Infine iteriamo sul dizionario e scriviamo ogni blocco di testo in un file *.txt* che condivide il nome base originale. Questo è il momento in cui **convert scanned images txt** diventa realtà.

```csharp
        // Save each recognized text to a .txt file with the same base name as the source TIFF
        foreach (var kvp in ocrResults)
        {
            string sourcePath = kvp.Key;
            string extractedText = kvp.Value;

            // Change extension from .tif to .txt
            string txtPath = Path.ChangeExtension(sourcePath, ".txt");

            // Write the text – UTF‑8 ensures all characters are preserved
            File.WriteAllText(txtPath, extractedText);
            System.Console.WriteLine($"Saved: {txtPath}");
        }

        System.Console.WriteLine("Batch conversion complete!");
    }
}
```

### Cosa fa il codice, in italiano semplice

1. **Crea** un motore OCR impostato per l'inglese.  
2. **Raccogli** ogni file TIFF dalla cartella di destinazione.  
3. **Esegui** `BatchOcr.RecognizeAll` con quattro thread, trasformando ogni immagine in una stringa.  
4. **Itera** sui risultati, sostituendo l'estensione `.tif` con `.txt` e scrivendo la stringa su disco.

Questo è l'intero flusso di lavoro per **convertire TIFF in testo** in meno di 50 righe di codice.

## Gestire i Casi Limite – Quando le Cose Non Vanno Liscie

- **TIFF mancanti o corrotti** – `BatchOcr` solleverà un `OcrException`. Avvolgi la chiamata in un `try / catch` se hai bisogno di una degradazione graduale.  
- **Documenti non‑inglesi** – cambia `OcrLanguage.English` in `OcrLanguage.Spanish`, `OcrLanguage.French`, ecc., o usa `OcrLanguage.AutoDetect`.  
- **Immagini molto grandi** – considera di ridurre il DPI prima dell'OCR (`ocrEngine.ImagePreprocessing.Dpi = 200`) per risparmiare memoria, anche se potresti perdere un po' di precisione.  
- **Codifica dell'output** – se ti serve una pagina di codice specifica (es., Windows‑1252), passala a `File.WriteAllText(txtPath, extractedText, Encoding.GetEncoding(1252))`.

## Consigli Pro per Conversioni Batch Affidabili

- **Registra i fallimenti**: crea una `List<string> failedFiles` e aggiungi ogni file che genera un'eccezione; scrivi la lista in un log dopo il ciclo.  
- **Riutilizza il motore**: la stessa istanza di `OcrEngine` può essere riutilizzata per molti file; non istanziarla dentro il ciclo.  
- **Valida il risultato**: un rapido `if (string.IsNullOrWhiteSpace(extractedText))` può segnalare scansioni vuote o illeggibili.  
- **Combina con PDF**: se la tua sorgente è un PDF multi‑pagina, converti prima ogni pagina in TIFF (Aspose.PDF lo fa) e poi esegui questo batch.

## Prossimi Passi – Oltre la Semplice Conversione

Ora che puoi **estrarre testo da TIFF** in blocco, potresti voler:

- Inserire i file *.txt* in un indice di ricerca (Elasticsearch, Azure Cognitive Search).  
- Eseguire il rilevamento della lingua su ogni risultato per indirizzare i documenti a pipeline specifiche per locale.  
- Generare PDF ricercabili sovrapponendo il testo OCR alle immagini originali (di nuovo Aspose.PDF).  

Tutti questi scenari si basano sulla stessa idea fondamentale: **la conversione batch di immagini in testo** è un blocco fondamentale per sistemi di elaborazione documenti più grandi.

---

### Conclusione

Hai appena imparato come **convertire TIFF in testo** usando Aspose.OCR, elaborare un'intera cartella in parallelo e salvare ogni risultato in un pulito file *.txt*. La soluzione è leggera, completamente configurabile e pronta per la produzione—che tu stia digitalizzando fatture legacy, archiviando contratti scansionati o alimentando un motore di ricerca testuale.

Provala, regola il parallelismo e inizia a inserire questi nuovi file di testo nel flusso di lavoro di cui hai bisogno. Buon OCR!

---

## Tutorial Correlati

- [Estrarre Testo da Immagini Usando l'Operazione OCR su Cartelle](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Estrarre Testo da Immagine – Ottimizzazione OCR con Aspose.OCR per .NET](/ocr/english/net/ocr-optimization/)
- [Estrarre testo da immagine C# con selezione della lingua usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}