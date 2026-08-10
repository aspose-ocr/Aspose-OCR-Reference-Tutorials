---
category: general
date: 2026-06-25
description: Il tutorial di elaborazione OCR batch mostra come convertire le immagini
  in testo ed estrarre testo dalle immagini utilizzando Aspose.OCR in C#. Scopri l'implementazione
  passo‑passo.
draft: false
keywords:
- batch ocr processing
- convert images to text
- how to extract text from images
language: it
og_description: L'elaborazione OCR batch in C# ti consente di convertire rapidamente
  le immagini in testo. Segui questa guida per imparare come estrarre il testo dalle
  immagini con Aspose.OCR.
og_title: Elaborazione OCR batch in C# – Converti le immagini in testo
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Batch OCR processing tutorial shows how to convert images to text and
    extract text from images using Aspose.OCR in C#. Learn step‑by‑step implementation.
  headline: Batch OCR Processing in C# – Convert Images to Text Quickly
  type: TechArticle
- description: Batch OCR processing tutorial shows how to convert images to text and
    extract text from images using Aspose.OCR in C#. Learn step‑by‑step implementation.
  name: Batch OCR Processing in C# – Convert Images to Text Quickly
  steps:
  - name: Expected Output
    text: 'When you run `dotnet run`, you’ll see something like:'
  - name: What image formats are supported?
    text: Aspose.OCR handles JPEG, PNG, TIFF, BMP, and GIF out of the box. If you
      encounter a format like WebP, convert it first or use a third‑party decoder.
  - name: Can I limit the OCR language to English only?
    text: 'Yes. Set the `Language` property on the `BatchRecognizer` before calling
      `Recognize`:'
  - name: How do I process thousands of files without blowing up memory?
    text: Break the list into smaller batches (e.g., 500 files each) and run the above
      routine in a loop. This keeps the in‑memory dictionary manageable and lets you
      log progress per batch.
  - name: What if I need the OCR results in a database instead of files?
    text: 'Replace the `File.WriteAllText` call with your preferred data‑access code.
      For example, using Dapper:'
  type: HowTo
tags:
- OCR
- Aspose
- C#
title: Elaborazione OCR batch in C# – Converti rapidamente le immagini in testo
url: /it/net/text-recognition/batch-ocr-processing-in-c-convert-images-to-text-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Elaborazione OCR in batch in C# – Converti le immagini in testo rapidamente

Ti sei mai chiesto come fare **batch OCR processing** su un'intera cartella di scansioni senza scrivere un ciclo separato per ogni file? Non sei l'unico. In molti progetti—pensa all'automazione delle fatture, all'archiviazione di vecchi documenti, o anche a una semplice utility personale foto‑a‑testo—hai bisogno di **convertire le immagini in testo** su larga scala.  

La buona notizia? Con Aspose.OCR puoi fare esattamente questo in poche righe. Questa guida ti accompagna passo passo attraverso un esempio completo, pronto‑da‑eseguire, che mostra **come estrarre testo dalle immagini** usando l'elaborazione OCR in batch, spiega perché ogni elemento è importante e ti offre consigli per evitare gli errori più comuni.

## Cosa imparerai

- Configurare Aspose.OCR per operazioni batch.
- Configurare il parallelismo per velocizzare i lavori di grandi dimensioni.
- Scrivere i risultati OCR in file `.txt` individuali automaticamente.
- Gestire gli eventi di avanzamento in modo da sapere sempre cosa sta succedendo.
- Estendere il codice per una gestione personalizzata degli errori o per formati di output diversi.

Non è necessaria alcuna esperienza pregressa con Aspose; basta una conoscenza di base di C# e .NET 6 (o successivo) installato.

---

## Passo 1: Preparare il progetto per l'elaborazione OCR in batch

Prima di immergerci nel codice, assicurati di avere il pacchetto NuGet Aspose.OCR. Apri un terminale nella cartella del tuo progetto ed esegui:

```bash
dotnet add package Aspose.OCR
```

> **Consiglio:** Usa l'ultima versione stabile (a giugno 2026 è la 23.9) per ottenere miglioramenti delle prestazioni e il supporto linguistico più recente.

Crea una nuova app console se non ne hai già una:

```bash
dotnet new console -n BatchOcrApp
cd BatchOcrApp
```

Ora sei pronto per scrivere la logica effettiva dell'elaborazione OCR in batch.

## Passo 2: Definire i file immagine da convertire

Il primo elemento del **batch OCR processing** è semplicemente indicare al riconoscitore quali file gestire. Puoi codificare una lista, leggere da una directory o persino estrarre i percorsi da un database. Per chiarezza useremo una lista statica:

```csharp
// Step 2: List of image files to be processed
var imageFiles = new List<string>
{
    @"C:\Images\invoice1.jpg",
    @"C:\Images\receipt2.png",
    @"C:\Images\scan3.tif"
};
```

> **Perché è importante:** Passando una collezione, il `BatchRecognizer` può programmare internamente il lavoro su più thread, il che è il fulcro delle operazioni rapide di **convertire le immagini in testo**.

## Passo 3: Creare e configurare il BatchRecognizer

Ora arriva il cuore del tutorial. La classe `BatchRecognizer` astrae i dettagli del threading per te. Puoi modificare la proprietà `Parallelism` per adattarla al numero di core della tua CPU o a un valore personalizzato se vuoi lasciare alcuni core liberi per altri compiti.

```csharp
// Step 3: Initialise the BatchRecognizer with optional settings
var ocrBatch = new BatchRecognizer
{
    // Number of concurrent threads (default = Environment.ProcessorCount)
    Parallelism = 4,

    // Optional: Hook into progress events for real‑time feedback
    ProgressChanged = (s, e) =>
        Console.WriteLine($"Processed {e.Completed}/{e.Total} – {e.CurrentFile}")
};
```

> **Spiegazione:** Impostare `Parallelism = 4` indica alla libreria di eseguire quattro job OCR contemporaneamente. Su un tipico laptop quad‑core questo offre un buon incremento di velocità senza saturare il sistema. Se lo esegui su un server con molti core, aumenta questo valore.

> **Caso limite:** Se stai elaborando immagini estremamente grandi, potresti raggiungere i limiti di memoria. In tal caso, riduci il parallelismo o elabora i file in blocchi più piccoli.

## Passo 4: Eseguire l'OCR e catturare i risultati

Chiamare `Recognize` sul `BatchRecognizer` restituisce un dizionario dove la chiave è il percorso originale del file e il valore è un `OcrResult` contenente il testo estratto, i punteggi di confidenza e altro.

```csharp
// Step 4: Execute batch OCR – returns a map of file → OcrResult
IDictionary<string, OcrResult> ocrResults = ocrBatch.Recognize(imageFiles);
```

> **Cosa ottieni:** Per ogni immagine, `OcrResult.Text` contiene la rappresentazione in testo semplice. Questo è esattamente ciò di cui hai bisogno quando vuoi **come estrarre testo dalle immagini** in modo programmatico.

## Passo 5: Salvare ogni risultato in un file .txt

La maggior parte degli scenari reali richiede di salvare l'output OCR per un'elaborazione successiva—magari inserirlo in un indice di ricerca o allegarlo a un record di database. Il ciclo seguente scrive un file `.txt` accanto a ciascuna immagine sorgente, preservando il nome file originale.

```csharp
// Step 5: Write each OCR result to a corresponding .txt file
foreach (var entry in ocrResults)
{
    string txtPath = Path.ChangeExtension(entry.Key, ".txt");
    File.WriteAllText(txtPath, entry.Value.Text);
    Console.WriteLine($"Saved OCR text to {txtPath}");
}
```

> **Suggerimento:** Se ti serve un formato diverso (JSON, CSV, ecc.), basta serializzare `entry.Value` come preferisci. L'oggetto `OcrResult` espone anche `Confidence` e `PageCount` se queste metriche ti sono utili.

## Passo 6: Segnalare il completamento e gestire gli errori in modo elegante

Una conclusione pulita rende la tua utility più professionale. Il codice di esempio stampa già una riga finale, ma aggiungiamo un blocco try‑catch per mostrare eventuali eccezioni inattese, come file mancanti o formati immagine non supportati.

```csharp
try
{
    // (All steps 2‑5 go here)
    Console.WriteLine("Batch OCR processing finished successfully.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during batch OCR processing: {ex.Message}");
}
```

> **Perché avvolgerlo:** Quando esegui il programma su una cartella grande, un'immagine corrotta potrebbe altrimenti interrompere l'intero lavoro. Con una corretta gestione degli errori puoi registrare il problema e continuare con i file rimanenti.

## Esempio completo, pronto‑da‑eseguire

Di seguito trovi il programma completo che puoi copiare‑incollare in `Program.cs`. Assicurati che i percorsi delle immagini puntino a file reali sulla tua macchina.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class BatchExample
{
    static void Main()
    {
        try
        {
            // Step 2: Define the image files to be processed
            var imageFiles = new List<string>
            {
                @"C:\Images\invoice1.jpg",
                @"C:\Images\receipt2.png",
                @"C:\Images\scan3.tif"
            };

            // Step 3: Create a BatchRecognizer and configure optional settings
            var ocrBatch = new BatchRecognizer
            {
                // Set the degree of parallelism (default = Environment.ProcessorCount)
                Parallelism = 4,

                // Hook into progress events to monitor processing
                ProgressChanged = (s, e) =>
                    Console.WriteLine($"Processed {e.Completed}/{e.Total} – {e.CurrentFile}")
            };

            // Step 4: Run OCR on the batch of images (returns file → OcrResult)
            IDictionary<string, OcrResult> ocrResults = ocrBatch.Recognize(imageFiles);

            // Step 5: Write each OCR result to a corresponding .txt file
            foreach (var entry in ocrResults)
            {
                string txtPath = Path.ChangeExtension(entry.Key, ".txt");
                File.WriteAllText(txtPath, entry.Value.Text);
                Console.WriteLine($"Saved OCR text to {txtPath}");
            }

            // Step 6: Indicate that batch processing has completed
            Console.WriteLine("Batch OCR processing finished successfully.");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during batch OCR processing: {ex.Message}");
        }
    }
}
```

### Output previsto

Quando esegui `dotnet run`, vedrai qualcosa di simile:

```
Processed 1/3 – C:\Images\invoice1.jpg
Saved OCR text to C:\Images\invoice1.txt
Processed 2/3 – C:\Images\receipt2.png
Saved OCR text to C:\Images\receipt2.txt
Processed 3/3 – C:\Images\scan3.tif
Saved OCR text to C:\Images\scan3.txt
Batch OCR processing finished successfully.
```

Ogni file `.txt` ora contiene la versione in testo semplice della sua immagine corrispondente—esattamente ciò di cui hai bisogno per **convertire le immagini in testo** su larga scala.

---

## Domande frequenti e casi limite

### Quali formati immagine sono supportati?

Aspose.OCR gestisce JPEG, PNG, TIFF, BMP e GIF nativamente. Se incontri un formato come WebP, converti prima l'immagine o usa un decoder di terze parti.

### Posso limitare la lingua OCR solo all'inglese?

Sì. Imposta la proprietà `Language` sul `BatchRecognizer` prima di chiamare `Recognize`:

```csharp
ocrBatch.Language = "en";
```

Limitare la lingua può migliorare accuratezza e velocità, specialmente quando ti interessa solo **come estrarre testo dalle immagini** in una singola lingua.

### Come elaborare migliaia di file senza esaurire la memoria?

Dividi la lista in batch più piccoli (ad esempio, 500 file ciascuno) ed esegui la routine sopra in un ciclo. Questo mantiene il dizionario in memoria gestibile e ti permette di registrare l'avanzamento per batch.

### E se ho bisogno dei risultati OCR in un database invece che in file?

Sostituisci la chiamata `File.WriteAllText` con il tuo codice di accesso ai dati preferito. Ad esempio, usando Dapper:

```csharp
connection.Execute(
    "INSERT INTO OcrResults (FilePath, Text) VALUES (@Path, @Text)",
    new { Path = entry.Key, Text = entry.Value.Text });
```

## Conclusione

Hai appena padroneggiato **l'elaborazione OCR in batch** in C# con Aspose.OCR, imparato un modo pulito per **convertire le immagini in testo**, e scoperto diversi consigli pratici su **come estrarre testo dalle immagini** in modo efficiente. L'intero flusso di lavoro—raccogliere i percorsi dei file, configurare un `BatchRecognizer`, eseguire l'OCR e salvare i risultati—entra in un unico programma facile da leggere.

Cosa fare dopo? Prova ad aumentare `Parallelism` su un server multicore, sperimenta con i language pack, o aggiungi post‑processing come il controllo ortografico. Potresti anche esplorare l'inserimento del testo estratto in Azure Cognitive Search per rendere i tuoi documenti scansionati ricercabili in pochi secondi.

Hai un'idea da condividere—magari OCR di PDF o gestione di TIFF multipagina? Lascia un commento qui sotto, e continuiamo la discussione. Buona programmazione!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Estrai testo dalle immagini usando l'operazione OCR su cartelle](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Come eseguire OCR in batch su immagini con List in Aspose.OCR per .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Come estrarre testo da archivi ZIP usando Aspose.OCR per .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}