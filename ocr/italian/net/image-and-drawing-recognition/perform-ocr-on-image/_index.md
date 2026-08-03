---
date: 2026-02-22
description: Scopri come eseguire l'OCR di un'immagine ed estrarre il testo dell'immagine
  con Aspose.OCR per .NET. Questa guida passo passo ti mostra come convertire rapidamente
  un'immagine in testo.
linktitle: Perform OCR on Image in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: Come fare OCR su un'immagine – Eseguire OCR su un'immagine nel riconoscimento
  OCR delle immagini
url: /it/net/image-and-drawing-recognition/perform-ocr-on-image/
weight: 14
---

.

Proceed.

Let's write.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR su un'immagine – Eseguire OCR su un'immagine nel riconoscimento OCR

## Introduzione

Nelle applicazioni moderne, **come eseguire OCR su un'immagine** è una domanda comune per gli sviluppatori che devono trasformare documenti scansionati, screenshot o foto in testo ricercabile e modificabile. Aspose.OCR per .NET offre un'API potente e facile da usare che consente di **estrarre testo da un'immagine**, **convertire immagine in testo** e **riconoscere testo nell'immagine** con poche righe di codice. In questo tutorial percorreremo l'intero processo—dalla configurazione della libreria alla visualizzazione del testo riconosciuto—così potrai integrare le funzionalità OCR nei tuoi progetti C# in pochi minuti.

## Risposte rapide
- **Quale libreria devo usare?** Aspose.OCR per .NET
- **Posso elaborare PNG, JPEG e TIFF?** Sì, tutti i formati immagine più comuni sono supportati
- **È necessaria una licenza per la produzione?** Sì, è richiesta una licenza commerciale per l'uso in produzione
- **Quali versioni di .NET sono compatibili?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6
- **Quanto tempo impiega una chiamata OCR di base?** Tipicamente meno di un secondo per un'immagine di dimensioni standard

## Che cos'è l'estrazione di testo da immagine OCR?

L'estrazione di testo da immagine OCR (Optical Character Recognition) è il processo di analisi di un'immagine bitmap, identificazione dei caratteri e output come testo modificabile. Questa tecnica alimenta tutto, dai PDF ricercabili all'inserimento automatico dei dati da ricevute.

## Perché scegliere Aspose.OCR come libreria OCR per C#?

- **Alta precisione** – I modelli linguistici integrati forniscono risultati affidabili anche su scansioni di bassa qualità.  
- **Ampio supporto di formati** – Gestisce PNG, JPEG, BMP, TIFF e altri, rendendo facile **convertire immagine in testo** indipendentemente dalla sorgente.  
- **Nessuna dipendenza esterna** – Libreria .NET pura; non è necessario installare motori OCR nativi.  
- **Estensibile** – Puoi affinare le impostazioni di riconoscimento o integrarla con altri prodotti Aspose per flussi di lavoro documentali end‑to‑end.

## Prerequisiti

Prima di immergerti nel codice, assicurati di avere:

1. **Libreria Aspose.OCR per .NET** – Scaricala e installala dal [link di download](https://releases.aspose.com/ocr/net/).  
2. **Ambiente di sviluppo** – Qualsiasi IDE compatibile con .NET (Visual Studio, Rider, VS Code, ecc.).  
3. **Un'immagine di esempio** – Per questa guida useremo `sample.png` posizionata in una cartella a tua scelta.

## Importare gli spazi dei nomi

Per prima cosa, aggiungi gli spazi dei nomi necessari affinché il compilatore sappia dove trovare le classi OCR:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

## Come eseguire OCR su un'immagine usando Aspose.OCR per .NET

Di seguito il flusso end‑to‑end suddiviso in passaggi numerati chiari. Ogni passaggio include una breve spiegazione seguita dal codice esatto da copiare.

### Passo 1: Specificare la directory del documento

```csharp
string dataDir = "Your Document Directory";
```

Sostituisci `"Your Document Directory"` con il percorso assoluto o relativo che contiene `sample.png`. Questo indica all'API dove cercare l'immagine da elaborare.

### Passo 2: Inizializzare Aspose.OCR

```csharp
AsposeOcr api = new AsposeOcr();
```

Creare un'istanza di `AsposeOcr` ti dà accesso a tutti i metodi OCR, come `RecognizeImage`.

### Passo 3: Riconoscere l'immagine

```csharp
string result = api.RecognizeImage(dataDir + "sample.png");
```

Il metodo `RecognizeImage` legge il file immagine e restituisce il testo estratto come stringa. È qui che avviene il lavoro pesante—**riconoscere testo nell'immagine**.

### Passo 4: Visualizzare il testo riconosciuto

```csharp
Console.WriteLine(result);
```

Puoi stampare il risultato sulla console, scriverlo su un file o passarlo a un altro componente per ulteriori elaborazioni.

### Passo 5: Finalizzare il processo

```csharp
Console.WriteLine("PerformOCROnImage executed successfully");
```

Un semplice messaggio di conferma ti aiuta a verificare che la chiamata OCR sia terminata senza eccezioni.

## Convertire immagine in testo .NET – Suggerimenti aggiuntivi

- **Usa `Path.Combine`** per costruire i percorsi dei file in modo sicuro su tutte le piattaforme.  
- **Imposta la lingua** se elabori testo non inglese: `api.Language = "eng";` (o il codice ISO appropriato).  
- **Regola la qualità dell'immagine** pre‑elaborandola (ad es., ridimensionamento, binarizzazione) per migliorare la precisione su scansioni a bassa risoluzione.

## Problemi comuni e risoluzione

| Sintomo | Causa probabile | Correzione |
|---------|-----------------|------------|
| Stringa vuota restituita | Percorso dell'immagine errato o file non trovato | Verifica `dataDir` e il nome file; usa `Path.Combine` per sicurezza |
| Caratteri illeggibili | Risoluzione dell'immagine troppo bassa o lingua non supportata | Usa un'immagine a risoluzione più alta; imposta le opzioni lingua tramite `api.Language = "eng"` |
| Eccezione `System.IO.FileNotFoundException` | `sample.png` mancante | Assicurati che il file esista nella cartella specificata |

## Domande frequenti

**D: Aspose.OCR può gestire più formati immagine?**  
R: Sì, supporta un'ampia gamma di formati, così puoi **estrarre testo da un'immagine** da PNG, JPEG, BMP, TIFF e altri.

**D: È disponibile una licenza temporanea per scopi di test?**  
R: Assolutamente. Puoi richiedere una licenza di valutazione di 30 giorni dal portale Aspose.

**D: Dove posso trovare la documentazione completa per Aspose.OCR per .NET?**  
R: La guida ufficiale è la [documentazione Aspose.OCR](https://reference.aspose.com/ocr/net/).

**D: Come posso ottenere supporto o entrare in contatto con la community per assistenza?**  
R: Visita il [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) per porre domande e condividere esperienze.

**D: Posso provare Aspose.OCR per .NET gratuitamente prima di acquistare?**  
R: Sì, è disponibile una **prova gratuita** completa nella pagina del [free trial](https://releases.aspose.com/).

## Conclusione

Seguendo i passaggi sopra, ora sai **come eseguire OCR su un'immagine** usando Aspose.OCR per .NET. Che tu stia costruendo un sistema di gestione documenti, un'app di elaborazione ricevute o qualsiasi soluzione che richieda di **convertire immagine in testo**, questa libreria offre un percorso semplice e ad alte prestazioni per trasformare dati visivi in contenuti ricercabili.

---

**Ultimo aggiornamento:** 2026-02-22  
**Testato con:** Aspose.OCR per .NET 24.12 (ultima versione al momento della stesura)  
**Autore:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}