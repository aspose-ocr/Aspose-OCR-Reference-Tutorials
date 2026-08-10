---
category: general
date: 2026-02-11
description: Scopri come eseguire l'OCR su un TIFF multipagina in C# usando Aspose
  OCR. Converti il TIFF in testo, estrai il testo dal TIFF e riconosci rapidamente
  il testo dall'immagine.
draft: false
keywords:
- how to run OCR
- recognize text from image
- convert tiff to text
- extract text from tiff
- perform OCR on image
language: it
og_description: Come eseguire l'OCR su un TIFF multipagina usando Aspose OCR in C#.
  Guida passo passo per convertire il TIFF in testo, estrarre il testo dal TIFF e
  riconoscere il testo dall'immagine.
og_title: Come eseguire OCR su immagini TIFF multi‑pagina – Tutorial completo C#
tags:
- OCR
- C#
- Aspose
- TIFF
title: Come eseguire l'OCR su immagini TIFF multi‑pagina con Aspose OCR – Guida C#
url: /it/net/text-recognition/how-to-run-ocr-on-multi-page-tiff-images-with-aspose-ocr-c-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR su immagini TIFF multi‑pagina con Aspose OCR

Ti sei mai chiesto **come eseguire OCR** su un TIFF scansionato che contiene diverse pagine? Non sei solo—molti sviluppatori incontrano questo ostacolo quando devono estrarre testo ricercabile da vecchi documenti. La buona notizia? Con Aspose OCR puoi riconoscere il testo da file immagine in poche righe di codice C#, e otterrai testo semplice concatenato pronto per l'indicizzazione o ulteriori elaborazioni.

In questo tutorial percorreremo l'intero flusso di lavoro: dall'installazione del pacchetto Aspose OCR, al caricamento di un TIFF multi‑pagina, alla conversione di TIFF in testo e infine alla visualizzazione del contenuto estratto. Alla fine sarai in grado di **estrarre testo da file TIFF**, **riconoscere testo da immagini** e persino automatizzare il processo per decine di file in un lavoro batch. Nessuna magia, solo passaggi chiari e pratici.

## Cosa imparerai

- Come configurare il motore Aspose OCR per il riconoscimento della lingua inglese.  
- Il codice esatto necessario per **convertire TIFF in testo** usando la classe `OcrEngine`.  
- Suggerimenti per gestire immagini multi‑pagina e garantire che ogni pagina sia separata correttamente.  
- Problemi comuni (come dipendenze native mancanti) e come evitarli.  

**Prerequisiti** – avrai bisogno di .NET 6 o successivo, Visual Studio (o qualsiasi editor C#), e una connessione internet per la funzionalità di download automatico delle risorse. Tutto qui; nessuna libreria nativa aggiuntiva con cui lottare.

---

## Passo 1 – Installa il pacchetto NuGet Aspose OCR

Prima di poter **eseguire OCR su file immagine** devi aggiungere la libreria al tuo progetto.

```bash
dotnet add package Aspose.OCR
```

> **Consiglio professionale:** Se lavori in Visual Studio, puoi anche fare clic con il tasto destro sul progetto → *Manage NuGet Packages* → cercare “Aspose.OCR” e fare clic su *Install*.

Il pacchetto include tutto il necessario, e con `AutomaticResourceDownload = true` il motore scaricherà i pacchetti linguistici al volo.

## Passo 2 – Inizializza il motore OCR (Come eseguire OCR)

Ora che il pacchetto è a posto, creiamo e configuriamo un'istanza di `OcrEngine`. Questo è il cuore di **come eseguire OCR** nel nostro scenario.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System.Drawing;   // For Image class
using System;

// Step 2: Create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,          // Recognize English text
    AutomaticResourceDownload = true,        // Auto‑download language data
    OutputFormat = OcrOutputFormat.Text      // Get plain concatenated text
};
```

**Perché è importante:** Impostare `Language` indica al motore quale set di caratteri aspettarsi, mentre `AutomaticResourceDownload` ti libera dal dover posizionare manualmente i file di lingua sul server. `OutputFormat` impostato su `Text` ci fornisce una semplice stringa—perfetta per pipeline **convertire TIFF in testo**.

## Passo 3 – Carica il TIFF multi‑pagina (Riconosci testo da immagine)

Un TIFF può contenere molti frame, ognuno dei quali rappresenta una pagina. La classe `System.Drawing.Image` astrae questo per noi.

```csharp
// Step 3: Load the multi‑page image to be processed
using (var image = Image.FromFile("YOUR_DIRECTORY/multi_page.tiff"))
{
    // Step 4: Run OCR on the image
    var ocrResult = ocrEngine.Recognize(image);

    // Step 5: Display the extracted text
    Console.WriteLine(ocrResult.Text);
}
```

> **E se il file non si trova nella stessa cartella?** Basta fornire un percorso assoluto completo o usare `Path.Combine` con `AppContext.BaseDirectory`.  
> **E per quanto riguarda l'uso della memoria?** L'istruzione `using` elimina l'immagine dopo l'elaborazione, prevenendo perdite—cruciale quando si elaborano in batch decine di TIFF di grandi dimensioni.

La chiamata `Recognize` itera automaticamente su ogni pagina del TIFF, concatenando i risultati con interruzioni di riga. È per questo che vedrai ogni pagina separata quando stampi `ocrResult.Text`.

## Passo 4 – Esempio completo funzionante (Tutti i passaggi in un unico file)

Di seguito trovi un'applicazione console completa, pronta per l'esecuzione. Copiala e incollala in un nuovo progetto console .NET e premi **F5**.

```csharp
// File: Program.cs
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Configure the OCR engine
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.English,
                AutomaticResourceDownload = true,
                OutputFormat = OcrOutputFormat.Text
            };

            // 2️⃣ Load your multi‑page TIFF (replace with your actual path)
            const string tiffPath = @"YOUR_DIRECTORY\multi_page.tiff";

            if (!System.IO.File.Exists(tiffPath))
            {
                Console.WriteLine($"File not found: {tiffPath}");
                return;
            }

            // 3️⃣ Perform OCR
            using (var image = Image.FromFile(tiffPath))
            {
                var result = ocrEngine.Recognize(image);

                // 4️⃣ Output the extracted text
                Console.WriteLine("=== OCR RESULT ===");
                Console.WriteLine(result.Text);
                Console.WriteLine("==================");
            }

            // Keep console open
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Output previsto** (troncato per brevità):

```
=== OCR RESULT ===
Page 1: The quick brown fox jumps over the lazy dog.
Page 2: Lorem ipsum dolor sit amet, consectetur adipiscing elit.
...
==================
Press any key to exit...
```

Ogni pagina appare su una propria riga perché `OcrOutputFormat.Text` inserisce un'interruzione di riga tra i frame. Se ti serve un delimitatore diverso, puoi post‑elaborare `result.Text` con `String.Replace`.

## Passo 5 – Gestione dei casi limite comuni

### 5.1 File TIFF di grandi dimensioni  
Quando si gestiscono TIFF di dimensioni gigabyte, caricare l'intero file in memoria può essere problematico. Una soluzione è elaborare ogni frame singolarmente:

```csharp
using (var image = Image.FromFile(tiffPath))
{
    for (int i = 0; i < image.GetFrameCount(FrameDimension.Page); i++)
    {
        image.SelectActiveFrame(FrameDimension.Page, i);
        var pageResult = ocrEngine.Recognize(image);
        Console.WriteLine($"--- Page {i + 1} ---");
        Console.WriteLine(pageResult.Text);
    }
}
```

### 5. Documenti non‑inglesi  
Se devi **riconoscere testo da immagine** in spagnolo o francese, basta cambiare la proprietà `Language`:

```csharp
ocrEngine.Language = OcrLanguage.Spanish; // or OcrLanguage.French
```

Aspose scaricherà automaticamente le risorse linguistiche appropriate.

### 5. Salvataggio dell'output  
Spesso vorrai **convertire TIFF in testo** e memorizzare il risultato in un file `.txt`:

```csharp
System.IO.File.WriteAllText("output.txt", ocrResult.Text);
```

Puoi anche dividere l'output per pagina usando `String.Split(Environment.NewLine)` e scrivere ogni segmento in un file separato.

## Consigli professionali e avvertenze

- **AutomaticResourceDownload** funziona la prima volta che esegui l'app; le esecuzioni successive sono offline.  
- Se vedi caratteri illeggibili, ricontrolla l'impostazione `Language`; i pacchetti linguistici non corrispondenti causano riconoscimenti errati.  
- Per i PDF rasterizzati in TIFF, potresti voler aumentare `ocrEngine.Dpi` (il valore predefinito è 300) per una maggiore precisione.  
- Avvolgi sempre `Image.FromFile` in un blocco `using`; altrimenti bloccherai il file e non potrai cancellarlo o spostarlo in seguito.

## Domande frequenti

**D: Funziona con TIFF a pagina singola?**  
R: Assolutamente. Il motore tratta un TIFF a frame singolo allo stesso modo; otterrai solo una riga di testo.

**D: Posso elaborare file PNG o JPEG allo stesso modo?**  
R: Sì—basta cambiare l'estensione del file. Il metodo `Recognize` accetta qualsiasi formato `System.Drawing.Image`.

**D: E se ho bisogno del risultato OCR come PDF invece che testo semplice?**  
R: Imposta `OutputFormat = OcrOutputFormat.Pdf` e `ocrResult` conterrà un array di byte PDF che potrai scrivere su disco.

## Conclusione

Ora hai una soluzione completa, end‑to‑end per **come eseguire OCR** su file TIFF multi‑pagina usando Aspose OCR in C#. Configurando il motore, caricando l'immagine e invocando `Recognize`, puoi **estrarre testo da TIFF**, **convertire TIFF in testo** e **riconoscere testo da immagine** con poche righe di codice. Sentiti libero di modificare la lingua, il formato di output o l'elaborazione frame‑per‑frame per adattarla alle tue esigenze di elaborazione batch.

Sei pronto per il passo successivo? Prova a combinare questo approccio con un servizio di monitoraggio cartelle per **eseguire OCR su file immagine** automaticamente non appena arrivano in una cartella di destinazione, oppure integra l'output in un indice di ricerca per una ricerca full‑text istantanea. Le possibilità sono infinite, e il codice che hai appena visto è una solida base.

Se hai incontrato problemi, lascia un commento qui sotto o contattami su GitHub. Buon coding e divertiti a trasformare quei testardi TIFF in testo ricercabile!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}