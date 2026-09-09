---
category: general
date: 2026-01-09
description: Estrai rapidamente il testo da PNG con Aspose OCR. Scopri come leggere
  il testo delle immagini, migliorare l'accuratezza OCR e ottenere risultati puliti
  in C#.
draft: false
keywords:
- extract text from png
- read image text
- improve ocr accuracy
- extract text from image
- aspose ocr tutorial
language: it
og_description: Estrai rapidamente il testo da PNG con Aspose OCR. Scopri come leggere
  il testo delle immagini, migliorare la precisione OCR e ottenere risultati puliti
  in C#.
og_title: Estrai testo da PNG – Tutorial completo di OCR Aspose
tags:
- Aspose OCR
- C#
- Image Processing
title: Estrai testo da PNG – Tutorial completo di OCR Aspose
url: /it/net/text-recognition/extract-text-from-png-complete-aspose-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrarre testo da PNG – Tutorial completo Aspose OCR

Hai mai dovuto **estrarre testo da file PNG** ma i risultati erano pieni di spazzatura? Non sei solo. In molti progetti reali – fatture, ricevute o moduli scansionati – la qualità dell'output OCR può fare la differenza per le pipeline di automazione.  

In questa guida ti mostreremo un metodo **passo‑a‑passo** per leggere il testo di un'immagine usando Aspose OCR, aggiungere un dizionario personalizzato per **migliorare l'accuratezza OCR**, pulire il rumore e infine stampare una stringa ordinata. Alla fine avrai un'app console C# pronta all'uso che estrae in modo affidabile il testo da immagini PNG.

> **Cosa otterrai**  
> * Un esempio di codice completo e eseguibile.  
> * Una comprensione del perché un dizionario personalizzato è importante.  
> * Suggerimenti per gestire casi particolari come scansioni a basso contrasto.  

## Prerequisiti

- .NET 6 SDK o successivo (il codice è mirato a .NET 6, ma funziona anche con .NET 5).  
- Visual Studio 2022 o qualsiasi editor tu preferisca.  
- Un'immagine **PNG** da elaborare – ad esempio `invoice.png`.  
- Il pacchetto NuGet **Aspose.OCR** (`dotnet add package Aspose.OCR`).  

Non servono file di configurazione aggiuntivi; tutto vive in un unico file `.cs`.

## Passo 1 – Installa e aggiungi riferimento ad Aspose OCR

Per prima cosa, scarica la libreria nel tuo progetto. Apri un terminale nella cartella della soluzione ed esegui:

```bash
dotnet add package Aspose.OCR
```

Questa singola riga recupera l'ultima versione stabile (a gennaio 2026, versione 23.9). Il pacchetto include la classe `OcrEngine` che useremo per tutta la durata del tutorial.

## Passo 2 – Inizializza il motore OCR

Creare un'istanza di `OcrEngine` è la base. Pensala come l'accensione di uno scanner pronto a interpretare i pixel.

```csharp
using Aspose.OCR;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();
```

> **Consiglio:** Se prevedi di elaborare molte immagini in un ciclo, riutilizza la stessa istanza di `OcrEngine`. Essa memorizza in cache le risorse interne e velocizza le chiamate successive.

## Passo 3 – Aumenta l'accuratezza con un dizionario personalizzato

L'OCR di base è buono, ma può inciampare su parole specifiche del dominio come “Aspose”, “OCR” o “SDK”. Aggiungere questi termini a un **dizionario personalizzato** indica al motore che tali stringhe sono valide, riducendo gli errori di riconoscimento.

```csharp
// Define domain‑specific terms that the engine should recognize
ocrEngine.CustomDictionary = new HashSet<string>
{
    "Aspose",
    "OCR",
    "SDK",
    "invoice"
};
```

### Perché un dizionario personalizzato aiuta

- I **modelli statistici** alla base dell'OCR pesano molto i pattern linguistici comuni. Le parole rare hanno bassa probabilità e possono essere sostituite da caratteri simili.  
- Elencandole esplicitamente, sovrascrivi le ipotesi del modello.  
- È particolarmente utile per **leggere testo da immagine** che contiene codici prodotto, abbreviazioni o nomi di brand.

## Passo 4 – Riconosci il testo dal file PNG

Ora forniamo al motore il percorso dell'immagine. Il metodo `RecognizeImage` restituisce una stringa grezza che contiene ancora token sconosciuti (es. “#@!”) che il motore non è riuscito a mappare.

```csharp
// Path to the PNG you want to process
string imagePath = @"YOUR_DIRECTORY/invoice.png";

// Perform OCR
string rawText = ocrEngine.RecognizeImage(imagePath);
```

> **Caso limite:** Se il file non viene trovato, `RecognizeImage` lancia una `FileNotFoundException`. Avvolgi la chiamata in un blocco try‑catch per il codice di produzione.

## Passo 5 – Pulisci il risultato con `CleanText`

Aspose OCR fornisce un helper che rimuove i caratteri contrassegnati come “sconosciuti”. Questo passaggio è cruciale per i progetti **estrarre testo da immagine** dove i parser successivi si aspettano solo caratteri alfanumerici e punteggiatura di base.

```csharp
// Remove unknown tokens and extra whitespace
string cleanedText = ocrEngine.CleanText(rawText);
```

Il metodo `CleanText` normalizza anche le terminazioni di riga, rendendo l'output sicuro da memorizzare in database o da passare ad altri servizi.

## Passo 6 – Stampa il testo pulito

Infine, visualizza o salva il risultato. In un'app console, `Console.WriteLine` fa al caso tuo.

```csharp
Console.WriteLine("=== Cleaned OCR Output ===");
Console.WriteLine(cleanedText);
```

Quando esegui il programma, dovresti vedere un blocco di testo ordinato che rispecchia il contenuto di `invoice.png`. Se l'immagine contiene la parola “Aspose”, il dizionario personalizzato garantisce che appaia correttamente anziché come “A5p0se”.

## Esempio completo funzionante

Mettendo tutto insieme, ecco il file `Program.cs` completo che puoi copiare‑incollare in un nuovo progetto console:

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Add domain‑specific terms to improve OCR accuracy
        ocrEngine.CustomDictionary = new HashSet<string>
        {
            "Aspose",
            "OCR",
            "SDK",
            "invoice"
        };

        // 3️⃣ Path to your PNG file (adjust as needed)
        string imagePath = @"YOUR_DIRECTORY/invoice.png";

        try
        {
            // 4️⃣ Recognize raw text from the image
            string rawText = ocrEngine.RecognizeImage(imagePath);

            // 5️⃣ Clean up unknown tokens
            string cleanedText = ocrEngine.CleanText(rawText);

            // 6️⃣ Show the result
            Console.WriteLine("=== Cleaned OCR Output ===");
            Console.WriteLine(cleanedText);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error processing image: {ex.Message}");
        }
    }
}
```

**Output previsto** (supponendo che il PNG contenga una fattura semplice):

```
=== Cleaned OCR Output ===
Invoice #12345
Date: 01/08/2026
Total: $1,250.00
Thank you for your business!
```

Se vedi simboli strani, ricontrolla la qualità dell'immagine o espandi il dizionario personalizzato con altri termini.

## Bonus: Gestire scansioni di bassa qualità

A volte i PNG sono scansionati a 72 dpi o presentano forti artefatti di compressione. Ecco alcuni trucchi rapidi per **migliorare l'accuratezza OCR** senza abbandonare C#:

1. **Pre‑elabora l'immagine** con una libreria come `SixLabors.ImageSharp` – aumenta il contrasto, converti in scala di grigi o applica una leggera sfocatura per ridurre il rumore.  
2. **Imposta la proprietà `Resolution`** su `OcrEngine` (es. `ocrEngine.Resolution = 300;`) per far capire al motore che l'immagine è ad alta risoluzione.  
3. **Abilita i language pack** se lavori con testo non inglese (`ocrEngine.Language = Language.English;`).

Tutte e tre le soluzioni possono essere aggiunte prima della chiamata a `RecognizeImage`.

## Domande frequenti

- **Funziona con altri formati di immagine?**  
  Sì. `RecognizeImage` accetta JPEG, BMP, TIFF e persino PDF (come contenitore di immagini). Gli stessi passaggi si applicano.

- **Posso estrarre testo da più PNG in una cartella?**  
  Assolutamente. Avvolgi la logica principale in un ciclo `foreach (var file in Directory.GetFiles(folder, "*.png"))` e salva ogni risultato in una lista o in file separati.

- **E se ho bisogno delle coordinate del testo?**  
  Aspose OCR fornisce anche oggetti `OcrResult` che includono le bounding box. Usa `ocrEngine.RecognizeImageToResult(imagePath)` per quello scenario avanzato.

## Conclusione

Abbiamo percorso una soluzione **completa, end‑to‑end** per **estrarre testo da file PNG** usando Aspose OCR. Inizializzando il motore, fornendogli un **dizionario personalizzato**, pulendo l'output grezzo e gestendo alcuni ostacoli comuni, puoi leggere in modo affidabile il testo da immagini e **migliorare l'accuratezza OCR** nelle tue applicazioni C#.

Pronto per il passo successivo? Prova a sostituire il PNG con una ricevuta scansionata, aggiungi altre parole specifiche al dizionario o integra l'output con un database per l'elaborazione automatica delle fatture. Il cielo è il limite quando combini Aspose OCR con l'ecosistema ricco di .NET.

Buona programmazione, e che il tuo OCR sia sempre preciso! 

![Esempio di estrazione testo da png](/images/extract-text-from-png.png "estrazione testo da png – demo Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}