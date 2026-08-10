---
category: general
date: 2026-03-23
description: Crea PDF ricercabile da immagine usando Aspose OCR. Scopri come convertire
  TIFF in PDF con alta compressione e riconoscere il testo dell'immagine in pochi
  minuti.
draft: false
keywords:
- create searchable pdf
- convert tiff to pdf
- high compression pdf
- recognize image text
- searchable pdf from image
language: it
og_description: Crea PDF ricercabile da immagine con Aspose OCR. Questo tutorial mostra
  come convertire TIFF in PDF, aggiungere uno strato di testo ricercabile e applicare
  un'elevata compressione.
og_title: Crea PDF Ricercabile da Immagine – Guida Completa C#
tags:
- Aspose OCR
- C#
- PDF generation
title: Crea PDF Ricercabile da Immagine – Guida Completa in C#
url: /it/net/text-recognition/create-searchable-pdf-from-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea PDF Ricercabile da Immagine – Guida Completa C#

Hai mai avuto bisogno di **creare PDF ricercabili** da un documento scansionato ma non sapevi da dove cominciare? Non sei l'unico—molti sviluppatori si trovano allo stesso ostacolo quando trasformano scansioni TIFF in PDF ricercabili. La buona notizia? Con Aspose OCR puoi **convert tiff to pdf**, aggiungere un livello di testo nascosto sopra e persino ridurre le dimensioni del file con le opzioni **high compression pdf**, il tutto in poche righe di C#.

In questo tutorial percorreremo l'intero processo: dall'installazione dei pacchetti NuGet corretti, al caricamento di un'immagine TIFF, al riconoscimento del suo testo, e infine all'esportazione di un PDF ricercabile. Alla fine avrai un'app console eseguibile che **recognize image text** e produce un PDF compatto e ricercabile pronto per l'indicizzazione. Nessuno strumento aggiuntivo, nessun passaggio OCR manuale—solo codice pulito e una breve spiegazione.

## Prerequisiti & Cosa Ti Serve

- **.NET 6+** (o .NET Framework 4.6+). L'API funziona su entrambi, ma .NET 6 ti offre i più recenti miglioramenti del runtime.  
- **Visual Studio 2022** o qualsiasi IDE tu preferisca.  
- Pacchetti NuGet **Aspose.OCR** e **Aspose.OCR.Gpu** (il pacchetto GPU è opzionale ma accelera il riconoscimento sull'hardware supportato).  
- Un file TIFF di esempio (ad esempio `invoice.tif`) posizionato in una cartella di tua scelta.  

Se hai già questi elementi, ottimo—passa oltre. Altrimenti, il passaggio di installazione qui sotto coprirà tutto.

## Passo 1: Installa i Pacchetti Aspose OCR

Per iniziare, apri la cartella del tuo progetto in un terminale ed esegui:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

Questi comandi scaricano sia il motore OCR core sia la libreria di accelerazione GPU. Quest'ultima non è obbligatoria; il motore tornerà alla modalità CPU se non trova una GPU compatibile.

> **Consiglio Pro:** Quando miri a un ambiente di produzione, blocca le versioni dei pacchetti nel tuo `csproj` per evitare cambiamenti inattesi che rompano il codice.

## Passo 2: Configura lo Scheletro del Progetto

Crea una nuova app console (se non ne hai già una):

```bash
dotnet new console -n PdfExportDemo
cd PdfExportDemo
```

Sostituisci il `Program.cs` generato automaticamente con il codice completo mostrato più avanti. Il programma:

1. Inizializza un `OcrEngine` con supporto GPU.  
2. Carica l'immagine TIFF.  
3. Esegue l'OCR e abortisce in modo pulito in caso di errore.  
4. Configura **PdfExportOptions** per un livello ricercabile e **high compression**.  
5. Scrive il file di output.

## Passo 3: Scrivi il Codice Completo (Esempio Completo)

Di seguito trovi il file sorgente *intero*. Copialo e incollalo in `Program.cs`. I commenti spiegano il “perché” dietro ogni riga, non solo il “cosa”.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;

class PdfExport
{
    static void Main()
    {
        // ------------------------------------------------------------
        // 1️⃣ Initialise OCR engine with GPU acceleration.
        //    GpuMode.Enabled tells Aspose to use the GPU if one is present.
        //    If no compatible GPU exists, the engine automatically falls back
        //    to CPU mode—no extra code required.
        // ------------------------------------------------------------
        using (OcrEngine ocrEngine = new OcrEngine(GpuMode.Enabled))
        {
            // ------------------------------------------------------------
            // 2️⃣ Load the source image.
            //    ImageStream.FromFile supports many formats; here we use TIFF.
            // ------------------------------------------------------------
            string inputPath = @"YOUR_DIRECTORY\invoice.tif";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // ------------------------------------------------------------
            // 3️⃣ Perform OCR recognition.
            //    Recognize() returns false if the engine cannot read the image.
            //    Exiting early prevents us from creating an empty PDF.
            // ------------------------------------------------------------
            if (!ocrEngine.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return;
            }

            // ------------------------------------------------------------
            // 4️⃣ Configure PDF export options.
            //    IncludeTextLayer = true adds an invisible, searchable text layer.
            //    CompressionLevel = High reduces file size dramatically.
            // ------------------------------------------------------------
            PdfExportOptions pdfExportOptions = new PdfExportOptions
            {
                IncludeTextLayer = true,
                CompressionLevel = PdfCompression.High
            };

            // ------------------------------------------------------------
            // 5️⃣ Save the searchable PDF.
            //    The output will be a compact, searchable PDF ready for indexing.
            // ------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\invoice.pdf";
            ocrEngine.Save(outputPath, pdfExportOptions);
            Console.WriteLine($"Searchable PDF saved to: {outputPath}");
        }
    }
}
```

### Perché Funziona

- **GPU acceleration** può ridurre il tempo di riconoscimento da secondi a millisecondi su schede moderne—utile per l'elaborazione in batch.  
- **IncludeTextLayer** incorpora il testo derivato dall'OCR in modo invisibile, permettendo ai visualizzatori PDF di cercare il documento senza alterarne l'aspetto visivo.  
- **High compression** utilizza la compressione Flate (ZIP) sul flusso dell'immagine, che è senza perdita ma riduce drasticamente le dimensioni del file—ideale per archiviare migliaia di fatture.

## Passo 4: Esegui l'Applicazione e Verifica l'Uscita

Apri un terminale nella cartella del progetto ed esegui:

```bash
dotnet run
```

Se tutto è configurato correttamente, vedrai:

```
Searchable PDF saved to: YOUR_DIRECTORY\invoice.pdf
```

Apri `invoice.pdf` in qualsiasi lettore PDF (Adobe Acrobat, Edge o anche un browser). Prova a cercare una parola che sai comparire nel TIFF originale—ad esempio “Total”. Il visualizzatore dovrebbe evidenziare la parola anche se fa parte dell'immagine. Questo è il segno distintivo di un **searchable pdf**.

### Dimensione del File Prevista

Una fattura scansionata tipica (≈300 KB TIFF) si riduce spesso a **~80 KB** dopo aver applicato `PdfCompression.High`. La dimensione esatta dipende dalla complessità dell'immagine, ma noterai una chiara riduzione.

## Passo 5: Varianti Comuni & Casi Limite

| Situazione | Cosa Modificare | Perché |
|-----------|----------------|-----|
| **Nessuna GPU disponibile** | Modifica `new OcrEngine(GpuMode.Enabled)` in `new OcrEngine(GpuMode.Disabled)` | Previene che il motore tenti l'inizializzazione della GPU, il che può causare un breve ritardo. |
| **Pagine multiple (TIFF multi‑pagina)** | Imposta `ocrEngine.Image = ImageStream.FromFile("multi.tif", PageRange.All);` | Carica tutti i frame; Aspose elaborerà ogni pagina e genererà un PDF multi‑pagina. |
| **Necessità di lingua OCR diversa dall'inglese** | `ocrEngine.Language = Language.French;` (o qualsiasi lingua supportata) | Migliora l'accuratezza per documenti non‑inglesi. |
| **Desideri una sovrapposizione di testo visibile invece del livello nascosto** | `pdfExportOptions.IncludeTextLayer = false;` e aggiungi manualmente gli oggetti `TextFragment`. | Utile quando vuoi che il testo OCR appaia come testo selezionabile sopra l'immagine. |
| **PDF ultra‑piccoli** | Combina `PdfCompression.High` con `ImageResolution = 150` DPI prima del riconoscimento. | Una DPI più bassa riduce i dati dell'immagine, riducendo ulteriormente il PDF a scapito della fedeltà visiva. |

> **Nota:** Testa sempre i casi limite su un piccolo campione prima di scalare in produzione. L'accuratezza dell'OCR può variare con la qualità dell'immagine, il rumore e la lingua.

## Passo 6: Consigli per Implementazioni Pronte per la Produzione

1. **Error Logging** – Sostituisci `Console.WriteLine` con un framework di logging appropriato (Serilog, NLog) per una diagnostica più semplice.  
2. **Batch Processing** – Avvolgi la logica principale in un metodo che accetta percorsi di input/output, poi itera su una directory di file TIFF.  
3. **Async I/O** – Sebbene Aspose OCR sia sincrono, il caricamento e il salvataggio dei file possono essere asincroni per mantenere i thread UI reattivi.  
4. **Security** – Se esponi questa funzionalità tramite un'API web, valida i percorsi dei file e limita le dimensioni dei file per prevenire abusi.  
5. **Version Pinning** – Usa numeri di versione esatti (`<PackageReference Include="Aspose.OCR" Version="23.12.0" />`) per garantire un comportamento coerente tra le build.

## Conclusione

Abbiamo appena costruito una **soluzione completa, end‑to‑end** che **create searchable pdf** file da immagini scansionate, **convert tiff to pdf**, e lo fa con impostazioni **high compression pdf** mentre **recognize image text** accuratamente. Il risultato, un **searchable pdf from image**, è leggero, ricercabile e pronto per flussi di lavoro a valle come indicizzazione, archiviazione o e‑discovery.

Hai un batch di fatture? Inserisci il metodo in un ciclo, puntalo a una cartella e lascia che Aspose OCR faccia il lavoro pesante. Vuoi sperimentare con diversi livelli di compressione o pacchetti linguistici? Il codice è sufficientemente modulare da scambiare queste opzioni in pochi secondi.

---

*Pronto a fare il salto di livello?* Prova ad aggiungere una filigrana, incorporare metadati, o persino unire più PDF elaborati con OCR. La suite Aspose offre molte estensioni—esplora la documentazione e mantieni lo slancio. Buon coding!

![Crea PDF ricercabile da immagine esempio screenshot](https://example.com/images/create-searchable-pdf.png "esempio di pdf ricercabile")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}