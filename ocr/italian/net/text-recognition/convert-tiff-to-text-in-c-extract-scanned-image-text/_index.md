---
category: general
date: 2026-03-05
description: Converti TIFF in testo in C# con Aspose OCR—estrai rapidamente il testo
  da file immagine scansionati e scopri come caricare un file immagine in C# per l'elaborazione
  OCR.
draft: false
keywords:
- convert TIFF to text
- extract text scanned image
- load image file C#
language: it
og_description: Converti TIFF in testo in C# usando Aspose OCR. Scopri l'intero flusso
  di lavoro per estrarre testo da immagini scannerizzate e caricare i file immagine
  in modo efficiente.
og_title: Converti TIFF in testo in C# – Estrai il testo dell'immagine scansionata
tags:
- OCR
- C#
- Aspose
title: Converti TIFF in testo in C# – Estrai il testo dell’immagine scannerizzata
url: /it/net/text-recognition/convert-tiff-to-text-in-c-extract-scanned-image-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Converti TIFF in Testo in C# – Estrai Testo da Immagine Scansionata

Hai bisogno di **convertire TIFF in testo in C#**? Non sei l'unico a lottare con immagini scansionate multi‑pagina che si rifiutano ostinatamente di diventare stringhe ricercabili.  
In questa guida percorreremo una soluzione completa, pronta all'uso, che prende un file TIFF, lo passa ad Aspose OCR e restituisce testo semplice—senza servizi aggiuntivi, senza magie nascoste.

> **Consiglio professionale:** se lavori con scansioni ad alta risoluzione, abilitare l'elaborazione GPU può ridurre di alcuni secondi il tempo per ogni pagina.

Ti mostreremo anche come **estrarre testo da immagini scansionate** e il modo migliore per **caricare file immagine C#** nel motore OCR, così potrai incorporare questa logica in qualsiasi progetto .NET oggi.

---

## Cosa Ti Serve

Prima di iniziare, assicurati di avere quanto segue sulla tua macchina:

| Requisito | Motivo |
|-------------|--------|
| .NET 6.0+ (or .NET Framework 4.7.2+) | Runtime moderno, supporta `Span<T>` e I/O asincrono |
| Aspose.OCR for .NET (NuGet package `Aspose.OCR`) | Il motore OCR che utilizzeremo |
| A valid Aspose OCR license file (`Aspose.OCR.lic`) | Senza di essa raggiungerai i limiti di valutazione |
| A TIFF file (single‑ or multi‑page) to test | Esempio usato: `scanned_multi_page.tif` |
| GPU with CUDA 11+ (optional) | Accelera il riconoscimento quando `EngineMode = Gpu` |

Se ti manca qualcuno di questi, scarica subito il pacchetto NuGet:

```bash
dotnet add package Aspose.OCR
```

---

## Passo 1: Configura il Progetto e Importa i Namespace

Crea una nuova app console (o aggiungi il codice a un progetto esistente). La prima cosa da fare è importare le classi di cui avremo bisogno.

```csharp
using System;
using Aspose.OCR;          // Core OCR classes
using Aspose.OCR.Image;   // ImageStream helper
```

> **Perché è importante:** importare `Aspose.OCR.Image` ci fornisce la factory `ImageStream`, che può leggere file TIFF direttamente dal disco o da uno stream. Saltare questo passaggio causerà un errore di compilazione.

---

## Passo 2: Inizializza il Motore OCR e Scegli la Modalità di Elaborazione

Il motore OCR deve essere configurato **prima** di assegnare qualsiasi immagine. Qui decidiamo se eseguire su CPU o sfruttare la GPU.

```csharp
// Step 2: Initialize the OCR engine and enable GPU processing (must be set before any OCR work)
OcrEngine ocrEngine = new OcrEngine();

// Choose the processing mode that fits your environment.
// Options: Cpu (default) | Gpu | Auto
ocrEngine.EngineMode = OcrEngineMode.Gpu;   // Switch to Cpu if you don’t have a compatible GPU
```

*Se sei su un server headless senza scheda grafica, cambia `Gpu` in `Cpu` o `Auto`.*  
La modalità del motore influisce sull'allocazione della memoria e sulla velocità; la modalità GPU può essere 2‑3× più veloce su TIFF grandi e ad alta risoluzione.

---

## Passo 3: Applica la Tua Licenza Aspose OCR

Eseguire senza licenza ti limita a poche pagine e aggiunge filigrane. Carica la licenza subito così ogni operazione successiva è senza restrizioni.

```csharp
// Step 3: Apply the Aspose OCR license (replace with your own license file if needed)
ocrEngine.SetLicense("Aspose.OCR.lic");
```

> **Errore comune:** posizionare `SetLicense` dopo `Recognize()` farà tornare il motore alla modalità di prova per quella chiamata.

---

## Passo 4: Carica il File TIFF – Gestione di Immagini Singole e Multi‑Pagina

Aspose OCR può leggere TIFF multi‑pagina subito, ma è necessario fornire lo stream corretto. Ecco un modello robusto che funziona per entrambi gli scenari.

```csharp
// Step 4: Load the image to be recognized
string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

using (var imageStream = ImageStream.FromFile(tiffPath))
{
    // Step 5: Assign the image to the engine
    ocrEngine.Image = imageStream;

    // Step 6: Perform the OCR operation
    OcrResult ocrResult = ocrEngine.Recognize();

    // Step 7: Output the recognized text
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(ocrResult.Text);
}
```

### Perché usare `ImageStream.FromFile`?

- Astrae lo `FileStream` sottostante, gestendo internamente l'enumerazione delle pagine TIFF.  
- Funziona anche con `MemoryStream`, così puoi caricare immagini da un database o da un'API web senza toccare il file system.

### Caso limite: TIFF molto grandi

Se il tuo TIFF supera i 200 MB, considera di caricarlo pagina per pagina per evitare eccezioni di out‑of‑memory:

```csharp
int pageCount = ImageInfo.GetPageCount(tiffPath);
for (int i = 0; i < pageCount; i++)
{
    using var pageStream = ImageStream.FromFile(tiffPath, i);
    ocrEngine.Image = pageStream;
    var pageResult = ocrEngine.Recognize();
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(pageResult.Text);
}
```

---

## Passo 5: Verifica l'Uscita

Quando esegui il programma, dovresti vedere qualcosa di simile:

```
=== OCR Output ===
Invoice #12345
Date: 2024‑12‑01
Total: $1,250.00
Thank you for your business!
```

Se il testo appare illeggibile, ricontrolla:

1. **Risoluzione** – L'OCR funziona al meglio con 300 dpi o più.  
2. **EngineMode** – Passa a `Cpu` se il driver GPU è obsoleto.  
3. **Licenza** – Assicurati che il percorso del file di licenza sia corretto e che il file sia leggibile.

---

## Domande Frequenti (FAQ)

### Funziona con altri formati immagine?

Assolutamente. `ImageStream.FromFile` supporta JPEG, PNG, BMP e anche PDF (via Aspose.PDF). Basta sostituire l'estensione del file.

### E se devo elaborare immagini archiviate in un database?

Leggi il BLOB in un `MemoryStream` e passalo a `ImageStream.FromStream(memoryStream)`. Il motore OCR lo tratta come uno stream basato su file.

### Posso eseguirlo su Linux?

Sì—Aspose OCR è cross‑platform. Installa il runtime .NET appropriato e assicurati che le librerie native richieste per la GPU (se usata) siano disponibili.

---

## Esempio Completo Funzionante (Pronto per Copia‑Incolla)

Di seguito trovi l'intero programma, pronto per la compilazione. Sostituisci `YOUR_DIRECTORY` e il percorso del file di licenza con le tue posizioni effettive.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Image;

namespace TiffToTextDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Choose processing mode: Gpu, Cpu, or Auto
            ocrEngine.EngineMode = OcrEngineMode.Gpu; // Change to Cpu if no GPU

            // Apply license (skip if you only need a trial)
            ocrEngine.SetLicense("Aspose.OCR.lic");

            // Path to the TIFF file
            string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

            // Load the TIFF (handles multi‑page automatically)
            using (var imageStream = ImageStream.FromFile(tiffPath))
            {
                // Assign image to engine
                ocrEngine.Image = imageStream;

                // Run OCR
                OcrResult result = ocrEngine.Recognize();

                // Display result
                Console.WriteLine("=== OCR Output ===");
                Console.WriteLine(result.Text);
            }

            // Optional: Process each page individually for huge files
            // int pages = ImageInfo.GetPageCount(tiffPath);
            // for (int i = 0; i < pages; i++) { ... }
        }
    }
}
```

Salva questo come `Program.cs`, esegui `dotnet run` e osserva il testo

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}