---
category: general
date: 2026-03-17
description: Estrai il testo da PNG usando Aspose OCR in C#. Impara a leggere il testo
  dall'immagine, elaborare l'OCR delle ricevute e creare un motore OCR con accelerazione
  GPU.
draft: false
keywords:
- extract text from png
- read text from image
- ocr receipt image
- process receipt ocr
- create ocr engine
language: it
og_description: Estrai il testo da PNG usando Aspose OCR. Questa guida mostra come
  leggere il testo da un'immagine, elaborare l'OCR di una ricevuta e creare un motore
  OCR in modo efficiente.
og_title: Estrai testo da PNG – Leggi il testo dall'immagine con OCR
tags:
- OCR
- CSharp
- Aspose
title: Estrai testo da PNG – Leggi il testo da un'immagine con OCR
url: /it/net/text-recognition/extract-text-from-png-read-text-from-image-with-ocr/
---

? Should translate alt text but keep file name. So alt text can be Italian: "estrai testo da png esempio". Title attribute also.

Proceed.

At end shortcodes.

Let's craft final output.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai testo da PNG – Leggi testo da immagine con OCR

Hai mai avuto bisogno di **estrarre testo da PNG** ma non eri sicuro quale libreria ti avrebbe fornito risultati affidabili? Non sei l'unico—gli sviluppatori chiedono continuamente: “Come leggo il testo da file immagine come ricevute senza scrivere una rete neurale personalizzata?” La buona notizia è che Aspose OCR fa il lavoro pesante per te, e puoi persino attivare la GPU per aumentare la velocità.

In questo tutorial passeremo in rassegna tutto ciò che ti serve per **elaborare OCR di ricevute**, dall'installazione del pacchetto NuGet alla creazione di un motore OCR che comprenda il tuo file PNG. Alla fine avrai un'app console autonoma che legge un'immagine di una ricevuta, stampa il testo riconosciuto e ti mostra come regolare il motore per scenari diversi. Nessuna documentazione esterna, solo codice puro e spiegazioni chiare.

## Prerequisiti

- .NET 6.0 SDK (o qualsiasi versione recente di .NET)  
- Visual Studio 2022 o VS Code con estensioni C#  
- Una GPU NVIDIA supportata con driver più recente (opzionale, ma consigliato per la modalità GPU)  
- Il pacchetto NuGet **Aspose.OCR** (`dotnet add package Aspose.OCR`)  

Se non disponi di una GPU, puoi comunque eseguire l'esempio in modalità CPU—basta saltare le righe di configurazione della GPU.

## Passo 1: Installa Aspose.OCR e configura il progetto

Per prima cosa, crea un nuovo progetto console e aggiungi la libreria Aspose OCR.

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
dotnet add package Aspose.OCR
```

Perché è importante: il pacchetto `Aspose.OCR` include il motore OCR, i caricatori di immagini e il supporto opzionale per GPU. Aggiungerlo tramite NuGet garantisce di ottenere l'ultima versione stabile (a marzo 2026 è la 23.10).

## Passo 2: Importa i namespace e crea il motore OCR

Ora apri **Program.cs** e aggiungi le direttive `using` necessarie. Poi istanzia il motore.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Optional: Enable GPU acceleration if a compatible GPU is present
            // This dramatically speeds up processing of high‑resolution PNGs
            ocrEngine.Config.EngineMode = EngineMode.Gpu;   // <-- primary way to "process receipt ocr" fast
            ocrEngine.Config.GpuDeviceId = 0; // selects the first GPU in the system

            // The rest of the code follows...
```

**Consiglio professionale:** se incontri `System.DllNotFoundException` su macchine senza GPU, commenta semplicemente le due righe che impostano `EngineMode` e `GpuDeviceId`. Il motore tornerà automaticamente alla CPU.

## Passo 3: Carica l'immagine PNG da cui vuoi estrarre il testo

Aspose OCR può leggere le immagini direttamente da un percorso file, da uno stream o anche da un array di byte. Per questa demo caricheremo un'immagine di ricevuta locale.

```csharp
            // Step 3: Load the image (replace the path with your own PNG file)
            string imagePath = @"C:\Images\receipt.png";

            // Validate the file exists to avoid runtime surprises
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found – {imagePath}");
                return;
            }

            // Load the image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);
```

Nota come gestiamo il caso di un file mancante. In applicazioni reali probabilmente mostreresti un messaggio UI amichevole invece di terminare semplicemente.

## Passo 4: Esegui il riconoscimento OCR

L'estrazione effettiva del testo avviene con una singola chiamata di metodo. Il motore restituisce un oggetto `OcrResult` che contiene la stringa grezza, i punteggi di confidenza e le informazioni di layout.

```csharp
            // Step 4: Run the OCR process
            OcrResult ocrResult = ocrEngine.Recognize();

            // Check if the engine succeeded
            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be recognized.");
                return;
            }
```

Perché controlliamo `ocrResult.Text`: a volte un PNG di bassa qualità restituisce una stringa vuota, ed è meglio informare l'utente piuttosto che non produrre alcun output in silenzio.

## Passo 5: Stampa il testo riconosciuto

Infine, stampa la stringa estratta sulla console. Puoi anche scriverla su un file, su un database o passarla a un altro servizio.

```csharp
            // Step 5: Display the recognized text
            Console.WriteLine("=== Extracted Text from PNG ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== End of Output ===");
        }
    }
}
```

Quando esegui il programma (`dotnet run`), dovresti vedere qualcosa di simile:

```
=== Extracted Text from PNG ===
Store: Coffee Corner
Date: 03/15/2026
Item      Qty   Price
Latte      2    $5.40
Muffin     1    $2.30
Total            $7.70
=== End of Output ===
```

Questa è la **soluzione completa per estrarre testo da file PNG** con Aspose OCR, e hai appena imparato a **leggere testo da immagini** che sembrano ricevute.

## Opzionale: Ottimizzazione fine del motore OCR (Avanzato)

Se ti serve una precisione maggiore per caratteri specifici o sfondi rumorosi, considera di regolare queste impostazioni:

```csharp
// Enable language detection (default is English)
ocrEngine.Config.Language = Language.English;

// Turn on automatic image preprocessing (deskew, binarization)
ocrEngine.Config.EnableImagePreprocessing = true;

// Set a confidence threshold if you only want high‑certainty results
ocrEngine.Config.ConfidenceThreshold = 0.75f;
```

Queste modifiche sono particolarmente utili quando **elabori OCR di ricevute** in lavori batch dove alcune scansioni non sono perfette.

## Problemi comuni e come evitarli

| Problema | Perché accade | Soluzione |
|----------|---------------|-----------|
| **Driver GPU mancante** | Il motore tenta di caricare CUDA ma non trova la DLL. | Installa l'ultimo driver NVIDIA o passa alla modalità CPU rimuovendo la riga `EngineMode.Gpu`. |
| **Percorso immagine errato** | `ImageStream.FromFile` genera eccezione se il file non è trovato. | Valida sempre il percorso (vedi Passo 3) o usa `Path.Combine` per sicurezza cross‑platform. |
| **Bassa confidenza su ricevute sfocate** | Il motore OCR non riesce a distinguere i caratteri. | Abilita `EnableImagePreprocessing` e, se necessario, aumenta il DPI dell'immagine prima di passarla al motore. |
| **Perdita di memoria in servizi a lunga esecuzione** | Ogni `OcrEngine` mantiene risorse non gestite. | Disporre del motore dopo l'uso: `using var ocrEngine = new OcrEngine();` |

## Esempio completo (copia‑incolla)

Di seguito trovi il **programma intero** da inserire in `Program.cs`. Include tutti i ritocchi opzionali commentati per una facile attivazione.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create OCR engine
            using var ocrEngine = new OcrEngine();

            // Enable GPU acceleration if you have a supported card
            ocrEngine.Config.EngineMode = EngineMode.Gpu;
            ocrEngine.Config.GpuDeviceId = 0;

            // Optional fine‑tuning (uncomment as needed)
            //ocrEngine.Config.Language = Language.English;
            //ocrEngine.Config.EnableImagePreprocessing = true;
            //ocrEngine.Config.ConfidenceThreshold = 0.75f;

            // Load PNG image
            string imagePath = @"C:\Images\receipt.png";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found – {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize();

            // Verify result
            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be recognized.");
                return;
            }

            // Output the extracted text
            Console.WriteLine("=== Extracted Text from PNG ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== End of Output ===");
        }
    }
}
```

Salva, esegui `dotnet run` e vedrai il contenuto della ricevuta stampato sulla console.

![estrai testo da png esempio](receipt.png "estrai testo da png esempio")

*L'immagine sopra mostra una ricevuta PNG di esempio che il codice può elaborare.*

## Riepilogo

Abbiamo coperto come **estrarre testo da file PNG** usando Aspose OCR, dimostrato come **leggere testo da immagini**, e illustrato un flusso completo di **elaborazione OCR di ricevute** che include l'accelerazione opzionale GPU. Creando **un motore OCR** da soli, ottieni il pieno controllo su configurazione, prestazioni e gestione degli errori.

## Cosa esplorare dopo?

- **Elaborazione batch**: cicla su una cartella di ricevute PNG e scrivi ogni risultato in un file CSV.  
- **Integrazione con Azure Functions**: trasforma questa app console in un endpoint serverless che accetta upload di immagini.  
- **Supporto multilingua**: sostituisci `Language.English` con `Language.Spanish` o aggiungi dizionari personalizzati.  
- **Post‑processing**: usa espressioni regolari per estrarre campi come importo totale, data o partita IVA dalla stringa OCR grezza.

Sentiti libero di sperimentare—OCR è uno strumento sorprendentemente flessibile una volta che conosci le leve giuste da regolare. Se incontri difficoltà, lascia un commento qui sotto o consulta il riferimento API di Aspose OCR per approfondimenti.

Buon coding e buona trasformazione di quelle testarde ricevute PNG in testo ricercabile!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}