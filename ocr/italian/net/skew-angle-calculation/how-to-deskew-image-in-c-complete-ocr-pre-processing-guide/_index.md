---
category: general
date: 2026-01-10
description: Come correggere l'inclinazione dell'immagine e migliorare i risultati
  OCR con Aspose.OCR. Impara a pre‑elaborare l'immagine per l'OCR, rimuovere il rumore
  dalla scansione e riconoscere il testo dalla scansione.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- recognize text from scan
- how to use ocr
- remove noise from scan
language: it
og_description: Come correggere l'inclinazione dell'immagine e migliorare l'accuratezza
  dell'OCR. Questa guida mostra come pre-elaborare l'immagine per l'OCR, rimuovere
  il rumore dalla scansione e riconoscere il testo dalla scansione utilizzando Aspose.OCR.
og_title: Come raddrizzare un'immagine in C# – Guida completa alla pre‑elaborazione
  OCR
tags:
- OCR
- C#
- Image Processing
title: Come correggere l'inclinazione di un'immagine in C# – Guida completa alla pre‑elaborazione
  OCR
url: /it/net/skew-angle-calculation/how-to-deskew-image-in-c-complete-ocr-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come deskeware un'immagine in C# – Guida completa al pre‑processing OCR

Ti sei mai chiesto **come deskeware un'immagine** prima di inviarla a un motore OCR? Non sei l'unico. I documenti scansionati sono spesso inclinati, rumorosi o a basso contrasto, e questo compromette qualsiasi tentativo di riconoscimento del testo.  

In questo tutorial vedremo un esempio completo e eseguibile che **preprocessa l'immagine per OCR**, rimuove il rumore dalla scansione e infine **riconosce il testo dalla scansione** usando la libreria Aspose.OCR. Alla fine avrai un'idea chiara di **come usare OCR** in C# mantenendo il codice breve e conciso.

> **Consiglio professionale:** Anche una piccola rotazione (5‑10°) può ridurre l'accuratezza OCR del 30 % o più. Il deskew è il primo passo che non dovresti mai saltare.

## Cosa ti servirà

- **.NET 6+** (il codice funziona anche su .NET Framework, ma .NET 6 è l'LTS attuale)
- **Aspose.OCR for .NET** – puoi ottenerlo da NuGet (`Install-Package Aspose.OCR`)
- Un file di esempio TIFF/PNG/JPEG ruotato o rumoroso (useremo `noisy_rotated.tif` nell'esempio)
- Qualsiasi IDE ti piaccia – Visual Studio, Rider o VS Code vanno bene

È tutto. Nessuna libreria aggiuntiva, nessun servizio esterno.

## Passo 1 – Carica l'immagine sorgente (Perché è importante)

Prima di poter **deskeware l'immagine**, dobbiamo leggerla in un `ImageStream` di Aspose. Questo oggetto astrae l'I/O del file e fornisce al motore OCR un'interfaccia coerente.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Load the original scan – replace the path with your own file
var sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/noisy_rotated.tif");

// Quick sanity check – make sure the image loaded
if (sourceImage == null)
{
    Console.WriteLine("Failed to load the image. Check the path and file permissions.");
    return;
}
```

*Perché caricare prima?* Perché tutti i filtri successivi operano su un'immagine in memoria. Se il file non può essere letto, l'intera pipeline collassa.

## Passo 2 – Costruisci una pipeline di pre‑processing (Deskew + Denoise + Contrast)

Un flusso di lavoro OCR robusto di solito concatena diversi filtri. Qui è dove **preprocessiamo l'immagine per OCR** e, cosa più importante, **come deskeware l'immagine** automaticamente.

```csharp
// Create a pipeline that will run three filters in order
var preprocessPipeline = new PreprocessPipeline()
{
    // 1️⃣ DeskewFilter – detects rotation up to 30° and corrects it
    new DeskewFilter { MaxAngle = 30 },

    // 2️⃣ DenoiseFilter – smooths out speckles while keeping edges
    new DenoiseFilter { Strength = 0.8 },

    // 3️⃣ ContrastBoostFilter – makes faint characters pop
    new ContrastBoostFilter { Level = 1.3 }
};
```

**Perché questi tre?**  
- **DeskewFilter** risolve automaticamente il problema del “come deskeware l'immagine”; non è necessario indovinare l'angolo.  
- **DenoiseFilter** affronta la necessità di “rimuovere il rumore dalla scansione”, che altrimenti crea caratteri fantasma.  
- **ContrastBoostFilter** aiuta il motore OCR a distinguere il testo scuro dallo sfondo chiaro, un problema classico quando *preprocessi l'immagine per OCR*.

## Passo 3 – Applica la pipeline (vedere la trasformazione)

Ora eseguiamo effettivamente i filtri. L'`processedImage` restituito è quello che forniremo al motore OCR.

```csharp
// Apply all filters – the result is a cleaned‑up bitmap
var processedImage = preprocessPipeline.Apply(sourceImage);

// Optional: Save the cleaned image for visual verification
processedImage.Save("cleaned_output.tif");
Console.WriteLine("Image preprocessing complete – cleaned_output.tif saved.");
```

Se apri `cleaned_output.tif`, dovresti notare che il testo è dritto, meno granuloso e con contrasto più elevato. Questo controllo visivo è utile quando *rimuovi il rumore dalla scansione* e vuoi confermare che il deskew abbia funzionato.

## Passo 4 – Crea e configura il motore OCR (Come usare OCR)

Con un'immagine pulita a disposizione, istanziamo `OcrEngine`. Questo è il cuore di **come usare OCR** con Aspose.

```csharp
// Initialize the OCR engine
var ocrEngine = new OcrEngine
{
    // Assign the pre‑processed image
    Image = processedImage,

    // Optional: Set language (English is default)
    // Language = Language.English,
    
    // Enable automatic page segmentation (helps with multi‑column scans)
    AutoPageSegmentation = true
};
```

*Perché impostare `AutoPageSegmentation`?* Perché molte scansioni contengono tabelle o più colonne. Attivarlo permette al motore di suddividere la pagina in modo intelligente, migliorando il risultato finale di **riconoscere il testo dalla scansione**.

## Passo 5 – Esegui il processo di riconoscimento (Riconosci finalmente il testo)

Ora il momento della verità: chiediamo al motore di leggere il testo.

```csharp
// Kick off the OCR process
ocrEngine.Recognize();

// Retrieve the plain‑text result
string recognizedText = ocrEngine.Text;

// Show the output in the console
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(recognizedText);
```

Se tutto è andato liscio, vedrai un blocco di testo pulito che corrisponde al documento originale. Questo è il risultato di un corretto **deskew dell'immagine**, **rimozione del rumore** e **preprocessing dell'immagine per OCR**.

## Passo 6 – Esempio completo funzionante (pronto per copia‑incolla)

Di seguito il programma completo, pronto per la compilazione. Basta sostituire il percorso del file e sei pronto.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Load the source image
        // -------------------------------------------------
        var sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/noisy_rotated.tif");
        if (sourceImage == null)
        {
            Console.WriteLine("Unable to load image. Check the path.");
            return;
        }

        // -------------------------------------------------
        // 2️⃣ Build the preprocessing pipeline
        // -------------------------------------------------
        var preprocessPipeline = new PreprocessPipeline()
        {
            new DeskewFilter { MaxAngle = 30 },          // how to deskew image
            new DenoiseFilter { Strength = 0.8 },       // remove noise from scan
            new ContrastBoostFilter { Level = 1.3 }      // improves OCR accuracy
        };

        // -------------------------------------------------
        // 3️⃣ Apply the pipeline
        // -------------------------------------------------
        var processedImage = preprocessPipeline.Apply(sourceImage);
        processedImage.Save("cleaned_output.tif");
        Console.WriteLine("Preprocessing finished – cleaned_output.tif saved.");

        // -------------------------------------------------
        // 4️⃣ Configure the OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Image = processedImage,
            AutoPageSegmentation = true   // how to use OCR effectively
        };

        // -------------------------------------------------
        // 5️⃣ Recognize text from scan
        // -------------------------------------------------
        ocrEngine.Recognize();
        string result = ocrEngine.Text;

        Console.WriteLine("\n=== Recognized Text ===");
        Console.WriteLine(result);
    }
}
```

**Output previsto** (troncato per brevità):

```
=== Recognized Text ===
This is a sample scanned document.
It contains several lines of text,
and the OCR engine has correctly read them.
```

Se l'output appare illeggibile, verifica che l'immagine sorgente non sia ruotata oltre 30°, o aumenta `DeskewFilter.MaxAngle`.

## Domande frequenti (casi limite e variazioni)

| Domanda | Risposta |
|----------|--------|
| **E se la mia scansione è ruotata di 45°?** | `DeskewFilter` è limitato a `MaxAngle`. Aumentalo (es., `MaxAngle = 60`) o pre‑ruota l'immagine con una libreria grafica prima di passarla alla pipeline. |
| **Posso elaborare i PDF pagina per pagina?** | Sì. Converti ogni pagina PDF in un'immagine (es., usando `Aspose.Pdf`) ed esegui la stessa pipeline su ogni bitmap. |
| **Il mio documento è in francese – devo cambiare qualcosa?** | Imposta `ocrEngine.Language = Language.French;` o carica un pacchetto linguistico personalizzato. Il resto della pipeline rimane invariato. |
| **C'è un modo per mantenere la risoluzione originale?** | `PreprocessPipeline` lavora sul bitmap originale, preservando i DPI. Basta evitare di chiamare `ImageStream.Resize` a meno che non sia necessario ridurre la scala per le prestazioni. |
| **Come influisce il potenziamento del contrasto sulle scansioni a colori?** | `ContrastBoostFilter` agisce su ogni canale; è sicuro per immagini in scala di grigi o a colori, ma puoi anche convertire in scala di grigi prima con `new GrayscaleFilter()`. |

## Esempio immagine (ausilio visivo)

![esempio di come deskeware un'immagine](/images/deskew-example.png)

*L'immagine mostra un prima/dopo di una scansione ruotata di 12°, rumorosa, che è stata deskewata e pulita.*

## Conclusione

Abbiamo coperto **come deskeware un'immagine** usando Aspose.OCR, dimostrato una pipeline completa di **preprocessare l'immagine per OCR**, mostrato come **rimuovere il rumore dalla scansione**, e infine **riconoscere il testo dalla scansione** con poche righe di C#. Concatenando `DeskewFilter`, `DenoiseFilter` e `ContrastBoostFilter` ottieni un bitmap pulito che permette al motore OCR di svolgere il suo lavoro senza incepparsi sugli artefatti.  

Prossimi passi? Prova a sperimentare con diverse intensità dei filtri, aggiungi un `BinarizationFilter` per un output in puro bianco‑e‑nero, o invia l'immagine pulita a una pipeline NLP successiva. Lo stesso schema funziona per ricevute, passaporti e documenti storici.  

Hai altre domande su **come usare OCR** in altri linguaggi o framework? Lascia un commento, e buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}