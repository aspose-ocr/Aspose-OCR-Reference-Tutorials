---
category: general
date: 2026-03-28
description: Impara come eseguire OCR batch in C# e convertire facilmente i file TIFF
  in testo. Questa guida passo‑a‑passo mostra come estrarre il testo dai file TIFF
  usando Aspose OCR.
draft: false
keywords:
- how to batch ocr
- convert tiff to text
- extract text from tiff
- c# ocr tutorial
language: it
og_description: Come eseguire OCR batch in C#? Segui questo tutorial completo per
  convertire file TIFF multipagina in testo ricercabile usando Aspose OCR.
og_title: Come eseguire OCR batch in C# – Convertire TIFF multi‑pagina in testo
tags:
- OCR
- C#
- Aspose
title: Come eseguire OCR in batch in C# – Convertire TIFF multi‑pagina in testo
url: /it/net/text-recognition/how-to-batch-ocr-in-c-convert-multi-page-tiff-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR batch in C# – Convertire TIFF multi‑pagina in testo

Ti sei mai chiesto **come eseguire OCR batch** su una pila di pagine scansionate senza scrivere un ciclo per ogni immagine? Non sei l'unico. In molti progetti—pensa all'elaborazione di fatture o alla digitalizzazione di archivi—la necessità di **convertire TIFF in testo** compare quotidianamente, e farlo pagina per pagina diventa rapidamente un incubo.

La buona notizia? Con poche righe di C# e Aspose OCR puoi fornire un intero TIFF multi‑pagina al motore e ottenere un dizionario di numeri di pagina associati alle loro stringhe estratte. In questo tutorial percorreremo un esempio completo e eseguibile che mostra esattamente **come eseguire OCR batch**, come **estrarre testo da TIFF**, e perché questo approccio supera l'alternativa manuale.

## Cosa imparerai

- Configurare la libreria Aspose OCR in un progetto .NET.  
- Caricare un file TIFF multi‑pagina usando `Image.FromMultiPageFile`.  
- Eseguire `RecognizeBatch` per ottenere un `Dictionary<int,string>` dei risultati per pagina.  
- Stampare l'output in un formato pulito e leggibile.  

Al termine avrai un'app console pronta‑da‑eseguire che trasforma qualsiasi TIFF multi‑pagina in testo semplice—senza strumenti aggiuntivi richiesti.  

### Prerequisiti

- .NET 6.0 SDK (o qualsiasi versione recente di .NET).  
- Visual Studio 2022 o VS Code—qualsiasi IDE preferito va bene.  
- Una licenza valida di Aspose OCR o una chiave di valutazione gratuita (l'API funziona senza licenza ma aggiunge una filigrana).  
- Un TIFF multi‑pagina di esempio chiamato `multipage.tif` posizionato in una cartella a cui puoi fare riferimento.

> **Consiglio professionale:** Se sei su Windows, la cartella di progetto predefinita è un luogo comodo dove inserire il TIFF; su Linux/macOS basta regolare il percorso di conseguenza.

## Passo 1: Installare il pacchetto NuGet Aspose OCR

Prima di scrivere qualsiasi codice, abbiamo bisogno della libreria OCR. Apri un terminale nella cartella del tuo progetto ed esegui:

```bash
dotnet add package Aspose.OCR
```

Questo scarica l'ultima versione stabile (a partire da marzo 2026 v23.9) e aggiunge i DLL necessari al tuo progetto. Non è necessaria alcuna configurazione aggiuntiva per una semplice app console.

## Passo 2: Creare lo scheletro dell'applicazione console

Creiamo una struttura minima di programma che fa riferimento al motore OCR. Le direttive `using` sono cruciali—senza di esse il compilatore segnalerà tipi mancanti.

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;   // Required for Image class
```

> **Perché è importante:** La classe `Image` si trova in un sotto‑namespace, e dimenticare l'import `ImageProcessing` ti darà un errore “type or namespace not found” che può far perdere un'ora di debug.

Ora aggiungi il metodo `Main` e un breve commento che descriva lo scopo:

```csharp
/// <summary>
/// Demonstrates how to batch OCR a multi‑page TIFF and output each page's text.
/// </summary>
class BatchOcrTutorial
{
    static void Main()
    {
        // Implementation will go here
    }
}
```

## Passo 3: Inizializzare il motore OCR

Il `OcrEngine` è il cavallo di battaglia. Istanziarlo una sola volta e riutilizzarlo per tutte le pagine è sia efficiente in termini di memoria sia veloce.

```csharp
// Step 3: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

> **Cosa succede dietro le quinte?** Il motore carica i modelli linguistici e pre‑configura le impostazioni predefinite (es., inglese, auto‑rotazione). Puoi modificarle in seguito, ma le impostazioni predefinite sono solide per la maggior parte dei documenti.

## Passo 4: Caricare il TIFF multi‑pagina

Aspose rende il caricamento di immagini multi‑frame semplice. Fornisci il percorso completo o relativo dalla directory di lavoro dell'eseguibile.

```csharp
// Step 4: Load a multi‑page TIFF image
string tiffPath = "YOUR_DIRECTORY/multipage.tif";   // ← replace with your actual path
var multiPageImage = Image.FromMultiPageFile(tiffPath);
```

Se il file non viene trovato, `FromMultiPageFile` lancia una `FileNotFoundException`. Avvolgilo in un `try/catch` se hai bisogno di una gestione degli errori elegante—qualcosa che mostreremo nel passo successivo.

## Passo 5: Eseguire OCR batch

Ora arriva la star dello spettacolo: `RecognizeBatch`. Restituisce un `Dictionary<int,string>` dove la chiave è l'indice della pagina (a partire da 0) e il valore è il testo riconosciuto.

```csharp
// Step 5: Perform batch OCR on all pages
Dictionary<int, string> ocrResults = ocrEngine.RecognizeBatch(multiPageImage);
```

> **Caso limite:** Alcuni TIFF contengono pagine vuote. Aspose restituisce una stringa vuota per quelle pagine, che puoi filtrare in seguito se non vuoi ingombri nell'output.

## Passo 6: Visualizzare i risultati

Infine, itera sul dizionario e stampa il testo di ogni pagina. L'uso di stringhe interpolate mantiene il codice ordinato.

```csharp
// Step 6: Output the recognized text for each page
foreach (var pageResult in ocrResults)
{
    Console.WriteLine($"--- Page {pageResult.Key + 1} ---"); // +1 for human‑friendly numbering
    Console.WriteLine(pageResult.Value);
    Console.WriteLine(); // Blank line for readability
}
```

Eseguire il programma dovrebbe produrre qualcosa del genere:

```
--- Page 1 ---
Invoice #12345
Date: 2024‑12‑01
Total: $1,250.00
...

--- Page 2 ---
Terms and Conditions
...
```

Se vedi output illeggibile, ricontrolla che il TIFF di origine non sia corrotto e che la lingua del testo corrisponda a quella predefinita del motore (inglese). Puoi anche impostare `ocrEngine.Language = OcrLanguage.Spanish;` per documenti non in inglese.

## Esempio completo funzionante

Mettendo insieme tutti i pezzi, ecco il programma completo che puoi copiare‑incollare in `Program.cs` ed eseguire:

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;   // Needed for Image class

/// <summary>
/// Demonstrates how to batch OCR a multi‑page TIFF and output each page's text.
/// </summary>
class BatchOcrTutorial
{
    static void Main()
    {
        try
        {
            // Step 1: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Step 2: Load a multi‑page TIFF image
            string tiffPath = "YOUR_DIRECTORY/multipage.tif";   // Change to your actual file location
            var multiPageImage = Image.FromMultiPageFile(tiffPath);

            // Step 3: Perform batch OCR on all pages
            Dictionary<int, string> ocrResults = ocrEngine.RecognizeBatch(multiPageImage);

            // Step 4: Output the recognized text for each page
            foreach (var pageResult in ocrResults)
            {
                Console.WriteLine($"--- Page {pageResult.Key + 1} ---");
                Console.WriteLine(pageResult.Value);
                Console.WriteLine(); // Extra line for visual separation
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
        }
    }
}
```

Salva, compila ed esegui:

```bash
dotnet run
```

Dovresti vedere il contenuto estratto di ogni pagina stampato sulla console. Questo è l'intero **tutorial OCR in C#** che hai richiesto.

## Domande frequenti e casi limite

### E se il mio TIFF contiene decine di pagine?

`RecognizeBatch` elabora tutti i frame in una singola chiamata, ma l'uso della memoria cresce linearmente con il numero di pagine. Per documenti molto grandi (centinaia di pagine) considera di elaborare a blocchi:

```csharp
for (int i = 0; i < multiPageImage.PageCount; i += 50)
{
    var subImage = multiPageImage.GetPages(i, Math.Min(50, multiPageImage.PageCount - i));
    var partialResults = ocrEngine.RecognizeBatch(subImage);
    // Merge partialResults into the main dictionary...
}
```

### Posso salvare il testo estratto in file invece di stamparlo?

Assolutamente. Sostituisci il blocco `Console.WriteLine` con operazioni di I/O su file:

```csharp
string outputFolder = "ExtractedText";
Directory.CreateDirectory(outputFolder);

foreach (var pageResult in ocrResults)
{
    string filePath = Path.Combine(outputFolder, $"Page_{pageResult.Key + 1}.txt");
    File.WriteAllText(filePath, pageResult.Value);
}
```

Ora ogni pagina ottiene il proprio file `.txt`—perfetto per l'indicizzazione successiva.

### Come modifico la lingua di output o abilito l'auto‑rotazione?

```csharp
ocrEngine.Language = OcrLanguage.French; // or any supported language
ocrEngine.AutoRotate = true;             // Detects rotated text automatically
```

Queste impostazioni devono essere applicate **prima** di chiamare `RecognizeBatch`.

## Conclusione

Abbiamo coperto **come eseguire OCR batch** su un TIFF multi‑pagina usando Aspose OCR in C#. Caricando l'immagine una sola volta, chiamando `RecognizeBatch` e iterando sul dizionario risultante, puoi **convertire TIFF in testo** in pochi secondi. L'esempio mostra anche come **estrarre testo da TIFF**, gestire gli errori e, facoltativamente, scrivere i risultati su file—tutto all'interno di un'app console pulita e autonoma.

Pronto per il passo successivo? Prova a combinare questo approccio con una libreria di generazione PDF per produrre PDF ricercabili, o collega l'output a un database per archivi ricercabili. Puoi anche sperimentare con altri formati immagine (PNG, JPEG) sostituendo `Image.FromMultiPageFile` con `Image.FromFile`.

Hai altre domande su OCR, licenze o ottimizzazione delle prestazioni? Lascia un commento qui sotto, e buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}