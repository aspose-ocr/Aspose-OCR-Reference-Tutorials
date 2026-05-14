---
date: 2026-02-22
description: Scopri come eseguire l'analisi del layout OCR riconoscendo le linee di
  testo in un'immagine ed estrarre i rettangoli delle linee utilizzando Aspose.OCR
  per .NET.
linktitle: Layout Analysis OCR – Get Line Rectangles from Images
second_title: Aspose.OCR .NET API
title: Analisi del layout OCR – Ottieni i rettangoli delle linee dalle immagini
url: /it/net/image-and-drawing-recognition/get-rectangles-for-lines/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Analisi del layout OCR – Ottenere i rettangoli delle linee da immagini

## Introduzione

In questo tutorial scoprirai **come ottenere i rettangoli delle linee OCR** con Aspose.OCR per .NET. Alla fine della guida sarai in grado di **riconoscere le linee di testo in un'immagine** e **estrarre le coordinate delle linee** per ogni linea rilevata—perfetto per l'elaborazione successiva come **analisi del layout OCR**, estrazione dati o rendering personalizzato.

## Risposte rapide
- **Cosa significa “get OCR line rectangles”?** Restituisce i riquadri di delimitazione di ogni linea di testo rilevata in un'immagine.  
- **Quale metodo API viene utilizzato?** `AsposeOcr.GetRectangles(..., AreasType.LINES, ...)`.  
- **Ho bisogno di una licenza?** Una prova gratuita funziona per lo sviluppo; è necessaria una licenza commerciale per la produzione.  
- **Formati immagine supportati?** PNG, JPEG, BMP, TIFF e altri.  
- **Posso eseguirlo su .NET Core?** Sì, Aspose.OCR supporta pienamente .NET Core e .NET 5/6.

## Prerequisiti

Prima di immergerti nel tutorial, assicurati di avere i seguenti prerequisiti:

- Conoscenza di base di C# e sviluppo .NET.  
- Un ambiente di sviluppo integrato (IDE) come Visual Studio.  
- Libreria Aspose.OCR per .NET installata. Puoi scaricarla [qui](https://releases.aspose.com/ocr/net/).  
- Un'immagine di esempio contenente testo per il riconoscimento OCR.

## Importa spazi dei nomi

Assicurati di aver importato gli spazi dei nomi necessari nel tuo progetto. Aggiungi le seguenti righe all'inizio del tuo file C#:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

Ora, scomponiamo il processo di ottenimento dei rettangoli per le linee nel riconoscimento OCR delle immagini in passaggi facili da seguire.

## analisi del layout ocr – Guida passo‑passo

### Passo 1: Configura la directory del documento

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

Sostituisci `"Your Document Directory"` con il percorso reale della cartella che contiene l'immagine di esempio.

### Passo 2: Inizializza Aspose.OCR

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

Crea un'istanza della classe `AsposeOcr` per accedere alle funzionalità OCR.

### Passo 3: Specifica il percorso dell'immagine

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

Definisci il percorso completo dell'immagine su cui eseguire l'OCR.

### Passo 4: Riconosci l'immagine e ottieni i rettangoli

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

Il metodo `GetRectangles` restituisce un elenco di oggetti `Rectangle`, ciascuno rappresentante le coordinate di una linea di testo rilevata. Questo è il fulcro di **ottenere i rettangoli delle linee OCR** e consente **l'analisi del layout OCR**.

### Passo 5: Stampa il risultato

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

Stampa le coordinate delle aree rilevate nella console. Vedrai valori che potrai successivamente utilizzare per **estrarre le coordinate delle linee** per elaborazioni personalizzate.

## Perché usare Aspose.OCR per i rettangoli delle linee?

- **Alta precisione** – Algoritmi avanzati rilevano le linee anche in immagini rumorose o inclinate.  
- **Cross‑platform** – Funziona su .NET Framework, .NET Core e .NET 5/6.  
- **Nessuna dipendenza esterna** – Libreria .NET pura, senza DLL native da distribuire.  
- **Output ricco** – Oltre ai rettangoli delle linee è possibile recuperare parole, caratteri e punteggi di confidenza.

## Problemi comuni e soluzioni

| Problema | Soluzione |
|----------|-----------|
| **Nessun rettangolo restituito** | Assicurati che l'immagine contenga testo chiaro e orizzontale e che sia specificato `AreasType.LINES`. |
| **Coordinate errate** | Verifica i DPI dell'immagine; le immagini a bassa risoluzione possono causare limiti imprecisi. |
| **Collo di bottiglia delle prestazioni su immagini grandi** | Ridimensiona l'immagine a una risoluzione ragionevole prima di chiamare `GetRectangles`. |
| **Eccezione di licenza** | Usa una licenza di prova per i test; applica una licenza completa per la produzione per evitare i limiti di valutazione. |

## Domande frequenti

**Q: Posso estrarre parole individuali invece di linee intere?**  
A: Sì, usa `AreasType.WORDS` con lo stesso metodo `GetRectangles` per ottenere riquadri a livello di parola.

**Q: L'API supporta PDF multi‑pagina?**  
A: Converti prima ogni pagina PDF in immagine, poi chiama `GetRectangles` su ciascuna immagine.

**Q: Come gestisco il testo ruotato?**  
A: Abilita l'opzione di auto‑rotazione nelle impostazioni OCR o ruota preventivamente l'immagine prima dell'elaborazione.

**Q: Esiste un modo per ottenere i punteggi di confidenza per ogni linea?**  
A: Dopo aver ottenuto i rettangoli, chiama `api.RecognizeImage(...).Lines` per accedere agli oggetti linea che includono i valori di confidenza.

**Q: Quali versioni .NET sono compatibili?**  
A: La libreria funziona con .NET Framework 4.5+, .NET Core 3.1+ e .NET 5/6.

## Casi d'uso reali

- **Analisi del layout OCR dei documenti** – Inserisci i rettangoli delle linee in un motore di layout per ricostruire le strutture delle colonne.  
- **Estrazione dati automatizzata** – Usa le coordinate per ritagliare linee individuali per pipeline NLP successive.  
- **Rendering personalizzato** – Sovrapponi i riquadri sull'immagine originale per verifica visiva o overlay UI.  

## Conclusione

Congratulazioni! Hai ottenuto con successo **i rettangoli delle linee OCR** per un'immagine usando Aspose.OCR per .NET. Con i riquadri a disposizione, ora puoi inserire le coordinate delle linee nei flussi di lavoro successivi come rendering personalizzato, estrazione dati o **analisi del layout OCR**.

---

**Ultimo aggiornamento:** 2026-02-22  
**Testato con:** Aspose.OCR 24.11 per .NET  
**Autore:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}