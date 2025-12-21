---
date: 2025-12-21
description: Scopri come eseguire l'OCR e estrarre il testo da un'immagine usando
  Aspose.OCR per .NET. Questa guida passo passo mostra il riconoscimento multilingue
  del testo e la selezione della lingua.
linktitle: How to Perform OCR with Language Selection in Aspose.OCR
second_title: Aspose.OCR .NET API
title: Come eseguire l'OCR con selezione della lingua in Aspose.OCR
url: /it/net/ocr-configuration/ocr-operation-with-language-selection/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR con selezione della lingua in Aspose.OCR

## Introduzione

Se hai bisogno di **come eseguire OCR** su immagini ed estrarre testo da file immagine in un'applicazione .NET, Aspose.OCR per .NET offre una soluzione veloce, accurata e consapevole della lingua. In questo tutorial percorreremo un esempio reale che dimostra il riconoscimento OCR delle immagini con selezione della lingua, così potrai estrarre testo multilingue dalle foto con poche righe di codice.

## Risposte rapide
- **Cosa fa Aspose.OCR?** Riconosce testo stampato e scritto a mano nelle immagini e restituisce il testo estratto.  
- **Posso scegliere la lingua?** Sì – puoi specificare qualsiasi lingua supportata come English, German, Spanish, Chinese, ecc.  
- **Ho bisogno di una licenza per lo sviluppo?** Una versione di prova gratuita è sufficiente per la valutazione; è necessaria una licenza per l'uso in produzione.  
- **Quali versioni .NET sono supportate?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **La correzione dell'inclinazione è automatica?** Puoi abilitare `AutoSkew` e regolare finemente l'impostazione `SkewAngle`.

## Perché scegliere Aspose.OCR per le attività OCR?

- **Alta precisione** su più font e qualità dell'immagine.  
- **Selezione della lingua integrata** elimina la necessità di pacchetti linguistici esterni.  
- **API semplice** che si integra perfettamente con progetti C# esistenti.  
- **Nessuna dipendenza esterna** – tutto gira localmente, mantenendo i dati sicuri.

## Prerequisiti

Prima di immergerci nel codice, assicurati di avere i seguenti prerequisiti:

- Aspose.OCR per .NET: Assicurati di avere la libreria Aspose.OCR installata. Puoi scaricarla dalla [pagina di download di Aspose.OCR per .NET](https://releases.aspose.com/ocr/net/).

- Ambiente di sviluppo: Configura un ambiente di lavoro con un'applicazione .NET. Se non lo hai ancora fatto, consulta la [documentazione](https://reference.aspose.com/ocr/net/) per istruzioni dettagliate.

## Importare gli spazi dei nomi

Nella tua applicazione .NET, inizia importando gli spazi dei nomi necessari:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Passo 1: Inizializzare Aspose.OCR

Inizia inizializzando un'istanza della classe Aspose.OCR. Questo prepara l'uso delle funzionalità OCR nella tua applicazione.

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Passo 2: Specificare il percorso dell'immagine

Successivamente, definisci il percorso dell'immagine su cui eseguire l'OCR. Assicurati che l'immagine sia accessibile dalla tua applicazione.

```csharp
// Image Path
string fullPath = dataDir + "sample.png";
```

## Passo 3: Riconoscere l'immagine con selezione della lingua

Ora arriva l'operazione OCR principale. Utilizza la libreria Aspose.OCR per riconoscere il testo dall'immagine specificata. Regola le impostazioni di riconoscimento, inclusa la selezione della lingua.

```csharp
// Recognize image           
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    SkewAngle = 0.2F,
    Language = Language.Eng, // Choose the language: none, eng, deu, por, spa, fra, ita, cze, dan, dum, est, fin, lav, lit, nor, pol, rum, srp_hrv, slk, slv, swe, chi
});
```

## Passo 4: Stampare e visualizzare i risultati

Dopo l'operazione OCR, stampa e visualizza i risultati, inclusi testo riconosciuto, aree, avvisi e rappresentazione JSON.

```csharp
// Print result
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
// ExEnd:1
```

## Problemi comuni e suggerimenti

- **Selezione della lingua errata** – Se l'output appare confuso, verifica che la proprietà `Language` corrisponda alla lingua dell'immagine di origine.  
- **Immagini inclinate** – Abilita `AutoSkew` o regola manualmente `SkewAngle` per una migliore precisione su scansioni inclinate.  
- **File di grandi dimensioni** – Elabora immagini grandi a blocchi o riduci la risoluzione prima di passarle a `RecognizeImage` per risparmiare memoria.

## Conclusione

Congratulazioni! Hai imparato **come eseguire OCR** con selezione della lingua usando Aspose.OCR per .NET. Questo tutorial ti ha mostrato come estrarre testo da file immagine, personalizzare le impostazioni di riconoscimento e gestire contenuti multilingue senza sforzo.

## FAQ

### Q1: Aspose.OCR è adatto al riconoscimento di testo multilingue?

A1: Sì, Aspose.OCR supporta varie lingue, offrendo flessibilità per compiti OCR multilingue.

### Q2: Posso perfezionare le impostazioni OCR per caratteristiche specifiche dell'immagine?

A2: Assolutamente! Regola parametri come l'angolo di inclinazione, il riconoscimento delle linee e il rilevamento delle aree per ottimizzare l'OCR in diversi scenari.

### Q3: Dove posso trovare supporto aggiuntivo o discussioni della community?

A3: Visita il [forum di Aspose.OCR](https://forum.aspose.com/c/ocr/16) per supporto e discussioni con la community.

### Q4: È disponibile una versione di prova gratuita?

A4: Sì, esplora la [versione di prova gratuita](https://releases.aspose.com/) per provare le funzionalità di Aspose.OCR.

### Q5: Come posso acquistare Aspose.OCR per .NET?

A5: Per acquistare, visita la [pagina di acquisto](https://purchase.aspose.com/buy).

**Last Updated:** 2025-12-21  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}