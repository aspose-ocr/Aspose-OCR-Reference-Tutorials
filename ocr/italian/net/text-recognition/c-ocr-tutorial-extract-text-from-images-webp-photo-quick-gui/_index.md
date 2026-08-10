---
category: general
date: 2026-03-17
description: Tutorial OCR in C# – scopri come estrarre testo da file immagine, leggere
  il testo da foto WebP e convertire l’immagine in testo usando un semplice OcrEngine.
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- read text from webp
- recognize text from photo
- convert image to text
language: it
og_description: Il tutorial C# OCR ti mostra come estrarre testo da file immagine,
  leggere testo da foto WebP e convertire un'immagine in testo con poche righe di
  codice.
og_title: c# tutorial OCR – Estrai il testo dalle immagini in pochi minuti
tags:
- C#
- OCR
- Image Processing
title: 'c# tutorial OCR: estrarre testo da immagini (WebP, foto) – Guida rapida'
url: /it/net/text-recognition/c-ocr-tutorial-extract-text-from-images-webp-photo-quick-gui/
---

inside fences. That's fine.

Make sure we preserve bullet list formatting.

Now produce final output with all content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR tutorial – Estrai testo dalle immagini (WebP, foto)

Hai mai avuto bisogno di **estrarre testo da immagini** ma non sapevi da dove cominciare in C#? Forse hai uno screenshot WebP, un JPEG di una ricevuta, o una pagina PDF scannerizzata e vuoi semplicemente le parole al suo interno. In questo **c# OCR tutorial** ti guideremo attraverso un esempio completo, pronto‑da‑eseguire, che legge il testo da una foto, gestisce WebP e altri formati moderni, e converte l'immagine in testo semplice—tutto in poche righe.

**Qual è il vantaggio?** Potrai trasformare qualsiasi immagine di testo in stringhe ricercabili, inserirle nei database o passarle a pipeline AI successive. Nessuna magia, solo un solido motore OCR, alcune API .NET e spiegazioni chiare del “perché” dietro ogni passaggio.

## Cosa ti serve

- **.NET 6 SDK** (o successivo). Il codice qui sotto si compila con .NET 6+ e funziona su Windows, Linux o macOS.
- **Visual Studio 2022** o qualsiasi editor tu preferisca (VS Code va bene).
- Il pacchetto NuGet **`Microsoft.Windows.SDK.Contracts`** (fornisce `Windows.Media.Ocr`). Installa con:

```bash
dotnet add package Microsoft.Windows.SDK.Contracts
```

- Un file immagine che vuoi elaborare – per questo tutorial useremo una foto **WebP** chiamata `photo.webp` collocata in una cartella chiamata `YOUR_DIRECTORY`.

> Consiglio professionale: Se sei su una piattaforma non‑Windows, puoi sostituire `OcrEngine` con una libreria cross‑platform come **Tesseract**. Il codice circostante rimane praticamente lo stesso.

## Passo 1: Configura un progetto C# OCR Tutorial

Per prima cosa, crea una nuova app console. Apri un terminale ed esegui:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Aggiungi il pacchetto richiesto (come mostrato sopra) e apri il progetto nel tuo IDE. Questa struttura ci fornisce una base pulita per il **c# OCR tutorial**.

## Passo 2: Importa i namespace e prepara l'immagine

Abbiamo bisogno di alcune direttive `using` affinché il compilatore sappia dove trovare `OcrEngine`, `SoftwareBitmap` e gli helper per il caricamento delle immagini.

```csharp
using System;
using System.IO;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;
```

> **Perché questi namespace?**  
> `Windows.Media.Ocr` contiene la classe `OcrEngine` che esegue effettivamente il riconoscimento. `Windows.Graphics.Imaging` ci permette di decodificare l'immagine (incluso WebP) in un `SoftwareBitmap` che il motore può comprendere. Gli helper `System.IO` e `Windows.Storage.Streams` rendono il caricamento dei file indolore.

Ora, carica l'immagine. Il decoder integrato può gestire WebP, HEIF, PNG, JPEG e altro, così puoi **leggere testo da WebP** senza plugin aggiuntivi.

```csharp
// Step 2: Load the image file into a SoftwareBitmap
string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

// Open the file as a random access stream
using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
{
    // Decode the image (auto-detects format)
    BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
    SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();
    
    // Optional: Convert to grayscale for better OCR accuracy
    SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);
    
    // Pass the bitmap to the next step
    await RecognizeTextAsync(grayBitmap);
}
```

> **Caso limite:** Se la tua immagine è già in bianco‑e‑nero, puoi saltare il passaggio di conversione. La conversione in scala di grigi è un piccolo guadagno di prestazioni e spesso migliora il riconoscimento su foto rumorose.

## Passo 3: Esegui il motore OCR – Riconosci il testo dalla foto

Ecco il cuore del **c# OCR tutorial**. Creiamo un'istanza di `OcrEngine`, le forniamo il bitmap e estraiamo il testo riconosciuto.

```csharp
static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
{
    // Step 3: Create the OCR engine instance – it automatically picks the best language
    OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

    if (ocrEngine == null)
    {
        Console.WriteLine("❌ No OCR engine available for the current language.");
        return;
    }

    // Perform recognition
    OcrResult ocrResult = await ocrEngine.RecognizeAsync(bitmap);

    // Step 4: Display the extracted text – this is the “convert image to text” part
    Console.WriteLine("📝 Recognized text:");
    Console.WriteLine(ocrResult.Text);
}
```

**Cosa sta succedendo?**  
- `TryCreateFromUserProfileLanguages()` seleziona le lingue impostate nel profilo utente di Windows, che di solito coprono Inglese, Spagnolo, ecc. Se ti serve una lingua specifica, usa `OcrEngine.TryCreateFromLanguage(new Language("fr-FR"))`.  
- `RecognizeAsync` esegue il lavoro pesante su un thread in background, restituendo un `OcrResult` che contiene la stringa grezza, i riquadri delle parole e i punteggi di confidenza.  
- Infine, stampiamo `ocrResult.Text`, fornendoti il risultato **convert image to text** che puoi inviare altrove.

## Passo 4: Esempio completo e eseguibile

Mettendo tutto insieme, ecco un programma autonomo che puoi copiare‑incollare in `Program.cs`. Si compila, si esegue e stampa il testo estratto da `photo.webp`.

```csharp
// Program.cs – Complete c# OCR tutorial example
using System;
using System.IO;
using System.Threading.Tasks;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;

class Program
{
    static async Task Main(string[] args)
    {
        // Replace with your actual directory and file name
        string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"❗ Image not found: {imagePath}");
            return;
        }

        // Load and optionally preprocess the image
        using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
        {
            BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
            SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();

            // Convert to grayscale – improves OCR accuracy on many photos
            SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);

            // Run OCR
            await RecognizeTextAsync(grayBitmap);
        }
    }

    static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
    {
        // Create OCR engine (auto‑detect language)
        OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

        if (ocrEngine == null)
        {
            Console.WriteLine("❌ Unable to create OCR engine. Ensure language packs are installed.");
            return;
        }

        // Perform recognition
        OcrResult result = await ocrEngine.RecognizeAsync(bitmap);

        // Output the extracted text
        Console.WriteLine("\n--- OCR Output ---");
        Console.WriteLine(result.Text);
        Console.WriteLine("--- End of Output ---\n");
    }
}
```

### Output previsto

Se `photo.webp` contiene la frase “Hello, world! This is a test.” vedrai qualcosa del genere:

```
--- OCR Output ---
Hello, world!
This is a test.
--- End of Output ---
```

Le interruzioni di riga esatte dipendono dal layout dell'immagine di origine, ma il risultato **extract text from image** sarà sempre una stringa semplice che puoi manipolare ulteriormente.

## Domande comuni e casi limite

### Funziona con altri formati immagine?

Assolutamente. Il decoder usato (`BitmapDecoder`) rileva automaticamente JPEG, PNG, BMP, GIF, **WebP**, HEIF e altro. Quindi puoi **read text from WebP**, JPEG o anche un TIFF senza modificare il codice.

### Cosa succede se il motore OCR restituisce bassa confidenza?

Puoi ispezionare `ocrResult.Lines` e ogni `OcrWord` per un `ConfidenceScore`. Se il punteggio è sotto una soglia (es., 0.6), considera:

- Pre‑processare l'immagine (aumentare contrasto, nitidezza, raddrizzare).  
- Usare un'immagine sorgente a risoluzione più alta.  
- Passare a una libreria dedicata come **Tesseract** per supporto multilingue.

### Come gestire più lingue nella stessa immagine?

Crea istanze separate di `OcrEngine` per ogni lingua e eseguile sequenzialmente, oppure usa una libreria che supporta il rilevamento di lingue miste. Per il motore integrato, puoi passare un oggetto `Language`:

```csharp
var spanishEngine = OcrEngine.TryCreateFromLanguage(new Language("es-ES"));
```

### Posso eseguirlo su Linux/macOS?

L'API `Windows.Media.Ocr` è disponibile solo su Windows. Su piattaforme non‑Windows, sostituisci la sezione OCR con **Tesseract** (via `Tesseract.Net.SDK`). Il codice di caricamento e pre‑elaborazione rimane identico, quindi il resto di questo **c# OCR tutorial** è ancora valido.

## Consigli professionali per una migliore precisione

- **Ridimensiona** le immagini grandi a un massimo di 2000 px sul lato più lungo – i motori OCR funzionano più velocemente su dimensioni moderate.  
- **Denoise** usando una semplice sfocatura gaussiana se la foto è granulosa.  
- **Deskew** il bitmap se il testo non è perfettamente orizzontale; `SoftwareBitmap` può essere ruotato prima di passarlo a `OcrEngine`.  
- **Cache** l'istanza `OcrEngine` se stai elaborando molte immagini in batch; crearla ripetutamente aggiunge overhead.

## Argomenti correlati da esplorare

- **Convert image to text** using **Tesseract** for cross‑platform projects.  
- **Extract text from PDF** by rendering each page to an image first.  
- **Batch OCR**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}