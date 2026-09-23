---
category: general
date: 2026-02-14
description: Carica il file immagine ed estrai il testo dalla ricevuta usando il motore
  OCR GPU di Aspose. Impara a impostare la memoria GPU massima, configurare la memoria
  GPU ed eseguire l'OCR sull'immagine in modo efficiente.
draft: false
keywords:
- load image file
- extract text from receipt
- set max gpu memory
- run OCR on image
- configure gpu memory
language: it
og_description: Carica il file immagine ed estrai il testo dalla ricevuta usando il
  motore OCR GPU di Aspose. Questa guida mostra come impostare la memoria GPU massima
  ed eseguire l'OCR sull'immagine in C#.
og_title: Carica file immagine e estrai il testo della ricevuta con OCR GPU in C#
tags:
- C#
- OCR
- Aspose
- GPU
title: Carica file immagine e estrai il testo della ricevuta con OCR GPU in C#
url: /it/net/ocr-configuration/load-image-file-extract-receipt-text-with-gpu-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Carica file immagine ed estrai il testo della ricevuta con OCR GPU in C#

Hai mai avuto bisogno di **load image file** e di estrarre il testo esatto da una ricevuta ma ti sei bloccato al passaggio OCR? Non sei l'unico. In molte app reali—tracciatori di spese, sistemi di inventario o anche semplici bot di scansione ricevute—la capacità di leggere rapidamente un'immagine di ricevuta può fare la differenza.  

La buona notizia? Con il motore GPU‑accelerated di Aspose.OCR puoi **load image file**, **set max GPU memory** e **run OCR on image** in poche linee pulite di C#. Di seguito percorreremo l'intero processo, dalla configurazione della GPU alla stampa del testo semplice estratto.

## Cosa imparerai

* **Load image file** dal disco usando `ImageStream` di Aspose.  
* **Configure GPU memory** così che il motore non consumi più RAM di quanto tu consenta.  
* **Run OCR on image** ed estrarre ogni carattere da una ricevuta.  
* Gestisci le insidie comuni—come errori out‑of‑memory o scansioni sfocate.  
* Verifica l'output e regola le impostazioni per una maggiore precisione.

Nessun servizio esterno, nessun trucco oscuro—solo puro codice C# che puoi inserire in qualsiasi progetto .NET 6+.

---

## Prerequisiti

Prima di immergerti, assicurati di avere:

* .NET 6 SDK o versioni successive installate.  
* Una licenza valida di Aspose.OCR (oppure puoi usare la modalità di valutazione gratuita).  
* I pacchetti NuGet `Aspose.OCR` e `Aspose.OCR.Gpu` aggiunti al tuo progetto.  
* Un'immagine di esempio di ricevuta (`receipt.png`) pronta su disco.

Se qualcuno di questi ti è sconosciuto, fermati un attimo e installa i pacchetti:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

Tutto qui—nessuna libreria nativa aggiuntiva è necessaria perché il supporto GPU è integrato direttamente nel pacchetto NuGet.

---

## Carica file immagine e prepara il motore GPU

La prima cosa da fare è **load image file** in un `ImageStream`. Questo oggetto astrae i dettagli del file‑system e fornisce al motore OCR una rappresentazione pulita, in memoria.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;

// Step 1️⃣: Initialize the GPU‑accelerated engine.
var gpuEngine = new GpuEngine
{
    // Step 2️⃣: Set a safety net for GPU RAM usage.
    // Here we limit the engine to 1024 MB (1 GB). Adjust as needed.
    MaxDeviceMemory = 1024 // MB
};

// Step 3️⃣: Load the receipt image from disk.
var receiptImage = ImageStream.FromFile(@"C:\MyReceipts\receipt.png");

// At this point the image is ready for OCR.
```

**Perché è importante:**  
*Loading the image file* tramite `ImageStream.FromFile` garantisce che il motore veda i dati pixel esatti, preservando DPI e profondità colore. Saltare questo passaggio o fornire uno stream corrotto farà sì che l'OCR perda caratteri o lanci eccezioni.

> **Consiglio pro:** Se gestisci file caricati dagli utenti, avvolgi la chiamata `FromFile` in un blocco try‑catch e valida prima la dimensione del file. Immagini grandi possono saturare la memoria GPU se non hai **configured GPU memory** correttamente.

---

## Imposta la memoria massima GPU per prestazioni ottimali

Le risorse GPU sono preziose, specialmente su server condivisi o laptop con VRAM limitata. La proprietà `MaxDeviceMemory` indica ad Aspose quanta memoria della GPU può allocare in modo sicuro.

```csharp
// Example: Restrict to 512 MB for low‑end GPUs.
gpuEngine.MaxDeviceMemory = 512; // MB
```

Quando **set max GPU memory**, il motore tornerà automaticamente all'elaborazione CPU se non può soddisfare la richiesta—evitando crash. Questo è il modo più sicuro per **configure GPU memory** senza codificare a mano limiti specifici del dispositivo.

**Quando regolare:**  
* Se noti `OutOfMemoryException` durante un'elaborazione batch intensiva, abbassa il limite.  
* Se le tue ricevute sono ad alta risoluzione (300 DPI+), aumentalo a 2 GB per mantenere alta la velocità.

---

## Esegui OCR sull'immagine per estrarre il testo dalla ricevuta

Ora la parte divertente—effettivamente **run OCR on image** ed estrarre il testo della ricevuta. Il metodo `Recognize` restituisce un oggetto `OcrResult` che contiene una proprietà `Text` con l'output in plain‑text.

```csharp
// Step 4️⃣: Perform OCR.
OcrResult ocrResult = gpuEngine.Recognize(receiptImage);

// Step 5️⃣: Output the extracted text.
Console.WriteLine("=== Receipt Text ===");
Console.WriteLine(ocrResult.Text);
```

La console visualizzerà qualcosa di simile:

```
=== Receipt Text ===
Store: Coffee Corner
Date: 02/13/2026
Item            Qty   Price
Latte           2     $5.00
Muffin          1     $2.50
Total                     $12.50
```

**Perché funziona:**  
Il motore GPU esegue un modello deep‑learning addestrato su una varietà di layout di documenti. Fornendo un'immagine pulita e correttamente caricata, dai al modello la migliore possibilità di **extract text from receipt** accuratamente.

---

## Verifica l'output e le insidie comuni

Anche con un motore potente, l'OCR non è magia. Ecco alcune cose a cui fare attenzione:

| Problema | Causa | Soluzione |
|----------|-------|-----------|
| Caratteri distorti | Basso contrasto o immagine sfocata | Pre‑processa con `ImageProcessor` di Aspose per aumentare il contrasto |
| Linee mancanti | Immagine ritagliata troppo strettamente | Assicurati che la ricevuta sia interamente entro i bordi dell'immagine |
| Errori out‑of‑memory | `MaxDeviceMemory` troppo basso per la dimensione dell'immagine | Aumenta `MaxDeviceMemory` o ridimensiona prima l'immagine |
| Lingua errata | La ricevuta contiene testo non‑inglese | Imposta `gpuEngine.Language = OcrLanguage.Spanish;` (o appropriato) |

Se incontri uno di questi problemi, la soluzione rapida è ridimensionare l'immagine a meno di 2000 px sul lato più lungo—ciò riduce drasticamente la pressione sulla GPU senza sacrificare la leggibilità per la maggior parte delle ricevute.

---

## Esempio completo funzionante (pronto per copia‑incolla)

Di seguito trovi l'intero programma, pronto per la compilazione. Sostituisci il percorso del file con la posizione della tua ricevuta.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

class ReceiptOcrDemo
{
    static void Main()
    {
        // 1️⃣ Create GPU‑accelerated engine with a safe memory cap.
        var gpuEngine = new GpuEngine
        {
            MaxDeviceMemory = 1024 // MB – adjust for your hardware
        };

        // 2️⃣ Load the receipt image from disk.
        //    Make sure the path points to a valid PNG/JPEG file.
        var receiptImage = ImageStream.FromFile(@"C:\MyReceipts\receipt.png");

        // 3️⃣ Run OCR – this will automatically use the GPU if available.
        OcrResult ocrResult = gpuEngine.Recognize(receiptImage);

        // 4️⃣ Print the extracted text.
        Console.WriteLine("=== Receipt Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Output console previsto** (la tua ricevuta sarà diversa, ovviamente):

```
=== Receipt Text ===
Store: Coffee Corner
Date: 02/13/2026
Item            Qty   Price
Latte           2     $5.00
Muffin          1     $2.50
Total                     $12.50
```

Esegui il programma con `dotnet run`. Se vedi il testo stampato, congratulazioni—hai completato con successo **load image file**, **set max GPU memory** e **run OCR on image** per **extract text from receipt**.

---

## Domande frequenti

**Q: Funziona su macchine senza GPU dedicata?**  
A: Sì. Aspose.OCR tornerà elegantemente alla modalità CPU se non viene rilevata una GPU compatibile. Potrai comunque **load image file** e **run OCR on image**, solo un po' più lentamente.

**Q: Posso elaborare più ricevute in batch?**  
A: Assolutamente. Avvolgi il codice di riconoscimento in un ciclo `foreach`, ma ricorda di riutilizzare la stessa istanza `GpuEngine`—questo evita di reinizializzare le risorse GPU per ogni file.

**Q: E se la mia ricevuta è in una lingua diversa dall'inglese?**  
A: Imposta la lingua prima di chiamare `Recognize`:

```csharp
gpuEngine.Language = OcrLanguage.French;
```

---

## Prossimi passi e argomenti correlati

Ora che hai padroneggiato le basi, considera di esplorare:

* **Fine‑tuning OCR accuracy** – sperimenta con `gpuEngine.RecognitionOptions` come `EnableDeskew` o `ContrastEnhancement`.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}