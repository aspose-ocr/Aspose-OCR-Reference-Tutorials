---
category: general
date: 2025-12-29
description: Scopri come raddrizzare l'immagine, rimuovere lo sfondo ed estrarre il
  testo con Aspose OCR. Codice C# passo‑passo per pre‑elaborare l'immagine per l'OCR
  e riconoscere il testo dall'immagine.
draft: false
keywords:
- how to deskew image
- how to remove background
- how to extract text
- preprocess image for ocr
- recognize text from image
language: it
og_description: Come raddrizzare l'immagine e migliorare l'accuratezza OCR. Segui
  questa guida per rimuovere lo sfondo, pre‑elaborare l'immagine per l'OCR e riconoscere
  il testo dall'immagine usando Aspose.
og_title: Come raddrizzare l'immagine – Tutorial di pre‑elaborazione OCR in C#
tags:
- Aspose OCR
- C#
- Image preprocessing
title: Come raddrizzare l'immagine – Guida completa C# per il pre‑processing OCR
url: /it/net/skew-angle-calculation/how-to-deskew-image-complete-c-guide-for-ocr-pre-processing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come correggere l'inclinazione di un'immagine – Guida completa C# per il pre‑processing OCR

Ti sei mai chiesto **come correggere l'inclinazione di un'immagine** che proviene da uno scanner e sembra una cartolina storta? Non sei l'unico. In molti progetti reali le immagini di origine sono inclinate, rumorose o afflitte da uno sfondo macchiato, e questo fa inciampare l'OCR.  

In questo tutorial vedremo una soluzione pratica che non solo **come correggere l'inclinazione di un'immagine**, ma anche **come rimuovere lo sfondo**, **come estrarre il testo**, e infine **riconoscere il testo da un'immagine** usando Aspose OCR per .NET. Alla fine avrai un programma C# pronto all'uso che pre‑processa un'immagine per l'OCR e restituisce testo pulito e ricercabile.

## Cosa ti serve

- .NET 6 SDK o versioni successive (il codice funziona sia su .NET Core che su .NET Framework)  
- Visual Studio 2022 (o qualsiasi editor tu preferisca)  
- Pacchetto NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- Un'immagine di esempio che è inclinata e rumorosa (ad es., `skewed_noisy.jpg`)  

Tutto qui—nessuna libreria nativa aggiuntiva, nessuno strumento da riga di comando complicato. Immergiamoci.

## Passo 1 – Carica l'immagine di input (Inizio della correzione dell'inclinazione)

La prima cosa da fare è caricare l'immagine in memoria. Il metodo `Image.Load` di Aspose OCR accetta un percorso file e restituisce un oggetto `Image` che puoi manipolare.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class Program
{
    static void Main()
    {
        // Load the original photo that needs deskewing and cleaning
        Image originalImage = Image.Load("YOUR_DIRECTORY/skewed_noisy.jpg");
```

> **Perché è importante:** Caricare l'immagine ci fornisce un riferimento per applicare tutte le trasformazioni successive, dalla correzione dell'inclinazione alla rimozione dello sfondo.

## Passo 2 – Correggi l'inclinazione dell'immagine (Correzione pratica dell'inclinazione)

Aspose OCR include un pratico filtro `Deskew` che rileva automaticamente l'angolo di inclinazione fino a una soglia configurabile. Qui permettiamo fino a **5°** perché la maggior parte dei documenti scansionati non supera questo valore.

```csharp
        // Auto‑detect and correct rotation up to 5 degrees
        Image deskewed = ImageFilters.Deskew(originalImage, angleThreshold: 5);
```

> **Consiglio:** Se i tuoi documenti sono ruotati più di 5°, aumenta `angleThreshold` a 10 o 15. L'algoritmo rimane veloce anche con angoli più grandi.

## Passo 3 – Rimuovi il rumore dall'immagine corretta

Il rumore è il killer silenzioso della precisione OCR. Un semplice passaggio di denoise elimina i granelli senza sfocare i caratteri reali.

```csharp
        // Reduce random speckles and grain
        Image denoised = deskewed.Denoise();
```

> **Cosa succede dietro le quinte?** Il filtro applica una sfocatura mediana che preserva i bordi (le lettere) mentre sopprime i pixel isolati.

## Passo 4 – Rimuovi lo sfondo (Rimozione efficace dello sfondo)

Uno sfondo chiaro o a trama può confondere il motore OCR. Il metodo `RemoveBackground` di Aspose OCR isola il testo in primo piano.

```csharp
        // Strip away uneven lighting or paper texture
        Image processedImage = denoised.RemoveBackground();
```

> **Perché rimuovere lo sfondo?** Aumentando il contrasto tra il testo e il suo sfondo, il motore può distinguere i caratteri in modo più affidabile, migliorando direttamente i risultati di **come estrarre il testo**.

## Passo 5 – Inizializza il motore OCR

Ora che l'immagine è dritta, pulita e ad alto contrasto, istanziamo il motore OCR. Non è necessaria alcuna configurazione aggiuntiva per gli script latini di base, ma è possibile cambiare lingua se necessario.

```csharp
        // Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **Nota:** Aspose OCR supporta oltre 100 lingue. Se ti serve il supporto multilingue, imposta `ocrEngine.Language = OcrLanguage.YourLanguage;` prima del riconoscimento.

## Passo 6 – Riconosci il testo dall'immagine (Come estrarre il testo)

Con il motore pronto, fornisci l'immagine pre‑processata. Il metodo `Recognize` restituisce un oggetto `OcrResult` che contiene il testo grezzo e i punteggi di confidenza.

```csharp
        // Perform the actual OCR
        OcrResult ocrResult = ocrEngine.Recognize(processedImage);
```

> **Informazione sul risultato:** `ocrResult.Text` contiene la stringa semplice, mentre `ocrResult.Confidence` (se la interroghi) indica quanto il motore è sicuro di ogni riga.

## Passo 7 – Output del testo riconosciuto

Infine, stampa il testo estratto sulla console—oppure scrivilo su un file, un database, qualunque cosa si adatti al tuo flusso di lavoro.

```csharp
        // Show the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Il programma completo è ora eseguibile. Compilalo ed eseguilo, e dovresti vedere testo pulito e leggibile anche se l'immagine di origine era inclinata e rumorosa.

![esempio di correzione dell'inclinazione dell'immagine](/images/deskew-demo.png "Demo della correzione dell'inclinazione dell'immagine usando Aspose OCR")

*Lo screenshot sopra mostra un prima‑e‑dopo dell'immagine corretta, illustrando l'impatto della pipeline di pre‑processing.*

## Casi limite e domande comuni

### E se l'immagine è ruotata più di 5°?
Aumenta `angleThreshold` nella chiamata a `Deskew`. L'algoritmo rileverà ancora automaticamente l'angolo corretto, ma all'interno di una finestra di ricerca più ampia.

### Il mio documento contiene testo colorato—`RemoveBackground` lo rovina?
`RemoveBackground` funziona sulla luminanza, quindi il testo colorato viene convertito in scala di grigi prima della pulizia. Se devi preservare il colore per elaborazioni successive, salta questo passaggio e affidati solo alla denoising.

### Come gestire PDF multi‑pagina?
Converti ogni pagina PDF in un'immagine (ad es., usando Aspose.PDF), poi passa ogni immagine attraverso la stessa pipeline. Cicla sulle pagine e concatena le stringhe `ocrResult.Text`.

### Posso migliorare l'accuratezza per appunti scritti a mano?
Considera di abilitare `ocrEngine.Options.UseNeuralNetwork = true;` (disponibile nelle versioni più recenti di Aspose) e aumenta la risoluzione dell'immagine ad almeno 300 dpi prima della elaborazione.

## Esempio completo funzionante (pronto per copia‑incolla)

Di seguito trovi l'intero file sorgente con tutte le direttive `using` necessarie e i commenti. Incollalo in un nuovo progetto console e premi **F5**.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the original image (skewed, noisy, etc.)
            Image originalImage = Image.Load("YOUR_DIRECTORY/skewed_noisy.jpg");

            // 2️⃣ Deskew – auto‑detect tilt up to 5°
            Image deskewed = ImageFilters.Deskew(originalImage, angleThreshold: 5);

            // 3️⃣ Denoise – smooth out speckles
            Image denoised = deskewed.Denoise();

            // 4️⃣ Remove background – boost contrast
            Image processedImage = denoised.RemoveBackground();

            // 5️⃣ Initialise OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // 6️⃣ Recognize text from the cleaned image
            OcrResult ocrResult = ocrEngine.Recognize(processedImage);

            // 7️⃣ Output the extracted text
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**Output previsto** (esempio per una semplice fattura):

```
=== OCR Output ===
Invoice #12345
Date: 2025‑12‑01
Total: $1,250.00
Thank you for your business!
```

Se l'output appare confuso, verifica che l'immagine di origine sia sufficientemente chiara e che l'angolo di correzione non superi la soglia impostata.

## Conclusione

Abbiamo coperto **come correggere l'inclinazione di un'immagine** passo dopo passo, mostrato **come rimuovere lo sfondo**, dimostrato **come estrarre il testo** mediante pre‑processing, e infine usato Aspose OCR per **riconoscere il testo da un'immagine**. L'intera pipeline è contenuta in un compatto programma C# che puoi estendere a elaborazione batch, conversione PDF o integrazione in un più ampio sistema di gestione documentale.

Pronto per la prossima sfida? Prova a fornire una cartella di PDF scansionati a questa pipeline, o sperimenta diverse impostazioni di denoise per vedere come influenzano i punteggi di confidenza. Più giochi con i parametri, più comprenderai i compromessi tra velocità e precisione.

Hai domande o un'immagine difficile che ancora non collabora? Lascia un commento qui sotto, e risolviamo insieme. Buona programmazione, e che i risultati del tuo OCR siano sempre cristallini!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}