---
category: general
date: 2026-04-03
description: Riconoscere il testo da un'immagine usando Aspose OCR in C#. Impara a
  caricare l'immagine per l'OCR, estrarre il testo dall'immagine, scrivere un file
  JSON in C# ed eseguire l'OCR su PNG.
draft: false
keywords:
- recognize text from image
- write json file c#
- load image for ocr
- extract text from image
- perform ocr on png
language: it
og_description: Riconosci il testo da un'immagine con Aspose OCR in C#. Guida passo‑passo
  per caricare l'immagine per l'OCR, estrarre il testo dall'immagine, scrivere un
  file JSON in C# ed eseguire l'OCR su PNG.
og_title: Riconoscere il testo da un'immagine in C# – Tutorial completo di Aspose
  OCR
tags:
- OCR
- C#
- Aspose
title: Riconoscere il testo da un'immagine in C# – Guida completa a Aspose OCR
url: /it/net/text-recognition/recognize-text-from-image-in-c-full-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# riconoscere testo da immagine in C# – Tutorial completo Aspose OCR

Hai mai dovuto **riconoscere testo da immagine** ma non sapevi quale libreria scegliere? Forse hai una serie di ricevute scannerizzate, uno screenshot PNG o una nota scritta a mano che vuoi trasformare in dati ricercabili. La buona notizia: con Aspose.OCR puoi farlo in poche righe di codice C#, e otterrai anche un file JSON ordinato da utilizzare in altri sistemi.

In questo tutorial vedremo come caricare un’immagine per l’OCR, estrarre il testo dall’immagine, serializzare il risultato in un file JSON e, infine, gestire i file PNG senza alcuna difficoltà. Alla fine avrai un’app console pronta all’uso che **riconosce testo da immagine** e scrive l’output in *output.json*.

## Cosa ti serve

- .NET 6.0 o versioni successive (il codice funziona anche con .NET Framework)
- Pacchetto NuGet Aspose.OCR (`Install-Package Aspose.OCR`)
- Un PNG (o qualsiasi formato supportato) che desideri elaborare
- Visual Studio, VS Code o qualsiasi editor C# tu preferisca

Non sono necessarie librerie di terze parti aggiuntive—solo il motore Aspose OCR e il serializer integrato `System.Text.Json`.

## Passo 1: Riconoscere testo da immagine usando Aspose OCR

La prima cosa da fare è creare un’istanza di `OcrEngine`. Questo oggetto esegue il lavoro pesante dietro le quinte.

```csharp
using Aspose.OCR;
using System.Drawing;
using System.IO;
using System.Text.Json;

class JsonExportDemo
{
    static void Main()
    {
        // Initialize the OCR engine – this is where the magic starts.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image for OCR – replace the path with your own file.
        Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/input.png");

        // Perform OCR on the loaded image and get a structured result.
        OcrResult ocrResult = ocrEngine.RecognizeToResult(sourceImage);

        // Serialize the result into a nicely indented JSON string.
        string json = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true });

        // Write JSON file C# – this will create output.json next to your exe.
        File.WriteAllText(@"YOUR_DIRECTORY/output.json", json);
    }
}
```

**Perché è importante:** Istanziare `OcrEngine` una sola volta e riutilizzarlo è più efficiente rispetto a crearne uno nuovo per ogni file. La chiamata `RecognizeToResult` restituisce un oggetto `OcrResult` che contiene già il testo estratto, i punteggi di confidenza e le bounding box—perfetto per l’elaborazione successiva.

## Passo 2: Caricare l’immagine per l’OCR – gestione di formati diversi

Aspose OCR può leggere PNG, JPEG, BMP e molti altri formati. Se lavori con un PNG che contiene trasparenza, potresti volerlo appiattire prima per evitare spazi vuoti inattesi.

```csharp
// Optional: flatten PNG with transparency to a white background.
if (sourceImage.RawFormat.Equals(System.Drawing.Imaging.ImageFormat.Png))
{
    Bitmap flat = new Bitmap(sourceImage.Width, sourceImage.Height);
    using (Graphics g = Graphics.FromImage(flat))
    {
        g.Clear(Color.White);
        g.DrawImage(sourceImage, 0, 0);
    }
    sourceImage = flat;
}
```

**Consiglio professionale:** Verifica sempre che le dimensioni dell’immagine siano ragionevoli (ad esempio, larghezza > 50 px). Immagini molto piccole possono far sì che il motore OCR perda caratteri, generando punteggi di confidenza bassi.

## Passo 3: Scrivere file JSON in C# – rendere l’output consumabile

Il serializer `System.Text.Json` è veloce e integrato, ma puoi sostituirlo con `Newtonsoft.Json` se ti servono convertitori personalizzati. L’esempio sopra usa già `WriteIndented = true` così il file risultante è leggibile dall’uomo.

```csharp
// Expected output (truncated):
{
  "Text": "Hello World",
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Hello World",
          "Confidence": 0.98,
          "BoundingBox": { "X": 10, "Y": 20, "Width": 120, "Height": 30 }
        }
      ]
    }
  ]
}
```

Avere i dati OCR in JSON ti permette di importarli facilmente in database, inviarli via HTTP o alimentarli a pipeline di machine‑learning.

## Passo 4: Verificare il risultato – rapido controllo di sanità

Dopo che il programma è stato eseguito, apri `output.json` e cerca il campo `"Text"`. Se contiene la stringa attesa, hai **estratto testo da immagine** con successo. Se la confidenza è bassa, considera di pre‑elaborare l’immagine (ad esempio, aumentare il contrasto o applicare una soglia binaria).

```csharp
Console.WriteLine($"Extracted text: {ocrResult.Text}");
Console.WriteLine($"Overall confidence: {ocrResult.Confidence:P2}");
```

L’esecuzione della console stamperà qualcosa di simile a:

```
Extracted text: Hello World
Overall confidence: 98.00%
```

Questo è un chiaro segnale che l’OCR ha funzionato come previsto.

## Problemi comuni e casi limite

| Problema | Perché accade | Come risolvere |
|----------|----------------|----------------|
| **Output vuoto** | L’immagine è troppo scura o ha uno spazio colore non supportato | Converti in scala di grigi, aumenta la luminosità o appiattisci il PNG (vedi Passo 2) |
| **Caratteri spazzatura** | DPI basso (< 72) o rumore eccessivo | Ingrandisci l’immagine o applica un filtro di denoise prima di passare a `RecognizeToResult` |
| **File grandi causano pressione sulla memoria** | Caricare un PNG multi‑megapixel in un `Bitmap` consuma RAM | Elabora le immagini a blocchi o ridimensionale mantenendo la leggibilità |
| **Errore di serializzazione JSON** | `OcrResult` contiene riferimenti circolari (raro) | Usa `JsonSerializerOptions { ReferenceHandler = ReferenceHandler.IgnoreCycles }` |

## Bonus: Eseguire OCR su PNG in un ciclo batch

Se hai una cartella piena di file PNG, puoi estendere la demo per iterare su di essi:

```csharp
string[] pngFiles = Directory.GetFiles(@"YOUR_DIRECTORY", "*.png");
foreach (var file in pngFiles)
{
    Image img = Image.FromFile(file);
    OcrResult res = ocrEngine.RecognizeToResult(img);
    string outPath = Path.ChangeExtension(file, ".json");
    File.WriteAllText(outPath, JsonSerializer.Serialize(res, new JsonSerializerOptions { WriteIndented = true }));
    Console.WriteLine($"Processed {Path.GetFileName(file)} → {Path.GetFileName(outPath)}");
}
```

Ora il programma **esegue OCR su PNG** in massa, scrivendo un file JSON corrispondente per ogni immagine.

## Conclusione

Hai appena imparato come **riconoscere testo da immagine** in C# con Aspose OCR, **caricare immagine per OCR**, **estrarre testo da immagine** e **scrivere file JSON in C#** per memorizzare i risultati. L’esempio completo, eseguibile, copre i passaggi essenziali, spiega perché ogni elemento è importante e mostra anche come gestire le particolarità dei PNG.

Passi successivi? Prova a importare il JSON in un indice di ricerca, combinarlo con il rilevamento della lingua o integrarlo in un’API web che elabora upload in tempo reale. Potresti anche esplorare il supporto di Aspose per il riconoscimento della scrittura a mano se il tuo caso d’uso lo richiede.

Hai domande su casi limite o ottimizzazioni delle prestazioni? Lascia un commento qui sotto—buona programmazione! 

![recognize text from image demo](/images/ocr-demo.png "Diagram showing how Aspose OCR recognizes text from image")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}