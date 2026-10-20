---
category: general
date: 2026-04-04
description: Come abilitare rapidamente la GPU in Aspose OCR. Impara a estrarre il
  testo da un'immagine, caricare l'immagine per l'OCR e riconoscere il testo usando
  C#.
draft: false
keywords:
- how to enable gpu
- extract text from image
- how to extract text
- how to recognize text
- load image for ocr
language: it
og_description: Come abilitare rapidamente la GPU in Aspose OCR. Segui questo tutorial
  per estrarre il testo da un'immagine, caricare l'immagine per l'OCR e riconoscere
  il testo con C#.
og_title: Come abilitare la GPU per l'OCR in C# – Guida completa
tags:
- Aspose OCR
- C#
- GPU acceleration
title: Come abilitare la GPU per l'OCR in C# – Guida passo‑passo
url: /it/net/ocr-configuration/how-to-enable-gpu-for-ocr-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come abilitare la GPU per l'OCR in C# – Guida completa

Ti sei mai chiesto **come abilitare la GPU** quando usi Aspose OCR? Forse hai incontrato un collo di bottiglia di prestazioni elaborando centinaia di ricevute, e la CPU non riesce a tenere il passo. La buona notizia è che attivare l'accelerazione GPU è un gioco da ragazzi, e una volta attivata vedrai il motore OCR elaborare le immagini a velocità fulminea.

In questo tutorial non solo attiveremo l'interruttore GPU, ma ti mostreremo anche come **caricare un'immagine per l'OCR**, **riconoscere il testo**, e infine **estrarre il testo dall'immagine** usando un esempio chiaro in C#. Alla fine avrai un programma pronto all'uso che estrae testo semplice da qualsiasi immagine supportata—senza servizi esterni.

## Cosa ti serve

- .NET 6+ (o .NET Framework 4.7.2 e successive).  
- Aspose.OCR per .NET, versione 24.2.0 o più recente (il flag GPU è stato aggiunto in questa release).  
- Una macchina con GPU abilitata e i driver appropriati (NVIDIA CUDA 11+ funziona benissimo).  
- Un file immagine da elaborare—ad esempio una ricevuta scannerizzata, una fattura fotografata o una nota scritta a mano.

Se hai già tutto questo, ottimo—tuffiamoci.

## Passo 1: Come abilitare la GPU – Configurare il motore OCR

La prima cosa da fare è dire ad Aspose OCR di usare la GPU. Questo si ottiene impostando la proprietà `UseGpu` sull'istanza `OcrEngine`. La proprietà è impostata di default su `false`, quindi la attiviamo esplicitamente.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // <-- GPU module namespace

// Create the OCR engine and enable GPU acceleration (available from version 24.2.0)
var ocrEngine = new OcrEngine
{
    // Enabling GPU can speed up recognition by 2‑5× on a modern card
    UseGpu = true
};
```

**Perché è importante:** Quando `UseGpu` è `true`, la libreria delega i calcoli matriciali pesanti al processore grafico. Su una modesta RTX 3060 noterai la latenza scendere da diversi secondi per immagine a una frazione di secondo.

> **Consiglio:** Se esegui il codice in un ambiente CI senza interfaccia grafica, assicurati che il driver GPU sia installato e che l'account di servizio abbia i permessi per accedere al dispositivo. Altrimenti il motore tornerà silenziosamente alla modalità CPU.

## Passo 2: Caricare immagine per OCR – Puntare il motore al tuo file

Ora dobbiamo **caricare immagine per OCR**. Aspose OCR accetta qualsiasi formato immagine supportato da System.Drawing (PNG, JPEG, BMP, TIFF, ecc.). L'helper `ImageStream.FromFile` avvolge il file nello stream richiesto.

```csharp
// Replace the path with the location of your receipt or document
string imagePath = @"C:\MyImages\receipt.jpg";

ocrEngine.Image = ImageStream.FromFile(imagePath);
```

Se preferisci caricare da un `byte[]` (ad esempio quando l'immagine proviene da un database), puoi usare `ImageStream.FromBytes(byteArray)` al suo posto—stesso risultato, solo una sorgente diversa.

## Passo 3: Come riconoscere il testo – Eseguire il processo OCR

Ora che il motore è configurato e l'immagine è caricata, è il momento di **riconoscere il testo**. Il metodo `Recognize` esegue tutto il lavoro pesante e restituisce un oggetto `OcrResult` che contiene il testo semplice, i punteggi di confidenza e persino le bounding box se ti servono in seguito.

```csharp
// Run the recognition process (English is the default language)
OcrResult ocrResult = ocrEngine.Recognize();
```

Puoi anche cambiare la lingua impostando `ocrEngine.Language = OcrLanguage.French;` prima di chiamare `Recognize()`. L'accelerazione GPU funziona indipendentemente dal pacchetto lingua caricato.

## Passo 4: Come estrarre testo dall'immagine – Restituire il risultato

Infine **estraiamo il testo dall'immagine** leggendo la proprietà `Text` dell'oggetto risultato. Per scopi dimostrativi lo stamperemo semplicemente sulla console, ma potresti scriverlo su un file, su un database o inviarlo a un altro servizio.

```csharp
// Output the extracted plain‑text to the console
Console.WriteLine("=== OCR RESULT ===");
Console.WriteLine(ocrResult.Text);
```

**Output previsto** (il tuo testo reale varierà in base all'immagine):

```
=== OCR RESULT ===
Store: Coffee Corner
Date: 03/28/2026
Item          Qty   Price
Latte          2    $5.00
Muffin         1    $2.50
Total                 $12.50
```

Se ti servono i valori di confidenza grezzi, puoi iterare `ocrResult.Regions` e ispezionare ogni `Region.Confidence`.

## Esempio completo funzionante – Un solo file, pronto da eseguire

Di seguito trovi il programma completo. Copialo in un nuovo progetto console, ripristina il pacchetto NuGet Aspose.OCR e premi **F5**.

```csharp
// ------------------------------------------------------------
// How to enable gpu for OCR in C# – Complete Example
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU module namespace

class Program
{
    static void Main()
    {
        // -------- Step 1: Enable GPU ----------
        var ocrEngine = new OcrEngine
        {
            UseGpu = true   // <-- crucial for acceleration
        };

        // -------- Step 2: Load image ----------
        // Make sure the file exists; otherwise an exception is thrown.
        string imagePath = @"YOUR_DIRECTORY/receipt.jpg";
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // -------- Step 3: Recognize text -------
        OcrResult ocrResult = ocrEngine.Recognize();

        // -------- Step 4: Extract text ----------
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Nota:** Sostituisci `YOUR_DIRECTORY/receipt.jpg` con il percorso reale della tua immagine. Se il programma genera una `FileNotFoundException`, verifica il percorso e i permessi del file.

## Domande frequenti & casi particolari

### E se la GPU non viene rilevata?

Aspose OCR tornerà automaticamente alla modalità CPU e registrerà un avviso. Per verificare quale modalità è attiva, controlla `ocrEngine.IsGpuEnabled` dopo la creazione—restituisce `true` solo quando il driver GPU è stato caricato correttamente.

### Posso elaborare più immagini in un ciclo?

Assolutamente. Basta spostare la riga `ocrEngine.Image = …` all'interno di un ciclo `foreach (var file in files)`. Mantieni la stessa istanza di `OcrEngine`; riutilizzarla evita l'overhead di allocare ripetutamente le risorse GPU.

```csharp
foreach (var file in Directory.GetFiles(@"C:\MyImages", "*.jpg"))
{
    ocrEngine.Image = ImageStream.FromFile(file);
    var result = ocrEngine.Recognize();
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text.Length} characters");
}
```

### Come gestisco lingue non inglesi?

Imposta la lingua prima di chiamare `Recognize()`:

```csharp
ocrEngine.Language = OcrLanguage.Spanish;   // or any supported language enum
```

L'accelerazione GPU funziona allo stesso modo; cambia solo il modello linguistico.

### E per foto grandi ad alta risoluzione?

Se incontri errori di out‑of‑memory, ridimensiona prima l'immagine. Aspose OCR fornisce `ImageHelper.Resize`—un modo rapido per ridurre le dimensioni senza perdere troppi dettagli.

```csharp
ocrEngine.Image = ImageHelper.Resize(
    ImageStream.FromFile(imagePath), 
    maxWidth: 2000, 
    maxHeight: 2000);
```

## Conclusione

Abbiamo coperto **come abilitare la GPU** per Aspose OCR, mostrato come **caricare immagine per OCR**, illustrato **come riconoscere il testo**, e dimostrato **come estrarre testo dall'immagine** con un programma C# conciso e pronto per la produzione. Attivando il flag `UseGpu` ottieni un notevole incremento di velocità, soprattutto quando elabori lotti di ricevute, fatture o qualsiasi flusso di documenti ad alto volume.

Pronto per il passo successivo? Prova a collegare questa pipeline OCR a un database per archiviare le ricevute estratte, o a inviare il testo semplice a un modello di elaborazione del linguaggio naturale per la categorizzazione delle spese. Puoi anche esplorare la collezione `OcrResult.Regions` per ottenere le coordinate delle bounding box e costruire un'interfaccia che evidenzi ogni parola sull'immagine originale.

Buona programmazione, e goditi la potenza extra che l'accelerazione GPU porta ai tuoi carichi di lavoro OCR!

---

![how to enable gpu illustration](gpu-ocr-diagram.png "how to enable gpu illustration")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}