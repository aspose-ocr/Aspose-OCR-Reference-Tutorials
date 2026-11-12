---
category: general
date: 2026-10-11
description: Scopri come eseguire l'OCR su un'immagine in C# con Aspose.OCR, includendo
  l'installazione di System.Drawing.Common e l'estrazione del testo da file JPG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from JPG
- recognize text from picture
- load image for OCR
- install System.Drawing.Common package
language: it
lastmod: 2026-10-11
og_description: Esegui OCR su un'immagine in C# usando Aspose.OCR. Questa guida ti
  mostra come installare System.Drawing.Common, caricare un'immagine per l'OCR e estrarre
  il testo da un JPG.
og_image_alt: Screenshot of C# console output displaying recognized text after performing
  OCR on image
og_title: Esegui OCR su un'immagine in C# – guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on image in C# with Aspose.OCR, including
    installing System.Drawing.Common and extracting text from JPG files.
  headline: How to perform OCR on image in C# using Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: Come eseguire OCR su un'immagine in C# usando Aspose.OCR
url: /it/net/text-recognition/how-to-perform-ocr-on-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR su immagine in C# usando Aspose.OCR

Se hai bisogno di **perform OCR on image** file in un'applicazione .NET, questa guida ti mostra una soluzione completa. Usando Aspose.OCR puoi rapidamente **recognize text from picture** file come JPG e visualizzare il risultato in una finestra della console.

Imparerai a:

* **install System.Drawing.Common package** – la libreria che fornisce la classe `Image`,
* **load image for OCR** – legge un JPEG o PNG in memoria,
* configura il modello linguistico,
* **perform OCR on image** e infine,
* **extract text from JPG** e lo stampa.

I passaggi sono scritti per .NET 6+, ma funzionano anche con .NET Framework 4.6.1 o versioni successive.

---

## Prerequisiti

| Requisito | Perché è importante |
|-----------|----------------------|
| .NET 6 SDK (or .NET Framework 4.6.1+) | Fornisce il runtime per l'app console C#. |
| Visual Studio 2022 (or any IDE) | Rende facile aggiungere pacchetti NuGet ed eseguire il programma. |
| Internet connection (first run only) | Aspose.OCR scarica automaticamente il modulo linguistico. |
| A sample image containing Cyrillic or Latin text (e.g., `sample_cyrillic.jpg`) | Utilizzata per dimostrare **extract text from JPG**. |

---

## Passo 1: Installa il pacchetto System.Drawing.Common

Il pacchetto NuGet `System.Drawing.Common` fornisce la classe `Image` che utilizzerai per **load image for OCR**. Apri la Package Manager Console ed esegui:

```powershell
Install-Package System.Drawing.Common
```

> **Suggerimento:** imposta il target su `net6.0-windows` o aggiungi `<UseWindowsForms>true</UseWindowsForms>` al file di progetto se incontri avvisi specifici della piattaforma su Linux/macOS.

---

## Passo 2: Aggiungi il pacchetto NuGet Aspose.OCR

Aspose.OCR contiene il motore OCR e i modelli linguistici. Installalo con:

```powershell
Install-Package Aspose.OCR
```

Il pacchetto è leggero; i dati linguistici richiesti (ad es., Cyrillic) vengono scaricati la prima volta che imposti `OcrEngine.Language`.

---

## Passo 3: Come caricare l'immagine per OCR

Caricare l'immagine è il primo passo concreto prima di poter **perform OCR on image**. Il metodo `Image.FromFile` legge qualsiasi formato supportato da GDI+, inclusi JPG, PNG, BMP e TIFF.

```csharp
using System.Drawing; // Requires System.Drawing.Common

// Replace the path with the location of your test picture.
string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
Image ocrImage = Image.FromFile(imagePath);
```

*Se il file non esiste, viene sollevata `FileNotFoundException` – avvolgi la chiamata in un blocco try/catch per il codice di produzione.*

---

## Passo 4: Configura il motore e **perform OCR on image**

Crea un'istanza di `OcrEngine`, seleziona il modello linguistico, assegna l'immagine caricata e chiama `Recognize()`.

```csharp
using Aspose.OCR;

// Step 4: Initialize OCR engine and set language
var ocrEngine = new OcrEngine
{
    // Choose the language you need; Cyrillic is used in this example.
    Language = OcrLanguage.Cyrillic,
    Image = ocrImage
};

// Execute the OCR operation
OcrResult ocrResult = ocrEngine.Recognize();
```

Il metodo `Recognize()` restituisce un oggetto `OcrResult` che contiene il testo estratto, i punteggi di confidenza e le bounding box. Il modulo linguistico viene scaricato automaticamente al primo utilizzo, quindi non sono necessari file aggiuntivi.

---

## Passo 5: **Extract text from JPG** e visualizzalo

Ora puoi **recognize text from picture** e stampare il risultato. La proprietà `Text` di `OcrResult` contiene la stringa semplice.

```csharp
// Step 5: Output recognized text
Console.WriteLine("Recognized text:");
Console.WriteLine(ocrResult.Text);
```

### Output della console previsto

```
Recognized text:
Пример текста на кириллице
```

Se l'immagine di origine contiene testo in inglese, l'output sarà la frase in inglese che hai inserito nell'immagine.

---

## Casi limite e consigli di best‑practice

| Situazione | Raccomandazione |
|------------|-----------------|
| **Large images ( > 5 MB )** | Ridimensiona l'immagine a ≤ 2000 px sul lato più lungo prima dell'OCR per ridurre l'uso di memoria e migliorare la velocità. |
| **Multiple languages in one picture** | Chiama `ocrEngine.AddLanguage(OcrLanguage.English)` oltre al Cyrillic, quindi imposta `ocrEngine.Language = OcrLanguage.Multilingual`. |
| **Low‑contrast scans** | Aumenta il contrasto con `System.Drawing.Graphics` prima di passare il bitmap al motore. |
| **Running on Linux/macOS** | Assicurati che la dipendenza nativa `libgdiplus` sia installata (`sudo apt-get install -y libgdiplus`). |
| **Repeated OCR calls** | Riutilizza la stessa istanza di `OcrEngine` e sostituisci solo `ocrEngine.Image` per evitare il caricamento ripetuto del modulo. |

---

## Programma completo, eseguibile

Di seguito trovi l'applicazione console completa che incorpora tutti i passaggi precedenti. Copia il codice in un nuovo progetto console C#, sostituisci il percorso dell'immagine ed eseguilo.

```csharp
using System;
using System.Drawing;                 // Install System.Drawing.Common if needed
using Aspose.OCR;                     // NuGet package: Aspose.OCR

class Program
{
    static void Main()
    {
        // Step 1: Install System.Drawing.Common (handled via NuGet)
        // Step 2: Install Aspose.OCR (handled via NuGet)

        // Step 3: Load the image that contains the text to be recognized
        // Replace the placeholder with the actual path to your JPG or PNG file.
        string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
        Image ocrImage;
        try
        {
            ocrImage = Image.FromFile(imagePath);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to load image: {ex.Message}");
            return;
        }

        // Step 4: Create the OCR engine and choose the language model
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Cyrillic, // Change to OcrLanguage.English for Latin scripts
            Image = ocrImage
        };

        // Step 5: Perform OCR on the loaded picture
        OcrResult ocrResult = ocrEngine.Recognize();

        // Step 6: Display the extracted text
        Console.WriteLine("Recognized text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Running the program** stampa la stringa riconosciuta nella console, confermando che hai eseguito con successo **performed OCR on image** e **extracted text from JPG**.

---

## Conclusione

Ora sai come **perform OCR on image** file in C# usando Aspose.OCR, dall'installazione del necessario **System.Drawing.Common package** al **loading image for OCR**, selezionando la lingua appropriata e infine **extracting text from JPG**. Questo esempio end‑to‑end ti fornisce una solida base per costruire pipeline di elaborazione documenti più avanzate, come l'elaborazione batch di cartelle di immagini o l'integrazione dell'OCR in un'API web.

### Cosa c'è dopo?

* Esplora **recognize text from picture** nei PDF convertendo prima ogni pagina in un'immagine.
* Sperimenta con le proprietà `Resolution`, `Threshold` e `MaxProcessingTime` di `OcrEngine` per affinare la precisione su scansioni rumorose.
* Combina l'output OCR con una libreria di elaborazione del linguaggio naturale per categorizzare automaticamente il contenuto estratto.

Sentiti libero di adattare il codice ad altri formati di immagine, aggiungere gestione degli errori o integrarlo in applicazioni più grandi. Buon coding!

## Cosa dovresti imparare dopo?

I seguenti tutorial trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Estrai testo da immagine in C# – Guida completa Aspose OCR](/ocr/english/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/)
- [Estrai testo da immagine C# con selezione della lingua usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Come eseguire l'estrazione di testo da immagine da stream usando Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}