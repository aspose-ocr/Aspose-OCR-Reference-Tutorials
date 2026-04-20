---
category: general
date: 2026-03-05
description: Come ottenere OCR rapidamente usando Aspose.OCR e riconoscere il testo
  da uno stream in pochi semplici passaggi. Scopri il codice C# completo e i consigli
  per lo streaming dei dati immagine.
draft: false
keywords:
- how to get OCR
- recognize text from stream
- Aspose OCR
- streaming OCR C#
- image chunk processing
language: it
og_description: Come ottenere OCR in C# e riconoscere il testo da uno stream usando
  Aspose.OCR. Segui questo tutorial passo‑passo per una soluzione pronta all'uso.
og_title: Come ottenere OCR in C# – Guida completa al riconoscimento di flussi
tags:
- OCR
- C#
- Aspose
title: Come ottenere OCR in C# – Riconoscere il testo da uno stream
url: /it/net/text-recognition/how-to-get-ocr-in-c-recognize-text-from-stream/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come ottenere OCR in C# – Riconoscere il testo dallo stream

Ti sei mai chiesto **come ottenere OCR** in un'app .NET senza prima salvare l'intera immagine su disco? Non sei l'unico. Molti sviluppatori hanno bisogno di **riconoscere il testo dallo stream** — ad esempio quando si elaborano immagini che arrivano tramite rete, un feed di telecamera o un'API di storage cloud.  

In questo tutorial percorreremo un esempio completo, pronto‑da‑eseguire, che mostra esattamente questo. Alla fine avrai un programma C# autonomo che crea un motore Aspose OCR, invia i blocchi di immagine in streaming e stampa il testo estratto sulla console. Nessuno strumento esterno misterioso, solo codice chiaro e qualche consiglio pratico.

## Cosa imparerai

- Come installare e licenziare la libreria Aspose.OCR.  
- Come alimentare i dati dell'immagine pezzo‑per‑pezzo usando il metodo `AppendChunk`.  
- Come avviare e terminare il ciclo di riconoscimento (`BeginRecognize` / `EndRecognize`).  
- Come gestire casi limite comuni come blocchi incompleti o errori di licenza.  
- Come appare l'output e come verificarlo.

### Prerequisiti

- .NET 6.0 o successivo (il codice funziona anche con .NET Core e .NET Framework).  
- Un file di licenza Aspose OCR valido (`Aspose.OCR.lic`). Puoi ottenerlo in prova gratuita dal sito Aspose.  
- Familiarità di base con C# e `async`/`await` se vuoi leggere da uno stream asincrono (l'esempio usa uno stub sincrono per chiarezza).

> **Perché è importante:** Lo streaming OCR ti consente di mantenere basso l'uso di memoria e ridurre la latenza quando si trattano immagini di grandi dimensioni o feed video continui. È un modello che troverai in scanner di documenti in tempo reale, app mobili e pipeline di elaborazione lato server.

## Passo 1: Configura il progetto e aggiungi Aspose.OCR

Per prima cosa, crea un nuovo progetto console e aggiungi il pacchetto NuGet Aspose.OCR.

```bash
dotnet new console -n StreamOcrDemo
cd StreamOcrDemo
dotnet add package Aspose.OCR
```

> **Suggerimento:** Se usi Visual Studio, fai clic destro sul progetto → *Manage NuGet Packages* → cerca “Aspose.OCR” e installa l'ultima versione stabile.

Ora aggiungi il file di licenza nella radice del progetto e imposta la proprietà **Copy to Output Directory** su **Copy always**. Questo garantisce che il file sia disponibile a runtime.

```csharp
// Program.cs – top of the file
using System;
using System.IO;
using Aspose.OCR;
```

## Passo 2: Inizializza il motore OCR e applica la licenza

Creare il motore è semplice, ma l'applicazione della licenza **deve** avvenire prima di qualsiasi chiamata di riconoscimento; altrimenti incorrerai in una restrizione di modalità di prova.

```csharp
static OcrEngine InitializeOcrEngine()
{
    var engine = new OcrEngine();

    // Load the license – adjust the path if your file lives elsewhere
    string licensePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "Aspose.OCR.lic");
    if (!File.Exists(licensePath))
    {
        Console.Error.WriteLine("License file not found at " + licensePath);
        Environment.Exit(1);
    }

    engine.SetLicense(licensePath);
    return engine;
}
```

> **Perché lo facciamo:** Impostare la licenza subito garantisce che tutte le successive chiamate API vengano eseguite in modalità completa, evitando il watermark “evaluation version”.

## Passo 3: Simula una sorgente in streaming

In un'app reale leggeresti da un `NetworkStream`, `FileStream` o da un SDK di telecamera. Per dimostrazione, imitermo uno stream con un helper che restituisce un array di byte che rappresenta un blocco di immagine JPEG.

```csharp
static byte[] GetNextChunk()
{
    // Replace this with your actual streaming logic.
    // Here we simply read the whole file and pretend it’s a single chunk.
    string sampleImagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "sample.jpg");
    if (!File.Exists(sampleImagePath))
    {
        Console.Error.WriteLine("Sample image not found at " + sampleImagePath);
        Environment.Exit(1);
    }

    return File.ReadAllBytes(sampleImagePath);
}
```

> **Nota su casi limite:** Se ricevi molti piccoli blocchi, puoi chiamare ripetutamente `engine.Image.AppendChunk(chunk)` prima di terminare il riconoscimento. Il motore effettua il buffering internamente finché non ha dati sufficienti per iniziare l'elaborazione.

## Passo 4: Alimenta i dati dell'immagine pezzo‑per‑pezzo ed esegui OCR

Ora mettiamo tutto insieme. La sequenza è:

1. `BeginRecognize()` – indica al motore che stiamo per fornire dati.  
2. `AppendChunk()` – aggiunge ogni array di byte (puoi ciclare su molti blocchi).  
3. `EndRecognize()` – segnala che l'ultimo blocco è stato inviato e avvia il vero riconoscimento.

```csharp
static string PerformOcr(OcrEngine engine, byte[] imageChunk)
{
    // Start the recognition session
    engine.BeginRecognize();

    // Feed the image data. If you have multiple chunks, call this in a loop.
    engine.Image.AppendChunk(imageChunk);

    // End the session – the engine now processes the accumulated data.
    engine.EndRecognize();

    // Retrieve the result object; .Text holds the plain string.
    return engine.GetResult().Text;
}
```

## Passo 5: Metti tutto insieme in `Main`

Ecco il metodo `Main` completo che collega tutto, stampa il testo riconosciuto e rilascia correttamente il motore.

```csharp
static void Main(string[] args)
{
    // 1️⃣ Initialize OCR engine with license
    var ocrEngine = InitializeOcrEngine();

    try
    {
        // 2️⃣ Get a chunk of image data (replace with your streaming source)
        byte[] imageChunk = GetNextChunk();

        // 3️⃣ Run OCR on the streamed data
        string recognizedText = PerformOcr(ocrEngine, imageChunk);

        // 4️⃣ Output the result
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
    catch (Exception ex)
    {
        // Helpful error handling – you’ll often see OCR exceptions when the image is corrupted.
        Console.Error.WriteLine("OCR failed: " + ex.Message);
    }
    finally
    {
        // Release any native resources held by the engine.
        ocrEngine.Dispose();
    }
}
```

### Output previsto

Se `sample.jpg` contiene la frase “Hello, World!” dovresti vedere:

```
=== Recognized Text ===
Hello, World!
```

Se l'immagine è sfocata o il blocco è incompleto, l'output potrebbe essere vuoto o contenere caratteri illeggibili — per questo è fondamentale gestire correttamente i blocchi (assicurandosi che l'ultimo blocco sia inviato).

## Gestione di più blocchi (Avanzato)

Quando si lavora con dati realmente in streaming, riceverai probabilmente molti piccoli pezzi. Il modello qui sotto mostra come ciclare fino a quando la sorgente termina.

```csharp
static string OcrFromStream(OcrEngine engine, Stream source)
{
    engine.BeginRecognize();

    byte[] buffer = new byte[8192]; // 8 KB per read – adjust as needed
    int bytesRead;
    while ((bytesRead = source.Read(buffer, 0, buffer.Length)) > 0)
    {
        // If the last read returned fewer bytes, copy only that many.
        if (bytesRead < buffer.Length)
        {
            byte[] chunk = new byte[bytesRead];
            Array.Copy(buffer, chunk, bytesRead);
            engine.Image.AppendChunk(chunk);
        }
        else
        {
            engine.Image.AppendChunk(buffer);
        }
    }

    engine.EndRecognize();
    return engine.GetResult().Text;
}
```

> **Perché è utile:** Trasmettendo direttamente da un `NetworkStream` o `FileStream`, non carichi mai l'intera immagine in memoria, il che è particolarmente vantaggioso per PDF di grandi dimensioni o foto ad alta risoluzione.

## Problemi comuni & Come evitarli

| Problema | Sintomo | Soluzione |
|----------|----------|-----------|
| Licenza non trovata | `SetLicense` lancia `FileNotFoundException` | Verifica il percorso e imposta *Copy to Output Directory* su *Copy always*. |
| Risultato vuoto | Nessun testo stampato | Assicurati di aver chiamato `BeginRecognize` **prima** di `AppendChunk` e `EndRecognize` **dopo** l'ultimo blocco. |
| Perdita di memoria | L'app rallenta dopo molte chiamate OCR | Disporre (`Dispose`) l'`OcrEngine` dopo ogni utilizzo o riutilizzare una singola istanza con chiamate `Dispose` appropriate. |
| Blocco corrotto | Caratteri illeggibili | Convalida la dimensione del blocco; per JPEG/PNG i primi byte dovrebbero iniziare con `0xFF 0xD8` o `0x89 0x50`. |

## Bonus: Uso di stream asincroni

Se la tua sorgente è uno stream di risposta `HttpClient`, puoi adattare il ciclo a letture `await`:

```csharp
static async Task<string> OcrFromAsyncStream(OcrEngine engine, Stream asyncSource)
{
    engine.BeginRecognize();

    byte[] buffer = new byte[8192];
    int bytesRead;
    while ((bytesRead = await asyncSource.ReadAsync(buffer, 0, buffer.Length)) > 0)
    {
        if (bytesRead < buffer.Length)
        {
            var chunk = new byte[bytesRead];
            Array.Copy(buffer, chunk, bytesRead);
            engine.Image.AppendChunk(chunk);
        }
        else
        {
            engine.Image.AppendChunk(buffer);
        }
    }

    engine.EndRecognize();
    return engine.GetResult().Text;
}
```

Questo mantiene l'interfaccia reattiva in app desktop o mobile e massimizza il throughput sui server.

## Conclusione

Ora disponi di una **soluzione completa e autonoma per ottenere OCR** in C# e **riconoscere il testo dallo stream** usando Aspose.OCR. Il tutorial ha coperto tutto, dalla licenza e inizializzazione all'invio dei blocchi di immagine, alla gestione dei casi limite, fino a una variante asincrona.  

Provalo — sostituisci `sample.jpg` con un feed di telecamera live, un'immagine memorizzata nel cloud o un upload multipart HTTP. Una volta acquisita dimestichezza, esplora funzionalità avanzate come i language pack, il preprocessing personalizzato o l'elaborazione batch di più stream.

**Passi successivi:**  
- Prova OCR su PDF convertendo prima ogni pagina in immagine.  
- Sperimenta con `engine.Config` per aumentare la precisione su font specifici.  
- Combina il tutto con Azure Functions o AWS Lambda per pipeline serverless di estrazione testo.

Buona programmazione, e che i tuoi stream siano sempre nitidi e i risultati OCR impeccabili!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}