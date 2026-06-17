---
category: general
date: 2026-03-15
description: Esegui OCR su un'immagine usando Aspose OCR in C#. Scopri come pre‑elaborare
  l’immagine prima dell’OCR per migliorare la precisione dell’OCR e riconoscere il
  testo dall’immagine in modo efficiente.
draft: false
keywords:
- perform OCR on image
- recognize text from image
- improve OCR accuracy
- preprocess image before OCR
language: it
og_description: Esegui OCR su un'immagine con Aspose OCR. Questa guida mostra come
  pre‑elaborare l’immagine prima dell’OCR, migliorare la precisione dell’OCR e riconoscere
  il testo dall’immagine in C#.
og_title: Esegui OCR su immagine – Aumenta l'accuratezza con Aspose OCR
tags:
- C#
- Aspose OCR
- Image Processing
title: Esegui OCR sull'immagine – Aumenta l'accuratezza con Aspose OCR
url: /it/net/ocr-optimization/perform-ocr-on-image-boost-accuracy-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esegui OCR su Immagine – Aumenta l'Accuratezza con Aspose OCR

Hai mai dovuto **eseguire OCR su file immagine** ma hai ottenuto output incomprensibili? Non sei solo. In molti progetti reali, una scansione rumorosa e inclinata può confondere anche i migliori motori OCR, lasciandoti con testo che sembra digitato da un gatto che cammina sulla tastiera.

Ecco la questione: l'immagine grezza è solo metà della battaglia. **Preprocessare l'immagine prima dell'OCR** può migliorare drasticamente **l'accuratezza dell'OCR** e permetterti di **riconoscere il testo da immagine** in modo affidabile. In questo tutorial percorreremo un esempio completo, pronto all'uso in C#, che mostra esattamente come fare con Aspose.OCR.

Tratteremo:

* Installazione del pacchetto NuGet Aspose.OCR.  
* Creazione di una pipeline di preprocessing (deskew, denoise, contrast boost, binarization).  
* Esecuzione del motore OCR e stampa del testo riconosciuto.  

Niente superflui, niente scorciatoie “vedi la documentazione più tardi” — solo una soluzione autonoma che puoi inserire subito in un'app console.

---

## Cosa Ti Serve

Prima di iniziare, assicurati di avere:

* **.NET 6+** (o .NET Framework 4.6.2+).  
* Un pacchetto NuGet **Aspose.OCR** recente (v23.10 o successivo).  
* Un file immagine un po' disordinato — pensa a una scansione inclinata, rumorosa, a basso contrasto.  
* Visual Studio, VS Code o qualsiasi IDE ti piaccia.

Tutto qui. Se ti manca il pacchetto NuGet, esegui:

```bash
dotnet add package Aspose.OCR
```

Ora mettiamoci al lavoro.

---

## ## Esegui OCR su Immagine – Configurazione del Motore

Il primo passo è creare un'istanza di `OcrEngine`. Questo oggetto è il cuore di Aspose OCR; contiene configurazioni, pipeline e la logica di riconoscimento vera e propria.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System.Drawing;          // For Image class
using System;                  // For Console

// Step 1: Instantiate the OCR engine
var ocrEngine = new OcrEngine();
```

> **Perché è importante:**  
> Istanziare il motore ti dà una base pulita. Potrai in seguito modificare impostazioni (lingua, modalità di riconoscimento, ecc.) senza toccare il resto del codice.

---

## ## Preprocessare l'Immagine Prima dell'OCR – Costruzione della Pipeline

Le scansioni grezze raramente sono perfette. Una buona pipeline di preprocessing può **migliorare l'accuratezza dell'OCR** fino al 30 % in alcuni casi. Di seguito concatenamo quattro filtri:

| Filtro | Cosa fa | Valori tipici |
|--------|---------|---------------|
| `DeskewFilter` | Rileva e corregge la rotazione | `Angle = 0.0` (auto‑rilevamento) |
| `DenoiseFilter` | Rimuove macchie e granulosità | `Strength = 70` (su 100) |
| `ContrastBoostFilter` | Fa risaltare il testo scuro | `Strength = 40` |
| `BinarizationFilter` | Converte l'immagine in bianco‑nero puro | `Threshold = 128` |

```csharp
// Step 2: Create a preprocessing pipeline
var preprocessingPipeline = new ImageProcessingPipeline()
    .Add(new DeskewFilter { Angle = 0.0 })               // auto‑detect skew angle
    .Add(new DenoiseFilter { Strength = 70 })           // reduce noise
    .Add(new ContrastBoostFilter { Strength = 40 })     // enhance contrast
    .Add(new BinarizationFilter { Threshold = 128 });   // convert to B/W

// Attach the pipeline to the OCR engine
ocrEngine.Configuration.PreProcessing = preprocessingPipeline;
```

> **Consiglio professionale:** Se le tue immagini di origine sono già pulite, puoi saltare il `DenoiseFilter` o ridurne il `Strength`. Un eccesso di filtraggio può a volte cancellare caratteri deboli.

---

## ## Caricare l'Immagine – Dove Trovare il File

Ora puntiamo il motore all'immagine che vogliamo leggere. Il metodo `Image.FromFile` funziona con qualsiasi formato supportato da System.Drawing (JPEG, PNG, BMP, ecc.).

```csharp
// Step 3: Load the image you want to recognize
var inputImagePath = @"C:\Images\skewed_noisy.jpg";   // change to your path
var inputImage = Image.FromFile(inputImagePath);
```

> **Caso limite:** Se il percorso del file contiene spazi o caratteri Unicode, racchiudilo in una stringa verbatim (`@"..."`) come mostrato sopra. Inoltre, gestisci sempre `FileNotFoundException` nel codice di produzione.

---

## ## Riconoscere il Testo da Immagine – Esecuzione del Motore OCR

Con il motore configurato e l'immagine caricata, il riconoscimento vero e proprio è una singola riga. Il risultato contiene il testo estratto più metriche di confidenza che potrai ispezionare in seguito.

```csharp
// Step 4: Perform OCR and get the result
var ocrResult = ocrEngine.Recognize(inputImage);

// Display the recognized text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

Quando esegui il programma, dovresti vedere qualcosa di simile:

```
=== OCR Output ===
Invoice #12345
Date: 03/12/2026
Total: $1,250.00
```

Se l'output sembra errato, regola le intensità della pipeline o sperimenta con un valore `Threshold` diverso. Piccoli aggiustamenti spesso fanno una grande differenza.

---

## ## Problemi Comuni & Come Risolverli

1. **Il risultato è vuoto o quasi incomprensibile**  
   *Controlla la pipeline.* Un denoise troppo aggressivo può cancellare tratti sottili. Riduci `Strength` o commenta temporaneamente il filtro.

2. **La correzione dell'inclinazione non funziona**  
   Il `DeskewFilter` funziona meglio su documenti in cui la linea di base del testo è approssimativamente orizzontale. Se l'immagine è ruotata più di 15°, potresti doverla pre‑ruotare manualmente usando `RotateFlip`.

3. **I caratteri non latini non vengono riconosciuti**  
   Per impostazione predefinita Aspose OCR utilizza modelli di lingua inglese. Imposta `ocrEngine.Configuration.Language` al codice ISO appropriato (es., `"fr"` per il francese) prima di chiamare `Recognize`.

```csharp
ocrEngine.Configuration.Language = "fr";   // for French text
```

4. **Le prestazioni sembrano lente**  
   Se elabori centinaia di pagine, riutilizza una singola istanza di `OcrEngine` e sostituisci solo l'oggetto `Image` ad ogni iterazione. Creare un nuovo motore ogni volta aggiunge overhead inutile.

---

## ## Risultato Visivo – Come Appare l'Immagine Preprocessata

Di seguito trovi una rapida illustrazione prima‑e‑dopo (il tuo output reale potrebbe variare).

![Risultato OCR su Immagine](https://example.com/ocr-before-after.png "Esegui OCR su Immagine – preprocessata vs originale")

*Testo alternativo:* “Esegui OCR su Immagine – confronto tra scansione originale rumorosa e versione preprocessata pronta per l'OCR”.

---

## ## Conclusione: Esempio Completo Funzionante

Copia l'intero frammento qui sotto in un nuovo progetto console (`dotnet new console`) e premi **F5**. Compila, esegue e stampa il testo riconosciuto nella console.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System.Drawing;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Build a preprocessing pipeline (improve OCR accuracy)
        var preprocessingPipeline = new ImageProcessingPipeline()
            .Add(new DeskewFilter { Angle = 0.0 })               // auto‑detect skew angle
            .Add(new DenoiseFilter { Strength = 70 })           // reduce noise
            .Add(new ContrastBoostFilter { Strength = 40 })     // enhance contrast
            .Add(new BinarizationFilter { Threshold = 128 });   // convert to B/W

        ocrEngine.Configuration.PreProcessing = preprocessingPipeline;

        // 3️⃣ Load the image you want to read
        var imagePath = @"YOUR_DIRECTORY\skewed_noisy.jpg";   // ← update this path
        var inputImage = Image.FromFile(imagePath);

        // 4️⃣ Run OCR – recognize text from image
        var ocrResult = ocrEngine.Recognize(inputImage);

        // 5️⃣ Show the result
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Output previsto:** La console stampa la versione testuale di ciò che era nell'immagine — che si tratti di una fattura, di una scansione di passaporto o di una nota scritta a mano.

---

## ## Prossimi Passi – Andare Oltre

* **Elaborazione batch:** Avvolgi la chiamata di riconoscimento in un ciclo `foreach` per gestire una cartella di immagini.  
* **Pacchetti lingua:** Installa dati linguistici aggiuntivi da Aspose per **riconoscere il testo da immagine** in spagnolo, tedesco, cinese, ecc.  
* **Post‑processing personalizzato:** Usa espressioni regolari per estrarre date, importi o ID dalla stringa OCR.  
* **Librerie alternative:** Confronta i risultati con Tesseract o Microsoft Azure Computer Vision per vedere come **preprocessare l'immagine prima dell'OCR** si comporta su diverse piattaforme.

---

## ## Conclusione

Abbiamo appena dimostrato come **eseguire OCR su file immagine** usando Aspose OCR, costruendo una pipeline di preprocessing intelligente, e visto che **preprocessare l'immagine prima dell'OCR** può **migliorare drasticamente l'accuratezza dell'OCR**. Seguendo i passaggi sopra, ora puoi **riconoscere il testo da immagine** in modo affidabile in qualsiasi applicazione C# — niente più frustrazione per output incomprensibili.

Sentiti libero di sperimentare con le intensità dei filtri, provare formati immagine diversi o integrare questo codice in un servizio più ampio di elaborazione documenti. Il cielo è il limite una volta che la pipeline OCR è solida.

Hai domande o un caso d'uso interessante? Lascia un commento qui sotto, e buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}