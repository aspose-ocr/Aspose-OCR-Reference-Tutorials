---
category: general
date: 2026-05-06
description: Scopri come riconoscere il testo da un'immagine usando Aspose OCR in
  C#. Estrai il testo da una ricevuta, carica l'immagine per l'OCR e visualizza un
  esempio completo di Aspose OCR.
draft: false
keywords:
- recognize text from image
- extract text from receipt
- load image for OCR
- Aspose OCR example
language: it
og_description: Impara a riconoscere il testo da un'immagine con Aspose OCR, estrarre
  il testo da una ricevuta e caricare l'immagine per l'OCR in una guida concisa, passo
  dopo passo.
og_title: Riconoscere il testo da un'immagine in C# – Tutorial completo su Aspose
  OCR
tags:
- C#
- OCR
- Aspose
title: Riconoscere il testo da un'immagine in C# – Tutorial completo di Aspose OCR
url: /it/net/text-recognition/recognize-text-from-image-in-c-complete-aspose-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# riconoscere testo da immagine in C# – Tutorial completo Aspose OCR

Hai mai avuto bisogno di **riconoscere testo da immagine** ma non eri sicuro di quale libreria scegliere? Non sei l'unico—molti sviluppatori si trovano nella stessa situazione quando cercano di estrarre numeri da una ricevuta o di scansionare un modulo. La buona notizia è che Aspose OCR rende l'intero processo un gioco da ragazzi, e in questo tutorial ti guideremo attraverso un **esempio completo di Aspose OCR** che ti permette di **estrarre testo da una ricevuta** in poche righe di C#.

Nei prossimi minuti imparerai come **caricare immagine per OCR**, definire l'esatta regione che contiene l'importo totale, eseguire il motore e infine visualizzare il risultato. Nessun riferimento vago a documenti esterni, nessun pezzo mancante—tutto ciò che ti serve per copiare‑incollare ed eseguire è qui. Un po' di configurazione, qualche passaggio, e sarai in grado di riconoscere testo da file immagine al volo.

> **Cosa otterrai**  
> * Un'app console C# eseguibile che riconosce testo da file immagine.  
> * Comprensione del motivo per cui potresti voler limitare l'OCR a un rettangolo specifico (velocità e precisione).  
> * Suggerimenti per gestire casi limite comuni come ricevute sfocate o scansioni ruotate.  

---

## Prerequisiti

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0 SDK (or later) | Aspose OCR è distribuito come libreria .NET Standard 2.0 / .NET 5+, quindi qualsiasi runtime recente funziona. |
| Visual Studio 2022 (or VS Code) | Un IDE confortevole accelera il debug, ma qualsiasi editor in grado di compilare C# va bene. |
| **Aspose.OCR for .NET** NuGet package | Questa è la libreria principale che effettivamente riconosce testo da immagine. |
| A sample receipt image (`receipt.jpg`) | Useremo questo file per dimostrare **estrarre testo da una ricevuta**. |

Puoi installare il pacchetto NuGet con il seguente comando:

```bash
dotnet add package Aspose.OCR
```

Una volta fatto, sei pronto per iniziare a caricare l'immagine per OCR.

---

## Passo 1: Carica l'immagine per OCR

La prima cosa da fare è puntare il motore al file che vuoi analizzare. È qui che compare naturalmente la keyword secondaria **caricare immagine per OCR**.

```csharp
using Aspose.OCR;
using System.Drawing;

// Create the OCR engine instance
var ocrEngine = new OcrEngine();

// Load the receipt image – replace the path with your own file location
ocrEngine.SetImage(@"C:\Images\receipt.jpg");
```

> **Consiglio professionale:** se la tua immagine si trova nella cartella del progetto, puoi usare un percorso relativo come `ocrEngine.SetImage("receipt.jpg");`. Assicurati solo che il file venga copiato nella directory di output (`Copy to Output Directory = PreserveNewest`).

Il metodo `SetImage` accetta qualsiasi formato che System.Drawing può decodificare (JPEG, PNG, BMP, ecc.), quindi non sei limitato a un unico tipo di file.

---

## Passo 2: Definisci l'area di interesse – **estrarre testo da una ricevuta**

Scansionare l'intera immagine spreca cicli CPU e può introdurre rumore. Indicando ad Aspose OCR esattamente dove si trova l'importo totale, aumenti sia la velocità che la precisione. Questa è la parte in cui **estraiamo testo da una ricevuta**.

```csharp
// Define a rectangle that covers the total amount on the receipt
// (x, y, width, height) – adjust these numbers for your own layout
var roi = new Rectangle(150, 500, 300, 80);
ocrEngine.SetRegionOfInterest(roi);
```

> **Perché un rettangolo?**  
> L'OCR engine lavora su una griglia di pixel. Quando lo limiti a una regione, ignora tutto il resto—non più caratteri sparsi dal logo del negozio o dalla riga dell'intestazione.

Se non sei sicuro delle coordinate esatte, puoi usare qualsiasi visualizzatore di immagini che mostri le posizioni dei pixel (ad esempio Paint.NET) per stimare i numeri.

---

## Passo 3: Esegui il motore – **riconoscere testo da immagine** (keyword principale)

Ora avviene la magia. Dici ad Aspose di leggere effettivamente i pixel all'interno del rettangolo appena definito.

```csharp
// Perform the recognition
OcrResult result = ocrEngine.Recognize();
```

`OcrResult` contiene il testo grezzo, i punteggi di confidenza e persino le bounding box per ogni parola. Per una demo rapida stamperemo solo il testo semplice.

```csharp
Console.WriteLine("Total amount detected: " + result.Text);
```

Quando esegui il programma, dovresti vedere qualcosa di simile a:

```
Total amount detected: $23.45
```

Se l'output appare confuso, ricontrolla le coordinate ROI o prova ad aumentare la risoluzione dell'immagine.

---

## Passo 4: Gestire il risultato – rifinire l'**esempio Aspose OCR**

Una soluzione robusta fa più che semplicemente stampare la stringa sulla console. Di seguito trovi un piccolo helper che rimuove gli spazi bianchi, elimina i ritorni a capo indesiderati e valida che il valore estratto abbia l'aspetto di un importo monetario.

```csharp
static string CleanAmount(string raw)
{
    // Remove any non‑numeric characters except dot and comma
    var cleaned = new string(raw
        .Where(c => char.IsDigit(c) || c == '.' || c == ',')
        .ToArray());

    // Normalize decimal separator to dot
    cleaned = cleaned.Replace(',', '.');

    // If we end up with an empty string, return a friendly message
    return string.IsNullOrWhiteSpace(cleaned) ? "N/A" : cleaned;
}

// ...

string amount = CleanAmount(result.Text);
Console.WriteLine($"Parsed amount: ${amount}");
```

L'helper dimostra un **esempio Aspose OCR** realistico che puoi inserire in qualsiasi sistema di fatturazione più grande.

---

## Passo 5: Programma completo eseguibile – la demo definitiva per **estrarre testo da una ricevuta**

Mettendo tutto insieme ottieni un unico file copiabile-incollabile. Salvalo come `Program.cs` ed esegui `dotnet run`.

```csharp
// Program.cs
using Aspose.OCR;
using System;
using System.Drawing;
using System.Linq;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the image for OCR
        var ocrEngine = new OcrEngine();
        ocrEngine.SetImage(@"C:\Images\receipt.jpg");   // <-- adjust path

        // 2️⃣ Define the region that holds the total amount
        var roi = new Rectangle(150, 500, 300, 80);
        ocrEngine.SetRegionOfInterest(roi);

        // 3️⃣ Run the engine – recognize text from image
        OcrResult result = ocrEngine.Recognize();

        // 4️⃣ Clean up the output
        string amount = CleanAmount(result.Text);
        Console.WriteLine($"Total amount detected: ${amount}");
    }

    // Helper that sanitises the OCR output
    static string CleanAmount(string raw)
    {
        var cleaned = new string(raw
            .Where(c => char.IsDigit(c) || c == '.' || c == ',')
            .ToArray());

        cleaned = cleaned.Replace(',', '.');
        return string.IsNullOrWhiteSpace(cleaned) ? "N/A" : cleaned;
    }
}
```

**Output previsto**

```
Total amount detected: $23.45
```

Se l'immagine della ricevuta è più scura o il testo è inclinato, potresti vedere qualcosa come `Total amount detected: 23,45`. Il metodo `CleanAmount` normalizza questo in un formato decimale standard.

---

## Problemi comuni quando **riconosci testo da immagine**

### 1. Coordinate ROI errate
Se il rettangolo è troppo piccolo, il motore taglierà i caratteri; se è troppo grande, re‑introdurrai rumore. Usa uno strumento visivo per affinare i numeri, o rileva programmaticamente i bordi della ricevuta con una semplice libreria di elaborazione immagini (ad esempio OpenCV).

### 2. Scansioni a bassa risoluzione
La precisione dell'OCR diminuisce drasticamente sotto i 150 dpi. Se controlli il processo di scansione, punta ad almeno 300 dpi. Se sei bloccato con un file a bassa risoluzione, prova `ocrEngine.SetResolution(300);` prima di chiamare `Recognize()`.

### 3. Ricevute inclinate o ruotate
Aspose OCR può ruotare automaticamente, ma devi abilitarlo:

```csharp
ocrEngine.SetAutoRotate(true);
```

### 4. Impostazioni della lingua
La lingua predefinita è l'inglese. Se la tua ricevuta contiene altri alfabeti, imposta la lingua esplicitamente:

```csharp
ocrEngine.Language = OcrLanguage.French; // or any supported language
```

---

## Casi limite e variazioni – estendere l'**esempio Aspose OCR**

* **Multiple fields:** Vuoi estrarre anche la data e l'importo dell'imposta? Basta ripetere il passo ROI con un nuovo rettangolo e chiamare `Recognize()` di nuovo (oppure riutilizzare lo stesso motore dopo aver reimpostato il ROI).  
* **Batch processing:** Avvolgi la logica in un ciclo `foreach (var file in Directory.GetFiles(@"C:\Receipts"))` per gestire automaticamente decine di file.  
* **Async execution:** Il metodo `Recognize` è sincrono, ma puoi spostarlo in un thread di background con `Task.Run` se stai costruendo un'app UI.  

---

## Riferimento visivo

![esempio di riconoscere testo da immagine](/images/ocr-demo.png "Screenshot che mostra il risultato di Aspose OCR – riconoscere testo da immagine")

*Lo screenshot dimostra l'output della console dopo aver eseguito il programma completo.*

---

## Conclusione

Abbiamo appena **riconosciuto testo da immagine** usando Aspose OCR, abbiamo illustrato come **caricare immagine per OCR**, e costruito un flusso pratico per **estrarre testo da una ricevuta** che puoi inserire in qualsiasi progetto .NET. L'**esempio completo di Aspose OCR** è composto da poche righe, ma copre gli scenari più comuni: selezione ROI, pulizia del risultato e gestione dei problemi tipici.

Prossimi passi? Prova a sostituire il rettangolo con una routine di rilevamento dinamico, sperimenta con lingue diverse, o integra l'output in un database per il tracciamento automatico delle spese. Il cielo è il limite, e con le basi che ora possiedi, sarà facile espandere.

Hai domande o una ricevuta ostinata che rifiuta di collaborare?

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}