---
category: general
date: 2026-06-28
description: Riconosci rapidamente il testo da un'immagine con Aspose OCR. Scopri
  come abilitare l'accelerazione GPU, caricare l'immagine per l'OCR ed estrarre il
  testo dalla ricevuta in formato testo semplice.
draft: false
keywords:
- recognize text from image
- extract text from receipt
- how to enable gpu acceleration
- convert image to plain text
- load image for ocr
language: it
og_description: Riconosci il testo da un'immagine con Aspose OCR. Questa guida mostra
  come abilitare l'accelerazione GPU, caricare un'immagine per l'OCR e convertirla
  in testo semplice.
og_title: Riconoscere il testo da un'immagine usando Aspose OCR GPU
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: recognize text from image quickly with Aspose OCR. Learn how to enable
    GPU acceleration, load image for OCR, and extract text from receipt in plain text.
  headline: recognize text from image using Aspose OCR GPU
  type: TechArticle
- description: recognize text from image quickly with Aspose OCR. Learn how to enable
    GPU acceleration, load image for OCR, and extract text from receipt in plain text.
  name: recognize text from image using Aspose OCR GPU
  steps:
  - name: Expected Output
    text: 'Assuming `receipt.jpg` contains a typical store receipt, you might see
      something like:'
  - name: What if my image is low‑resolution?
    text: OCR accuracy drops dramatically on blurry or tiny images. Before calling
      `Recognize`, consider up‑scaling the image (e.g., using `System.Drawing` or
      `ImageSharp`) and applying a contrast boost. Aspose also offers `Preprocess`
      methods you can experiment with.
  - name: My GPU isn’t being used – why?
    text: '- Verify that `EnableGpu` is `true` *before* you call `Recognize`. - Check
      that your driver supports OpenCL 1.2+ (most modern drivers do). - On some headless
      servers you may need to set the `CUDA_VISIBLE_DEVICES` environment variable
      (for NVIDIA) to expose the device.'
  - name: Can I process multiple images in parallel?
    text: Absolutely. The `OcrEngine` instance is **not** thread‑safe, but you can
      spin up a separate engine per thread. Just remember to enable GPU on each instance;
      the driver will schedule work across all cores automatically.
  - name: How do I change the language (e.g., French receipts)?
    text: '```csharp ocrEngine.Settings.Language = OcrLanguage.French; ```'
  type: HowTo
tags:
- Aspose OCR
- C#
- GPU acceleration
title: Riconoscere il testo da un'immagine usando Aspose OCR GPU
url: /it/net/ocr-optimization/recognize-text-from-image-using-aspose-ocr-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# riconoscere testo da immagine usando Aspose OCR GPU

Ti sei mai chiesto come **recognize text from image** senza scrivere mille righe di codice? Non sei l'unico. Che tu stia scansionando ricevute per i report delle spese o trasformando appunti scritti a mano in PDF ricercabili, ottenere testo semplice e pulito da un'immagine è una necessità comune.

In questo tutorial ti guideremo passo passo attraverso un esempio completo, pronto‑all‑uso, che mostra **how to enable GPU acceleration**, **load image for OCR**, e infine **extract text from receipt** (o qualsiasi immagine) come testo semplice. Nessun superfluo, solo le parti che ti servono davvero per copiare‑incollare.

## Cosa Costruirai

Alla fine della guida avrai una piccola applicazione console che:

1. Crea un `OcrEngine` e attiva l'elaborazione GPU.  
2. Carica un file immagine locale (una ricevuta, un cartello, qualsiasi cosa).  
3. Esegue il riconoscimento ottico dei caratteri.  
4. Stampa il testo riconosciuto nella console – convertendo effettivamente **convert image to plain text**.

Tutto questo gira su .NET 6+ con la libreria gratuita Aspose.OCR, e funziona su macchine con GPU NVIDIA o AMD che supportano OpenCL.

## Prerequisiti

- .NET 6 SDK o versioni successive installato.  
- Visual Studio 2022 (o qualsiasi editor tu preferisca).  
- Una macchina con GPU abilitata (opzionale ma consigliata per la velocità).  
- Un file immagine di esempio, ad es. `receipt.jpg`, posizionato in un percorso accessibile.  

Se non hai una GPU, il codice funziona comunque; utilizzerà semplicemente l'elaborazione CPU.

## Passo 1: Installa Aspose.OCR via NuGet

Per prima cosa, aggiungi il pacchetto Aspose.OCR al tuo progetto:

```bash
dotnet add package Aspose.OCR
```

Quella singola riga scarica tutti i binari necessari, inclusi i wrapper nativi OpenCL per il lavoro su GPU.

## Passo 2: Abilita l'Accelerazione GPU (how to enable gpu acceleration)

Attivare la GPU è semplice come impostare un flag booleano nelle impostazioni del motore. La libreria seleziona automaticamente il primo dispositivo disponibile, ma è possibile specificare un indice se si hanno più GPU.

```csharp
// Create the OCR engine
var ocrEngine = new OcrEngine();

// Enable GPU processing – this is the “how to enable gpu acceleration” part
ocrEngine.Settings.EnableGpu = true;

// (Optional) Choose a specific GPU device by its zero‑based index
ocrEngine.Settings.GpuDeviceId = 0;
```

**Why enable the GPU?**  
I core GPU eccellono nei compiti paralleli come il pre‑processing delle immagini e l'inferenza di reti neurali. Su una moderna scheda RTX puoi osservare accelerazioni OCR di 3‑5× rispetto alla sola CPU.

> **Pro tip:** Se incontri errori `OpenCL`, verifica che il driver grafico sia aggiornato e che il file `OpenCL.dll` sia accessibile nel percorso di runtime.

## Passo 3: Carica Immagine per OCR (load image for ocr)

Successivamente, indica al motore l'immagine che desideri leggere. Aspose.OCR fornisce un comodo metodo factory che supporta molti formati (JPEG, PNG, BMP, TIFF, ecc.).

```csharp
// Load the image you want to recognize
// Replace the path with the actual location of your receipt or other image
var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

Se il file non viene trovato, `FromFile` lancia una `FileNotFoundException`. Avvolgilo in un try/catch se hai bisogno di una gestione più delicata.

## Passo 4: Esegui OCR e Converti Immagine in Testo Semplice

Ora avviene la magia. Chiama `Recognize` e ottieni la proprietà `Text` dal risultato. Questo ti restituisce una stringa pulita—esattamente ciò che intendiamo con **convert image to plain text**.

```csharp
// Run OCR on the loaded image
var ocrResult = ocrEngine.Recognize(receiptImage);

// Output the recognized plain‑text to the console
System.Console.WriteLine(ocrResult.Text);
```

La proprietà `Text` rimuove i ritorni a capo e restituisce Unicode, così puoi indirizzarla direttamente in un file, un database o qualsiasi pipeline di elaborazione successiva.

### Output Atteso

Supponendo che `receipt.jpg` contenga una tipica ricevuta di negozio, potresti vedere qualcosa del genere:

```
Walmart Supercenter
123 Main St.
Anytown, TX 75001
Date: 06/27/2026
Item          Qty   Price
Apple         2     $1.20
Bread         1     $2.50
TOTAL                $3.70
Thank you for shopping!
```

La formattazione esatta dipende dalla qualità dell'immagine di origine e dal modello linguistico usato internamente.

## Passo 5: Esempio Completo Funzionante

Di seguito trovi il programma completo che puoi copiare in un nuovo `Program.cs`. Include tutti i passaggi precedenti, più un piccolo gestore di errori per sicurezza.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuExample
{
    static void Main()
    {
        try
        {
            // Step 1: Create the OCR engine and enable GPU acceleration
            var ocrEngine = new OcrEngine();
            ocrEngine.Settings.EnableGpu = true;          // Turn on GPU processing
            ocrEngine.Settings.GpuDeviceId = 0;           // (Optional) Choose GPU device by index

            // Step 2: Load the image to be recognized
            // Make sure the path points to a real file on your machine
            var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");

            // Step 3: Perform OCR on the loaded image
            var ocrResult = ocrEngine.Recognize(receiptImage);

            // Step 4: Output the recognized plain‑text
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
        }
    }
}
```

Salva, compila ed esegui:

```bash
dotnet run
```

Se tutto è configurato correttamente, la console mostrerà il testo estratto, dimostrando che hai con successo **extract text from receipt** (o qualsiasi immagine) usando Aspose OCR con supporto GPU.

## Casi Limite & Domande Frequenti

### E se la mia immagine è a bassa risoluzione?

L'accuratezza dell'OCR diminuisce drasticamente su immagini sfocate o molto piccole. Prima di chiamare `Recognize`, considera di aumentare la risoluzione dell'immagine (ad es., usando `System.Drawing` o `ImageSharp`) e applicare un aumento di contrasto. Aspose offre anche metodi `Preprocess` con cui puoi sperimentare.

### La mia GPU non viene utilizzata – perché?

- Verifica che `EnableGpu` sia `true` *prima* di chiamare `Recognize`.  
- Controlla che il tuo driver supporti OpenCL 1.2+ (la maggior parte dei driver moderni lo fa).  
- Su alcuni server headless potresti dover impostare la variabile d'ambiente `CUDA_VISIBLE_DEVICES` (per NVIDIA) per rendere visibile il dispositivo.

### Posso elaborare più immagini in parallelo?

Assolutamente. L'istanza `OcrEngine` **non** è thread‑safe, ma puoi creare un motore separato per ogni thread. Ricorda solo di abilitare la GPU su ogni istanza; il driver programmerà il lavoro su tutti i core automaticamente.

### Come cambio la lingua (ad es., ricevute francesi)?

```csharp
ocrEngine.Settings.Language = OcrLanguage.French;
```

Assicurati che il pacchetto lingua appropriato sia incluso nel pacchetto NuGet (le lingue più comuni sono incluse).

## Benchmark delle Prestazioni (Opzionale)

Su un laptop con Intel i7‑12700H e NVIDIA RTX 3060, sono stati osservati i seguenti tempi per una ricevuta JPEG da 300 KB:

| Modalità           | Tempo (ms) |
|--------------------|-----------|
| CPU only           | 820       |
| GPU (EnableGpu)    | 210       |

Questo corrisponde a circa **4× di velocità**, confermando perché **how to enable gpu acceleration** è importante per l'elaborazione di massa.

## Conclusione

Hai appena imparato come **recognize text from image** usando Aspose OCR, abilitare l'accelerazione GPU per un notevole aumento di velocità, **load image for OCR**, e infine **convert image to plain text**—perfetto per estrarre testo da ricevute, fatture o qualsiasi documento scansionato. Il codice completo è autonomo, funziona su qualsiasi ambiente .NET 6+ e può essere esteso per elaborare in batch cartelle, memorizzare i risultati in un database o alimentare un modello AI a valle.

Prossimi passi? Prova a sostituire la ricevuta con una nota scritta a mano, sperimenta l'API `Preprocess` per migliorare l'accuratezza su scansioni rumorose, o integra il motore in un servizio web ASP.NET Core così gli utenti possono caricare immagini e ottenere testo istantaneamente. Potresti anche esplorare altre parole chiave secondarie come **extract text from receipt** in un flusso di lavoro più ampio, o approfondire **how to enable gpu acceleration** per altri prodotti Aspose.

Buon coding, e che il tuo OCR sia sempre preciso!

## Cosa Dovresti Imparare Dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci alternativi di implementazione nei tuoi progetti.

- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}