---
category: general
date: 2026-04-08
description: Estrai il testo da un'immagine usando Aspose OCR in C#. Scopri come pre‑elaborare
  l'immagine per l'OCR e come pre‑elaborare l'immagine per aumentare l'accuratezza.
draft: false
keywords:
- extract text from image
- preprocess image for ocr
- how to preprocess image
- Aspose OCR C#
- image preprocessing techniques
language: it
og_description: Estrai il testo da un'immagine usando Aspose OCR in C#. Questa guida
  mostra come preelaborare l'immagine per l'OCR e come preelaborare l'immagine per
  ottenere i migliori risultati.
og_title: Estrai il testo da un'immagine con Aspose OCR – Guida completa C#
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Estrai testo da immagine con Aspose OCR – Guida completa C#
url: /it/net/ocr-optimization/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai testo da immagine con Aspose OCR – Guida completa C# 

Hai mai avuto bisogno di **estrarre testo da immagine** ma i risultati erano pieni di errori? Non sei solo—la maggior parte degli sviluppatori si imbatte in questo problema quando l'immagine di origine è inclinata, rumorosa o a basso contrasto. La buona notizia è che una breve routine di pre‑elaborazione può trasformare uno scatto traballante in una fonte pulita per l'OCR, e Aspose OCR rende il tutto un gioco da ragazzi.

In questo tutorial percorreremo un esempio reale che mostra **come pre‑elaborare un'immagine per l'OCR** usando i filtri integrati di Aspose OCR, per poi **estrarre testo da immagine** con poche righe di C#. Alla fine avrai un programma pronto da eseguire, comprenderai perché ogni filtro è importante e saprai come regolare la pipeline per i tuoi casi particolari.

## Cosa ti serve

- .NET 6.0 o versioni successive (il codice funziona anche su .NET Framework 4.7+)
- Il pacchetto NuGet Aspose.OCR (`Install-Package Aspose.OCR`)
- Un'immagine di esempio che è inclinata, rumorosa o a basso contrasto (ad es., `skewed_noisy.jpg`)
- Qualsiasi IDE tu preferisca—Visual Studio, Rider o VS Code vanno bene

Nessuna libreria nativa aggiuntiva, nessun servizio web, solo puro C#.

## Passo 1: Configura il motore OCR – Il punto di partenza per estrarre testo

Prima di tutto: crea un'istanza di `OcrEngine` e indica quale lingua cercare. L'inglese è la più comune, ma puoi sostituire `"en"` con `"fr"`, `"de"` e così via.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Filters;
using System;

public static class ImageOcrDemo
{
    public static void PreprocessAndOcr()
    {
        // 1️⃣ Initialize the OCR engine – this is where we define the language.
        var ocrEngine = new OcrEngine { Language = "en" };
```

**Perché è importante:** Il motore contiene dizionari interni e euristiche specifiche per lingua. Se ometti di impostare la lingua, Aspose usa l'inglese per default, ma essere espliciti evita sorprese quando cambi lingua in seguito.

## Passo 2: Costruisci una pipeline di pre‑elaborazione – Come pre‑elaborare l'immagine per i migliori risultati

Ora aggiungiamo i filtri. Pensali come una mini suite di fotoritocco che viene eseguita automaticamente prima del passo OCR. I tre filtri qui sotto coprono i problemi più comuni:

| Filter | Cosa corregge | Quando usarlo |
|--------|---------------|----------------|
| `DeskewFilter` | Ruota l'immagine nuovamente in orizzontale | Immagini scattate con angolo |
| `DenoiseFilter` | Riduce macchie casuali e granulosità | Foto con scarsa illuminazione o documenti scannerizzati |
| `ContrastStretchFilter` | Aumenta il contrasto, facendo risaltare il testo scuro | Stampe sbiadite o screenshot sbiancati |

```csharp
        // 2️⃣ Add preprocessing steps – this is the core of “how to preprocess image”.
        ocrEngine.Preprocess.Add(new DeskewFilter());               // correct skew
        ocrEngine.Preprocess.Add(new DenoiseFilter());             // reduce noise
        ocrEngine.Preprocess.Add(new ContrastStretchFilter());     // enhance contrast
```

**Consiglio:** L'ordine è importante. Prima Deskew, poi Denoise e infine il contrast stretch. Se li inverti, potresti amplificare il rumore invece di rimuoverlo.

## Passo 3: Esegui l'OCR – Finalmente estrai testo da immagine

Con la pipeline pronta, passa al motore il percorso della tua immagine. Aspose applicherà automaticamente i filtri, poi eseguirà l'algoritmo di riconoscimento.

```csharp
        // 3️⃣ Recognize text from the pre‑processed image.
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/skewed_noisy.jpg");
```

Se il file non viene trovato, otterrai una chiara `FileNotFoundException`. Per questo consigliamo di usare percorsi assoluti durante lo sviluppo, poi passare a percorsi relativi o valori di configurazione in produzione.

## Passo 4: Visualizza il risultato – Guarda cosa hai ottenuto

L'oggetto `OcrResult` contiene il testo grezzo, i punteggi di confidenza e persino le bounding box di ogni parola. Per una demo veloce stamperemo solo il testo sulla console.

```csharp
        // 4️⃣ Output the extracted text.
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Quando esegui il programma, dovresti vedere qualcosa del genere:

```
=== OCR Output ===
Invoice Number: 2023-0456
Date: 03/15/2024
Total: $1,234.56
```

Se l'output appare confuso, ricontrolla la qualità dell'immagine o sperimenta con filtri aggiuntivi (ad es., `BinarizationFilter` per immagini binarie).

## Esempio completo funzionante – Copia‑incolla ed esegui

Di seguito trovi il programma completo e autonomo. Sostituisci `YOUR_DIRECTORY/skewed_noisy.jpg` con il percorso reale della tua immagine di test.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Filters;
using System;

public static class ImageOcrDemo
{
    public static void Main()
    {
        PreprocessAndOcr();
    }

    public static void PreprocessAndOcr()
    {
        // Step 1: Create OCR engine and set language
        var ocrEngine = new OcrEngine { Language = "en" };

        // Step 2: Build preprocessing pipeline
        ocrEngine.Preprocess.Add(new DeskewFilter());               // correct skew
        ocrEngine.Preprocess.Add(new DenoiseFilter());             // reduce noise
        ocrEngine.Preprocess.Add(new ContrastStretchFilter());     // enhance contrast

        // Step 3: Recognize text from the pre‑processed image
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/skewed_noisy.jpg");

        // Step 4: Show the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Output previsto** – La console stamperà la rappresentazione in testo semplice di ciò che è nell'immagine. Se l'immagine contiene un semplice cartello che dice “OpenAI”, vedrai esattamente quella parola, senza simboli aggiuntivi.

## Casi limite e come regolare la pipeline

### 1️⃣ Immagini molto scure

Se il filtro di contrasto non è sufficiente, aggiungi prima un `BrightnessCorrectionFilter`:

```csharp
ocrEngine.Preprocess.Add(new BrightnessCorrectionFilter(30)); // increase brightness by 30%
```

### 2️⃣ Documenti multilingua

Imposta `Language = "en+fr"` (Aspose supporta codici lingua separati da virgola) e aggiungi un `LanguageDetectionFilter` se vuoi che il motore rilevi automaticamente.

### 3️⃣ PDF di grandi dimensioni convertiti in immagini

Elaborare un PDF di mille pagine immagine per immagine può essere lento. Usa `Parallel.ForEach` per eseguire l'OCR su più immagini contemporaneamente, ma ricorda che `OcrEngine` non è thread‑safe—crea un'istanza separata per ogni thread.

```csharp
Parallel.ForEach(imagePaths, path =>
{
    var engine = new OcrEngine { Language = "en" };
    // add same filters...
    var result = engine.RecognizeImage(path);
    // store result...
});
```

### 4️⃣ Ottenere le bounding box

Se ti serve la posizione di ogni parola (ad es., per evidenziare), ispeziona `ocrResult.Regions`. Ogni regione contiene coordinate `Rectangle` che puoi utilizzare in un overlay UI.

```csharp
foreach (var region in ocrResult.Regions)
{
    Console.WriteLine($"{region.Text} at {region.Bounds}");
}
```

## Errori comuni (e come evitarli)

- **Saltare il passo Deskew** – Anche una inclinazione di 2 gradi può ridurre la confidenza del 20 %. Aggiungi sempre `DeskewFilter` quando la sorgente non è perfettamente allineata.
- **Usare JPEG con compressione elevata** – Gli artefatti di compressione sembrano rumore; passa a PNG o TIFF per un OCR migliore.
- **Hard‑coding dei percorsi** – I percorsi relativi funzionano localmente, ma nelle pipeline CI/CD è preferibile leggere la posizione dell'immagine da configurazione o variabili d'ambiente.

## Testare la configurazione

1. Esegui il programma con un'immagine pulita e ad alto contrasto. Dovresti ottenere un testo quasi perfetto.
2. Sostituisci con una foto rumorosa e inclinata. Verifica che l'output migliori dopo aver aggiunto i tre filtri.
3. Sperimenta rimuovendo un filtro alla volta per vedere il suo impatto—questo ti aiuta a capire *perché* ogni passo è importante.

## Conclusione

Abbiamo appena dimostrato come **estrarre testo da immagine** usando Aspose OCR, e abbiamo mostrato un modo pratico per **pre‑elaborare l'immagine per l'OCR** che funziona nella maggior parte degli scenari reali. Concatenando `DeskewFilter`, `DenoiseFilter` e `ContrastStretchFilter` fornisci al motore una tela pulita, migliorando drasticamente l'accuratezza.

Da qui puoi esplorare filtri più avanzati, gestire documenti multi‑pagina, o integrare i risultati OCR in un indice di ricerca. Qualunque cosa tu scelga, il modello di base—inizializzare, pre‑elaborare, riconoscere e consumare—rimane lo stesso.

Pronto a fare il salto di livello? Prova ad aggiungere un `BinarizationFilter` per scansioni in bianco‑nero, o collega l'output a un database per PDF ricercabili. Buona programmazione, e che ogni immagine che invii ad Aspose restituisca testo nitido e leggibile!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}