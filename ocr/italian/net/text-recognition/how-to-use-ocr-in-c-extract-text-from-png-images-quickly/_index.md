---
category: general
date: 2026-03-29
description: Come utilizzare l'OCR con Aspose per estrarre testo da file PNG e convertire
  le immagini in testo. Impara l'OCR asincrono passo‑passo in C#.
draft: false
keywords:
- how to use OCR
- extract text from png
- convert images to text
- extract text from images
language: it
og_description: Come utilizzare l'OCR con Aspose in C# per estrarre testo da file
  PNG. Questa guida ti accompagna passo passo nell'OCR asincrono, nel codice e nei
  consigli.
og_title: Come usare l'OCR in C# – Estrarre testo da immagini PNG
tags:
- OCR
- C#
- Aspose
title: Come utilizzare l'OCR in C# – Estrai rapidamente il testo dalle immagini PNG
url: /it/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-png-images-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come usare OCR in C# – Estrarre testo da immagini PNG rapidamente

Ti sei mai chiesto **come usare OCR** per estrarre testo da un piccolo numero di screenshot PNG? Forse hai ricevute scannerizzate, fatture o mock‑up UI e ti serve quel testo in un formato ricercabile. La buona notizia? Con Aspose.OCR puoi convertire le immagini in testo con poche righe di codice C# asincrono.  

In questo tutorial ti mostreremo esattamente come estrarre testo da file PNG, spiegheremo perché ogni passaggio è importante e ti forniremo un programma pronto all'uso che stampa il testo riconosciuto per ogni pagina. Alla fine sarai in grado di **estrarre testo dalle immagini** senza dover setacciare la documentazione.

## Cosa imparerai

- Installa e aggiungi riferimento al pacchetto NuGet Aspose.OCR.  
- Inizializza il motore OCR e imposta la lingua (English in questo esempio).  
- Fornisci un array di file PNG a `RecognizeImagesAsync` per un'elaborazione veloce e non bloccante.  
- Itera sugli oggetti `OcrResult` e stampa le stringhe estratte.  

Nessun servizio esterno, nessuna callback complicata—solo C# async pulito che funziona su .NET 6+.

---

## Prerequisiti

| Requisito | Motivo |
|-------------|--------|
| .NET 6 SDK (or later) | Funzionalità linguistiche moderne come `async Main`. |
| Visual Studio 2022 or VS Code | IDE per compilare ed eseguire il codice. |
| Aspose.OCR NuGet package (`Aspose.OCR`) | Fornisce la classe `OcrEngine` usata nell'esempio. |
| A few PNG images (`page1.png`, `page2.png`, …) | File di input per il processo OCR. |

Se hai già un progetto .NET, esegui semplicemente `dotnet add package Aspose.OCR`. Altrimenti crea una nuova app console con `dotnet new console -n OcrDemo`.

---

## Passo 1: Installa Aspose.OCR e configura il progetto

First, add the OCR library to your project:

```bash
dotnet add package Aspose.OCR
```

Perché è importante: Aspose.OCR include il motore OCR nativo, i pacchetti lingua e una API semplice. Ottenerlo tramite NuGet garantisce la compatibilità delle versioni e aggiornamenti automatici.

---

## Passo 2: Inizializza il motore OCR e scegli una lingua

Il motore deve sapere quale lingua cercare. L'inglese è la più comune, ma puoi sostituire `Language.Spanish`, `Language.French`, ecc.

```csharp
using Aspose.OCR;

// ...

// Step 2: Create the engine and set the language to English
var ocrEngine = new OcrEngine
{
    Language = Language.English   // Change this if you need a different language
};
```

> **Suggerimento professionale:** Imposta sempre la lingua esplicitamente; lasciarla al valore predefinito può ridurre l'accuratezza e aumentare i tempi di elaborazione.

---

## Passo 3: Prepara l'elenco dei file PNG

Puoi fornire un singolo file o un array. Fornire un array consente al motore di elaborarli in batch in modo asincrono, ideale per un piccolo numero di pagine.

```csharp
// Step 3: Define the image files you want to process
string[] imagePaths = { "page1.png", "page2.png", "page3.png" };
```

Se le tue immagini si trovano in una sottocartella, basta anteporre il percorso relativo (`"images/page1.png"`). Il motore lancerà una chiara `FileNotFoundException` se un percorso è errato—quindi ricontrolla i nomi dei file.

---

## Passo 4: Esegui OCR asincrono su tutte le immagini

Il metodo `RecognizeImagesAsync` restituisce un array di `OcrResult`. Poiché è async, la tua UI (o console) rimane reattiva mentre l'OCR viene eseguito in background.

```csharp
// Step 4: Perform async OCR on every image
OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);
```

**Perché async?**  
Se integri OCR in una web API o in un'app desktop, non vuoi che il thread si blocchi mentre il motore analizza ogni pixel. `await` rilascia il thread al pool, migliorando la scalabilità.

---

## Passo 5: Visualizza il testo estratto per ogni pagina

Ora che abbiamo i risultati, iteriamo su di essi e stampiamo il testo riconosciuto. La proprietà `Text` contiene l'output in plain‑text, pronto per ulteriori elaborazioni (ad esempio, salvataggio in un database).

```csharp
// Step 5: Output the recognized text for every page
for (int i = 0; i < ocrResults.Length; i++)
{
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(ocrResults[i].Text);
}
```

### Output previsto

Supponendo che `page1.png` contenga “Invoice #12345” e `page2.png` contenga “Total: $89.99”, vedrai qualcosa del genere:

```
--- Page 1 ---
Invoice #12345
Date: 03/28/2026
--- Page 2 ---
Total: $89.99
Paid by: Credit Card
```

Se l'OCR non riesce a trovare alcun testo, la proprietà `Text` sarà una stringa vuota—gestisci questo caso nel codice di produzione controllando `string.IsNullOrWhiteSpace`.

---

## Esempio completo funzionante

Di seguito trovi il programma completo che puoi copiare‑incollare in `Program.cs`. Include tutte le direttive using, l'`async Main`, e commenti che chiariscono ogni passaggio.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    // Async Main is supported from C# 7.1 onward
    static async Task Main()
    {
        // Step 1: Initialize the OCR engine and set the language to English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Step 2: Define the image files to be processed
        string[] imagePaths = { "page1.png", "page2.png", "page3.png" };

        // Step 3: Perform asynchronous OCR on all images
        OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);

        // Step 4: Output the recognized text for each page
        for (int i = 0; i < ocrResults.Length; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].Text);
        }
    }
}
```

Salva il file, posiziona i tuoi PNG accanto all'eseguibile (o regola i percorsi), e esegui:

```bash
dotnet run
```

Dovresti vedere il testo estratto stampato sulla console, confermando che hai convertito con successo le **immagini in testo**.

---

## Gestione dei casi limite comuni

| Situazione | Cosa fare |
|-----------|------------|
| **Low‑resolution PNG** | Aumenta `ocrEngine.ImageProcessingOptions.Dpi` prima del riconoscimento. |
| **Multiple languages** | Imposta `ocrEngine.Language = Language.English | Language.Spanish;` (OR bitwise). |
| **Large batch (hundreds of files)** | Elabora in blocchi (ad es., 20 file per chiamata a `RecognizeImagesAsync`) per evitare picchi di memoria. |
| **Need the confidence score** | Usa `ocrResults[i].Confidence` (un float tra 0 e 1) per filtrare i risultati di bassa qualità. |

Queste regolazioni mantengono la tua pipeline OCR robusta, soprattutto quando passi da una demo a produzione.

---

## Bonus: Salvataggio dei risultati in un file di testo

Se preferisci una copia persistente anziché l'output console, aggiungi un piccolo helper:

```csharp
using System.IO;

// After the for‑loop:
File.WriteAllLines("OcrOutput.txt", ocrResults.Select(r => r.Text));
Console.WriteLine("All pages saved to OcrOutput.txt");
```

Ora hai un unico file che **estrae testo dalle immagini** per l'elaborazione successiva—perfetto per indicizzare, cercare o alimentare un modello linguistico.

---

## Conclusione

Abbiamo illustrato **come usare OCR** in C# con Aspose per **estrarre testo da file PNG** e **convertire immagini in testo** in modo efficiente. L'approccio async garantisce che la tua applicazione rimanga reattiva, mentre l'API semplice mantiene il codice leggibile e manutenibile.  

Provalo con i tuoi documenti, sperimenta con lingue diverse, e magari collega l'output a un indice di ricerca o a un servizio di sintesi. Il cielo è il limite quando puoi trasformare affidabilmente le immagini in stringhe ricercabili.

---

### Prossimi passi e argomenti correlati

- **Estrai testo dalle immagini** in altri formati (JPEG, TIFF) – basta cambiare le estensioni dei file.  
- **Elaborazione batch con Parallel.ForEach** per carichi di lavoro massivi.  
- **Pulizia post‑OCR** usando espressioni regolari per normalizzare date, importi o ID.  
- **Integra con Azure Cognitive Services** se ti serve OCR basato su cloud con funzionalità aggiuntive.  

Sentiti libero di lasciare un commento se incontri problemi, o condividi come hai esteso questo flusso di base. Buon coding!   (Image: ![OCR result screenshot showing extracted text](/images/ocr-result.png){.align-center alt="esempio di output di come usare OCR"} )

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}