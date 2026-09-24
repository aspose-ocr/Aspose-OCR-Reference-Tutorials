---
description: Scopri come salvare i risultati OCR con Aspose.OCR per .NET – converti
  l'immagine in PDF, estrai il testo da PNG e salva il testo riconosciuto in DOCX,
  TXT, PDF o XLSX.
linktitle: How to Save OCR Result as Document
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

In questo tutorial scoprirai **come salvare OCR** l'output utilizzando Aspose.OCR per .NET. Ti guideremo attraverso il riconoscimento del testo in un'immagine, per poi convertire quel testo nei formati di documento più popolari come DOCX, TXT, PDF e XLSX. Alla fine, sarai in grado di automatizzare l'estrazione dei dati dalle immagini e memorizzarli come file ricercabili e modificabili—perfetti per l'archiviazione, la creazione di report o l'elaborazione successiva.

## Risposte rapide
- **Cosa significa “come salvare ocr”?** Si riferisce al persistere del testo riconosciuto da un'immagine in un formato file come DOCX, PDF, ecc.  
- **In quali formati posso esportare?** DOCX, TXT, PDF e XLSX sono supportati subito.  
- **È necessaria una licenza?** Una prova gratuita è sufficiente per la valutazione; è richiesta una licenza commerciale per l'uso in produzione.  
- **Posso convertire direttamente l'immagine in PDF?** Sì—salva il risultato OCR come PDF per ottenere un documento PDF ricercabile.  
- **Il PNG è supportato?** Assolutamente; puoi **estrarre testo da PNG** con la stessa API.

## Cos'è l'OCR e perché salvare i risultati come documenti?

L'Optical Character Recognition (OCR) trasforma il testo stampato o scritto a mano presente nelle immagini in stringhe leggibili dalla macchina. Salvare queste stringhe come documenti ti permette di:

* Creare PDF ricercabili per la conformità.  
* Popolare fogli di calcolo (XLSX) per l'analisi dei dati.  
* Generare report modificabili (DOCX).  
* Archiviare log di testo semplice (TXT) per ricerche rapide.

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

Imposta il percorso della tua directory di lavoro e crea un'istanza del motore OCR.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### Passo 2: Riconoscere l'immagine

Passa il file immagine (ad esempio un PNG) al riconoscitore. È qui che **riconosciamo immagini di testo** e le trasformiamo in un `RecognitionResult`.

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

### Passo 3: Salvare il risultato in formati diversi

Ora esportiamo il testo riconosciuto. Scegli il formato che si adatta al tuo flusso di lavoro—che tu debba **convertire immagine in PDF**, **estrarre testo da PNG**, o generare un foglio di calcolo.

```csharp
// Save the result in your preferred format
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

### Passo 4: Visualizzare il messaggio di successo

Un semplice messaggio nella console conferma che il processo è terminato senza errori.

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

## Problemi comuni e suggerimenti

- **Percorsi dei file:** Usa sempre percorsi assoluti o assicurati che `dataDir` termini con un separatore di percorso (`\` o `/`).  
- **Qualità dell'immagine:** Immagini ad alta risoluzione migliorano l'accuratezza; considera la pre‑elaborazione (raddrizzamento, riduzione del rumore) per risultati migliori.  
- **Modalità licenza:** In modalità valutazione l'output può contenere una filigrana; applica una licenza valida per rimuoverla.

## Domande frequenti

**D1. Aspose.OCR è compatibile con diversi formati immagine?**  
R1: Sì, Aspose.OCR supporta un'ampia gamma di formati immagine, garantendo flessibilità nelle tue attività OCR.

**D2: Posso personalizzare le impostazioni di riconoscimento per una migliore accuratezza?**  
R2: Assolutamente! Aspose.OCR fornisce `RecognitionSettings` per affinare il processo OCR in base alle tue esigenze specifiche.

**D3: È disponibile una prova gratuita?**  
R3: Sì, puoi iniziare con una prova gratuita **[qui](https://releases.aspose.com/)**.

**D4: Come posso ottenere una licenza temporanea per Aspose.OCR?**  
R4: Le licenze temporanee possono essere ottenute **[qui](https://purchase.aspose.com/temporary-license/)**.

**D5: Dove posso trovare supporto o entrare in contatto con la community?**  
R5: Unisciti alla community Aspose.OCR su **[Aspose Forum](https://forum.aspose.com/c/ocr/16)** per supporto e discussioni.

---

**Ultimo aggiornamento:** 2026-02-12  
**Testato con:** Aspose.OCR 24.11 per .NET  
**Autore:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}