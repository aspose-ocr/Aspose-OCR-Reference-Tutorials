---
date: 2026-06-29
description: Scopri come salvare i risultati OCR con Aspose.OCR per .NET – una guida
  passo‑passo su come salvare l'output OCR, convertire l'immagine in PDF ricercabile,
  estrarre testo da PNG e esportare in DOCX, TXT, PDF o XLSX.
keywords:
- how to save ocr
- image to searchable pdf
- extract text from png
- create searchable pdf
- ocr result to txt
linktitle: Come salvare il risultato OCR come documento
schemas:
- author: Aspose
  dateModified: '2026-06-29'
  description: Learn how to save OCR results with Aspose.OCR for .NET – a step‑by‑step
    guide on how to save ocr output, convert image to searchable pdf, extract text
    from png, and export to DOCX, TXT, PDF, or XLSX.
  headline: How to Save OCR Result as Document
  type: TechArticle
- description: Learn how to save OCR results with Aspose.OCR for .NET – a step‑by‑step
    guide on how to save ocr output, convert image to searchable pdf, extract text
    from png, and export to DOCX, TXT, PDF, or XLSX.
  name: How to Save OCR Result as Document
  steps:
  - name: Initialize Aspose.OCR
    text: AsposeOcr is the primary class that performs OCR operations. Set the path
      to your working directory and create an instance of the OCR engine.
  - name: Recognize Image
    text: RecognitionResult holds the text and layout information extracted from the
      image. Pass the image file (e.g., a PNG) to the recognizer. This is where we
      **recognize text images** and turn them into a `RecognitionResult`.
  - name: Save Result in Different Formats
    text: Now we export the recognized text. Choose the format that fits your workflow—whether
      you need to **convert image to searchable pdf**, **extract text from png**,
      or generate a spreadsheet.
  - name: Display Success Message
    text: A simple console message confirms that the process completed without errors.
  type: HowTo
- questions:
  - answer: It refers to persisting the text recognized from an image into a file
      format like DOCX, PDF, etc.
    question: What does “how to save ocr” mean?
  - answer: DOCX, TXT, PDF, and XLSX are supported out‑of‑the‑box.
    question: Which formats can I export to?
  - answer: A free trial works for evaluation; a commercial license is required for
      production use.
    question: Do I need a license?
  - answer: Yes—save the OCR result as PDF to get a searchable PDF document.
    question: Can I convert image to PDF directly?
  - answer: Absolutely; you can **extract text from PNG** images with the same API.
    question: Is PNG supported?
  type: FAQPage
second_title: Aspose.OCR .NET API
title: Come salvare il risultato OCR come documento
url: /it/net/ocr-settings/save-result-as-document/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come salvare il risultato OCR come documento

## Introduzione

In questo tutorial scoprirai **come salvare l'OCR** utilizzando Aspose.OCR per .NET. Ti guideremo nel riconoscimento del testo in un'immagine, quindi nella conversione di quel testo nei formati di documento più popolari come DOCX, TXT, PDF e XLSX. Alla fine, sarai in grado di automatizzare l'estrazione dei dati dalle immagini e archiviarli come file ricercabili e modificabili—perfetti per l'archiviazione, la creazione di report o l'elaborazione successiva.

## Risposte rapide
- **Cosa significa “come salvare l'OCR”?** Si riferisce al persistere del testo riconosciuto da un'immagine in un formato file come DOCX, PDF, ecc.  
- **Quali formati posso esportare?** DOCX, TXT, PDF e XLSX sono supportati subito.  
- **Ho bisogno di una licenza?** Una versione di prova gratuita è sufficiente per la valutazione; è necessaria una licenza commerciale per l'uso in produzione.  
- **Posso convertire direttamente l'immagine in PDF?** Sì—salva il risultato OCR come PDF per ottenere un documento PDF ricercabile.  
- **Il PNG è supportato?** Assolutamente; puoi **estrarre testo da immagini PNG** con la stessa API.

## Cos'è l'OCR e perché salvare i risultati come documenti?

L'OCR (Optical Character Recognition) converte il testo stampato o scritto a mano presente nelle immagini in stringhe leggibili da macchina. Salvare queste stringhe come documenti ti consente di creare **PDF ricercabili**, popolare fogli di calcolo, generare report modificabili o archiviare log di testo semplice. Aspose.OCR può trasformare un'immagine scansionata in un **PDF ricercabile** in un unico passaggio, eliminando la necessità di strumenti separati per la creazione di PDF.

## Prerequisiti

Prima di iniziare, assicurati di avere:

- Aspose.OCR per .NET installato. Puoi scaricarlo **[qui](https://releases.aspose.com/ocr/net/)**.  
- Una cartella sul tuo computer che conterrà le immagini di origine e i documenti di output. Aggiorna la variabile `dataDir` nel codice per puntare a questa cartella.

## Importare gli spazi dei nomi

Abbiamo bisogno di alcuni spazi dei nomi .NET per accedere a I/O file e alle classi Aspose OCR.

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

### Passo 1: Inizializzare Aspose.OCR

AsposeOcr è la classe principale che esegue le operazioni OCR. Imposta il percorso della tua directory di lavoro e crea un'istanza del motore OCR.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### Passo 2: Riconoscere l'immagine

`RecognitionResult` contiene il testo e le informazioni di layout estratte dall'immagine. Passa il file immagine (ad es., un PNG) al riconoscitore. Qui è dove **riconosciamo le immagini di testo** e le trasformiamo in un `RecognitionResult`.

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

### Passo 3: Salvare il risultato in diversi formati

Ora esportiamo il testo riconosciuto. Scegli il formato che si adatta al tuo flusso di lavoro—che tu abbia bisogno di **convertire l'immagine in PDF ricercabile**, **estrarre testo da PNG**, o generare un foglio di calcolo.

```csharp
// Save the result in your preferred format
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

### Passo 4: Visualizzare il messaggio di successo

Un semplice messaggio sulla console conferma che il processo è terminato senza errori.

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

## Problemi comuni e consigli

- **Percorsi dei file:** Usa sempre percorsi assoluti o assicurati che `dataDir` termini con un separatore di percorso (`\` o `/`).  
- **Qualità dell'immagine:** Immagini ad alta risoluzione migliorano l'accuratezza; considera la pre‑elaborazione (raddrizzamento, riduzione del rumore) per risultati migliori.  
- **Modalità licenza:** In modalità di valutazione l'output può contenere una filigrana; applica una licenza valida per rimuoverla.

## Domande frequenti

**Q1. Aspose.OCR è compatibile con diversi formati immagine?**  
A1: Sì, Aspose.OCR supporta oltre 30 formati immagine—incluse PNG, JPEG, TIFF, BMP e GIF—garantendo flessibilità nelle tue attività OCR.

**Q2: Posso personalizzare le impostazioni di riconoscimento per una migliore accuratezza?**  
A2: Assolutamente! Aspose.OCR fornisce `RecognitionSettings` per affinare il processo OCR secondo le tue esigenze specifiche.

**Q3: È disponibile una versione di prova gratuita?**  
A3: Sì, puoi iniziare con una versione di prova gratuita **[qui](https://releases.aspose.com/)**.

**Q4: Come posso ottenere una licenza temporanea per Aspose.OCR?**  
A4: Le licenze temporanee possono essere ottenute **[qui](https://purchase.aspose.com/temporary-license/)**.

**Q5: Dove posso cercare aiuto o entrare in contatto con la community?**  
A5: Unisciti alla community di Aspose.OCR su **[Aspose Forum](https://forum.aspose.com/c/ocr/16)** per supporto e discussioni.

---

**Ultimo aggiornamento:** 2026-06-29  
**Testato con:** Aspose.OCR 24.11 per .NET  
**Autore:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Tutorial correlati

- [Estrai testo da immagine usando Aspose.OCR .NET](/ocr/net/image-and-drawing-recognition/)
- [Converti immagini in PDF C# – Salva risultato OCR multipagina](/ocr/net/ocr-optimization/save-multipage-result-as-document/)
- [Estrai immagini di testo – Impostazioni OCR](/ocr/net/ocr-settings/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}