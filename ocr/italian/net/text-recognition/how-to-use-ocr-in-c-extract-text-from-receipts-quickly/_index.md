---
category: general
date: 2026-03-05
description: come usare l'OCR in C# per estrarre testo dalle immagini di ricevute.
  Scopri come caricare un'immagine per l'OCR e riconoscere l'immagine della ricevuta
  in pochi minuti.
draft: false
keywords:
- how to use OCR
- extract text from receipt
- load image for OCR
- recognize receipt image
language: it
og_description: come utilizzare l'OCR in C# per estrarre il testo dalle ricevute.
  Segui questa guida passo passo per caricare un'immagine per l'OCR e riconoscere
  l'immagine della ricevuta in modo efficiente.
og_title: come usare OCR in C# – Estrarre rapidamente il testo delle ricevute
tags:
- OCR
- C#
- Aspose
- Receipt Processing
title: Come usare OCR in C# – Estrai rapidamente il testo dalle ricevute
url: /it/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-receipts-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# come usare OCR in C# – Estrarre il testo dalle ricevute rapidamente

Ti sei mai chiesto **come usare OCR** per estrarre dati direttamente da una foto di una ricevuta della spesa? Non sei l'unico. In molte app per piccole imprese, il collo di bottiglia è trasformare un PNG sfocato in testo strutturato con cui puoi effettivamente lavorare.  

La buona notizia? Con poche righe di C# e Aspose.OCR puoi **load image for OCR**, eseguire il motore e **recognize receipt image** in meno di un minuto. Di seguito vedrai un esempio completo, pronto‑all‑uso, più consigli per le parti più complicate che la maggior parte dei tutorial tralascia.

## Cosa copre questa guida

Passeremo in rassegna tutto ciò che devi sapere:

* Installare il pacchetto NuGet Aspose.OCR.  
* Configurare il motore OCR – il cuore di **how to use OCR** correttamente.  
* Caricare un file di ricevuta (questo è il passaggio **load image for OCR**).  
* Eseguire il processo di riconoscimento ed estrarre sia i dati di layout JSON che XML.  
* Gestire le difficoltà comuni come licenze mancanti o formati immagine non supportati.  

Alla fine avrai un programma autonomo che estrae il testo da qualsiasi ricevuta inserita in una cartella. Nessun servizio esterno, nessuna magia nascosta.

## Prerequisiti

* .NET 6 SDK o successivo (il codice si compila anche con .NET Core).  
* Un file di licenza Aspose.OCR valido (`Aspose.OCR.lic`). Puoi ottenere una prova gratuita da Aspose se non ne possiedi ancora uno.  
* Un'immagine di esempio di una ricevuta – `receipt.png` va bene, ma qualsiasi formato raster comune andrà bene.  

Se li hai già, ottimo – immergiamoci.

![how to use OCR example](https://example.com/ocr-receipt.png "how to use OCR example")

## Passo 1: Installare Aspose.OCR e creare un nuovo progetto

Prima di tutto: hai bisogno della libreria che esegue effettivamente il lavoro pesante. Apri un terminale nella cartella del tuo progetto e esegui:

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
dotnet add package Aspose.OCR
```

Quel comando genera un'app console e scarica l'ultimo pacchetto Aspose.OCR. Secondo la mia esperienza, mantenere il nome del progetto breve rende i percorsi generati più facili da leggere, soprattutto quando inizi a gestire più app demo.

## Passo 2: Inizializzare il motore OCR – il cuore di **how to use OCR**

Ora scriveremo il codice che risponde alla domanda “**how to use OCR** in C#”. Apri `Program.cs` e sostituisci il suo contenuto con lo snippet qui sotto. Nota i commenti – spiegano il *perché* dietro ogni riga, non solo il *cosa*.

```csharp
using System;
using System.IO;
using Aspose.OCR;          // Aspose OCR namespace
using Aspose.OCR.Image;   // For loading images

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Create and configure the OCR engine.
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // Why set a license? Without it the engine runs in evaluation mode,
        // which adds a watermark to the output and limits batch size.
        ocrEngine.SetLicense("Aspose.OCR.lic");

        // -------------------------------------------------
        // 2️⃣ Load the receipt image – this is the **load image for OCR** step.
        // -------------------------------------------------
        // Change the path to point at your own receipt file.
        string imagePath = Path.Combine(
            Environment.CurrentDirectory, "receipt.png");

        // The ImageStream class abstracts file I/O and supports many formats.
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // -------------------------------------------------
        // 3️⃣ Run the recognition process – this is where we **recognize receipt image**.
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize();

        // -------------------------------------------------
        // 4️⃣ Export the layout information as JSON.
        // -------------------------------------------------
        string jsonResult = ocrResult.ToJson();
        File.WriteAllText("receipt.json", jsonResult);
        Console.WriteLine("✅ JSON saved to receipt.json");

        // -------------------------------------------------
        // 5️⃣ Export the same layout information as XML.
        // -------------------------------------------------
        string xmlResult = ocrResult.ToXml();
        File.WriteAllText("receipt.xml", xmlResult);
        Console.WriteLine("✅ XML saved to receipt.xml");

        // -------------------------------------------------
        // 6️⃣ Quick preview – print the plain text to console.
        // -------------------------------------------------
        Console.WriteLine("\n--- Extracted Text ---");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Perché funziona

* **`OcrEngine`** è il punto di ingresso; contiene tutta la configurazione che potresti modificare in seguito (lingua, DPI, ecc.).  
* **`SetLicense`** rimuove il watermark di valutazione – un passaggio cruciale quando prevedi di distribuire il codice.  
* **`ImageStream.FromFile`** esegue il lavoro di **load image for OCR**, gestendo PNG, JPEG, BMP, TIFF e altro.  
* **`Recognize()`** è il metodo che effettivamente **recognize receipt image**. Internamente esegue binarizzazione, segmentazione e classificazione dei caratteri.  
* L'esportazione in JSON e XML ti fornisce sia un dump leggibile dall'uomo sia una struttura adatta alle macchine che puoi passare a parser successivi.

## Passo 3: Eseguire la demo e verificare l'output

Compila ed esegui:

```bash
dotnet run
```

Se tutto è collegato correttamente vedrai qualcosa di simile:

```
✅ JSON saved to receipt.json
✅ XML saved to receipt.xml

--- Extracted Text ---
Walmart Supercenter
Date: 03/04/2026
Item    Qty   Price
Milk    2     2.58
Bread   1     1.99
Total   4.57
```

La console stampa il testo semplice, mentre `receipt.json` e `receipt.xml` contengono informazioni dettagliate sul layout (coordinate, punteggi di confidenza, ecc.). Quei file sono utili se devi mappare ogni riga a un campo del database in seguito.

## Casi limite e consigli professionali

### 1️⃣ Licenza mancante o non valida

Se `SetLicense` fallisce, il motore passa alla modalità di prova e otterrai un watermark nell'output. Avvolgi la chiamata in un try/catch e registra un messaggio amichevole:

```csharp
try { ocrEngine.SetLicense("Aspose.OCR.lic"); }
catch (Exception ex)
{
    Console.WriteLine("⚠️ License not found – running in trial mode.");
    Console.WriteLine(ex.Message);
}
```

### 2️⃣ Formati immagine non supportati

Aspose.OCR supporta la maggior parte dei formati raster, ma se gli fornisci un PDF o un TIFF multi‑pagina dovrai prima convertire la pagina di interesse in un'immagine. La libreria `Aspose.PDF` può gestire quella conversione.

### 3️⃣ Ricevute grandi e prestazioni

Elaborare un'immagine da 10 MB può essere lento. Riduci la risoluzione prima di passarla al motore:

```csharp
ocrEngine.Image = ImageStream.FromFile(imagePath).Resize(1024, 0);
```

Il metodo `Resize` mantiene il rapporto d'aspetto (`0` per l'altezza) e riduce drasticamente la dimensione del file senza sacrificare la precisione OCR per le tipiche ricevute.

### 4️⃣ Problemi di lingua e carattere

Le ricevute possono contenere caratteri speciali (€, ¥, ecc.). Imposta la lingua esplicitamente se conosci la localizzazione:

```csharp
ocrEngine.Language = Language.English; // or Language.Spanish, etc.
```

Per ricevute multilingue, puoi abilitare la modalità multilingua:

```csharp
ocrEngine.Language = Language.English | Language.French;
```

### 5️⃣ Estrarre dati strutturati

Il testo grezzo è utile, ma la maggior parte delle app necessita di campi strutturati (data, totale, articoli). Il layout JSON include le coordinate `BoundingBox` per ogni parola. Puoi post‑processarlo così:

```csharp
var layout = Newtonsoft.Json.Linq.JObject.Parse(jsonResult);
foreach (var word in layout["Words"])
{
    string text = (string)word["Text"];
    // Simple heuristics: look for "$" or "Total"
}
```

Quello snippet mostra l'idea; in produzione probabilmente useresti un'espressione regolare o un piccolo motore di regole.

## Domande frequenti

**Q: Posso eseguirlo su Linux?**  
A: Assolutamente. Aspose.OCR è cross‑platform; basta installare il runtime .NET sulla tua macchina Linux e lo stesso codice funziona.

**Q: E se devo elaborare decine di ricevute al minuto?**  
A: Avvia un ciclo `Parallel.ForEach` e riutilizza una singola istanza di `OcrEngine` – è thread‑safe per operazioni di sola lettura. Ricorda di gestire i limiti di concorrenza della licenza.

**Q: Funziona con foto mobili scattate di lato?**  
A: Il motore include una correzione di base dell'inclinazione, ma per immagini molto inclinate potresti pre‑processare con una libreria di elaborazione immagini (ad es., OpenCV) per raddrizzare prima la ricevuta.

## Esempio completo funzionante (copia‑incolla)

Di seguito trovi il programma *intero* che puoi inserire in `Program.cs`. Non sono necessari altri file oltre alla licenza e a un'immagine di ricevuta.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // Create and configure the OCR engine
        var ocrEngine = new OcrEngine();
        try
        {
            ocrEngine.SetLicense("Aspose.OCR.lic");
        }
        catch (Exception)
        {
            Console.WriteLine("⚠️ Running in trial mode – license not found.");
        }

        // Load the image to be processed (load image for OCR)
        string imagePath = Path.Combine(Environment.CurrentDirectory, "

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}