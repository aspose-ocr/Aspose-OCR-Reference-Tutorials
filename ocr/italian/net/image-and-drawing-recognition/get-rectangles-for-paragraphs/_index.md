---
date: 2025-12-17
description: Scopri come estrarre i rettangoli per i paragrafi nelle immagini OCR
  usando Aspose.OCR per .NET – la guida di riferimento su come estrarre i rettangoli
  e le coordinate dei paragrafi.
linktitle: Get Rectangles for Paragraphs in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: Come estrarre i rettangoli per i paragrafi nel riconoscimento OCR delle immagini
url: /it/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come estrarre rettangoli per i paragrafi nel riconoscimento di immagini OCR

## Introduzione

Benvenuti alla nostra guida completa su **come estrarre rettangoli** per i paragrafi nel riconoscimento di immagini OCR con Aspose.OCR per .NET. Se desideri migliorare il tuo flusso di lavoro di elaborazione dei documenti, estrarre i confini dei paragrafi e automatizzare l'estrazione dei dati, sei nel posto giusto. Ti guideremo passo passo—dalla configurazione dell'ambiente alla stampa delle coordinate dei rettangoli—così potrai iniziare a utilizzare i risultati OCR immediatamente.

## Risposte rapide
- **Cosa significa “estrarre rettangoli”?** Restituisce le bounding box (x, y, larghezza, altezza) delle aree di testo rilevate.  
- **Quale metodo API fornisce i rettangoli?** `AsposeOcr.GetRectangles` con `AreasType.PARAGRAPHS`.  
- **È necessaria una licenza per lo sviluppo?** Una versione di prova gratuita è sufficiente per i test; è necessaria una licenza commerciale per la produzione.  
- **Posso elaborare più immagini contemporaneamente?** Sì—itera sulla tua lista di immagini e chiama `GetRectangles` per ogni file.  
- **Quali formati sono supportati?** PNG, JPEG, TIFF, BMP e molti altri.

## Cos'è “come estrarre rettangoli” in OCR?
Nel gergo OCR, estrarre rettangoli significa identificare i confini geometrici che racchiudono ogni paragrafo o riga di testo all'interno di un'immagine. Queste coordinate ti consentono di evidenziare, ritagliare o analizzare ulteriormente sezioni specifiche di un documento scansionato.

## Perché estrarre le coordinate dei paragrafi?
- **Elaborazione post‑processing precisa** – puoi inserire ogni rettangolo nei flussi di lavoro successivi (ad es., traduzione, redazione).  
- **UI/UX migliorata** – sovrapponi le bounding box sull'immagine originale per mostrare agli utenti dove è stato trovato il testo.  
- **Automazione batch** – individua e isola rapidamente i paragrafi in grandi insiemi di documenti.

## Prerequisiti

- Conoscenza di base di C# e sviluppo .NET.  
- Un ambiente di sviluppo con Aspose.OCR per .NET installato – puoi scaricarlo [qui](https://releases.aspose.com/ocr/net/).  
- Familiarità con i concetti di elaborazione delle immagini e con il motivo per cui l'OCR è essenziale per estrarre testo da file scansionati.

## Importa gli spazi dei nomi

Nel tuo file C#, importa gli spazi dei nomi richiesti affinché le classi OCR siano disponibili:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Passo 1: Configura la cartella del documento

Definisci la cartella che contiene le immagini che desideri analizzare:

```csharp
string dataDir = "Your Document Directory";
```

## Passo 2: Inizializza l'istanza AsposeOcr

Crea un oggetto `AsposeOcr` – questo ti dà accesso a tutte le funzioni OCR:

```csharp
AsposeOcr api = new AsposeOcr();
```

## Passo 3: Specifica il percorso dell'immagine

Indica il file immagine esatto che desideri elaborare:

```csharp
string fullPath = dataDir + "sample.png";
```

## Passo 4: Riconosci l'immagine e ottieni i rettangoli dei paragrafi

Chiama il metodo `GetRectangles`. Impostare `detect_areas` su `true` indica al motore di restituire i rettangoli dei **paragrafi**:

```csharp
List<Rectangle> rectangles = api.GetRectangles(fullPath, AreasType.PARAGRAPHS, true);
```

## Passo 5: Stampa i risultati

Stampa le coordinate in modo da poter vedere le **coordinate dei paragrafi estratti** rilevate:

```csharp
Console.WriteLine("Areas coordinates:");
rectangles.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
```

## Problemi comuni e soluzioni

| Problema | Motivo | Soluzione |
|----------|--------|-----------|
| Nessun rettangolo restituito | Qualità dell'immagine troppo bassa o `AreasType` errato | Assicurati che l'immagine sia chiara e utilizza `AreasType.PARAGRAPHS`. |
| Le coordinate sono sfasate di uno | Mancata corrispondenza della scala DPI | Imposta il DPI corretto durante il caricamento dell'immagine o usa `api.Config.Dpi`. |
| Eccezione di licenza | Esecuzione senza licenza valida in produzione | Applica una licenza temporanea o permanente tramite `api.SetLicense`. |

## Domande frequenti

**D: Aspose.OCR è compatibile con diversi formati immagine?**  
R: Sì, Aspose.OCR supporta PNG, JPEG, TIFF, BMP e molti altri formati comuni.

**D: Posso usare Aspose.OCR per l'elaborazione batch di più immagini?**  
R: Assolutamente! Scorri una collezione di percorsi file e chiama `GetRectangles` per ogni immagine.

**D: È disponibile una versione di prova gratuita per Aspose.OCR per .NET?**  
R: Sì, puoi provare una versione di prova gratuita [qui](https://releases.aspose.com/).

**D: Come posso ottenere una licenza temporanea per Aspose.OCR?**  
R: Puoi acquisire una licenza temporanea [qui](https://purchase.aspose.com/temporary-license/).

**D: Dove posso trovare supporto aggiuntivo e discussioni relative ad Aspose.OCR?**  
R: Vai al [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) per supporto della community e discussioni.

## Conclusione

In questo tutorial abbiamo mostrato **come estrarre rettangoli** per i paragrafi usando Aspose.OCR per .NET, esaminato ogni frammento di codice e spiegato come interpretare le coordinate restituite. Integrando questi passaggi nella tua applicazione, potrai estrarre in modo affidabile i confini dei paragrafi, migliorare i flussi di lavoro dei documenti e creare soluzioni OCR più intelligenti.

---

**Ultimo aggiornamento:** 2025-12-17  
**Testato con:** Aspose.OCR 24.11 per .NET  
**Autore:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}