---
category: general
date: 2026-03-26
description: Come eseguire OCR in batch in C# rende facile l'estrazione del testo
  da file PNG. Segui questo tutorial passo‑passo su OCR in C# per l'estrazione di
  testo in batch con Aspose OCR.
draft: false
keywords:
- how to batch OCR
- extract text from png
- c# ocr tutorial
- how to create OCR
- batch text extraction
language: it
og_description: Come eseguire OCR batch in C# ti consente di estrarre rapidamente
  testo da file PNG. Questa guida ti accompagna attraverso un tutorial completo di
  OCR in C# con estrazione di testo batch.
og_title: Come eseguire OCR in batch in C# – Estrarre testo da PNG
tags:
- OCR
- C#
- Aspose
title: Come eseguire OCR in batch in C# – Estrarre testo da PNG
url: /it/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR in batch in C# – Estrarre testo da PNG

Ti sei mai chiesto **come eseguire OCR in batch** su una pila di screenshot senza dover scrivere un programma separato per ogni file? Non sei solo. In molti progetti ci ritroviamo con decine di PNG da cui estrarre il testo, e farlo uno‑per‑uno è una seccatura.  

La buona notizia? Con Aspose OCR puoi creare una piccola applicazione console C# che elabora tutte quelle immagini in parallelo, offrendoti una rapida **estrazione di testo in batch** e un set di risultati pulito. In questa guida percorreremo un **c# ocr tutorial** completo, spiegheremo perché ogni pezzo è importante e ti mostreremo esattamente come appare l’output.

Alla fine di questo articolo sarai in grado di:

* Caricare un elenco di file PNG (o qualsiasi immagine supportata) in un’unica operazione.  
* Configurare un `OcrEngine` condiviso così le impostazioni rimangono coerenti per tutto il batch.  
* Eseguire la coda di riconoscimento con fino a quattro worker in parallelo.  
* Recuperare il testo riconosciuto per ogni pagina e stamparlo sulla console.

Niente magia, solo codice solido che puoi inserire nella tua soluzione oggi.

## Cosa ti serve

Prima di immergerci, assicurati di avere:

* .NET 6 SDK (o qualsiasi versione recente di .NET).  
* Una licenza valida di Aspose OCR o una chiave di valutazione temporanea.  
* Una cartella che contiene i file PNG da elaborare.  
* Visual Studio 2022 o il tuo editor preferito.

Tutto qui—nessun pacchetto NuGet aggiuntivo oltre `Aspose.OCR` e il classico `System.Collections.Generic`.

## Come eseguire OCR in batch – Configurazione del progetto

Prima di tutto, crea un nuovo progetto console e aggiungi la libreria Aspose OCR.

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

Dopo che il restore è terminato, apri **Program.cs** (o crea un nuovo file) e aggiungi le consuete direttive `using`:

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
```

Questa semplice struttura ci dà accesso a `OcrEngine`, `RecognitionQueue` e alle classi di supporto di cui avremo bisogno più avanti.

## Estrarre testo da PNG – Preparare l’elenco delle immagini

Ora dobbiamo indicare al programma **quali PNG** far passare attraverso l’OCR. Il modo più diretto è costruire una `List<string>` che contenga percorsi assoluti o relativi.

```csharp
// Step 1: Define the image files to be processed
var imagePaths = new List<string>
{
    @"YOUR_DIRECTORY/page1.png",
    @"YOUR_DIRECTORY/page2.png",
    @"YOUR_DIRECTORY/page3.png",
    @"YOUR_DIRECTORY/page4.png"
};
```

Sostituisci `YOUR_DIRECTORY` con il percorso reale della cartella. Se hai un set dinamico, potresti anche usare `Directory.GetFiles(@"YOUR_DIRECTORY", "*.png")` e inserire il risultato nella lista. Il punto chiave è che **estrarre testo da PNG** è semplicemente una questione di fornire i nomi dei file corretti alla coda.

![How to batch OCR workflow](https://example.com/placeholder.png "Diagram illustrating how to batch OCR a collection of PNG files")

*Testo alternativo immagine: diagramma del flusso di lavoro OCR in batch*

## C# OCR tutorial – Configurare la coda di riconoscimento

Il cuore dell’operazione batch è il `RecognitionQueue`. Pensalo come un nastro trasportatore che consegna ogni immagine a un `OcrEngine` condiviso. Condividendo il motore manteniamo basso l’uso di memoria e garantiamo impostazioni identiche per ogni pagina.

```csharp
// Step 2: Create a recognition queue with shared OCR engine and parallelism
var recognitionQueue = new RecognitionQueue
{
    MaxDegreeOfParallelism = 4,          // run up to 4 images at the same time
    Engine = new OcrEngine()            // shared configuration for all images
};
```

Perché impostare `MaxDegreeOfParallelism` a 4? Su un tipico laptop quad‑core questo offre la migliore velocità senza sovraccaricare il sistema operativo. Se esegui il codice su un server con più core, aumenta il valore di conseguenza.

### Consiglio professionale

Se ti servono pacchetti linguistici personalizzati, impostazioni DPI o ritaglio di regioni di interesse, fallo **una sola volta** sul `Engine` condiviso prima di accodare le immagini. Per esempio:

```csharp
recognitionQueue.Engine.Language = Language.English;
recognitionQueue.Engine.Dpi = 300;
```

Tutte le successive riconoscenze ereditano automaticamente queste opzioni—questa è l’essenza di **come creare pipeline OCR** coerenti.

## Estrazione di testo in batch – Accodare le immagini ed eseguire la coda

Con la coda pronta, il passo successivo è inserire ogni immagine. Il metodo `Enqueue` accetta un’istanza `OcrImage`, che creiamo a partire da un percorso file.

```csharp
// Step 3: Enqueue each image for OCR processing
foreach (var path in imagePaths)
    recognitionQueue.Enqueue(OcrImage.FromFile(path));
```

Una volta che tutti i file sono in coda, avviamo l’elaborazione:

```csharp
// Step 4: Run the queue and collect OCR results
List<OcrResult> ocrResults = recognitionQueue.ExecuteAll();
```

`ExecuteAll` blocca l’esecuzione finché ogni immagine non termina, poi restituisce una lista in cui ogni elemento corrisponde all’ordine di input. Questo garantisce che il risultato della pagina 1 sia all’indice 0, della pagina 2 all’indice 1, e così via—pratico quando devi mappare i risultati ai file originali.

## Come creare OCR – Visualizzare i risultati

Infine, stampiamo il testo riconosciuto sulla console. È qui che vedrai davvero la **estrazione di testo in batch** in azione.

```csharp
// Step 5: Output the recognized text for each page
for (int i = 0; i < ocrResults.Count; i++)
{
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(ocrResults[i].Text);
}
```

Quando esegui il programma (`dotnet run`), dovresti vedere qualcosa del genere:

```
--- Page 1 ---
Welcome to the quarterly report.
--- Page 2 ---
Revenue increased by 12% YoY.
--- Page 3 ---
All figures are provisional.
--- Page 4 ---
Contact finance@example.com for details.
```

Se qualche immagine fallisce (ad es., file corrotto), il relativo `OcrResult` avrà una proprietà `Text` vuota e potrai ispezionare `ocrResults[i].Exception` per i dettagli diagnostici.

## Come creare OCR – Suggerimenti, casi limite e buone pratiche

### Gestire batch di grandi dimensioni

Elaborare centinaia di PNG può comunque consumare memoria se mantieni tutti gli oggetti `OcrResult` in vita. In questi casi, scrivi l’output su file o database non appena arriva ogni risultato:

```csharp
recognitionQueue.OnResultReady += (sender, args) =>
{
    File.AppendAllText("OcrOutput.txt",
        $"--- {args.Image.Path} ---{Environment.NewLine}{args.Result.Text}{Environment.NewLine}");
};
```

### Lavorare con formati non‑PNG

Aspose OCR supporta anche JPEG, BMP e TIFF nativamente. Basta cambiare l’estensione del file nella tua lista o usare una ricerca con wildcard. Gli stessi passaggi del **c# ocr tutorial** si applicano—nessuna modifica al codice necessaria.

### Saltare pagine vuote

Se hai PDF scansionati che a volte contengono pagine bianche, puoi filtrare i risultati:

```csharp
if (!string.IsNullOrWhiteSpace(result.Text))
    // process non‑empty text
```

### Considerazioni sulla licenza

La versione di valutazione aggiunge un watermark a ogni pagina. Per l’uso in produzione, assicurati di incorporare il file di licenza all’inizio di `Main`:

```csharp
License lic = new License();
lic.SetLicense("Aspose.OCR.lic");
```

### Ottimizzazione del parallelismo

`MaxDegreeOfParallelism` di default è `Environment.ProcessorCount`. Se noti un uso eccessivo della CPU o pressione sulla memoria, riduci il valore. Al contrario, su una VM cloud con molti core, aumentalo per sfruttare al massimo l’hardware.

## Riepilogo

Ora disponi di una soluzione completa **come eseguire OCR in batch** in C# che può **estrarre testo da PNG**, elaborarlo in parallelo e restituire risultati ordinati e puliti. Condividendo un unico `OcrEngine` hai appreso **come creare pipeline OCR** efficienti in termini di memoria e facili da mantenere. Questo **c# ocr tutorial** mostra anche come scalare l’**estrazione di testo in batch** a centinaia di immagini con poche righe aggiuntive.

---

### Qual è il prossimo passo?

* Prova ad aggiungere il rilevamento della lingua (`Engine.Language = Language.AutoDetect`).  
* Sperimenta con formati di output—scrivi i risultati in JSON o CSV per analisi successive.  
* Combina questo OCR batch con una fase di conversione PDF‑to‑image per elaborare documenti scansionati interi.

Sentiti libero di regolare il parallelismo, sostituire le tue fonti di immagini o collegare i risultati a un indice di ricerca. Il cielo è il limite quando domini **come eseguire OCR in batch** in C#.

Buon coding, e che le tue esecuzioni OCR siano veloci e prive di errori!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}