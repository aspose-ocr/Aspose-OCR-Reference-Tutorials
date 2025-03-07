---
title: Specificare i caratteri consentiti nel riconoscimento immagine OCR
linktitle: Specificare i caratteri consentiti nel riconoscimento immagine OCR
second_title: API Aspose.OCR .NET
description: Sblocca un OCR preciso in .NET con Aspose.OCR. Riconoscere facilmente il testo dalle immagini. Scaricalo ora per un'esperienza di sviluppo trasformativa.
weight: 13
url: /it/net/ocr-settings/specify-allowed-characters/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Specificare i caratteri consentiti nel riconoscimento immagine OCR

## introduzione

Nel panorama in continua evoluzione della tecnologia, il riconoscimento ottico dei caratteri (OCR) è emerso come uno strumento di trasformazione, consentendo alle macchine di comprendere il testo dalle immagini. Aspose.OCR per .NET si distingue come una soluzione potente, fornendo una perfetta integrazione per gli sviluppatori che cercano solide funzionalità OCR nelle loro applicazioni .NET.

## Prerequisiti

Prima di immergerti nel tutorial, assicurati di disporre dei seguenti prerequisiti:

- Una conoscenza pratica dello sviluppo .NET.
-  Aspose.OCR per la libreria .NET. Puoi scaricarlo[Qui](https://releases.aspose.com/ocr/net/).
- Familiarità con Visual Studio o qualsiasi altro ambiente di sviluppo .NET preferito.

## Importa spazi dei nomi

Nel tuo progetto .NET, importa gli spazi dei nomi necessari per sfruttare in modo efficace le funzionalità di Aspose.OCR per .NET:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

Ora suddividiamo il tutorial in una serie di passaggi completi:

## Passaggio 1: specificare i caratteri consentiti nel riconoscimento immagine OCR

Per iniziare, imposta il percorso della directory dei documenti:

```csharp
string dataDir = "Your Document Directory";
```

## Passaggio 2: inizializza Aspose.OCR con i simboli consentiti

Crea un'istanza di AsposeOcr, specificando i simboli consentiti. In questo caso, consentiamo le cifre (0-9):

```csharp
AsposeOcr api = new AsposeOcr("0123456789");
```

## Passaggio 3: riconoscere l'immagine

Utilizza l'istanza AsposeOcr per riconoscere il testo da un'immagine:

```csharp
string result = api.RecognizeLine(dataDir + "0001460985.Jpeg");
```

## Passaggio 4: Visualizza il testo riconosciuto

Stampa il testo riconosciuto sulla console:

```csharp
Console.WriteLine(result);
```

## Passaggio 5: Secondo caso: riconoscimento dell'immagine con impostazioni specifiche

Inizializza un'altra istanza di AsposeOcr, questa volta con impostazioni più specifiche:

```csharp
AsposeOcr api2 = new AsposeOcr();
RecognitionResult result2 = api2.RecognizeImage(dataDir + "0001460985.Jpeg", 
    new RecognitionSettings { 
        AllowedCharacters = CharactersAllowedType.DIGITS,
        RecognizeSingleLine = true
    });
```

## Passaggio 6: visualizzare il testo riconosciuto secondo maiuscolo/minuscolo

Stampa il testo riconosciuto dal secondo caso alla console:

```csharp
Console.WriteLine(result2.RecognitionText);
```

## Passaggio 7: esecuzione riuscita

Infine, conferma la corretta esecuzione del tutorial SpecificaAllowedCharacters:

```csharp
Console.WriteLine("SpecifyAllowedCharacters executed successfully");
```

Seguendo questi passaggi, hai sbloccato la possibilità di specificare i caratteri consentiti nel riconoscimento delle immagini OCR utilizzando Aspose.OCR per .NET.

## Conclusione

Aspose.OCR per .NET consente agli sviluppatori di integrare perfettamente le funzionalità OCR nelle loro applicazioni, aprendo le porte a soluzioni innovative in vari domini. Sfrutta la potenza dell'OCR e migliora i tuoi progetti con il riconoscimento accurato del testo.

## Domande frequenti

### Q1: Aspose.OCR per .NET è adatto sia ai principianti che agli sviluppatori esperti?

R1: Assolutamente! Aspose.OCR per .NET si rivolge a sviluppatori di tutti i livelli, fornendo funzionalità intuitive per un'integrazione perfetta.

### Q2: Posso utilizzare Aspose.OCR per .NET per riconoscere caratteri in più lingue?

A2: Sì, Aspose.OCR supporta il riconoscimento in varie lingue, rendendolo versatile per diverse applicazioni.

### Q3: Con quale frequenza viene aggiornato Aspose.OCR per .NET?

 R3: Gli aggiornamenti vengono rilasciati regolarmente per garantire la compatibilità con le tecnologie più recenti e risolvere eventuali problemi. Controlla il[documentazione](https://reference.aspose.com/ocr/net/) per le informazioni più recenti.

### Q4: È disponibile una prova gratuita per Aspose.OCR per .NET?

 A4: Sì, puoi esplorare le funzionalità di Aspose.OCR scaricando il file[prova gratuita](https://releases.aspose.com/).

### D5: Dove posso chiedere assistenza o connettermi con la comunità per ricevere supporto?

 A5: Visita il[Forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) interagire con la comunità e ottenere assistenza da esperti.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
