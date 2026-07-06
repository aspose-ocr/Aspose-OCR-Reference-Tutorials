---
category: general
date: 2026-03-07
description: Impara come usare l'OCR in C# per estrarre testo da file immagine. Questa
  guida mostra l'OCR offline, la conversione dell'immagine in testo e il caricamento
  dell'immagine per l'OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from png
- convert image to text
- load image for ocr
language: it
og_description: Come utilizzare OCR in C# per estrarre testo dalle immagini offline.
  Codice passo‑passo, consigli e spiegazione completa per convertire l’immagine in
  testo.
og_title: Come utilizzare OCR in C# – Guida completa offline
tags:
- OCR
- C#
- Aspose
title: Come utilizzare l'OCR in C# – Estrarre testo dalle immagini offline
url: /it/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-offline/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come utilizzare OCR in C# – Estrarre testo da immagini offline

Ti sei mai chiesto **come utilizzare OCR** in un progetto .NET senza inviare dati al cloud? Non sei l'unico. Molti sviluppatori hanno bisogno di *estrarre testo da file immagine* su una postazione sicura e temono che il traffico di rete possa esporre informazioni sensibili.  

La buona notizia? Con Aspose.OCR puoi riconoscere testo da PNG, JPEG o PDF interamente offline. In questo tutorial vedremo come caricare un'immagine per OCR, configurare il motore in modalità offline e infine **convertire immagine in testo** con poche righe di C#.

Al termine di questa guida sarai in grado di:

* Installare il pacchetto NuGet Aspose.OCR.  
* Configurare il motore OCR per l'elaborazione offline.  
* Caricare un'immagine per OCR ed estrarne il contenuto testuale.  

Nessun servizio esterno, nessuna chiave API—solo puro codice C# che gira su qualsiasi macchina Windows o Linux.

---

## Prerequisiti

Prima di immergerci, assicurati di avere:

* .NET 6.0 SDK o successivo (il codice funziona anche con .NET Framework 4.7+).  
* Visual Studio 2022, VS Code o qualsiasi editor che supporti C#.  
* Una copia della libreria **Aspose.OCR** – puoi ottenerla da NuGet (`Aspose.OCR`).  
* Una cartella delle risorse OCR (`Resources`) fornita con la libreria (contiene i file dei dati linguistici).  
* Un'immagine di esempio (ad es., `offline_test.png`) posizionata in una directory nota.

> **Consiglio:** Mantieni la cartella delle risorse accanto al tuo eseguibile; semplifica la configurazione di `ResourcesPath`.

---

## Passo 1: Installa il pacchetto NuGet Aspose.OCR

Per prima cosa, aggiungi la libreria al tuo progetto. Apri un terminale nella cartella del progetto ed esegui:

```bash
dotnet add package Aspose.OCR
```

Oppure, se preferisci l'interfaccia di Visual Studio, fai clic destro su **Dependencies → Manage NuGet Packages**, cerca *Aspose.OCR* e fai clic su **Install**.

> L'installazione del pacchetto scarica tutti i binari necessari, quindi non avrai bisogno di DLL aggiuntive.

---

## Passo 2: Crea e configura il motore OCR (Come utilizzare OCR – Modalità offline)

Ora istanzieremo il motore OCR e gli diremo di operare **offline**. Questo garantisce che non avvenga traffico di rete durante il riconoscimento.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Switch the engine to offline mode – crucial for privacy‑first apps
ocrEngine.Settings.EngineMode = EngineMode.Offline;
```

**Perché offline?**  
Quando `EngineMode` è impostato su `Online`, il motore contatta il cloud di Aspose per scaricare i pacchetti linguistici al volo. In ambienti regolamentati (finanza, sanità) quel traffico è spesso proibito. Forzando la modalità offline garantisci che tutto rimanga sulla macchina locale.

---

## Passo 3: Indica al motore la cartella delle risorse OCR

Il motore OCR necessita dei dati linguistici (modelli addestrati) per riconoscere i caratteri. Indica dove si trovano questi file:

```csharp
// Replace with the absolute or relative path to your Resources folder
ocrEngine.Settings.ResourcesPath = @"C:\MyProject\Resources";
```

Se non sei sicuro di dove si trovi la cartella, cercala nella directory del pacchetto NuGet (`%USERPROFILE%\.nuget\packages\aspose.ocr\*\resources`). Copia l'intera cartella nel tuo progetto per una distribuzione più semplice.

---

## Passo 4: Carica l'immagine per OCR (Load Image for OCR)

Puoi fornire al motore qualsiasi bitmap supportata. Qui caricheremo un PNG memorizzato su disco:

```csharp
// Load the image you want to recognize – this is the “load image for OCR” step
ocrEngine.Image = ImageStream.FromFile(@"C:\MyProject\offline_test.png");
```

**Suggerimento:** Se hai bisogno di elaborare immagini da uno stream (ad es., caricate tramite un'API), usa `ImageStream.FromStream(yourStream)`.

---

## Passo 5: Esegui il processo di riconoscimento e converti l'immagine in testo

Con tutto pronto, avvia l'OCR. Il metodo `Recognize()` fa il lavoro pesante, e il testo estratto è disponibile tramite la proprietà `Text`.

```csharp
// Perform OCR – this is where the engine reads the pixels and produces text
ocrEngine.Recognize();

// Grab the result – now you have “convert image to text” completed
string extractedText = ocrEngine.Text;
```

---

## Passo 6: Visualizza il testo estratto

Infine, visualizza il risultato. In un'app console puoi semplicemente scrivere sulla console, ma in un'API web restituiresti la stringa come JSON.

```csharp
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(extractedText);
```

Eseguendo il programma dovrebbe stampare il contenuto testuale di `offline_test.png`. Ad esempio, se l'immagine contiene la frase *“Hello, World!”*, vedrai:

```
=== OCR Result ===
Hello, World!
```

---

## Esempio completo funzionante

Di seguito trovi il programma completo, pronto per l'esecuzione. Copialo e incollalo in un nuovo progetto console (`dotnet new console`) e adatta i percorsi al tuo ambiente.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // Step 2: Set offline mode – no network traffic
        // -------------------------------------------------
        ocrEngine.Settings.EngineMode = EngineMode.Offline;

        // -------------------------------------------------
        // Step 3: Provide path to OCR resource files
        // -------------------------------------------------
        ocrEngine.Settings.ResourcesPath = @"C:\MyProject\Resources";

        // -------------------------------------------------
        // Step 4: Load the image you want to recognize
        // -------------------------------------------------
        ocrEngine.Image = ImageStream.FromFile(@"C:\MyProject\offline_test.png");

        // -------------------------------------------------
        // Step 5: Run recognition and extract text
        // -------------------------------------------------
        ocrEngine.Recognize();
        string extractedText = ocrEngine.Text;

        // -------------------------------------------------
        // Step 6: Show the result
        // -------------------------------------------------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(extractedText);
    }
}
```

> **Output previsto:** La console stampa il testo esatto contenuto nel file PNG. Se l'immagine è sfocata, il risultato può includere caratteri riconosciuti in modo errato—vedi la sezione di risoluzione dei problemi qui sotto.

---

## Problemi comuni e consigli (Riconoscere testo da PNG in modo efficiente)

| Problema | Perché succede | Come risolvere |
|----------|----------------|----------------|
| **Output vuoto** | `ResourcesPath` punta alla cartella sbagliata o mancano i file linguistici. | Verifica che la cartella contenga `eng.traineddata` (o altri file di lingua) e ricontrolla la stringa del percorso. |
| **Caratteri spazzatura** | La risoluzione dell'immagine è troppo bassa o l'immagine non è binarizzata. | Pre‑elabora l'immagine (aumenta DPI, applica `ImageProcessor` per affinare). |
| **Ritardo di prestazioni** | Le immagini grandi vengono elaborate a piena risoluzione. | Ridimensiona l'immagine a una larghezza massima di 2000 px prima di passarla a OCR. |
| **Formato non supportato** | Uso di un BMP con un formato pixel insolito. | Converti l'immagine in PNG o JPEG prima (`System.Drawing.Image.Save`). |

**Consiglio:** Se devi riconoscere più lingue, imposta `ocrEngine.Settings.Language = Language.English | Language.French;` prima di chiamare `Recognize()`.

---

## Domande frequenti

**D: Posso usare questo codice su Linux?**  
Assolutamente. Aspose.OCR è cross‑platform; basta assicurarsi che le librerie native siano presenti (sono incluse nel pacchetto NuGet).  

**D: E se non ho una cartella Resources?**  
Puoi scaricare i pacchetti linguistici gratuiti dal sito di Aspose o estrarli dal pacchetto NuGet (`.../aspose.ocr/<version>/resources`).  

**D: È possibile ottenere i punteggi di confidenza?**  
Sì. Dopo `Recognize()`, ispeziona `ocrEngine.RecognizedWords` – ogni parola include una proprietà `Confidence`.

---

## Conclusione

Abbiamo coperto **come utilizzare OCR** in C# per *estrarre testo da file immagine* completamente offline. Installando Aspose.OCR, configurando `EngineMode.Offline`, indicando le risorse, caricando un'immagine e chiamando `Recognize()`, puoi affidabilmente **convertire immagine in testo** senza mai toccare Internet.  

Prendi il codice sopra, sostituisci i percorsi delle tue immagini e inizia a costruire funzionalità come PDF ricercabili, automazione dell'inserimento dati o strumenti di accessibilità. Successivamente, potresti esplorare **riconoscere testo da PNG** in blocco, o integrare il motore in un'API ASP.NET Core per fornire risultati OCR alle applicazioni front‑end.  

Buona programmazione, e sentiti libero di sperimentare—OCR è sorprendentemente indulgente una volta che il motore è configurato correttamente!

--- 

![Diagramma che mostra il flusso di lavoro OCR offline – come utilizzare OCR in un ambiente sicuro](https://example.com/ocr-workflow.png "diagramma di come utilizzare OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}