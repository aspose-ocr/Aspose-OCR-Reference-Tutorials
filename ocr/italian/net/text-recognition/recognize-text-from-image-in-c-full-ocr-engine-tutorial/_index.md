---
category: general
date: 2026-06-06
description: Riconosci il testo da un'immagine usando il motore OCR C#. Impara a convertire
  l'immagine in JSON, a convertire l'immagine in XML e a caricare l'immagine per l'OCR
  in pochi minuti.
draft: false
keywords:
- recognize text from image
- convert image to json
- convert image to xml
- ocr engine c#
- load image for ocr
language: it
og_description: Riconosci il testo da un'immagine con il motore OCR C#. Esporta i
  risultati in JSON e XML e gestisci il caricamento delle immagini per l'OCR.
og_title: Riconosci il testo da un'immagine in C# – Tutorial completo del motore OCR
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Recognize text from image using C# OCR engine. Learn to convert image
    to JSON, convert image to XML, and load image for OCR in minutes.
  headline: Recognize Text from Image in C# – Full OCR Engine Tutorial
  type: TechArticle
tags:
- OCR
- C#
- Image Processing
title: Riconosci il testo da un'immagine in C# – Tutorial completo sul motore OCR
url: /it/net/text-recognition/recognize-text-from-image-in-c-full-ocr-engine-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Riconoscere il testo da un'immagine in C# – Tutorial completo del motore OCR

Ti è mai capitato di dover **riconoscere il testo da un'immagine** senza sapere quale libreria C# scegliere? Non sei l'unico: gli sviluppatori lottano continuamente per trasformare ricevute scannerizzate, screenshot o appunti scritti a mano in testo ricercabile. La buona notizia? Con un moderno **OCR engine C#** puoi farlo in poche righe, e poi **convertire l'immagine in JSON** o **convertire l'immagine in XML** per l'elaborazione successiva.

In questa guida percorreremo ogni passaggio: installare il pacchetto OCR, caricare un'immagine per l'OCR, estrarre il testo e infine esportare i risultati sia in JSON che in XML. Alla fine avrai un'app console autonoma che potrai inserire in qualsiasi progetto .NET. Niente riferimenti vaghi, solo una soluzione completa e funzionante.

## Cosa imparerai

- Una chiara panoramica su come **caricare un'immagine per OCR** usando un popolare motore OCR C#.  
- Codice funzionante che **riconosce il testo da un'immagine** e restituisce un ricco oggetto risultato.  
- Snippet semplici che **convertiscono l'immagine in JSON** e **convertiscono l'immagine in XML** senza librerie aggiuntive.  
- Suggerimenti per gestire PDF multi‑pagina, diversi formati immagine e problemi comuni come scansioni a basso contrasto.

### Prerequisiti

- .NET 6 SDK o successivo (puoi anche mirare a .NET Framework 4.8 se preferisci).  
- Conoscenza di base di C#—nulla di complesso, solo una comprensione di classi e `async`/`await`.  
- Un file immagine (`structured.png` negli esempi) che desideri sottoporre a OCR.  

Se hai tutto questo, immergiamoci.

---

## Riconoscere il testo da un'immagine – Configurare il motore OCR

Prima di tutto. Abbiamo bisogno di una libreria OCR affidabile. Per questo tutorial useremo **IronOcr**, un motore di livello commerciale che offre un'edizione community gratuita su NuGet. Supporta l'inglese subito pronto all'uso e ci fornisce la classe `OcrEngine` mostrata nello snippet originale.

```bash
dotnet add package IronOcr --version 2024.3.0
```

> **Pro tip:** Se il budget è più ristretto, sostituisci `IronOcr` con `Tesseract`—l'API è leggermente diversa ma i concetti rimangono identici.

Ora crea un nuovo progetto console e aggiungi le dichiarazioni `using` richieste:

```csharp
using IronOcr;
using System.IO;
```

### Configurazione passo‑passo del motore

```csharp
// Step 1: Create and configure the OCR engine
var ocrEngine = new IronTesseract();           // IronOcr’s engine class
ocrEngine.Language = OcrLanguage.English;     // Load English language data
```

*Perché è importante:* Inizializzare il motore una sola volta e riutilizzarlo per molte immagini riduce l'overhead. Inoltre, impostare esplicitamente la lingua evita la routine di auto‑rilevamento del motore, che può essere più lenta e meno accurata.

---

## Caricare un'immagine per OCR – Fornire al motore i dati corretti

Il motore si aspetta un oggetto `OcrInput`. Puoi puntarlo a un percorso file, a uno stream o anche a un `Bitmap`. Ecco l'approccio più semplice:

```csharp
// Step 2: Load the image to be processed
var input = new OcrInput(@"YOUR_DIRECTORY\structured.png");

// Optional: improve accuracy on low‑contrast images
input.Deskew();          // Straighten tilted pages
input.Contrast(10);      // Boost contrast by 10%
```

> **Caso limite:** Se la tua sorgente è un PDF multi‑pagina, chiama `input.AddPdf("file.pdf")` invece di un PNG. Il motore OCR tratterà ogni pagina come un'immagine separata automaticamente.

---

## Riconoscere il testo da un'immagine – Eseguire il processo OCR

Con il motore e l'input pronti, il riconoscimento vero e proprio è una singola riga:

```csharp
// Step 3: Recognize text in the image
using var result = ocrEngine.Read(input);
```

`result` è un oggetto `OcrResult` che contiene:

- `Text` – stringa grezza estratta.  
- `Lines` – collezione di oggetti `OcrLine` con punteggi di confidenza.  
- `Words` – collezione di parole individuali, anch'esse con confidenza.  

Puoi ispezionarlo direttamente nel debugger, ma la maggior parte delle volte vorrai serializzare i dati.

---

## Convertire l'immagine in JSON – Esportare i risultati OCR

IronOcr include la serializzazione JSON integrata tramite `System.Text.Json`. Lo snippet seguente scrive un file JSON ordinato accanto all'immagine sorgente:

```csharp
// Step 4: Export the recognition result to JSON and save it
string jsonResult = System.Text.Json.JsonSerializer.Serialize(result, new System.Text.Json.JsonSerializerOptions
{
    WriteIndented = true
});
File.WriteAllText(@"YOUR_DIRECTORY\result.json", jsonResult);
```

**Ciò che vedrai:** un documento JSON ben formattato contenente il testo grezzo, i punteggi di confidenza e le bounding box per ogni riga e parola. Questa struttura è perfetta per alimentare servizi downstream come ElasticSearch o Azure Cognitive Search.

---

## Convertire l'immagine in XML – Output dati strutturato

Alcuni sistemi legacy richiedono ancora XML. Il metodo `ToXml()` di IronOcr fornisce una conversione rapida:

```csharp
// Step 5: Export the recognition result to XML and save it
string xmlResult = result.ToXml();
File.WriteAllText(@"YOUR_DIRECTORY\result.xml", xmlResult);
```

L'XML rispecchia la gerarchia JSON, con elementi `<Line>` e `<Word>` che includono l'attributo `Confidence`. Se ti serve uno schema personalizzato, puoi proiettare manualmente `result` in un `XDocument`—l'API è completamente compatibile con LINQ.

---

## Codice di esempio completo end‑to‑end

Mettiamo tutto insieme, ecco un `Program.cs` pronto da eseguire:

```csharp
using IronOcr;
using System;
using System.IO;
using System.Text.Json;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure the OCR engine
        var ocrEngine = new IronTesseract();
        ocrEngine.Language = OcrLanguage.English;

        // 2️⃣ Load the image (adjust the path to your file)
        var input = new OcrInput(@"YOUR_DIRECTORY\structured.png");
        input.Deskew();
        input.Contrast(10);

        // 3️⃣ Perform recognition
        using var result = ocrEngine.Read(input);
        Console.WriteLine("✅ OCR completed. Extracted text:");
        Console.WriteLine(result.Text);

        // 4️⃣ Convert image to JSON
        string json = JsonSerializer.Serialize(result, new JsonSerializerOptions { WriteIndented = true });
        string jsonPath = @"YOUR_DIRECTORY\result.json";
        File.WriteAllText(jsonPath, json);
        Console.WriteLine($"📄 JSON saved to {jsonPath}");

        // 5️⃣ Convert image to XML
        string xml = result.ToXml();
        string xmlPath = @"YOUR_DIRECTORY\result.xml";
        File.WriteAllText(xmlPath, xml);
        Console.WriteLine($"📄 XML saved to {xmlPath}");
    }
}
```

**Output previsto** (troncato per brevità):

```
✅ OCR completed. Extracted text:
Invoice #12345
Date: 2024‑04‑01
Total: $1,234.56
...
📄 JSON saved to YOUR_DIRECTORY\result.json
📄 XML saved to YOUR_DIRECTORY\result.xml
```

Esegui il programma con `dotnet run`. Se tutto è collegato correttamente, vedrai il dump sulla console e due file appariranno in `YOUR_DIRECTORY`.

---

## Domande frequenti & Trucchi

| Domanda | Risposta |
|----------|--------|
| *E se l'immagine è un JPEG con rotazione EXIF?* | Usa `input.AutoRotate()` prima di `Deskew()`. IronOcr leggerà il tag EXIF e correggerà l'orientamento. |
| *Posso fare OCR su una cartella di immagini in un solo passaggio?* | Assolutamente. Avvolgi la logica sopra in un ciclo `foreach (var file in Directory.GetFiles(folder, "*.png"))`. |
| *Come migliorare l'accuratezza su scansioni rumorose?* | Incrementa `input.Denoise()` e considera `input.BlackWhiteThreshold(120)`. Inoltre, fornisci un language pack che corrisponda alla lingua del documento. |
| *Il formato JSON è compatibile con altre librerie OCR?* | Lo schema è sufficientemente generico—`Text`, `Lines`, `Words`—così puoi mappare l'output a quello di Tesseract con una minima trasformazione. |

---

## Suggerimenti sulle prestazioni (Livello Pro)

- **Riutilizza il motore**: istanziare `IronTesseract` all'interno di un ciclo stretto può ridurre il throughput fino al 30 %. Mantieni un singleton per dominio dell'applicazione.  
- **Parallelizza I/O**: se elabori decine di immagini, leggile in memoria in modo concorrente (`Task.WhenAll`) e passa ogni `OcrInput` allo stesso motore—IronOcr è thread‑safe.  
- **Esportazione batch**: invece di scrivere ogni file JSON/XML singolarmente, aggrega i risultati in una singola collezione e serializza una volta sola. Questo riduce l'usura del disco.

---

## Prossimi passi & Argomenti correlati

Ora che puoi **riconoscere il testo da un'immagine**, considera di estendere la pipeline:

- **Integrazione ricerca** – invia il JSON a Elasticsearch per la ricerca full‑text.  
- **Classificazione documenti** – alimenta l'output OCR a un modello ML leggero per auto‑taggare fatture, contratti o ricevute.  
- **Testo scritto a mano** – passa al language pack `OcrLanguage.EnglishHandwritten` (disponibile nella versione premium di IronOcr).  

Ognuno di questi si basa sulla base che hai appena costruito e ti terrà occupato per settimane.

---

## Conclusione

Abbiamo appena coperto come **riconoscere il testo da un'immagine** usando un moderno **OCR engine C#**, poi **convertire l'immagine in JSON** e **convertire l'immagine in XML**, e infine come **caricare un'immagine per OCR** in modo robusto. L'esempio completo gira in meno di un minuto, e i file esportati sono pronti per qualsiasi sistema downstream.

Prova il codice, personalizzalo,

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come usare Aspose OCR per ottenere risultati JSON nel riconoscimento delle immagini](/ocr/english/net/text-recognition/get-result-as-json/)
- [Estrarre il testo da un'immagine in C# con selezione della lingua usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Convertire immagine in testo – Eseguire OCR su un'immagine da URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}