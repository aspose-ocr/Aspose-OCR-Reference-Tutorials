---
category: general
date: 2026-03-07
description: Estrai il testo da file PNG usando C#. Scopri come convertire un'immagine
  in testo con C# e leggi rapidamente il testo dalle immagini scannerizzate.
draft: false
keywords:
- extract text from png
- convert image to text c#
- read text from scanned images
- how to run ocr on images
language: it
og_description: Estrai testo da file PNG usando C#. Questa guida mostra come convertire
  un'immagine in testo con C# e leggere il testo da immagini scannerizzate con Aspose
  OCR.
og_title: Estrai testo da PNG in C# – Guida completa OCR
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Estrai testo da PNG in C# – Guida completa all'OCR
url: /it/net/text-recognition/extract-text-from-png-in-c-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai testo da PNG in C# – Guida completa OCR

Hai mai dovuto **estrarre testo da PNG** ma non sapevi da dove cominciare? Non sei solo—la maggior parte degli sviluppatori si imbatte in questo ostacolo quando si trovano per la prima volta di fronte a grafiche scansionate o screenshot che devono diventare testo ricercabile. La buona notizia? Con poche righe di C# e Aspose OCR puoi trasformare qualsiasi PNG in stringhe modificabili in un attimo.

In questo tutorial percorreremo l'intero processo: dalla ricerca dei PNG sul disco, all'avvio di attività OCR in parallelo, fino alla visualizzazione di un'anteprima ordinata di ogni risultato. Alla fine saprai come **convert image to text C#**, sarai in grado di **read text from scanned images** in modo efficiente, e vedrai anche il modo migliore per **run OCR on images** senza sovraccaricare il thread UI.

## Cosa ti serve

- .NET 6.0 o successivo (il codice funziona anche su .NET Core e .NET Framework)  
- Pacchetto NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- Una cartella piena di file *.png* che desideri elaborare  
- Qualsiasi IDE ti piaccia (Visual Studio, VS Code, Rider…)

Non è necessaria alcuna configurazione aggiuntiva; la libreria include tutto il necessario per decodificare PNG, JPEG, TIFF, quello che vuoi.

## Passo 1: Individua tutti i file PNG – Inizia “Extract Text from PNG”

Per prima cosa dobbiamo trovare tutti i PNG su cui eseguire l'OCR. Usare `Directory.GetFiles` è veloce e affidabile.

```csharp
// Step 1: Find all PNG images in the input folder
string[] imageFiles = Directory.GetFiles("YOUR_DIRECTORY", "*.png");

// Quick sanity check – throw if nothing was found
if (imageFiles.Length == 0)
    throw new FileNotFoundException("No PNG files found in the specified folder.");
```

*Perché è importante:* Scansionare la directory una sola volta mantiene il resto della pipeline semplice, e il controllo iniziale evita una situazione silenziosa di “nessun output” difficile da debug in seguito.

## Passo 2: Avvia attività OCR in parallelo – Esegui efficientemente **run OCR on images**

Eseguire l'OCR in modo sequenziale va bene per una manciata di file, ma i progetti reali spesso gestiscono decine o centinaia. Avviando un `Task` per immagine manteniamo la CPU occupata mentre la libreria svolge il lavoro pesante.

```csharp
// Step 2: Prepare a list to hold OCR tasks (one per image)
var ocrTasks = new List<Task<string>>();

// Step 3: Launch a parallel task for each image
foreach (var filePath in imageFiles)
{
    ocrTasks.Add(Task.Run(() =>
    {
        // Load the image and run OCR
        var engine = new OcrEngine();
        engine.Image = ImageStream.FromFile(filePath);
        engine.Recognize();
        return engine.Text;          // This is the extracted string
    }));
}
```

*Consiglio:* `Task.Run` delega il lavoro al thread pool, il che significa che la tua UI (se ne hai una) rimane reattiva. Se sei su un server, lo stesso schema scala bene tra i core.

## Passo 3: Attendi tutte le attività – Raccogli i risultati

Ora attendiamo che ogni operazione OCR termini. `Task.WhenAll` restituisce un array che corrisponde all'ordine originale dei file, facilitando l'abbinamento dei risultati con i nomi dei file.

```csharp
// Step 4: Await all tasks and gather the recognized texts
string[] ocrResults = await Task.WhenAll(ocrTasks);
```

*Nota caso limite:* Se un'immagine genera un'eccezione (file corrotto, formato non supportato) l'intero `WhenAll` propagherà l'eccezione. Puoi avvolgere il `Task.Run` interno in un try/catch e restituire una stringa vuota o un messaggio diagnostico se ti serve tolleranza agli errori.

## Passo 4: Mostra un'anteprima – Verifica l'output di **convert image to text C#**

Un'anteprima rapida ti aiuta a confermare che l'OCR abbia funzionato prima di iniziare a salvare i dati altrove.

```csharp
// Step 5: Show a short preview of each result
for (int i = 0; i < ocrResults.Length; i++)
{
    string fileName = Path.GetFileName(imageFiles[i]);
    string preview = ocrResults[i].Length > 100
        ? ocrResults[i][..100] + "..."
        : ocrResults[i];
    Console.WriteLine($"{fileName}: {preview}");
}
```

Un tipico output della console appare così:

```
invoice-001.png: Invoice Number: 2025-07-14   Date: 07/14/2025   Total: $1,250.00...
receipt-202.png: Thank you for your purchase!   Order #12345   Amount: $89.99...
```

Se l'anteprima mostra spazzatura, ricontrolla la qualità dell'immagine o considera un pre‑processing (ad es., binarizzazione) – ma per la maggior parte dei PNG puliti Aspose OCR lo fa correttamente al primo tentativo.

## Opzionale: Salva i risultati in CSV – Un caso d'uso reale

La maggior parte dei progetti necessita del testo estratto in un formato strutturato. Di seguito trovi un piccolo helper che scrive il nome file e il testo OCR completo in un file CSV.

```csharp
string csvPath = Path.Combine("YOUR_DIRECTORY", "ocr-results.csv");
using var writer = new StreamWriter(csvPath);
writer.WriteLine("FileName,ExtractedText");

for (int i = 0; i < imageFiles.Length; i++)
{
    string escaped = ocrResults[i].Replace("\"", "\"\"");
    writer.WriteLine($"\"{Path.GetFileName(imageFiles[i])}\",\"{escaped}\"");
}
Console.WriteLine($"All results saved to {csvPath}");
```

Ora puoi importare il CSV in Excel, Power BI, o qualsiasi sistema a valle che si aspetta **read text from scanned images**.

## Domande frequenti

**Cosa succede se i miei PNG sono enormi (oltre 5 MB)?**  
Aspose OCR ridimensiona automaticamente le immagini grandi per mantenere un uso della memoria ragionevole, ma puoi ridimensionare manualmente con `engine.Image = ImageStream.FromFile(filePath).Resize(2000, 0);` per limitare la larghezza a 2000 px mantenendo le proporzioni.

**Posso eseguirlo su Linux?**  
Sì. Aspose OCR è cross‑platform; assicurati solo che le dipendenze native (`libgdiplus` su alcune distribuzioni) siano installate.

**La lingua OCR è impostata su inglese per impostazione predefinita?**  
Corretto. Se ti serve un'altra lingua, imposta `engine.Language = OcrLanguage.French;` (o qualsiasi enum supportato) prima di chiamare `Recognize()`.

**Come gestisco PDF protetti da password che contengono PNG?**  
Converti prima le pagine PDF in immagini (usando Aspose PDF o un'altra libreria), poi inserisci quei PNG nella stessa pipeline. Il principio di **how to run OCR on images** rimane invariato.

## Esempio completo funzionante (Async Main)

Di seguito trovi un programma autonomo che puoi copiare‑incollare in un progetto console. Include tutti i componenti sopra, più un piccolo helper per convalidare la cartella di input.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;
using System.Threading.Tasks;

class Program
{
    static async Task Main()
    {
        // -------------------------------------------------
        // 1️⃣ Locate PNGs – the heart of “extract text from png”
        // -------------------------------------------------
        const string folder = @"YOUR_DIRECTORY";   // <-- change this
        if (!Directory.Exists(folder))
        {
            Console.WriteLine($"Folder not found: {folder}");
            return;
        }

        string[] imageFiles = Directory.GetFiles(folder, "*.png");
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to do.");
            return;
        }

        // -------------------------------------------------
        // 2️⃣ Fire off OCR tasks – best way to “run OCR on images”
        // -------------------------------------------------
        var ocrTasks = new List<Task<string>>();
        foreach (var filePath in imageFiles)
        {
            ocrTasks.Add(Task.Run(() =>
            {
                var engine = new OcrEngine();
                engine.Image = ImageStream.FromFile(filePath);
                engine.Recognize();
                return engine.Text;
            }));
        }

        // -------------------------------------------------
        // 3️⃣ Await results
        // -------------------------------------------------
        string[] ocrResults = await Task.WhenAll(ocrTasks);

        // -------------------------------------------------
        // 4️⃣ Show previews
        // -------------------------------------------------
        for (int i = 0; i < ocrResults.Length; i++)
        {
            string fileName = Path.GetFileName(imageFiles[i]);
            string preview = ocrResults[i].Length > 100
                ? ocrResults[i][..100] + "..."
                : ocrResults[i];
            Console.WriteLine($"{fileName}: {preview}");
        }

        // -------------------------------------------------
        // 5️⃣ Optional: write CSV – perfect for “read text from scanned images”
        // -------------------------------------------------
        string csvPath = Path.Combine(folder, "ocr-results.csv");
        using var writer = new StreamWriter(csvPath);
        writer.WriteLine("FileName,ExtractedText");
        for (int i = 0; i < imageFiles.Length; i++)
        {
            string escaped = ocrResults[i].Replace("\"", "\"\"");
            writer.WriteLine($"\"{Path.GetFileName(imageFiles[i])}\",\"{escaped}\"");
        }

        Console.WriteLine($"✅ OCR complete – results saved to {csvPath}");
    }
}
```

**Output previsto** (esempio per due PNG):

```
invoice-001.png: Invoice Number: 2025-07-14   Date: 07/14/2025   Total: $1,250.00...
receipt-202.png: Thank you for your purchase!   Order #12345   Amount: $89.99...
✅ OCR complete – results saved to C:\MyImages\ocr-results.csv
```

## Conclusioni

Abbiamo appena coperto tutto ciò di cui hai bisogno per **extract text from PNG** usando C#. Dalla localizzazione dei file, all'avvio di lavori OCR in parallelo, all'anteprima delle stringhe, fino al salvataggio in CSV—questa guida ti fornisce un modello pronto per la produzione per scenari **convert image to text C#**.  

Se sei pronto per il passo successivo, prova a far passare JPEG o TIFF nella stessa pipeline, sperimenta con diverse lingue OCR, o collega i risultati a un indice di ricerca così potrai **read text from scanned images** istantaneamente.  

Hai domande su casi limite, ottimizzazione delle prestazioni o licenze? Lascia un commento o contatta la community di Aspose—buon coding!

![Extract text from PNG example](extract-text-png.png "Extract text from PNG using Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}