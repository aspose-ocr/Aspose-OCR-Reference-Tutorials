---
category: general
date: 2026-02-20
description: Impara a leggere una ricevuta in C# estraendo il testo dall'immagine
  e convertendolo in JSON. Codice passo‑passo con Aspose OCR.
draft: false
keywords:
- how to read receipt
- extract text from image
- convert image to json
- load image file c#
- OCR receipt C#
- Aspose OCR tutorial
language: it
og_description: Scopri come leggere una ricevuta in C# caricando un file immagine,
  estrarre il testo con Aspose OCR e convertire il risultato in JSON. Esempio di codice
  completo.
og_title: Come leggere una ricevuta in C# – estrarre il testo, convertire in JSON
tags:
- C#
- OCR
- Image Processing
- JSON
title: Come leggere una ricevuta in C# – Guida completa per estrarre il testo da un'immagine
url: /it/net/text-recognition/how-to-read-receipt-in-c-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come leggere una ricevuta in C# – Guida completa

Ti sei mai chiesto **come leggere le ricevute** in modo programmatico? Forse stai creando un'app di tracciamento delle spese e hai bisogno di estrarre le voci da una foto di una ricevuta della spesa. Nella mia esperienza il punto dolente più grande è trasformare quel JPEG sfocato in dati strutturati effettivamente utilizzabili. La buona notizia? Con poche righe di C# e Aspose OCR puoi **estrarre testo da immagine**, poi **convertire immagine in JSON** in modo quasi magico.

In questo tutorial otterrai una soluzione pronta all'uso che **carica un file immagine C#**, esegue l'OCR e restituisce un payload JSON dettagliato. Nessun servizio esterno, nessuna chiamata REST complicata—solo puro codice .NET che puoi inserire in qualsiasi progetto console o ASP.NET. Alla fine comprenderai perché ogni passaggio è importante, come gestire i casi limite più comuni (come ricevute di dimensioni non standard) e come appare effettivamente l'output JSON.

## Cosa ti serve

- **.NET 6.0 o successivo** – il codice utilizza `System.Drawing.Common` che è supportato su Windows, Linux e macOS.
- **Aspose.OCR per .NET** – puoi scaricare il pacchetto NuGet di prova gratuita (`Aspose.OCR`) o usare una copia con licenza se ne possiedi una.
- Un **esempio di immagine di ricevuta** (`receipt.jpg`) posizionata in una cartella accessibile dall'app.
- Qualsiasi IDE ti piaccia (Visual Studio, Rider, VS Code).  

Tutto qui. Nessuna configurazione aggiuntiva, nessuna chiave API.

---

## Passo 1 – Carica il file immagine C# (Parola chiave principale in azione)

Prima che il motore OCR possa fare la sua magia, devi caricare l’immagine in memoria. Questo è il classico passaggio “carica file immagine C#” che molti sviluppatori trascurano.

```csharp
using System.Drawing;          // Required for Image
using Aspose.OCR;
using Aspose.OCR.Models;

// Path to your receipt image – adjust as needed
string imagePath = @"C:\Receipts\receipt.jpg";

// Load the image into a System.Drawing.Image object
Image receiptImage = Image.FromFile(imagePath);
```

**Perché è importante:**  
`Image.FromFile` legge il file *una sola volta* e mantiene aperta una handle, il che è perfetto per una rapida passata OCR. Se stai elaborando molte ricevute in un ciclo, considera l'uso di `Image.FromStream` per evitare di bloccare il file.

> **Consiglio esperto:** Se ti imbatte in una *FileNotFoundException*, ricontrolla il percorso e assicurati che l’immagine sia realmente presente. Anche i percorsi relativi funzionano (`"./receipt.jpg"`), ma i percorsi assoluti sono più sicuri in ambienti di produzione.

---

## Passo 2 – Crea e configura il motore OCR

Aspose OCR fornisce un `OcrEngine` pronto all’uso. Non è necessario addestrare un modello; la libreria sa già leggere il testo stampato, che è esattamente quello usato nella maggior parte delle ricevute.

```csharp
// Instantiate the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Optional: tweak recognition settings if your receipts are low‑contrast
ocrEngine.Config.Language = OcrLanguage.English;
ocrEngine.Config.DetectOrientation = true;   // Handles rotated receipts
```

**Perché impostiamo queste opzioni:**  
`DetectOrientation` indica al motore di ruotare automaticamente l’immagine se la ricevuta è stata scansionata capovolta. Impostare la lingua restringe il set di caratteri, il che può migliorare l'accuratezza—soprattutto quando ti servono solo dati alfanumerici in inglese.

---

## Passo 3 – Riconosci l’immagine e converti in JSON

Ora arriva la parte divertente: **estrarre testo da immagine** e **convertire immagine in JSON** con una singola chiamata.

```csharp
// Perform OCR and get the result as a JSON string
string jsonResult = ocrEngine.RecognizeToJson(receiptImage);
```

Il metodo `RecognizeToJson` restituisce una struttura JSON ricca che include:

- `Text`: il testo semplice concatenato.
- `Lines`: un array di oggetti linea con coordinate.
- `Words`: ogni parola con punteggi di confidenza.
- `Regions`: riquadri delimitanti per i blocchi di testo rilevati.

Puoi deserializzare questo JSON in un oggetto C# se ti serve un accesso tipizzato, ma nella maggior parte degli scenari stampare il JSON grezzo è sufficiente.

---

## Passo 4 – Output del JSON (o salvataggio)

Vediamo l'output e discutiamo cosa farne.

```csharp
// Write the JSON to the console – perfect for quick debugging
Console.WriteLine(jsonResult);

// Bonus: Save the JSON to a file for later processing
File.WriteAllText("receipt_output.json", jsonResult);
```

### Output di esempio

```json
{
  "Text":"Walmart\n123 Main St\nItem A  $2.99\nItem B  $5.49\nTotal   $8.48",
  "Lines":[
    {"Text":"Walmart","BoundingBox":{"X":10,"Y":15,"Width":200,"Height":30}},
    {"Text":"123 Main St","BoundingBox":{"X":10,"Y":50,"Width":180,"Height":25}},
    {"Text":"Item A  $2.99","BoundingBox":{"X":10,"Y":85,"Width":210,"Height":28}},
    {"Text":"Item B  $5.49","BoundingBox":{"X":10,"Y":120,"Width":210,"Height":28}},
    {"Text":"Total   $8.48","BoundingBox":{"X":10,"Y":155,"Width":210,"Height":30}}
  ],
  "Words":[
    {"Text":"Walmart","Confidence":0.99,"BoundingBox":{...}},
    …
  ]
}
```

**Cosa fare dopo?**  
Analizza l'array `Lines` per estrarre l'importo `Total`, oppure invia il JSON a un servizio downstream che memorizza le voci di spesa. Poiché il risultato è già in formato JSON, lo puoi collegare direttamente a qualsiasi database NoSQL, Azure Function o flusso Power Automate.

---

## Passo 5 – Gestione dei casi limite più comuni

Anche i migliori motori OCR inciampano su alcune situazioni. Di seguito trovi scenari che potresti incontrare mentre impari **come leggere le ricevute** in immagini.

| Situazione | Correzione / Raccomandazione |
|------------|------------------------------|
| **Ricevuta a bassa risoluzione (≤ 150 dpi)** | Ingrandisci l’immagine prima usando `Bitmap` e `Graphics` (`InterpolationMode.HighQualityBicubic`). |
| **Ricevuta ruotata o inclinata** | Mantieni `DetectOrientation = true`. Per inclinazioni severe, pre‑processa con `Image.RotateFlip` o una libreria di terze parti come OpenCV. |
| **Sfondo colorato (es. ricevuta su un tavolo)** | Converti in scala di grigi e aumenta il contrasto prima dell'OCR (`ImageAttributes`). |
| **Più ricevute in una foto** | Ritaglia manualmente ogni regione di ricevuta o usa `ocrEngine.Config.RecognizeMultipleRegions = true`. |
| **File di grandi dimensioni che causano OutOfMemory** | Usa istruzioni `using` per eliminare rapidamente gli oggetti `Image`, oppure elabora a blocchi. |

```csharp
// Example: simple grayscale conversion
using (Bitmap bmp = new Bitmap(receiptImage))
{
    for (int y = 0; y < bmp.Height; y++)
        for (int x = 0; x < bmp.Width; x++)
        {
            Color c = bmp.GetPixel(x, y);
            int gray = (int)(c.R * 0.3 + c.G * 0.59 + c.B * 0.11);
            bmp.SetPixel(x, y, Color.FromArgb(gray, gray, gray));
        }
    receiptImage = (Image)bmp.Clone();
}
```

---

## Passo 6 – Esempio completo (pronto da copiare‑incollare)

Di seguito trovi il programma *completo* che puoi compilare subito. Include tutti i passaggi, le direttive `using` corrette e una gestione degli errori elegante.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptReaderDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image file C#
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY\receipt.jpg";

            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found: {imagePath}");
                return;
            }

            Image receiptImage;
            try
            {
                receiptImage = Image.FromFile(imagePath);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"⚠️ Failed to load image: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Create and configure OCR engine
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine
            {
                Config =
                {
                    Language = OcrLanguage.English,
                    DetectOrientation = true
                }
            };

            // -------------------------------------------------
            // 3️⃣ Recognize and convert to JSON
            // -------------------------------------------------
            string jsonResult;
            try
            {
                jsonResult = ocrEngine.RecognizeToJson(receiptImage);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"🛑 OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 4️⃣ Output results
            // -------------------------------------------------
            Console.WriteLine("🗂️ OCR JSON Result:");
            Console.WriteLine(jsonResult);

            // Optionally persist the JSON
            string outputPath = Path.Combine(
                Path.GetDirectoryName(imagePath) ?? ".", "receipt_output.json");
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"✅ JSON saved to {outputPath}");
        }
    }
}
```

**Esegui:**  
`dotnet run` dalla cartella del progetto. Se tutto è configurato correttamente vedrai il JSON stampato nella console e salvato accanto all’immagine della ricevuta.

---

## Conclusione

Abbiamo appena coperto **come leggere le ricevute** in C# dall'inizio alla fine. Caricando l’immagine, configurando Aspose OCR e chiamando `RecognizeToJson`, puoi **estrarre testo da immagine** e **convertire immagine in JSON** con praticamente nessun boilerplate. L'approccio scala—da una demo con una singola ricevuta a un processore batch che gestisce centinaia di ricevute ogni notte.

Prossimi passi che potresti esplorare:

- **Analizzare il JSON** per estrarre date, totali e voci di linea (usa `System.Text.Json` o `Newtonsoft.Json`).
- **Integrare con un database** (SQL, Cosmos DB) per memorizzare automaticamente i record di spesa.
- **Aggiungere un’interfaccia UI** (WinForms, WPF o Blazor) così gli utenti possono trascinare le ricevute.
- **Sostituire Aspose OCR** con un altro motore (Tesseract, Microsoft Azure OCR) se la licenza è un problema—basta mantenere lo stesso pattern “carica file immagine C#”.

Sentiti libero di sperimentare, rompere le cose e poi tornare qui per un ripasso. Se incontri difficoltà, la community (e i forum Aspose) sono ottimi posti dove chiedere. Buona programmazione e divertiti a trasformare quelle ricevute cartacee in dati puliti e ricercabili!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}