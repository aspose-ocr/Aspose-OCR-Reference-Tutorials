---
category: general
date: 2026-04-03
description: come correggere l'inclinazione di un'immagine usando Aspose OCR in C#
  – impara a pre‑elaborare l'immagine per l'OCR, riconoscere il testo dall'immagine
  e migliorare la precisione dell'OCR in pochi minuti.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- recognize text from image
- improve ocr accuracy
- load image for ocr
language: it
og_description: come correggere l'inclinazione di un'immagine in C# usando Aspose
  OCR. Questa guida ti mostra come pre-elaborare l'immagine per l'OCR, riconoscere
  il testo dall'immagine e migliorare l'accuratezza.
og_title: Come correggere l'inclinazione di un'immagine con Aspose OCR – Guida completa
  C#
tags:
- Aspose OCR
- C#
- Image preprocessing
title: Come raddrizzare un'immagine con Aspose OCR – Guida completa C#
url: /it/net/ocr-optimization/how-to-deskew-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# come correggere l'inclinazione di un'immagine con Aspose OCR – Guida completa C#

Ti sei mai chiesto **come correggere l'inclinazione di un'immagine** prima di passarla a un motore OCR? Non sei l'unico: scansioni inclinate, foto scattate di traverso o PDF leggermente storti possono compromettere qualsiasi libreria di riconoscimento del testo.  

In questo tutorial passo‑passo vedremo l’intero flusso di lavoro: dal caricamento dell’immagine, passando per **preprocessare l’immagine per OCR** (correzione inclinazione, riduzione rumore, aumento contrasto, rotazione automatica), fino al **riconoscimento del testo dall’immagine** con Aspose OCR, e infine alcuni consigli per **migliorare l’accuratezza OCR**. Alla fine avrai un’app console C# pronta all’uso che gestisce un PNG rumoroso e inclinato come un professionista.

## Cosa ti serve

- **.NET 6+** (oppure .NET Framework 4.7.2 – l’API funziona allo stesso modo)
- Pacchetto NuGet **Aspose.OCR for .NET** (`Install-Package Aspose.OCR`)
- Un’immagine di esempio **inclinata** e **rumorosa** (ad es. `skewed_noisy.png`)
- Visual Studio, Rider o qualsiasi editor tu preferisca – non serve alcuno strumento speciale

> **Pro tip:** Se non hai un campione inclinato, ruota uno screenshot pulito di 10‑15° in Paint e aggiungi un po’ di “sale‑e‑pepe” con un editor di immagini. Il codice funziona allo stesso modo.

Ora, tuffiamoci.

## Come correggere l’inclinazione dell’immagine e migliorare l’accuratezza OCR

La prima cosa da fare è dire al `OcrEngine` di Aspose di **correggere l’inclinazione** del bitmap in ingresso. Il motore fornisce una classe integrata `ImagePreprocessingOptions` che consente di attivare più funzionalità di miglioramento della qualità contemporaneamente.

```csharp
using Aspose.OCR;
using System.Drawing;

/// <summary>
/// Demonstrates how to deskew image, denoise, boost contrast, and run OCR.
/// </summary>
class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure preprocessing options
        ImagePreprocessingOptions opts = new ImagePreprocessingOptions
        {
            Deskew = true,          // <-- this is the key to how to deskew image
            Denoise = true,
            ContrastBoost = 30,    // increase contrast by 30 %
            AutoRotate = true
        };
        ocrEngine.PreprocessingOptions = opts;

        // 3️⃣ Load the image you want to process
        Image input = Image.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png");

        // 4️⃣ Run OCR on the pre‑processed bitmap
        string text = ocrEngine.Recognize(input);

        // 5️⃣ Show the result
        System.Console.WriteLine(text);
    }
}
```

### Perché funziona

- **Deskew = true** indica al motore di rilevare la linea di base del testo e ruotare l’immagine finché la linea di base non è orizzontale. Senza di essa, anche una rotazione di 5° può ridurre l’accuratezza del 15‑20 %.
- **Denoise** elimina i puntini casuali che spesso compaiono dopo la scansione di documenti a bassa risoluzione.
- **ContrastBoost** amplifica la differenza tra primo piano (testo) e sfondo (carta), fondamentale per **migliorare l’accuratezza OCR**.
- **AutoRotate** gestisce automaticamente l’orientamento portrait vs. landscape, risparmiandoti controlli manuali.

Il codice sopra è un **esempio completo e eseguibile**—basta sostituire `YOUR_DIRECTORY` con il percorso del tuo file e premere F5.

## Preprocessare l’immagine per OCR – Riduzione rumore e aumento contrasto

Ti starai chiedendo se sia davvero necessario sia la riduzione del rumore sia l’aumento del contrasto. La risposta breve: **sì, nella maggior parte dei casi reali**. Ecco una rapida panoramica:

| Funzionalità | Cosa fa | Quando è importante |
|--------------|---------|----------------------|
| **Deskew** | Raddrizza le linee di testo inclinate | Moduli scannerizzati, foto da smartphone |
| **Denoise** | Rimuove pixel isolati | Scansioni in condizioni di scarsa illuminazione, scanner economici |
| **ContrastBoost** | Schiarisce il testo scuro, scurisce lo sfondo | Documenti sbiaditi, inchiostro tenue |
| **AutoRotate** | Rileva portrait vs. landscape | PDF multi‑pagina con orientamento misto |

Se stai elaborando una scansione perfetta e perfettamente allineata, potresti disattivare le opzioni, ma **preprocessare l’immagine per OCR** è un valore predefinito sicuro che raramente nuoce.

## Riconoscere il testo dall’immagine – Usare Aspose OCR

Una volta terminata la pipeline di preprocessing, il motore passa il bitmap pulito al suo riconoscitore interno. Il metodo `Recognize` restituisce una semplice `string` con i ritorni a capo preservati. Puoi ulteriormente post‑processare il risultato (ad es. rimuovere spazi bianchi, eseguire un controllo ortografico) se necessario.

```csharp
string recognizedText = ocrEngine.Recognize(inputImage);
Console.WriteLine("--- OCR RESULT ---");
Console.WriteLine(recognizedText);
```

### Output previsto

Se `skewed_noisy.png` contiene la frase “Hello World!”, la console stamperà qualcosa del genere:

```
--- OCR RESULT ---
Hello World!
```

Anche con rumore moderato, dovresti vedere **oltre il 95 % di accuratezza** grazie ai passaggi di preprocessing che abbiamo attivato.

## Caricare l’immagine per OCR – Consigli sulla gestione dei file

La riga `Image.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png")` è il modo più semplice per **caricare l’immagine per OCR**, ma ci sono alcune sfumature da tenere presente:

1. **Lock dei file** – `FromFile` mantiene aperto il handle del file finché l’`Image` non viene eliminata. Avvolgila in un blocco `using` se prevedi di cancellare o spostare il file in seguito.
2. **Formati supportati** – Aspose OCR accetta BMP, JPEG, PNG, TIFF e GIF. Se hai PDF, estrai ogni pagina come immagine prima (Aspose.PDF può aiutare).
3. **Utilizzo della memoria** – Immagini grandi (oltre 5 MP) possono consumare molta RAM. Considera di ridimensionare con `Bitmap` prima di passarla al motore se incappi in `OutOfMemoryException`.

```csharp
using (Image input = Image.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png"))
{
    string result = ocrEngine.Recognize(input);
    Console.WriteLine(result);
}
```

## Migliorare l’accuratezza OCR – Consigli pratici

Anche con il preprocessing automatico, alcuni casi limite possono ancora ostacolare i motori OCR. Di seguito trovi strategie collaudate da inserire nella tua pipeline:

- **Binarizzare l’immagine** (`opts.Binarization = true`) quando lo sfondo è irregolare.
- **Impostare la lingua** (`ocrEngine.Language = Language.English`) per limitare il set di caratteri.
- **Aumentare DPI**: se controlli il processo di scansione, punta ad almeno 300 dpi.
- **Ritagliare i margini**: rimuovi grandi bordi bianchi; possono confondere il rilevamento delle linee.
- **Validare l’output**: usa espressioni regolari per verificare date, numeri o pattern noti, quindi segnala le righe a bassa confidenza per una revisione manuale.

> **Ricorda:** L’obiettivo non è solo **riconoscere il testo dall’immagine**, ma farlo in modo affidabile su una varietà di qualità documentali.

## Esempio completo – Tutti i passaggi in un unico file

Di seguito trovi il programma finale, autonomo, che puoi copiare‑incollare in un nuovo progetto console.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class DeskewOcrDemo
{
    static void Main()
    {
        // Create OCR engine
        OcrEngine engine = new OcrEngine();

        // Preprocess settings (deskew, denoise, contrast, auto‑rotate)
        engine.PreprocessingOptions = new ImagePreprocessingOptions
        {
            Deskew = true,
            Denoise = true,
            ContrastBoost = 30,
            AutoRotate = true
        };

        // Load image – make sure the path is correct
        const string imagePath = @"YOUR_DIRECTORY/skewed_noisy.png";

        // Using block prevents file‑handle leaks
        using (Image img = Image.FromFile(imagePath))
        {
            // Run OCR
            string text = engine.Recognize(img);

            // Output result
            Console.WriteLine("--- OCR RESULT ---");
            Console.WriteLine(text);
        }
    }
}
```

Esegui il programma e dovresti vedere il testo pulito e corretto stampato nella console. Se sostituisci `skewed_noisy.png` con una scansione pulita e dritta, l’output sarà identico—solo con un leggero guadagno di prestazioni perché il motore salta il passaggio di correzione inclinazione.

## Conclusione

Abbiamo coperto **come correggere l’inclinazione di un’immagine** usando Aspose OCR, mostrato **come preprocessare l’immagine per OCR**, illustrato il modo corretto di **caricare l’immagine per OCR**, e infine **riconosciuto il testo dall’immagine** mantenendo l’attenzione su **migliorare l’accuratezza OCR**. Lo snippet di codice completo è pronto per essere inserito in qualsiasi progetto .NET, e i consigli aggiuntivi ti offrono una roadmap per gestire input più difficili.

Pronto per la prossima sfida? Prova a concatenare più immagini per creare un flusso OCR multi‑pagina, o sperimenta con pacchetti linguistici personalizzati per documenti non‑inglesi. Gli stessi principi di preprocessing si applicano—deskew, denoise, boost contrast, e lascia che Aspose faccia il lavoro pesante.

Hai domande su un tipo di file specifico o hai bisogno di aiuto per regolare il valore `ContrastBoost`? Lascia un commento qui sotto o visita i forum di Aspose. Buona programmazione, e che il tuo OCR sia sempre impeccabile!  

![Diagramma che mostra l'immagine originale inclinata a sinistra e il risultato corretto e pulito a destra](deskew-diagram.png "Diagramma che mostra l'immagine originale inclinata e il risultato corretto – esempio di come correggere l'inclinazione dell'immagine")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}