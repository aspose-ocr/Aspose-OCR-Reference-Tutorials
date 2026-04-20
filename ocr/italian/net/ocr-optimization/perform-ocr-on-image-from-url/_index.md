---
date: 2026-02-25
description: Scopri come convertire un'immagine in testo usando Aspose.OCR per .NET,
  estraendo il testo dall'immagine con impostazioni di riconoscimento OCR precise.
linktitle: convert image to text – Perform OCR on Image from URL
second_title: Aspose.OCR .NET API
title: Converti immagine in testo – Esegui OCR su immagine da URL
url: /it/net/ocr-optimization/perform-ocr-on-image-from-url/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Converti Immagine in Testo – Esegui OCR su Immagine da URL

## Introduzione

Se hai bisogno di **convert image to text** in un'applicazione .NET, Aspose.OCR per .NET ti offre un modo affidabile per estrarre testo da immagini ospitate ovunque sul web. In questo tutorial imparerai a riconoscere il testo da un'immagine situata a un URL pubblico, configurare le impostazioni di riconoscimento OCR e gestire il risultato—tutto in pochi minuti.

## Risposte Rapide
- **Di cosa tratta questo tutorial?** Converting image to text from a public URL using Aspose.OCR for .NET.  
- **Qual è la parola chiave principale?** *convert image to text*  
- **È necessaria una licenza?** A trial is available, but a commercial license is required for production use.  
- **Quali versioni .NET sono supportate?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Quanto tempo richiede l'implementazione?** Typically under 10 minutes for a basic setup.

## Cos'è “convert image to text”?
Convertire immagine in testo significa trasformare la rappresentazione visiva dei caratteri in stringhe modificabili e ricercabili. Questo processo—noto anche come **estrarre testo da immagine**—alimenta la digitalizzazione dei documenti, l'automazione dell'inserimento dati e le soluzioni di accessibilità.

## Perché usare Aspose.OCR per .NET per convertire immagine in testo?
- **Alta precisione** con supporto linguistico integrato e opzionali estensioni **OCR language pack**.  
- **Impostazioni di riconoscimento OCR granulari** come correzione automatica dell'inclinazione, rilevamento dell'area e gestione multilinea.  
- **API semplice** che funziona sia con .NET Framework sia con .NET Core senza dipendenze esterne.  
- **Supporto diretto per URL** – puoi **recognize text from URL** senza scaricare prima l'immagine, anche se hai la possibilità di **download image for OCR** se necessario.

## Prerequisiti

Prima di iniziare, assicurati di avere:

- Aspose.OCR per .NET installato. Scarica l'ultima libreria dalla [pagina di rilascio](https://releases.aspose.com/ocr/net/).  
- Un ambiente di sviluppo .NET (Visual Studio, VS Code o il tuo IDE preferito).  
- Accesso a Internet per recuperare l'immagine da elaborare.

## Importa Namespace

Aggiungi i namespace richiesti così da poter lavorare con le classi Aspose.OCR:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
```

## Guida Passo‑Passo per Convertire Immagine in Testo da un URL

### Passo 1: Configura la Cartella del Documento
Definisci dove archiviare eventuali file temporanei o risultati.

```csharp
string dataDir = "Your Document Directory";
```

### Passo 2: Fornisci l'URL dell'Immagine
Fornisci un URL accessibile pubblicamente. Se l'immagine richiede autenticazione, dovrai prima **download image for OCR** e poi usare uno stream.

```csharp
string uri = "https://qph.fs.quoracdn.net/main-qimg-0ff82d0dc3543dcd3b06028f5476c2e4";
```

### Passo 3: Inizializza il Motore AsposeOcr
Crea un'istanza del motore OCR.

```csharp
AsposeOcr api = new AsposeOcr();
```

### Passo 4: Configura le Impostazioni di Riconoscimento OCR
Regola finemente come il motore elabora l'immagine. Qui abilitiamo il rilevamento dell'area, la correzione automatica dell'inclinazione e specifichiamo due rettangoli personalizzati come esempio di **ocr recognition settings**.

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

> **Suggerimento:** Se non ti servono aree personalizzate, imposta `DetectAreas = false` e lascia che il motore individui automaticamente i blocchi di testo.

### Passo 5: Output del Risultato OCR
Stampa il testo riconosciuto, le aree rilevate, eventuali avvisi e il payload JSON completo per il debug.

```csharp
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
```

### Passo 6: Conferma l'Esecuzione Riuscita
Un semplice messaggio di conferma ti indica che il processo è terminato senza eccezioni.

```csharp
Console.WriteLine("PerformOCROnImageFromUrl executed successfully");
```

## Problemi Comuni e Soluzioni

- **Immagine non accessibile pubblicamente** – Verifica che l'URL funzioni in un browser. Per immagini protette, scaricale prima e chiama `RecognizeImageFromStream`.  
- **Le aree di riconoscimento sono errate** – Regola i valori di `Rectangle` o disabilita `DetectAreas` per far sì che il motore rilevi automaticamente.  
- **Lingua non riconosciuta** – Installa il relativo **OCR language pack** e imposta `Language = "eng"` (o un altro codice ISO) in `RecognitionSettings`.  

## Domande Frequenti

### Q1: Aspose.OCR è adatto per gestire più lingue?
**A:** Sì. Aggiungendo il relativo **ocr language pack**, puoi riconoscere testo in decine di lingue.

### Q2: Posso usare Aspose.OCR sia per l'estrazione di testo a riga singola che multilinea?
**A:** Assolutamente. Attiva/disattiva `RecognizeSingleLine` in `RecognitionSettings` a seconda dello scenario.

### Q3: Esistono opzioni di licenza per progetti commerciali?
**A:** Sì, puoi esplorare le opzioni di licenza e acquistare una licenza completa nello [store Aspose](https://purchase.aspose.com/buy).

### Q4: È disponibile una versione di prova gratuita?
**A:** Sì, una versione di prova è scaricabile dalla [pagina dei rilasci](https://releases.aspose.com/).

### Q5: Dove posso trovare supporto dalla community?
**A:** Visita il dedicato [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) per assistenza e discussioni.

## Conclusione

Con Aspose.OCR per .NET, convertire immagine in testo da un URL remoto è semplice e altamente personalizzabile. Seguendo i passaggi sopra potrai integrare capacità OCR robuste in qualsiasi applicazione .NET, sia che tu abbia bisogno di una semplice funzionalità **estrarre testo da immagine** o di avanzate **ocr recognition settings** per documenti complessi.

---

**Last Updated:** 2026-02-25  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}