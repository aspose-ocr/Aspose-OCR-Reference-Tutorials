---
category: general
date: 2026-06-16
description: Esegui l'OCR su un'immagine usando Aspose OCR in C#. Impara passo passo
  come ottenere risultati JSON, gestire i file e risolvere i problemi comuni.
draft: false
keywords:
- perform OCR on image
- Aspose OCR C#
- JSON result handling
- C# image recognition
- OCR engine configuration
language: it
og_description: Esegui OCR su immagine con Aspose OCR in C#. Questa guida ti accompagna
  attraverso l'output JSON, la configurazione del motore e consigli pratici.
og_title: Esegui OCR su immagine in C# – Tutorial completo di Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Perform OCR on image using Aspose OCR in C#. Learn step‑by‑step how
    to get JSON results, handle files, and troubleshoot common issues.
  headline: Perform OCR on Image in C# with Aspose – Complete Programming Guide
  type: TechArticle
- questions:
  - answer: Aspose.OCR handles PNG, JPEG, BMP, TIFF, and GIF. If you need to work
      with PDFs, convert each page to an image first (Aspose.PDF can help).
    question: What image formats are supported?
  - answer: Yes – set `ocrEngine.Settings.ResultFormat = ResultFormat.Text;`. JSON
      is preferred when you need more metadata.
    question: Can I get plain text instead of JSON?
  - answer: Feed each page image to `RecognizeImage` in a loop and concatenate the
      results, or use `RecognizePdf` which returns a combined JSON structure.
    question: How do I handle multi‑page documents?
  - answer: For batch processing, reuse a single `OcrEngine` instance rather than
      creating a new one per image. Also, enable `RecognitionMode.Fast` if accuracy
      can be traded for speed.
    question: Performance concerns?
  - answer: Without a license, the output JSON will include a watermark field. Apply
      your license early in `Main` with `License license = new License(); license.SetLicense("Aspose.OCR.lic");`.
    question: License warnings?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
title: Esegui OCR su immagine in C# con Aspose – Guida completa alla programmazione
url: /it/net/text-recognition/perform-ocr-on-image-in-c-with-aspose-complete-programming-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esegui OCR su Immagine in C# – Guida Completa alla Programmazione

Hai mai dovuto **eseguire OCR su file immagine** ma non sapevi come trasformare i pixel grezzi in testo utilizzabile? Non sei solo. Che tu stia scannerizzando ricevute, estraendo dati da passaporti o digitalizzando vecchi documenti, la capacità di **eseguire OCR su immagine** in modo programmatico è un vero punto di svolta per qualsiasi sviluppatore .NET.

In questo tutorial percorreremo un esempio pratico che mostra esattamente come **eseguire OCR su immagine** usando la libreria Aspose.OCR, catturare i risultati in JSON e salvarli per l'elaborazione successiva. Alla fine avrai un’app console pronta all’uso, spiegazioni chiare di ogni passaggio di configurazione e una serie di consigli professionali per evitare le insidie più comuni.

## Prerequisiti

Prima di immergerci, assicurati di avere:

- .NET 6.0 SDK o versioni successive installate (puoi scaricarlo dal sito di Microsoft).  
- Una licenza valida di Aspose.OCR o una prova gratuita – la libreria funziona senza licenza ma aggiunge una filigrana.  
- Un file immagine (PNG, JPEG o TIFF) su cui vuoi **eseguire OCR su immagine** – per questa guida useremo `receipt.png`.  
- Visual Studio 2022, VS Code o qualsiasi editor tu preferisca.

Non sono necessari altri pacchetti NuGet oltre a `Aspose.OCR`.

## Passo 1: Configura il Progetto e Installa Aspose.OCR

Per prima cosa, crea un nuovo progetto console e aggiungi la libreria OCR.

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

> **Consiglio professionale:** Se usi Visual Studio, puoi aggiungere il pacchetto tramite l’interfaccia UI di NuGet Package Manager. Ripristina automaticamente le dipendenze, risparmiandoti un `dotnet restore` manuale in seguito.

Ora apri `Program.cs` – sostituiremo il suo contenuto con il codice che effettivamente **esegue OCR su immagine**.

## Passo 2: Crea e Configura il Motore OCR

Il cuore di qualsiasi flusso di lavoro Aspose OCR è la classe `OcrEngine`. Di seguito la istanziamo e indichiamo al motore di restituire i risultati in JSON – un formato facile da analizzare in seguito.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonResultDemo
{
    static void Main()
    {
        // Step 2.1: Create an OCR engine instance.
        var ocrEngine = new OcrEngine();

        // Step 2.2: Tell the engine we want JSON output.
        ocrEngine.Settings.ResultFormat = ResultFormat.Json;

        // Optional: tweak language or recognition speed.
        // ocrEngine.Settings.Language = Language.English; // default is English
        // ocrEngine.Settings.RecognitionMode = RecognitionMode.Fast; // or Accurate
```

**Perché impostare `ResultFormat` su JSON?**  
JSON è indipendente dal linguaggio e può essere deserializzato in oggetti tipizzati in C#, JavaScript, Python o qualsiasi ambiente con cui ti integri. Inoltre conserva i punteggi di confidenza e le coordinate delle bounding box, utili per la validazione successiva.

## Passo 3: Esegui OCR su Immagine e Cattura il JSON

Ora che il motore è pronto, **eseguiamo OCR su immagine** chiamando `RecognizeImage`. Il metodo restituisce una stringa contenente il payload JSON.

```csharp
        // Step 3: Perform OCR on the image and capture the JSON output.
        // Replace the path with the location of your own image file.
        string imagePath = "YOUR_DIRECTORY/receipt.png";
        string jsonResult = ocrEngine.RecognizeImage(imagePath);
```

> **Caso limite:** Se l’immagine è corrotta o il percorso è errato, `RecognizeImage` lancia una `FileNotFoundException`. Avvolgi la chiamata in un blocco `try/catch` se ti serve una gestione degli errori più delicata.

## Passo 4: Salva il Risultato JSON per Ulteriori Elaborazioni

Memorizzare l’output OCR ti permette di inserirlo in database, API o componenti UI in un secondo momento. Ecco un modo semplice per scrivere il JSON su disco.

```csharp
        // Step 4: Save the JSON result for later use.
        string outputPath = "YOUR_DIRECTORY/receipt.json";
        File.WriteAllText(outputPath, jsonResult);
```

Se lavori in un ambiente cloud, potresti sostituire `File.WriteAllText` con una chiamata ad Azure Blob Storage o AWS S3 – la stringa JSON funziona allo stesso modo.

## Passo 5: Notifica l’Utente e Pulisci

Un piccolo messaggio console conferma che tutto è andato a buon fine. In un’app reale potresti loggarlo su file o inviarlo a un servizio di monitoraggio.

```csharp
        // Step 5: Inform the user that the JSON file has been saved.
        Console.WriteLine("JSON result saved to " + outputPath);
    }
}
```

Questo è l’intero flusso! Esegui il programma con `dotnet run` e dovresti vedere il messaggio di conferma, più un file `receipt.json` contenente qualcosa del genere:

```json
{
  "Pages": [
    {
      "Blocks": [
        {
          "Text": "Total: $23.45",
          "Confidence": 0.98,
          "Rectangle": { "X": 120, "Y": 340, "Width": 150, "Height": 20 }
        }
      ]
    }
  ]
}
```

## Esempio Completo e Eseguibile

Per completezza, ecco il file *esatto* che puoi copiare‑incollare in `Program.cs`. Nessuna parte è mancante.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonResultDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance.
        var ocrEngine = new OcrEngine();

        // Step 2: Configure the engine to return results in JSON format.
        ocrEngine.Settings.ResultFormat = ResultFormat.Json;

        // Optional: adjust language or recognition mode if needed.
        // ocrEngine.Settings.Language = Language.English;
        // ocrEngine.Settings.RecognitionMode = RecognitionMode.Accurate;

        // Step 3: Perform OCR on the image and capture the JSON output.
        string imagePath = "YOUR_DIRECTORY/receipt.png";
        string jsonResult = ocrEngine.RecognizeImage(imagePath);

        // Step 4: Save the JSON result for further processing.
        string outputPath = "YOUR_DIRECTORY/receipt.json";
        File.WriteAllText(outputPath, jsonResult);

        // Step 5: Notify that the JSON file has been saved.
        Console.WriteLine($"JSON result saved to {outputPath}");
    }
}
```

> **Suggerimento:** Sostituisci `YOUR_DIRECTORY` con un percorso assoluto o relativo basato sulla radice del progetto. Usare `Path.Combine(Environment.CurrentDirectory, "receipt.png")` evita separatori hard‑coded su Windows vs. Linux.

## Domande Frequenti e Trappole

- **Quali formati immagine sono supportati?**  
  Aspose.OCR gestisce PNG, JPEG, BMP, TIFF e GIF. Se devi lavorare con PDF, converti ogni pagina in immagine prima (Aspose.PDF può aiutare).

- **Posso ottenere testo semplice invece di JSON?**  
  Sì – imposta `ocrEngine.Settings.ResultFormat = ResultFormat.Text;`. JSON è preferito quando ti servono più metadati.

- **Come gestire documenti multi‑pagina?**  
  Fornisci ogni immagine di pagina a `RecognizeImage` in un ciclo e concatena i risultati, oppure usa `RecognizePdf` che restituisce una struttura JSON combinata.

- **Preoccupazioni di performance?**  
  Per elaborazioni batch, riutilizza una singola istanza di `OcrEngine` anziché crearne una nuova per immagine. Inoltre, abilita `RecognitionMode.Fast` se la precisione può essere scambiata con la velocità.

- **Avvisi di licenza?**  
  Senza licenza, il JSON di output includerà un campo filigrana. Applica la licenza subito in `Main` con `License license = new License(); license.SetLicense("Aspose.OCR.lic");`.

## Panoramica Visiva

Di seguito trovi un diagramma rapido che visualizza il flusso di dati da file immagine → motore OCR → output JSON → archiviazione. Aiuta a capire dove ogni passaggio si inserisce in una pipeline più ampia.

![Diagramma del flusso di lavoro per eseguire OCR su immagine](https://example.com/ocr-workflow.png "Diagramma del flusso di lavoro per eseguire OCR su immagine")

*Testo alternativo: Diagramma che mostra come eseguire OCR su immagine usando Aspose OCR, convertendo in JSON e salvando su file.*

## Estendere l’Esempio

Ora che sai come **eseguire OCR su immagine** e ottenere un payload JSON, potresti voler:

- **Analizzare il JSON** con `System.Text.Json` o `Newtonsoft.Json` per estrarre campi specifici.  
- **Inserire il testo in un database** per archivi ricercabili.  
- **Integrare con un’API web** così i client possono caricare immagini e ricevere risultati OCR istantaneamente.  
- **Applicare pre‑elaborazione dell’immagine** (deskew, aumento contrasto) usando `Aspose.Imaging` per migliorare l’accuratezza.

Ognuno di questi argomenti si basa sulla base che abbiamo trattato, e la stessa istanza di `OcrEngine` può essere riutilizzata in tutti i casi.

## Conclusione

Hai appena imparato come **eseguire OCR su file immagine** in C# usando Aspose OCR, configurare il motore per output JSON e persistere i risultati per usi futuri. Il tutorial ha coperto ogni riga di codice, spiegato perché ogni impostazione è importante e evidenziato i casi limite che potresti incontrare in produzione.

Da qui, sperimenta con lingue diverse (`ocrEngine.Settings.Language`), regola `RecognitionMode`, o collega il JSON a una pipeline di analisi downstream. Il cielo è il limite quando combini OCR affidabile con gli strumenti moderni di .NET.

Se questa guida ti è stata utile, considera di mettere una stella al repository GitHub di Aspose.OCR, condividere l’articolo con i colleghi o lasciare un commento con i tuoi consigli. Buon coding!

## Cosa Dovresti Imparare Dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci alternativi nei tuoi progetti.

- [Come Usare Aspose OCR per Ottenere Risultato JSON nel Riconoscimento Immagine](/ocr/english/net/text-recognition/get-result-as-json/)
- [Come Estrarre Testo da Immagine Usando Aspose.OCR per .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [Converti Immagine in Testo – Esegui OCR su Immagine da URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}