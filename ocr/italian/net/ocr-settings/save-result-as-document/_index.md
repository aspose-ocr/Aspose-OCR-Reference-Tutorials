---
title: Salva risultato come documento nel riconoscimento immagine OCR
linktitle: Salva risultato come documento nel riconoscimento immagine OCR
second_title: API Aspose.OCR .NET
description: Sblocca il potenziale di Aspose.OCR per .NET. Riconosci facilmente il testo nelle immagini e salva i risultati in vari formati di documenti.
weight: 10
url: /it/net/ocr-settings/save-result-as-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Salva risultato come documento nel riconoscimento immagine OCR

## introduzione

Benvenuti nell'emozionante mondo del riconoscimento ottico dei caratteri (OCR) con Aspose.OCR per .NET! In questo tutorial completo, approfondiremo le complessità dell'utilizzo di Aspose.OCR per riconoscere il testo nelle immagini e dimostrare come salvare i risultati in vari formati di documento.

## Prerequisiti

Prima di intraprendere questo viaggio nell'OCR, assicurati di disporre dei seguenti prerequisiti:

-  Aspose.OCR per .NET. Assicurati di avere la libreria Aspose.OCR installata. Puoi scaricarlo[Qui](https://releases.aspose.com/ocr/net/).

-  Directory dei documenti: disponi di una directory designata per i tuoi documenti e aggiorna il file`dataDir` variabile nel codice fornito di conseguenza.

## Importa spazi dei nomi

Inizia importando gli spazi dei nomi necessari. Questi sono gli elementi costitutivi che potenzieranno il tuo codice con funzionalità OCR.

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

Ora suddividiamo l'esempio in più passaggi:

## Passaggio 1: inizializzare Aspose.OCR

```csharp
// Il percorso della directory dei documenti.
string dataDir = "Your Document Directory";

// Inizializza un'istanza di AsposeOcr
AsposeOcr api = new AsposeOcr();
```

Questo passaggio pone le basi inizializzando l'API Aspose.OCR.

## Passaggio 2: riconoscere l'immagine

```csharp
// Riconoscere l'immagine
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

Qui utilizziamo Aspose.OCR per riconoscere il testo all'interno dell'immagine specificata (sostituisci "sample.png" con il tuo file immagine).

## Passaggio 3: salva il risultato in diversi formati

```csharp
// Salva il risultato nel formato preferito
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

Personalizza questo passaggio in base alle tue esigenze. Aspose.OCR ti consente di salvare il testo riconosciuto in vari formati di documento come DOCX, TXT, PDF e XLSX.

## Passaggio 4: Visualizza il messaggio di successo

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

Un semplice messaggio di conferma per farti sapere che il processo si è concluso senza intoppi.

Seguendo questi passaggi, hai sfruttato con successo la potenza di Aspose.OCR per .NET nel riconoscere il testo all'interno delle immagini e nel salvare i risultati in diversi formati di documento.

## Conclusione

In conclusione, Aspose.OCR per .NET apre un mondo di possibilità per il riconoscimento del testo nelle immagini. Che tu stia estraendo dati o creando documenti ricercabili, Aspose.OCR semplifica il processo con la sua API intuitiva.

## Domande frequenti

### Q1. Aspose.OCR è compatibile con diversi formati di immagine?

A1: Sì, Aspose.OCR supporta un'ampia gamma di formati di immagine, garantendo flessibilità nelle attività OCR.

### Q2: Posso personalizzare le impostazioni di riconoscimento per una maggiore precisione?

A2: Assolutamente! Aspose.OCR fornisce impostazioni di riconoscimento per ottimizzare il processo OCR in base alle vostre esigenze specifiche.

### Q3: È disponibile una prova gratuita?

 R3: Sì, puoi iniziare con una prova gratuita[Qui](https://releases.aspose.com/).

### Q4: Come posso ottenere licenze temporanee per Aspose.OCR?

 A4: È possibile ottenere licenze temporanee[Qui](https://purchase.aspose.com/temporary-license/).

### D5: Dove posso cercare aiuto o connettermi con la comunità?

 A5: Unisciti alla comunità Aspose.OCR su[Aspose Forum](https://forum.aspose.com/c/ocr/16) per supporto e discussioni.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
