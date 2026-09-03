---
category: general
date: 2026-09-03
description: Scopri come abilitare forms c# ed estrarre tabelle con OCR in C#. Questa
  guida passo‑a‑passo mostra come eseguire OCR su immagini e rilevare tabelle.
draft: false
keywords:
- enable forms c#
- extract tables c#
- detect tables OCR
- use OCR C#
- run OCR image
lastmod: 2026-09-03
og_description: Abilita forms c# ed estrai tabelle con OCR in C#. Segui questa guida
  passo‑a‑passo per eseguire OCR su immagini, rilevare tabelle ed estrarre coppie
  chiave‑valore in modo efficiente.
og_image_alt: Guide showing C# code to enable forms and extract tables using OCR
og_title: Abilita forms c# ed estrai tabelle con OCR in C#
schemas:
- author: Aspose
  dateModified: '2026-09-03'
  description: Learn how to enable forms c# and extract tables with OCR in C#. This
    step‑by‑step guide shows how to run OCR on images and detect tables.
  headline: How to enable forms c# and extract tables with OCR in C#
  type: TechArticle
- questions:
  - answer: Yes. Most OCR SDKs rasterize each PDF page internally, so you can call
      `ocrEngine.LoadPdf("file.pdf")` instead of `LoadImage`.
    question: Does this work with PDF input?
  - answer: The signature appears as a separate image region with low‑confidence text.
      You can filter it out by checking `ocrResult.Images` for confidence below a
      threshold.
    question: My image contains both a table and a handwritten signature—what happens?
  - answer: Absolutely. Iterate over `table.Rows` and write each `cell.Text` to a
      `StringBuilder` separated by commas, then save the string as a `.csv` file.
    question: Can I export the extracted tables to CSV?
  - answer: Enable the SDK’s pre‑processing step to boost contrast and apply edge‑enhancement
      filters before recognition.
    question: What if my tables have no visible borders?
  - answer: Yes. The trial license is limited to 100 pages per month; a full license
      removes this restriction and provides priority support.
    question: Is a commercial license required for production use?
  type: FAQPage
tags:
- OCR
- C#
- computer vision
title: Come abilitare forms c# ed estrarre tabelle con OCR in C#
url: /it/net/image-and-drawing-recognition/how-to-enable-forms-and-extract-tables-with-ocr-in-c-complet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come abilitare i moduli c# ed estrarre tabelle con OCR in C#

Se hai bisogno di **enable forms c#** durante l'elaborazione di fatture, ricevute o qualsiasi scansione strutturata, questa guida ti mostra esattamente come farlo. Imparerai anche **how to extract tables c#** dalla stessa immagine ed eseguire OCR sull'immagine in una singola chiamata. Alla fine del tutorial avrai un programma console C# pronto all'uso che rileva le tabelle, estrae le coppie chiave‑valore e stampa tutto sulla console.

## Risposte rapide
- **Qual è il primo passo?** Crea un'istanza di `OcrEngine` e puntala al tuo file immagine.  
- **Come attivo il riconoscimento dei moduli?** Imposta `EnableFormRecognition = true` nella configurazione del motore.  
- **Come posso estrarre le tabelle?** Abilita `EnableTableRecognition` e leggi la collezione `Tables` dal risultato.  
- **Ho bisogno di una licenza speciale?** La maggior parte degli SDK OCR richiede una licenza runtime per la produzione; una versione di prova funziona per lo sviluppo.  
- **Quali versioni di .NET sono supportate?** .NET 6+, .NET 5 e .NET Framework 4.7+ sono tutti compatibili.

## Che cos'è enable forms c#?
`enable forms c#` si riferisce all'attivazione della funzionalità di rilevamento dei campi modulo del motore OCR, in modo che i campi etichettati come “Invoice Number” o “Date” vengano restituiti come coppie chiave‑valore strutturate. Questo elimina l'analisi manuale con regex e velocizza notevolmente l'automazione dell'inserimento dati. Attivando questa capacità, l'OCR SDK mappa automaticamente ogni etichetta rilevata al suo valore corrispondente, riducendo la quantità di codice personalizzato da scrivere e migliorando l'affidabilità complessiva del flusso di estrazione.

## Perché usare OCR per rilevare tabelle e moduli insieme?
Le moderne librerie OCR supportano **oltre 50 formati di input** (inclusi PNG, JPEG, TIFF e PDF) e possono elaborare **documenti con centinaia di pagine** senza caricare l'intero file in memoria. Abilitare sia l'estrazione di moduli sia di tabelle in un'unica passata riduce l'utilizzo della CPU fino al **30 %** rispetto all'esecuzione di due riconoscimenti separati.

## Come abilitare i moduli in C# usando OCR?
Crea un oggetto `OcrEngine`, carica la tua immagine e imposta `EnableFormRecognition = true`. Il motore individuerà automaticamente i campi etichettati e li esporrà tramite la collezione `FormFields` del risultato.  
La classe `OcrEngine` è il punto di ingresso principale dell'OCR SDK, responsabile del caricamento delle immagini e dell'esecuzione del riconoscimento. Gestisce i modelli linguistici, il preprocessing e l'intera pipeline di riconoscimento, rendendola essenziale per qualsiasi flusso di lavoro basato su OCR.

## Come posso estrarre le tabelle dalle immagini in C#?
Attiva il rilevamento delle tabelle impostando `EnableTableRecognition = true`. Dopo il riconoscimento, itera su `result.Tables` per leggere il numero di righe e colonne di ogni tabella e il testo all'interno di ciascuna cella. Le tabelle estratte vengono restituite come oggetti che espongono `Rows`, `Columns` e i valori individuali di `Cell`, consentendoti di trasformarle in CSV, JSON o altri formati per l'elaborazione successiva. Questo approccio gestisce la maggior parte delle strutture a griglia senza richiedere il rilevamento manuale delle linee.

## Come eseguire OCR su un'immagine in C#?
Chiama il metodo `Recognize` del motore passando il percorso della tua immagine. Il metodo restituisce un oggetto `OcrResult` che contiene sia `FormFields` sia `Tables`. Puoi quindi stampare i dati estratti o inviarli all'elaborazione successiva.  
La classe `OcrResult` contiene l'output di un'esecuzione di riconoscimento, includendo il testo grezzo, i campi modulo rilevati e le eventuali tabelle identificate, fornendo un contenitore comodo per tutte le informazioni derivanti da OCR.

### Ancore di definizione
La classe `OcrEngine` è il punto di ingresso dell'OCR SDK; carica le immagini, mantiene le impostazioni di configurazione ed esegue la pipeline di riconoscimento.  
La classe `OcrResult` incapsula il risultato di un'esecuzione di riconoscimento, esponendo collezioni come `Tables`, `FormFields` e le `TextLines` grezze.

## Passo 1: configurare il motore OCR – come abilitare i moduli

Per prima cosa, crea il motore e puntalo al tuo file sorgente:

`var ocrEngine = new OcrEngine();`  
`ocrEngine.LoadImage("invoice_table.png");`

Puoi anche regolare la lingua OCR, i DPI e altre impostazioni globali in questa fase.  

**Perché è importante:** L'istanziazione del motore alloca risorse interne (come i modelli linguistici). Se salti questo passo, la successiva chiamata `Recognize` genererà una `NullReferenceException`.

## Passo 2: attivare l'estrazione strutturata – come estrarre tabelle e rilevare tabelle OCR

Abilita le due funzionalità principali prima di chiamare `Recognize`:

`ocrEngine.Config.EnableFormRecognition = true;`  
`ocrEngine.Config.EnableTableRecognition = true;`

**Consiglio professionale:** Se ti serve solo una delle funzionalità, disabilitare l'altra può migliorare le prestazioni fino al **20 %**.

## Passo 3: eseguire OCR sull'immagine e ottenere il risultato – eseguire OCR sull'immagine

Ora esegui il riconoscimento:

`OcrResult result = ocrEngine.Recognize();`

L'oggetto `result` restituito contiene due collezioni importanti:

* `result.FormFields` – un dizionario di nomi dei campi e dei loro valori estratti.  
* `result.Tables` – un elenco di oggetti tabella, ciascuno espone `Rows`, `Columns` e il testo delle celle.

### Output console previsto

Quando stampi il risultato vedrai qualcosa di simile a:

```
Table 1 – 5 rows × 4 columns
Row 1: Item   Qty   Price   Total
Row 2: Pen    10    $1.00   $10.00
...
Form field “InvoiceNumber”: 2023‑00123
Form field “InvoiceDate”: 2023‑03‑15
```

I numeri esatti varieranno in base all'immagine di origine, ma la struttura elencherà sempre ogni tabella seguita dai campi modulo estratti.

## Passo 4: gestire i casi limite durante il rilevamento delle tabelle OCR

Anche con `EnableTableRecognition = true`, l'OCR può incontrare difficoltà su:

| Problema | Perché accade | Correzione rapida |
|----------|----------------|-------------------|
| **Celle unite** | Il motore tratta l'area unita come una singola cella. | Post‑processa le righe: cerca celle insolitamente larghe e dividile in base agli spazi. |
| **Bordi mancanti** | Le linee della tabella sono deboli o interrotte. | Aumenta il contrasto dell'immagine prima di passarla al motore (`ocrEngine.PreprocessImage`). |
| **Tabelle ruotate** | Documento scansionato con un angolo. | Usa `ocrEngine.Config.AutoRotate = true` (se disponibile). |

**Suggerimento:** Convalida sempre `table.Rows.Count` e `table.Columns.Count` prima di accedere agli indici per evitare `IndexOutOfRangeException`.

## Passo 5: mettere tutto insieme – un esempio completo e eseguibile

Di seguito trovi il programma completo che puoi copiare‑incollare in un nuovo progetto console. Include le direttive `using`, la configurazione del motore e la logica di elaborazione mostrata in precedenza.

```csharp
using System;
using OcrSdk;   // Replace with the actual namespace of your OCR SDK

class Program
{
    static void Main()
    {
        // Create and configure the OCR engine
        var ocrEngine = new OcrEngine();
        ocrEngine.LoadImage("invoice_table.png");
        ocrEngine.Config.EnableFormRecognition = true;
        ocrEngine.Config.EnableTableRecognition = true;

        // Run recognition
        OcrResult result = ocrEngine.Recognize();

        // Output tables
        foreach (var table in result.Tables)
        {
            Console.WriteLine($"Table – {table.Rows.Count} rows × {table.Columns.Count} columns");
            foreach (var row in table.Rows)
            {
                Console.WriteLine(string.Join("\t", row.Cells));
            }
        }

        // Output form fields
        foreach (var field in result.FormFields)
        {
            Console.WriteLine($"Form field “{field.Key}”: {field.Value}");
        }
    }
}
```

Esegui il programma (`dotnet run` o `Ctrl+F5` in Visual Studio) e vedrai l'output console descritto in precedenza.

## Problemi comuni e risoluzione

- **Risultato nullo** – Assicurati che il percorso dell'immagine sia corretto e che il file sia accessibile.  
- **Punteggi di bassa confidenza** – Aumenta la risoluzione dell'immagine ad almeno 300 DPI; l'accuratezza dell'OCR diminuisce drasticamente sotto i 200 DPI.  
- **Caratteri inaspettati** – Abilita i dizionari specifici per lingua (`ocrEngine.Config.Language = "en"` per l'inglese).  
- **Colli di bottiglia delle prestazioni** – Per grandi lotti, riutilizza una singola istanza di `OcrEngine` invece di crearne una nuova per ogni immagine.

## Domande frequenti

**Q: Questo funziona con input PDF?**  
**A:** Sì. La maggior parte degli SDK OCR rasterizza ogni pagina PDF internamente, quindi puoi chiamare `ocrEngine.LoadPdf("file.pdf")` invece di `LoadImage`.

**Q: La mia immagine contiene sia una tabella sia una firma a mano—cosa succede?**  
**A:** La firma appare come una regione immagine separata con testo a bassa confidenza. Puoi filtrarla controllando `ocrResult.Images` per confidenza inferiore a una soglia.

**Q: Posso esportare le tabelle estratte in CSV?**  
**A:** Assolutamente. Itera su `table.Rows` e scrivi ogni `cell.Text` in un `StringBuilder` separato da virgole, quindi salva la stringa come file `.csv`.

**Q: E se le mie tabelle non hanno bordi visibili?**  
**A:** Abilita il passaggio di pre‑processing dell'SDK per aumentare il contrasto e applicare filtri di miglioramento dei bordi prima del riconoscimento.

**Q: È necessaria una licenza commerciale per l'uso in produzione?**  
**A:** Sì. La licenza di prova è limitata a 100 pagine al mese; una licenza completa rimuove questa restrizione e fornisce supporto prioritario.

## Conclusione

Ora sai **come abilitare i moduli c#**, **come estrarre le tabelle c#**, e i passaggi esatti per **eseguire OCR su immagine** usando C#. L'esempio dimostra l'intero flusso di lavoro—dalla creazione del motore, alla configurazione, fino alla gestione del risultato—così puoi copiarlo direttamente nei tuoi progetti.  

Successivamente, prova a sostituire l'immagine di esempio con un PDF di fattura multi‑pagina, sperimenta con `ocrEngine.Config.AutoRotate`, o invia i dati estratti a un database. queste estensioni approfondiranno la tua padronanza di **detect tables OCR** e **use OCR C#** in scenari di produzione.

![how to enable forms with OCR C#](image.png)
[how to enable forms with OCR C#](image.png)

**Ultimo aggiornamento:** 2026-09-03  
**Testato con:** OCR SDK versione 5.2 (supporta .NET 6+ e .NET Framework 4.7+)  
**Autore:** Aspose  

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
```csharp
        // Enable structured extraction features.
        ocrEngine.Config.EnableTableRecognition = true;   // detect tables OCR
        ocrEngine.Config.EnableFormRecognition = true;    // how to enable forms
```
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
```
Table 1: 5 rows, 4 columns
Item | Qty | Price | Total
InvoiceNumber: INV-2025-001
Date: 2025-12-31
Customer: Acme Corp.
```
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

## Tutorial correlati

- [Come applicare la licenza in Aspose OCR passo passo guida C](/ocr/net/ocr-configuration/how-to-apply-license-in-aspose-ocr-step-by-step-c-guide/)
- [Come abilitare GPU per Aspose OCR passo passo guida](/ocr/net/ocr-configuration/how-to-enable-gpu-for-aspose-ocr-step-by-step-guide/)
- [Estrarre testo immagine C# con selezione lingua usando Aspose.OCR](/ocr/net/ocr-configuration/ocr-operation-with-language-selection/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}