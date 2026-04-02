---
category: general
date: 2026-04-01
description: Come convertire l'output OCR in JSON e XML in C# – impara a estrarre
  il testo da un'immagine e a scrivere un file JSON in C# usando Aspose.OCR.
draft: false
keywords:
- how to convert ocr
- extract text from image
- write json file c#
- write xml file c#
- how to extract text
language: it
og_description: Come convertire i risultati OCR in file JSON e XML strutturati con
  C#. Guida passo passo per estrarre il testo da un'immagine e scrivere un file JSON
  in C#.
og_title: Come convertire OCR in JSON e XML in C# – Scrivi file JSON
tags:
- OCR
- C#
- Aspose
title: Come convertire OCR in JSON e XML in C# – Scrivere file JSON
url: /it/net/text-recognition/how-to-convert-ocr-to-json-xml-in-c-write-json-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come Convertire OCR in JSON & XML in C# – Scrivere File JSON

**Come convertire OCR** i risultati in qualcosa di realmente utilizzabile è una domanda che molti sviluppatori si pongono. In questa guida ti mostreremo come estrarre testo da un’immagine, trasformare l’output OCR in JSON e XML ben formattati e poi scrivere quei file su disco con C#.

Se ti sei mai trovato a fissare una stringa OCR grezza pensando “Deve esserci un modo migliore per memorizzarla”, sei nel posto giusto. Alla fine avrai un programma completo, eseguibile, che non solo **estrae testo da image** file ma sa anche come **write JSON file C#** e **write XML file C#** senza alcuno sforzo.

## Cosa Ti Serve

- **.NET 6.0** o versioni successive (il codice funziona anche con .NET Framework 4.6+).  
- Pacchetto NuGet **Aspose.OCR** – installalo con `dotnet add package Aspose.OCR`.  
- Un’immagine contenente testo (ad es., `invoice.png`).  
- Qualsiasi IDE ti piaccia – Visual Studio, Rider o VS Code vanno bene.

> **Pro tip:** Tieni i file immagine in una cartella dedicata (ad es., `Resources/`) così i percorsi rimangono ordinati.

## Step 1: Configurare il Motore OCR – How to Convert OCR

Per prima cosa, creiamo un’istanza di `OcrEngine` e indichiamo quale lingua cercare. Nella maggior parte dei casi l’inglese è sufficiente, ma puoi sostituire `Language.English` con qualsiasi lingua supportata.

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine for English text
        var ocrEngine = new OcrEngine { Language = Language.English };
```

> **Why this matters:** Inizializzare il motore con la lingua corretta migliora drasticamente la precisione, specialmente per script non latini.

## Step 2: Riconoscere il Testo – Extract Text from Image

Ora forniamo l’immagine al motore. Il metodo `Recognize` restituisce un oggetto `OcrResult` che contiene il testo grezzo e i dati di posizione.

```csharp
        // Step 2: Recognise text from the supplied image
        // Replace "YOUR_DIRECTORY/invoice.png" with your actual file path
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");
```

Se l’immagine non viene trovata, `Recognize` lancia una `FileNotFoundException`. Per mantenere la demo semplice assumiamo che il percorso sia corretto, ma in produzione dovresti avvolgere il tutto in un blocco try‑catch.

## Step 3: Convertire il Risultato in JSON – Write JSON File C#

Aspose.OCR rende la serializzazione un gioco da ragazzi. Il metodo `ToJson` accetta un flag `indent` per produrre un output formattato, perfetto quando prevedi di aprire il file in un editor di testo.

```csharp
        // Step 3: Convert OCR result to formatted JSON
        string jsonOutput = ocrResult.ToJson(indent: true);
```

### Expected JSON Sample

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑31\nTotal: $250.00",
  "Regions": [
    {
      "Bounds": { "X": 10, "Y": 20, "Width": 200, "Height": 30 },
      "Text": "Invoice #12345"
    }
    // … more regions …
  ]
}
```

> **How to extract text**: La proprietà `Text` ti fornisce la stringa semplice che puoi inviare ad altri servizi (indici di ricerca, database, ecc.).

## Step 4: Persistire il JSON – Write JSON File C# (Continued)

Con la stringa JSON pronta, la scriviamo semplicemente su file usando `File.WriteAllText`. Questo garantisce la codifica UTF‑8 per impostazione predefinita.

```csharp
        // Step 4: Save JSON to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);
```

Ora hai un `invoice.json` accanto alla tua immagine, pronto per l’elaborazione successiva.

## Step 5: Convertire il Risultato in XML – Write XML File C#

Se preferisci XML per sistemi legacy, il metodo `ToXml` fa il lavoro pesante. Come `ToJson`, supporta anche la stampa formattata.

```csharp
        // Step 5: Convert OCR result to formatted XML
        string xmlOutput = ocrResult.ToXml(indent: true);
```

### Expected XML Sample

```xml
<OcrResult>
  <Text>Invoice #12345
Date: 2024-03-31
Total: $250.00</Text>
  <Regions>
    <Region>
      <Bounds X="10" Y="20" Width="200" Height="30" />
      <Text>Invoice #12345</Text>
    </Region>
    <!-- … more regions … -->
  </Regions>
</OcrResult>
```

## Step 6: Persistire l’XML – Write XML File C# (Continued)

Salvare l’XML è identico al passaggio JSON; basta puntare a un’estensione `.xml`.

```csharp
        // Step 6: Save XML to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

### Full Working Example

Mettendo tutto insieme, ecco il programma completo che puoi copiare‑incollare in una console app:

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Initialise OCR engine for English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Recognise text from image
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");

        // Convert to JSON and save
        string jsonOutput = ocrResult.ToJson(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);

        // Convert to XML and save
        string xmlOutput = ocrResult.ToXml(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

Esegui il programma e troverai due nuovi file—`invoice.json` e `invoice.xml`—esattamente dove li hai indicati. Aprili per verificare che la struttura corrisponda ai campioni sopra.

## Common Questions & Edge Cases

| Question | Answer |
|----------|--------|
| **What if the image contains multiple languages?** | Create separate `OcrEngine` instances for each language or use `Language.Multi` if supported. |
| **Can I control the output format (e.g., exclude region data)?** | Yes. Both `ToJson` and `ToXml` accept optional parameters to filter fields; check the Aspose.OCR docs for `ExportOptions`. |
| **How do I handle large PDFs with many pages?** | Process each page individually, aggregate the results, then serialize once. |
| **Is the output UTF‑8 safe?** | Absolutely—Aspose.OCR uses Unicode internally, and `File.WriteAllText` writes UTF‑8 by default. |
| **What about performance?** | OCR is CPU‑intensive. For batch jobs consider parallelising across cores or using Aspose’s cloud API. |

## Conclusion

Ora sai **come convertire OCR** i risultati sia in JSON che in XML usando C#. Seguendo i passaggi sopra potrai **extract text from image**, poi **write JSON file C#** e **write XML file C#** con poche righe di codice. Questo approccio è veloce, affidabile e funziona con qualsiasi tipo di immagine supportata da Aspose.OCR.

Pronto per la prossima sfida? Prova a fornire il

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}