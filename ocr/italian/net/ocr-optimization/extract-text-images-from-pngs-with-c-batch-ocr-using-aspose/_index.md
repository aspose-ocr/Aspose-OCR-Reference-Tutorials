---
category: general
date: 2026-02-09
description: Estrarre rapidamente il testo dalle immagini con C# impostando il massimo
  parallelismo per l'OCR batch – impara a convertire pagine scannerizzate, gestire
  OCR su più immagini e leggere il testo dei PNG in modo efficiente.
draft: false
keywords:
- extract text images
- set max parallelism
- convert scanned pages
- multiple image ocr
- read png text
language: it
og_description: Estrai il testo dalle immagini in C# impostando il massimo parallelismo.
  Questo tutorial mostra come convertire pagine scannerizzate, eseguire OCR su più
  immagini e leggere il testo PNG con Aspose OCR.
og_title: Estrarre testo dalle immagini PNG con C# – Guida completa all'OCR batch
tags:
- OCR
- C#
- Aspose
- Batch Processing
title: Estrai testo dalle immagini PNG con C# – OCR batch con Aspose OCR
url: /it/net/ocr-optimization/extract-text-images-from-pngs-with-c-batch-ocr-using-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# estrarre immagini di testo da PNG con C# – OCR batch usando Aspose OCR

Hai mai avuto bisogno di **estrarre immagini di testo** da una cartella di PNG scansionati ma ti sei sentito bloccato dalla domanda “come posso renderlo veloce?”? Non sei solo. In molti progetti reali, gli sviluppatori devono **impostare il massimo parallelismo** in modo che decine di pagine vengano elaborate in secondi anziché minuti.  

In questa guida percorreremo un esempio completo e eseguibile che **converte pagine scansionate**, esegue **OCR multiplo di immagini** e infine **legge il testo PNG** senza alcuno sforzo. Niente link vaghi tipo “vedi la documentazione”—solo codice pronto da copiare‑incollare, spiegazioni sul perché ogni riga è importante e consigli per evitare le solite insidie.

> **Pro tip:** Se stai già usando Aspose OCR altrove, noterai che la stessa classe `OcrEngine` compare qui, ma ne modificheremo la configurazione per un vero processamento parallelo.

---

## Cosa ti serve

- **.NET 6+** (o .NET Framework 4.6+). L'API funziona allo stesso modo, ma i runtime più recenti offrono una migliore gestione dei thread.  
- **Aspose.OCR for .NET** – installa via NuGet: `Install-Package Aspose.OCR`.  
- Una cartella che contiene alcuni PNG scansionati (`page1.png`, `page2.png`, …).  
- Un IDE o editor con cui ti trovi a tuo agio (Visual Studio, Rider, VS Code…).

È tutto. Nessun servizio aggiuntivo, nessuna chiave cloud, solo elaborazione locale pura.

---

## estrarre immagini di testo – Impostare il Max Parallelism per OCR batch

Quando avvii l'OCR su diversi file, il motore, per impostazione predefinita, utilizza un singolo thread. È sicuro ma terribilmente lento. Configurando `MaxDegreeOfParallelism` indichi al motore quante thread può avviare contemporaneamente.

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };
```

**Perché 4?**  
Quattro è un punto di equilibrio sulla maggior parte dei laptop moderni—basti pochi core per tenere occupata la CPU, ma non così tanti da soffocare gli altri processi. Se esegui questo su un server con 16 core, alza il valore a 12 o 14 per notare un miglioramento significativo della velocità.

---

## Convertire pagine scansionate – Costruire la collezione di Image Stream

Aspose si aspetta ogni immagine come un `ImageStream`. L'helper `FromFile` legge il file, lo mantiene in memoria e lo passa al motore OCR. Puoi anche fornire un `MemoryStream` se le tue immagini provengono da un database o da una risposta HTTP.

```csharp
        // 2️⃣ Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };
```

**Caso limite:** Se qualche file è mancante o corrotto, `FromFile` lancerà una `FileNotFoundException`. Avvolgi la costruzione in un `try/catch` se ti aspetti input inaffidabili.

---

## OCR multiplo di immagini – Eseguire OCR batch

Ora avviene il lavoro pesante. `RecognizeBatch` avvia fino al numero di thread impostato in precedenza, elabora ogni immagine e restituisce una lista di oggetti `OcrResult`.

```csharp
        // 3️⃣ Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

Dietro le quinte, ogni thread carica la sua immagine, esegue la rete neurale e estrae il testo semplice. L'ordine dei risultati corrisponde all'ordine della lista di input, così puoi mappare in sicurezza pagina 1 → risultato 0, e così via.

---

## leggere testo png – Visualizzare il contenuto estratto

Infine cicliamo sui risultati e stampiamo il testo semplice sulla console. Qui puoi reindirizzare l'output a un file, a un database o anche a un servizio NLP a valle.

```csharp
        // 4️⃣ Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

### Output atteso della console

```
--- Page 1 ---
This is the first scanned line of text.
Another line appears here.

--- Page 2 ---
Second page starts with a header.
More content follows…

--- Page 3 ---
Final page ends with a signature.
```

Se vedi sezioni vuote, verifica che i PNG non siano immagini completamente bianche—l'OCR ha bisogno di un po' di contrasto.

---

## Consigli pratici e problemi comuni

| Situation | What to Do |
|-----------|------------|
| **Memory pressure** on large batches | Process images in chunks of 10‑20 files, then call `GC.Collect()` if you notice spikes. |
| **Incorrect language detection** | Set `ocrEngine.Configuration.Language = OcrLanguage.English;` (or your target language) before calling `RecognizeBatch`. |
| **Slow performance despite parallelism** | Verify that your SSD isn’t throttling I/O; read all files into memory first (as we do with `ImageStream.FromFile`). |
| **Missing characters** | Increase `ocrEngine.Configuration.DPI = 300;` for higher‑resolution processing. |

---

## Estendere l'esempio – Da PNG a PDF o DOCX

Se in futuro devi **convertire pagine scansionate** in PDF ricercabili, basta fornire lo stesso `ocrResults[i].PlainText` a una libreria PDF (ad esempio Aspose.PDF) e sovrapporre il testo come livello invisibile. Anche lì funziona lo stesso trucco di parallelismo.

---

## Codice sorgente completo (pronto per copia‑incolla)

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };

        // Step 2: Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };

        // Step 3: Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Step 4: Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

Salva questo file come `BatchExample.cs`, esegui `dotnet run` e osserva la console riempirsi del testo che prima era nascosto dentro quei PNG scansionati.

---

## Riepilogo visivo

![extract text images example](images/ocr-batch.png){alt="extract text images example"}

Il diagramma mostra il flusso: **File PNG → Collezione ImageStream → OcrEngine (max parallelism) → Risultati OCR → Console / archiviazione a valle**.

---

## Conclusione

Ora disponi di una ricetta solida, end‑to‑end, per **estrarre immagini di testo** in C# impostando il **max parallelism**, **convertendo pagine scansionate**, gestendo **OCR multiplo di immagini** e **leggendo testo PNG** in modo efficiente. Il codice è autonomo, le spiegazioni coprono sia il “come” sia il “perché”, e i consigli ti evitano le comuni seccature.

Qual è il prossimo passo? Prova a sostituire l'elenco statico di PNG con un ciclo dinamico `Directory.GetFiles`, sperimenta con diversi conteggi di thread, o invia l'output a un PDF ricercabile. Lo stesso schema scala a centinaia di pagine con quasi nessuna riga di codice aggiuntivo.

Hai domande o un caso limite difficile? Lascia un commento qui sotto, e buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}