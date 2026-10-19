---
category: general
date: 2026-01-09
description: Impara come eseguire l'OCR di un'immagine e estrarre il testo dell’immagine
  usando Aspose.OCR. Include i passaggi per convertire un documento scansionato, abilitare
  la GPU e leggere l’immagine con OCR.
draft: false
keywords:
- how to ocr image
- extract image text
- convert scanned document
- how to enable gpu
- read image with ocr
language: it
og_description: Come eseguire l'OCR di un'immagine rapidamente con Aspose.OCR. Segui
  questo tutorial passo‑passo per estrarre il testo dall'immagine, convertire il documento
  scansionato e abilitare la GPU.
og_title: Come fare OCR di un'immagine in C# – Guida accelerata dalla GPU
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Come fare OCR di un'immagine in C# – Guida completa con supporto GPU
url: /it/net/ocr-configuration/how-to-ocr-image-in-c-complete-guide-with-gpu-support/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come fare OCR di un'immagine in C# – Guida completa con supporto GPU

Ti sei mai chiesto **come fare OCR di un'immagine** direttamente dalla tua app .NET? Non sei l'unico—gli sviluppatori hanno costantemente bisogno di estrarre testo da PDF, TIFF e foto, soprattutto quando si tratta di grandi documenti scansionati. La buona notizia? Con Aspose.OCR puoi **estrarre il testo dell'immagine** in poche righe, e puoi anche **abilitare l'accelerazione GPU** per una elaborazione più veloce.

In questo tutorial ti guideremo attraverso tutto ciò che devi sapere: dall'installazione della libreria, all'inizializzazione del motore OCR con fallback GPU, fino a **leggere l'immagine con OCR** e visualizzare il risultato. Alla fine sarai in grado di **convertire documenti scansionati** in stringhe modificabili—senza servizi esterni.

---

## Cosa ti servirà

Before we get our hands dirty, make sure you have the following:

- **.NET 6.0** o successivo (il codice funziona anche su .NET Core e .NET Framework).
- Una **licenza** per Aspose.OCR o una chiave di valutazione temporanea (la prova gratuita funziona per i test).
- Un file immagine da elaborare—preferibilmente un TIFF o PNG ad alta risoluzione.
- (Opzionale) Una macchina con GPU abilitata se vuoi vedere l'incremento di velocità; altrimenti il motore tornerà automaticamente alla CPU.

Avere questi prerequisiti coperti significa che puoi concentrarti sul flusso di lavoro OCR reale senza incontrare ostacoli in seguito.

---

## Passo 1: Installa il pacchetto NuGet Aspose.OCR

First things first—add the Aspose.OCR library to your project. Open a terminal in your solution folder and run:

```bash
dotnet add package Aspose.OCR
```

Oppure, se usi l'interfaccia NuGet di Visual Studio, cerca semplicemente **Aspose.OCR** e premi installa. Questo singolo comando scarica tutti i DLL necessari, inclusi i binari GPU nativi quando disponibili.

> **Consiglio professionale:** Mantieni il pacchetto aggiornato. Le nuove versioni includono spesso miglioramenti ai modelli linguistici e un migliore supporto GPU.

---

## Passo 2: Importa i namespace richiesti  

Now that the package is installed, bring the relevant namespaces into scope. This step is where we start **come fare OCR di un'immagine** in code.

```csharp
// Step 2: Import required namespaces
using Aspose.OCR;
using Aspose.OCR.Settings;
```

Queste due righe ti danno accesso alla classe `OcrEngine` e all'oggetto impostazioni che ti permette di attivare o disattivare l'uso della GPU. Senza di esse, il compilatore non saprebbe cosa sia `OcrEngine`.

---

## Passo 3: Inizializza il motore OCR e abilita la GPU  

If you’ve ever asked **how to enable GPU** for OCR, this is the answer. We create an `OcrEngineSettings` instance, flip the `UseGpu` flag, and pass it to the engine constructor. The engine automatically detects whether a compatible GPU is present; if not, it falls back to CPU—so you don’t need extra error handling.

```csharp
// Step 3: Initialize the OCR engine with GPU support (falls back to CPU if unavailable)
var ocrSettings = new OcrEngineSettings { UseGpu = true };
var ocrEngine   = new OcrEngine(ocrSettings);
```

Perché abilitare la GPU? Per immagini grandi—pensa a TIFF multi‑pagina o scansioni ad alta risoluzione—il tempo di elaborazione può scendere da diversi secondi a una frazione di secondo. Se stai costruendo una pipeline di elaborazione batch, questo guadagno di velocità si somma rapidamente.

---

## Passo 4: Esegui l'OCR sull'immagine di destinazione  

Here’s where we actually **read image with OCR**. Supply the path to your file, and the engine returns the recognized text as a string. This works for any raster format supported by Aspose (PNG, JPEG, TIFF, BMP, etc.).

```csharp
// Step 4: Perform OCR on the target image file
string imagePath = @"C:\Images\large-document.tif";
string recognizedText = ocrEngine.RecognizeImage(imagePath);
```

Se hai bisogno di **convertire documenti scansionati** pagina per pagina, basta iterare sui nomi dei file e chiamare `RecognizeImage` per ciascuno. Il metodo è thread‑safe, quindi puoi anche parallelizzare il carico di lavoro su una CPU multi‑core.

---

## Passo 5: Visualizza o salva il testo estratto  

Finally, we output the result. In a console app, `Console.WriteLine` does the trick. In a real‑world scenario you might write the text to a database, a JSON file, or feed it into a search index.

```csharp
// Step 5: Display the extracted text
Console.WriteLine(recognizedText);
```

La riga sopra stampa l'output OCR grezzo. Noterai interruzioni di riga, occasionali errori di riconoscimento e forse qualche carattere estraneo—niente di insolito per l'OCR. Un post‑processing (ad esempio pulizia con regex) può sistemare il risultato se necessario.

> **Nota:** Aspose.OCR supporta anche dizionari specifici per lingua. Se elabori testi non‑inglesi, imposta `ocrEngine.Settings.Language` di conseguenza prima di chiamare `RecognizeImage`.

---

## Esempio completo funzionante  

Putting it all together, here’s a self‑contained program you can copy‑paste into a new console project:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // Initialize OCR engine with GPU support
        var ocrSettings = new OcrEngineSettings { UseGpu = true };
        var ocrEngine   = new OcrEngine(ocrSettings);

        // Path to the image you want to process
        string imagePath = @"C:\Images\large-document.tif";

        // Perform OCR
        string recognizedText = ocrEngine.RecognizeImage(imagePath);

        // Output the result
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

**Output previsto** (troncato per brevità):

```
=== OCR Result ===
This is a sample scanned document.
It contains several lines of text that have been
converted from image to editable characters.
...
```

Esegui il programma, e dovresti vedere il testo estratto apparire nella finestra della console. Se la GPU è disponibile, il tempo di elaborazione sarà notevolmente più breve rispetto a macchine solo CPU‑only.

---

## Problemi comuni e come evitarli  

| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| **Caratteri spazzatura** | Fonte a bassa risoluzione o sfondo rumoroso. | Pre‑elabora l'immagine (aumenta DPI, applica binarizzazione) prima dell'OCR. |
| **GPU non utilizzata** | Nessun driver CUDA compatibile installato. | Verifica la versione del driver, o imposta `UseGpu = false` per forzare la CPU. |
| **Memoria esaurita su TIFF grandi** | Caricamento dell'intero file in una volta. | Usa `OcrEngineSettings.MaxMemoryUsage` per limitare l'utilizzo di memoria, o elabora le pagine singolarmente. |
| **Rilevamento lingua errato** | La lingua predefinita è l'inglese. | Imposta `ocrEngine.Settings.Language = Language.YourLanguage;` prima di chiamare `RecognizeImage`. |

Affrontare questi casi limite garantisce che la tua implementazione **come fare OCR di un'immagine** rimanga solida su diversi ambienti.

---

## Estendere la soluzione  

Now that you can **extract image text**, you might want to:

- **Converti documenti scansionati** PDF in PDF ricercabili incorporando il layer OCR.
- Memorizza i risultati in un indice **Azure Cognitive Search** per un recupero veloce.
- Collega l'output OCR a un'**API di traduzione** se ti serve supporto multilingue.
- Usa il metodo `GetBoundingBoxes` di **Aspose.OCR** per individuare dove appare ogni parola sull'immagine—utile per strumenti di redazione.

Tutte queste estensioni si basano sullo stesso principio fondamentale che abbiamo trattato: inizializzare il motore, fornirgli un'immagine e leggere il testo.

---

## Conclusione  

We’ve walked through a complete, end‑to‑end example of **how to OCR image** using Aspose.OCR in C#. By installing the NuGet package, importing the right namespaces, enabling GPU (or falling back to CPU), and calling `RecognizeImage`, you can reliably **extract image text**, **convert scanned document** pages, and **read image with OCR** in any .NET application.

Provalo su un gruppo di tue scansioni—sperimenta con diversi formati immagine, attiva/disattiva il flag GPU, e osserva come cambia le prestazioni. Quando sei pronto, esplora le funzionalità avanzate come i dizionari di lingua o l'estrazione di bounding‑box per rendere la tua soluzione ancora più intelligente.

Buon coding, e che le tue pipeline OCR siano veloci, accurate e senza problemi!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}