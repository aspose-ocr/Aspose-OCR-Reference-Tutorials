---
category: general
date: 2026-02-16
description: Scopri come eseguire l'OCR in C# usando Aspose.OCR – riconosci il testo
  da una foto, leggi il testo da una scansione e estrai il testo da una ricevuta con
  alta precisione.
draft: false
keywords:
- how to perform OCR
- recognize text from photo
- read text from scan
- extract text from receipt
- improve OCR accuracy
language: it
og_description: Scopri come eseguire l'OCR in C# con Aspose.OCR. Questa guida ti mostra
  come riconoscere il testo da una foto, leggere il testo da una scansione e estrarre
  il testo da una ricevuta.
og_title: Come eseguire l'OCR in C# – Guida completa di Aspose
tags:
- C#
- Aspose.OCR
- Image Processing
title: Come eseguire l'OCR in C# – Guida completa di Aspose
url: /it/net/text-recognition/how-to-perform-ocr-in-c-complete-aspose-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR in C# – Guida completa Aspose

Ti sei mai chiesto **come eseguire OCR** su una ricevuta sfocata o su una foto casuale scattata con il tuo telefono? Non sei l'unico. In molte applicazioni reali dobbiamo **riconoscere testo da foto**, **leggere testo da documenti scannerizzati**, o **estrarre testo da immagini di ricevute** senza inviare i dati a un servizio cloud.  

In questo tutorial passeremo in rassegna un esempio autonomo che ti mostra **come eseguire OCR** con Aspose.OCR, e inseriremo consigli su come **migliorare l'accuratezza OCR** lungo il percorso. Alla fine avrai un programma console C# pronto all'uso che estrae testo semplice da qualsiasi immagine a cui lo indirizzi.

> **Cosa ti servirà**  
> * .NET 6 SDK (o qualsiasi versione recente di .NET)  
> * Pacchetto NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
> * Un'immagine di esempio – ad esempio una foto di una ricevuta chiamata `photo_receipt.jpg`  

Se ti suona familiare, ottimo – immergiamoci.

![esempio di come eseguire OCR](image.png){alt="come eseguire OCR"}

## Come eseguire OCR con Aspose.OCR in C#

Il primo passo è configurare il motore OCR e caricare un modello linguistico inglese. Questo è il fulcro di **come eseguire OCR** con Aspose; senza un modello linguistico il motore non saprebbe quali caratteri cercare.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Load the English language model – change this if you need another language
ocrEngine.LoadLanguage(LanguageModel.English);
```

*Perché è importante*: Caricare il modello linguistico corretto influisce direttamente sulla velocità e sull'accuratezza del riconoscimento. L'inglese è il caso più comune, ma Aspose fornisce decine di altri modelli se mai avrai bisogno di **leggere testo da documenti scannerizzati** in francese, tedesco, ecc.

## Riconoscere testo da foto

Le foto scattate con un telefono spesso presentano rotazione, rumore o basso contrasto. Prima di chiedere al motore di **riconoscere testo da foto**, configuriamo alcune opzioni di pre‑elaborazione che puliscono l'immagine.

```csharp
// Configure preprocessing to boost OCR results
PreprocessingOptions preprocessingOptions = new PreprocessingOptions
{
    Deskew = true,                     // Auto‑correct rotation (helps with tilted receipts)
    Denoise = DenoiseLevel.Medium,    // Reduce graininess
    Binarize = BinarizeMethod.Otsu,   // Convert to black‑and‑white for sharper edges
    ContrastEnhancement = true        // Boost contrast for faint characters
};

// Apply the preprocessing configuration
ocrEngine.Preprocessing = preprocessingOptions;
```

*Consiglio professionale*: Se noti caratteri mancanti, prova a impostare `DenoiseLevel` su `High` o a usare `BinarizeMethod.Sauvola`. Queste modifiche fanno parte delle strategie per **migliorare l'accuratezza OCR**.

## Leggere testo da scansione

Ora che il motore è pronto, carichiamo l'immagine. Che si tratti di una pagina PDF scannerizzata salvata come JPEG o di una foto di un modulo stampato, il codice rimane lo stesso.

```csharp
// Load the image you want to process
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/photo_receipt.jpg");
```

Se hai uno `Stream` invece di un percorso file, sostituisci semplicemente `FromFile` con `FromStream`. Questa flessibilità è utile quando **leggi testo da scansioni** di immagini provenienti da un caricamento web.

## Estrarre testo da ricevuta

Con tutto configurato, la chiamata OCR reale è una singola riga. Il metodo restituisce la stringa di testo semplice estratta, che possiamo quindi visualizzare, memorizzare o inviare a un altro sistema.

```csharp
// Perform OCR and capture the result
string extractedText = ocrEngine.Recognize();

// Output the text to the console
Console.WriteLine("=== OCR RESULT ===");
Console.WriteLine(extractedText);
```

**Output previsto** (esempio per una semplice ricevuta):

```
=== OCR RESULT ===
Store: CoffeeShop
Date: 2024-02-15
Item      Qty   Price
Latte      2    4.50
Bagel      1    2.75
Total            7.25
```

Se l'output appare confuso, rivedi la sezione di pre‑elaborazione – è il punto più comune per **migliorare l'accuratezza OCR**.

## Migliorare l'accuratezza OCR – Ottimizzazioni avanzate

Mentre le impostazioni predefinite funzionano per molti casi, le pipeline di livello produzione spesso richiedono cure aggiuntive:

| Situazione | Regolazione | Motivo |
|-----------|------------|--------|
| Sfondo molto scuro | `ContrastEnhancement = true` + `Binarize = BinarizeMethod.Sauvola` | Aumenta la separazione tra testo e sfondo |
| Note scritte a mano | `ocrEngine.LoadLanguage(LanguageModel.EnglishHandwritten)` | Modello specializzato per tratti corsivi |
| Scansioni multi‑pagina | Loop over each page image and call `Recognize()` per iteration | Mantiene basso l'utilizzo di memoria |
| Immagini grandi (> 2000 px) | Resize before feeding to OCR (`Image.Resize(width, height)`) | Elaborazione più veloce, meno consumo di memoria |

Ricorda, **come eseguire OCR** non è una ricetta universale – sperimenterai spesso con queste impostazioni finché l'output non soddisfa il tuo livello di qualità.

## Esempio completo funzionante

Di seguito trovi il programma completo, pronto per il copia‑incolla. Include tutti gli elementi di cui abbiamo parlato, più un piccolo helper che verifica se il file esiste prima di tentare di leggerlo.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine and load language
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.LoadLanguage(LanguageModel.English);

        // 2️⃣ Set up preprocessing to improve OCR accuracy
        ocrEngine.Preprocessing = new PreprocessingOptions
        {
            Deskew = true,
            Denoise = DenoiseLevel.Medium,
            Binarize = BinarizeMethod.Otsu,
            ContrastEnhancement = true
        };

        // 3️⃣ Path to the image – change this to your own file
        string imagePath = Path.Combine("YOUR_DIRECTORY", "photo_receipt.jpg");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"⚠️  Image not found: {imagePath}");
            return;
        }

        // 4️⃣ Load the image (recognize text from photo / read text from scan)
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // 5️⃣ Perform OCR – this is the core of how to perform OCR
        string extractedText = ocrEngine.Recognize();

        // 6️⃣ Show the result – you can now extract text from receipt, invoice, etc.
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(extractedText);
    }
}
```

Esegui il programma con `dotnet run`. Se tutto è configurato correttamente vedrai il testo estratto stampato sulla console.

## Domande comuni e casi particolari

**D: Cosa succede se l'immagine è un PDF?**  
R: Converti prima ogni pagina PDF in un'immagine (ad esempio, usando `Aspose.Pdf` o `PdfSharp`) e poi passa il bitmap risultante a `ocrEngine.Image`.

**D: Posso elaborare le immagini in parallelo?**  
R: Sì, ma istanzia un `OcrEngine` separato per thread. Il motore non è thread‑safe, quindi condividere un'unica istanza può causare condizioni di gara.

**D: Funziona su Linux?**  
R: Assolutamente. Aspose.OCR è cross‑platform; assicurati solo che le dipendenze native siano installate (`libgdiplus` per .NET Core su Linux).

**D: Come gestisco le ricevute multilingue?**  
R: Carica più modelli linguistici prima del riconoscimento:  
```csharp
ocrEngine.LoadLanguage(LanguageModel.English);
ocrEngine.LoadLanguage(LanguageModel.Spanish);
```  
Il motore proverà ogni modello in ordine.

## Conclusione

Ora hai una risposta solida, end‑to‑end, a **come eseguire OCR** in C# con Aspose.OCR. Il tutorial ha coperto tutto, dall'inizializzazione del motore, **riconoscere testo da foto**, **leggere testo da scansioni**, a **estrarre testo da ricevute**, e ti ha fornito metodi pratici per **migliorare l'accuratezza OCR**.  

Passi successivi? Prova a sostituire il modello inglese con uno scritto a mano, sperimenta valori diversi di `BinarizeMethod`, o integra la chiamata OCR in un'API ASP.NET che elabora i caricamenti al volo. Le possibilità sono ampie quanto le immagini che le fornisci.

Hai altre domande su OCR, pre‑elaborazione delle immagini o le librerie Aspose? Lascia un commento o esplora la documentazione ufficiale di Aspose.OCR per approfondimenti. Buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}