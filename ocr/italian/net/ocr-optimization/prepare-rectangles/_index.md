---
date: 2026-07-23
description: Scopri come estrarre testo da un'immagine usando Aspose.OCR for .NET,
  preparando rettangoli per migliorare la precisione OCR e convertire l'immagine in
  testo in modo efficiente.
keywords:
- extract text from image
- convert image to text
- improve ocr accuracy
lastmod: 2026-07-23
linktitle: Prepara rettangoli nel riconoscimento immagini OCR
og_description: Estrai testo da un'immagine usando Aspose.OCR for .NET. Scopri come
  preparare rettangoli, aumentare la precisione OCR e convertire l'immagine in testo
  in modo efficiente.
og_image_alt: Guide to extract text from image using rectangles with Aspose.OCR for
  .NET
og_title: Estrai testo da immagine con rettangoli – Guida OCR
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Learn how to extract text from image using Aspose.OCR for .NET, preparing
    rectangles to improve OCR accuracy and convert image to text efficiently.
  headline: Extract Text from Image with Rectangles – OCR Guide
  type: TechArticle
- questions:
  - answer: It converts visual characters in a picture into machine‑readable strings.
    question: What does “extract text from image” mean?
  - answer: Aspose.OCR for .NET provides a full‑featured OCR engine.
    question: Which library handles this in .NET?
  - answer: A free trial works for development; a commercial license is required for
      deployment.
    question: Do I need a license for production?
  - answer: Yes—define rectangles to target only the areas that contain useful text.
    question: Can I limit OCR to specific zones?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
    question: What .NET versions are supported?
  type: FAQPage
second_title: Aspose.OCR .NET API
tags:
- ocr
- Aspire.OCR
- .NET image processing
- extract text from image
title: Estrai testo da immagine con rettangoli – Guida OCR
url: /it/net/ocr-optimization/prepare-rectangles/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai Testo da Immagine con Rettangoli – Guida OCR

## Introduzione

Il riconoscimento ottico dei caratteri (OCR) ti consente di **estrarre testo da immagine** in modo che i file diventino ricercabili e modificabili. In questo tutorial ti mostreremo come aumentare la precisione dell'OCR preparando rettangoli personalizzati che concentrano il motore sulle zone esatte di cui hai bisogno. Utilizzando Aspose.OCR per .NET, vedrai l'intero flusso di lavoro — dalla configurazione del progetto al recupero delle stringhe riconosciute — così potrai incorporare una conversione affidabile da immagine a testo in qualsiasi applicazione .NET.

## Risposte Rapide
- **Cosa significa “estrarre testo da immagine”?** Converte i caratteri visivi in una foto in stringhe leggibili dalla macchina.  
- **Quale libreria gestisce questo in .NET?** Aspose.OCR per .NET fornisce un motore OCR completo.  
- **È necessaria una licenza per la produzione?** Una versione di prova gratuita funziona per lo sviluppo; è richiesta una licenza commerciale per il deployment.  
- **Posso limitare l'OCR a zone specifiche?** Sì — definisci rettangoli per mirare solo alle aree che contengono testo utile.  
- **Quali versioni di .NET sono supportate?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Cos'è “estrarre testo da immagine” con rettangoli?
Il processo `estrarre testo da immagine` legge i caratteri all'interno di zone rettangolari definite, ignorando tutto il resto. Limitando l'OCR a quelle zone ottieni maggiore precisione, elaborazione più veloce e meno lavoro di post‑processing. Questo approccio isola il testo di cui ti interessa mentre scarta grafiche di sfondo, elementi decorativi e altri rumori visivi che possono confondere il motore OCR.

## Perché preparare rettangoli prima dell'OCR?
Preparare i rettangoli ti consente di concentrare il motore OCR sulle parti più rilevanti di un'immagine, migliorando sia la velocità che la precisione. Riducendo l'area di analisi diminuisci la quantità di dati che il motore deve esaminare, portando a risultati più rapidi e a meno errori di riconoscimento causati da rumore visivo superfluo.

- **Concentrati sul contenuto rilevante:** Salta intestazioni, piè di pagina o grafiche decorative che confonderebbero il motore.  
- **Migliora le prestazioni:** Regioni più piccole richiedono meno calcoli, riducendo il tempo di esecuzione fino al 40 % su scansioni di grandi dimensioni.  
- **Migliora la precisione:** Ridurre il rumore visivo aumenta i tassi di riconoscimento dei caratteri dal ~85 % a >95 % su documenti rumorosi.

## Perché questo è importante per progetti reali
Molti documenti aziendali — ricevute, fatture, carte d'identità — mescolano testo con loghi o codici a barre. Disegnando rettangoli attorno ai campi di cui hai realmente bisogno, estrai solo i dati preziosi, riducendo drasticamente il lavoro di pulizia successivo e aumentando l'affidabilità dei flussi di lavoro automatizzati. Questa estrazione mirata riduce lo sforzo di post‑processing e aiuta a mantenere la conformità agli standard di gestione dei dati.

## Casi d'uso comuni
- **Automazione dell'inserimento dati:** Estrarre campi specifici da moduli scansionati o ricevute di spese.  
- **Controlli di conformità:** Isolare clausole legali o dichiarazioni normative per la verifica.  
- **Indicizzazione dei contenuti:** Indicizzare solo il titolo o la didascalia di un'immagine per la visibilità nei motori di ricerca.

## Prerequisiti

- Conoscenza di base di C# e sviluppo .NET.  
- Libreria Aspose.OCR per .NET installata – scaricala **[qui](https://releases.aspose.com/ocr/net/)** o sfoglia tutte le versioni **[qui](https://releases.aspose.com/)**.  
- Un'immagine di esempio (ad es., `sample.png`) che contiene il testo che desideri estrarre.

## Importa Namespace

Le istruzioni `using` portano il motore OCR e le classi di geometria nello scope.

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Passo 1: Configura la Cartella dei Documenti

Specifica la cartella che contiene le tue immagini e crea un'istanza del motore OCR.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Come estrarre testo da immagine usando più rettangoli
Carica l'immagine una volta, poi fornisci un elenco di rettangoli al motore OCR. Ogni rettangolo definisce una regione di interesse e il motore restituisce una stringa separata per ogni regione, consentendoti di gestire i campi individualmente e combinare i risultati secondo necessità.

### Definisci i rettangoli

`Rectangle` oggetti descrivono le coordinate X‑Y e le dimensioni di ogni zona che desideri scansionare.  

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

### Esegui il riconoscimento OCR

Il metodo `RecognizeImage` elabora l'immagine usando l'elenco di rettangoli fornito e restituisce il testo riconosciuto per ogni regione.  

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

## Come estrarre testo da immagine usando RecognitionSettings (Approccio Alternativo)
Se preferisci una chiamata basata su impostazioni, puoi ottenere lo stesso risultato con `RecognitionSettings`. Questo oggetto ti consente di raggruppare le definizioni dei rettangoli insieme a lingua, DPI e altre opzioni OCR, fornendo una chiamata API pulita a singolo parametro.

### Definisci le impostazioni di riconoscimento

`RecognitionSettings` ti permette di raggruppare l'elenco dei rettangoli e opzioni aggiuntive (ad es., lingua, DPI) in un unico oggetto.  

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

### Visualizza il testo riconosciuto

Itera sulle stringhe restituite e stampa il testo di ogni regione.  

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## Problemi Comuni & Suggerimenti

- **Coordinate del rettangolo errate:** Verifica che `X`, `Y`, `Width` e `Height` corrispondano all'area desiderata.  
- **Qualità dell'immagine:** Immagini a bassa risoluzione o fortemente compresse degradano i risultati OCR; considera pre‑processi come la binarizzazione.  
- **Risultati vuoti:** Assicurati che i rettangoli contengano effettivamente testo leggibile; altrimenti il motore restituisce stringhe vuote.

## Risoluzione dei problemi e migliori pratiche

| Sintomo | Causa Probabile | Rimedio |
|---------|-----------------|---------|
| Nessun output o stringhe vuote | Rettangoli fuori dai limiti dell'immagine | Verifica le dimensioni dell'immagine e le coordinate dei rettangoli |
| Caratteri illeggibili | Basso contrasto o rumore | Applica conversione in scala di grigi e soglia prima dell'OCR |
| Prestazioni lente su file grandi | Troppi rettangoli o immagine molto grande | Dividi l'immagine o riduci il numero di rettangoli dove possibile |

## Conclusione

Ora sai come **estrarre testo da immagine** preparando rettangoli personalizzati con Aspose.OCR per .NET. Questo approccio ti offre un controllo preciso sull'elaborazione OCR, fornendo funzionalità di estrazione del testo più rapide e accurate per qualsiasi soluzione .NET.

## Domande Frequenti

**Q:** Posso usare Aspose.OCR per .NET con altri framework .NET?  
**A:** Sì, Aspose.OCR per .NET funziona con .NET Framework 4.5+, .NET Core 3.1+, e .NET 5/6/7.

**Q:** È disponibile una versione di prova gratuita?  
**A:** Assolutamente! Scarica la versione di prova **[qui](https://releases.aspose.com/)**.

**Q:** Dove posso ottenere supporto per Aspose.OCR per .NET?  
**A:** Visita il **[forum Aspose.OCR](https://forum.aspose.com/c/ocr/16)** per assistenza dedicata.

**Q:** Posso ottenere una licenza temporanea per i test?  
**A:** Sì, una licenza temporanea è disponibile **[qui](https://purchase.aspose.com/temporary-license/)**.

**Q:** Dove si trova la documentazione ufficiale?  
**A:** Il riferimento completo dell'API è disponibile **[qui](https://reference.aspose.com/ocr/net/)**.

---

**Ultimo aggiornamento:** 2026-07-23  
**Testato con:** Aspose.OCR 24.11 per .NET  
**Autore:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Tutorial Correlati

- [Come Estrarre Rettangoli per Paragrafi nel Riconoscimento Immagini OCR](/ocr/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/)
- [Come OCR Immagine – Eseguire OCR su Immagine nel Riconoscimento Immagini OCR](/ocr/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [Come Estrarre Testo da Immagine Usando Aspose.OCR per .NET](/ocr/net/text-recognition/get-recognition-result/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}