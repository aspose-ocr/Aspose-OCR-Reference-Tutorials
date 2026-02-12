---
date: 2026-01-02
description: Scopri come ottenere le scelte dei caratteri OCR utilizzando Aspose.OCR
  per .NET. Questa guida mostra passo dopo passo come recuperare le alternative dei
  caratteri nel riconoscimento delle immagini.
linktitle: Get Choices for Recognized Characters in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: Come ottenere le scelte di caratteri OCR per i caratteri riconosciuti nel riconoscimento
  delle immagini
url: /it/net/text-recognition/get-choices-for-recognized-characters/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ottieni le scelte per i caratteri riconosciuti nel riconoscimento OCR delle immagini

## Introduzione

Sblocca la potenza del riconoscimento ottico dei caratteri (OCR) nelle moderne applicazioni .NET e impara **come ottenere le scelte dei caratteri OCR** per ogni simbolo riconosciuto. Aspose.OCR per .NET rende tutto questo semplice, fornendoti non solo il testo più probabile ma anche i caratteri alternativi che il motore ha considerato. Alla fine di questo tutorial sarai in grado di integrare questa funzionalità in qualsiasi progetto C# e migliorare la gestione dei glifi ambigui.

## Risposte rapide
- **Cosa significa “get OCR character choices”?** Restituisce un elenco di caratteri alternativi per ogni glifo riconosciuto.  
- **Perché usare le scelte dei caratteri?** Per gestire riconoscimenti incerti, eseguire post‑processing o implementare una convalida personalizzata.  
- **Cosa serve in anticipo?** Ambiente di sviluppo .NET, Visual Studio e la libreria Aspose.OCR per .NET.  
- **È necessaria una licenza?** Una versione di prova gratuita è sufficiente per i test; per la produzione è necessaria una licenza commerciale.  
- **Posso eseguirlo su .NET Core / .NET 6?** Sì, Aspose.OCR supporta tutti i runtime .NET moderni.

## Cos'è “get OCR character choices”?
Quando il motore OCR analizza un'immagine, ogni modello di pixel può corrispondere a diversi possibili caratteri. L'API **get OCR character choices** espone queste alternative, consentendo agli sviluppatori di decidere quale carattere si adatta meglio al contesto.

## Perché usare Aspose.OCR per .NET?
- **Alta precisione** su molte lingue e caratteri.  
- **Integrazione facile** con una semplice API C#.  
- **Accesso alle alternative dei caratteri** tramite `RecognitionCharactersList`.  
- **Nessuna dipendenza esterna** – funziona subito su Windows, Linux e macOS.

## Prerequisiti

Prima di immergerti nel tutorial, assicurati di avere i seguenti prerequisiti:

- Conoscenza di base di C# e sviluppo .NET.  
- Visual Studio installato sulla tua macchina.  
- Libreria Aspose.OCR per .NET, che puoi scaricare [qui](https://releases.aspose.com/ocr/net/).

## Importa gli spazi dei nomi

Nel tuo progetto C#, inizia importando gli spazi dei nomi necessari:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Passo 1: Inizializza Aspose.OCR

Inizia inizializzando un'istanza di Aspose.OCR:

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Passo 2: Specifica il percorso dell'immagine

Imposta il percorso dell'immagine che desideri analizzare:

```csharp
// Image Path
string fullPath = dataDir + "sample.png";
```

## Passo 3: Riconosci l'immagine

Esegui il processo di riconoscimento dell'immagine:

```csharp
// Recognize image           
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    // Default or custom settings
});
```

## Panoramica su Get OCR Character Choices

Ora che l'immagine è stata riconosciuta, puoi recuperare l'elenco delle alternative dei caratteri che il motore OCR ha considerato per ogni posizione.

## Passo 4: Ottieni le scelte per i caratteri riconosciuti

Recupera le scelte per i caratteri riconosciuti:

```csharp
List<char[]> resultWithChoices = result.RecognitionCharactersList;
```

## Passo 5: Stampa i risultati

Visualizza il testo riconosciuto e le scelte:

```csharp
// Print result
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Choices:");
resultWithChoices.ForEach(a => Console.WriteLine($"character: {a[0]} . Choices: {a[1]} {a[2]} {a[3]} {a[4]}"));

Console.WriteLine("GetChoiceForRecognizedCharacters executed successfully");
```

Ripeti questi passaggi, personalizzandoli in base ai requisiti della tua applicazione.

## Problemi comuni e soluzioni

- **`RecognitionCharactersList` vuoto** – Assicurati che l'immagine abbia una risoluzione e un contrasto sufficienti.  
- **Caratteri inaspettati** – Regola `RecognitionSettings` (ad es., lingua, dizionario) per migliorare la precisione.  
- **Problemi di prestazioni** – Elabora le immagini in modo asincrono o in batch per mantenere l'interfaccia reattiva.

## Domande frequenti

### Q1: Aspose.OCR per .NET è adatto per l'elaborazione di documenti su larga scala?
R1: Assolutamente! Aspose.OCR per .NET è progettato per gestire grandi volumi di documenti con efficienza e precisione.

### Q2: Posso usare Aspose.OCR per .NET in un'applicazione web?
R2: Sì, puoi integrare Aspose.OCR per .NET nelle applicazioni web, rendendolo versatile per vari scenari di sviluppo.

### Q3: Sono disponibili opzioni di licenza per Aspose.OCR per .NET?
R3: Sì, puoi esplorare le opzioni di licenza e effettuare un acquisto [qui](https://purchase.aspose.com/buy).

### Q4: Come posso ottenere supporto o fare domande su Aspose.OCR per .NET?
R4: Visita il [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) per ottenere supporto, fare domande e connetterti con la community.

### Q5: È disponibile una versione di prova gratuita per Aspose.OCR per .NET?
R5: Sì, puoi accedere a una versione di prova gratuita [qui](https://releases.aspose.com/) per provare le funzionalità di Aspose.OCR per .NET.

## Conclusione

In questo tutorial, abbiamo esplorato come **ottenere le scelte dei caratteri OCR** usando Aspose.OCR per .NET. Questa funzionalità aggiunge una nuova dimensione alle tue capacità OCR, consentendo una gestione più intelligente dei caratteri ambigui e una logica di post‑processing più ricca.

---

**Last Updated:** 2026-01-02  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}