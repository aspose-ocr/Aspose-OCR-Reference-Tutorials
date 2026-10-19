---
category: general
date: 2026-04-17
description: Come raddrizzare rapidamente un'immagine usando Aspose.OCR – impara a
  caricare l'immagine per OCR, preelaborare l'immagine per OCR e riconoscere il testo
  dell'immagine con alta precisione.
draft: false
keywords:
- how to deskew image
- recognize text image
- improve ocr accuracy
- load image ocr
- preprocess image ocr
language: it
og_description: Come correggere l'inclinazione di un'immagine e migliorare l'accuratezza
  OCR in C#. Impara a caricare l'immagine per OCR, pre‑elaborare l'immagine per OCR
  e riconoscere il testo dell'immagine con Aspose.OCR.
og_title: Come raddrizzare un'immagine – Tutorial completo OCR in C#
tags:
- Aspose.OCR
- C#
- Image Processing
title: Come correggere l'inclinazione dell'immagine e migliorare l'accuratezza OCR
  in C# – Guida passo passo
url: /it/net/ocr-optimization/how-to-deskew-image-and-boost-ocr-accuracy-in-c-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come raddrizzare un'immagine e migliorare l'accuratezza OCR in C#

**Come raddrizzare un'immagine** è un ostacolo comune ogni volta che devi estrarre testo da una foto che non è perfettamente allineata. In questa guida vedremo come caricare l'immagine, pre‑elaborarla e infine **riconoscere il testo dell'immagine** usando la potente catena di filtri di Aspose.OCR.

Se hai mai puntato la fotocamera del telefono su una ricevuta, un cartello o un modulo scansionato e sei finito con caratteri storti e illeggibili, sai quanto può essere frustrante. La buona notizia? Poche righe di codice C# possono raddrizzare l'immagine, eliminare il rumore e darti una stringa pulita che puoi effettivamente usare. Tratteremo anche come **migliorare l'accuratezza OCR** regolando i passaggi di pre‑elaborazione.

## Cosa ti serve

- .NET 6.0 o successivo (il codice funziona anche con .NET Core)  
- Una licenza o una copia di valutazione di **Aspose.OCR** (disponibile via NuGet)  
- Un file immagine leggermente ruotato o rumoroso (ad es., `skewed_photo.png`)  

Nessuno strumento di terze parti complicato—solo la libreria Aspose.OCR e un po' di conoscenza di C#.

![Esempio di come raddrizzare un'immagine](/images/deskew-demo.png "Come raddrizzare un'immagine – originale vs corretto")

---

## Passo 1 – Caricare l'immagine OCR: Preparare il file sorgente

Prima di poter raddrizzare qualcosa, dobbiamo portare l'immagine in memoria. Il metodo `OcrImage.FromFile` fa esattamente questo.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Load the image you want to process
var ocrImage = OcrImage.FromFile(@"C:\Images\skewed_photo.png");
```

> **Perché è importante:** Caricare l'immagine come `OcrImage` fornisce al motore OCR l'accesso diretto ai dati dei pixel, fondamentale per i successivi passaggi di **pre‑elaborazione dell'immagine OCR**. Se il percorso del file è errato, otterrai una `FileNotFoundException`, quindi verifica attentamente la posizione.

## Passo 2 – Pre‑elaborazione dell'immagine OCR: Costruire una catena di filtri per il deskew

Ora arriva il cuore di **come raddrizzare un'immagine**. Aspose.OCR include una collezione di filtri che puoi impilare in qualsiasi ordine. Per la maggior parte delle foto reali vorrai:

1. **Deskew** – correggere la rotazione  
2. **Denoise** – eliminare i punti di sale e pepe  
3. **ContrastEnhance** – far risaltare i caratteri deboli  

```csharp
// Create a chain of preprocessing filters
var filterChain = new ImageFilterCollection
{
    new DeskewFilter(),          // Detects and corrects rotation
    new DenoiseFilter(),        // Reduces noise
    new ContrastEnhanceFilter() // Boosts contrast for faint text
};

// Apply the filter chain to obtain a cleaned image
var filteredImage = filterChain.Apply(ocrImage);
```

> **Consiglio professionale:** Se la tua immagine è già ben esposta, puoi omettere il `ContrastEnhanceFilter`. Meno elaborazione significa esecuzione più veloce.

### Casi particolari

- **Rotazione estrema (>45°):** Il `DeskewFilter` funziona al meglio fino a circa 30°. Per angoli più ampi potresti dover ruotare l'immagine manualmente prima (`filteredImage.Rotate(…)`).
- **Sfondi colorati:** Converti in scala di grigi prima della denoising per risultati migliori (`filteredImage = filteredImage.ToGrayscale();`).

## Passo 3 – Riconoscere il testo dell'immagine: Eseguire il motore OCR

Con un bitmap pulito e raddrizzato, è il momento di estrarre i caratteri.

```csharp
// Create an OCR engine instance
using var ocrEngine = new OcrEngine();

// Recognize text from the filtered image
var ocrResult = ocrEngine.Recognize(filteredImage);

// Display the recognized text
Console.WriteLine(ocrResult.Text);
```

> **Cosa succede dietro le quinte?** `OcrEngine` esegue un riconoscitore basato su rete neurale che si aspetta un'immagine quasi verticale e ad alto contrasto. Ecco perché il precedente passaggio di **pre‑elaborazione dell'immagine OCR** è cruciale per **migliorare l'accuratezza OCR**.

### Output previsto

Se la foto originale conteneva la riga “Invoice #12345 – Total $89.99”, la console stamperà qualcosa di simile:

```
Invoice #12345 – Total $89.99
```

Se vedi caratteri incomprensibili, rivedi la catena di filtri—potrebbe servire una nitidezza aggiuntiva (`new SharpenFilter()`).

## Passo 4 – Ottimizzare per una migliore accuratezza OCR

Anche dopo il deskew, l'OCR può inciampare su alcuni font o scansioni a bassa risoluzione. Ecco alcuni piccoli aggiustamenti:

| Problema | Correzione |
|----------|------------|
| Dimensione del font piccola (<10 pt) | Ingrandire l'immagine (`filteredImage = filteredImage.Resize(2.0);`) |
| Testo grigio chiaro su sfondo bianco | Aumentare ulteriormente il contrasto (`new ContrastEnhanceFilter(1.5)`) |
| Testo multilingue | Impostare `ocrEngine.Language = OcrLanguage.Multilingual;` |

Queste modifiche migliorano direttamente **l'accuratezza OCR** senza cambiare la struttura principale del codice.

## Esempio completo funzionante

Di seguito trovi il programma completo, pronto per l'esecuzione, che incorpora tutti i passaggi descritti. Copialo in un nuovo progetto console e premi **F5**.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // Step 1: Load the image you want to process
        var ocrImage = OcrImage.FromFile(@"C:\Images\skewed_photo.png");

        // Step 2: Build a chain of preprocessing filters
        var filterChain = new ImageFilterCollection
        {
            new DeskewFilter(),          // Detects and corrects rotation
            new DenoiseFilter(),        // Reduces salt‑and‑pepper noise
            new ContrastEnhanceFilter() // Improves faint characters
        };

        // Step 3: Apply the filter chain to obtain a cleaned image
        var filteredImage = filterChain.Apply(ocrImage);

        // Step 4: Create an OCR engine instance
        using var ocrEngine = new OcrEngine();

        // Optional: set language or other engine options here
        // ocrEngine.Language = OcrLanguage.English;

        // Step 5: Recognize text from the filtered image
        var ocrResult = ocrEngine.Recognize(filteredImage);

        // Step 6: Display the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Esegui il programma e dovresti vedere il testo pulito e raddrizzato stampato nella console.

## Domande frequenti

**D: Funziona anche sui PDF?**  
R: Sì. Converti ogni pagina PDF in un'immagine (ad es., usando `Aspose.PDF`) e passa il bitmap risultante nella stessa catena di filtri.

**D: E se la mia immagine è già perfettamente allineata?**  
R: Il `DeskewFilter` rileverà un angolo quasi nullo e lascerà l'immagine invariata—nessun danno.

**D: Posso elaborare più immagini in batch?**  
R: Assolutamente. Avvolgi il codice in un ciclo `foreach (var path in Directory.GetFiles(...))` e salva ogni `ocrResult.Text` in una lista o in un file.

---

## Conclusione

Abbiamo mostrato **come raddrizzare un'immagine** programmaticamente, attraversato il passo **caricare l'immagine OCR**, applicato una robusta pipeline di **pre‑elaborazione dell'immagine OCR** e infine **riconosciuto il testo dell'immagine** con Aspose.OCR. Regolando i filtri e, opzionalmente, scalando o nitidendo, puoi **migliorare l'accuratezza OCR** per una vasta gamma di scenari reali.

Pronto per la prossima sfida? Prova a integrare questa pipeline in una Web API, o sperimenta il riconoscimento di note scritte a mano aggiungendo `new BinarizationFilter()` prima del deskew. Le possibilità sono infinite—buon coding!

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}