---
category: general
date: 2026-09-06
description: conversione OCR di immagine in JSON in C# usando Aspose.OCR – guida passo‑passo
  per estrarre il testo dall'immagine e ottenere l'output JSON.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- ocr image to json
- extract text from image
- convert image to text
- recognize text from photo
- load image for ocr
language: it
lastmod: 2026-09-06
og_description: OCR immagine in JSON in C# con Aspose.OCR. Scopri come caricare un'immagine
  per l'OCR, riconoscere il testo dalla foto e convertire il risultato in JSON.
og_image_alt: Screenshot of C# code that converts an OCR image to JSON using Aspose.OCR
og_title: Converti un'immagine OCR in JSON in C# – guida completa ad Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-09-06'
  description: ocr image to json conversion in C# using Aspose.OCR – step‑by‑step
    guide to extract text from image and get JSON output.
  headline: How to convert an OCR image to JSON in C# with Aspose.OCR
  type: TechArticle
- description: ocr image to json conversion in C# using Aspose.OCR – step‑by‑step
    guide to extract text from image and get JSON output.
  name: How to convert an OCR image to JSON in C# with Aspose.OCR
  steps:
  - name: Place an image named `input.jpg` in the project root.
    text: Place an image named `input.jpg` in the project root.
  - name: Execute `dotnet run`.
    text: Execute `dotnet run`.
  - name: Observe the console output and open `output.json` to see the structured
      data.
    text: Observe the console output and open `output.json` to see the structured
      data.
  type: HowTo
- questions:
  - answer: Yes. Use `ocrEngine.SaveJson(Stream)` to write directly to a `MemoryStream`,
      then call `stream.ToArray()`.
    question: Can I get the OCR result as a byte array instead of a file?
  - answer: Aspose.OCR can accept PDF pages converted to images via Aspose.PDF, but
      the OCR engine itself works on raster images. Convert PDFs to images first,
      then **load image for ocr**.
    question: Does the engine support PDF input?
  - answer: 'Set `ocrEngine.Language = OcrLanguage.Arabic`. The JSON includes the
      correct text direction, which you can render in UI frameworks that support RTL.
      ## Conclusion You now have a complete solution for **ocr image to json** in
      C#. By loading an image, configuring the language, running the OCR engine, '
    question: How do I handle right‑to‑left scripts like Arabic?
  type: FAQPage
tags:
- Aspose.OCR
- C#
- JSON
- Image processing
title: Come convertire un'immagine OCR in JSON in C# con Aspose.OCR
url: /it/net/text-recognition/how-to-convert-an-ocr-image-to-json-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come convertire un'immagine OCR in JSON in C# con Aspose.OCR

Se hai bisogno di **ocr image to json** in un'applicazione .NET, questa guida ti mostra come farlo con Aspose.OCR. Ti accompagneremo passo passo nel caricamento di un'immagine per l'OCR, nel riconoscimento del testo da una foto e nella conversione del risultato in JSON così da poter utilizzare i dati in API o database.

Estrarre testo da file immagine è una necessità comune per l'elaborazione di fatture, la scansione di ricevute e progetti di archiviazione. Alla fine di questo tutorial sarai in grado di **convert image to text**, recuperare il risultato in plain‑text e generare un payload JSON strutturato che preserva le informazioni di layout.

## Prerequisiti

Prima di iniziare, assicurati di avere:

- .NET 6.0 SDK o successivo installato  
- Visual Studio 2022 (o qualsiasi editor che supporti .NET)  
- Un pacchetto NuGet Aspose.OCR (`Aspose.OCR`) aggiunto al tuo progetto  
- Un'immagine di esempio (`input.jpg`) posizionata in una cartella a cui puoi fare riferimento dal codice  

Non ti servono altri motori OCR; Aspose.OCR gestisce tutto internamente.

## Passo 1: Installa il pacchetto NuGet Aspose.OCR

Apri un terminale nella cartella del tuo progetto ed esegui:

```bash
dotnet add package Aspose.OCR
```

Il pacchetto include la classe `Aspose.OCR.OcrEngine`, che fornisce metodi per **load image for ocr**, la selezione della lingua e l'esportazione del risultato.

## Passo 2: Crea un nuovo progetto console C#

Se non hai ancora un progetto, creane uno:

```bash
dotnet new console -n OcrToJsonDemo
cd OcrToJsonDemo
```

Aggiungi le direttive `using` di cui avrai bisogno:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using System.IO;
```

## Passo 3: Carica l'immagine e configura il motore OCR

Il codice seguente dimostra come **load image for ocr**, impostare la lingua e preparare il motore per l'elaborazione. In questo esempio usiamo il cirillico, ma puoi passare a `OcrLanguage.English`, `OcrLanguage.French`, ecc., a seconda della lingua di origine.

```csharp
// Step 3: Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Choose the language that matches the text in the image.
// Replace OcrLanguage.Cyrillic with the language you need.
ocrEngine.Language = OcrLanguage.Cyrillic;

// Load the image file. The ImageStream class abstracts file, stream, or byte[] sources.
string imagePath = Path.Combine(Environment.CurrentDirectory, "input.jpg");
ocrEngine.Image = ImageStream.FromFile(imagePath);
```

> **Perché è importante:** Impostare la lingua corretta migliora drasticamente la precisione quando **recognize text from photo**. Il motore utilizza dizionari e set di caratteri specifici per lingua.

## Passo 4: Esegui il processo OCR e recupera i risultati

Ora esegui il motore OCR. Se il processo ha successo, puoi **extract text from image** come plain text, HTML o JSON. Aspose.OCR fornisce il metodo `SaveJson` che scrive il risultato strutturato in un file.

```csharp
// Step 4: Execute the OCR process
if (ocrEngine.Process())
{
    // Plain‑text output
    string plainText = ocrEngine.Text;
    Console.WriteLine("=== Plain Text ===");
    Console.WriteLine(plainText);

    // JSON output – includes bounding boxes, confidence scores, and line information
    string jsonPath = Path.Combine(Environment.CurrentDirectory, "output.json");
    ocrEngine.SaveJson(jsonPath);
    Console.WriteLine($"\nJSON result saved to: {jsonPath}");
}
else
{
    Console.WriteLine("OCR processing failed. Check the image path and format.");
}
```

### Struttura JSON prevista

Un tipico file `output.json` appare così (formattato per leggibilità):

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Пример текста",
          "Confidence": 0.96,
          "Rect": { "X": 45, "Y": 120, "Width": 210, "Height": 30 }
        },
        {
          "Text": "Еще одна строка",
          "Confidence": 0.93,
          "Rect": { "X": 45, "Y": 160, "Width": 230, "Height": 28 }
        }
      ]
    }
  ]
}
```

Il payload JSON contiene il testo di ogni riga, un punteggio di confidenza e il rettangolo che racchiude la riga nella foto originale. Questo rende semplice mappare il risultato OCR a elementi UI o campi di database.

## Passo 5: Codice sorgente completo per la demo

Di seguito trovi il programma completo, pronto per l'esecuzione, che realizza il flusso **ocr image to json**. Copialo in `Program.cs` ed esegui `dotnet run`.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrToJsonDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Select the language (Cyrillic in this example)
            ocrEngine.Language = OcrLanguage.Cyrillic;

            // 3️⃣ Load the image you want to process
            string imagePath = Path.Combine(Environment.CurrentDirectory, "input.jpg");
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found: {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 4️⃣ Run the OCR process
            if (ocrEngine.Process())
            {
                // 5️⃣ Retrieve plain text (optional)
                string plainText = ocrEngine.Text;
                Console.WriteLine("=== Plain Text ===");
                Console.WriteLine(plainText);

                // 6️⃣ Save the result as JSON
                string jsonPath = Path.Combine(Environment.CurrentDirectory, "output.json");
                ocrEngine.SaveJson(jsonPath);
                Console.WriteLine($"\nJSON result saved to: {jsonPath}");
            }
            else
            {
                Console.WriteLine("OCR processing failed. Verify the image format and language settings.");
            }
        }
    }
}
```

### Esecuzione dell'esempio

1. Posiziona un'immagine chiamata `input.jpg` nella radice del progetto.  
2. Esegui `dotnet run`.  
3. Osserva l'output della console e apri `output.json` per vedere i dati strutturati.

## Consigli pratici e ostacoli comuni

| Situazione | Raccomandazione |
|-----------|----------------|
| **Foto a bassa risoluzione** | Aumenta DPI prima dell'elaborazione o usa `ocrEngine.Image = ImageStream.FromFile(path, 300)` per forzare 300 DPI. |
| **Lingue miste** | Imposta `ocrEngine.Language = OcrLanguage.Multilingual` e, facoltativamente, fornisci una lista di lingue tramite `ocrEngine.Language = new[] { OcrLanguage.English, OcrLanguage.Cyrillic }`. |
| **Documenti di grandi dimensioni** | Elabora una pagina alla volta per mantenere basso l'uso di memoria; il motore supporta TIFF multi‑pagina. |
| **Caratteri errati** | Verifica di aver selezionato il `OcrLanguage` corretto; usare la lingua sbagliata riduce la precisione quando **convert image to text**. |
| **JSON senza campi** | Assicurati di usare Aspose.OCR versione 23.6 o successiva; le versioni più vecchie non esponevano il metodo `SaveJson`. |

## Domande frequenti

**D: Posso ottenere il risultato OCR come array di byte invece che come file?**  
R: Sì. Usa `ocrEngine.SaveJson(Stream)` per scrivere direttamente su un `MemoryStream`, poi chiama `stream.ToArray()`.

**D: Il motore supporta input PDF?**  
R: Aspose.OCR può accettare pagine PDF convertite in immagini tramite Aspose.PDF, ma il motore OCR stesso opera su immagini raster. Converti i PDF in immagini prima, poi **load image for ocr**.

**D: Come gestisco script da destra a sinistra come l'arabo?**  
R: Imposta `ocrEngine.Language = OcrLanguage.Arabic`. Il JSON include la direzione corretta del testo, che puoi renderizzare in framework UI che supportano RTL.

## Conclusione

Ora disponi di una soluzione completa per **ocr image to json** in C#. Caricando un'immagine, configurando la lingua, eseguendo il motore OCR e esportando il risultato in JSON, puoi **extract text from image**, **convert image to text** e **recognize text from photo** in un unico flusso ottimizzato.  

Da qui potresti approfondire:

- Integrare l'output JSON con una Web API (`ASP.NET Core`)  
- Salvare il risultato in un database NoSQL come MongoDB  
- Aggiungere post‑processing per correggere errori OCR comuni  

Sentiti libero di sperimentare con lingue diverse, formati immagine e opzioni di output per adattare la soluzione alle esigenze del tuo progetto. Buon coding!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [recognize text from image in C# – Complete Guide to OCR and JSON](/ocr/english/net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/)
- [Convert Image to Text in C# with Aspose OCR – Step‑by‑Step Guide](/ocr/english/net/text-recognition/convert-image-to-text-in-c-with-aspose-ocr-step-by-step-guid/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}