---
category: general
date: 2026-03-13
description: Come correggere l'inclinazione dell'immagine e aumentare il contrasto
  per l'OCR. Scopri come rimuovere il rumore, estrarre l'immagine del testo e ottenere
  risultati affidabili con Aspose OCR.
draft: false
keywords:
- how to deskew image
- extract text image
- how to remove noise
- how to boost contrast
- how to extract text
language: it
og_description: Come correggere l'inclinazione di un'immagine in C# ed estrarre il
  testo. Questa guida mostra come rimuovere il rumore, aumentare il contrasto e ottenere
  risultati OCR accurati.
og_title: Come raddrizzare l'immagine – OCR veloce con Aspose in C#
tags:
- OCR
- C#
- Image Processing
title: Come raddrizzare l'immagine ed estrarre il testo in C# – Guida completa
url: /it/net/ocr-optimization/how-to-deskew-image-and-extract-text-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come correggere l'inclinazione di un'immagine ed estrarre testo in C# – Guida completa

Ti sei mai chiesto **come correggere l'inclinazione di un'immagine** prima di passarla a un motore OCR? Non sei solo. Una scansione storta può trasformare un'estrazione di testo perfetta in un gioco di indovinelli, soprattutto quando l'immagine è anche rumorosa o a basso contrasto. In questo tutorial vedremo passo passo come raddrizzare, pulire e illuminare un'immagine così da poter **estrarre testo dall'immagine** in modo affidabile. Lungo il percorso tratteremo anche **come rimuovere il rumore**, **come aumentare il contrasto** e infine **come estrarre il testo** usando Aspose.OCR.

Alla fine di questa guida avrai un programma C# pronto all'uso che prende un PNG inclinato e macchiato, lo corregge e stampa il testo riconosciuto sulla console. Nessun misterioso link “vedi la documentazione”—solo una soluzione completa e autonoma che puoi copiare‑incollare.

## Cosa ti servirà

- **.NET 6.0** o versioni successive (il codice funziona anche su .NET Framework 4.7+).  
- **Aspose.OCR per .NET** – installa via NuGet: `Install-Package Aspose.OCR`.  
- Un’immagine di esempio che sia ruotata, rumorosa o a basso contrasto (useremo `skewed_noisy.png`).  
- Qualsiasi IDE ti piaccia—Visual Studio, Rider o VS Code vanno bene.

Questo è tutto. Nessuna libreria nativa aggiuntiva, nessun servizio esterno.

![esempio di come correggere l'inclinazione dell'immagine – prima e dopo l'elaborazione](image-placeholder.png)

*(Testo alternativo dell'immagine: esempio di come correggere l'inclinazione dell'immagine – prima e dopo l'elaborazione)*

## Come correggere l'inclinazione di un'immagine – Panoramica

L'idea di base dietro **come correggere l'inclinazione di un'immagine** è semplice: rilevare l'angolo di rotazione e ruotare il bitmap nuovamente su una linea orizzontale. Aspose.OCR fornisce un `DeskewFilter` che fa esattamente questo. Ma una buona pipeline OCR raramente si ferma alla correzione dell'inclinazione; vuoi anche **rimuovere il rumore**, **aumentare il contrasto** e infine **estrarre il testo**. Le sezioni seguenti scompongono ciascuna parte.

### Perché una pipeline di pre‑elaborazione è importante

Immagina di dover leggere un appunto scritto a mano che è stato scansionato con un leggero angolo, con macchie di caffè sparse sulla pagina. Anche il più intelligente motore OCR inciamperebbe. Fornendo un’immagine pulita e raddrizzata, dai al motore un segnale chiaro, il che si traduce in maggiore precisione e meno correzioni post‑elaborazione.

## Passo 1: Carica l'immagine

Per prima cosa, ci serve uno `ImageStream` che punti al file sorgente. Aspose.OCR può leggere molti formati (PNG, JPEG, TIFF), quindi scegli quello che hai.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Load the image from disk
ImageStream imageStream = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.png");
```

**Perché è importante:** Caricare l’immagine in uno `ImageStream` fornisce al motore OCR un modo unificato per accedere ai dati dei pixel, indipendentemente dal tipo di file originale.

## Passo 2: Costruisci una pipeline di pre‑elaborazione (Correzione inclinazione, Riduzione rumore, Aumento contrasto)

Qui rispondiamo a **come rimuovere il rumore**, **come aumentare il contrasto**, e naturalmente **come correggere l'inclinazione di un'immagine**—tutto in un unico `FilterPipeline`.

```csharp
// Create a pipeline to hold the filters
FilterPipeline preprocessingPipeline = new FilterPipeline();

// 1️⃣ Deskew – correct rotation up to 15 degrees
preprocessingPipeline.Add(new DeskewFilter { MaxAngleDegrees = 15 });

// 2️⃣ Despeckle – eliminate isolated dark/bright pixels (noise)
preprocessingPipeline.Add(new DespeckleFilter());

// 3️⃣ Contrast boost – make darks darker, lights lighter (Level 30 is a good start)
preprocessingPipeline.Add(new ContrastBoostFilter { Level = 30 });

// 4️⃣ Binarize – convert to pure black‑and‑white using Otsu’s method
preprocessingPipeline.Add(new BinarizeOtsuFilter());
```

### Come aiuta ciascun filtro

| Filtro | Scopo | Caso d'uso tipico |
|--------|-------|-------------------|
| **DeskewFilter** | Ruota l’immagine nuovamente in orizzontale. | Pagine scansionate con qualche grado di inclinazione. |
| **DespeckleFilter** | Rimuove macchie isolate che sembrano caratteri sparsi. | Scansioni di vecchi giornali o fotocopie di bassa qualità. |
| **ContrastBoostFilter** | Amplifica la differenza tra primo piano e sfondo. | Inchiostro sbiadito o screenshot a basso contrasto. |
| **BinarizeOtsuFilter** | Produce un’immagine pulita in bianco‑nero, ideale per OCR. | Qualsiasi scenario in cui il colore non è necessario per il riconoscimento del testo. |

**Consiglio esperto:** Se la tua immagine è gravemente ruotata (oltre 15°), aumenta `MaxAngleDegrees` a 30 o 45, ma tieni presente che angoli estremi possono introdurre artefatti di interpolazione.

## Passo 3: Configura il motore OCR

Ora colleghiamo l’immagine e la pipeline, indichiamo ad Aspose la lingua che ci aspettiamo e creiamo l’istanza `OcrEngine`.

```csharp
// Set up the OCR engine with the image, pipeline, and language
OcrEngine ocrEngine = new OcrEngine
{
    Image = imageStream,
    PreProcessingFilters = preprocessingPipeline,
    Language = Language.English      // Change if you need another language
};
```

**Perché impostiamo la lingua:** Specificare `Language.English` restringe il set di caratteri che il motore cerca, velocizzando l’elaborazione e riducendo i falsi positivi. Se ti serve il supporto multilingue, puoi passare una lista separata da virgole (es. `Language.English | Language.French`).

## Passo 4: Riconosci ed estrai il testo

Con tutto pronto, il riconoscimento vero e proprio è una singola chiamata di metodo.

```csharp
// Perform the OCR operation
ocrEngine.Recognize();

// The recognized text is now available via the Text property
string extractedText = ocrEngine.Text;
Console.WriteLine(extractedText);
```

Quella riga stampa il risultato OCR direttamente sulla console, perfetto per una verifica rapida o per reindirizzare l’output a un altro sistema.

## Output atteso e verifica

Eseguendo il programma completo su `skewed_noisy.png` dovresti ottenere qualcosa di simile:

```
Lorem ipsum dolor sit amet,
consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut
labore et dolore magna aliqua.
```

Se l’output appare confuso, ricontrolla quanto segue:

1. **Intervallo angolo:** La rotazione originale era più grande di `MaxAngleDegrees`?  
2. **Livello di rumore:** L’immagine è molto macchiata? Considera di aggiungere un secondo `DespeckleFilter`.  
3. **Livello di contrasto:** Per inchiostro molto tenue, aumenta `ContrastBoostFilter.Level` a 40‑50.

## Come rimuovere il rumore – Opzioni avanzate

A volte un singolo `DespeckleFilter` non è sufficiente, soprattutto con scansioni di pellicola granulosa. Aspose offre un `MedianFilter` che funziona bene su sfondi testurizzati.

```csharp
preprocessingPipeline.Add(new MedianFilter { KernelSize = 3 });
```

Aggiungi questo **prima** del `DespeckleFilter` per ottenere i migliori risultati. L’operazione mediana leviga le regioni mantenendo i bordi, il che aiuta a preservare i caratteri.

## Come aumentare il contrasto – Messa a punto

Se il valore predefinito `Level = 30` lascia ancora alcuni caratteri poco visibili, puoi concatenare più aumenti di contrasto:

```csharp
preprocessingPipeline.Add(new ContrastBoostFilter { Level = 20 });
preprocessingPipeline.Add(new ContrastBoostFilter { Level = 20 });
```

Due aumenti moderati spesso superano un singolo boost aggressivo, perché evitano il clipping dei pixel estremi.

## Estrarre testo dall'immagine usando Aspose – Suggerimenti di post‑elaborazione

Dopo aver ottenuto `ocrEngine.Text`, potresti voler:

- **Rimuovere spazi bianchi**: `extractedText = extractedText.Trim();`
- **Normalizzare le interruzioni di riga**: `extractedText = extractedText.Replace("\r\n", "\n");`
- **Rimuovere caratteri non‑ASCII** (se ti aspetti solo inglese): `extractedText = Regex.Replace(extractedText, @"[^\x00-\x7F]+", string.Empty);`

Questi passaggi trasformano l’output OCR grezzo in stringhe pulite e ricercabili—perfette per l’indicizzazione o per l’inserimento in una pipeline NLP successiva.

## Problemi comuni e consigli

| Sintomo | Probabile causa | Soluzione |
|---------|----------------|-----------|
| Il testo è inclinato dopo l'OCR | Angolo massimo di `DeskewFilter` troppo basso | Aumentare `MaxAngleDegrees`. |
| Molti caratteri casuali | Rumore non completamente rimosso | Aggiungere `MedianFilter` o aumentare l’aggressività di `DespeckleFilter`. |
| Lettere deboli non riconosciute | Contrasto non sufficientemente forte | Impilare due `ContrastBoostFilter` o aumentare `Level`. |
| Le prestazioni sono lente su immagini grandi | La pipeline gira su bitmap a piena risoluzione | Ridimensionare prima: `preprocessingPipeline.Add(new ResizeFilter { Width = 1200 });` |

**Ricorda:** La migliore pipeline OCR è spesso un equilibrio tra qualità dell’immagine e tempo di elaborazione. Testa con alcuni campioni rappresentativi prima di fissare le impostazioni.

## Esempio completo funzionante

Di seguito trovi il programma completo, pronto per il copia‑incolla. Salvalo come `Program.cs`, ripristina il pacchetto NuGet e avvialo.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Passo 1: Carica l'immagine sorgente da sottoporre a OCR
        // -------------------------------------------------
        ImageStream imageStream = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.png");

        // -------------------------------------------------
        // Passo 2: Costruisci una pipeline di pre‑elaborazione
        // -------------------------------------------------
        FilterPipeline preprocessingPipeline = new FilterPipeline();

        // Deskew – corregge la rotazione fino a 15°
        preprocessingPipeline.Add(new DeskewFilter { MaxAngleDegrees = 15 });

        // Despeckle – rimuove pixel di rumore isolati
        preprocessingPipeline.Add(new DespeckleFilter());

        // Optional: Median filter per granulosità elevata
        // preprocessingPipeline.Add(new MedianFilter { KernelSize = 3 });

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}