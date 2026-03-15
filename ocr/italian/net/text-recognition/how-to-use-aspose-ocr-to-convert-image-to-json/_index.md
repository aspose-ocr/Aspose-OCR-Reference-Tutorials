---
category: general
date: 2026-03-15
description: Come utilizzare Aspose OCR per estrarre testo dalle immagini e convertire
  l'immagine in JSON in C#. Impara a riconoscere il testo da PNG e ottenere rapidamente
  un output strutturato.
draft: false
keywords:
- how to use aspose
- convert image to json
- extract text from image
- recognize text from png
- how to extract ocr
language: it
og_description: Come utilizzare Aspose OCR per estrarre testo dalle immagini e convertire
  l'immagine in JSON in C#. Questa guida ti accompagna nel riconoscere il testo da
  PNG e ottenere un output strutturato.
og_title: Come usare Aspose OCR per convertire un'immagine in JSON
tags:
- Aspose
- OCR
- C#
- JSON
title: Come usare Aspose OCR per convertire un'immagine in JSON
url: /it/net/text-recognition/how-to-use-aspose-ocr-to-convert-image-to-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come utilizzare Aspose OCR per convertire un'immagine in JSON

Come utilizzare Aspose OCR è una domanda comune quando gli sviluppatori devono estrarre testo dalle immagini. Se stai cercando di **convertire immagine in JSON** o **riconoscere testo da PNG**, questa guida ti copre—senza fronzoli, solo una soluzione pratica, end‑to‑end.

Nei prossimi minuti passeremo in rassegna tutto ciò di cui hai bisogno: installare la libreria, configurare il motore per l'output JSON, caricare un PNG di ricevuta, eseguire l'OCR e infine scrivere il risultato in un file `.json`. Alla fine sarai in grado di **estrarre testo da immagine** con una singola chiamata di metodo, e comprenderai perché ogni passaggio è importante.

> **Suggerimento professionale:** Aspose OCR funziona con un'ampia gamma di formati immagine (PNG, JPEG, BMP, TIFF). Lo stesso codice qui sotto li gestirà tutti, così non dovrai scrivere logica specifica per formato.

## Di cosa avrai bisogno

- .NET 6.0 o successivo (il codice funziona anche su .NET Framework 4.6+)  
- Un pacchetto NuGet Aspose.OCR valido (versione di prova gratuita o con licenza)  
- Un file immagine da elaborare (ad es., `receipt.png`)  
- Visual Studio, VS Code, o qualsiasi editor C# tu preferisca  

È tutto—nessuna dipendenza aggiuntiva, nessun servizio esterno. Pronto? Immergiamoci.

![come utilizzare il motore OCR di aspose](image-placeholder.png "come utilizzare il motore OCR di aspose")

## Come utilizzare Aspose OCR – Configurare l'output JSON

La prima cosa da fare quando **come utilizzare aspose** per OCR è creare un'istanza `OcrEngine` e indicarle di emettere JSON. Questo piccolo switch di configurazione ti salva dal dover serializzare manualmente il risultato in seguito.

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine – this is the core object that does the heavy lifting.
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Tell Aspose to give us JSON instead of plain text.
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Load the image you want to recognize.
        var inputImage = Image.FromFile(@"YOUR_DIRECTORY/receipt.png");

        // 4️⃣ Run the OCR process.
        var ocrResult = ocrEngine.Recognize(inputImage);

        // 5️⃣ Save the JSON payload to disk.
        File.WriteAllText(@"YOUR_DIRECTORY/receipt.json", ocrResult.Text);

        // 6️⃣ Let the developer know we’re done.
        Console.WriteLine("JSON saved.");
    }
}
```

**Perché è importante:** Impostare `OutputFormat` su `Json` significa che il motore OCR struttura già il testo in una gerarchia di pagine, linee e parole. Non è necessario analizzare stringhe grezze in seguito, il che rende l'elaborazione a valle—come inserire dati in un database—molto più pulita.

## Convertire immagine in JSON con Aspose OCR

Ora che il motore è configurato, parliamo più in dettaglio della parte **convertire immagine in JSON**.

1. **Carica l'immagine** – `Image.FromFile` funziona per qualsiasi formato supportato. Se stai gestendo uno stream (ad es., un file caricato), puoi usare `Image.FromStream` al suo posto.  
2. **Esegui `Recognize`** – questo metodo restituisce un oggetto `OcrResult`. Poiché abbiamo impostato l'output su JSON, `ocrResult.Text` contiene già una stringa JSON.  
3. **Scrivi il file** – `File.WriteAllText` è il modo più semplice per persistere il JSON. Se devi memorizzarlo in un bucket cloud, basta sostituire questa riga con la chiamata SDK appropriata.

### Output JSON previsto

Un tipico payload JSON appare così (ridotto per brevità):

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Words": [
            { "Text": "Total", "Confidence": 0.99 },
            { "Text": "$12.34", "Confidence": 0.98 }
          ]
        }
      ]
    }
  ]
}
```

Ora puoi alimentare questa struttura in qualsiasi sistema a valle—che sia uno strumento di reporting, un modello di machine‑learning o un semplice file di log.

## Estrarre testo da immagine usando Aspose OCR

Se ti serve solo la stringa grezza (cioè, non ti interessa il JSON), basta cambiare il formato di output a testo semplice:

```csharp
ocrEngine.Configuration.OutputFormat = OutputFormat.PlainText;
var plainResult = ocrEngine.Recognize(inputImage);
Console.WriteLine(plainResult.Text);
```

**Quando scegliere il testo semplice?**  
- Debug rapido o output su console.  
- Scenari in cui applicherai post‑processing personalizzato (ad es., estrazione con regex).  

Ma ricorda, **estrarre testo da immagine** usando JSON ti fornisce dati posizionali—utili per evidenziare il testo in un'interfaccia UI o allinearlo con i campi di un modulo.

## Riconoscere testo da file PNG

PNG è un formato lossless, che spesso offre una migliore precisione OCR rispetto ai JPEG fortemente compressi. Ecco una rapida checklist per assicurarti di ottenere i migliori risultati quando **riconosci testo da PNG**:

| Voce della checklist | Perché aiuta |
|----------------------|--------------|
| Usa una DPI di 300+ | Una risoluzione più alta fornisce al motore più pixel con cui lavorare. |
| Mantieni l'immagine in scala di grigi | Riduce il rumore; Aspose OCR converte automaticamente, ma la pre‑elaborazione può velocizzare le cose. |
| Rimuovi il rumore di sfondo | Sfondi puliti migliorano i punteggi di confidenza. |

Se incontri punteggi di confidenza bassi, prova ad aumentare la DPI o applicare un semplice filtro di soglia prima di fornire l'immagine ad Aspose.

## Come estrarre i risultati OCR programmaticamente

Oltre a salvare il JSON, potresti voler leggere programmaticamente campi specifici—ad esempio, l'importo totale su una ricevuta. Poiché il JSON contiene una gerarchia, puoi deserializzarlo in un oggetto C#:

```csharp
using System.Text.Json;

// Assuming ocrResult.Text contains the JSON string
var ocrData = JsonSerializer.Deserialize<OcrResponse>(ocrResult.Text);

// Example class definitions (simplified)
public class OcrResponse
{
    public Page[] Pages { get; set; }
}
public class Page
{
    public int PageNumber { get; set; }
    public Line[] Lines { get; set; }
}
public class Line
{
    public Word[] Words { get; set; }
}
public class Word
{
    public string Text { get; set; }
    public double Confidence { get; set; }
}
```

Ora puoi interrogare `ocrData` con LINQ:

```csharp
var totalLine = ocrData.Pages
    .SelectMany(p => p.Lines)
    .FirstOrDefault(l => l.Words.Any(w => w.Text.Equals("Total", StringComparison.OrdinalIgnoreCase)));

if (totalLine != null)
{
    var amount = totalLine.Words
        .FirstOrDefault(w => w.Text.StartsWith("$"))
        ?.Text;
    Console.WriteLine($"Extracted amount: {amount}");
}
```

**Perché funziona:** Il JSON ti indica già dove si trova ogni parola nella pagina, così puoi localizzare in modo affidabile i campi anche se il layout cambia leggermente.

## Casi limite e problemi comuni

- **Risultato nullo:** Se `ocrEngine.Recognize` restituisce `null`, l'immagine potrebbe non essere supportata o corrotta. Assicurati sempre di gestirlo:

  ```csharp
  var ocrResult = ocrEngine.Recognize(inputImage);
  if (ocrResult == null) throw new InvalidOperationException("OCR failed – check the image path.");
  ```

- **File di grandi dimensioni:** Per immagini multi‑megabyte, considera lo streaming dell'immagine o il ridimensionamento prima dell'OCR per evitare un uso eccessivo della memoria.

- **Problemi di licenza:** La versione di prova aggiunge una filigrana all'output. Assicurati di caricare la licenza all'inizio del programma:

  ```csharp
  Aspose.OCR.License license = new Aspose.OCR.License();
  license.SetLicense("Aspose.OCR.lic");
  ```

- **Script non latini:** Aspose OCR supporta molte lingue, ma devi impostare la proprietà `Language` di conseguenza (ad es., `ocrEngine.Configuration.Language = Language.English;`).

## Esempio completo funzionante (pronto per copia‑incolla)

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // Load your Aspose license (optional for trial)
        // var license = new Aspose.OCR.License();
        // license.SetLicense("Aspose.OCR.lic");

        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Set output to JSON – this is the key step for convert image to JSON
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Optional: improve accuracy for PNG files
        ocrEngine.Configuration.Dpi = 300; // higher DPI = better results

        // 4️⃣ Load the image you want to process
        var inputImagePath = @"YOUR_DIRECTORY/receipt.png";
        if (!File.Exists(inputImagePath))
            throw new FileNotFoundException($"Image not found: {inputImagePath}");

        var inputImage = Image.FromFile(inputImagePath);

        // 5️⃣ Run OCR – this is where we actually extract text from image
        var ocrResult = ocrEngine.Recognize(inputImage);
        if (ocrResult == null)
            throw new InvalidOperationException("OCR

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}