---
category: general
date: 2026-04-04
description: Impara come estrarre il testo da file TIFF utilizzando un esempio di
  motore OCR in C#. Guida passo‑passo con output JSON e XML.
draft: false
keywords:
- extract text from tiff
- ocr engine example
- Aspose OCR C#
- multi‑page TIFF OCR
- JSON OCR result
language: it
og_description: Estrai testo da file TIFF usando un motore OCR, esempio in C#. Passaggi
  dettagliati, codice completo e consigli per l'output JSON/XML.
og_title: Estrai il testo da TIFF con il motore OCR di Aspose – Guida completa
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Estrai il testo da TIFF con il motore OCR di Aspose – Esempio completo
url: /it/net/text-recognition/extract-text-from-tiff-with-aspose-ocr-engine-complete-examp/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai testo da TIFF – Esempio completo di motore OCR in C#

Hai mai avuto bisogno di **estrarre testo da TIFF** immagini ma non eri sicuro quale libreria potesse gestire file multi‑pagina senza un circo di soluzioni alternative? Non sei l'unico. In molti sistemi legacy, i documenti arrivano come scansioni TIFF multi‑pagina, e estrarre il testo grezzo è una funzionalità indispensabile per la ricerca, la conformità o l'automazione dell'inserimento dati.

La buona notizia? Con Aspose OCR puoi farlo in poche righe—senza armeggiare con buffer di pixel a basso livello. Questo tutorial ti guida attraverso un **esempio completo di motore OCR** che carica un TIFF multi‑pagina, riconosce ogni pagina e genera sia JSON formattato in modo leggibile che XML opzionale. Alla fine avrai un'app console C# pronta all'uso che estrae testo da file TIFF in pochi secondi.

## Cosa imparerai

- Come configurare il motore Aspose OCR in un progetto .NET.  
- Il codice esatto necessario per **estrarre testo da TIFF** file, inclusa la gestione multi‑pagina.  
- Perché potresti preferire l'output JSON rispetto a XML e come generarli entrambi.  
- Suggerimenti per risolvere problemi comuni (ad esempio, DPI dell'immagine, utilizzo della memoria).  

### Prerequisiti

- .NET 6.0 SDK o successivo (il codice funziona con .NET Core e .NET Framework).  
- Una licenza valida di Aspose OCR (o una chiave di prova gratuita).  
- Visual Studio 2022 o qualsiasi editor C# tu preferisca.  
- Un file TIFF multi‑pagina di esempio (chiamato `multi-page.tiff` nell'esempio).  

> **Consiglio professionale:** Se hai un budget limitato, la prova gratuita ti consente comunque di estrarre testo da fino a 100 pagine al mese—perfetto per i test.

---

## Passo 1 – Inizializzare il motore OCR (esempio del motore OCR)

Prima di poter **estrarre testo da TIFF**, abbiamo bisogno di un'istanza del motore OCR. Questo oggetto contiene tutta la configurazione che potresti modificare in seguito (lingua, risoluzione, ecc.).

```csharp
using Aspose.OCR;
using System.IO;

// Create a new OCR engine – this is the core of our ocr engine example
var ocrEngine = new OcrEngine();

// Optional: set language if you know the document’s language
// ocrEngine.Language = Language.English;
```

*Perché è importante:* La classe `OcrEngine` astrae il lavoro pesante. Istanziare una sola volta e riutilizzarla per più immagini è più efficiente in termini di memoria rispetto a creare un nuovo motore per ogni pagina.

---

## Passo 2 – Caricare il TIFF multi‑pagina (estrarre testo da TIFF)

Ora indirizziamo il motore al nostro file sorgente. `ImageStream.FromFile` supporta TIFF, JPEG, PNG e molti altri, ma per questo tutorial ci concentriamo su TIFF.

```csharp
// Load the multi‑page TIFF you want to process
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/multi-page.tiff");
```

> **Nota:** Sostituisci `YOUR_DIRECTORY` con il percorso reale della cartella sul tuo computer.  
> **Suggerimento:** Se il tuo TIFF ha un DPI basso (inferiore a 150), considera di pre‑processarlo per migliorare l'accuratezza OCR.

---

## Passo 3 – Riconoscere tutte le pagine

Chiamare `Recognize()` esegue l'algoritmo OCR su **ogni pagina** del TIFF. L'oggetto risultato contiene il testo grezzo, i punteggi di confidenza e la segmentazione per pagina.

```csharp
// Run OCR on the loaded image – this extracts text from all pages
var ocrResult = ocrEngine.Recognize();
```

*Cosa ottieni:* `ocrResult` contiene una collezione di oggetti `PageResult`. Il testo di ogni pagina è accessibile tramite `ocrResult.Pages[i].Text`. Il motore fornisce anche i livelli di confidenza, utili per controlli di qualità.

---

## Passo 4 – Salvare i risultati come JSON (e XML opzionale)

La maggior parte delle pipeline moderne preferisce JSON, ma i sistemi legacy utilizzano ancora XML. Ecco come generare entrambi, formattati in modo leggibile.

```csharp
// Convert the recognition result to pretty‑printed JSON
string jsonResult = ocrResult.ToJson(prettyPrint: true);
File.WriteAllText(@"YOUR_DIRECTORY/result.json", jsonResult);

// Optional: also output XML for older workflows
string xmlResult = ocrResult.ToXml();
File.WriteAllText(@"YOUR_DIRECTORY/result.xml", xmlResult);
```

### Esempio di output JSON (troncato)

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Text": "Invoice #12345\nDate: 2024‑03‑15\nTotal: $1,250.00",
      "Confidence": 0.97
    },
    {
      "PageNumber": 2,
      "Text": "Itemized List\n1. Widget A – $500.00\n2. Widget B – $750.00",
      "Confidence": 0.95
    }
  ]
}
```

Il JSON è leggibile dall'uomo, rendendo il debug un gioco da ragazzi. L'XML rispecchia la stessa struttura se ti serve.

---

## Passo 5 – Verificare l'estrazione (estrarre testo da TIFF)

Dopo che i file sono stati scritti, un rapido controllo di coerenza aiuta a garantire che nulla sia andato storto.

```csharp
// Load the JSON back just to confirm it was saved correctly
string loadedJson = File.ReadAllText(@"YOUR_DIRECTORY/result.json");
Console.WriteLine("First 200 characters of JSON output:");
Console.WriteLine(loadedJson.Substring(0, Math.Min(200, loadedJson.Length)));
```

Se vedi stampato lo snippet, hai estratto con successo **testo da TIFF** e lo hai salvato. Da qui puoi inviare il JSON a un indice di ricerca, a un database o a qualsiasi servizio downstream.

---

## Perché usare Aspose OCR per estrarre testo da TIFF?

- **Supporto multi‑pagina pronto all'uso** – nessuna necessità di dividere manualmente il TIFF.  
- **Alta precisione** grazie a modelli proprietari di rete neurale.  
- **Cross‑platform** – funziona su runtime .NET Windows, Linux e macOS.  
- **Formati di output ricchi** (JSON, XML, plain text) che si adattano sia a stack moderni che legacy.  

Se sei ancora indeciso, prova la versione di prova gratuita su un documento di esempio. Noterai la velocità e la semplicità rispetto alle alternative open‑source che spesso richiedono pre‑elaborazione aggiuntiva dell'immagine.

---

## Problemi comuni e come evitarli

| Problema | Sintomo | Soluzione |
|----------|---------|-----------|
| TIFF a bassa risoluzione | Caratteri mancanti, bassa confidenza | Ingrandisci l'immagine a ≥150 DPI prima dell'OCR (`ocrEngine.Image = ImageStream.FromFile(...).Resize(150)` ) |
| Lingua errata | Parole illeggibili, soprattutto per testi non‑inglesi | Imposta `ocrEngine.Language = Language.Spanish` (o la lingua appropriata) prima di `Recognize()` |
| Out‑of‑memory su file enormi | `OutOfMemoryException` | Elabora le pagine in batch: cicla su `ocrEngine.Image.Pages` e chiama `RecognizePage(i)` |
| Licenza non applicata | Filigrana “Evaluation” nell'output | Registra la tua licenza: `License license = new License(); license.SetLicense("Aspose.OCR.lic");` |

---

## Esempio completo funzionante (pronto per copia‑incolla)

Di seguito trovi il programma completo che puoi inserire in un nuovo progetto console. Include tutti gli elementi di cui abbiamo parlato—inizializzazione, caricamento, riconoscimento e salvataggio.

```csharp
using Aspose.OCR;
using System;
using System.IO;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Initialize the OCR engine (ocr engine example)
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // Optional: set license if you have one
            // var license = new License();
            // license.SetLicense("Aspose.OCR.lic");

            // -------------------------------------------------
            // 2️⃣  Load the multi‑page TIFF (extract text from TIFF)
            // -------------------------------------------------
            string tiffPath = @"YOUR_DIRECTORY/multi-page.tiff";
            if (!File.Exists(tiffPath))
            {
                Console.WriteLine($"File not found: {tiffPath}");
                return;
            }

            ocrEngine.Image = ImageStream.FromFile(tiffPath);

            // -------------------------------------------------
            // 3️⃣  Recognize every page
            // -------------------------------------------------
            var ocrResult = ocrEngine.Recognize();

            // -------------------------------------------------
            // 4️⃣  Save JSON (pretty) and optional XML
            // -------------------------------------------------
            string jsonPath = @"YOUR_DIRECTORY/result.json";
            string jsonResult = ocrResult.ToJson(prettyPrint: true);
            File.WriteAllText(jsonPath, jsonResult);
            Console.WriteLine($"JSON saved to {jsonPath}");

            // Optional XML output
            string xmlPath = @"YOUR_DIRECTORY/result.xml";
            string xmlResult = ocrResult.ToXml();
            File.WriteAllText(xmlPath, xmlResult);
            Console.WriteLine($"XML saved to {xmlPath}");

            // -------------------------------------------------
            // 5️⃣  Quick verification (extract text from TIFF)
            // -------------------------------------------------
            string preview = jsonResult.Length > 200 ? jsonResult.Substring(0, 200) + "..." : jsonResult;
            Console.WriteLine("\nPreview of JSON output:");
            Console.WriteLine(preview);
        }
    }
}
```

Salva il file come `Program.cs`, esegui `dotnet run` e osserva la console indicarti dove sono stati salvati JSON e XML. Tutto qui—hai appena completato un **esempio di motore OCR** che estrae testo da TIFF.

---

## Prossimi passi e argomenti correlati

- **Elaborazione batch:** Avvolgi la logica sopra in un ciclo `foreach` per gestire automaticamente decine di file TIFF.  
- **Integrazione ricerca:** Invia il JSON a Elasticsearch o Azure Cognitive Search per abilitare la ricerca full‑text sui documenti scansionati.  
- **Pre‑elaborazione immagine:** Esplora l'API `ImageProcessing` di Aspose per correggere l'inclinazione, rimuovere i punti o regolare il contrasto prima dell'OCR.  
- **Output alternativo:** Usa `ocrResult.ToPlainText()` se ti servono solo stringhe grezze senza metadati.  

Se sei curioso di altri formati immagine, lo stesso schema funziona per PDF (basta cambiare il file sorgente) o PNG. Il punto chiave è che una volta configurato il motore, il resto è una pipeline ripetibile.

---

## Conclusione

Abbiamo illustrato un **esempio completo di motore OCR** che ti permette di **estrarre testo da file TIFF** con Aspose OCR, generando JSON pulito e XML opzionale per qualsiasi flusso di lavoro downstream. Il codice è autonomo, le spiegazioni coprono il “perché” di ogni passaggio

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}