---
title: Esegui l'OCR sull'immagine dall'URL in Riconoscimento immagini OCR
linktitle: Esegui l'OCR sull'immagine dall'URL in Riconoscimento immagini OCR
second_title: API Aspose.OCR .NET
description: Esplora l'integrazione perfetta dell'OCR con Aspose.OCR per .NET. Riconoscere il testo dalle immagini con precisione.
type: docs
weight: 10
url: /it/net/ocr-optimization/perform-ocr-on-image-from-url/
---
## introduzione

Nel regno del riconoscimento ottico dei caratteri (OCR), Aspose.OCR per .NET si distingue come un potente strumento che consente agli sviluppatori di estrarre contenuto testuale dalle immagini con precisione. Se stai cercando di integrare le funzionalità OCR nella tua applicazione .NET ed eseguire il riconoscimento del testo senza sforzo, questa guida passo passo ti guiderà attraverso il processo di esecuzione dell'OCR su un'immagine da un URL.

## Prerequisiti

Prima di approfondire il tutorial, assicurati di disporre dei seguenti prerequisiti:

-  Aspose.OCR per .NET: assicurati di avere la libreria Aspose.OCR integrata nel tuo progetto .NET. Puoi scaricarlo da[pagina di rilascio](https://releases.aspose.com/ocr/net/).

- Ambiente di sviluppo: disporre di un ambiente di sviluppo .NET funzionante configurato sul computer.

## Importa spazi dei nomi

Nel tuo progetto .NET, includi gli spazi dei nomi necessari per accedere alle funzionalità Aspose.OCR. Aggiungi il seguente snippet di codice al tuo progetto:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
```

## Passaggio 1: imposta la directory dei documenti

 Inizia specificando la directory in cui sono archiviati i tuoi documenti. Sostituire`"Your Document Directory"` con il percorso effettivo dei tuoi documenti.

```csharp
string dataDir = "Your Document Directory";
```

## Passaggio 2: ottieni l'immagine per il riconoscimento

Fornisci l'URL dell'immagine su cui desideri eseguire l'OCR. Assicurati che l'immagine sia accessibile al pubblico.

```csharp
string uri = "https://qph.fs.quoracdn.net/main-qimg-0ff82d0dc3543dcd3b06028f5476c2e4";
```

## Passaggio 3: inizializzare AsposeOcr

Crea un'istanza della classe AsposeOcr per accedere alle funzionalità OCR.

```csharp
AsposeOcr api = new AsposeOcr();
```

## Passaggio 4: riconoscere l'immagine

Utilizza la libreria Aspose.OCR per riconoscere il testo dall'URL dell'immagine specificata. Modifica le impostazioni di riconoscimento in base alle tue esigenze.

```csharp
RecognitionResult result = api.RecognizeImageFromUri(uri, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    RecognitionAreas = new List<Rectangle>()
    {
        new Rectangle(1,3,390,70),
        new Rectangle(1,72,390,70)
    }
});
```

## Passaggio 5: stampa del risultato

Visualizza il risultato del riconoscimento, incluso il testo riconosciuto, le aree ed eventuali avvisi.

```csharp
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
```

## Passaggio 6: eseguire e verificare

Esegui la tua applicazione e, se tutto è impostato correttamente, dovresti vedere il processo OCR eseguito correttamente.

```csharp
Console.WriteLine("PerformOCROnImageFromUrl executed successfully");
```

## Conclusione

Con Aspose.OCR per .NET, l'integrazione delle funzionalità OCR nelle tue applicazioni .NET diventa un'esperienza senza soluzione di continuità. Questo tutorial ti ha guidato attraverso il processo di esecuzione dell'OCR su un'immagine da un URL, fornendoti le basi per sfruttare la potenza del riconoscimento del testo nei tuoi progetti.

## Domande frequenti

### Q1: Aspose.OCR è adatto alla gestione di più lingue?

A1: Sì, Aspose.OCR supporta il riconoscimento del testo in varie lingue, rendendolo versatile per applicazioni internazionali.

### Q2: Posso utilizzare Aspose.OCR per il riconoscimento del testo sia su riga singola che su più righe?

A2: Assolutamente! Aspose.OCR offre flessibilità per riconoscere sia il testo a riga singola che quello multilinea, adattandosi al tuo caso d'uso specifico.

### Q3: Sono disponibili opzioni di licenza per Aspose.OCR?

 R3: Sì, puoi esplorare le opzioni di licenza ed effettuare acquisti su[Aspose negozio](https://purchase.aspose.com/buy).

### Q4: È disponibile una prova gratuita per Aspose.OCR?

 A4: Sì, puoi provare Aspose.OCR gratuitamente visitando il sito[pagina delle uscite](https://releases.aspose.com/).

### Q5: Dove posso trovare supporto o discussioni della community relative ad Aspose.OCR?

 A5: Visita il[Forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) per il supporto e il coinvolgimento con la comunità.