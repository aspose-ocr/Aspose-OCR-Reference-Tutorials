---
category: general
date: 2026-11-26
description: Scopri come eseguire l'OCR su file PNG, convertire PNG in testo ed estrarre
  testo cirillico usando Aspose.OCR – guida passo‑passo per sviluppatori.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- convert PNG to text
- recognize text from PNG
- extract Cyrillic text
- load image for OCR
language: it
lastmod: 2026-11-26
og_description: Come eseguire l'OCR su file PNG ed estrarre testo cirillico usando
  Aspose.OCR in C#. Segui questo tutorial completo per convertire PNG in testo.
og_image_alt: how to perform OCR on a PNG image using Aspose.OCR
og_title: Come eseguire l'OCR su immagini PNG con Aspose.OCR – Guida C#
schemas:
- author: Aspose
  dateModified: '2026-11-26'
  description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  headline: How to perform OCR on PNG images with Aspose.OCR in C#
  type: TechArticle
- description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  name: How to perform OCR on PNG images with Aspose.OCR in C#
  steps:
  - name: Handling large images
    text: 'If the PNG is larger than 2 MB, consider down‑scaling it before recognition
      to speed up processing:'
  - name: 'Edge case: Missing language module'
    text: 'If the download fails (e.g., offline environment), the engine throws an
      `OcrException`. Catch it to provide a graceful fallback:'
  - name: Expected output
    text: 'If `sample_image.png` contains the Cyrillic phrase “Привет мир”, the console
      will display:'
  - name: How it works
    text: 1. **Engine creation** – prepares the OCR pipeline. 2. **Image loading**
      – supports both raw PNG and down‑scaled versions for performance. 3. **Language
      selection** – demonstrates **extract Cyrillic text** while handling missing
      modules. 4. **Recognition** – the core **recognize text from PNG** call
  type: HowTo
tags:
- OCR
- C#
- Aspose.OCR
title: Come eseguire l'OCR su immagini PNG con Aspose.OCR in C#
url: /it/net/text-recognition/how-to-perform-ocr-on-png-images-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR su immagini PNG con Aspose.OCR in C#

Se hai bisogno di **come eseguire OCR** su un file PNG, questa guida ti mostra i passaggi esatti per convertire PNG in testo usando Aspose.OCR. Che tu stia estraendo testo cirillico da documenti scansionati o semplicemente riconoscendo testo da screenshot PNG, la soluzione funziona subito e richiede solo poche righe di codice C#.

In questo tutorial imparerai a:

* **caricare immagine per OCR** da una cartella locale,
* configurare il motore per **estrarre testo cirillico**,
* **riconoscere testo da PNG** e ottenere una stringa pulita,
* gestire problemi comuni come moduli lingua mancanti e immagini di grandi dimensioni.

Non è necessaria alcuna esperienza pregressa con Aspose.OCR—basta un ambiente di sviluppo .NET e un'immagine PNG che desideri elaborare.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* .NET 6.0 (o successivo) installato.
* Una copia con licenza o di prova di **Aspose.OCR for .NET**. Puoi ottenere una prova gratuita dal sito web di Aspose.
* Visual Studio 2022 (o qualsiasi IDE che supporti .NET).
* Un file PNG contenente il testo che vuoi estrarre (l'esempio utilizza `sample_image.png`).

## Passo 1: Installa il pacchetto NuGet Aspose.OCR

Apri un terminale nella cartella del tuo progetto ed esegui:

```bash
dotnet add package Aspose.OCR
```

Il pacchetto include il motore OCR di base e tutti i moduli lingua. Quando richiedi una lingua che non è presente localmente, Aspose.OCR scarica automaticamente il modulo necessario.

## Passo 2: Crea un'istanza del motore OCR (come eseguire OCR)

Il primo passo pratico in qualsiasi flusso di lavoro OCR è istanziare il motore. Questo oggetto gestisce tutte le operazioni successive, come il caricamento dell'immagine e il riconoscimento.

```csharp
using Aspose.OCR;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

**Perché è importante:** La classe `OcrEngine` incapsula la pipeline OCR. Creare un'unica istanza e riutilizzarla su più immagini riduce il consumo di memoria e migliora le prestazioni.

## Passo 3: Carica immagine per OCR – specifica il file PNG di origine

Il caricamento dell'immagine è il punto in cui **carichi immagine per OCR**. Aspose.OCR accetta diversi tipi di input; il più semplice è `ImageStream.FromFile`.

```csharp
// Load the PNG image from disk
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_image.png");
```

> **Suggerimento professionale:** Usa un percorso assoluto o `Path.Combine` per evitare errori di runtime in ambienti diversi.

### Gestione di immagini grandi

Se il PNG è più grande di 2 MB, considera di ridimensionarlo prima del riconoscimento per velocizzare l'elaborazione:

```csharp
using System.Drawing;

// Downscale large images to a maximum width of 1200 pixels
Bitmap original = new Bitmap(@"YOUR_DIRECTORY/sample_image.png");
int maxWidth = 1200;
int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

using (var ms = new MemoryStream())
{
    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
    ocrEngine.Image = ImageStream.FromStream(ms);
}
```

## Passo 4: Configura la lingua – estrarre testo cirillico

Per impostazione predefinita, Aspose.OCR assume l'inglese. Per **estrarre testo cirillico**, imposta la proprietà `Language` su `Language.Cyrillic`. Il modulo richiesto verrà scaricato automaticamente al primo avvio del codice.

```csharp
// Set the OCR language to Cyrillic
ocrEngine.Language = Language.Cyrillic;
```

Se hai bisogno di riconoscere più lingue (ad es. inglese e cirillico), puoi combinarle:

```csharp
ocrEngine.Language = Language.English | Language.Cyrillic;
```

### Caso limite: Modulo lingua mancante

Se il download fallisce (ad es. ambiente offline), il motore genera un'`OcrException`. Catturala per fornire un fallback elegante:

```csharp
try
{
    ocrEngine.Language = Language.Cyrillic;
}
catch (OcrException ex)
{
    Console.WriteLine($"Language module could not be loaded: {ex.Message}");
    // Optionally, fall back to English or abort the process
}
```

## Passo 5: Esegui l'operazione di riconoscimento (riconoscere testo da PNG)

Ora che l'immagine e la lingua sono impostate, puoi **riconoscere testo da PNG**. Il metodo `Recognize` esegue la pipeline OCR in modo sincrono.

```csharp
// Run OCR
ocrEngine.Recognize();
```

**Perché funziona:** Internamente, Aspose.OCR applica pre‑elaborazioni (binarizzazione, rimozione del rumore) prima di inviare l'immagine a un riconoscitore basato su rete neurale ottimizzato per la lingua selezionata.

## Passo 6: Recupera e visualizza il testo riconosciuto (convertire PNG in testo)

Dopo il riconoscimento, la stringa estratta è disponibile tramite la proprietà `Text`. Questo è il passaggio finale in **convertire PNG in testo**.

```csharp
// Get the recognized text
string recognizedText = ocrEngine.Text;

// Output the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

### Output previsto

Se `sample_image.png` contiene la frase cirillica “Привет мир”, la console mostrerà:

```
=== OCR Result ===
Привет мир
```

L'output può includere interruzioni di riga e punteggiatura esattamente come appaiono nell'immagine. Puoi post‑processare la stringa con `String.Trim()`, `Regex` o altre utility di pulizia del testo, se necessario.

## Passo 7: Opzionale – Salva il risultato in un file

Salvare il risultato OCR consente ulteriori elaborazioni (ad es. indicizzazione, traduzione). Ecco un modo rapido per scrivere il testo in un file UTF‑8:

```csharp
File.WriteAllText(@"YOUR_DIRECTORY/ocr_output.txt", recognizedText, Encoding.UTF8);
Console.WriteLine("OCR text saved to ocr_output.txt");
```

## Problemi comuni e come evitarli

| Problema | Sintomo | Soluzione |
|----------|---------|-----------|
| **Modulo lingua mancante** | `OcrException` su `Language = Language.Cyrillic` | Assicurati di avere connettività internet al primo avvio o pre‑scarica i moduli tramite il pacchetto offline di Aspose. |
| **Immagine sfocata o a basso contrasto** | Scarsa accuratezza, molti caratteri “?” | Pre‑elabora l'immagine: aumenta il contrasto, applica sharpening o converti in scala di grigi prima di passarla al motore. |
| **PNG molto grande** | Tempo di elaborazione lungo, possibile `OutOfMemoryException` | Ridimensiona come mostrato nel Passo 3, oppure dividi un'immagine multi‑pagina in tasselli separati. |
| **Caratteri non UTF‑8** | Output corrotto | Verifica che la console o lo scrittore di file utilizzi la codifica UTF‑8 (`Encoding.UTF8`). |

## Esempio completo, eseguibile

Di seguito trovi il programma completo che incorpora tutti i passaggi sopra descritti. Copialo in un nuovo progetto console e eseguilo dopo aver adeguato i percorsi dei file.

```csharp
using System;
using System.Drawing;
using System.IO;
using System.Text;
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1. Create OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // 2. Load PNG image (with optional down‑scaling for large files)
            string imagePath = @"YOUR_DIRECTORY/sample_image.png";
            Bitmap original = new Bitmap(imagePath);
            const int maxWidth = 1200;

            if (original.Width > maxWidth)
            {
                int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
                Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

                using (var ms = new MemoryStream())
                {
                    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    ocrEngine.Image = ImageStream.FromStream(ms);
                }
            }
            else
            {
                ocrEngine.Image = ImageStream.FromFile(imagePath);
            }

            // 3. Set language to Cyrillic (fallback to English if needed)
            try
            {
                ocrEngine.Language = Language.Cyrillic;
            }
            catch (OcrException ex)
            {
                Console.WriteLine($"Failed to load Cyrillic module: {ex.Message}");
                Console.WriteLine("Falling back to English.");
                ocrEngine.Language = Language.English;
            }

            // 4. Recognize text
            ocrEngine.Recognize();

            // 5. Retrieve and display the text (convert PNG to text)
            string recognizedText = ocrEngine.Text;
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(recognizedText);

            // 6. Save result to a UTF‑8 file
            string outputPath = @"YOUR_DIRECTORY/ocr_output.txt";
            File.WriteAllText(outputPath, recognizedText, Encoding.UTF8);
            Console.WriteLine($"OCR text saved to {outputPath}");
        }
    }
}
```

### Come funziona

1. **Creazione del motore** – prepara la pipeline OCR.  
2. **Caricamento dell'immagine** – supporta sia PNG grezzi sia versioni ridimensionate per le prestazioni.  
3. **Selezione della lingua** – dimostra **estrarre testo cirillico** gestendo i moduli mancanti.  
4. **Riconoscimento** – la chiamata principale **riconoscere testo da PNG**.  
5. **Gestione del risultato** – mostra **convertire PNG in testo** e scrive l'output in un file.

Esegui il programma con `dotnet run`. Se tutto è configurato correttamente, vedrai il testo riconosciuto stampato sulla console e salvato in `ocr_output.txt`.

## Conclusione

In questo tutorial hai imparato **come eseguire OCR** su file PNG usando Aspose.OCR per .NET, coprendo tutto, dal **caricare immagine per OCR** all'**estrarre testo cirillico** e **convertire PNG in testo**. L'esempio completo e eseguibile dimostra il flusso di lavoro standard, i casi limite comuni e consigli pratici per mantenere affidabile la tua pipeline OCR.

**Passi successivi**

* Esplora **riconoscere testo da PNG** con lingue aggiuntive (arabo, cinese) combinando i flag `Language`.  
* Integra il risultato OCR con Azure Cognitive Search per archivi di documenti ricercabili.  
* Sperimenta le impostazioni di `OcrEngine` di Aspose.OCR come `Resolution

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Download Aspose.OCR Model and Extract Text from PNG in C#](/ocr/english/net/text-recognition/how-to-download-ocr-model-and-extract-text-from-png-using-as/)
- [How to Perform OCR in C# – Recognize Cyrillic Text with Aspose](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-recognize-cyrillic-text-with-aspose/)
- [How to Batch OCR in C# – Fast Way to Extract Text PNG Files](/ocr/english/net/ocr-optimization/how-to-batch-ocr-in-c-fast-way-to-extract-text-png-files/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}