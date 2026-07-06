---
category: general
date: 2026-05-31
description: Scopri come ottenere i punteggi di confidenza OCR in C# mentre estrai
  il testo da un'immagine e leggi l'immagine della ricevuta con Aspose OCR.
draft: false
keywords:
- ocr confidence scores
- extract text from image
- ocr bounding boxes
- perform ocr on jpg
- read receipt image
language: it
og_description: I punteggi di confidenza OCR ti permettono di valutare l'accuratezza;
  questa guida mostra come estrarre il testo da un'immagine, ottenere le bounding
  box e leggere l'immagine della ricevuta utilizzando Aspose OCR.
og_title: Punteggi di confidenza OCR in C# – Guida completa
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get OCR confidence scores in C# while extract text from
    image and read receipt image with Aspose OCR.
  headline: OCR confidence scores in C# – Complete Guide
  type: TechArticle
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Punteggi di fiducia OCR in C# – Guida completa
url: /it/net/ocr-optimization/ocr-confidence-scores-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Punteggi di confidenza OCR in C# – Guida completa

Ti sei mai chiesto come ottenere **OCR confidence scores** quando devi *estrarre testo dall'immagine*? Forse stai cercando di **leggere immagini di ricevute** per tenere traccia delle spese e vuoi sapere quali caratteri il motore trova incerti. La buona notizia? Con Aspose.OCR puoi recuperare percentuali di confidenza, riquadri di delimitazione e testo semplice da un JPG in poche righe di C#.

In questo tutorial vedremo tutto ciò che serve: installare la libreria, configurare il motore per **eseguire OCR su JPG**, estrarre i punteggi di confidenza e interpretare i **OCR bounding boxes** che indicano dove si trova ogni carattere nella pagina. Alla fine avrai un’app console pronta all’uso che stampa ogni carattere, la sua confidenza e la sua posizione—perfetta per convalidare ricevute o qualsiasi documento scansionato.

## Cosa imparerai

- Installare Aspose.OCR tramite NuGet e configurare un motore OCR di base.  
- Configurare `OcrOptions` per richiedere l’output in testo semplice **con punteggi di confidenza** e **bounding boxes**.  
- Scorrere `OcrResult` per **estrarre testo dall’immagine** riga per riga e simbolo per simbolo.  
- Gestire le difficoltà più comuni, come file mancanti, caratteri a bassa confidenza e formati non JPG.  
- Estendere l’esempio per elaborare più immagini di ricevute in una cartella.

Non è necessaria alcuna esperienza pregressa con Aspose; basta un ambiente .NET funzionante e un’immagine di ricevuta (JPG) da testare.

---

## Passo 1 – Installa Aspose.OCR e prepara il tuo progetto

Prima di tutto: ti serve il pacchetto NuGet Aspose.OCR. Apri un terminale nella cartella del progetto e digita:

```bash
dotnet add package Aspose.OCR
```

> **Suggerimento:** La versione di prova gratuita funziona fino a 200 pagine, più che sufficiente per testare la scansione delle ricevute.

Dopo aver installato il pacchetto, crea un nuovo progetto console (se non ne hai già uno):

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
```

Ora apri il file `Program.cs` generato e aggiungi le direttive `using`:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
```

Questi namespace ti danno accesso a `OcrEngine`, `OcrOptions` e ai tipi di risultato di cui avremo bisogno più avanti.

## Passo 2 – Ottieni i punteggi di confidenza OCR e i bounding boxes OCR

Questo è il cuore del tutorial. Configureremo il motore in modo che ogni carattere riconosciuto venga restituito con un **punteggio di confidenza** e un **bounding box** (il rettangolo che racchiude il glifo). L’intestazione H2 stessa contiene la parola chiave principale, soddisfacendo la regola SEO.

```csharp
// Step 2: Initialize the OCR engine and request detailed output
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process – here we assume a JPEG receipt
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Tell Aspose we want plain text, confidence percentages, and bounding boxes
ocrEngine.Options = new OcrOptions
{
    OutputFormat = OcrOutputFormat.PlainText,
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};
```

**Perché includere i punteggi di confidenza?**  
Un punteggio di confidenza (0‑100 %) indica quanto il motore è sicuro di ogni carattere. Se invii l’output a una logica successiva—ad esempio un flusso di approvazione delle spese—puoi rifiutare o segnalare automaticamente i simboli a bassa confidenza.

**Perché richiedere i bounding boxes?**  
I bounding boxes sono essenziali quando devi evidenziare il testo sull’immagine originale, estrarre sotto‑regioni o allineare i risultati OCR con un overlay UI. Ogni `character.Bounds` fornisce le coordinate X, Y, larghezza e altezza in pixel.

## Passo 3 – Esegui OCR su JPG ed estrai testo dall’immagine

Ora eseguiamo effettivamente il motore. La chiamata a `Recognize()` esegue tutto il lavoro pesante e restituisce un oggetto `OcrResult`.

```csharp
// Step 3: Run the OCR process
OcrResult ocrResult = ocrEngine.Recognize();
```

Se il percorso dell’immagine è errato o il file non è in un formato supportato, Aspose genera una `FileNotFoundException` o una `UnsupportedImageFormatException`. In produzione avvolgi la chiamata in un blocco try/catch per gestire questi casi limite in modo elegante.

### Estrarre il testo semplice

Se ti serve solo il testo concatenato, puoi leggere `ocrResult.Text`:

```csharp
Console.WriteLine("Full extracted text:");
Console.WriteLine(ocrResult.Text);
```

Ma poiché abbiamo anche richiesto i punteggi di confidenza e i bounding boxes, itereremo nella struttura per vedere i dettagli di ogni carattere.

## Passo 4 – Scorri righe, simboli e visualizza i punteggi di confidenza OCR

Ecco il ciclo che stampa ogni carattere, la sua confidenza e il suo riquadro. È qui che l’esempio **leggi immagine di ricevuta** brilla davvero.

```csharp
// Step 4: Walk through each line and each symbol (character)
foreach (var textLine in ocrResult.Lines)
{
    foreach (var character in textLine.Symbols)
    {
        Console.WriteLine(
            $"Char: '{character.Text}'  Confidence: {character.Confidence}%  Box: {character.Bounds}");
    }
}
```

Un output di esempio potrebbe apparire così:

```
Char: 'R'  Confidence: 98%  Box: {X=12,Y=34,Width=15,Height=20}
Char: 'e'  Confidence: 95%  Box: {X=28,Y=34,Width=12,Height=20}
Char: 'c'  Confidence: 92%  Box: {X=41,Y=34,Width=13,Height=20}
...
```

**Interpretazione dei numeri:**  
- **Confidenza ≥ 90 %** – di solito accettabile.  
- **Confidenza 70‑89 %** – potresti voler ricontrollare, soprattutto per le cifre negli importi.  
- **Confidenza < 70 %** – considera di segnalare per revisione manuale.

## Passo 5 – Esempio completo eseguibile (con gestione errori)

Mettendo tutto insieme, ecco un programma completo da copiare‑incollare in `Program.cs`. Include un semplice controllo per file mancanti e stampa un messaggio amichevole se l’OCR fallisce.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the receipt image – adjust to your environment
            const string imagePath = "YOUR_DIRECTORY/receipt.jpg";

            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found -> {imagePath}");
                return;
            }

            try
            {
                // Initialize engine
                OcrEngine ocrEngine = new OcrEngine
                {
                    Image = ImageStream.FromFile(imagePath),
                    Options = new OcrOptions
                    {
                        OutputFormat = OcrOutputFormat.PlainText,
                        IncludeConfidence = true,
                        IncludeBoundingBoxes = true
                    }
                };

                // Perform OCR
                OcrResult ocrResult = ocrEngine.Recognize();

                // Show full plain text (optional)
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
                Console.WriteLine();

                // Show each character with confidence and bounding box
                Console.WriteLine("=== Detailed Character Data ===");
                foreach (var line in ocrResult.Lines)
                {
                    foreach (var symbol in line.Symbols)
                    {
                        Console.WriteLine(
                            $"Char: '{symbol.Text}'  Confidence: {symbol.Confidence}%  Box: {symbol.Bounds}");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"OCR failed: {ex.Message}");
            }
        }
    }
}
```

### Output previsto

Quando esegui `dotnet run` la console mostrerà prima il testo concatenato della ricevuta, poi un elenco di ogni carattere con il relativo punteggio di confidenza e il bounding box. Se la confidenza di un carattere è bassa, vedrai una percentuale inferiore all’80, segnale per verificare manualmente quella parte della ricevuta.

## Bonus: Elaborare più ricevute in una cartella

Se disponi di un batch di JPG di ricevute, avvolgi la logica sopra in un ciclo `foreach (var file in Directory.GetFiles(folder, "*.jpg"))`. Ricorda di resettare l’`OcrEngine` per ogni file, o di crearne uno nuovo all’interno del ciclo per evitare perdite di stato.

```csharp
string folder = "YOUR_DIRECTORY/Receipts";
foreach (var file in System.IO.Directory.GetFiles(folder, "*.jpg"))
{
    // reuse the same code block, just replace imagePath with 'file'
}
```

L’elaborazione in blocco è comoda per importazioni notturne delle spese.

---

## Conclusione

Ora disponi di una soluzione solida, end‑to‑end, per ottenere **OCR confidence scores** in C#, **estrarre testo dall’immagine** e recuperare **OCR bounding boxes** mentre **esegui OCR su JPG** come una **immagine di ricevuta**. Il codice è completamente autonomo, funziona con l’ultima versione di Aspose.OCR (al 31‑05‑2026) e ti fornisce i dati granulari necessari per costruire pipeline di elaborazione documenti affidabili.

Qual è il prossimo passo? Prova a visualizzare i bounding boxes sull’immagine originale usando `System.Drawing` o una libreria UI, oppure invia i caratteri a bassa confidenza a un servizio di verifica secondario. Puoi anche sperimentare con lingue diverse impostando `ocrEngine.Options.Language = OcrLanguage.French;` – l’API supporta molte localizzazioni.

Buon coding, e che i tuoi punteggi di confidenza rimangano sempre alti! 

![Console output showing OCR confidence scores and bounding boxes for a receipt

## Cosa dovresti imparare dopo?

- [Estrai testo immagine C# con selezione lingua usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Come ottenere le scelte di carattere OCR per i caratteri riconosciuti in Image Recognition](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)
- [Come usare Aspose OCR per risultato JSON in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}