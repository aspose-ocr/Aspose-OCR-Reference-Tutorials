---
date: 2026-04-29
description: Scopri come convertire le immagini in PDF con C# usando Aspose.OCR, salvare
  i risultati OCR multipagina come documenti ed estrarre il testo dalle immagini con
  C#.
keywords:
- convert images to pdf
- extract text from images
- c# ocr library
- convert images to xlsx
- generate pdf from tiff
linktitle: Converti immagini in PDF C# – Salva risultato OCR multipagina
second_title: Aspose.OCR .NET API
title: Converti immagini in PDF C# – Salva risultato OCR multipagina
url: /it/net/ocr-optimization/save-multipage-result-as-document/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Converti immagini in PDF C# – Salva risultato OCR multipagina

## Introduzione

In questo tutorial scoprirai come **convertire immagini in PDF C#** usando la potente libreria **Aspose.OCR** per .NET. Che tu abbia bisogno di **convertire file TIFF scansionati in PDF ricercabili**, estrarre testo dalle immagini per l'analisi dei dati, o generare una cartella di lavoro Excel da un batch di foto, questa guida ti accompagna passo passo con spiegazioni chiare, consigli pratici e raccomandazioni di best practice.

## Risposte rapide
- **Qual è l'argomento di questo tutorial?** Conversione di più immagini in PDF, Docx, Text e Xlsx usando Aspose.OCR in C# e salvataggio del risultato OCR come documento multipagina.  
- **Quali formati di output sono supportati?** Docx, Text, Pdf e Xlsx (puoi anche esportare direttamente in PDF).  
- **È necessaria una licenza?** Una versione di prova gratuita è sufficiente per la valutazione; è necessaria una licenza permanente per la produzione.  
- **Quali versioni di .NET sono compatibili?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.  
- **Posso estrarre il testo durante la conversione?** Sì—usa i risultati OCR per ottenere testo ricercabile prima di salvare.

## Cos'è “convertire immagini in PDF C#”?

Convertire immagini in PDF in C# significa prendere programmaticamente uno o più file bitmap (PNG, JPEG, TIFF, ecc.) e generare un documento PDF che preserva il layout visivo, includendo opzionalmente testo ricercabile tramite OCR. Aspose.OCR fornisce una **libreria c# ocr** che gestisce l'intero processo, compreso il supporto multipagina e il salvataggio diretto nei formati office più diffusi.

## Perché usare Aspose.OCR per questo compito?

- **OCR ad alta precisione** che supporta decine di lingue.  
- **Elaborazione multipagina** – fornisci un'intera cartella di immagini e ottieni un unico PDF ricercabile.  
- **Esportazione diretta** in Docx, Text, Pdf e Xlsx senza necessità di un secondo passaggio di conversione.  
- **Pure .NET** – nessuna dipendenza nativa, funziona su Windows, Linux e ambienti cloud.  

## Prerequisiti

1. Installa Aspose.OCR per .NET. Puoi scaricarlo [qui](https://releases.aspose.com/ocr/net/).  
2. Ottieni una versione di prova gratuita o una licenza acquistata – prendi una prova [qui](https://releases.aspose.com/) o **acquista una** [qui](https://purchase.aspose.com/buy).  
3. Consulta la [documentazione](https://reference.aspose.com/ocr/net/) ufficiale per familiarizzare con l'API.  
4. Unisciti alla community nei [forum di supporto](https://forum.aspose.com/c/ocr/16) per assistenza su eventuali ostacoli.  

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

## Passo 1: Imposta la directory del documento

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

Creare un oggetto `AsposeOcr` ti consente di accedere a tutte le operazioni OCR, incluso il flusso di lavoro **convertire immagini in PDF C#**.

## Passo 3: Riconosci le immagini

```csharp
// Recognize image
List<RecognitionResult> result = api.RecognizeMultipleImages(
    new List<string> { dataDir + "sample.png", dataDir + "sample_bad.png" },
    new RecognitionSettings { }
).ToList();
```

Il metodo `RecognizeMultipleImages` elabora ogni file nella lista e restituisce una collezione di `RecognitionResult`. Puoi fornire un numero qualsiasi di immagini, perfetto per scenari di **conversione di immagini scansionate in PDF**.

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
- **Text** – estrazione di testo semplice per rapida analisi dei dati (**estrarre testo dalle immagini**).  
- **Pdf** – l'output PDF classico, ideale per l'archiviazione.  
- **Xlsx** – rappresentazione in foglio di calcolo per dati tabulari (**convertire immagini in xlsx**).

## Come convertire immagini in PDF C# – Riepilogo passo‑passo

1. **Prepara la cartella** con le immagini che desideri convertire.  
2. **Crea un'istanza `AsposeOcr`** per accedere alle funzioni OCR.  
3. **Chiama `RecognizeMultipleImages`** per ottenere i risultati OCR per ogni file.  
4. **Salva il risultato multipagina** usando `SaveMultipageDocument` nel formato necessario.

## Casi d'uso comuni

- **Archiviazione digitale:** Converti contratti cartacei scansionati in PDF ricercabili.  
- **Automazione dell'inserimento dati:** Estrai testo da ricevute o fatture e inseriscilo in un database.  
- **Elaborazione batch:** Gestisci migliaia di immagini in un unico job con codice minimo.  
- **Genera PDF da TIFF:** Ideale per documenti scansionati ad alta risoluzione che devono rimanere fedeli all'originale.

## Risoluzione dei problemi e consigli

- **Set di immagini grandi:** Elabora le immagini in batch più piccoli per evitare picchi di memoria.  
- **Qualità dell'immagine:** Assicurati che le immagini siano almeno a 300 dpi per una precisione OCR ottimale.  
- **Errori di licenza:** Verifica che il file di licenza sia caricato correttamente prima di chiamare i metodi OCR.  
- **Risultati vuoti:** Se un'immagine non può essere letta, il relativo `RecognitionResult` avrà una proprietà `Text` vuota—controlla valori null o stringhe vuote prima di salvare.  

## Domande frequenti

**Q: Posso convertire immagini in PDF C# senza usare OCR?**  
A: Sì, puoi usare Aspose.PDF o altre librerie per una conversione pura immagine‑a‑PDF, ma l'OCR aggiunge testo ricercabile che rende il PDF molto più utile.

**Q: Come estraggo il testo dalle immagini C# dopo la conversione?**  
A: La lista `result` restituita da `RecognizeMultipleImages` contiene una proprietà `Text` per ogni pagina. Puoi scrivere queste stringhe in un file `.txt` o elaborarle direttamente nella tua applicazione.

**Q: È possibile impostare margini di pagina o orientamento personalizzati?**  
A: Quando salvi in PDF o Docx, puoi modificare il layout del documento tramite le API Aspose.Words o Aspose.PDF prima di chiamare `SaveMultipageDocument`.

**Q: Cosa succede se un'immagine non può essere letta?**  
A: Il motore OCR restituisce un `RecognitionResult` vuoto per quella pagina; puoi rilevarlo e saltare o registrare il file problematico.

**Q: L'API supporta il deployment in cloud?**  
A: Sì, la libreria funziona su qualsiasi runtime .NET, inclusi Azure Functions e AWS Lambda, purché il runtime soddisfi i requisiti di versione.

## Conclusione

Ora disponi di un flusso di lavoro completo e pronto per la produzione per **convertire immagini in PDF C#**, estrarre testo ricercabile e persino generare file Word, testo semplice o Excel da un batch di foto. Sentiti libero di sperimentare con diversi formati di output, regolare le impostazioni OCR per lingue specifiche, o integrare il codice in pipeline di elaborazione documenti più ampie.

---

**Ultimo aggiornamento:** 2026-04-29  
**Testato con:** Aspose.OCR 24.11 per .NET  
**Autore:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}