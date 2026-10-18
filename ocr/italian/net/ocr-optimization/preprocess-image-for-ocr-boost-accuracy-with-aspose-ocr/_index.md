---
category: general
date: 2026-01-15
description: Preprocessa l'immagine per OCR per convertire la scansione in testo rapidamente.
  Scopri come rimuovere il rumore dalla scansione e migliorare l'accuratezza dell'OCR
  usando i filtri OCR di Aspose.
draft: false
keywords:
- preprocess image for ocr
- convert scan to text
- extract text from scan
- remove noise from scan
- improve ocr accuracy
language: it
og_description: Preelabora l'immagine per OCR per convertire rapidamente la scansione
  in testo. Scopri come rimuovere il rumore dalla scansione e migliorare l'accuratezza
  dell'OCR con un semplice codice C#.
og_title: Preelabora l'immagine per OCR – Aumenta l'accuratezza con Aspose OCR
tags:
- Aspose OCR
- C#
- Image Preprocessing
title: Preelabora l'immagine per OCR – Aumenta l'accuratezza con Aspose OCR
url: /it/net/ocr-optimization/preprocess-image-for-ocr-boost-accuracy-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Preprocessare l'immagine per OCR – Un tutorial completo in C#

Hai mai avuto bisogno di **preprocessare l'immagine per OCR** ma non eri sicuro di quali filtri facciano davvero la differenza? Non sei solo—le pagine scansionate sono spesso storte, macchiate o semplicemente rumorose, e questo interferisce con qualsiasi motore OCR.  

La buona notizia è che pochi passaggi ben scelti possono **convertire la scansione in testo** in modo affidabile, e noterai un evidente miglioramento nella qualità del riconoscimento. In questa guida vedremo come caricare un TIFF inclinato, eliminare il disordine visivo e infine estrarre testo pulito—così potrai **rimuovere il rumore dalla scansione** dei file e **migliorare l'accuratezza OCR** senza dover setacciare una documentazione infinita.

## Cosa copre questo tutorial

- Configurare un motore Aspose OCR in C#  
- Caricare un'immagine scansionata reale (ad esempio una fattura storta o un modulo sbiadito)  
- Applicare i filtri Deskew, Denoise e Binarization per **preprocessare l'immagine per OCR**  
- Eseguire il motore OCR per **estrarre il testo dalla scansione** e stamparlo sulla console  
- Suggerimenti per gestire casi particolari come PDF multi‑pagina o documenti a basso contrasto  

Alla fine avrai un programma autonomo che potrai inserire in qualsiasi progetto .NET e iniziare a **convertire la scansione in testo** istantaneamente.

### Prerequisiti

- .NET 6.0 o successivo (il codice funziona anche su .NET Core e .NET Framework)  
- Pacchetto NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- Un file TIFF di esempio chiamato `skewed_scan.tif` posizionato in una cartella a tua scelta  
- Conoscenza di base di C#—nessun trucco avanzato richiesto  

Se hai tutto questo, immergiamoci.

## Preprocessare l'immagine per OCR – Passo‑per‑passo

Di seguito suddividiamo il processo in cinque passaggi logici. Ogni sezione ha un'intestazione chiara, una breve spiegazione del **perché** il passaggio è importante e uno snippet di codice completo da copiare‑incollare.

### Passo 1: Inizializzare il motore OCR

Il motore è il cuore dell'operazione; senza di esso nulla viene riconosciuto. Crearlo una volta e riutilizzarlo su più immagini è anche più efficiente.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Create a single OCR engine instance – this is cheap and reusable
        var ocrEngine = new OcrEngine();
```

*Perché è importante:* Aspose OCR include pacchetti linguistici e algoritmi adattivi che vengono caricati quando istanzi `OcrEngine`. Inizializzarlo subito evita latenze nascoste in seguito.

### Passo 2: Caricare e ispezionare il documento scansionato

Devi indicare al motore il file immagine reale. Usare `OcrImage.FromFile` ti fornisce un oggetto che può essere concatenato con i filtri.

```csharp
        // Load the skewed, noisy scan – adjust the path to match your environment
        var originalImage = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_scan.tif");
```

*Perché è importante:* Inviare direttamente una scansione grezza all'OCR di solito produce risultati spazzatura perché il motore si aspetta un input abbastanza pulito. Questo è il punto perfetto per **rimuovere il rumore dalla scansione** prima del riconoscimento.

### Passo 3: Applicare i filtri Deskew, Denoise e Binarization

Ecco dove avviene la vera magia. Concatenamo tre filtri:

1. **DeskewFilter** – raddrizza le pagine ruotate.  
2. **DenoiseFilter** – leviga le macchie e la grana.  
3. **BinarizationFilter** – impone una palette in bianco‑e‑nero, che la maggior parte dei motori OCR adora.

```csharp
        // Chain the preprocessing filters
        var preprocessedImage = originalImage
            .Apply(new DeskewFilter())          // corrects rotation
            .Apply(new DenoiseFilter())         // reduces visual noise
            .Apply(new BinarizationFilter());   // converts to B/W
```

*Perché è importante:* Una riga di testo storta viene interpretata come caratteri separati, e punti casuali possono essere scambiati per punteggiatura. **Preprocessando l'immagine per OCR** con questi tre passaggi migliori drasticamente **l'accuratezza OCR**.

> **Consiglio pro:** Se le tue scansioni sono già per lo più dritte, puoi saltare `DeskewFilter` per risparmiare qualche millisecondo.

### Passo 4: Riconoscere il testo e convertire la scansione in testo

Ora consegniamo finalmente l'immagine pulita al motore OCR. Chiederemo l'inglese, ma qualsiasi lingua supportata funziona allo stesso modo.

```csharp
        // Perform OCR on the processed image using English language
        var ocrResult = ocrEngine.Recognize(preprocessedImage, Language.English);
```

*Perché è importante:* Il motore ora lavora con una bitmap ad alto contrasto e senza rumore, quindi i punteggi di confidenza sono molto più alti. Questo è il momento in cui realmente **estrai il testo dalla scansione**.

### Passo 5: Stampare il testo riconosciuto e verificare i risultati

Un rapido `Console.WriteLine` ti mostra la stringa grezza. In un'app reale potresti scriverla su un file, su un database o inserirla in una pipeline NLP a valle.

```csharp
        // Output the recognized text to the console
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

**Output previsto** (esempio per una semplice fattura):

```
Invoice #12345
Date: 01/12/2024
Total Amount: $1,234.56
Thank you for your business!
```

Se il testo appare confuso, ricontrolla la risoluzione della scansione originale (300 dpi è una buona base) e considera di regolare l'intensità del `DenoiseFilter`.

![esempio di preprocessare l'immagine per OCR](https://example.com/images/preprocess-ocr.png "esempio di preprocessare l'immagine per OCR")

*L'immagine sopra illustra una vista prima‑e‑dopo di una pagina scansionata dopo l'applicazione dei tre filtri.*

## Suggerimenti aggiuntivi per rimuovere il rumore dai file di scansione

- **Aumentare DPI prima della scansione** – 300 dpi o più fornisce ai filtri più dati su cui lavorare.  
- **Ritagliare i margini** – lo spazio bianco inutile può confondere il passaggio di binarizzazione.  
- **Usare `ContrastFilter`** se il documento è sbiadito; può essere inserito prima di `BinarizationFilter`.  
- **Elaborazione batch** – avvolgi il codice sopra in un ciclo `foreach` per gestire automaticamente decine di file.

## Domande comuni e casi particolari

**E se il mio documento ha più pagine?**  
Avvolgi il passaggio di caricamento in un ciclo che legge ogni pagina come un `OcrImage` separato. Aspose OCR può anche accettare flussi PDF direttamente.

**Posso riconoscere lingue diverse dall'inglese?**  
Sì—basta sostituire `Language.English` con `Language.French`, `Language.Spanish`, ecc., a condizione che il pacchetto linguistico sia installato.

**C'è un modo per ottenere i punteggi di confidenza?**  
`ocrResult` contiene una proprietà `Confidence` per carattere. Puoi iterare su `ocrResult.Regions` per registrare le aree a bassa confidenza per una revisione manuale.

**E se la scansione è a colori?**  
I filtri funzionano anche su immagini a colori; convertono internamente in scala di grigi prima della binarizzazione. Tuttavia, convertire in scala di grigi da soli (`new GrayscaleFilter()`) a volte può velocizzare il processo.

## Conclusione

Ora hai un esempio completo, pronto‑all'uso, che **preprocessa l'immagine per OCR**, **rimuove il rumore dalla scansione** e **converte la scansione in testo** con Aspose OCR. Concatenando i filtri Deskew, Denoise e Binarization migliorerai costantemente **l'accuratezza OCR**, rendendo l'estrazione dei dati a valle molto più affidabile.

Pronto per il passo successivo? Prova a inviare l'output a un writer CSV, a inserirlo in un indice di ricerca, o sperimenta con altri filtri Aspose come `ContrastFilter` o `SharpenFilter`. Il cielo è il limite quando combini una solida pre‑elaborazione con un potente motore OCR.

Buona programmazione, e che le tue scansioni siano sempre nitide!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}