---
date: 2025-12-17
description: Scopri come ottenere i rettangoli delle linee OCR utilizzando Aspose.OCR
  per .NET per riconoscere le linee di testo nelle immagini ed estrarre facilmente
  le coordinate delle linee.
linktitle: Get OCR Line Rectangles for Image Text Lines
second_title: Aspose.OCR .NET API
title: Ottieni i rettangoli delle linee OCR per le linee di testo dell'immagine
url: /it/net/image-and-drawing-recognition/get-rectangles-for-lines/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ottieni i Rettangoli delle Linee OCR per le Linee di Testo in Immagine

## Introduzione

In questo tutorial scoprirai **come ottenere i rettangoli delle linee OCR** con Aspose.OCR per .NET. Alla fine della guida sarai in grado di **riconoscere le linee di testo in un'immagine** e **estrarre le coordinate delle linee** per ogni linea rilevata—perfetto per elaborazioni successive come analisi del layout, estrazione dati o rendering personalizzato.

## Risposte Rapide
- **Cosa significa “ottenere i rettangoli delle linee OCR”?** Restituisce i riquadri di delimitazione di ogni linea di testo rilevata in un'immagine.  
- **Quale metodo API viene utilizzato?** `AsposeOcr.GetRectangles(..., AreasType.LINES, ...)`.  
- **È necessaria una licenza?** Una versione di prova gratuita è sufficiente per lo sviluppo; è richiesta una licenza commerciale per la produzione.  
- **Formati immagine supportati?** PNG, JPEG, BMP, TIFF e altri.  
- **Posso eseguirlo su .NET Core?** Sì, Aspose.OCR supporta pienamente .NET Core e .NET 5/6.

## Prerequisiti

Prima di immergerti nel tutorial, assicurati di avere i seguenti prerequisiti:

- Conoscenza di base di C# e sviluppo .NET.  
- Un ambiente di sviluppo integrato (IDE) come Visual Studio.  
- Libreria Aspose.OCR per .NET installata. Puoi scaricarla [qui](https://releases.aspose.com/ocr/net/).  
- Un'immagine di esempio contenente testo per il riconoscimento OCR.

## Importare i Namespace

Assicurati di aver importato i namespace necessari nel tuo progetto. Aggiungi le seguenti righe all'inizio del tuo file C#:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

Ora, analizziamo il processo di ottenimento dei rettangoli per le linee nel riconoscimento OCR di un'immagine in passaggi facili da seguire.

## Passo 1: Configura la Directory del Documento

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

Sostituisci `"Your Document Directory"` con il percorso reale della cartella che contiene la tua immagine di esempio.

## Passo 2: Inizializza Aspose.OCR

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

Crea un'istanza della classe `AsposeOcr` per accedere alle funzionalità OCR.

## Passo 3: Specifica il Percorso dell'Immagine

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

Definisci il percorso completo dell'immagine su cui eseguire l'OCR.

## Passo 4: Riconosci l'Immagine e Ottieni i Rettangoli

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

Il metodo `GetRectangles` restituisce un elenco di oggetti `Rectangle`, ciascuno dei quali rappresenta le coordinate di una linea di testo rilevata. Questo è il cuore del **ottenere i rettangoli delle linee OCR**.

## Passo 5: Stampa il Risultato

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

Stampa le coordinate delle aree rilevate sulla console. Vedrai valori che potrai successivamente utilizzare per **estrarre le coordinate delle linee** per un'elaborazione personalizzata.

## Perché Usare Aspose.OCR per i Rettangoli delle Linee?

- **Alta precisione** – Algoritmi avanzati rilevano le linee anche in immagini rumorose o inclinate.  
- **Cross‑platform** – Funziona su .NET Framework, .NET Core e .NET 5/6.  
- **Nessuna dipendenza esterna** – Libreria .NET pura, senza DLL native da distribuire.  
- **Output ricco** – Oltre ai rettangoli delle linee è possibile recuperare parole, caratteri e punteggi di confidenza.

## Problemi Comuni e Soluzioni

| Problema | Soluzione |
|----------|-----------|
| **Nessun rettangolo restituito** | Assicurati che l'immagine contenga testo chiaro e orizzontale e che `AreasType.LINES` sia specificato. |
| **Coordinate errate** | Verifica i DPI dell'immagine; immagini a bassa risoluzione possono generare limiti imprecisi. |
| **Collo di bottiglia di prestazioni su immagini grandi** | Ridimensiona l'immagine a una risoluzione ragionevole prima di chiamare `GetRectangles`. |
| **Eccezione di licenza** | Usa una licenza di prova per i test; applica una licenza completa per la produzione per evitare limiti di valutazione. |

## FAQ

### Q1: Posso usare Aspose.OCR per .NET con qualsiasi tipo di immagine?

A1: Aspose.OCR supporta un'ampia gamma di formati immagine, garantendo flessibilità nelle tue applicazioni OCR.

### Q2: Quanto è accurato il riconoscimento OCR?

A2: Aspose.OCR utilizza algoritmi avanzati per un'alta precisione, rendendolo adatto a vari scenari di riconoscimento testo.

### Q3: È disponibile una versione di prova?

A3: Sì, puoi esplorare le funzionalità di Aspose.OCR per .NET con la [versione di prova gratuita](https://releases.aspose.com/).

### Q4: Dove posso trovare la documentazione completa?

A4: Consulta la [documentazione](https://reference.aspose.com/ocr/net/) per informazioni dettagliate e linee guida d'uso.

### Q5: Hai bisogno di assistenza o hai domande specifiche?

A5: Visita il [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) per supporto della community e discussioni.

## Domande Frequenti

**D: Posso estrarre parole individuali invece di intere linee?**  
R: Sì, usa `AreasType.WORDS` con lo stesso metodo `GetRectangles` per ottenere riquadri a livello di parola.

**D: L'API supporta PDF multi‑pagina?**  
R: Converte ogni pagina PDF in immagine, poi chiama `GetRectangles` su ciascuna immagine.

**D: Come gestire testo ruotato?**  
R: Abilita l'opzione di auto‑rotazione nelle impostazioni OCR o ruota l'immagine in anticipo prima dell'elaborazione.

**D: È possibile ottenere i punteggi di confidenza per ogni linea?**  
R: Dopo aver ottenuto i rettangoli, chiama `api.RecognizeImage(...).Lines` per accedere agli oggetti linea che includono i valori di confidenza.

**D: Quali versioni di .NET sono compatibili?**  
R: La libreria funziona con .NET Framework 4.5+, .NET Core 3.1+ e .NET 5/6.

## Conclusione

Congratulazioni! Hai ottenuto con successo **i rettangoli delle linee OCR** per un'immagine usando Aspose.OCR per .NET. Con i riquadri a disposizione, ora puoi inserire le coordinate delle linee nei flussi di lavoro successivi, come rendering personalizzato, estrazione dati o analisi del layout.

---

**Ultimo aggiornamento:** 2025-12-17  
**Testato con:** Aspose.OCR 24.11 per .NET  
**Autore:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}