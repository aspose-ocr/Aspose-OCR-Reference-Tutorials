---
category: general
date: 2026-02-22
description: Genera PDF ricercabile ed estrai il testo dall'immagine usando Aspose
  OCR. Scopri come convertire un'immagine in PDF e ottenere testo semplice in un unico
  tutorial.
draft: false
keywords:
- generate searchable pdf
- extract text from image
- convert image to pdf
- output plain text
- convert scanned image pdf
language: it
og_description: Genera PDF ricercabile da immagini scannerizzate con Aspose OCR. Questa
  guida mostra come estrarre il testo dall'immagine, produrre testo semplice e convertire
  l'immagine in PDF.
og_title: Genera PDF Ricercabile da Immagini – Tutorial Completo C#
tags:
- C#
- OCR
- PDF generation
- Aspose
title: Genera PDF Ricercabile da Immagini in C# – Guida Passo‑Passo
url: /it/net/text-recognition/generate-searchable-pdf-from-images-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Genera PDF Ricercabile da Immagini in C# – Tutorial Completo

Hai mai avuto bisogno di **generare PDF ricercabile** da un'immagine scansionata ma non sapevi da dove cominciare? Non sei solo—la maggior parte degli sviluppatori si imbatte in questo ostacolo al primo contatto con l'OCR. La buona notizia? Con Aspose OCR puoi **estrarre testo da immagine**, **generare testo semplice** e **convertire immagine in PDF** in poche righe di C#.

In questa guida percorreremo l’intero processo, dal caricamento di un file PNG al salvataggio di un PDF ricercabile e di un file di testo semplice. Alla fine avrai uno snippet riutilizzabile da inserire in qualsiasi progetto .NET. Niente fronzoli, solo ciò che serve a portare a termine il lavoro.

## Cosa Imparerai

- Come configurare **Aspose.OCR** in un’app console .NET.  
- La differenza tra le modalità **output plain text** e **searchable PDF**.  
- Come **estrarre testo da immagine** e scriverlo in un file `.txt`.  
- Come **convertire immagine in PDF** mantenendo il bitmap originale e aggiungendo un livello di testo nascosto.  
- Suggerimenti per gestire grandi batch, errori comuni e dove regolare le impostazioni per una migliore precisione.

> **Prerequisiti** – Hai bisogno di .NET 6+ (o .NET Framework 4.7+), Visual Studio 2022 (o qualsiasi editor), e una licenza Aspose OCR (o una prova gratuita). Non sono richieste altre librerie di terze parti.

![generate searchable pdf example](image-placeholder.png "Example of a generated searchable PDF")

## Passo 1: Installa Aspose OCR e Crea il Motore

Prima di tutto—aggiungi il pacchetto NuGet al tuo progetto:

```bash
dotnet add package Aspose.OCR
```

Ora possiamo avviare il motore OCR e indicare quale lingua stiamo usando. L'inglese è il valore predefinito, ma puoi passare a francese, spagnolo, ecc., modificando l’enumerazione `Language`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System.IO;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine for English
        OcrEngine ocrEngine = new OcrEngine { Language = Language.English };
```

**Perché è importante:** Il motore contiene tutte le configurazioni—lingua, formato di output e flag opzionali di pre‑elaborazione. Impostarlo una volta e riutilizzarlo evita l’overhead di creare una nuova istanza per ogni file.

## Passo 2: Estrarre Testo e Salvare come Testo Semplice

Se ti servono solo i caratteri grezzi, imposta il motore su `OutputFormat.Text`. Questo dice ad Aspose OCR di saltare completamente la generazione del PDF e restituirti una stringa.

```csharp
        // Tell the engine to return plain text
        ocrEngine.OutputFormat = OutputFormat.Text;

        // Path to your source image (PNG, JPEG, BMP, etc.)
        string inputImagePath = @"YOUR_DIRECTORY/input.png";

        // Perform recognition – the result contains the extracted string
        OcrResult plainTextResult = ocrEngine.Recognize(Image.Load(inputImagePath));

        // Write the text to a .txt file
        string textOutputPath = @"YOUR_DIRECTORY/output.txt";
        File.WriteAllText(textOutputPath, plainTextResult.Text);
```

**Consiglio professionale:** `plainTextResult.Text` rimuove già le interruzioni di riga che appartengono al layout OCR. Se ti serve la spaziatura originale, ispeziona `plainTextResult.TextBlocks` invece.

### Risultato Atteso

Apri `output.txt` e dovresti vedere qualcosa di simile:

```
Hello, world!
This is a sample scanned document.
```

Questa è la parte **output plain text** del tutorial—rapida, leggera e perfetta per l’elaborazione successiva (ad es., indicizzazione).

## Passo 3: Passa alla Modalità PDF Ricercabile

Ora creiamo un **PDF ricercabile**. Il motore incorporerà il bitmap originale e sovrapporrà il testo generato dall’OCR, rendendo il documento ricercabile in qualsiasi visualizzatore PDF.

```csharp
        // Change the output format to searchable PDF
        ocrEngine.OutputFormat = OutputFormat.SearchablePdf;

        // Recognize the same image again – this time we get PDF bytes
        OcrResult pdfResult = ocrEngine.Recognize(Image.Load(inputImagePath));

        // Save the PDF bytes to a file
        string pdfOutputPath = @"YOUR_DIRECTORY/output.pdf";
        File.WriteAllBytes(pdfOutputPath, pdfResult.RawData);
    }
}
```

**Perché riconosciamo di nuovo:** Il motore OCR memorizza nella cache l’ultima immagine, ma il formato di output determina quali dati restituisce. Cambiare il formato forza un nuovo passaggio che include il livello di testo nascosto.

### Come Appare il PDF

Apri `output.pdf` in Adobe Reader o in qualsiasi visualizzatore e prova a selezionare il testo. Vedrai che puoi copiare, cercare e evidenziare il contenuto—anche se l’aspetto visivo è ancora il bitmap originale. Questo è il segno distintivo di una **convert scanned image pdf**.

## Passo 4: Gestire più File (Opzionale)

I progetti reali raramente trattano una sola immagine. Di seguito trovi un ciclo rapido che elabora tutti i PNG in una cartella, producendo i corrispondenti file `.txt` e `.pdf`.

```csharp
        string folder = @"YOUR_DIRECTORY";
        foreach (var file in Directory.GetFiles(folder, "*.png"))
        {
            // Plain‑text extraction
            ocrEngine.OutputFormat = OutputFormat.Text;
            var txtResult = ocrEngine.Recognize(Image.Load(file));
            File.WriteAllText(Path.ChangeExtension(file, ".txt"), txtResult.Text);

            // Searchable PDF generation
            ocrEngine.OutputFormat = OutputFormat.SearchablePdf;
            var pdfResult = ocrEngine.Recognize(Image.Load(file));
            File.WriteAllBytes(Path.ChangeExtension(file, ".pdf"), pdfResult.RawData);
        }
```

**Nota su casi limite:** Immagini molto grandi possono esaurire la memoria. Se incontri `OutOfMemoryException`, considera di ridimensionare con `Image.Resize` prima del riconoscimento, o elabora i file in batch più piccoli.

## Passo 5: Ottimizzare la Precisione dell’OCR

Aspose OCR offre alcune impostazioni regolabili:

| Impostazione | Cosa fa | Quando usarla |
|--------------|---------|---------------|
| `ocrEngine.PageSegmentationMode` | Controlla come il motore suddivide l'immagine in blocchi di testo. | Utile per layout a più colonne. |
| `ocrEngine.Deskew` | Ruota automaticamente pagine leggermente inclinate. | Documenti scansionati non perfettamente allineati. |
| `ocrEngine.RemoveNoise` | Cerca di pulire macchie e artefatti di sfondo. | Scansioni di bassa qualità o pagine fax. |

Esempio:

```csharp
ocrEngine.Deskew = true;
ocrEngine.RemoveNoise = true;
```

Abilitare queste opzioni può aumentare il tempo di elaborazione, ma il miglioramento nella qualità di **extract text from image** è spesso compensativo.

## Passo 6: Verificare l’Output Programmaticamente

A volte è necessario accertarsi che il PDF contenga effettivamente testo ricercabile (ad es., nei test automatizzati). Il controllo più semplice è verificare che l’array di byte del PDF non sia vuoto e che la lunghezza di `RawData` superi la dimensione dell’immagine.

```csharp
if (pdfResult.RawData.Length > Image.Load(inputImagePath).Data.Length)
{
    Console.WriteLine("Searchable PDF generated successfully!");
}
else
{
    Console.WriteLine("Warning: PDF may not contain hidden text.");
}
```

Per una validazione più approfondita potresti usare una libreria PDF (come iTextSharp) per estrarre il flusso di testo e confrontarlo con `plainTextResult.Text`.

## Problemi Comuni e Come Evitarli

- **Licenza Mancante** – Senza una licenza Aspose valida la libreria funziona in modalità di valutazione, aggiungendo una filigrana ai PDF. Registra la tua licenza subito (`License license = new License(); license.SetLicense("Aspose.OCR.lic");`).  
- **Percorso Errato** – Codificare percorsi assoluti funziona sulla tua macchina ma si rompe altrove. Usa `Path.Combine` con `AppDomain.CurrentDomain.BaseDirectory` per la portabilità.  
- **Formati Immagine Non Supportati** – GIF e TIFF con più frame richiedono una gestione speciale (`Image.LoadMultiPage`). Converti prima in PNG/JPEG se ti serve solo la prima pagina.  
- **Colli di Bottiglia delle Prestazioni** – Ricreare `OcrEngine` all'interno di un ciclo è costoso. Mantieni un'unica istanza e cambia solo `OutputFormat` come mostrato.

## Riepilogo

Abbiamo coperto l’intero flusso di lavoro per **generare PDF ricercabile** da un’immagine scansionata usando Aspose OCR:

1. Installa il pacchetto NuGet e crea un `OcrEngine`.  
2. Imposta `OutputFormat.Text` per **output plain text** e scrivilo in un file `.txt`.  
3. Passa a `OutputFormat.SearchablePdf` per **convert image to PDF** con un livello di testo invisibile.  
4. Salva i byte del PDF e, facoltativamente, elabora una directory per il batch processing.  
5. Ottimizza la precisione con deskew, rimozione del rumore e opzioni di segmentazione pagina.  

Il tutto in un programma compatto e autonomo che puoi copiare‑incollare in Visual Studio.

## Cosa Provare Dopo?

- **Elaborazione batch** con interfaccia UI (WinForms o WPF) così gli utenti possono trascinare i file.  
- **Rilevamento lingua** – Aspose OCR può rilevare automaticamente la lingua; prova `ocrEngine.Language = Language.AutoDetect`.  
- **Post‑processing** – Invia il testo estratto a un indice di ricerca (ElasticSearch, Azure Cognitive Search) per il recupero immediato dei documenti.  
- **Output alternativi** – Usa `OutputFormat.Hocr` per risultati OCR basati su HTML, utili per anteprime web.

Sentiti libero di sperimentare con diverse risoluzioni d’immagine, modalità colore e impostazioni OCR. Più giochi, più capirai i compromessi tra velocità e precisione.

---

**Buon coding!** Se incontri qualche strano problema, lascia un commento qui sotto o consulta la documentazione di Aspose OCR per approfondimenti. Il tuo prossimo progetto—che sia fatturazione, archiviazione o la creazione di una base di conoscenza ricercabile—è appena diventato molto più semplice.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}