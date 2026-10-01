---
category: general
date: 2026-01-04
description: Scopri come abilitare i moduli e estrarre tabelle dalle immagini usando
  OCR in C#. Questo tutorial passo‑passo mostra anche come eseguire l'OCR su un'immagine
  e rilevare le tabelle.
draft: false
keywords:
- how to enable forms
- how to extract tables
- run OCR image
- use OCR C#
- detect tables OCR
language: it
og_description: Guida passo‑passo su come abilitare i moduli, estrarre tabelle, eseguire
  OCR su immagini e rilevare tabelle OCR usando C#.
og_title: Come abilitare i moduli e estrarre le tabelle con OCR in C#
tags:
- OCR
- C#
- Computer Vision
title: Come abilitare i moduli e estrarre tabelle con OCR in C# – Guida completa
url: /it/net/image-and-drawing-recognition/how-to-enable-forms-and-extract-tables-with-ocr-in-c-complet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come abilitare i moduli e estrarre tabelle con OCR in C# – Guida completa

Ti sei mai chiesto **come abilitare i moduli** quando scansioni fatture, ricevute o qualsiasi documento strutturato? Non sei solo. In molti progetti reali il punto di attrito più grande è far capire all'OCR sia i campi del modulo **che** le tabelle senza un milione di righe di parsing personalizzato.  

In questo tutorial percorreremo una soluzione pratica, end‑to‑end, che mostra **come abilitare i moduli**, **come estrarre le tabelle**, e persino **come eseguire l'elaborazione OCR di un'immagine** in un unico programma C#. Alla fine avrai uno snippet pronto all'uso che rileva le tabelle in stile OCR, estrae coppie chiave‑valore e le stampa sulla console.

> **Prerequisiti** – .NET 6+ (o .NET Framework 4.7+), un riferimento all'OCR SDK che stai usando (l'esempio presuppone una classe generica `OcrEngine`), e un file immagine (`invoice_table.png`) che contiene una tabella o un modulo. Non sono richieste altre librerie esterne.

![how to enable forms with OCR C#](image.png)

## Cosa copre questo tutorial

- **Abilitare il riconoscimento dei moduli** in modo che campi come “Invoice Number” o “Date” vengano identificati automaticamente.  
- **Estrarre le tabelle** da documenti scansionati, ottenendo conteggi di righe/colonne e contenuti delle celle.  
- **Eseguire l'elaborazione OCR di un'immagine** con una singola chiamata e gestire il risultato programmaticamente.  
- Suggerimenti per i casi limite **detect tables OCR**, come celle unite o bordi mancanti.  

Iniziamo.

## Passo 1: Configurare il motore OCR – come abilitare i moduli

Prima che possa avvenire qualsiasi riconoscimento è necessario un'istanza del motore OCR. La maggior parte degli SDK espone un costruttore semplice; indicheremo anche dove è possibile modificare le opzioni di configurazione in seguito.

```csharp
using System;
using System.Linq;

// Assume the OCR SDK namespace is OcrSdk
using OcrSdk;

public class OcrDemo
{
    public static void Main()
    {
        // Create the OCR engine – this is where “how to enable forms” starts.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image that contains a table or form.
        // Replace the path with the actual location of your PNG/JPEG/TIFF file.
        ocrEngine.LoadImage(@"YOUR_DIRECTORY/invoice_table.png");
```

**Perché è importante:** L'istanziazione del motore alloca risorse interne (come i modelli linguistici). Se salti questo passo la successiva chiamata `Recognize` genererà una `NullReferenceException`.

## Passo 2: Attivare l'estrazione strutturata – come estrarre tabelle & detect tables OCR

Ora abilitiamo le due funzionalità principali: il riconoscimento delle tabelle e l'estrazione dei campi del modulo. La maggior parte dei moderni motori OCR espone flag booleani o un oggetto `Config` più granulare.

```csharp
        // Enable structured extraction features.
        ocrEngine.Config.EnableTableRecognition = true;   // detect tables OCR
        ocrEngine.Config.EnableFormRecognition = true;    // how to enable forms
```

**Consiglio professionale:** Se ti serve solo una delle due funzionalità, disabilitare l'altra può migliorare le prestazioni fino al 20 %.

## Passo 3: Eseguire OCR Image e ottenere il risultato – run OCR image

Con il motore configurato, una singola chiamata al metodo fa il lavoro pesante. L'`OcrResult` restituito contiene collezioni per tabelle e campi del modulo.

```csharp
        // Run OCR – this is the “run OCR image” step.
        OcrResult ocrResult = ocrEngine.Recognize();

        // -----------------------------------------------------------------
        // Step 4: Process Detected Tables – how to extract tables
        // -----------------------------------------------------------------
        foreach (var table in ocrResult.Tables)
        {
            Console.WriteLine($"Table {table.Id}: {table.Rows.Count} rows, {table.Columns.Count} columns");

            // Show the first row for a quick sanity check.
            if (table.Rows.Count > 0)
            {
                var firstRow = table.Rows[0];
                Console.WriteLine(string.Join(" | ", firstRow.Cells.Select(c => c.Text)));
            }
        }

        // -----------------------------------------------------------------
        // Step 5: Process Detected Form Fields – how to enable forms
        // -----------------------------------------------------------------
        foreach (var field in ocrResult.FormFields)
        {
            Console.WriteLine($"{field.Key}: {field.Value}");
        }
    }
}
```

### Output previsto sulla console

```
Table 1: 5 rows, 4 columns
Item | Qty | Price | Total
InvoiceNumber: INV-2025-001
Date: 2025-12-31
Customer: Acme Corp.
```

I numeri esatti varieranno in base all'immagine di origine, ma dovresti vedere una riga di riepilogo per ogni tabella seguita dai valori delle celle della prima riga, e poi un elenco di coppie chiave‑valore per i campi del modulo.

## Passo 4: Gestire i casi limite durante il rilevamento delle tabelle OCR

Anche con `EnableTableRecognition = true`, l'OCR può incontrare difficoltà su:

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **Merged cells** | The engine treats the merged area as a single cell. | Post‑process rows: look for unusually wide cells and split them based on whitespace. |
| **Missing borders** | Table lines are faint or broken. | Increase image contrast before feeding it to the engine (`ocrEngine.PreprocessImage`). |
| **Rotated tables** | Document scanned at an angle. | Use `ocrEngine.Config.AutoRotate = true` (if available). |

**Suggerimento:** Controlla sempre `table.Rows.Count` e `table.Columns.Count` prima di accedere agli indici per evitare `IndexOutOfRangeException`.

## Passo 5: Mettere tutto insieme – un esempio completo e eseguibile

Di seguito trovi il programma completo che puoi copiare‑incollare in un nuovo progetto console. Include le direttive `using`, la configurazione del motore e la logica di elaborazione mostrata in precedenza.

```csharp
using System;
using System.Linq;
using OcrSdk;   // Replace with your actual OCR SDK namespace

public class OcrDemo
{
    public static void Main()
    {
        // 1️⃣ Create OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the target image
        ocrEngine.LoadImage(@"YOUR_DIRECTORY/invoice_table.png");

        // 3️⃣ Enable structured extraction (forms + tables)
        ocrEngine.Config.EnableTableRecognition = true;   // detect tables OCR
        ocrEngine.Config.EnableFormRecognition = true;    // how to enable forms

        // 4️⃣ Run OCR – “run OCR image”
        OcrResult ocrResult = ocrEngine.Recognize();

        // 5️⃣ Process tables – “how to extract tables”
        foreach (var table in ocrResult.Tables)
        {
            Console.WriteLine($"Table {table.Id}: {table.Rows.Count} rows, {table.Columns.Count} columns");
            if (table.Rows.Count > 0)
            {
                var firstRow = table.Rows[0];
                Console.WriteLine(string.Join(" | ", firstRow.Cells.Select(c => c.Text)));
            }
        }

        // 6️⃣ Process form fields – “how to enable forms”
        foreach (var field in ocrResult.FormFields)
        {
            Console.WriteLine($"{field.Key}: {field.Value}");
        }
    }
}
```

Esegui il programma (`dotnet run` o `Ctrl+F5` in Visual Studio) e vedrai l'output sulla console descritto prima.

## Domande frequenti (FAQ)

**Q: Funziona con input PDF?**  
A: La maggior parte degli OCR SDK accetta PDF rasterizzando internamente ogni pagina. Basta chiamare `ocrEngine.LoadPdf("file.pdf")` invece di `LoadImage`.

**Q: E se la mia immagine contiene sia una tabella *che* una firma?**  
A: La firma apparirà come una regione immagine separata. Puoi ignorarla controllando `ocrResult.Images` per testo a bassa confidenza.

**Q: Posso esportare le tabelle in CSV?**  
A: Assolutamente. Dopo aver iterato su `table.Rows`, scrivi ogni `cell.Text` in un `StringBuilder` separato da virgole, quindi salva la stringa in un file `.csv`.

## Conclusione

Ora sai **come abilitare i moduli**, **come estrarre le tabelle**, e i passaggi esatti per **eseguire l'elaborazione OCR di un'immagine** usando C#. L'esempio dimostra l'intero flusso di lavoro—dalla creazione del motore, alla configurazione, fino alla gestione del risultato—così da poterlo copiare direttamente nei tuoi progetti.  

Successivamente, prova a sostituire l'immagine di esempio con un PDF fattura a più pagine, sperimenta con `ocrEngine.Config.AutoRotate`, o invia i dati estratti a un database. Queste estensioni approfondiranno la tua padronanza di **detect tables OCR** e **use OCR C#** in scenari di produzione.

Se incontri problemi, lascia un commento qui sotto. Buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}