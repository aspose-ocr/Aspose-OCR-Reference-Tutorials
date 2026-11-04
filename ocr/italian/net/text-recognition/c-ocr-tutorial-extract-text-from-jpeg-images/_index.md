---
category: general
date: 2026-01-04
description: Tutorial OCR in C# che mostra come estrarre testo da JPEG, eseguire OCR
  sull'immagine e riconoscere il testo da una ricevuta usando l'accelerazione GPU.
draft: false
keywords:
- c# OCR tutorial
- extract text from JPEG
- perform OCR on image
- load image for OCR
- recognize text from receipt
language: it
og_description: Il tutorial OCR in C# ti guida nel caricamento di un'immagine per
  OCR, nell'estrazione del testo da JPEG e nel riconoscimento del testo da una ricevuta
  con supporto GPU.
og_title: Tutorial OCR in C# – Estrai il testo dalle immagini JPEG
tags:
- C#
- OCR
- Image Processing
title: Tutorial OCR in C# – Estrai il testo dalle immagini JPEG
url: /it/net/text-recognition/c-ocr-tutorial-extract-text-from-jpeg-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR tutorial – Estrarre testo da immagini JPEG

Hai mai avuto bisogno di un **c# OCR tutorial** per estrarre testo da una ricevuta scansionata o da una foto di un documento? Non sei solo. In molte app reali—tracciatori di spese, inserimento dati automatizzato, o anche un veloce strumento di annotazione—ti troverai a dover **estrarre testo da JPEG** file al volo.

In questa guida ti forniremo una soluzione completa, pronta all'uso. Imparerai come **caricare l'immagine per OCR**, **eseguire OCR sull'immagine**, e infine **riconoscere il testo dalla ricevuta** usando un motore accelerato da GPU. Niente scorciatoie vaghe tipo “vedi la documentazione”—solo il codice completo, spiegazioni sul perché ogni riga è importante e consigli per evitare gli errori più comuni.

## Cosa ti serve

- .NET 6.0 o versioni successive (il codice utilizza la sintassi moderna di C#).  
- Una libreria OCR che espone una classe `OcrEngine` con un oggetto `Config`—la maggior parte degli SDK commerciali segue questo schema.  
- Una GPU compatibile con CUDA se desideri l'accelerazione opzionale (altrimenti il fallback su CPU funziona bene).  
- Un'immagine JPEG di esempio, ad esempio `receipt.jpg`, posizionata in una cartella a cui puoi fare riferimento.

È tutto. Se hai già Visual Studio, apri un nuovo progetto console e sei pronto per copiare‑incollare.

![esempio di c# OCR tutorial che mostra l'elaborazione di un'immagine di ricevuta](https://example.com/placeholder.jpg "esempio di c# OCR tutorial")

*(Testo alternativo: c# OCR tutorial – screenshot del motore OCR che elabora un'immagine di ricevuta)*

## Passo 1 – Creare e configurare il motore OCR (fondamenta del c# OCR tutorial)

Per prima cosa istanziamo il motore e attiviamo la modalità GPU. Abilitare la GPU può ridurre di alcuni secondi il tempo di riconoscimento per grandi batch, ma è opzionale.

```csharp
using System;

// Assume the OCR SDK namespace is OcrSdk
using OcrSdk;

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Enable GPU acceleration (requires a CUDA‑compatible GPU)
        ocrEngine.Config.EnableGPU = true;   // Turn on GPU mode
        ocrEngine.Config.GpuDeviceId = 0;    // Optional: select GPU index (0 = first GPU)

        // The rest of the steps follow...
```

**Perché è importante:** Il motore contiene tutta la logica pesante—modelli linguistici, pre‑elaborazione delle immagini e la pipeline di inferenza. Attivare `EnableGPU` indica all'SDK di delegare questi calcoli alla scheda grafica, il che è particolarmente utile quando si elaborano JPEG ad alta risoluzione o decine di ricevute contemporaneamente.

## Passo 2 – Caricare l'immagine per OCR (passo “caricare immagine per OCR”)

Successivamente indirizziamo il motore verso il file che vogliamo leggere. Il percorso può essere assoluto o relativo; assicurati semplicemente che il file esista.

```csharp
        // Step 2: Load the image you want to recognize
        // Replace YOUR_DIRECTORY with the actual folder containing receipt.jpg
        string imagePath = @"YOUR_DIRECTORY/receipt.jpg";
        ocrEngine.LoadImage(imagePath);
```

**Consiglio professionale:** Se gestisci file caricati dagli utenti, valida l'estensione e la dimensione prima di chiamare `LoadImage`. Il motore OCR tipicamente si aspetta un bitmap in memoria, quindi passare un JPEG corrotto genererà un'eccezione.

## Passo 3 – Eseguire OCR sull'immagine (azione principale “eseguire OCR sull'immagine”)

Ora il motore esegue il lavoro pesante. Il metodo `Recognize` restituisce un oggetto `OcrResult` che contiene l'output di testo semplice e, opzionalmente, i punteggi di confidenza.

```csharp
        // Step 3: Perform the recognition and retrieve the text
        OcrResult ocrResult = ocrEngine.Recognize();
```

**Cosa succede dietro le quinte?** L'SDK solitamente esegue una serie di fasi:  
1. **Pre‑elaborazione** – correzione dell'inclinazione, binarizzazione, rimozione del rumore.  
2. **Rilevamento delle linee di testo** – individua dove iniziano e finiscono le parole.  
3. **Classificazione dei caratteri** – la rete neurale predice ogni glifo.  

Comprendere questo flusso ti aiuta a risolvere i problemi—se vedi output confuso, controlla la qualità dell'immagine prima di modificare le impostazioni del motore.

## Passo 4 – Estrarre testo da JPEG (visualizzare il risultato)

Infine stampiamo la stringa riconosciuta sulla console. In un'app reale potresti memorizzarla in un database, inviarla a un'API o passarla a un altro pipeline NLP.

```csharp
        // Step 4: Display the recognized text
        Console.WriteLine("Recognized Text:");
        Console.WriteLine(ocrResult.Text);

        // Keep the console window open (useful when running from VS)
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

**Output previsto:**  
Se `receipt.jpg` contiene una tipica ricevuta di supermercato, vedrai qualcosa del genere:

```
Recognized Text:
WALMART
123 Main St.
Date: 01/03/2026
Item   Qty   Price
Milk    2    $4.58
Bread   1    $2.99
Total          $7.57
```

Nota come i ritorni a capo e gli spazi siano preservati—la maggior parte degli SDK OCR cerca di mantenere intatto il layout, il che è utile quando in seguito analizzi campi come “Totale”.

## Passo 5 – Casi limite comuni e consigli (potenziare il tuo c# OCR tutorial)

- **JPEG a bassa risoluzione:** Se l'immagine è inferiore a 300 dpi, considera l'upscaling con un filtro bicubico prima di chiamare `LoadImage`.  
- **Lingue multiple:** Alcuni motori permettono di impostare `ocrEngine.Config.Language = "en,es";`. È utile quando le ricevute contengono sia testo in inglese che in spagnolo.  
- **Elaborazione batch:** Avvolgi i passaggi in un ciclo `foreach` su una lista di percorsi file. Ricorda di riutilizzare la stessa istanza `OcrEngine` per evitare il sovraccarico di reinizializzare il contesto GPU.  
- **Gestione degli errori:** Circonda la chiamata di riconoscimento con `try…catch (OcrException ex)` per catturare problemi come “GPU non disponibile” o “formato immagine non supportato”.  

```csharp
        try
        {
            OcrResult result = ocrEngine.Recognize();
            Console.WriteLine(result.Text);
        }
        catch (OcrException ex)
        {
            Console.Error.WriteLine($"OCR failed: {ex.Message}");
        }
```

## Riepilogo – Cosa abbiamo ottenuto

Ora hai un **c# OCR tutorial** che ti guida attraverso ogni fase dell'estrazione del testo da una ricevuta JPEG: creazione del motore, caricamento dell'immagine, esecuzione dell'OCR e infine recupero del risultato in testo semplice. L'esempio mostra come **eseguire OCR sull'immagine** in modo efficiente con accelerazione GPU opzionale, e dimostra il flusso di lavoro tipico per scenari di **riconoscere il testo dalla ricevuta**.

## Prossimi passi e argomenti correlati

- **Affinare la pre‑elaborazione** – sperimenta con `ocrEngine.Config.DenoiseLevel` o binarizzazione personalizzata per aumentare l'accuratezza su scansioni rumorose.  
- **Integrare con un database** – memorizza `ocrResult.Text` insieme a metadati come `imagePath` e timestamp di elaborazione.  
- **Esplorare altre parole chiave secondarie** – prova “extract text from JPEG” in un contesto di web‑service, o costruisci una piccola API che accetta un'immagine caricata e restituisce il testo riconosciuto.  
- **Passare a un provider OCR diverso** – la maggior parte degli SDK commerciali espone classi simili (`Engine`, `Config`, `Result`), quindi il modello appreso si trasferisce facilmente.  

Provalo, modifica le impostazioni, e vedrai quanto rapidamente OCR può diventare una parte affidabile del tuo toolbox C#. Buon coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}