---
title: Operazione OCR con selezione della lingua nel riconoscimento delle immagini OCR
linktitle: Operazione OCR con selezione della lingua nel riconoscimento delle immagini OCR
second_title: API Aspose.OCR .NET
description: Sblocca potenti funzionalità OCR con Aspose.OCR per .NET. Estrai testo dalle immagini senza problemi.
weight: 12
url: /it/net/ocr-configuration/ocr-operation-with-language-selection/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Operazione OCR con selezione della lingua nel riconoscimento delle immagini OCR

## introduzione

Nel mondo del riconoscimento delle immagini e del riconoscimento ottico dei caratteri (OCR), Aspose.OCR per .NET si distingue come un potente strumento per gli sviluppatori che cercano un'estrazione di testo accurata ed efficiente dalle immagini. Questa guida passo passo ti guiderà attraverso il processo di riconoscimento delle immagini OCR utilizzando Aspose.OCR per .NET, concentrandosi sull'operazione con la selezione della lingua.

## Prerequisiti

Prima di approfondire il tutorial, assicurati di disporre dei seguenti prerequisiti:

-  Aspose.OCR per .NET: assicurati di avere la libreria Aspose.OCR installata. Puoi scaricarlo da[Aspose.OCR per la pagina di download di .NET](https://releases.aspose.com/ocr/net/).

- Ambiente di sviluppo: configura un ambiente di lavoro con un'applicazione .NET. Se non lo hai ancora fatto, fai riferimento a[documentazione](https://reference.aspose.com/ocr/net/) per istruzioni dettagliate.

## Importa spazi dei nomi

Nella tua applicazione .NET, inizia importando gli spazi dei nomi necessari:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Passaggio 1: inizializzare Aspose.OCR

Inizia inizializzando un'istanza della classe Aspose.OCR. Ciò pone le basi per l'utilizzo delle funzionalità OCR all'interno dell'applicazione.

```csharp
// Inizio ex:1
// Il percorso della directory dei documenti.
string dataDir = "Your Document Directory";

// Inizializza un'istanza di AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Passaggio 2: specificare il percorso dell'immagine

Successivamente, definisci il percorso dell'immagine su cui desideri eseguire l'OCR. Assicurati che l'immagine sia accessibile dalla tua applicazione.

```csharp
//Percorso immagine
string fullPath = dataDir + "sample.png";
```

## Passaggio 3: riconoscere l'immagine con la selezione della lingua

Ora arriva l'operazione principale dell'OCR. Utilizza la libreria Aspose.OCR per riconoscere il testo dall'immagine specificata. Regola le impostazioni di riconoscimento, inclusa la selezione della lingua.

```csharp
// Riconoscere l'immagine
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    SkewAngle = 0.2F,
    Language = Language.Eng, // Scegli la lingua: none, eng, deu, por, spa, fra, ita, cze, dan, dum, est, fin, lav, lit, nor, pol, rum, srp_hrv, slk, slv, swe, chi
});
```

## Passaggio 4: stampare e visualizzare i risultati

Dopo l'operazione OCR, stampare e visualizzare i risultati, inclusi testo riconosciuto, aree, avvisi e rappresentazione JSON.

```csharp
// Stampa il risultato
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
// Fine Estesa:1
```

## Conclusione

Congratulazioni! Hai eseguito con successo il riconoscimento delle immagini OCR con la selezione della lingua utilizzando Aspose.OCR per .NET. Questo tutorial ha dimostrato i passaggi essenziali per estrarre il testo dalle immagini e ha evidenziato la flessibilità delle opzioni linguistiche.

## Domande frequenti

### Q1: Aspose.OCR è adatto al riconoscimento di testo multilingue?

A1: Sì, Aspose.OCR supporta varie lingue, fornendo flessibilità per attività OCR multilingue.

### D2: Posso ottimizzare le impostazioni OCR per caratteristiche specifiche dell'immagine?

A2: Assolutamente! Regola parametri come l'angolo di inclinazione, il riconoscimento della linea e il rilevamento dell'area per ottimizzare l'OCR per diversi scenari.

### Q3: Dove posso trovare ulteriore supporto o discussioni nella community?

 A3: Visita il[Forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) per supporto e discussioni con la comunità.

### Q4: È disponibile una prova gratuita?

 A4: Sì, esplora il[prova gratuita](https://releases.aspose.com/) per sperimentare le capacità di Aspose.OCR.

### Q5: Come posso acquistare Aspose.OCR per .NET?

 A5: Per acquistare, visitare il[pagina di acquisto](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
