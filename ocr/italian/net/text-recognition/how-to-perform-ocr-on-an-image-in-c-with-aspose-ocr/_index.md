---
category: general
date: 2026-10-18
description: Esegui OCR su un'immagine in C# rapidamente. Impara a estrarre testo
  da JPG, convertire l'immagine in testo e leggere il testo dall'immagine usando Aspose.OCR.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from JPG
- convert image to text
- read text from image
- load image for OCR
language: it
lastmod: 2026-10-18
og_description: Esegui OCR su un'immagine in C# con Aspose.OCR. Questo tutorial mostra
  come estrarre testo da JPG, convertire l'immagine in testo e leggere il testo dall'immagine
  in pochi minuti.
og_image_alt: Console output displaying recognized Cyrillic text after performing
  OCR on an image
og_title: Esegui OCR su un'immagine in C# – guida completa
schemas:
- author: Aspose
  dateModified: '2026-10-18'
  description: Perform OCR on an image in C# quickly. Learn to extract text from JPG,
    convert image to text and read text from image using Aspose.OCR.
  headline: How to perform OCR on an image in C# with Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose.OCR
title: Come eseguire l'OCR su un'immagine in C# con Aspose.OCR
url: /it/net/text-recognition/how-to-perform-ocr-on-an-image-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR su un'immagine in C# con Aspose.OCR

Se hai bisogno di **eseguire OCR su un'immagine** in un'applicazione .NET, questa guida ti mostra una soluzione completa, pronta‑da‑eseguire. Vedrai come **caricare l'immagine per OCR**, riconoscere caratteri cirillici e **estrarre testo da JPG** senza scrivere alcun codice di elaborazione immagine a basso livello.

In questo tutorial imparerai a:

* Installare il pacchetto NuGet Aspose.OCR.  
* Caricare un file immagine (JPG, PNG, BMP, ecc.).  
* Eseguire il motore OCR per **convertire immagine in testo**.  
* **Leggere il testo dall'immagine** nella console.  

I passaggi funzionano con qualsiasi immagine compatibile con .NET, così potrai adattarli a PDF, ricevute scannerizzate o screenshot.

## Prerequisiti

* .NET 6.0 SDK o successivo (il codice funziona anche con .NET Framework 4.7+).  
* Visual Studio 2022 o qualsiasi editor C# tu preferisca.  
* Accesso a Internet per la prima esecuzione – Aspose.OCR scarica automaticamente il modulo della lingua cirillica.  

> **Suggerimento:** Mantieni il pacchetto NuGet aggiornato; le versioni più recenti migliorano la precisione del riconoscimento e aggiungono pacchetti linguistici.

## Passo 1: Installa Aspose.OCR

Apri un terminale nella cartella del tuo progetto ed esegui:

```bash
dotnet add package Aspose.OCR
```

Il pacchetto contiene la classe `OcrEngine` utilizzata per **eseguire OCR su immagine**. Dopo il completamento del comando, il riferimento al pacchetto appare nel tuo file *.csproj*.

## Passo 2: Crea lo scheletro di un programma console

Crea un nuovo progetto console se non ne hai già uno:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Sostituisci il *Program.cs* generato con il codice mostrato nelle sezioni successive. Lo scheletro include le direttive `using` richieste e un metodo `Main` che gestisce il processo OCR.

## Passo 3: Caricare l'immagine per OCR

La prima riga di codice **carica l'immagine** che desideri analizzare. Aspose.OCR accetta qualsiasi stream, quindi puoi caricare un file dal disco, da un URL web o da una risorsa incorporata.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Step 3: Load the image containing Cyrillic text
        // Replace the path with the location of your JPG file.
        string imagePath = @"YOUR_DIRECTORY\cyrillic-sample.jpg";
        using var image = ImageStream.FromFile(imagePath);
```

*Perché è importante*: L'uso di `ImageStream.FromFile` astrae la gestione del formato, garantendo che il motore OCR riceva un bitmap coerente indipendentemente dal tipo di file originale. Inoltre, lo stream viene smaltito automaticamente grazie all'istruzione `using`.

## Passo 4: Inizializzare il motore OCR e impostare la lingua (opzionale)

Per impostazione predefinita Aspose.OCR tenta di rilevare automaticamente la lingua. Per il testo cirillico puoi richiedere esplicitamente il modulo `Language.Cyrillic`, che velocizza il download iniziale.

```csharp
        // Step 4: Initialize the OCR engine
        var engine = new OcrEngine();

        // Optional: force Cyrillic language to avoid auto‑detection overhead
        engine.Language = Language.Cyrillic;
```

Se ometti l'assegnazione della lingua, il motore scaricherà il modulo necessario al primo utilizzo di `Recognize`. Il download avviene tramite HTTPS ed è memorizzato nella cache locale per le esecuzioni successive.

## Passo 5: Eseguire OCR e convertire immagine in testo

Ora **esegui OCR su immagine** e ottieni una stringa di testo semplice. Il metodo `Recognize` si occupa di tutta la parte pesante: pre‑elaborazione, analisi del layout e classificazione dei caratteri.

```csharp
        // Step 5: Perform OCR – convert image to text
        engine.Image = image;
        string recognizedText = engine.Recognize();
```

Il valore restituito `recognizedText` contiene interruzioni di riga che corrispondono al layout originale, facilitando il post‑processing o la memorizzazione in un database.

## Passo 6: Visualizzare il risultato – leggere il testo dall'immagine

Infine, **leggi il testo dall'immagine** scrivendo il risultato nella console. Questo passaggio verifica che l'OCR sia riuscito e mostra esattamente ciò che è stato estratto.

```csharp
        // Step 6: Display the recognized text – read text from image
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

Quando esegui il programma (`dotnet run`), dovresti vedere un output simile a:

```
=== OCR Result ===
Пример текста на кириллице
```

> **Nota:** L'output esatto dipende dalla qualità del JPG di origine. Immagini chiare e ad alta risoluzione producono i migliori risultati.

## Codice completo, eseguibile

Di seguito trovi il programma completo che puoi copiare‑incollare in *Program.cs* ed eseguire senza modifiche (ad eccezione del percorso dell'immagine).

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Load the image containing Cyrillic text
        string imagePath = @"YOUR_DIRECTORY\cyrillic-sample.jpg";
        using var image = ImageStream.FromFile(imagePath);

        // Initialize the OCR engine
        var engine = new OcrEngine
        {
            // Force Cyrillic language; optional but speeds up first run
            Language = Language.Cyrillic,
            Image = image
        };

        // Recognize the text – this converts the image to text
        string recognizedText = engine.Recognize();

        // Display the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

L'esecuzione del programma stampa i caratteri estratti nella console, dimostrando che hai **estratto testo da JPG** e **convertito immagine in testo** con successo.

## Gestire variazioni comuni

| Scenario | Adeguamento |
|----------|------------|
| **Lingua diversa** | Imposta `engine.Language = Language.English;` o un altro enum supportato. |
| **PDF multi‑pagina** | Converti ogni pagina in un'immagine (ad es., usando `Aspose.PDF`) e chiama il ciclo OCR per ciascuna immagine. |
| **Grande batch** | Avvolgi la chiamata OCR in un ciclo `Parallel.ForEach`; riutilizza una singola istanza `OcrEngine` per ridurre il consumo di memoria. |
| **Immagine a bassa risoluzione** | Pre‑elabora con `engine.Image = ImageProcessing.Filters.GaussianBlur(image, 1.5);` per ridurre il rumore prima del riconoscimento. |

Queste variazioni ti consentono di **estrarre testo da JPG** di qualsiasi lingua, dimensione o qualità.

## Consigli sulle prestazioni

* **Cache dei moduli linguistici** – il primo download può richiedere qualche secondo; le esecuzioni successive sono istantanee. |
* **Riutilizza l'istanza `OcrEngine`** per più immagini per evitare costi di inizializzazione ripetuti. |
* **Limita le dimensioni dell'immagine** – foto estremamente grandi aumentano l'uso di memoria. Ridimensiona a un massimo di 2000 px in larghezza prima di passarle al motore. |

## Conclusione

Ora sai come **eseguire OCR su immagine** in C# usando Aspose.OCR. Caricando un'immagine, configurando il motore e chiamando `Recognize`, puoi **estrarre testo da JPG**, **convertire immagine in testo** e **leggere il testo dall'immagine** con poche righe di codice.  

Da qui potresti approfondire:

* Memorizzare i risultati OCR in un database per archivi ricercabili.  
* Integrare il flusso di lavoro in un'API web che accetta immagini caricate.  
* Utilizzare altri moduli linguistici (Arabo, Hindi, ecc.) per ampliare la portata della tua applicazione.

Sentiti libero di sperimentare con diversi formati immagine, lingue e strategie di elaborazione batch. Il modello di base — **caricare immagine per OCR → riconoscere → gestire l'output di testo semplice** — rimane invariato, fornendoti una solida base per qualsiasi progetto di estrazione testo.

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Estrai testo da immagine C# con selezione della lingua usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Converti immagine in testo – Esegui OCR su immagine da URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Come estrarre testo da immagine usando Aspose.OCR per .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}