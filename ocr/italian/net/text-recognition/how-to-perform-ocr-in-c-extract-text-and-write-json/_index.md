---
category: general
date: 2026-02-09
description: Impara a eseguire l'OCR in C# per estrarre il testo da un'immagine, riconoscere
  il testo da PNG e scrivere rapidamente un file JSON in C#.
draft: false
keywords:
- how to perform OCR
- extract text from image
- recognize text from png
- write json file c#
language: it
og_description: Come eseguire l'OCR in C#? Segui questa guida passo‑passo per estrarre
  il testo da un'immagine, riconoscere il testo da PNG e scrivere un file JSON in
  C# in modo efficiente.
og_title: Come eseguire OCR in C# – Estrarre testo e scrivere JSON
tags:
- OCR
- C#
- Aspose
- JSON
title: Come eseguire OCR in C# – Estrarre testo e scrivere JSON
url: /it/net/text-recognition/how-to-perform-ocr-in-c-extract-text-and-write-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR in C# – Guida completa

Eseguire OCR in C# è un ostacolo comune quando è necessario **estrarre testo da immagine**. In questa guida vedremo come riconoscere il testo da PNG, esportare il risultato dettagliato in una stringa JSON e infine **scrivere file JSON C#**. Hai mai fissato un modulo scansionato e ti sei chiesto come trasformare quei segni in testo ricercabile? Non sei solo; molti sviluppatori incontrano questo problema all'inizio.

Utilizzeremo la libreria Aspose.OCR perché fornisce la confidenza per simbolo subito pronto all'uso e si integra bene con i progetti .NET 6+. Alla fine di questo tutorial avrai un'app console pronta all'uso che carica un PNG, estrae ogni carattere e salva un file JSON ordinato che puoi inserire in un database o in un modello AI. Nessun trucco misterioso “vedi la documentazione”—solo una soluzione autonoma.

## Di cosa avrai bisogno

- **.NET 6 SDK** (o successivo) – l'attuale versione LTS al momento della scrittura.
- **Aspose.OCR per .NET** pacchetto NuGet – `Install-Package Aspose.OCR`.
- Un'immagine PNG che desideri scansionare (ad es., `form.png`).  
- Un IDE o editor – Visual Studio, VS Code, Rider – quello con cui ti trovi più a tuo agio.

È tutto. Se hai questi componenti, sei pronto per partire.

![Esempio di come eseguire OCR](ocr-example.png "Come eseguire OCR in C#")

*Testo alternativo dell'immagine: illustrazione di come eseguire OCR che mostra un'app console C# che elabora un PNG.*

## Passo 1: Configurare il progetto e aggiungere le dipendenze

Per prima cosa, crea un nuovo progetto console e aggiungi la libreria Aspose OCR.

```csharp
// Create a new console app (run in terminal)
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo

// Add Aspose.OCR NuGet package
dotnet add package Aspose.OCR
```

> **Consiglio:** Usa il flag `--framework net6.0` se vuoi fissare esplicitamente il framework di destinazione.

Perché questo passo è importante: il pacchetto NuGet contiene le classi `OcrEngine`, `ImageStream` e `JsonExporter` di cui faremo affidamento. Senza di esse, il compilatore non avrà idea di cosa significhi “OCR”.

## Passo 2: Scrivere la logica OCR principale

Apri `Program.cs` (o crea un nuovo file) e sostituisci il suo contenuto con il seguente. Ogni sezione è commentata così puoi vedere perché è presente.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Export;
using System;

namespace OcrJsonDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Initialize the OCR engine – this prepares the
            //    internal models and allocates native resources.
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // 2️⃣ Load the image you want to process.
            //    Replace the path with your own PNG file.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/form.png";
            ImageStream image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // 3️⃣ Perform OCR recognition – the heavy lifting.
            //    The result includes text, per‑symbol confidence,
            //    and layout information.
            // -------------------------------------------------
            RecognitionResult ocrResult = ocrEngine.Recognize(image);

            // -------------------------------------------------
            // 4️⃣ Export the result to a JSON string.
            //    JsonExporter respects the confidence values.
            // -------------------------------------------------
            JsonExporter jsonExporter = new JsonExporter();
            string jsonContent = jsonExporter.ExportToString(ocrResult);

            // -------------------------------------------------
            // 5️⃣ Write the JSON to disk – this is how we
            //    **write JSON file C#** style.
            // -------------------------------------------------
            string jsonPath = @"YOUR_DIRECTORY/form.json";
            System.IO.File.WriteAllText(jsonPath, jsonContent);

            // -------------------------------------------------
            // 6️⃣ Let the user know we succeeded.
            // -------------------------------------------------
            Console.WriteLine($"JSON file saved successfully at {jsonPath}");
        }
    }
}
```

### Perché ogni parte è importante

- **OcrEngine**: Consideralo il cervello dell'operazione. Carica i modelli linguistici e imposta la pipeline di inferenza.
- **ImageStream.FromFile**: Gestisce qualsiasi PNG, JPEG, BMP, ecc. Astrae le particolarità di I/O dei file.
- **RecognitionResult**: Contiene il testo grezzo più i punteggi di confidenza. Qui ottieni i dati granulari necessari per la validazione a valle.
- **JsonExporter**: Converte il ricco `RecognitionResult` in un payload JSON pulito, perfetto per le API.
- **File.WriteAllText**: Il modo diretto .NET per **scrivere file JSON C#** senza dipendenze aggiuntive.

## Passo 3: Eseguire l'applicazione e verificare l'output

Compila ed esegui il programma:

```bash
dotnet run
```

Dovresti vedere un messaggio console simile a:

```
JSON file saved successfully at YOUR_DIRECTORY/form.json
```

Apri `form.json` – troverai qualcosa del genere:

```json
{
  "Text": "Sample Form\nName: John Doe\nDate: 2026-02-09",
  "Symbols": [
    { "Char": "S", "Confidence": 0.99, "X": 12, "Y": 8 },
    { "Char": "a", "Confidence": 0.98, "X": 22, "Y": 8 },
    // … more symbols …
  ]
}
```

Il passo **estrarre testo da immagine** è riuscito, e ora hai una rappresentazione JSON leggibile da macchine di ogni carattere.

## Passo 4: Gestire i casi limite comuni

### File mancanti o corrotti

Se il percorso PNG è errato, `ImageStream.FromFile` lancia una `FileNotFoundException`. Avvolgi il codice di caricamento in un blocco try‑catch:

```csharp
try
{
    ImageStream image = ImageStream.FromFile(imagePath);
}
catch (FileNotFoundException ex)
{
    Console.Error.WriteLine($"Could not find image: {ex.Message}");
    return;
}
```

### Punteggi di bassa confidenza

A volte l'OCR restituisce bassa confidenza per scansioni rumorose. Puoi filtrare i simboli prima dell'esportazione:

```csharp
ocrResult.Symbols.RemoveAll(s => s.Confidence < 0.6);
```

Ciò garantisce che il JSON contenga solo caratteri ragionevolmente affidabili—utile quando inserisci i dati in pipeline di validazione a valle.

### File di grandi dimensioni e memoria

Elaborare un PNG di diversi megabyte può aumentare l'uso della memoria. Considera lo streaming dell'immagine a blocchi o l'uso di `OcrEngine.RecognizeAsync` (disponibile nelle versioni più recenti di Aspose) per mantenere l'interfaccia reattiva.

## Passo 5: Estendere la soluzione (Opzionale)

- **Elaborazione batch**: Scorri una directory di PNG e genera un JSON corrispondente per ogni file.
- **Archiviazione su database**: Inserisci il JSON in una colonna SQL `NVARCHAR(MAX)` per analisi successive.
- **Selezione della lingua**: Imposta `ocrEngine.Language = OcrLanguage.Spanish;` se ti serve supporto non‑inglese.

Tutte queste estensioni seguono lo stesso modello **come eseguire OCR** che abbiamo stabilito—inizializzare, riconoscere, esportare e persistere.

## Domande frequenti

**D: Funziona con JPG o TIFF?**  
R: Assolutamente. `ImageStream.FromFile` rileva automaticamente il formato, quindi puoi sostituire il PNG con qualsiasi immagine raster supportata.

**D: E se devo estrarre testo da un PDF?**  
R: Converti prima ogni pagina PDF in un'immagine (ad es., usando `Aspose.PDF`) e poi fornisci il PNG al flusso OCR descritto qui.

**D: Posso ottenere il risultato OCR come XML invece di JSON?**  
R: Sì. Aspose.OCR fornisce anche un `XmlExporter`. Sostituisci `JsonExporter` con `XmlExporter` e adegua l'estensione del file.

## Conclusione

Abbiamo percorso **come eseguire OCR** in C# dall'inizio alla fine, mostrandoti come **estrarre testo da immagine**, **riconoscere testo da PNG** e **scrivere file JSON C#** senza intoppi. L'esempio completo e eseguibile si trova nei frammenti di codice sopra, e ora comprendi il perché di ogni passo—inizializzare il motore, gestire i casi limite e persistere i risultati.

Successivamente, potresti esplorare pipeline OCR batch, integrare l'output JSON con Azure Cognitive Search, o sperimentare modelli linguistici personalizzati. Il cielo è il limite una volta che hai padroneggiato le basi dell'OCR in C#.

Se hai incontrato problemi o hai idee per ulteriori estensioni, lascia un commento qui sotto. Buona programmazione e divertiti a trasformare quelle scansioni pixelate in dati puliti e ricercabili!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}