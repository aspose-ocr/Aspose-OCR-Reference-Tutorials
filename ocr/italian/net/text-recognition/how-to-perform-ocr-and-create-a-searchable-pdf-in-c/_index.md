---
category: general
date: 2026-02-14
description: Impara come eseguire l'OCR su un file TIFF o un'immagine e convertire
  PDF usando l'OCR per creare un PDF ricercabile—guida passo‑passo in C#.
draft: false
keywords:
- how to perform OCR
- convert pdf using OCR
- make searchable pdf
- tiff to searchable pdf
- searchable pdf from image
language: it
og_description: Scopri come eseguire l'OCR su immagini, convertire PDF usando l'OCR
  e creare un PDF ricercabile con Aspose OCR in un conciso tutorial C#.
og_title: Come eseguire l'OCR e creare un PDF ricercabile in C#
tags:
- OCR
- C#
- Aspose
- PDF conversion
title: Come eseguire OCR e creare un PDF ricercabile in C#
url: /it/net/text-recognition/how-to-perform-ocr-and-create-a-searchable-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR e creare un PDF ricercabile in C#

Hai mai avuto bisogno di **perform OCR** su un documento scansionato ma non eri sicuro di come trasformare il risultato in un PDF ricercabile? Non sei solo—molti sviluppatori incontrano questo ostacolo quando lavorano con archivi TIFF legacy o PDF solo immagine. La buona notizia? Con poche righe di C# e la libreria Aspose.OCR, puoi convertire un TIFF o qualsiasi immagine in un PDF completamente ricercabile in pochi secondi.

In questo tutorial ti guideremo attraverso tutto ciò che devi sapere: dall'installazione della libreria, al caricamento di un TIFF multi‑pagina, fino alla chiamata di `RecognizeToPdf` così potrai **convert PDF using OCR** e **make searchable PDF** file che i tuoi utenti potranno effettivamente cercare. Alla fine, avrai un'app console pronta all'uso che produce un PDF ricercabile da una sorgente immagine.

## Prerequisiti

- **.NET 6.0** o versioni successive (il codice funziona anche su .NET Framework 4.7+).
- Una licenza valida di **Aspose.OCR** o una chiave di valutazione temporanea (la versione di prova gratuita è sufficiente per i test).
- Visual Studio 2022 (o qualsiasi editor tu preferisca) con il gestore di pacchetti **NuGet**.
- Un file di input chiamato `input.tif` posizionato in una cartella di tua scelta—i TIFF multi‑pagina funzionano subito.

> **Pro tip:** Se sei su Windows, copia il TIFF nella stessa cartella dell'`.exe` compilato per evitare problemi legati ai percorsi.

## Passo 1: Installa il pacchetto NuGet Aspose.OCR

Apri la cartella del tuo progetto in un terminale ed esegui:

```bash
dotnet add package Aspose.OCR
```

Questo scarica l'ultima versione stabile (a febbraio 2026 è 23.10) e aggiunge tutte le dipendenze necessarie. Dopo il completamento del restore, vedrai `Aspose.OCR` elencato sotto **Dependencies** in Solution Explorer.

## Passo 2: Crea un'applicazione console minimale

Crea un nuovo progetto console se non ne hai già uno:

```bash
dotnet new console -n OcrSearchablePdfDemo
cd OcrSearchablePdfDemo
```

Sostituisci il `Program.cs` generato automaticamente con il codice completo mostrato in **Step 3**. Il programma:

1. Istanzia il motore OCR.
2. Carica l'immagine di origine (o il TIFF multi‑pagina).
3. Esegue l'OCR e scrive l'output direttamente in un PDF ricercabile.
4. Notifica all'utente che il processo è riuscito.

## Passo 3: Codice completo – Dall'immagine al PDF ricercabile

Di seguito trovi il file sorgente **intero**. Copialo e incollalo in `Program.cs`. I commenti sono inclusi per spiegare le parti non ovvie.

```csharp
using System;
using Aspose.OCR;          // Core OCR namespace
using Aspose.OCR.Image;   // Provides ImageStream helpers

namespace OcrSearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Initialise the OCR engine.
            // -------------------------------------------------
            // The Engine class is the entry point for all OCR operations.
            // You can optionally pass a license object here if you have one.
            var ocrEngine = new Engine();

            // -------------------------------------------------
            // 2️⃣ Load the source image.
            // -------------------------------------------------
            // ImageStream.FromFile supports TIFF, PDF, JPEG, PNG, etc.
            // For multi‑page TIFFs the stream automatically contains all pages.
            string inputPath = "YOUR_DIRECTORY/input.tif";
            var imageStream = ImageStream.FromFile(inputPath);

            // -------------------------------------------------
            // 3️⃣ Perform OCR and write a searchable PDF.
            // -------------------------------------------------
            // RecognizeToPdf does the heavy lifting:
            // • It runs the OCR engine on every page.
            // • It embeds the extracted text as an invisible layer.
            // • The visual appearance of the original image is preserved.
            string outputPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.RecognizeToPdf(imageStream, outputPath);

            // -------------------------------------------------
            // 4️⃣ Inform the user.
            // -------------------------------------------------
            Console.WriteLine("Searchable PDF created at: " + outputPath);
        }
    }
}
```

**Cosa vedrai:** Dopo aver eseguito il programma, appare un file chiamato `searchable.pdf` nella cartella di destinazione. Aprilo con Adobe Reader o qualsiasi visualizzatore PDF e prova a cercare una parola presente nel TIFF originale. Il testo dovrebbe essere trovato immediatamente, dimostrando che hai **made searchable PDF** con successo da un'immagine.

### Esecuzione dell'app

```bash
dotnet run
```

Se tutto è configurato correttamente otterrai:

```
Searchable PDF created at: YOUR_DIRECTORY/searchable.pdf
```

Apri il PDF, premi `Ctrl+F`, digita una parola dalla sorgente e osserva l'evidenziazione saltare nella posizione corretta.

## Passo 4: Varianti comuni e casi limite

### Conversione di un PDF normale (solo immagine) in PDF ricercabile

Se la tua sorgente è un PDF che contiene immagini scansionate anziché testo, puoi comunque usare lo stesso metodo—basta cambiare la sorgente `ImageStream`:

```csharp
var pdfStream = ImageStream.FromFile("YOUR_DIRECTORY/input.pdf");
ocrEngine.RecognizeToPdf(pdfStream, "YOUR_DIRECTORY/searchable_from_pdf.pdf");
```

Ciò soddisfa lo scenario **convert pdf using OCR** senza alcun codice aggiuntivo.

### Gestione di documenti multi‑pagina di grandi dimensioni

Per documenti che superano qualche centinaio di pagine, considera:

- **Aumentare i limiti di memoria** (`Engine.MemoryLimit = 2_000; // MB`).
- **Elaborare a blocchi**: carica un sottoinsieme di pagine, scrivi PDF intermedi, poi uniscili usando una libreria PDF (ad esempio, Aspose.PDF).

### Gestione di lingue diverse dall'inglese

Aspose.OCR supporta molte lingue fin da subito. Imposta la lingua prima del riconoscimento:

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

Se ti serve **tiff to searchable pdf** in uno script non latino, assicurati che il relativo language pack sia installato.

### Cosa fare se il PDF di output è vuoto?

- Verifica che il file di input non sia corrotto.
- Assicurati che il motore OCR abbia una licenza valida—la modalità di valutazione può imporre limiti di pagine.
- Controlla che la risoluzione dell'immagine sia almeno 300 dpi; risoluzioni inferiori possono causare un riconoscimento scadente.

## Passo 5: Verifica del risultato programmaticamente (opzionale)

A volte vuoi confermare che il PDF contenga effettivamente un livello di testo. Puoi usare Aspose.PDF per estrarre il testo:

```csharp
using Aspose.Pdf;

var pdfDoc = new Document("YOUR_DIRECTORY/searchable.pdf");
string extracted = pdfDoc.Pages[1].ExtractText();
Console.WriteLine("First page text snippet: " + extracted.Substring(0, 100));
```

Se `extracted` non è vuoto, hai **made searchable pdf** con successo.

## Conclusione

Abbiamo coperto **how to perform OCR** su un TIFF (o qualsiasi immagine) e in modo fluido **convert PDF using OCR** per creare un **searchable PDF** che si comporta come un documento nativo. I passaggi chiave sono:

1. Installa Aspose.OCR.  
2. Inizializza `Engine`.  
3. Carica l'immagine tramite `ImageStream`.  
4. Chiama `RecognizeToPdf`.  

Da lì puoi sperimentare con le impostazioni della lingua, l'elaborazione di grandi batch, o combinare l'output con altre attività di manipolazione PDF. Lo stesso schema funziona per **tiff to searchable pdf**, **searchable pdf from image**, e anche per PDF scansionati.

Pronto per la prossima sfida? Prova a incorporare l'OCR in una web API così gli utenti possono caricare scansioni e ricevere PDF ricercabili istantaneamente, oppure esplora l'OCR su note scritte a mano usando le impostazioni avanzate di `OcrEngine`. Le possibilità sono infinite—buon coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}