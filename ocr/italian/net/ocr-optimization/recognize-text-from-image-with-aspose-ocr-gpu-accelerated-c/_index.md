---
category: general
date: 2026-01-13
description: Impara a riconoscere il testo da un'immagine ed estrarre il testo da
  una ricevuta rapidamente usando Aspose OCR. Include i passaggi per caricare l'immagine
  per OCR e impostare l'ID del dispositivo GPU.
draft: false
keywords:
- recognize text from image
- extract text from receipt
- load image for ocr
- set gpu device id
language: it
og_description: Riconosci il testo da un'immagine istantaneamente con Aspose OCR.
  Segui questa guida passo‑passo per caricare l'immagine per l'OCR, impostare l'ID
  del dispositivo GPU e estrarre il testo dalla ricevuta.
og_title: Riconosci il testo da un'immagine – Guida completa C# con accelerazione
  GPU
tags:
- Aspose OCR
- C#
- GPU computing
title: Riconoscere il testo da un'immagine con Aspose OCR – Tutorial C# accelerato
  GPU
url: /it/net/ocr-optimization/recognize-text-from-image-with-aspose-ocr-gpu-accelerated-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# riconoscere testo da immagine – Guida completa C# accelerata da GPU

Hai mai dovuto **riconoscere testo da immagine** ma hai trovato la versione CPU dolorosamente lenta? Forse stai cercando di **estrarre testo da ricevute** e la latenza sta rovinando l'esperienza dell'utente. La buona notizia è che non devi accontentarti di prestazioni lente: il pacchetto GPU di Aspose OCR può dare una spinta turbo al processo, e il codice è lungo solo poche righe.

In questo tutorial percorreremo un esempio completo, eseguibile, che mostra come **caricare l'immagine per OCR**, configurare la GPU con **impostare l'ID del dispositivo GPU**, e infine recuperare il risultato in testo semplice. Alla fine avrai uno snippet pronto da inserire che funziona su qualsiasi macchina Windows o Linux moderna con una scheda NVIDIA supportata.

---

## Cosa ti serve

- **.NET 6+** (o .NET Framework 4.7.2+) – l'API funziona con entrambi.
- Pacchetto NuGet **Aspose.OCR** **plus** l'add‑on **Aspose.OCR.Gpu**.
- Una GPU NVIDIA con almeno 2 GB di VRAM (la demo limita l'uso a 1 GB).
- Un'immagine di esempio, ad es. una ricevuta scansionata (`receipt.jpg`).

Se hai già un progetto, esegui semplicemente `dotnet add package Aspose.OCR` e `dotnet add package Aspose.OCR.Gpu`. Non sono richieste librerie native aggiuntive; l'SDK fornisce i binari CUDA necessari.

---

## Implementazione passo‑passo

### ## Come riconoscere testo da immagine usando Aspose OCR e GPU

Di seguito trovi il **programma completo e autonomo**. Copialo e incollalo in un nuovo progetto console e premi `Ctrl+F5`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑accelerated namespace

class GpuOcrDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize a GPU‑enabled OCR engine
        // -------------------------------------------------
        var ocrEngine = new GpuOcrEngine();

        // -------------------------------------------------
        // Step 2: (Optional) Select the GPU device and limit memory usage
        // -------------------------------------------------
        ocrEngine.DeviceId = 0;        // set GPU device ID – first GPU in the system
        ocrEngine.MaxMemoryMb = 1024;  // cap at 1 GB to avoid OOM on shared machines

        // -------------------------------------------------
        // Step 3: Load the image you want to recognize
        // -------------------------------------------------
        var receiptImage = OcrImage.FromFile(@"YOUR_DIRECTORY/receipt.jpg");

        // -------------------------------------------------
        // Step 4: Perform OCR – here we extract text from receipt (English)
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(receiptImage, OcrLanguage.English);

        // -------------------------------------------------
        // Step 5: Output the recognized plain text
        // -------------------------------------------------
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

> **Consiglio:** Se la tua macchina ha più GPU, cambia `DeviceId` in `1`, `2`, ecc., per scegliere la scheda meno occupata. L'SDK lancerà una chiara `GpuDeviceNotFoundException` se l'ID è fuori intervallo.

### ### Passo 1: Caricare l'immagine per OCR

La chiamata `OcrImage.FromFile` fa più che leggere un bitmap—pre‑processa l'immagine (deskew, binarizzazione) basandosi su euristiche interne. Per questo **caricare immagine per OCR** è un passaggio separato: puoi sostituire con un `MemoryStream` se l'immagine è memorizzata in un database.

```csharp
var receiptImage = OcrImage.FromFile(@"C:\Invoices\receipt.jpg");
```

Se devi **riconoscere testo da immagine** già presente in memoria:

```csharp
using (var ms = new MemoryStream(File.ReadAllBytes(@"receipt.jpg")))
{
    var receiptImage = OcrImage.FromStream(ms);
}
```

### ### Passo 2: Impostare l'ID del dispositivo GPU e i limiti di memoria

Le risorse GPU sono limitate. Esporre `DeviceId` e `MaxMemoryMb` permette ad Aspose di **impostare l'ID del dispositivo GPU** in modo sicuro, evitando che un processo monopolizzi l'intera scheda.

```csharp
ocrEngine.DeviceId = 0;        // first GPU
ocrEngine.MaxMemoryMb = 1024; // 1 GB ceiling
```

Se superi il limite di memoria, il motore effettuerà automaticamente lo spill nella RAM di sistema, più lenta ma che previene crash.

### ### Passo 3: Estrarre testo dalla ricevuta (riconoscere testo da immagine)

Il metodo `Recognize` esegue il lavoro pesante. Puoi passare qualsiasi lingua supportata da Aspose OCR; per le ricevute, l'inglese funziona nella maggior parte dei casi, ma puoi aggiungere anche `OcrLanguage.Spanish` o un pacchetto lingua personalizzato.

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, OcrLanguage.English);
Console.WriteLine(ocrResult.Text);
```

**Output previsto** (esempio):

```
Store: QuickMart
Date: 2025-12-01
Total: $23.45
Thank you for shopping!
```

---

## Varianti comuni & casi limite

| Situazione | Cosa cambiare | Perché |
|-----------|----------------|-----|
| **Più ricevute in una sola immagine** | Chiama `ocrEngine.Recognize` su ogni regione ritagliata (usa `OcrImage.Crop`) | Migliora l'accuratezza perché il motore vede un'area più piccola e pulita. |
| **Scansioni a bassa risoluzione (<150 dpi)** | Pre‑ingrandisci con `receiptImage.Resize(2.0)` prima del riconoscimento | Una densità di pixel più alta fornisce alla GPU più dati su cui lavorare. |
| **Ricevute non in inglese** | Passa `OcrLanguage.French` (o un `.traineddata` personalizzato) | I modelli specifici per lingua riducono i falsi positivi. |
| **GPU non disponibile** | Fallback a `OcrEngine` (CPU) dentro un blocco try‑catch | Garantisce che l'app funzioni comunque su server senza GPU. |

```csharp
try
{
    var gpuEngine = new GpuOcrEngine();
    // configure GPU as shown earlier …
    var result = gpuEngine.Recognize(receiptImage, OcrLanguage.English);
    Console.WriteLine(result.Text);
}
catch (GpuDeviceNotFoundException)
{
    // Graceful fallback
    var cpuEngine = new OcrEngine();
    var result = cpuEngine.Recognize(receiptImage, OcrLanguage.English);
    Console.WriteLine(result.Text);
}
```

---

## Consigli per un OCR pronto per la produzione

- **Elaborazione batch:** Avvolgi il ciclo di riconoscimento in `Parallel.ForEach` ma limita il grado di parallelismo al numero di stream GPU che puoi allocare (di solito 1‑2 per scheda).
- **Igiene della memoria:** Rilascia prontamente gli oggetti `OcrImage` (`receiptImage.Dispose()`), specialmente quando elabori migliaia di ricevute.
- **Logging:** Cattura `ocrResult.Confidence` per ogni riga; una bassa confidenza può attivare un flusso di revisione manuale.
- **Sicurezza:** Quando gestisci ricevute sensibili, assicurati che i file immagine siano archiviati in cartelle temporanee criptate e cancellati dopo l'elaborazione.

---

## Conclusione

Ora disponi di un **esempio completo e eseguibile** che mostra come **riconoscere testo da immagine** con l'accelerazione GPU di Aspose OCR, **caricare immagine per OCR**, **impostare l'ID del dispositivo GPU**, e infine **estrarre testo dalla ricevuta** in pochi passaggi concisi. Il codice è pronto per il copy‑paste, e le spiegazioni ti forniscono il contesto necessario per adattarlo a scenari multilingua, multi‑GPU o ad alto throughput.

Pronto per la prossima sfida? Prova a alimentare un flusso video live in `GpuOcrEngine` per la scansione di ricevute in tempo reale, o integra il risultato in un'API di contabilità. Il cielo è il limite quando combini OCR GPU veloce con un design C# pulito.

*Buon coding, e che il tuo OCR sia sempre rapido!* 

![recognize text from image demo screenshot](placeholder-image.png "recognize text from image example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}