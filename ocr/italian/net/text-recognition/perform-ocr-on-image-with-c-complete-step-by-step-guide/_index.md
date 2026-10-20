---
category: general
date: 2026-05-21
description: Esegui OCR su un'immagine usando C#. Scopri come caricare l'immagine
  per l'OCR, estrarre il testo da un PNG e riconoscere il testo dall'immagine con
  un piccolo esempio di codice.
draft: false
keywords:
- perform OCR on image
- extract text from PNG
- recognize text from image
- load image for OCR
language: it
og_description: Esegui OCR su un'immagine in C# rapidamente. Questa guida mostra come
  caricare l'immagine per l'OCR, estrarre il testo da PNG e riconoscere il testo dall'immagine
  con output HTML sensibile al layout.
og_title: Esegui OCR su Immagine con C# – Tutorial Completo di Programmazione
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Perform OCR on image using C#. Learn how to load image for OCR, extract
    text from PNG, and recognize text from image with a tiny code sample.
  headline: Perform OCR on Image with C# – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Perform OCR on image using C#. Learn how to load image for OCR, extract
    text from PNG, and recognize text from image with a tiny code sample.
  name: Perform OCR on Image with C# – Complete Step‑by‑Step Guide
  steps:
  - name: Load Image for OCR
    text: The line `engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");`
      is where we **load image for OCR**. The `ImageStream` helper abstracts away
      file‑format details, so you can feed JPEG, BMP, or TIFF without changing code.
  - name: Extract Text from PNG
    text: 'Once `engine.Recognize()` finishes, the OCR engine holds the recognized
      text internally. You can pull it out as a string if you only need raw text:'
  - name: Recognize Text from Image
    text: 'The `Recognize()` call does the heavy lifting. Under the hood the engine:'
  - name: Handling Layout‑Aware HTML Output
    text: 'Most developers stop at plain text, but the `HtmlSaveOptions` we used let
      you **perform OCR on image** and keep the visual structure intact. Two flags
      matter:'
  - name: Scaling to Multiple Files
    text: 'If you need to **perform OCR on image** files in a folder, wrap the core
      logic in a simple loop:'
  type: HowTo
tags:
- OCR
- C#
- Image Processing
- Aspose.OCR
title: Esegui OCR su un'immagine con C# – Guida completa passo passo
url: /it/net/text-recognition/perform-ocr-on-image-with-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esegui OCR su Immagine con C# – Guida Completa Passo‑Passo

Ti sei mai chiesto come **eseguire OCR su immagine** senza dover combattere con interfacce grafiche pesanti? Non sei l'unico. Che tu stia digitalizzando ricevute, estraendo dati da moduli scannerizzati, o semplicemente abbia bisogno di trasformare un PNG in testo ricercabile, poche righe di C# possono fare il lavoro.

In questo tutorial vedremo come caricare un'immagine per OCR, riconoscere il testo dall'immagine e, infine, estrarre il testo da PNG come HTML pulito. Alla fine avrai un'app console pronta all'uso che **esegue OCR su file immagine** e preserva il layout originale.

## Cosa Costruirai

- Un programma console minimale che legge un PNG (o qualsiasi immagine supportata)  
- Utilizza un motore OCR per **riconoscere testo da immagine**  
- Salva il risultato come HTML sensibile al layout, incorporando l'immagine originale  
- Mostra come **caricare immagine per OCR**, **estrarre testo da PNG** e gestire casi limite comuni  

> **Prerequisiti**  
> - .NET 6.0 SDK o successivo (puoi anche puntare a .NET Framework 4.7+)  
> - Una libreria OCR compatibile con NuGet – l'esempio usa *Aspose.OCR* ma qualsiasi libreria con API simile funzionerà  
> - Conoscenze di base di C# (nulla di complicato)  

Hai tutto? Ottimo—tuffiamoci.

## Esegui OCR su Immagine – Analisi Completa del Codice

Di seguito trovi il programma **completo e eseguibile**. Copialo e incollalo in un nuovo progetto console (`dotnet new console`) e premi **F5**.

```csharp
using System;
using Aspose.OCR;               // OCR engine namespace
using Aspose.OCR.Models;        // Save options namespace
using Aspose.OCR.ImageProcessing; // Image loading helpers

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine and set the language
            // -------------------------------------------------
            var engine = new OcrEngine
            {
                Language = OcrLanguage.English   // You can change to French, German, etc.
            };

            // -------------------------------------------------
            // Step 2: Load the image for OCR
            // -------------------------------------------------
            // Replace the path with your actual PNG/JPEG/TIFF file.
            engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");

            // -------------------------------------------------
            // Step 3: Perform OCR recognition
            // -------------------------------------------------
            engine.Recognize();

            // -------------------------------------------------
            // Step 4: Configure HTML save options – keep layout
            // -------------------------------------------------
            var htmlOptions = new HtmlSaveOptions
            {
                PreserveLayout = true,   // Keep columns, tables, and spacing
                EmbedImages = true       // Embed the original PNG inside the HTML
            };

            // -------------------------------------------------
            // Step 5: Save the recognized content as layout‑aware HTML
            // -------------------------------------------------
            engine.Save("YOUR_DIRECTORY/form.html", htmlOptions);

            Console.WriteLine("HTML with layout saved.");
        }
    }
}
```

> **Output previsto**  
> ```
> HTML with layout saved.
> ```  
> Dopo l'esecuzione troverai `form.html` accanto al tuo PNG. Aprilo in un browser e vedrai lo stesso layout, ma ora il testo sarà selezionabile e ricercabile.

### Carica Immagine per OCR

La riga `engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");` è dove **carichiamo l'immagine per OCR**. L'helper `ImageStream` astrae i dettagli del formato file, così puoi fornire JPEG, BMP o TIFF senza modificare il codice.  

**Perché non passare direttamente un `Bitmap`?**  
Perché molti SDK OCR si aspettano uno stream che includa anche i metadati DPI. Usare il loader integrato della libreria garantisce che il motore veda l'immagine esattamente come appare sullo schermo, migliorando l'accuratezza.

#### Consiglio professionale
Se stai elaborando un batch di file, avvolgi il passaggio di caricamento in un `try/catch` e registra eventuali `FileNotFoundException`. Questo impedisce che l'intero batch si blocchi perché un file mancante.

### Estrarre Testo da PNG

Una volta terminato `engine.Recognize()`, il motore OCR conserva internamente il testo riconosciuto. Puoi estrarlo come stringa se ti serve solo il testo grezzo:

```csharp
string plainText = engine.Text;   // Returns the whole document as plain text
Console.WriteLine(plainText);
```

Questo è il modo più rapido per **estrarre testo da PNG** quando non ti interessa il layout. Per la maggior parte dei lavori di inserimento dati, il testo semplice è sufficiente—ricorda solo di rimuovere le interruzioni di riga se prevedi di importarlo in un CSV.

### Riconoscere Testo da Immagine

La chiamata `Recognize()` svolge il lavoro pesante. Dietro le quinte il motore:

1. Normalizza l'immagine (rimuove inclinazioni, elimina rumore)  
2. La segmenta in linee e parole  
3. Esegue un classificatore neurale addestrato su milioni di glifi  

Poiché abbiamo impostato `Language = OcrLanguage.English`, il motore applica dizionari specifici per l'inglese, riducendo drasticamente i falsi positivi. Se ti serve supporto multilingue, passa semplicemente un array di lingue:

```csharp
engine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

### Gestione dell'Output HTML Sensibile al Layout

La maggior parte degli sviluppatori si ferma al testo semplice, ma le `HtmlSaveOptions` che abbiamo usato ti permettono di **eseguire OCR su immagine** mantenendo intatta la struttura visiva. Due flag sono importanti:

- `PreserveLayout = true` – conserva colonne, tabelle e spaziature.  
- `EmbedImages = true` – inserisce il PNG originale come elemento `<img>` codificato in Base64, rendendo l'HTML autonomo.

Se preferisci un file più leggero, imposta `EmbedImages = false` e l'HTML farà riferimento al PNG originale su disco.

#### Caso limite: File di grandi dimensioni

Per immagini superiori a 5 MB, l'incorporamento può gonfiare le dimensioni dell'HTML. In questi casi, passa a riferimenti esterni alle immagini e considera di comprimere il PNG in anticipo con `ImageProcessor.Compress`.

## Problemi Comuni e Consigli Professionali

| Sintomo | Probabile Causa | Soluzione |
|--------|--------------|-----|
| Caratteri illeggibili | Lingua impostata errata o pacchetto lingua mancante | Installa i file di dati della lingua appropriata e imposta correttamente `engine.Language` |
| Nessun testo nell'output | Immagine troppo scura o a bassa risoluzione | Pre‑elabora con `engine.Image = ImageProcessor.AdjustContrast(engine.Image, 1.2)` |
| Layout rotto in HTML | `PreserveLayout` lasciato al valore predefinito `false` | Imposta `PreserveLayout = true` in `HtmlSaveOptions` |
| Elaborazione lenta su molte pagine | Il motore si reinizializza per ogni file | Riutilizza la stessa istanza di `OcrEngine` e cambia solo `engine.Image` ad ogni ciclo |

### Scalare a più File

Se devi **eseguire OCR su immagine** in una cartella, avvolgi la logica principale in un semplice ciclo:

```csharp
foreach (var file in Directory.GetFiles("YOUR_DIRECTORY", "*.png"))
{
    engine.Image = ImageStream.FromFile(file);
    engine.Recognize();
    var htmlPath = Path.ChangeExtension(file, ".html");
    engine.Save(htmlPath, htmlOptions);
    Console.WriteLine($"Processed {Path.GetFileName(file)}");
}
```

Nota che **carichiamo l'immagine per OCR** all'interno del ciclo, ma manteniamo gli stessi oggetti `engine` e `htmlOptions`. Questo riduce il churn di memoria e velocizza i lavori batch.

## Andare Oltre: Esportare in PDF o DOCX

Il medesimo `engine` può salvare in altri formati:

```csharp
engine.Save("output.pdf", new PdfSaveOptions { PreserveLayout = true });
engine.Save("output.docx", new WordSaveOptions { PreserveLayout = true });
```

Se il tuo sistema a valle richiede PDF ricercabili, è una modifica a una riga—non serve creare una pipeline di conversione separata.

## Conclusione

Ti abbiamo appena mostrato come **eseguire OCR su immagine** con C#, dal caricamento della foto a **estrarre testo da PNG** e infine **riconoscere testo da immagine** in un file HTML sensibile al layout. L'esempio completo è pronto per l'esecuzione, e ora comprendi perché ogni passaggio è importante, come adattarlo a lingue diverse e quali insidie tenere d'occhio.

Ora prova a sostituire la lingua inglese con un'altra locale, sperimenta `PreserveLayout = false` per ottenere un HTML più snello, o indirizza l'output di testo semplice verso un database per archivi ricercabili. Il cielo è il limite quando combini un motore OCR solido con poche righe di C#.

Hai domande sulla gestione di TIFF multi‑pagina, o vuoi sapere come integrare tutto in un'API ASP.NET Core? Lascia un commento qui sotto, e buona programmazione!

## Tutorial Correlati

- [Estrai testo da immagine C# con selezione della lingua usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Come Estrarre Testo da Immagine Preparando Rettangoli in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Estrai Testo da Immagine – Riconosci Linea con Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}