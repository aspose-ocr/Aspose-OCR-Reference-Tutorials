---
category: general
date: 2026-01-07
description: Estrai il testo da un'immagine usando Aspose OCR in C#. Scopri come riconoscere
  il testo da una foto, migliorare la precisione dell'OCR, caricare l'immagine per
  l'OCR e impostare la lingua dell'OCR.
draft: false
keywords:
- extract text from image
- recognize text from photo
- improve ocr accuracy
- load image for ocr
- set ocr language
language: it
og_description: Estrai il testo da un'immagine usando Aspose OCR. Questa guida mostra
  come riconoscere il testo da una foto, migliorare la precisione dell'OCR, caricare
  l'immagine per l'OCR e impostare la lingua dell'OCR.
og_title: Estrai testo da immagine con Aspose OCR – Tutorial C#
tags:
- Aspose OCR
- C#
- Image Processing
title: Estrai testo da un'immagine con Aspose OCR – Guida completa C#
url: /it/net/text-recognition/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai testo da immagine – Implementazione completa in C# con Aspose OCR

Hai mai dovuto **estrarre testo da un’immagine** ma non sapevi quale libreria garantisse risultati affidabili? Non sei solo. In molte applicazioni reali—scanner di ricevute, verificatori di ID o semplici strumenti di presa appunti—la capacità di **riconoscere testo da una foto** è una funzionalità indispensabile.

In questo tutorial percorreremo un esempio completo, pronto all’esecuzione, che mostra come **caricare l’immagine per OCR**, configurare il motore per **impostare la lingua OCR** e applicare alcuni trucchi di pre‑elaborazione per **migliorare l’accuratezza dell’OCR**. Alla fine avrai un unico file C# che stampa il testo estratto sulla console e comprenderai perché ogni impostazione è importante.

> **Suggerimento:** il codice funziona con Aspose.OCR ≥ 23.5, .NET 6+ e qualsiasi ambiente Windows, Linux o macOS in grado di eseguire .NET Core.

## Prerequisiti

- .NET 6 SDK (o versione più recente) installato  
- Visual Studio 2022, VS Code o qualsiasi editor tu preferisca  
- Pacchetto NuGet `Aspose.OCR` (installalo con `dotnet add package Aspose.OCR`)  
- Un file immagine (JPEG/PNG) che contenga testo stampato o digitato chiaramente  

Se hai tutto questo, immergiamoci.

![estrarre testo da immagine esempio](/images/ocr-example.png "estrarre testo da immagine – output di Aspose OCR")

## Passo 1: Creare e rilasciare il motore OCR – Core “Estrai testo da immagine”

La prima cosa di cui hai bisogno è un’istanza di `OcrEngine`. Avvolgerla in un blocco `using` garantisce il corretto rilascio delle risorse native.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

/// <summary>
/// Demonstrates how to extract text from image using Aspose OCR.
/// </summary>
class Program
{
    static void Main()
    {
        // Step 1 – Initialize the OCR engine (the heart of the process)
        using (var ocrEngine = new OcrEngine())
        {
            // The rest of the workflow lives inside this block.
```

**Perché è importante:** `OcrEngine` mantiene memoria non gestita per le DLL OCR native. Rilasciarlo tempestivamente evita perdite di memoria, soprattutto quando si elaborano molte immagini in batch.

## Passo 2: Definire le impostazioni di riconoscimento – Migliorare l’accuratezza dell’OCR

Successivamente creiamo un oggetto `RecognitionSettings`. Qui **impostiamo la lingua OCR** e aggiungiamo filtri di pre‑elaborazione che spesso fanno la differenza tra una stringa incomprensibile e un output pulito.

```csharp
            // Step 2 – Configure recognition settings
            var recognitionSettings = new RecognitionSettings
            {
                // Set the language to English; other languages are available via Language enum.
                Language = Language.English,

                // PreprocessFilters help the engine deal with real‑world photo issues.
                PreprocessFilters = new[]
                {
                    PreprocessFilter.Deskew,          // Corrects slight rotation
                    PreprocessFilter.Denoise,         // Reduces grainy noise
                    PreprocessFilter.ContrastEnhance // Boosts text visibility
                }
            };
```

**Perché questi filtri?**  
- **Deskew** corregge il problema comune di una foto scattata con il telefono leggermente inclinata.  
- **Denoise** rimuove i granelli che potrebbero essere interpretati come caratteri.  
- **ContrastEnhance** fa risaltare l’inchiostro tenue, essenziale per **migliorare l’accuratezza dell’OCR**.

## Passo 3: Caricare l’immagine – Caricare immagine per OCR in modo efficiente

Aspose fornisce `ImageStream.FromFile` per un caricamento rapido. Puoi anche fornire un `MemoryStream` se l’immagine proviene da una richiesta web o da un database.

```csharp
            // Step 3 – Load the image you want to analyze
            var imagePath = @"YOUR_DIRECTORY/phone_photo.jpg";
            var imageStream = ImageStream.FromFile(imagePath);
```

**Errore comune:** fornire un percorso con barre oblique (`/`) su Windows funziona, ma usare `Path.Combine` è più sicuro per progetti multipiattaforma.

## Passo 4: Eseguire il riconoscimento – Riconoscere testo da foto

Ora chiamiamo `Recognize`, passando sia lo stream dell’immagine sia le impostazioni. Il metodo restituisce una stringa semplice con il testo estratto.

```csharp
            // Step 4 – Run OCR and capture the result
            string recognizedText = ocrEngine.Recognize(imageStream, recognitionSettings);
```

Se l’immagine contiene più blocchi di testo, Aspose li concatena con interruzioni di riga, preservando il layout originale il più possibile.

## Passo 5: Restituire il risultato – Verificare l’estrazione

Infine, scrivi il risultato sulla console. In un’applicazione reale potresti salvarlo in un database, inviarlo a un altro servizio o visualizzarlo in un’interfaccia utente.

```csharp
            // Step 5 – Show the extracted text
            Console.WriteLine("=== Extracted Text Start ===");
            Console.WriteLine(recognizedText);
            Console.WriteLine("=== Extracted Text End ===");
        } // End of using block – OcrEngine disposed
    }
}
```

### Output console previsto

```
=== Extracted Text Start ===
This is a sample receipt.
Total: $23.45
Thank you for shopping!
=== Extracted Text End ===
```

Se vedi caratteri incomprensibili, ricontrolla che l’immagine sia chiara, che la lingua corrisponda al testo e che i filtri di pre‑elaborazione siano appropriati.

## Passo 6: Ottimizzazioni opzionali – Affinare per casi limite

### a. Cambio lingua

```csharp
recognitionSettings.Language = Language.Spanish; // For Spanish receipts
```

### b. Aggiunta di filtri personalizzati

Aspose offre anche `PreprocessFilter.Sharpen` o `PreprocessFilter.Binarize`. Sperimenta con questi quando il trio predefinito non è sufficiente.

### c. Gestione di immagini di grandi dimensioni

Per foto ad altissima risoluzione, ridimensiona prima per mantenere basso l’utilizzo di memoria:

```csharp
var resizedStream = ImageProcessor.Resize(imageStream, 1024, 768);
string text = ocrEngine.Recognize(resizedStream, recognitionSettings);
```

## Domande frequenti

**D: Funziona con appunti scritti a mano?**  
R: Aspose OCR è ottimizzato per testo stampato. Il riconoscimento della scrittura a mano richiede un motore diverso (ad es. Aspose.OCR for Handwriting o un modello di machine‑learning).

**D: Posso elaborare più immagini in un ciclo?**  
R: Assolutamente. Sposta il blocco `using (var ocrEngine = new OcrEngine())` fuori dal ciclo e riutilizza il motore per migliori prestazioni.

**D: E se l’immagine è una pagina PDF?**  
R: Converti prima la pagina PDF in immagine (Aspose.PDF può renderizzare pagine come PNG/JPEG), poi passala al motore OCR.

## Riepilogo – Cosa abbiamo realizzato

- **Estratto testo da immagine** usando un unico programma C# autonomo.  
- Dimostrato come **riconoscere testo da foto** con pre‑elaborazione che **migliora l’accuratezza dell’OCR**.  
- Mostrato il modo corretto di **caricare immagine per OCR** e **impostare la lingua OCR** per scenari multilingua.  

## Prossimi passi e argomenti correlati

- **Elaborazione batch:** combina questo snippet con `Directory.GetFiles` per OCR di un’intera cartella.  
- **Post‑elaborazione:** usa espressioni regolari per pulire date, importi o ID dopo l’estrazione.  
- **Integrazioni:** invia il testo estratto ad Azure Cognitive Search o Elastic per documenti ricercabili.  

Sentiti libero di sperimentare con diverse combinazioni di filtri, lingue e sorgenti di immagine. Il modello di base rimane lo stesso: crea il motore, configura le impostazioni, carica l’immagine, riconosci e restituisci. Buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}