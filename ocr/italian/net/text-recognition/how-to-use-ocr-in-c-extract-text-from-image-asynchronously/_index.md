---
category: general
date: 2026-02-25
description: Come utilizzare rapidamente l'OCR in C# per estrarre testo da un'immagine,
  caricare l'immagine per l'OCR e impostare la lingua dell'OCR con Aspose OCR. Guida
  passo passo.
draft: false
keywords:
- how to use OCR
- extract text from image
- load image for OCR
- set OCR language
language: it
og_description: Scopri come utilizzare l'OCR in C# per estrarre testo da un'immagine,
  caricare l'immagine per l'OCR e impostare la lingua OCR usando Aspose OCR. Esempio
  completo asincrono.
og_title: Come usare OCR in C# – Guida completa all'asincrono
tags:
- C#
- Aspose OCR
- async programming
title: Come usare OCR in C# – Estrarre testo da un'immagine in modo asincrono
url: /it/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-asynchronously/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come usare l'OCR in C# – Estrarre testo da un'immagine in modo asincrono

Ti è mai capitato di **come usare l'OCR** su una ricevuta, fattura o modulo scansionato e di chiederti perché gli esempi di codice che trovi sono incompleti o bloccati in modalità sincrona? Non sei l'unico. In molte applicazioni reali vuoi **estrarre testo da un'immagine** senza bloccare l'interfaccia utente, e desideri anche la flessibilità di scegliere la lingua giusta per il riconoscimento.  

In questo tutorial vedremo un esempio completo, eseguibile, che ti mostra esattamente come **caricare l'immagine per l'OCR**, configurare l'opzione **impostare la lingua OCR**, ed eseguire il riconoscimento in modo asincrono. Alla fine avrai un'app console autonoma che stampa il testo riconosciuto nella console, più una serie di consigli per gestire casi limite e scalare la soluzione.

## Prerequisiti

- .NET 6.0 o successivo (il codice funziona anche con .NET Core e .NET Framework)  
- Pacchetto NuGet Aspose.OCR (`Aspose.OCR`) installato  
- Un file immagine di esempio (ad es. `receipt.jpg`) posizionato in una cartella a cui puoi fare riferimento  
- Conoscenze di base di C# – non servono trucchi async avanzati, solo le fondamenta  

Se ti manca qualcosa, aggiungi il pacchetto NuGet con `dotnet add package Aspose.OCR` e crea una semplice cartella per l'immagine di test. Nulla di complicato.

---

## Come usare l'OCR: Implementazione passo‑passo

Di seguito suddividiamo il processo in quattro passaggi logici. Ogni passaggio ha il proprio header H2, e il primo header ripete la keyword principale per soddisfare la SEO.

### Passo 1 – Inizializzare il motore OCR (How to Use OCR)

La prima cosa di cui hai bisogno è un'istanza di `OcrEngine`. Pensala come il cervello dietro l'operazione; contiene la configurazione, l'immagine e il risultato.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Enums;

public class AsyncExample
{
    public static async Task RunAsync()
    {
        // Create the OCR engine – this object will manage everything.
        var ocrEngine = new OcrEngine();

        // Next steps will configure it further.
```

**Perché è importante:**  
Creare il motore una sola volta e riutilizzarlo può migliorare le prestazioni quando elabori molte immagini. Ti offre anche un unico punto dove impostare opzioni globali come la lingua.

### Passo 2 – Impostare la lingua OCR (Set OCR Language Properly)

Se salti la selezione della lingua, Aspose OCR usa l'inglese per impostazione predefinita, il che può andare bene per le ricevute ma non per documenti stranieri. Impostare la lingua richiede una sola riga:

```csharp
        // Set the recognition language to English.
        // You can change OcrLanguage.French, OcrLanguage.Spanish, etc.
        ocrEngine.Config.Language = OcrLanguage.English;
```

**Consiglio professionale:**  
Quando ti serve il supporto multilingue, puoi passare un array di lingue (`OcrLanguage.English | OcrLanguage.French`). Il motore proverà ciascuna in ordine, utile per ricevute con più lingue.

### Passo 3 – Caricare l'immagine per l'OCR (Load Image for OCR Efficiently)

Ora puntiamo il motore al file che vogliamo leggere. Aspose fornisce `ImageStream.FromFile`, che astrae la gestione dello stream sottostante.

```csharp
        // Load the image you want to analyze.
        // Replace the path with the actual location of your image file.
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

**Caso limite:**  
Se il percorso del file è errato o il formato dell'immagine non è supportato, `FromFile` genera un'eccezione. Avvolgi il codice in un try/catch se stai costruendo un'interfaccia utente robusta.

### Passo 4 – Eseguire il riconoscimento asincrono (Extract Text from Image)

Qui avviene la magia. Il metodo `RecognizeAsync` esegue l'OCR su un thread in background, liberando il thread chiamante—perfetto per UI o app web.

```csharp
        // Run OCR asynchronously.
        var ocrResult = await ocrEngine.RecognizeAsync();

        // Display the recognized text.
        Console.WriteLine("OCR completed:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Cosa vedrai:**  
Se `receipt.jpg` contiene il testo “Total: $12.34”, l'output della console sarà:

```
OCR completed:
Total: $12.34
```

**Perché async?**  
L'OCR sincrono può bloccare il thread per diversi secondi, soprattutto con immagini ad alta risoluzione. Usare `await` mantiene l'app reattiva e si integra bene con le pipeline di richieste di ASP.NET Core.

---

## Esempio completo funzionante

Copia l'intero snippet qui sotto in un nuovo progetto console (`dotnet new console`) ed eseguilo. Ricorda di sostituire `YOUR_DIRECTORY/receipt.jpg` con il percorso reale della tua immagine.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Enums;

public class AsyncExample
{
    public static async Task Main(string[] args)
    {
        await RunAsync();
    }

    public static async Task RunAsync()
    {
        // Step 1: Create the OCR engine.
        var ocrEngine = new OcrEngine();

        // Step 2: Set the OCR language (English by default).
        ocrEngine.Config.Language = OcrLanguage.English;

        // Step 3: Load the image you want to process.
        // Ensure the file exists; otherwise an exception is thrown.
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

        // Step 4: Perform asynchronous OCR recognition.
        var ocrResult = await ocrEngine.RecognizeAsync();

        // Output the recognized text.
        Console.WriteLine("OCR completed:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Output previsto** (supponendo che l'immagine contenga testo inglese leggibile):

```
OCR completed:
Your extracted text appears here, line by line.
```

Se ottieni una stringa vuota, verifica che l'immagine sia chiara e che l'impostazione della lingua corrisponda al testo.

---

## Problemi comuni e come evitarli

| Problema | Perché accade | Soluzione |
|----------|---------------|-----------|
| **Risultato vuoto** | Immagine a bassa risoluzione o lingua errata | Usa una scansione ad alta risoluzione, o imposta `ocrEngine.Config.Language` sulla lingua corretta |
| **Eccezione su `FromFile`** | Percorso errato o formato non supportato | Verifica il percorso, usa percorsi assoluti, o converti l'immagine in PNG/JPEG prima |
| **Ritardo di prestazioni** | Elaborazione di grandi batch in modo sincrono | Elabora le immagini in parallelo usando `Task.WhenAll` e riutilizza una singola istanza di `OcrEngine` |
| **Perdita di memoria** | Stream non chiusi nel codice di caricamento personalizzato | Affidati a `ImageStream.FromFile` che gestisce la chiusura, o usa blocchi `using` se carichi manualmente |

**Suggerimento extra:**  
Se devi estrarre dati strutturati (ad es. coppie chiave‑valore da ricevute), considera di post‑processare `ocrResult.Text` con espressioni regolari o una libreria NLP leggera.

---

## Estendere la soluzione

Ora che sai **come usare l'OCR** per un'immagine singola, potresti chiederti: “E se avessi dozzine di ricevute ogni notte?”  

- **Elaborazione batch:** Avvolgi la logica `RunAsync` in un ciclo e raccogli i risultati in una lista.  
- **Parallelismo:** Usa `Parallel.ForEach` con supporto async (`Parallel.ForEachAsync` in .NET 6) per eseguire più riconoscimenti simultaneamente.  
- **Persistenza dei risultati:** Salva `ocrResult.Text` in un database, o scrivilo in un CSV per analisi successive.  

Tutte queste estensioni si basano ancora sui passaggi fondamentali trattati: inizializzare il motore, impostare la lingua, caricare l'immagine e chiamare `RecognizeAsync`.

---

## Riepilogo visivo

![esempio di come usare OCR](/images/ocr-example.png "come usare l'OCR in C# con Aspose OCR")

*Il diagramma sopra illustra il flusso dal caricamento dell'immagine al testo riconosciuto.*

---

## Conclusione

Abbiamo appena percorso un esempio completo, pronto per la produzione, che mostra **come usare l'OCR** in C# per **estrarre testo da un'immagine**, **caricare immagine per OCR** e **impostare la lingua OCR** correttamente—tutto mantenendo l'interfaccia reattiva grazie alle chiamate asincrone.  

In un unico script autonomo hai ora tutto il necessario per iniziare a estrarre testo da foto, ricevute o qualsiasi documento scansionato. Da qui puoi scalare a batch, aggiungere gestione degli errori o integrare i risultati in flussi di lavoro più ampi.

Pronto per il passo successivo? Prova a sostituire `OcrLanguage.English` con un'altra lingua, sperimenta con formati immagine diversi, o collega l'output a un semplice database. Le possibilità sono ampie quanto i documenti che devi leggere.

Domande o difficoltà? Lascia un commento qui sotto, e buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}