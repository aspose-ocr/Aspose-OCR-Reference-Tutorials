---
category: general
date: 2026-02-20
description: Tutorial OCR in C# che mostra come estrarre testo da un'immagine, riconoscere
  il testo da un PNG e convertire l'immagine in testo in poche righe di codice.
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- recognize text from png
- convert image to text
- how to extract text
language: it
og_description: Tutorial OCR in C# che ti guida nell'estrazione del testo da file
  immagine, nel riconoscimento del testo da PNG e nella conversione delle immagini
  in testo usando Aspose.OCR.
og_title: c# tutorial OCR – Guida rapida per estrarre testo dalle immagini
tags:
- OCR
- C#
- Aspose
title: c# tutorial OCR – Estrai il testo dalle immagini con Aspose.OCR
url: /it/net/text-recognition/c-ocr-tutorial-extract-text-from-images-with-aspose-ocr/
---

/products/products-backtop-button >}}

All unchanged.

Now produce final content with translations. Ensure no extra explanation.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Estrarre testo dalle immagini con Aspose.OCR

Hai mai avuto bisogno di un **c# ocr tutorial** che funzioni davvero su un file PNG reale? Non sei l'unico. In molti progetti—pensa alla scansione di fatture, all'archiviazione di ricevute o al semplice parsing di screenshot—gli sviluppatori si trovano di fronte a un ostacolo quando cercano di **estrarre testo da un'immagine** senza una libreria affidabile.  

La buona notizia è che Aspose.OCR rende l'intero processo un gioco da ragazzi. In questa guida percorreremo un esempio completo e eseguibile che mostra **come estrarre testo** da un PNG, spiega *perché* ogni riga è importante e tocca anche casi particolari come licenze e pre‑elaborazione delle immagini. Alla fine sarai in grado di **riconoscere testo da file png** e **convertire immagine in testo** con solo poche istruzioni C#.

## Cosa copre questo tutorial

- Configurare il motore Aspose.OCR in un'app console .NET.  
- Caricare un PNG (o qualsiasi bitmap supportata) dal disco.  
- Eseguire l'OCR e stampare il risultato sulla console.  
- Licenza opzionale, gestione degli errori e consigli sulle prestazioni.  

Nessun servizio esterno, nessuna magia nascosta—solo puro codice C# che puoi copiare‑incollare ed eseguire. Se ti sei mai chiesto **come estrarre testo** da un documento scansionato, resta con noi; risponderemo a questa domanda e a qualche “cosa succede se” lungo il percorso.

## Prerequisiti

- .NET 6.0 SDK o versioni successive (il codice funziona anche su .NET Framework 4.7+).  
- Visual Studio 2022 (o qualsiasi editor tu preferisca).  
- Un pacchetto NuGet Aspose.OCR per .NET gratuito o a pagamento.  
- Un file immagine chiamato `sample.png` collocato in una cartella a cui puoi fare riferimento.  

Questo è tutto—non sono necessari altri strumenti di terze parti.

## c# OCR Tutorial: Configurare Aspose.OCR

Prima di tutto: hai bisogno della libreria Aspose.OCR. Apri il terminale nella cartella del progetto ed esegui:

```bash
dotnet add package Aspose.OCR
```

Questo scarica l'ultima versione stabile e aggiunge i riferimenti DLL necessari. Se possiedi un file di licenza (`Aspose.OCR.lic`), tienilo a portata di mano; altrimenti la versione di prova gratuita funzionerà, ma con filigrane sul risultato OCR.

### Perché una licenza è importante

Senza licenza il motore funziona in modalità di valutazione, inserendo una riga “Powered by Aspose” nell'output per alcune lingue. Per il codice di produzione dovrai chiamare `SetLicense` subito, come mostrato nel codice qui sotto. È una chiamata a una sola riga, ma rimuove la filigrana e sblocca l'elaborazione a piena velocità.

## Estrarre testo da un'immagine usando Aspose.OCR

Ora immergiamoci nel codice OCR reale. Di seguito trovi un programma **completo e autonomo** che puoi compilare ed eseguire immediatamente.

```csharp
using System;
using System.Drawing;          // Needed for Image class
using Aspose.OCR;               // Core OCR namespace
using Aspose.OCR.Models;       // For OCR settings (optional)

class LicenseCheck
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize the OCR engine
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // Step 2 (Optional): Apply your Aspose.OCR license
        // -------------------------------------------------
        // Uncomment and set the correct path if you have a license file.
        // ocrEngine.SetLicense(@"C:\MyLicenses\Aspose.OCR.lic");

        // -------------------------------------------------
        // Step 3: Load the image you want to process
        // -------------------------------------------------
        // You can use any supported format (png, jpg, bmp, tiff, etc.)
        string imagePath = @"C:\Images\sample.png";
        Image inputImage = Image.FromFile(imagePath);

        // -------------------------------------------------
        // Step 4: Recognize text from the loaded image
        // -------------------------------------------------
        // The Recognize method returns a plain string.
        string recognizedText = ocrEngine.Recognize(inputImage);

        // -------------------------------------------------
        // Step 5: Display the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

**Cosa sta succedendo?**  

1. **Engine creation** – `OcrEngine` è il punto di ingresso principale; carica internamente i dati della lingua.  
2. **License loading** – opzionale ma consigliata; basta indicare il tuo file `.lic`.  
3. **Image loading** – `Image.FromFile` funziona per qualsiasi formato bitmap; usiamo un PNG perché conserva la qualità lossless, fondamentale per l'accuratezza dell'OCR.  
4. **Recognition** – `ocrEngine.Recognize` esegue tutto il lavoro pesante, restituendo una stringa con i caratteri rilevati.  
5. **Output** – scriviamo il risultato sulla console, ma potresti facilmente inviarlo a un file, a un database o a un controllo UI.

### Output previsto

Se `sample.png` contiene il testo “Hello World”, la console mostrerà:

```
=== OCR Result ===
Hello World
```

Se l'immagine è sfocata o contiene caratteri non latini, l'output potrebbe includere simboli illeggibili. È qui che entra in gioco la pre‑elaborazione (regolazione del contrasto, binarizzazione) — trattata nella sezione successiva.

## Riconoscere testo da file PNG – Consigli e trucchi

PNG è un formato popolare perché memorizza i pixel senza artefatti di compressione. Tuttavia, non tutti i PNG sono uguali. Ecco alcuni consigli pratici che potrebbero esserti utili:

- **La risoluzione è importante** – Punta a almeno 300 dpi. Qualsiasi valore inferiore può causare caratteri mancanti.  
- **Colore vs. scala di grigi** – Convertire un PNG a colori in scala di grigi prima dell'OCR può migliorare la velocità senza compromettere l'accuratezza.  
- **Rimozione del rumore** – Piccole macchie spesso confondono il motore; un semplice filtro mediano può aiutare.

Di seguito trovi un breve snippet che mostra come pre‑elaborare un'immagine prima di passarla a Aspose.OCR:

```csharp
using System.Drawing.Imaging;

// Convert to grayscale
Bitmap grayBitmap = new Bitmap(inputImage.Width, inputImage.Height);
using (Graphics g = Graphics.FromImage(grayBitmap))
{
    var colorMatrix = new ColorMatrix(
        new float[][]{
            new float[]{0.3f,0.3f,0.3f,0,0},
            new float[]{0.59f,0.59f,0.59f,0,0},
            new float[]{0.11f,0.11f,0.11f,0,0},
            new float[]{0,0,0,1,0},
            new float[]{0,0,0,0,1}});
    var attributes = new ImageAttributes();
    attributes.SetColorMatrix(colorMatrix);
    g.DrawImage(inputImage, new Rectangle(0,0,grayBitmap.Width,grayBitmap.Height),
                0,0,inputImage.Width,inputImage.Height, GraphicsUnit.Pixel, attributes);
}

// Optional: Apply a simple binary threshold
Bitmap binBitmap = new Bitmap(grayBitmap.Width, grayBitmap.Height);
for (int y = 0; y < grayBitmap.Height; y++)
{
    for (int x = 0; x < grayBitmap.Width; x++)
    {
        Color pixel = grayBitmap.GetPixel(x, y);
        int bw = pixel.R < 128 ? 0 : 255; // threshold at 128
        binBitmap.SetPixel(x, y, Color.FromArgb(bw, bw, bw));
    }
}

// Now run OCR on the cleaned bitmap
string cleanedText = ocrEngine.Recognize(binBitmap);
Console.WriteLine(cleanedText);
```

**Consiglio professionale:** Se elabori decine di immagini, istanzia un unico `OcrEngine` e riutilizzalo. Creare un nuovo motore per ogni immagine aggiunge overhead non necessario.

## Convertire immagine in testo – Opzioni avanzate

Aspose.OCR non si limita all'estrazione di testo semplice. Puoi chiedere di restituire **dati strutturati** (come i riquadri di delimitazione delle parole) o impostare **suggerimenti di lingua** per migliorare l'accuratezza su documenti multilingue.

```csharp
// Set language to English + Spanish (ISO codes)
ocrEngine.Language = Language.English | Language.Spanish;

// Request detailed OCR result
OcrResult result = ocrEngine.RecognizeImage(inputImage, OcrOptions.DetectTextBlocks);

// Iterate over detected words
foreach (var word in result.Words)
{
    Console.WriteLine($"{word.Text} (x:{word.Bounds.X}, y:{word.Bounds.Y})");
}
```

L'oggetto `OcrResult` fornisce le coordinate di ogni parola, utile per evidenziare il testo in un'interfaccia UI o per il post‑processing (ad esempio, per oscurare informazioni sensibili).

## Come estrarre testo in scenari reali

Affrontiamo alcune domande “cosa succede se” che spesso emergono negli ambienti di produzione.

### E se l'immagine è una pagina PDF?

Aspose.OCR può leggere i PDF direttamente, ma avrai bisogno della libreria Aspose.PDF per rasterizzare ogni pagina in un'immagine prima. Il flusso di lavoro è:

1. Carica il PDF con `Aspose.Pdf.Document`.  
2. Converti una pagina in bitmap (`PdfConverter`).  
3. Passa la bitmap a `OcrEngine.Recognize`.

### E se il risultato OCR contiene caratteri spazzatura?

Le cause tipiche sono bassa risoluzione, rumore eccessivo o font non supportati. Prova a:

- **Upscaling** dell'immagine (ridimensionamento `Bitmap`).  
- Applicare un filtro di nitidezza.  
- Specificare la lingua corretta (come mostrato sopra).

### E se devo elaborare immagini in parallelo?

Poiché `OcrEngine` non è thread‑safe, crea un'**istanza separata per thread** o utilizza un pool thread‑local. Esempio con `Parallel.ForEach`:

```csharp
Parallel.ForEach(imagePaths, path =>
{
    var engine = new OcrEngine(); // each thread gets its own engine
    var img = Image.FromFile(path);
    string text = engine.Recognize(img);
    // Store or log 'text' as needed
});
```

## Esempio completo funzionante

Mettendo tutto insieme, ecco una versione compatta che puoi inserire in un nuovo progetto console:

```csharp
using System;
using System.Drawing;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Initialize OCR engine (single instance for this demo)
        OcrEngine engine = new OcrEngine();

        // Uncomment if you have a license file
        // engine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

        // Path to the PNG you want to read
        string file = @"C:\Images\sample.png";

        // Load, optionally preprocess, then recognize
        using (Image img = Image.FromFile(file))
        {
            string text = engine.Recognize(img);
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(text);
        }
    }
}
```

Compila con `dotnet run` e osserva la console stampare il testo estratto. Semplice, vero? Questa è la bellezza di un ben‑des

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}