---
category: general
date: 2026-06-22
description: Riconosci il testo da un'immagine usando Aspose OCR in C#. Scopri come
  correggere automaticamente l'inclinazione dell'immagine, preelaborare l'immagine
  per l'OCR e abilitare la correzione automatica dell'inclinazione in un conciso esempio
  OCR in C#.
draft: false
keywords:
- recognize text from image
- auto deskew image
- preprocess image for ocr
- c# ocr example
- enable auto deskew
language: it
og_description: Riconosci il testo da un'immagine con Aspose OCR in C#. Questa guida
  mostra come correggere automaticamente l'inclinazione dell'immagine, preelaborare
  l'immagine per l'OCR e abilitare la correzione automatica dell'inclinazione in un
  esempio pratico di OCR in C#.
og_title: Riconosci il testo da un'immagine in C# – Esempio completo di OCR
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Recognize text from image using Aspose OCR in C#. Learn how to auto
    deskew image, preprocess image for OCR, and enable auto deskew in a concise c#
    ocr example.
  headline: Recognize Text from Image in C# – Full OCR Example
  type: TechArticle
- description: Recognize text from image using Aspose OCR in C#. Learn how to auto
    deskew image, preprocess image for OCR, and enable auto deskew in a concise c#
    ocr example.
  name: Recognize Text from Image in C# – Full OCR Example
  steps:
  - name: 1. Low Contrast or Dark Backgrounds
    text: 'Aspose.OCR offers an extra flag `PreprocessingOptions.ContrastEnhancement`.
      Add it to the `Preprocessing` line:'
  - name: 2. Non‑English Documents
    text: Swap `OcrLanguage.English` for `OcrLanguage.Spanish`, `OcrLanguage.French`,
      etc. The engine auto‑loads the appropriate language model.
  - name: 3. Large Images
    text: 'Processing a 5 MP photo can be memory‑hungry. Scale it down first:'
  - name: 4. Getting Bounding Boxes
    text: 'If you need the exact location of each word (e.g., for a UI overlay), iterate
      over `result.Regions`:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Riconosci il testo da un'immagine in C# – Esempio completo di OCR
url: /it/net/ocr-optimization/recognize-text-from-image-in-c-full-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Riconoscere il testo da un'immagine in C# – Esempio completo di OCR

Ti sei mai chiesto come **recognize text from image** in un'applicazione C# senza impazzire per scansioni sfocate? Non sei solo. Che tu stia digitalizzando ricevute, estraendo dati da moduli, o semplicemente giocando con trucchi di immagine alimentati dall'AI, ottenere risultati OCR puliti dipende da una corretta pre‑elaborazione—pensa a auto deskew image e riduzione del rumore.  

In questo tutorial vedremo un **c# ocr example** che utilizza la libreria Aspose.OCR per **enable auto deskew**, raddrizzare automaticamente le foto inclinate e **preprocess image for OCR** in poche righe di codice. Alla fine avrai un programma eseguibile che stampa il testo riconosciuto direttamente sulla console.

## Cosa imparerai

- Come installare e fare riferimento al pacchetto NuGet Aspose.OCR.  
- Configurare un `OcrEngine` con supporto per la lingua inglese.  
- Abilitare **auto deskew image** e altre opzioni di pre‑elaborazione in un unico passaggio.  
- Eseguire il motore su una foto reale e gestire l'output.  
- Suggerimenti per gestire casi limite come immagini fortemente ruotate o scansioni a basso contrasto.

> **Prerequisiti** – Hai bisogno di .NET 6 (o successivo) e una conoscenza di base di C#. Non è richiesta esperienza pregressa con OCR.

---

## ## Riconoscere il testo da immagine – Installa il pacchetto Aspose.OCR

Prima di scrivere qualsiasi codice, la libreria deve essere aggiunta al progetto. Apri un terminale nella cartella della tua soluzione ed esegui:

```bash
dotnet add package Aspose.OCR
```

Questo comando scarica l'ultima versione stabile di Aspose.OCR, che include il motore OCR, i pacchetti lingua e le utility di pre‑elaborazione di cui avremo bisogno.  

*Pro tip:* Se stai puntando a .NET Framework anziché .NET Core, usa l'interfaccia UI del Visual Studio NuGet Package Manager—cerca “Aspose.OCR” e fai clic su **Install**.

## ## Riconoscere il testo da immagine – Inizializza il motore OCR

Ora che il pacchetto è pronto, possiamo creare il motore. Il primo passo è indicare al motore quale lingua aspettarsi. Nella maggior parte dei casi l'inglese è sufficiente, ma la libreria supporta decine di lingue pronte all'uso.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine and set the language to English
        var engine = new OcrEngine
        {
            Language = OcrLanguage.English,

            // Step 2: Enable preprocessing to automatically deskew and denoise the image
            Preprocessing = PreprocessingOptions.AutoDeskew | PreprocessingOptions.Denoise
        };
```

**Perché è importante:**  
- `Language = OcrLanguage.English` indica al motore quale set di caratteri usare, migliorando drasticamente la precisione.  
- La proprietà `Preprocessing` combina due flag—`AutoDeskew` e `Denoise`. Questo passaggio **auto deskew image** ruota l'immagine riportandola a una linea orizzontale, mentre `Denoise` rimuove gli artefatti granulosi che altrimenti confonderebbero il motore OCR.  

Se salti la pre‑elaborazione, spesso otterrai output confuso su ricevute scansionate o foto scattate di lato.

## ## Riconoscere il testo da immagine – Fornisci l'immagine al motore

Con il motore pronto, il passo successivo è fornire un file immagine. Aspose.OCR accetta un percorso o uno `Stream`, così puoi lavorare con file locali, risorse incorporate o anche immagini scaricate dal web.

```csharp
        // Step 3: Recognize text from the input image
        var result = engine.RecognizeImage(@"YOUR_DIRECTORY/skewed_photo.jpg");
```

**Nota sui casi limite:**  
- Se l'immagine è **heavily rotated** (> 45°), `AutoDeskew` farà comunque del suo meglio, ma potresti volerla pre‑ruotare manualmente usando `System.Drawing` o `ImageSharp` prima di passarla al motore.  
- Per **multi‑page PDFs**, chiama `engine.RecognizePdf` invece; gli stessi flag di pre‑elaborazione si applicano.

## ## Riconoscere il testo da immagine – Output del risultato

Infine, mostriamo il testo estratto. L'oggetto `result` contiene più del semplice testo—offre anche punteggi di confidenza, bounding box e l'immagine originale con le regioni evidenziate. Per una demo veloce, stampare `result.Text` è sufficiente.

```csharp
        // Step 4: Output the recognized text to the console
        System.Console.WriteLine(result.Text);
    }
}
```

Quando esegui il programma, dovresti vedere qualcosa del genere:

```
Invoice #12345
Date: 2026-06-01
Total: $256.78
Thank you for your business!
```

Se l'output appare confuso, verifica che l'immagine di origine sia chiara, ben illuminata, e che **preprocess image for OCR** sia effettivamente abilitato (i flag `Preprocessing` sopra).  

## ## Riconoscere il testo da immagine – Gestione dei problemi comuni

### 1. Basso contrasto o sfondi scuri
Aspose.OCR offre un flag aggiuntivo `PreprocessingOptions.ContrastEnhancement`. Aggiungilo alla riga `Preprocessing`:

```csharp
Preprocessing = PreprocessingOptions.AutoDeskew |
                PreprocessingOptions.Denoise |
                PreprocessingOptions.ContrastEnhancement
```

### 2. Documenti non‑inglesi
Sostituisci `OcrLanguage.English` con `OcrLanguage.Spanish`, `OcrLanguage.French`, ecc. Il motore carica automaticamente il modello linguistico appropriato.

### 3. Immagini grandi
Elaborare una foto da 5 MP può consumare molta memoria. Ridimensionala prima:

```csharp
engine.Image = ImageProcessor.Resize(@"YOUR_DIRECTORY/skewed_photo.jpg", 1024, 768);
```

### 4. Ottenere le bounding box
Se ti serve la posizione esatta di ogni parola (ad esempio per un overlay UI), itera su `result.Regions`:

```csharp
foreach (var region in result.Regions)
{
    System.Console.WriteLine($"{region.Text} at {region.Bounds}");
}
```

## ## Riconoscere il testo da immagine – Esempio completo funzionante

Di seguito trovi il programma **completo, pronto da copiare‑incollare** che incorpora tutti i suggerimenti sopra. Salvalo come `Program.cs`, sostituisci `YOUR_DIRECTORY` con la cartella che contiene la tua immagine di test, ed esegui `dotnet run`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

class Program
{
    static void Main()
    {
        // Create and configure the OCR engine
        var engine = new OcrEngine
        {
            Language = OcrLanguage.English,
            // Enable auto deskew, denoise, and contrast enhancement
            Preprocessing = PreprocessingOptions.AutoDeskew |
                            PreprocessingOptions.Denoise |
                            PreprocessingOptions.ContrastEnhancement
        };

        // Path to the image you want to process
        string imagePath = @"YOUR_DIRECTORY/skewed_photo.jpg";

        // Recognize the image
        var result = engine.RecognizeImage(imagePath);

        // Output plain text
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);
        Console.WriteLine();

        // Optional: print bounding boxes for each detected region
        Console.WriteLine("=== Detected Regions ===");
        foreach (var region in result.Regions)
        {
            Console.WriteLine($"{region.Text}  -->  {region.Bounds}");
        }
    }
}
```

**Output console previsto** (supponendo che l'immagine contenga una semplice ricevuta):

```
=== Recognized Text ===
Invoice #12345
Date: 2026-06-01
Total: $256.78
Thank you for your business!

=== Detected Regions ===
Invoice #12345  -->  {X=12,Y=34,Width=250,Height=20}
Date: 2026-06-01  -->  {X=12,Y=60,Width=200,Height=18}
Total: $256.78  -->  {X=12,Y=86,Width=180,Height=18}
Thank you for your business!  -->  {X=12,Y=112,Width=300,Height=22}
```

Se vedi il testo stampato correttamente, congratulazioni—hai **recognize text from image** con auto‑deskewing e pre‑elaborazione!

## ## Riconoscere il testo da immagine – Prossimi passi e argomenti correlati

- **Batch processing:** Avvolgi la chiamata al motore all'interno di un ciclo `foreach` per gestire decine di foto in una volta.  
- **PDF conversion:** Usa `engine.RecognizePdf` per documenti multi‑pagina, poi unisci i risultati.  
- **Custom dictionaries:** Fornisci una lista di parole a `engine.CustomWords` per migliorare la precisione su terminologia specifica del dominio (ad es., codici medici).  
- **Performance tuning:** Metti in cache l'istanza `OcrEngine` se stai elaborando molte immagini; la creazione del motore è l'operazione più costosa.  

Queste estensioni coinvolgono naturalmente gli stessi concetti—**preprocess image for OCR**, **enable auto deskew**, e **recognize text from image**—così puoi riutilizzare i pattern di codice appena appresi.

## Conclusione

Abbiamo appena esaminato un **c# ocr example** che mostra come **recognize text from image** usando Aspose.OCR, mentre si deskewa e si denoise automaticamente l'immagine. Abilitando `AutoDeskew` (la funzionalità **auto deskew image**) e aggiungendo alcuni flag di pre‑elaborazione, aumenti drasticamente l'affidabilità dell'OCR senza scrivere una sola riga di codice per la manipolazione delle immagini.

Ora puoi prendere questo scheletro, inserire le tue immagini e iniziare a estrarre dati da fatture, ID o qualsiasi altro tipo di documento cartaceo. Hai una scansione difficile? Prova le opzioni di pre‑elaborazione extra che abbiamo menzionato, o sperimenta con pacchetti linguistici personalizzati. Il cielo è il limite.

Se questa guida ti ha aiutato a sbloccare la situazione, lascia un commento, condividi i tuoi risultati, o contattami su GitHub—buon coding!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come usare AspOCR: Filtri di pre‑elaborazione OCR per immagini in .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Estrai testo da immagine – Ottimizzazione OCR con Aspose.OCR per .NET](/ocr/english/net/ocr-optimization/)
- [Come estrarre testo da immagine usando Aspose.OCR per .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}