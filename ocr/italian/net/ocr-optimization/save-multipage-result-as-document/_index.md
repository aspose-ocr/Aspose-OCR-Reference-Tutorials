---
date: 2026-04-23
description: Scopri come convertire le immagini in PDF con C# usando Aspose.OCR, salvare
  i risultati OCR multipagina come documenti ed estrarre il testo dalle immagini.
keywords:
- extract text from images
- batch image to pdf
- convert scanned images pdf
linktitle: Converti immagini in PDF C# – Salva risultato OCR multipagina
second_title: Aspose.OCR .NET API
title: Estrai testo dalle immagini – Converti immagini in PDF C#
url: /it/net/ocr-optimization/save-multipage-result-as-document/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai testo dalle immagini – Converti immagini in PDF C#

## Introduzione

In questo tutorial scoprirai come **estrarre testo dalle immagini** mentre **converti immagini in PDF C#** usando Aspose.OCR per .NET, e poi salvare il risultato OCR multipagina come documento. Che tu abbia bisogno di **batch image to pdf** per l'archiviazione, **convert scanned images pdf** per la conformità, o semplicemente estrarre testo ricercabile dalle foto, ti guideremo passo passo con spiegazioni chiare, consigli pratici e raccomandazioni di best practice.

## Risposte rapide
- **Di cosa tratta questo tutorial?** Converting multiple images to PDF/Docx/Txt/Xlsx and extracting text from images with Aspose.OCR in C#.
- **Quali formati di output sono supportati?** Docx, Text, Pdf, and Xlsx (you can also output PDF directly).
- **Ho bisogno di una licenza?** A free trial works for evaluation; a permanent license is required for production.
- **Quali versioni .NET sono compatibili?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
- **Posso estrarre testo durante la conversione?** Yes—use the OCR results to pull text before saving.

## Cos'è “estrarre testo dalle immagini” e perché combinarlo con la conversione PDF?

Estrarre testo dalle immagini significa utilizzare l'OCR (Optical Character Recognition) per trasformare i caratteri visivi in stringhe ricercabili e modificabili. Quando **converti immagini in PDF C#**, inserisci queste stringhe nel PDF in modo che il documento diventi ricercabile e indicizzabile—perfetto per l'archiviazione digitale e l'analisi dei dati.

## Perché usare Aspose.OCR per questo compito?

- **Alta precisione** in decine di lingue.  
- **Supporto multipagina** – gestisci batch di immagini in una singola chiamata (ideale per **batch image to pdf** scenari).  
- **Salvataggio diretto** in formati Office popolari senza passaggi di conversione aggiuntivi.  
- **Integrazione completa .NET** – nessuna dipendenza nativa, funziona su Windows, Linux e ambienti cloud.

## Prerequisiti

Prima di immergerci, assicurati di avere:

1. Installato Aspose.OCR per .NET. Puoi scaricarlo [qui](https://releases.aspose.com/ocr/net/).  
2. Ottenuta una prova gratuita o una licenza acquistata – ottieni una prova [qui](https://releases.aspose.com/) o acquista una licenza [qui](https://purchase.aspose.com/buy).  
3. Consultata la [documentazione](https://reference.aspose.com/ocr/net/) ufficiale per familiarizzare con le API.  
4. Unito alla community sui [forum di supporto](https://forum.aspose.com/c/ocr/16) per assistenza su eventuali problemi.  

Ora che tutto è pronto, iniziamo a programmare.

## Importa spazi dei nomi

Inizia aggiungendo gli spazi dei nomi richiesti al tuo file C#:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using Aspose.OCR;
```

Queste importazioni ti danno accesso a collezioni, gestione dei file, LINQ e alle classi Aspose OCR.

## Passo 1: Imposta la directory dei documenti

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

Sostituisci `"Your Document Directory"` con il percorso assoluto o relativo dove si trovano le tue immagini di origine e dove desideri salvare i file di output.

## Passo 2: Inizializza Aspose.OCR

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

Creare un oggetto `AsposeOcr` ti dà accesso a tutte le operazioni OCR, incluso il flusso di lavoro **converti immagini in PDF C#**.

## Passo 3: Riconosci le immagini

```csharp
// Recognize image
List<RecognitionResult> result = api.RecognizeMultipleImages(
    new List<string> { dataDir + "sample.png", dataDir + "sample_bad.png" },
    new RecognitionSettings { }
).ToList();
```

Il metodo `RecognizeMultipleImages` elabora ogni file nella lista e restituisce una collezione di `RecognitionResult`. Puoi fornire un numero qualsiasi di immagini, il che è perfetto per scenari **convert scanned images pdf**.

## Passo 4: Salva i risultati nei formati preferiti

```csharp
// Save the result in your preferred format
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR()+"sample.docx", SaveFormat.Docx, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx, result);
```

Scegli il formato che meglio si adatta al tuo flusso di lavoro a valle:

- **Docx** – documento Word modificabile con testo ricercabile.  
- **Text** – estrazione di testo semplice per rapida analisi dei dati (**extract text from images**).  
- **Pdf** – l'output PDF classico, ideale per l'archiviazione.  
- **Xlsx** – rappresentazione in foglio di calcolo per dati tabulari.

## Casi d'uso comuni

- **Digital archiving:** Converti contratti cartacei scansionati in PDF ricercabili.  
- **Data entry automation:** Estrai testo da ricevute o fatture e inseriscilo in un database.  
- **Batch processing:** Gestisci migliaia di immagini in un unico lavoro con codice minimo—perfetto per le esigenze **batch image to pdf**.

## Risoluzione dei problemi e consigli

- **Large image sets:** Elabora le immagini in batch più piccoli per evitare picchi di memoria.  
- **Image quality:** Assicurati che le immagini siano almeno a 300 dpi per una precisione OCR ottimale.  
- **License errors:** Verifica che il file di licenza sia caricato correttamente prima di chiamare i metodi OCR.  
- **Empty results:** Il motore OCR restituisce un `RecognitionResult` vuoto per le pagine illeggibili; controlla `result[i].Text` per valori null o stringhe vuote e gestiscilo di conseguenza.

## Domande frequenti

**Q: Posso convertire immagini in PDF C# senza usare OCR?**  
A: Yes, you can use Aspose.PDF or other libraries for pure image‑to‑PDF conversion, but OCR adds searchable text.

**Q: Come estraggo testo dalle immagini C# dopo la conversione?**  
A: The `result` list returned by `RecognizeMultipleImages` contains `Text` properties you can write to a `.txt` file or process directly.

**Q: È possibile impostare margini di pagina o orientamento personalizzati?**  
A: When saving to PDF or Docx, you can modify the document layout via Aspose.Words or Aspose.PDF APIs before calling `SaveMultipageDocument`.

**Q: Cosa succede se un'immagine non può essere letta?**  
A: The OCR engine returns an empty `RecognitionResult` for that page; you can check `result[i].Text` for null or empty strings and handle accordingly.

**Q: L'API supporta il deployment su cloud?**  
A: Yes, the library works on any .NET runtime, including Azure Functions and AWS Lambda, as long as the runtime meets the version requirements.

---

**Ultimo aggiornamento:** 2026-04-23  
**Testato con:** Aspose.OCR 24.11 for .NET  
**Autore:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}