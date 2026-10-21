---
category: general
date: 2026-10-21
description: Scopri come eseguire l'OCR su un JPG, estrarre il testo dall'immagine
  e caricare l'immagine per l'OCR usando Aspose.OCR in C#. Guida completa passo‑passo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- recognize text from jpg
- load image for OCR
- perform OCR on image
language: it
lastmod: 2026-10-21
og_description: Come eseguire l'OCR su un'immagine in C# con Aspose.OCR. Segui questa
  guida per caricare l'immagine per l'OCR, riconoscere il testo da un JPG ed estrarre
  il testo dall'immagine.
og_image_alt: Screenshot showing how to perform OCR on a Cyrillic image in C#
og_title: Come eseguire l'OCR su un'immagine in C# – guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-10-21'
  description: Learn how to perform OCR on a JPG, extract text from image and load
    image for OCR using Aspose.OCR in C#. Complete step‑by‑step guide.
  headline: How to perform OCR on an image in C# with Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose.OCR
- Image processing
- Text extraction
title: Come eseguire l'OCR su un'immagine in C# con Aspose.OCR
url: /it/net/text-recognition/how-to-perform-ocr-on-an-image-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR su un'immagine in C# con Aspose.OCR

Se hai bisogno di **how to perform OCR** su un'immagine, questo tutorial ti mostra una soluzione completa, pronta all'uso. Imparerai come caricare un'immagine per OCR, riconoscere il testo da file JPG e estrarre il testo dall'immagine usando la libreria Aspose.OCR.

La guida copre tutto, dall'installazione del pacchetto NuGet alla gestione dei modelli linguistici e alla stampa del risultato riconosciuto. Alla fine sarai in grado di integrare OCR in qualsiasi progetto .NET e di elaborare testi in cirillico o altre lingue senza uscire dall'IDE.

## Cosa ti servirà

- .NET 6.0 o versioni successive (il codice funziona anche su .NET Framework 4.7+)
- Visual Studio 2022 (o qualsiasi editor C#)
- Accesso a Internet per la prima esecuzione (Aspose.OCR scarica automaticamente il modello linguistico)
- Un'immagine di esempio, ad es. `cyrillic_sample.jpg`, posizionata in una cartella a cui puoi fare riferimento dal codice

## Passo 1: Installa Aspose.OCR

Apri il NuGet Package Manager e aggiungi **Aspose.OCR** al tuo progetto:

```bash
dotnet add package Aspose.OCR
```

Il pacchetto contiene il motore OCR, i modelli linguistici e le classi di supporto necessarie per l'elaborazione delle immagini. Non sono richieste DLL aggiuntive.

## Passo 2: Crea il motore OCR – how to perform OCR

Il primo vero compito in **how to perform OCR** è istanziare il motore. Questo oggetto gestisce l'intera pipeline di riconoscimento.

```csharp
using Aspose.OCR;

// Create an OCR engine instance
OcrEngine engine = new OcrEngine();
```

`OcrEngine` è leggero; puoi riutilizzare la stessa istanza per più immagini, il che migliora le prestazioni durante l'elaborazione di batch.

## Passo 3: Carica l'immagine per OCR

Prima del riconoscimento devi fornire i dati dell'immagine. Il passo **load image for OCR** accetta molti formati, ma questo esempio si concentra su un file JPEG.

```csharp
// Load the image you want to process
engine.Image = OcrImage.FromFile(@"C:\Images\cyrillic_sample.jpg");
```

`OcrImage.FromFile` legge il file in memoria e lo prepara per il motore. Se il percorso del file è non valido, viene sollevata un'`ArgumentException`, quindi assicurati che il percorso sia corretto.

## Passo 4: Seleziona la lingua appropriata (opzionale ma consigliato)

Se la tua immagine contiene caratteri cirillici, imposta la lingua su `Cyrillic`. Il modello richiesto viene scaricato automaticamente al primo avvio.

```csharp
// Choose the language model
engine.Language = OcrLanguage.Cyrillic;
```

Puoi passare ad altre lingue (ad es., `OcrLanguage.English`) modificando questa proprietà. La libreria supporta oltre 60 lingue.

## Passo 5: Riconosci il testo da JPG – how to perform OCR on a JPEG

Ora chiama il metodo `Recognize`. Questo è il nucleo di **how to perform OCR** e traduce la bitmap in testo Unicode.

```csharp
// Perform the recognition
engine.Recognize();
```

Il metodo blocca l'esecuzione finché il processo OCR non termina. Per immagini di grandi dimensioni potresti voler eseguire questo su un thread in background per mantenere l'interfaccia utente reattiva.

## Passo 6: Estrai il testo dall'immagine

Dopo il riconoscimento, il motore memorizza il risultato nella proprietà `Text`. Questo completa il passo **extract text from image**.

```csharp
// Retrieve the extracted text
string extractedText = engine.Text;

// Output the recognized text to the console
Console.WriteLine(extractedText);
```

L'output conterrà i caratteri esatti trovati nell'immagine, preservando le interruzioni di riga e la punteggiatura.

## Esempio completo, eseguibile

Unendo tutti i passaggi ottieni un unico programma che puoi copiare, incollare ed eseguire:

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 1: Create the OCR engine
        OcrEngine engine = new OcrEngine();

        // Step 2: Load the image for OCR
        engine.Image = OcrImage.FromFile(@"C:\Images\cyrillic_sample.jpg");

        // Step 3: Choose the language model (Cyrillic in this case)
        engine.Language = OcrLanguage.Cyrillic;

        // Step 4: Perform OCR on the image
        engine.Recognize();

        // Step 5: Extract text from image
        string extractedText = engine.Text;

        // Step 6: Output the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(extractedText);
    }
}
```

### Output previsto

Se `cyrillic_sample.jpg` contiene la frase “Привет мир” (Hello world), la console visualizzerà:

```
=== OCR Result ===
Привет мир
```

Font diversi o la qualità dell'immagine possono influire sulla precisione, ma Aspose.OCR generalmente raggiunge un riconoscimento >95 % su stampe nitide.

## Problemi comuni e consigli pratici

- **La qualità dell'immagine è importante** – JPEG a bassa risoluzione o rumorosi riducono la precisione. Pre‑elabora l'immagine (ad es., aumenta il contrasto) usando `engine.Image.AdjustContrast()` se necessario.
- **Download del modello linguistico** – la prima esecuzione scarica il modello in `%USERPROFILE%\.Aspose\OCR`. Assicurati che il processo abbia i permessi di scrittura.
- **Elaborazione batch** – riutilizza la stessa istanza di `OcrEngine` e cambia solo `engine.Image` tra i file. Questo evita il caricamento ripetuto del modello.
- **Utilizzo della memoria** – immagini grandi consumano più RAM. Chiama `engine.Image.Dispose()` dopo ogni riconoscimento se elabori molti file in un ciclo.
- **Sicurezza dei thread** – `OcrEngine` non è thread‑safe. Crea un'istanza separata per thread quando parallelizzi.

## Conclusione

Ora sai **how to perform OCR** su un JPEG, **load image for OCR** e **extract text from image** usando Aspose.OCR in C#. La soluzione completa dimostra come impostare la lingua, riconoscere il testo da JPG e stampare il risultato, fornendoti una solida base per qualsiasi progetto di estrazione del testo.

Successivamente, esplora argomenti correlati come **perform OCR on image** batch, l'integrazione di OCR con le API ASP.NET Core, o la conversione del testo estratto in PDF ricercabili. Sperimenta con lingue diverse e la pre‑elaborazione delle immagini per massimizzare la qualità del riconoscimento.

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Perform OCR in C# – Convert Image to Text with Aspose OCR](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-convert-image-to-text-with-aspose-oc/)
- [How to Perform OCR in C# – Recognize Text from Image](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-recognize-text-from-image/)
- [How to extract text from image using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}