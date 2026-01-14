---
category: general
date: 2026-01-13
description: come correggere l'inclinazione di un'immagine e rimuovere il rumore in
  C# – impara ad aumentare il contrasto dell'immagine, preelaborare l'OCR dell'immagine
  e applicare più filtri.
draft: false
keywords:
- how to deskew image
- remove image noise
- increase image contrast
- preprocess image ocr
- multiple image filters
language: it
og_description: come raddrizzare un'immagine e rimuovere il rumore dell'immagine in
  C# – impara ad aumentare il contrasto dell'immagine, preelaborare l'OCR dell'immagine
  e applicare più filtri immagine
og_title: come raddrizzare un'immagine – Guida completa al pre‑processing C# per OCR
tags:
- OCR
- C#
- Image Processing
title: come correggere l'inclinazione dell'immagine – Guida completa al pre‑processing
  in C# per OCR
url: /it/net/skew-angle-calculation/how-to-deskew-image-complete-c-pre-processing-guide-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# come raddrizzare un'immagine – Guida completa di pre‑elaborazione C# per OCR

Ti sei mai chiesto **come raddrizzare un'immagine** prima di passarla a un motore OCR? Non sei l’unico. In molti scenari reali—contratti scansionati, ricevute o vecchie fotocopie—il testo è leggermente inclinato, l’immagine appare granulosa e il contrasto è irregolare. La buona notizia? Alcune righe di codice C# possono raddrizzare quell’inclinazione, rimuovere il rumore dell’immagine e aumentare il contrasto, fornendo una solida base al tuo OCR.

In questo tutorial percorreremo un **esempio completo e eseguibile** che mostra esattamente come raddrizzare un’immagine, rimuovere il rumore, aumentare il contrasto e poi eseguire l’OCR con Aspose.OCR. Alla fine avrai una pipeline riutilizzabile che applica **più filtri immagine** in una singola chiamata fluida—senza congetture.

## Cosa ti serve

- **.NET 6+** (o qualsiasi versione recente di .NET; l’API funziona allo stesso modo)
- Pacchetto NuGet **Aspose.OCR for .NET** (`Aspose.OCR` e `Aspose.OCR.Filters`)
- Un’immagine di esempio scansionata (ad es. `skewed_noisy.png`) che presenti inclinazione, rumore e basso contrasto
- Il tuo IDE preferito (Visual Studio, Rider, VS Code—scegli quello che ti è più comodo)

Se hai già un progetto impostato, aggiungi semplicemente il riferimento NuGet:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Filters
```

> **Consiglio pratico:** Aspose offre una prova gratuita con numero di pagine limitato—perfetta per provare il codice qui sotto.

## Passo 1: Creare l’istanza del motore OCR

La prima cosa che facciamo è istanziare un `OcrEngine`. Pensalo come il cervello che leggerà il testo in seguito. Niente di complicato, ma è la pietra angolare per tutto ciò che seguirà.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new OcrEngine();
```

> **Perché è importante:** Inizializzare il motore una sola volta e riutilizzarlo per molte immagini evita il sovraccarico di caricare ripetutamente i dati della lingua.

## Passo 2: Caricare l’immagine scansionata grezza

Successivamente carichiamo l’immagine dal disco. Il metodo `OcrImage.FromFile` legge il file in un formato che Aspose può manipolare.

```csharp
        // Step 2: Load the raw scanned image (skewed, noisy, low‑contrast)
        var rawImage = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png");
```

> **Caso limite:** Se la tua immagine è in un formato non standard (TIFF, BMP), Aspose la gestisce comunque, ma potresti volerla convertire in PNG prima per coerenza.

## Passo 3: Costruire una pipeline di pre‑elaborazione (Deskew → Denoise → Contrast)

Qui rispondiamo alla domanda centrale **come raddrizzare un’immagine** rimuovendo anche **il rumore dell’immagine** e **aumentando il contrasto**. L’API fluida di Aspose consente di concatenare i filtri, facendo leggere il codice come una frase.

```csharp
        // Step 3: Apply Deskew, Denoise, and Contrast filters in one pipeline
        var processedImage = rawImage
            .ApplyFilter(new DeskewFilter())      // Corrects rotation
            .ApplyFilter(new DenoiseFilter())     // Reduces grainy artifacts
            .ApplyFilter(new ContrastFilter());   // Boosts foreground/background separation
```

### Cosa fa ciascun filtro

| Filtro | Scopo | Impatto tipico |
|--------|-------|----------------|
| **DeskewFilter** | Rileva l’angolo delle linee di testo e ruota l’immagine per renderle orizzontali. | Elimina l’inclinazione che confonde l’OCR, riducendo spesso i tassi di errore del 30‑50 %. |
| **DenoiseFilter** | Applica un algoritmo di smoothing che preserva i bordi scartando il rumore casuale dei pixel. | Pulisce ricevute scansionate o foto in condizioni di scarsa illuminazione, rendendo i caratteri più chiari. |
| **ContrastFilter** | Allunga l’istogramma così le aree scure diventano più scure e quelle chiare più luminose. | Migliora la distinzione tra testo e sfondo, particolarmente utile per documenti sbiaditi. |

> **Perché concatenarli?** Raddrizzare per primo garantisce che il denoiser lavori su un’immagine correttamente orientata; aumentare il contrasto per ultimo fa risaltare il testo pulito per il motore OCR.

## Passo 4: Eseguire l’OCR sull’immagine elaborata

Ora che l’immagine è dritta, pulita e ad alto contrasto, la passiamo al motore OCR. Useremo i dati della lingua inglese, ma Aspose supporta oltre 150 lingue.

```csharp
        // Step 4: Recognize text using the English language pack
        var ocrResult = ocrEngine.Recognize(processedImage, OcrLanguage.English);
```

Se ti serve un’altra lingua, sostituisci semplicemente `OcrLanguage.English` con il valore enum appropriato (ad es. `OcrLanguage.Spanish`).

## Passo 5: Restituire il testo riconosciuto

Infine, stampiamo il risultato sulla console. In un’applicazione reale potresti scriverlo su file, su un database o alimentare il testo a pipeline NLP successive.

```csharp
        // Step 5: Display the recognized text
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

### Output previsto

Eseguendo il programma completo su una tipica ricevuta inclinata otterrai qualcosa di simile:

```
Invoice #12345
Date: 2025‑12‑31
Total: $1,234.56
Thank you for your business!
```

Se l’output appare illeggibile, ricontrolla l’immagine originale—eccessiva sfocatura o oscurità estrema potrebbero richiedere pre‑elaborazioni aggiuntive (ad es. un `SharpenFilter`).

![esempio di come raddrizzare l'immagine](images/deskewed_example.png "come raddrizzare l'immagine – prima e dopo l'elaborazione")

*L’immagine sopra mostra la scansione originale inclinata a sinistra e la versione corretta, denoisata e ad alto contrasto a destra.*

## Suggerimenti aggiuntivi e problemi comuni

### 1. Quando l’angolo di inclinazione è estremo

Se il documento è inclinato più di 30°, il `DeskewFilter` potrebbe avere difficoltà. In tal caso, ruota manualmente l’immagine in anticipo:

```csharp
var manuallyRotated = rawImage.Rotate(45); // rotates 45 degrees clockwise
var processed = manuallyRotated.ApplyFilter(new DeskewFilter());
```

### 2. Gestione delle immagini a colori

I filtri operano internamente in scala di grigi, ma puoi forzare una conversione:

```csharp
var grayImage = rawImage.ConvertToGrayscale();
var processed = grayImage.ApplyFilter(new DeskewFilter());
```

### 3. Regolare la forza del denoise

`DenoiseFilter` accetta un parametro opzionale `strength` (0‑100). Valori più alti rimuovono più rumore ma possono sfocare i dettagli fini.

```csharp
.ApplyFilter(new DenoiseFilter(strength: 70))
```

### 4. Utilizzare più filtri immagine oltre le basi

Aspose fornisce molti altri filtri: `SharpenFilter`, `BinarizeFilter`, `ResizeFilter`, ecc. Puoi combinarli per creare una pipeline personalizzata adatta al tuo tipo di documento.

```csharp
var processed = rawImage
    .ApplyFilter(new DeskewFilter())
    .ApplyFilter(new DenoiseFilter())
    .ApplyFilter(new BinarizeFilter())
    .ApplyFilter(new SharpenFilter());
```

## Esempio completo funzionante (pronto per il copia‑incolla)

Di seguito trovi l’intero programma, pronto da inserire in un progetto console.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Initialize OCR engine
        var ocrEngine = new OcrEngine();

        // Load the original scanned image
        var rawImage = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png");

        // Build preprocessing pipeline: Deskew → Denoise → Contrast
        var processedImage = rawImage
            .ApplyFilter(new DeskewFilter())
            .ApplyFilter(new DenoiseFilter())
            .ApplyFilter(new ContrastFilter());

        // Run OCR using English language
        var ocrResult = ocrEngine.Recognize(processedImage, OcrLanguage.English);

        // Output recognized text
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

Esegui il programma con `dotnet run`. Se tutto è configurato correttamente, la console mostrerà testo pulito e leggibile estratto dalla tua immagine originale inclinata e rumorosa.

## Conclusione

Abbiamo appena coperto **come raddrizzare un’immagine** in C# rimuovendo contemporaneamente **il rumore**, **aumentando il contrasto** e **pre‑elaborando l’immagine per OCR** con una catena di **più filtri immagine**. Il punto chiave è che una pipeline di pre‑elaborazione ben ordinata può migliorare drasticamente l’accuratezza dell’OCR—spesso trasformando una scansione quasi illeggibile in testo perfettamente leggibile.

Pronto per il passo successivo? Prova a sostituire il `ContrastFilter` con un `BinarizeFilter` per vedere come la conversione in bianco‑nero influisce sui risultati, oppure sperimenta con il `ResizeFilter` per fornire al motore un’immagine a risoluzione più alta. Lo stesso schema vale per qualsiasi filtro tu scelga, così avrai una base flessibile per tutti i tuoi futuri progetti OCR.

Hai domande su come gestire PDF, OCR multilingua o integrare tutto in un’API ASP.NET? Lascia un commento qui sotto, e buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}