---
title: Ottieni scelte per i caratteri riconosciuti nel riconoscimento delle immagini OCR
linktitle: Ottieni scelte per i caratteri riconosciuti nel riconoscimento delle immagini OCR
second_title: API Aspose.OCR .NET
description: Migliora le tue applicazioni .NET con Aspose.OCR per un riconoscimento accurato dei caratteri. Segui la nostra guida passo passo per recuperare le scelte per i caratteri riconosciuti nel riconoscimento delle immagini.
weight: 10
url: /it/net/text-recognition/get-choices-for-recognized-characters/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ottieni scelte per i caratteri riconosciuti nel riconoscimento delle immagini OCR

## introduzione

Sbloccare la potenza del riconoscimento ottico dei caratteri (OCR) è fondamentale nell'era digitale di oggi e Aspose.OCR per .NET si distingue come una soluzione solida per il riconoscimento accurato dei caratteri. In questo tutorial approfondiremo una funzionalità specifica: ottenere scelte per i personaggi riconosciuti. Al termine di questa guida integrerai perfettamente questa funzionalità nelle tue applicazioni .NET.

## Prerequisiti

Prima di immergerti nel tutorial, assicurati di possedere i seguenti prerequisiti:

- Conoscenza base dello sviluppo C# e .NET.
- Visual Studio installato sul tuo computer.
-  Libreria Aspose.OCR per .NET, che puoi scaricare[Qui](https://releases.aspose.com/ocr/net/).

## Importa spazi dei nomi

Nel tuo progetto C#, inizia importando gli spazi dei nomi necessari:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Passaggio 1: inizializzare Aspose.OCR

Inizia inizializzando un'istanza di Aspose.OCR:

```csharp
// Il percorso della directory dei documenti.
string dataDir = "Your Document Directory";

// Inizializza un'istanza di AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Passaggio 2: specificare il percorso dell'immagine

Imposta il percorso per l'immagine che desideri analizzare:

```csharp
//Percorso immagine
string fullPath = dataDir + "sample.png";
```

## Passaggio 3: riconoscere l'immagine

Eseguire il processo di riconoscimento dell'immagine:

```csharp
// Riconoscere l'immagine
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    // Impostazioni predefinite o personalizzate
});
```

## Passaggio 4: ottieni scelte per i personaggi riconosciuti

Recupera le scelte per i personaggi riconosciuti:

```csharp
List<char[]> resultWithChoices = result.RecognitionCharactersList;
```

## Passaggio 5: stampare i risultati

Visualizzare il testo e le scelte di riconoscimento:

```csharp
// Stampa il risultato
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Choices:");
resultWithChoices.ForEach(a => Console.WriteLine($"character: {a[0]} . Choices: {a[1]} {a[2]} {a[3]} {a[4]}"));

Console.WriteLine("GetChoiceForRecognizedCharacters executed successfully");
```

Ripeti questi passaggi, personalizzandoli in base ai requisiti della tua applicazione.

## Conclusione

In questo tutorial, abbiamo esplorato come sfruttare Aspose.OCR per .NET per ottenere scelte per i caratteri riconosciuti nel riconoscimento delle immagini. Questa funzionalità aggiunge una nuova dimensione alle tue capacità OCR, migliorando la versatilità delle tue applicazioni.

## Domande frequenti

### Q1: Aspose.OCR per .NET è adatto per l'elaborazione di documenti su larga scala?

R1: Assolutamente! Aspose.OCR per .NET è progettato per gestire grandi volumi di documenti con efficienza e precisione.

### Q2: Posso utilizzare Aspose.OCR per .NET in un'applicazione web?

A2: Sì, puoi integrare Aspose.OCR per .NET in applicazioni web, rendendolo versatile per vari scenari di sviluppo.

### Q3: Sono disponibili opzioni di licenza per Aspose.OCR per .NET?

 R3: Sì, puoi esplorare le opzioni di licenza ed effettuare un acquisto[Qui](https://purchase.aspose.com/buy).

### Q4: Come posso ottenere supporto o porre domande su Aspose.OCR per .NET?

 A4: Visita il[Forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) per ottenere supporto, porre domande e connettersi con la comunità.

### Q5: È disponibile una prova gratuita per Aspose.OCR per .NET?

 R5: Sì, puoi accedere a una prova gratuita[Qui](https://releases.aspose.com/) per sperimentare le funzionalità di Aspose.OCR per .NET.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
