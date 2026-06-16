---
category: general
date: 2026-03-29
description: Riconosci il testo da un'immagine usando il motore OCR GPU di Aspose
  – estrai il testo dai file TIFF in modo rapido ed efficiente.
draft: false
keywords:
- recognize text from image
- extract text from tiff
language: it
og_description: Riconosci il testo dalle immagini istantaneamente con Aspose OCR GPU
  in C#. Impara a estrarre il testo dai file TIFF, configurare i dispositivi e evitare
  gli errori più comuni.
og_title: Riconoscere il testo da un'immagine con Aspose OCR GPU – Guida completa
tags:
- OCR
- C#
- Aspose
- GPU
title: Riconoscere il testo da un'immagine con Aspose OCR GPU in C#
url: /it/net/ocr-optimization/recognize-text-from-image-with-aspose-ocr-gpu-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Riconoscere il testo da immagine con Aspose OCR GPU – Guida completa

Ti è mai capitato di **recognize text from image** ma il file era un enorme TIFF ad alta risoluzione? Non sei solo. In molti progetti reali, la scansione di archivi o l'elaborazione di fatture ti lascia con enormi file .tif che le librerie OCR tradizionali non riescono a gestire.  

Fortunatamente, il motore GPU di Aspose OCR può **recognize text from image** in un attimo, e scarica automaticamente i pacchetti lingua quando ne hai bisogno. In questo tutorial ti mostreremo anche come **extract text from tiff** senza sforare il tuo budget di memoria.

## Cosa ti servirà

- .NET 6 (o qualsiasi runtime .NET recente) – il codice funziona anche su .NET Core.  
- Pacchetto NuGet Aspose.OCR per .NET (versione 23.10 o successiva).  
- Una GPU con almeno 2 GB di VRAM – opzionale ma altamente consigliata per scansioni di grandi dimensioni.  

Se non hai una GPU, il motore CPU funzionerà comunque; basta sostituire `GpuOcrEngine` con `OcrEngine`.  

## Installa Aspose OCR per .NET

Per prima cosa, aggiungi la libreria al tuo progetto:

```bash
dotnet add package Aspose.OCR
```

## Passo 1: Inizializzare il motore GPU OCR

Per **recognize text from image** sulla GPU, crea un'istanza di `GpuOcrEngine`. Questo oggetto comunica direttamente con il driver grafico, così ottieni enormi velocità su file raster di grandi dimensioni.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU engine namespace

// Create a GPU‑accelerated OCR engine
var ocrEngine = new GpuOcrEngine();
```

> **Perché è importante:** Il motore GPU delega i pesanti calcoli matriciali alla scheda grafica, il che è particolarmente utile quando l'immagine di origine è un TIFF ad alta risoluzione (ad esempio 3000 × 4000 px o più).

## Passo 2: (Opzionale) Selezionare il dispositivo GPU e limitare la memoria

Se la tua macchina ha più GPU, puoi sceglierne una tramite il suo `DeviceId`. Puoi anche limitare la VRAM che il motore può allocare—utile su server condivisi.

```csharp
// Choose the first GPU (ID 0) – change if you have more than one
ocrEngine.DeviceId = 0;

// Reserve at most 2 GB of VRAM for this OCR session
ocrEngine.MaxMemoryInMb = 2048;
```

> **Consiglio professionale:** Quando elabori decine di pagine in batch, mantieni `MaxMemoryInMb` leggermente inferiore alla memoria totale della scheda per evitare crash per esaurimento della memoria.

## Passo 3: Scegliere la lingua (e scaricare automaticamente se necessario)

Aspose OCR include l'inglese di default, ma puoi richiedere qualsiasi lingua. Se il file della lingua non è presente localmente, il motore lo scarica automaticamente dal CDN di Aspose.

```csharp
// Set the recognition language – English in this example
ocrEngine.Language = Language.English;
```

> **Caso limite:** Se devi riconoscere giapponese o arabo, imposta `Language.Japanese` o `Language.Arabic`. La prima chiamata potrebbe richiedere qualche secondo mentre il pacchetto viene scaricato.

## Passo 4: Riconoscere il testo da un'immagine TIFF

Ora effettivamente **extract text from tiff**. Il metodo `RecognizeImage` restituisce un `OcrResult` contenente il testo semplice, i punteggi di confidenza e le bounding box.

```csharp
// Path to your high‑resolution TIFF file
string imagePath = @"C:\Scans\high_res_scan.tif";

// Perform OCR – this is where the GPU shines
OcrResult result = ocrEngine.RecognizeImage(imagePath);
```

> **Perché il percorso completo?** I percorsi relativi funzionano, ma i percorsi assoluti evitano l'eventuale “file non trovato” quando la directory di lavoro differisce (ad esempio, eseguendo da VS Code vs. Visual Studio).

## Passo 5: Output del testo riconosciuto

Infine, stampa il testo sulla console o scrivilo su un file. La proprietà `Text` contiene già le interruzioni di riga così come apparivano nell'immagine.

```csharp
// Print the OCR output to the console
Console.WriteLine("=== OCR RESULT ===");
Console.WriteLine(result.Text);
```

**Output previsto** (troncato per brevità):

```
=== OCR RESULT ===
Invoice #12345
Date: 2026‑03‑01
Total: $1,274.56
Thank you for your business!
```

Se l'immagine conteneva più pagine, potresti iterare su di esse e concatenare i risultati.

## Esempio completo funzionante

Mettendo tutto insieme, ecco un programma autonomo che puoi copiare e incollare in un nuovo progetto console:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU engine namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Create the GPU OCR engine
        var ocrEngine = new GpuOcrEngine();

        // 2️⃣ (Optional) Pick GPU device & limit VRAM usage
        ocrEngine.DeviceId = 0;            // first GPU
        ocrEngine.MaxMemoryInMb = 2048;    // cap at 2 GB

        // 3️⃣ Choose language – English will be auto‑downloaded if missing
        ocrEngine.Language = Language.English;

        // 4️⃣ Path to the TIFF you want to process
        string tiffPath = @"YOUR_DIRECTORY/high_res_scan.tif";

        // 5️⃣ Run OCR – this returns the recognized text and metadata
        OcrResult result = ocrEngine.RecognizeImage(tiffPath);

        // 6️⃣ Show the result
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);
    }
}
```

Salva il file come `Program.cs`, esegui `dotnet run` e osserva la GPU fare la sua magia.

## Estrarre testo da TIFF in modo efficiente – considerazioni aggiuntive

### Gestione dei TIFF multi‑pagina

Se il tuo file di origine contiene più di una pagina, Aspose OCR tratta ogni pagina come un'immagine separata. Puoi iterare così:

```csharp
var pages = ocrEngine.RecognizeMultipageImage(tiffPath);
foreach (var pageResult in pages)
{
    Console.WriteLine("--- Page ---");
    Console.WriteLine(pageResult.Text);
}
```

### Gestione della memoria per scansioni enormi

- **Downscale only when needed**: Il motore GPU può elaborare la risoluzione originale, ma se raggiungi i limiti di memoria, considera `ocrEngine.DownscaleFactor = 0.5;`.
- **Dispose**: Chiama `ocrEngine.Dispose();` quando hai finito per liberare rapidamente le risorse GPU.

### Problemi comuni

| Sintomo | Probabile causa | Soluzione |
|---------|----------------|-----------|
| Output vuoto | DeviceId errato o driver non inizializzato | Verifica i driver GPU, prova `DeviceId = 0` o ometti l'impostazione. |
| Bassa accuratezza | Pacchetto lingua errato | Imposta `ocrEngine.Language` sulla lingua corretta, assicurati che il pacchetto sia stato scaricato completamente. |
| Crash per esaurimento memoria | `MaxMemoryInMb` troppo alto per la scheda | Riduci il limite o elabora le pagine una alla volta. |

## Consigli professionali e migliori pratiche

- **Batch processing**: Avvolgi il ciclo OCR in un `Parallel.ForEach` solo se la tua GPU ha abbastanza VRAM; altrimenti, l'elaborazione sequenziale evita il throttling.
- **Logging**: Usa `ocrEngine.Logger = new ConsoleLogger();` per ottenere informazioni dettagliate sui tempi—utile per l'ottimizzazione delle prestazioni.
- **Security**: Se gestisci documenti sensibili, abilita `ocrEngine.Sanitize = true;` per rimuovere eventuali metadati nascosti dal risultato.

## Conclusione

Ora hai una soluzione completa, end‑to‑end, per **recognize text from image** usando il motore GPU di Aspose OCR, e sai come **extract text from tiff** in modo efficiente. Il codice di esempio mostra ogni passaggio necessario—dall'installazione del pacchetto NuGet alla gestione di scansioni multi‑pagina e dei vincoli di memoria.  

Il passo successivo potrebbe essere esplorare il **post‑processing** dell'output OCR (controllo ortografico, estrazione con regex di numeri di fattura, ecc.) o integrare il risultato in un database per archivi ricercabili. Se sei curioso di altri formati, prova a fornire un JPEG o PNG nella stessa pipeline—l'API è indipendente dal formato.  

Hai domande sulla selezione della GPU, i pacchetti lingua o sullo scaling a centinaia di pagine al giorno? Lascia un commento qui sotto, e buona programmazione!  

![Diagramma che illustra la pipeline OCR in cui un TIFF ad alta risoluzione viene inviato al motore GPU, producendo l'output di testo riconosciuto – recognize text from image](https://example.com/ocr-pipeline.png "riconoscere il testo da immagine usando il motore GPU di Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}