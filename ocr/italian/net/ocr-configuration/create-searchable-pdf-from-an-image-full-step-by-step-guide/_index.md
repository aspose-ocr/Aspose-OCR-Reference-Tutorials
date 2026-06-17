---
category: general
date: 2026-06-06
description: Scopri come creare PDF ricercabili e convertire immagini in PDF con OCR.
  Include l'aggiunta di layer, le impostazioni di compressione e il codice C# completo.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- how to ocr image
- how to add layer
- how to set compression
language: it
og_description: Crea PDF ricercabile da un'immagine usando OCR. Questa guida mostra
  come aggiungere un livello di testo nascosto, impostare la compressione e convertire
  l'immagine in PDF.
og_title: Crea PDF Ricercabile – Tutorial Completo C#
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Learn how to create searchable PDF and convert image to PDF with OCR.
    Includes layer addition, compression settings, and full C# code.
  headline: Create Searchable PDF from an Image – Full Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to create searchable PDF and convert image to PDF with OCR.
    Includes layer addition, compression settings, and full C# code.
  name: Create Searchable PDF from an Image – Full Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.7+). - The
      Aspose.OCR and Aspose.Pdf NuGet packages (or any equivalent library that offers
      `OcrEngine` and `PdfSaveOptions`). - A sample image, e.g., `invoice.png`, placed
      in a folder you can reference. - A basic understanding of C# syntax'
  - name: Full Working Example
    text: 'Putting it all together, here’s the complete, ready‑to‑run program:'
  - name: Pro tip
    text: If you need to **convert image to PDF** without OCR (just a plain image
      PDF), set `AddTextLayer = false`. The same `PdfSaveOptions` still lets you control
      compression, which is handy for archiving scanned documents that don’t need
      searchability.
  type: HowTo
tags:
- OCR
- PDF
- C#
- Aspose
title: Crea PDF ricercabile da un'immagine – Guida completa passo‑passo
url: /it/net/ocr-configuration/create-searchable-pdf-from-an-image-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea PDF Ricercabile – Tutorial Completo C#

Ti sei mai chiesto come **creare PDF ricercabile** da una fattura scansionata senza passare ore in uno strumento GUI? Non sei solo. Molti sviluppatori si trovano in difficoltà quando devono trasformare un'immagine in un PDF che mantenga l'aspetto originale e permetta agli utenti di copiare o cercare il testo.  

In questo tutorial percorreremo i passaggi esatti per **convertire immagine in PDF**, eseguire l'OCR, aggiungere un livello di testo nascosto e persino regolare le impostazioni di compressione. Alla fine avrai uno snippet C# pronto all'uso da inserire in qualsiasi progetto .NET.

## Cosa Imparerai

- Configurare un motore OCR e capire **come fare OCR su file immagine**.
- Usare le opzioni **come aggiungere livello** per incorporare una sovrapposizione di testo ricercabile.
- Applicare **come impostare la compressione** per PDF più piccoli compressi in zip.
- Trasformare un'immagine semplice in un flusso di lavoro per **creare PDF ricercabile** che puoi automatizzare.
- Problemi comuni e consigli professionali per mantenere i PDF nitidi e veloci.

### Prerequisiti

- .NET 6.0 o successivo (il codice funziona anche su .NET Framework 4.7+).
- I pacchetti NuGet Aspose.OCR e Aspose.Pdf (o qualsiasi libreria equivalente che offra `OcrEngine` e `PdfSaveOptions`).
- Un'immagine di esempio, ad es. `invoice.png`, posizionata in una cartella a cui puoi fare riferimento.
- Una comprensione di base della sintassi C# — non è necessario avere conoscenze approfondite di OCR.

> **Consiglio professionale:** Se stai usando Visual Studio, installa i pacchetti tramite la Package Manager Console:  
> `Install-Package Aspose.OCR`  
> `Install-Package Aspose.Pdf`

---

![Esempio di PDF ricercabile che mostra un'immagine di fattura trasformata in PDF con livello di testo nascosto](/images/create-searchable-pdf.png)

## Passo 1: Inizializzare il Motore OCR – **come fare OCR immagine**

Per prima cosa abbiamo bisogno di un motore OCR in grado di leggere il testo inglese dalla nostra immagine. La classe `OcrEngine` è il punto di ingresso; basta impostare la lingua e successivamente fornire un'immagine.

```csharp
using Aspose.OCR;
using Aspose.Pdf;

// Create and configure the OCR engine
OcrEngine engine = new OcrEngine
{
    Language = OcrLanguage.English
};
```

*Perché è importante:* Inizializzare il motore con la lingua corretta migliora notevolmente l'accuratezza. Se lo salti, potresti ottenere caratteri illeggibili.

## Passo 2: Caricare l'Immagine – **convertire immagine in pdf**

Adesso indirizziamo il motore al file che vogliamo elaborare. `ImageStream.FromFile` legge i byte e li prepara per l'OCR.

```csharp
// Load the image you want to turn into a searchable PDF
engine.Image = ImageStream.FromFile(@"C:\Docs\invoice.png");
```

Puoi anche caricare da un `MemoryStream` se l'immagine proviene da una richiesta web o da un database.

## Passo 3: Eseguire il Riconoscimento OCR – **come fare OCR immagine**

Con l'immagine caricata, l'elaborazione pesante avviene in una singola chiamata. Il metodo `Recognize` restituisce un `OcrResult` che contiene sia il testo estratto sia il bitmap originale.

```csharp
// Perform OCR on the loaded image
OcrResult ocrResult = engine.Recognize();
```

*Dietro le quinte:* Il motore analizza ogni pixel, rileva i caratteri e costruisce una stringa Unicode. Conserva anche i dati posizionali necessari per il livello di testo nascosto successivamente.

## Passo 4: Configurare le Opzioni di Salvataggio PDF – **come aggiungere livello** & **come impostare compressione**

Ecco dove avviene la magia di un PDF ricercabile. Creiamo un oggetto `PdfSaveOptions` che indica ad Aspose.Pdf come incorporare l'immagine originale, aggiungere una sovrapposizione di testo nascosta e comprimere il file finale.

```csharp
// Set up PDF options for a searchable PDF
PdfSaveOptions pdfOptions = new PdfSaveOptions
{
    IncludeImage = true,          // Keep the original image in the PDF
    AddTextLayer = true,          // Add a hidden text layer with OCR results
    Compression = PdfCompression.Zip   // Use ZIP compression for smaller size
};
```

- **IncludeImage** garantisce la fedeltà visiva della scansione originale.
- **AddTextLayer** crea un livello invisibile che i browser e i lettori PDF possono indicizzare per la ricerca.
- **Compression** riduce le dimensioni del file senza sacrificare la qualità; ZIP è un buon valore predefinito per la maggior parte dei documenti.

## Passo 5: Salvare il Risultato – **creare PDF ricercabile**

Infine, scriviamo il risultato OCR su disco usando le opzioni appena definite. Il metodo `Save` accetta il percorso di destinazione e l'istanza `PdfSaveOptions`.

```csharp
// Save the OCR result as a searchable PDF
ocrResult.Save(@"C:\Docs\invoice_searchable.pdf", pdfOptions);
```

Quando apri `invoice_searchable.pdf` in Adobe Reader o in qualsiasi visualizzatore moderno, vedrai l'immagine originale, ma ora potrai selezionare, copiare e cercare il testo come se fosse un PDF nativo.

### Esempio Completo Funzionante

Mettiamo tutto insieme, ecco il programma completo, pronto per l'esecuzione:

```csharp
using System;
using Aspose.OCR;
using Aspose.Pdf;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            OcrEngine engine = new OcrEngine
            {
                Language = OcrLanguage.English
            };

            // 2️⃣ Load the source image
            string imagePath = @"C:\Docs\invoice.png";
            engine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Perform OCR
            OcrResult result = engine.Recognize();

            // 4️⃣ Configure PDF options (layer + compression)
            PdfSaveOptions pdfOptions = new PdfSaveOptions
            {
                IncludeImage = true,
                AddTextLayer = true,
                Compression = PdfCompression.Zip
            };

            // 5️⃣ Save as searchable PDF
            string pdfPath = @"C:\Docs\invoice_searchable.pdf";
            result.Save(pdfPath, pdfOptions);

            Console.WriteLine($"Searchable PDF created at: {pdfPath}");
        }
    }
}
```

**Output previsto** (nella console):  
`Searchable PDF created at: C:\Docs\invoice_searchable.pdf`

Apri il file risultante, premi **Ctrl F**, digita una parola presente nella fattura e osserva il visualizzatore saltare immediatamente a quella posizione. Questo è il cuore di **creare PDF ricercabile** in azione.

## Problemi Comuni & Come Evitarli

| Problema | Perché accade | Soluzione |
|----------|----------------|-----------|
| Testo non ricercabile | `AddTextLayer` impostato a `false` o utilizzo di una versione più vecchia di Aspose | Assicurati che `AddTextLayer = true` e aggiorna all'ultimo pacchetto NuGet |
| PDF enorme (megabyte) | Compression impostata a `PdfCompression.None` | Passa a `PdfCompression.Zip` o `PdfCompression.Jpeg` per le immagini |
| Caratteri illeggibili | Lingua errata o immagine a bassa risoluzione | Imposta `engine.Language` correttamente e fornisci immagini di almeno 300 dpi |
| Livello nascosto invisibile in alcuni visualizzatori | PDF generato con una versione PDF non standard | Usa `PdfSaveOptions.PdfVersion = PdfVersion.PDF_1_7` (predefinita) o aggiorna il visualizzatore |

### Consiglio professionale

Se hai bisogno di **convertire immagine in PDF** senza OCR (solo un PDF immagine semplice), imposta `AddTextLayer = false`. Le stesse `PdfSaveOptions` ti permettono comunque di controllare la compressione, utile per archiviare documenti scansionati che non richiedono la ricercabilità.

## Estendere la Soluzione

- **Pagine multiple**: Itera su un elenco di file immagine, chiama `engine.Image = ...` ogni volta e accumula i risultati in un unico PDF usando l'aggregazione `PdfDocument`.
- **Lingue diverse**: Cambia `engine.Language = OcrLanguage.Spanish` (o qualsiasi lingua supportata) per gestire fatture multilingue.
- **Compressione personalizzata**: Per immagini ricche di colore, `PdfCompression.Jpeg` con un'impostazione di qualità (`pdfOptions.JpegQuality = 80`) può ridurre ulteriormente le dimensioni dei file.

## Conclusione

Abbiamo appena coperto tutto ciò di cui hai bisogno per **creare PDF ricercabili** da immagini usando C#. Dall'inizializzazione del motore OCR, al caricamento dell'immagine, al riconoscimento, alla configurazione di un livello di testo nascosto, fino all'impostazione della compressione — ogni elemento svolge un ruolo cruciale nel fornire un documento veloce e ricercabile.  

Ora puoi automatizzare l'elaborazione delle fatture, archiviare contratti o creare un'utilità di scansione di massa che trasforma pile di carta in PDF ricercabili istantaneamente.  

Pronto per la prossima sfida? Prova ad aggiungere filigrane, unire più PDF ricercabili o esporre questa logica tramite una Web API così che l'intera organizzazione possa caricare immagini e ricevere PDF ricercabili al volo.

---

*Se hai trovato utile questa guida, metti un ⭐, condividila con i colleghi o lascia un commento con le tue modifiche. Buon coding!*

## Cosa Dovresti Imparare Dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come fare OCR su PDF in .NET con Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Convertire Immagini in PDF C# – Salva Risultato OCR Multipagina](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [Come fare OCR su Immagine – Eseguire OCR su Immagine nel Riconoscimento Immagini OCR](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}