---
category: general
date: 2026-03-28
description: Scopri come estrarre tabelle dalle immagini con Aspose OCR in C#. Questa
  guida copre come rilevare le tabelle nell'immagine, caricare l'immagine per l'OCR
  ed estrarre le tabelle dai file PNG.
draft: false
keywords:
- how to extract tables
- extract table from image
- detect tables in image
- load image for ocr
- extract tables from png
language: it
og_description: Tutorial passo passo su come estrarre tabelle dalle immagini con Aspose
  OCR in C#. Include codice, spiegazioni e consigli per rilevare le tabelle nei file
  immagine.
og_title: Come estrarre tabelle dalle immagini usando Aspose OCR (C#)
tags:
- Aspose OCR
- C#
- Table Extraction
title: Come estrarre tabelle dalle immagini usando Aspose OCR (C#)
url: /it/net/image-and-drawing-recognition/how-to-extract-tables-from-images-using-aspose-ocr-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come estrarre tabelle da immagini usando Aspose OCR (C#)

Ti sei mai chiesto **come estrarre tabelle** da una fattura scansionata o da uno screenshot di un foglio di calcolo? Non sei l'unico. In molti progetti reali dobbiamo trasformare un'immagine di una tabella in qualcosa su cui poter eseguire query—di solito un CSV o un DataTable. La buona notizia? Aspose OCR lo rende un gioco da ragazzi, e puoi farlo in poche righe di C#.

In questo tutorial percorreremo l'intero processo: dal **caricare l'immagine per OCR**, al **rilevare le tabelle nell'immagine**, e infine **estrarre la tabella dall'immagine** e salvarla come file CSV. Alla fine avrai un'app console pronta all'uso che può **estrarre tabelle da file PNG** (o qualsiasi bitmap supportata) senza alcuna difficoltà.

## Prerequisiti

Prima di iniziare, assicurati di avere:

- .NET 6.0 SDK o versioni successive (il codice funziona anche con .NET Framework)
- Visual Studio 2022 (o qualsiasi IDE tu preferisca)
- Un file di licenza Aspose.OCR per .NET (puoi iniziare con una prova gratuita)
- Un'immagine di esempio contenente una tabella (ad es., `invoice_table.png`)

Se qualcuno di questi elementi ti è sconosciuto, non preoccuparti—installa semplicemente il .NET SDK e scarica il pacchetto NuGet, e sarai pronto a partire.

## Panoramica della soluzione

A livello alto il flusso di lavoro è il seguente:

1. **Caricare l'immagine** che desideri elaborare.
2. **Eseguire il riconoscimento OCR** così il motore sa dove si trova il testo.
3. **Creare un TableExtractor** che analizza i risultati OCR alla ricerca di strutture a griglia.
4. **Estrarre tutte le tabelle rilevate** e scegliere quella di cui hai bisogno.
5. **Salvare la tabella** come CSV (o in qualsiasi altro formato preferisci).

Ogni passaggio è spiegato in dettaglio di seguito, con snippet di codice completi da copiare‑incollare.

<img src="table_extraction_example.png" alt="esempio di come estrarre tabelle da immagine" width="600">

*(L'immagine sopra mostra una tabella di fattura di esempio che estrarremo.)*

## Passo 1 – Caricare l'immagine per OCR

La prima cosa da fare è indicare ad Aspose OCR quale file leggere. La libreria supporta PNG, JPEG, BMP, TIFF e alcuni altri formati. Ecco il codice minimo:

```csharp
using Aspose.OCR;
using System.Drawing;   // Required for Image.FromFile

// ...

// Load the image that contains the table
var ocrEngine = new OcrEngine
{
    Image = Image.FromFile(@"C:\Images\invoice_table.png") // <-- adjust the path
};
```

**Perché è importante:**  
`Image.FromFile` si occupa della decodifica del PNG (o di qualsiasi altro bitmap) in un formato che il motore OCR può comprendere. Se salti questo passaggio o passi un file corrotto, la chiamata successiva a `Recognize()` genererà un'eccezione.

> **Consiglio:** Se lavori con PDF di grandi dimensioni, estrai prima ogni pagina come immagine—altrimenti il motore OCR esaurirà la memoria.

## Passo 2 – Riconoscere la pagina (necessario prima del rilevamento della tabella)

Il riconoscimento converte i dati pixel grezzi in un layout di testo ricercabile. Senza questo passaggio il `TableExtractor` non ha nulla su cui operare.

```csharp
// Perform OCR recognition – this populates internal structures
ocrEngine.Recognize();
```

**Cosa succede dietro le quinte?**  
Aspose OCR esegue un rilevatore di testo basato su rete neurale, poi crea una gerarchia di oggetti `Page`, `Paragraph` e `Word`. Il rilevatore di tabelle esamina successivamente le relazioni spaziali tra quelle parole.

Se elabori molte immagini in un ciclo, considera di riutilizzare la stessa istanza di `OcrEngine` e semplicemente sostituire la proprietà `Image`—questo riduce l'overhead di allocazione.

## Passo 3 – Creare un TableExtractor e rilevare le tabelle nell'immagine

Ora che i dati OCR esistono, possiamo chiedere ad Aspose di trovare le tabelle. La classe `TableExtractor` fa esattamente questo.

```csharp
using Aspose.OCR.Table;

// ...

// Initialize the TableExtractor with the recognized engine
var tableExtractor = new TableExtractor(ocrEngine);

// Extract all tables detected on the page
List<Table> extractedTables = tableExtractor.ExtractAll();
```

**Perché usare `ExtractAll()`?**  
Un'unica immagine può contenere più tabelle (pensa a un report a più sezioni). `ExtractAll()` restituisce una `List<Table>` così puoi iterare, scegliere quella giusta, o addirittura unirle in seguito.

Se ti serve solo la prima tabella, puoi usare tranquillamente `extractedTables[0]`, ma proteggi sempre contro una lista vuota per evitare `IndexOutOfRangeException`.

```csharp
if (extractedTables.Count == 0)
{
    Console.WriteLine("No tables were detected. Check the image quality or try adjusting OCR settings.");
    return;
}
```

## Passo 4 – Salvare la tabella estratta come CSV (o qualsiasi altro formato)

Aspose rende l'esportazione banale. La classe `Table` dispone di metodi integrati `SaveCsv`, `SaveXls` e `SaveJson`. Ecco come scrivere un file CSV:

```csharp
// Save the first detected table to CSV
string outputPath = @"C:\Output\invoice_table.csv";
extractedTables[0].SaveCsv(outputPath);

Console.WriteLine($"Table extraction completed. CSV saved to {outputPath}");
```

**Come appare il CSV?**  
Supponendo che l'immagine di origine contenesse una griglia 4 × 3, il CSV potrebbe risultare così:

```
Item,Quantity,Price
Widget A,2,19.99
Widget B,5,9.50
Service C,1,150.00
```

Puoi aprire questo file in Excel, Power BI, o alimentarlo direttamente nel tuo flusso di dati.

## Esempio completo end‑to‑end

Di seguito trovi il programma completo, autonomo. Copialo in un nuovo progetto console (`dotnet new console`) ed eseguilo. Assicurati che il pacchetto NuGet `Aspose.OCR` sia installato (`dotnet add package Aspose.OCR`).

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;          // For Image
using Aspose.OCR;
using Aspose.OCR.Table;

namespace TableExtractTutorial
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Load the image that contains the table
            // -------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                Image = Image.FromFile(@"C:\Images\invoice_table.png")
            };

            // -------------------------------------------------
            // Step 2: Recognize the page (required before table detection)
            // -------------------------------------------------
            ocrEngine.Recognize();

            // -------------------------------------------------
            // Step 3: Create a TableExtractor and detect tables
            // -------------------------------------------------
            var tableExtractor = new TableExtractor(ocrEngine);
            List<Table> extractedTables = tableExtractor.ExtractAll();

            // Guard against no tables found
            if (extractedTables.Count == 0)
            {
                Console.WriteLine("No tables detected. Verify image quality or OCR settings.");
                return;
            }

            // -------------------------------------------------
            // Step 4: Save the first extracted table as CSV
            // -------------------------------------------------
            string csvPath = @"C:\Output\invoice_table.csv";
            extractedTables[0].SaveCsv(csvPath);

            Console.WriteLine($"Table extraction completed. CSV saved at: {csvPath}");
        }
    }
}
```

### Output previsto

Quando esegui il programma dovresti vedere qualcosa di simile:

```
Table extraction completed. CSV saved at: C:\Output\invoice_table.csv
```

Apri `invoice_table.csv` e troverai le righe e le colonne che rispecchiano l'immagine originale.

## Domande frequenti e casi particolari

### E se l'immagine è un JPEG invece di PNG?

Lo stesso codice funziona—basta cambiare l'estensione del file in `Image.FromFile`. Aspose OCR rileva automaticamente il formato, quindi **estrarre tabelle da png** non è un requisito rigido; funziona con qualsiasi bitmap supportata.

### La mia tabella ha celle unite. Verranno preservate?

Le celle unite vengono trattate come colonne separate nell'output CSV perché il CSV non supporta l'unione. Se ti serve una formattazione più ricca (ad es., Excel con celle unite), usa `SaveXls` invece:

```csharp
extractedTables[0].SaveXls(@"C:\Output\invoice_table.xls");
```

### Il rilevamento ha saltato una colonna. Come posso migliorare l'accuratezza?

- Aumenta la risoluzione dell'immagine (≥300 dpi è l'ideale).
- Pre‑elabora l'immagine: converti in scala di grigi, aumenta il contrasto o applica un filtro di deskew.
- Regola le impostazioni di Aspose OCR come `PageSegMode` o `Language` se la tabella contiene caratteri non latini.

### Posso estrarre tabelle direttamente da un PDF?

Sì. Converti prima ogni pagina PDF in immagine (usando `Aspose.PDF` o qualsiasi libreria PDF‑to‑image), poi passa quelle immagini nello stesso flusso di lavoro.

## Consigli per implementazioni pronte per la produzione

1. **Avvolgi l'OCR in try/catch** – ambienti con licenza di rete possono lanciare eccezioni di licenza.
2. **Dispose degli oggetti `Image`** – utilizza blocchi `using` per liberare le risorse native.
3. **Registra i punteggi di confidenza** – `TableExtractor` espone `Table.Confidence` che puoi salvare per il monitoraggio della qualità.
4. **Elaborazione batch** – quando gestisci centinaia di fatture, parallelizza le chiamate OCR ma rispetta le linee guida di thread‑safety della licenza.

## Prossimi passi

Ora che sai **come estrarre tabelle** da immagini, potresti voler esplorare:

- **Rilevare tabelle in video** (usando `TableExtractor` di Aspose su ogni frame).
- **Caricare l'immagine per OCR** da una Web API, abilitando servizi di estrazione tabelle basati su cloud.
- **Estrarre tabelle da PNG** memorizzati in Azure Blob Storage, integrandoli con Azure Functions per elaborazione serverless.

Sentiti libero di sperimentare con formati di file diversi, modificare le impostazioni OCR, o inviare direttamente l'output CSV a un database. Il cielo è il limite.

---

*Buona programmazione! Se incontri difficoltà o hai idee per miglioramenti, lascia un commento qui sotto. Troveremo una soluzione insieme.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}