---
category: general
date: 2026-03-20
description: Scopri come raddrizzare l'immagine e rimuovere il rumore dell'immagine
  con Aspose OCR. Questa guida passo passo mostra anche come pre‑elaborare l'immagine
  per l'OCR e migliorare l'accuratezza dell'OCR.
draft: false
keywords:
- how to deskew image
- remove image noise
- preprocess image for OCR
- recognize text from image
- improve OCR accuracy
language: it
og_description: Scopri come raddrizzare le immagini e rimuovere il rumore con Aspose
  OCR. Migliora la precisione del tuo OCR in pochi minuti.
og_title: Come correggere l'inclinazione dell'immagine – Guida completa C# per la
  pre‑elaborazione OCR
tags:
- OCR
- C#
- Image Processing
title: Come raddrizzare l'immagine – Guida completa in C# per la pre‑elaborazione
  OCR
url: /it/net/ocr-optimization/how-to-deskew-image-complete-c-guide-for-ocr-pre-processing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come correggere l'inclinazione di un'immagine – Guida completa C# per il pre‑processing OCR

Ti sei mai chiesto **come correggere l'inclinazione di un'immagine** quando il file proviene da uno scanner con un angolo strano? Non sei l’unico; molti sviluppatori incontrano questo ostacolo quando cercano di alimentare una foto a un motore OCR. La buona notizia è che, con poche righe di C# e Aspose OCR, puoi raddrizzare, ridurre il rumore e aumentare il contrasto in una pipeline ordinata—niente Photoshop necessario.

In questo tutorial vedremo tutto quello che devi sapere: dal caricamento di un’immagine inclinata, alla **rimozione del rumore dell’immagine**, al **pre‑processing dell’immagine per OCR**, e infine al **riconoscimento del testo dall’immagine** con un alto punteggio di **miglioramento della precisione OCR**. Alla fine avrai un’app console pronta all’uso che trasforma una scansione disordinata in testo pulito e ricercabile.

## Cosa ti serve

- .NET 6 o successivo (il codice usa la sintassi `using var`, supportata da C# 8)
- Un pacchetto NuGet Aspose OCR (`Aspose.OCR`) – installalo con `dotnet add package Aspose.OCR`
- Un’immagine di esempio che sia sia inclinata sia rumorosa (ad es., `skewed_noisy.png`)
- Un IDE o editor a tua scelta (Visual Studio, VS Code, Rider… scegli tu)

> **Consiglio esperto:** Se non hai un file di esempio, ruota uno screenshot chiaro di qualche grado e aggiungi del rumore “sale‑e‑pepe” con un editor di immagini. La pipeline funziona allo stesso modo.

## Passo 1: Come correggere l'inclinazione di un'immagine con un filtro Deskew

La prima cosa che facciamo è correggere la rotazione. Aspose fornisce un `DeskewFilter` che può rilevare automaticamente angoli fino a un `MaxAngle` configurabile. Impostarlo a **5°** è un valore predefinito sicuro per la maggior parte dei documenti scansionati.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System.Drawing;   // For Image class

// Initialize the OCR engine – English is the most common language
using var ocrEngine = new OcrEngine
{
    Language = Language.English
};

// Build the preprocessing pipeline
var preprocessPipeline = new PreprocessPipeline()
    .Add(new DeskewFilter { MaxAngle = 5 })          // This is where we answer “how to deskew image”
    .Add(new DespeckleFilter { Strength = 2 })      // Next we’ll remove image noise
    .Add(new ContrastFilter { Level = 1.5 });        // Finally we boost contrast for OCR
```

**Perché è importante:**  
Se il testo è inclinato, l'algoritmo OCR può interpretare erroneamente i caratteri—pensa a una “l” che diventa “i”. **Correggendo l’inclinazione** prima, fornisci al motore una tela dritta su cui lavorare.

## Passo 2: Rimuovere il rumore dell’immagine con Despeckle

Le scansioni da telefoni economici o scanner vecchi contengono spesso macchie che sembrano punti casuali. Quei punti confondono il riconoscitore di caratteri. Il `DespeckleFilter` leviga l’immagine preservando i bordi.

```csharp
// The DespeckleFilter is already part of the pipeline (see Step 1)
// Strength = 2 is a balanced setting; increase for very noisy pics
```

Se devi **rimuovere il rumore dell’immagine** in modo più aggressivo, alza `Strength` a 3 o 4—ma fai attenzione a non perdere tratti sottili.

## Passo 3: Pre‑processing dell’immagine per OCR – Aumento del contrasto

Scansioni a basso contrasto (grigio chiaro su carta bianca) possono far sì che l'OCR non rilevi le lettere più deboli. Il `ContrastFilter` estende la gamma tonale, rendendo i pixel scuri più scuri e quelli chiari più chiari.

```csharp
// Contrast level of 1.5 is a good starting point.
// You can experiment with values between 1.0 (no change) and 2.0 (strong boost).
```

**Caso limite:** Se la tua immagine di origine è già ad alto contrasto, applicare questo filtro potrebbe sbiadire i dettagli. In tal caso, imposta `Level` a `1.0` (disabilitandolo effettivamente).

## Passo 4: Caricare e pulire l’immagine di origine

Ora carichiamo effettivamente l’immagine e la facciamo passare attraverso la pipeline che abbiamo assemblato.

```csharp
// Load the source image – replace the path with your own file location
var sourceImage = Image.FromFile("YOUR_DIRECTORY/skewed_noisy.png");

// Apply the entire preprocessing pipeline
var cleanedImage = preprocessPipeline.Apply(sourceImage);
```

> **Nota:** Il metodo `Apply` restituisce un nuovo oggetto `Image`; quello originale rimane intatto. Questo rende facile confrontare “prima” e “dopo” se vuoi fare debug del processo.

## Passo 5: Riconoscere il testo dall’immagine usando Aspose OCR

Con un’immagine dritta, priva di rumore e ad alto contrasto, la consegniamo finalmente al motore OCR.

```csharp
// Perform OCR on the cleaned image
var ocrResult = ocrEngine.Recognize(cleanedImage);

// Output the recognized text to the console
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

**Cosa dovresti vedere:** La console stampa il contenuto testuale della scansione originale, solitamente con molte meno errate interpretazioni rispetto a quando avresti fornito il file grezzo direttamente.

## Passo 6: Verificare e migliorare la precisione OCR

Anche con una pipeline solida, alcuni caratteri potrebbero ancora risultare sbagliati—soprattutto se il font originale è insolito. Ecco alcuni trucchi rapidi per **migliorare la precisione OCR**:

| Problema | Soluzione rapida |
|----------|------------------|
| Punteggiatura piccola mancante | Aggiungi un `BinaryThresholdFilter` prima del passaggio di contrasto |
| Lingua mista (ad es., Inglese + Spagnolo) | Imposta `ocrEngine.Language = Language.English | Language.Spanish;` |
| Sfondo molto scuro | Inverti l’immagine (`new InvertFilter()`) prima del deskew |
| Documenti di grandi dimensioni | Elabora le pagine in parallelo (`Parallel.ForEach`) per velocizzare |

Sperimenta con l’ordine dei filtri; a volte applicare **contrasto** prima del **despeckle** produce risultati migliori su scansioni di bassa qualità.

## Esempio completo funzionante

Di seguito trovi il programma completo che puoi copiare‑incollare in un nuovo progetto console. Include tutti i pezzi di cui abbiamo parlato, più un paio di controlli di sicurezza.

```csharp
// File: Program.cs
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialize OCR engine (English language)
        // -------------------------------------------------
        using var ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // -------------------------------------------------
        // 2️⃣ Build preprocessing pipeline:
        //    Deskew → Despeckle → Contrast Boost
        // -------------------------------------------------
        var preprocessPipeline = new PreprocessPipeline()
            .Add(new DeskewFilter { MaxAngle = 5 })          // how to deskew image
            .Add(new DespeckleFilter { Strength = 2 })      // remove image noise
            .Add(new ContrastFilter { Level = 1.5 });        // preprocess image for OCR

        // -------------------------------------------------
        // 3️⃣ Load the source image (adjust path as needed)
        // -------------------------------------------------
        const string imagePath = "YOUR_DIRECTORY/skewed_noisy.png";
        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"❌ File not found: {imagePath}");
            return;
        }

        var sourceImage = Image.FromFile(imagePath);

        // -------------------------------------------------
        // 4️⃣ Apply the pipeline → cleaned image
        // -------------------------------------------------
        var cleanedImage = preprocessPipeline.Apply(sourceImage);

        // -------------------------------------------------
        // 5️⃣ Recognize text (this is the “recognize text from image” step)
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(cleanedImage);

        // -------------------------------------------------
        // 6️⃣ Output the result
        // -------------------------------------------------
        Console.WriteLine("\n=== OCR Output ===\n");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Output previsto** (supponendo che l’immagine di esempio contenga “Hello World!”):

```
=== OCR Output ===

Hello World!
```

Se vedi caratteri incomprensibili, ricontrolla l’ordine della pipeline o aumenta il valore di `DespeckleFilter.Strength`.

## Conclusione

Abbiamo coperto **come correggere l'inclinazione di un'immagine**, **rimuovere il rumore dell’immagine**, **pre‑processare l’immagine per OCR**, e infine **riconoscere il testo dall’immagine** usando Aspose OCR—tutto mantenendo l’attenzione su **migliorare la precisione OCR**. L’esempio completo, eseguibile, mostra ogni passaggio nel contesto, così puoi inserirlo in qualsiasi progetto .NET e iniziare subito a estrarre testo.

Pronto per la prossima sfida? Prova a estendere la pipeline per gestire PDF multi‑pagina, o sperimenta con i language pack per documenti multilingue. Gli stessi concetti si applicano—basta cambiare il flag `Language` e magari aggiungere un `RotateFilter` per pagine capovolte.

Hai domande o un’immagine difficile che ancora non collabora? Lascia un commento qui sotto, e risolveremo il problema insieme. Buon coding! 

![esempio di come correggere l'inclinazione dell'immagine](/images/deskew-example.png "Illustrazione di come correggere l'inclinazione dell'immagine usando Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}