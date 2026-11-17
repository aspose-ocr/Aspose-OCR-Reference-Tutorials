---
category: general
date: 2026-04-26
description: Estrai il testo da un'immagine in C# usando Aspose.OCR e impara a convertire
  l'immagine nei formati JSON e XML in pochi minuti.
draft: false
keywords:
- extract text from image
- convert image to json
- convert image to xml
- Aspose OCR C#
- image to JSON C#
- image to XML C#
language: it
og_description: Estrai il testo da un'immagine in C# con Aspose.OCR. Scopri passo
  passo come convertire il risultato in JSON e XML istantaneamente.
og_title: Estrai il testo da un'immagine in C# – Converti in JSON e XML
tags:
- OCR
- C#
- Aspose
- JSON
- XML
title: Estrai testo da immagine in C# – Converti in JSON e XML
url: /it/net/text-recognition/extract-text-from-image-in-c-convert-to-json-xml/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai testo da immagine in C# – Converti in JSON e XML

Ti è mai capitato di dover **estrarre testo da un'immagine** in un progetto .NET ma di rimanere bloccato sul “come ottengo effettivamente i dati?” Non sei solo. In molte applicazioni reali — pensa all'elaborazione di fatture, alla scansione di ricevute o alla verifica di badge — estrarre i caratteri grezzi da un'immagine è il primo, cruciale passaggio.  

La buona notizia? Con Aspose.OCR puoi farlo in poche righe, per poi convertire immediatamente **l'immagine in JSON** o **l'immagine in XML** per i sistemi a valle. In questa guida percorreremo il codice completo, pronto per l'esecuzione, spiegheremo perché ogni parte è importante e ti mostreremo alcuni trucchi per evitare le insidie più comuni.

---

## Cosa ti servirà

- **.NET 6+** (qualsiasi SDK recente funziona; il campione è destinato a .NET 6)
- **Aspose.OCR for .NET** pacchetto NuGet  
  ```bash
  dotnet add package Aspose.OCR
  ```
- Un file immagine (PNG, JPG, ecc.) che contiene testo stampabile; useremo `invoice.png` come esempio.
- Un editor di codice — Visual Studio, VS Code o Rider — quello che preferisci.

È tutto. Nessun motore OCR aggiuntivo, nessun servizio esterno, solo un singolo pacchetto NuGet.

---

## Passo 1: Configura il motore OCR – Come estrarre testo da un'immagine

Per prima cosa creiamo un'istanza di `OcrEngine` e la puntiamo al file immagine. Questo passo è la base; senza un'immagine caricata correttamente il motore non può riconoscere nulla.

```csharp
using Aspose.OCR;
using System.IO;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process
// Replace YOUR_DIRECTORY with the actual folder path
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/invoice.png");

// Optional: verify the image was loaded
if (ocrEngine.Image == null)
{
    throw new FileNotFoundException("Image not found. Check the path and filename.");
}
```

**Perché è importante:**  
- `OcrEngine` incapsula tutta la pre‑elaborazione dell'immagine a basso livello (binarizzazione, correzione dell'inclinazione).  
- Caricare l'immagine tramite `ImageStream.FromFile` garantisce che il motore legga i byte esatti, preservando DPI e profondità di colore — entrambi possono influenzare l'accuratezza del riconoscimento.  

> **Consiglio professionale:** Se le tue immagini di origine sono in uno stream (ad es., caricate tramite un'API web), usa `ImageStream.FromStream(yourStream)` invece di `FromFile`.

---

## Passo 2: Indica al motore quale lingua aspettarsi – estrarre testo da immagine con precisione

Aspose.OCR supporta molti alfabeti. Specificare la lingua corretta restringe il set di caratteri e aumenta l'accuratezza.

```csharp
// Set the language; Latin covers English, French, German, etc.
ocrEngine.Language = Language.Latin;
```

**Perché:**  
Quando imposti `Language.Latin`, il motore OCR ignora i glifi cirillici o asiatici, riducendo i falsi positivi. Se in seguito devi gestire documenti multilingua, puoi passare a `Language.Multilingual` o combinare più lingue.

---

## Passo 3: Esegui il processo di riconoscimento – estrarre testo da immagine in una sola chiamata

Ora riconosciamo effettivamente il testo. Il metodo `Recognize` restituisce un oggetto `RecognitionResult` che contiene il testo grezzo, i punteggi di confidenza e anche i dati di layout.

```csharp
// Perform OCR
RecognitionResult recognitionResult = ocrEngine.Recognize();

// Quick sanity check
if (recognitionResult == null || string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text was detected. Verify the image quality.");
    return;
}

// Print the raw extracted text to the console
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(recognitionResult.Text);
```

**Perché:**  
Chiamare `Recognize` una sola volta è sufficiente perché il motore esegue internamente pre‑elaborazione, segmentazione e classificazione dei caratteri. La proprietà `Text` fornisce una rappresentazione stringa semplice, perfetta per il logging o una rapida validazione.

---

## Passo 4: Converti il risultato in JSON – converti immagine in JSON facilmente

Molti servizi moderni preferiscono payload JSON. Aspose.OCR fornisce un comodo metodo `ToJson` che serializza l'intero `RecognitionResult`, includendo i valori di confidenza e le bounding box.

```csharp
// Serialize the result to JSON
string jsonResult = recognitionResult.ToJson();

// Save the JSON to a file
File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonResult);

Console.WriteLine("JSON file saved at YOUR_DIRECTORY/invoice.json");
```

**Perché potresti volere JSON:**  
- **Interoperabilità:** Le app front‑end (React, Angular) possono consumare direttamente il JSON.  
- **Debugging:** Il JSON include la confidenza per carattere, permettendoti di segnalare parole a bassa confidenza per una revisione manuale.  

> **Caso limite:** Se il tuo sistema a valle ha bisogno solo del testo semplice, puoi estrarre `recognitionResult.Text` e avvolgerlo in un oggetto JSON personalizzato invece del payload completo di Aspose.

---

## Passo 5: Converti il risultato in XML – converti immagine in XML per sistemi legacy

Alcune aziende si affidano ancora a schemi XML per lo scambio di dati. Il metodo `ToXml` rispecchia `ToJson` ma produce XML.

```csharp
// Serialize the result to XML
string xmlResult = recognitionResult.ToXml();

// Save the XML to a file
File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlResult);

Console.WriteLine("XML file saved at YOUR_DIRECTORY/invoice.xml");
```

**Perché XML:**  
- **Validazione schema:** Puoi definire un XSD che corrisponde alla struttura emessa da Aspose, garantendo la conformità al contratto.  
- **Integrazione:** I vecchi sistemi ERP o di gestione documentale spesso analizzano XML nativamente.

---

## Esempio completo funzionante – Codice tutto in uno

Di seguito trovi il programma completo che unisce tutto. Copialo e incollalo in un nuovo progetto console (`dotnet new console`) ed eseguilo.

```csharp
using Aspose.OCR;
using System;
using System.IO;

namespace ImageOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Initialize OCR engine and load the image
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();
            // Adjust the path to point at your PNG/JPG file
            string imagePath = "YOUR_DIRECTORY/invoice.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            if (ocrEngine.Image == null)
            {
                Console.WriteLine($"Unable to load image at {imagePath}");
                return;
            }

            // -------------------------------------------------
            // Step 2: Specify language (Latin for most European scripts)
            // -------------------------------------------------
            ocrEngine.Language = Language.Latin;

            // -------------------------------------------------
            // Step 3: Run OCR and get the result
            // -------------------------------------------------
            RecognitionResult result = ocrEngine.Recognize();

            if (result == null || string.IsNullOrWhiteSpace(result.Text))
            {
                Console.WriteLine("No text detected – check image quality or language setting.");
                return;
            }

            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(result.Text);
            Console.WriteLine();

            // -------------------------------------------------
            // Step 4: Convert to JSON (convert image to json)
            // -------------------------------------------------
            string json = result.ToJson();
            string jsonPath = "YOUR_DIRECTORY/invoice.json";
            File.WriteAllText(jsonPath, json);
            Console.WriteLine($"JSON output written to {jsonPath}");

            // -------------------------------------------------
            // Step 5: Convert to XML (convert image to xml)
            // -------------------------------------------------
            string xml = result.ToXml();
            string xmlPath = "YOUR_DIRECTORY/invoice.xml";
            File.WriteAllText(xmlPath, xml);
            Console.WriteLine($"XML output written to {xmlPath}");
        }
    }
}
```

**Output previsto (console):**

```
=== Extracted Text ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...

JSON file saved at YOUR_DIRECTORY/invoice.json
XML file saved at YOUR_DIRECTORY/invoice.xml
```

I file JSON e XML conterranno una struttura più ricca, ad esempio:

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑15\nTotal: $1,250.00",
  "Confidence": 0.96,
  "Blocks": [
    { "Text": "Invoice #12345", "Confidence": 0.98, "Rectangle": { "X": 12, "Y": 30, "Width": 200, "Height": 20 } },
    ...
  ]
}
```

```xml
<RecognitionResult>
  <Text>Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00</Text>
  <Confidence>0.96</Confidence>
  <Blocks>
    <Block>
      <Text>Invoice #12345</Text>
      <Confidence>0.98</Confidence>
      <Rectangle X="12" Y="30" Width="200" Height="20"/>
    </Block>
    ...
  </Blocks>
</RecognitionResult>
```

---

## Domande comuni e casi limite

### Cosa succede se l'immagine è sfocata o ruotata?

Aspose.OCR corregge automaticamente l'inclinazione della maggior parte delle immagini, ma per casi estremi potresti voler pre‑elaborare con `ocrEngine.Image = ImageProcessor.Deskew(ocrEngine.Image)`. Aggiungere un leggero aumento del contrasto (`ImageProcessor.AdjustContrast`) può migliorare anche il punteggio di confidenza.

### Posso estrarre testo da PDF?

Sì — converti prima ogni pagina PDF in un'immagine (ad esempio, usando Aspose.PDF o una libreria gratuita come PDFium) e poi passa quelle immagini nello stesso flusso OCR.

### Come gestisco più lingue in un unico documento?

Imposta `ocrEngine.Language = Language.Multilingual;` o combina lingue specifiche:

```csharp
ocrEngine.Language = Language.English | Language.French | Language.German;
```

Be aware that broader language sets may

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}