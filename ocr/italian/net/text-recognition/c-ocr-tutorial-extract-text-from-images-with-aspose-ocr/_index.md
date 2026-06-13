---
category: general
date: 2026-03-21
description: 'Tutorial OCR in C#: Impara come estrarre testo da un''immagine, scansionare
  fatture e caricare immagini in C# usando Aspose OCR con accelerazione GPU.'
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- ocr invoice scanning
- how to ocr image
- load image in c#
language: it
og_description: 'c# OCR tutorial: Guida passo‑passo per estrarre testo da un''immagine,
  eseguire la scansione OCR di fatture e imparare come fare OCR su un''immagine in
  C# usando l''accelerazione GPU.'
og_title: Tutorial OCR in C# – Estrai il testo dalle immagini con Aspose OCR
tags:
- OCR
- C#
- Image Processing
title: c# tutorial OCR – Estrai il testo dalle immagini con Aspose OCR
url: /it/net/text-recognition/c-ocr-tutorial-extract-text-from-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR tutorial – Estrai testo dalle immagini con Aspose OCR

Ti sei mai chiesto come fare un **c# OCR tutorial** su un problema reale come trasformare una fattura scannerizzata in testo modificabile? Non sei solo. Molti sviluppatori si trovano in difficoltà quando devono *estrarre testo da immagine* file e finiscono per scrivere parser fragili che si rompono al primo scan rumoroso.

Ecco la questione—Aspose.OCR rende l'intero processo un gioco da ragazzi, soprattutto quando abiliti l'accelerazione GPU. In questa guida vedrai esattamente **come fare ocr su immagine** file in C#, caricare immagini in c# correttamente, e gestire anche le stranezze comuni della scansione delle fatture senza impazzire.

Alla fine di questo tutorial avrai un'app console eseguibile che legge una fattura TIFF, esegue OCR sulla GPU e stampa un output di testo semplice e pulito. Nessuna magia, solo codice solido che puoi copiare‑incollare e adattare.

---

## Cosa ti serve

- **.NET 6.0** (o versioni successive) – l'attuale versione LTS, così sarai a prova di futuro.
- **Aspose.OCR for .NET** pacchetto NuGet – versione 23.10 (l'ultima al momento della stesura).
- Una **macchina con GPU abilitata** (opzionale ma consigliata) – il codice ricade su CPU se non viene trovata una GPU compatibile.
- Un'immagine di esempio, ad es. `large_invoice.tif`. Qualsiasi formato supportato (PNG, JPEG, TIFF, PDF) funziona.

Se non hai ancora installato il pacchetto NuGet, esegui:

```bash
dotnet add package Aspose.OCR
```

Ora che abbiamo coperto i prerequisiti, immergiamoci nei passaggi effettivi.

---

## Passo 1: Crea un nuovo progetto console e aggiungi Aspose.OCR

Per prima cosa, avvia una nuova app console così possiamo mantenere il tutorial autonomo.

```bash
dotnet new console -n OcrInvoiceDemo
cd OcrInvoiceDemo
dotnet add package Aspose.OCR
```

> **Consiglio professionale:** Usa il flag `-n` per dare al tuo progetto un nome significativo; mantiene la soluzione ordinata quando inizi ad aggiungere altri moduli in seguito.

Il file `Program.cs` che Visual Studio crea sarà il nostro campo di gioco. Aprilo e rimuovi la riga predefinita `Console.WriteLine` – la sostituiremo con la logica OCR.

## Passo 2: Carica immagine in C# – Il modo corretto

Caricare un'immagine può sembrare banale, ma farlo in modo errato può causare perdite di memoria o bloccare il file. La classe `System.Drawing.Image` funziona bene nella maggior parte degli scenari, tuttavia devi avvolgerla in un blocco `using` per garantirne lo smaltimento.

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrInvoiceDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 👉 Step 2: Load the image you want to OCR.
            // Replace the path with the actual location of your invoice file.
            const string imagePath = @"C:\Invoices\large_invoice.tif";

            // The using statement ensures the image gets disposed automatically.
            using var inputImage = Image.FromFile(imagePath);
            
            // Continue to the OCR engine setup…
        }
    }
}
```

Nota il commento `// 👉 Step 2:` – rispecchia la numerazione dei passaggi nel nostro tutorial e aiuta chiunque esamini il codice in seguito.

## Passo 3: Inizializza il motore OCR con accelerazione GPU

Aspose.OCR ti permette di scegliere la modalità di elaborazione al momento della costruzione. `OcrEngineMode.Gpu` indica alla libreria di usare la scheda grafica se ne rileva una; altrimenti ricade silenziosamente su CPU, così non devi scrivere logica di fallback aggiuntiva.

```csharp
// 👉 Step 3: Create the OCR engine.
// The constructor argument selects GPU mode; it's the fastest option for large invoices.
var ocrEngine = new OcrEngine(OcrEngineMode.Gpu);
```

> **Perché GPU?**  
> L'OCR su fatture ad alta risoluzione può essere intensivo per la CPU. Spostare il carico sulla GPU riduce il tempo di esecuzione da diversi secondi a una frazione, specialmente quando elabori lotti.

## Passo 4: Esegui OCR ed estrai testo dall'immagine

Ora avviene la magia. Chiama `Recognize` e ottieni il testo semplice. Aspose restituisce un oggetto `OcrResult` che contiene il testo grezzo, i punteggi di confidenza e persino le bounding box per carattere se ti servono in seguito.

```csharp
// 👉 Step 4: Perform the OCR operation.
OcrResult ocrResult = ocrEngine.Recognize(inputImage);

// Display the extracted text.
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

Quando esegui il programma, dovresti vedere qualcosa del genere:

```
=== OCR Output ===
Invoice #12345
Date: 03/15/2026
Total: $1,234.56
...
```

Se l'output appare confuso, verifica che l'immagine abbia alto contrasto e che la lingua OCR sia impostata correttamente (l'inglese è predefinito). Puoi anche modificare `ocrEngine.Settings` per una maggiore precisione, ma le impostazioni predefinite funzionano bene per la maggior parte delle fatture stampate.

## Passo 5: Gestire i casi limite della scansione OCR delle fatture

Le fatture hanno molte forme—alcune sono multi‑pagina, altre hanno tabelle o note scritte a mano. Ecco alcuni rapidi aggiustamenti che puoi fare senza riscrivere l'intera pipeline.

### 5.1 PDF o TIFF multi‑pagina

Se il tuo file di origine contiene più pagine, dovrai iterare su ciascuna pagina e concatenare i risultati.

```csharp
using var multiPageImage = Image.FromFile(@"C:\Invoices\multi_page_invoice.tif");

// Aspose can split multi‑page TIFFs into separate images.
for (int i = 0; i < multiPageImage.GetFrameCount(FrameDimension.Page); i++)
{
    multiPageImage.SelectActiveFrame(FrameDimension.Page, i);
    using var page = (Image)multiPageImage.Clone();
    var pageResult = ocrEngine.Recognize(page);
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(pageResult.Text);
}
```

### 5.2 Scansioni a bassa risoluzione

Se i DPI sono inferiori a 150, ingrandisci l'immagine prima di inviarla al motore. Questo migliora notevolmente il riconoscimento dei caratteri.

```csharp
// Simple nearest‑neighbor scaling – replace with a better algorithm if needed.
var highRes = new Bitmap(inputImage, new Size(inputImage.Width * 2, inputImage.Height * 2));
var highResResult = ocrEngine.Recognize(highRes);
Console.WriteLine(highResResult.Text);
```

### 5.3 Pacchetti linguistici personalizzati

Per impostazione predefinita Aspose utilizza l'inglese. Per altre lingue, scarica il pacchetto linguistico appropriato dal sito di Aspose e registralo:

```csharp
ocrEngine.Settings.Language = OcrLanguage.Spanish; // example for Spanish invoices
```

Queste modifiche rendono la tua soluzione **ocr invoice scanning** abbastanza robusta per carichi di lavoro in produzione.

## Esempio completo funzionante

Di seguito trovi il programma completo, pronto‑all'uso, che incorpora tutti i passaggi sopra. Copialo in `Program.cs`, regola il percorso del file e premi **F5**.

```csharp
// ---------------------------------------------------------------
// Complete c# OCR tutorial – Aspose OCR with GPU acceleration
// ---------------------------------------------------------------
using System;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrInvoiceDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Initialize the OCR engine (GPU mode)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine(OcrEngineMode.Gpu);

            // -----------------------------------------------------------------
            // Step 2: Load the image you want to process
            // -----------------------------------------------------------------
            const string imagePath = @"C:\Invoices\large_invoice.tif";

            // Using ensures the image is disposed properly.
            using var inputImage = Image.FromFile(imagePath);

            // -----------------------------------------------------------------
            // Step 3: Run OCR and extract plain text
            // -----------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(inputImage);

            // -----------------------------------------------------------------
            // Step 4: Output the result
            // -----------------------------------------------------------------
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);

            // -----------------------------------------------------------------
            // Optional: Demonstrate handling a multi‑page TIFF (comment out if not needed)
            // -----------------------------------------------------------------
            // HandleMultiPageTiff(@"C:\Invoices\multi_page_invoice.tif", ocrEngine);
        }

        // ---------------------------------------------------------------
        // Helper for multi‑page TIFFs – shows how to iterate pages
        // ---------------------------------------------------------------
        static void HandleMultiPageTiff(string path, OcrEngine engine)
        {
            using var multiPage = Image.FromFile(path);
            int pageCount = multiPage.GetFrameCount(FrameDimension.Page);

            for (int i = 0; i < pageCount; i++)
            {
                multiPage.SelectActiveFrame(FrameDimension.Page, i);
                using var page = (Image)multiPage.Clone();
                var result = engine.Recognize(page);
                Console.WriteLine($"\n--- Page {i + 1} ---");
                Console.WriteLine(result.Text);
            }
        }
    }
}
```

**Output previsto** (troncato per brevità):

```
=== OCR Output ===
Invoice #98765
Date: 02/28/2026
Bill To: Acme Corp.
Subtotal: $2,500.00
Tax (8%): $200.00
Total: $2,700.00
...
```

Esegui il programma e verifica che la console stampi il testo presente sulla fattura. Se ottieni stringhe vuote, ricontrolla che il percorso dell'immagine sia corretto e che il file non sia corrotto.

---

## Domande frequenti (FAQ)

**Q: Funziona su Linux?**  
A: Sì. Aspose.OCR è cross‑platform. Basta installare il runtime .NET per Linux e lo stesso pacchetto NuGet funziona. L'accelerazione GPU richiede una GPU compatibile CUDA e il driver appropriato.

**Q: E se non ho una GPU?**  
A: Il costruttore `OcrEngineMode.Gpu` ricade automaticamente su CPU quando non viene rilevata una GPU compatibile. Otterrai comunque risultati accurati; impiegherà solo un po' più di tempo.

**Q: Posso fare OCR su note scritte a mano?**  
A: I modelli predefiniti di Aspose si concentrano sul testo stampato. Per la scrittura a mano avresti bisogno di un modello specializzato o di un servizio diverso (ad es., Azure Form Recognizer). Tuttavia, puoi comunque provare lo stesso codice—aspettati solo punteggi di confidenza più bassi.

## Conclusione

Hai appena completato un **c# OCR tutorial** che mostra come *estrarre testo da immagine* file, eseguire **ocr invoice scanning**, e capire **come o

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}