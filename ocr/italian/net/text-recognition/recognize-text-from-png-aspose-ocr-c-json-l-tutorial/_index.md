---
category: general
date: 2026-03-26
description: Riconosci il testo da un PNG ed estrai i dati della ricevuta usando Aspose
  OCR in C#. Converti l'immagine in JSON‑L ed elabora la ricevuta con OCR in un esempio
  completo.
draft: false
keywords:
- recognize text from png
- extract text from receipt
- convert image to jsonl
- process receipt with ocr
- aspose ocr example c#
language: it
og_description: Riconosci il testo da PNG e trasforma le ricevute in JSON‑L con Aspose
  OCR in C#. Codice completo passo‑passo e consigli.
og_title: Riconoscere il testo da PNG – Guida Aspose OCR C#
tags:
- Aspose OCR
- C#
- JSONL
- Receipt Processing
title: Riconoscere il testo da PNG – tutorial Aspose OCR C# JSON‑L
url: /it/net/text-recognition/recognize-text-from-png-aspose-ocr-c-json-l-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Riconoscere testo da png – Guida completa Aspose OCR C#  

Hai mai avuto bisogno di **recognize text from png** file ma non eri sicuro quale libreria ti avrebbe fornito risultati puliti, riga per riga? Non sei solo. In molte app per piccole imprese lo scontrino è salvato come immagine PNG, e estrarre l'importo, la data o il nome del commerciante è un problema quotidiano.  

La buona notizia? Con poche righe di C# e la libreria **Aspose OCR** puoi **extract text from receipt**, poi **convert image to jsonl** per analisi successive. In questo tutorial percorreremo l'intera pipeline—caricamento di un PNG, esecuzione dell'OCR e scrittura di ogni riga in un file JSON‑L—così potrai **process receipt with OCR** subito.

Copriamo tutto ciò di cui hai bisogno: pacchetti NuGet richiesti, un programma completo eseguibile, spiegazioni sul perché ogni passaggio è importante e una serie di consigli pratici che apprezzerai quando gli scontrini diventano disordinati. Nessuna documentazione esterna necessaria; basta copiare‑incollare, eseguire e adattare.

---

## Cosa imparerai

- Come **recognize text from png** usando `Aspose.OCR`.
- Come **extract text from receipt** oggetti riga e catturare i punteggi di confidenza.
- Come **convert image to jsonl** così ogni riga OCR diventa un oggetto JSON separato.
- Come **process receipt with OCR** end‑to‑end, gestendo casi limite come immagini vuote o righe a bassa confidenza.
- Suggerimenti per risolvere i problemi comuni di OCR e migliorare l'accuratezza.

### Prerequisiti

- .NET 6.0 o successivo (il codice funziona anche con .NET Core e .NET Framework).
- Visual Studio 2022 o qualsiasi IDE tu preferisca.
- Una licenza valida Aspose OCR (puoi iniziare con una licenza temporanea gratuita da Aspose.com).
- Un esempio di scontrino salvato come `receipt.png` in una cartella a tua disposizione.

---

## Passo 1: Riconoscere testo da png con Aspose OCR

La prima cosa di cui abbiamo bisogno è un `OcrEngine` inizializzato. Questo oggetto contiene le impostazioni del motore OCR (lingua, modalità di rilevamento, ecc.). Per impostazione predefinita utilizza l'inglese e rileva automaticamente il layout della pagina, il che funziona bene per la maggior parte degli scontrini.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;
using System.IO;

class JsonLExample
{
    static void Main()
    {
        // Initialize the OCR engine – this is where Aspose loads its models.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the PNG image that contains the receipt.
        string imagePath = @"YOUR_DIRECTORY\receipt.png";
        OcrImage receiptImage = OcrImage.FromFile(imagePath);

        // Run OCR and get the result object.
        OcrResult ocrResult = ocrEngine.Recognize(receiptImage);
```

**Perché è importante:**  
`OcrEngine` è il componente che svolge il lavoro pesante; crearlo una sola volta e riutilizzarlo su molte immagini riduce il consumo di memoria. Se ti serve una lingua diversa (ad esempio scontrini spagnoli), puoi impostare `ocrEngine.Language = OcrLanguage.Spanish;` prima di chiamare `Recognize`.

---

## Passo 2: Estrarre testo dalle righe dello scontrino

`OcrResult` contiene una collezione chiamata `Lines`. Ogni riga contiene il testo grezzo e un punteggio di confidenza (0‑100). Estrarre questi dati ti dà un controllo granulare—puoi scartare le righe a bassa confidenza o segnalarle per una revisione manuale.

```csharp
        // Prepare to write each line as a JSON‑L record.
        string jsonlPath = @"YOUR_DIRECTORY\receipt.jsonl";

        using (StreamWriter jsonLineWriter = new StreamWriter(jsonlPath))
        {
            foreach (var line in ocrResult.Lines)
            {
                // Build a simple JSON object for the line.
                string json = $"{{\"text\":\"{EscapeJson(line.Text)}\",\"confidence\":{line.Confidence}}}";
                jsonLineWriter.WriteLine(json);
            }
        }

        Console.WriteLine("JSON‑L file written to " + jsonlPath);
    }

    // Helper to escape quotes and backslashes in JSON strings.
    private static string EscapeJson(string s) => s.Replace("\\", "\\\\").Replace("\"", "\\\"");
}
```

**Perché sfuggiamo al JSON:**  
Il testo dello scontrino può contenere virgolette (`"`) o backslash (`\`) che romperebbero una stringa JSON ingenua. Il metodo `EscapeJson` garantisce una riga JSON valida.

**Come appare l'output:**  

```
{"text":"Store XYZ","confidence":98.5}
{"text":"Date: 2024-07-15","confidence":97.2}
{"text":"Total $23.45","confidence":99.1}
```

Ogni riga è un record separato, perfetto per lo streaming in un data lake o per alimentare un modello di machine‑learning.

---

## Passo 3: Convertire immagine in JSONL – gestione dei casi limite

Quando elabori un batch di scontrini, alcune immagini potrebbero essere vuote, corrotte o avere punteggi di confidenza estremamente bassi. Rendiamo la pipeline un po' più robusta.

```csharp
        // After OCR, check if any lines were detected.
        if (ocrResult.Lines.Count == 0)
        {
            Console.WriteLine("Warning: No text detected. Verify the image path and quality.");
            return;
        }

        // Optional: filter out lines with confidence below a threshold.
        const double minConfidence = 80.0;
        foreach (var line in ocrResult.Lines)
        {
            if (line.Confidence < minConfidence)
                continue; // skip noisy line
            // write as before...
        }
```

**Perché filtrare:**  
Gli scontrini stampati su carta sbiadita possono generare caratteri sparsi con bassa confidenza. Eliminare tutto sotto l'80 % di solito rimuove il rumore mantenendo i dati utili.

---

## Passo 4: Processare lo scontrino con OCR – esempio end‑to‑end

Mettendo tutto insieme, ecco il programma **completo, pronto‑all‑uso**. Sostituisci `YOUR_DIRECTORY` con la cartella che contiene il tuo file PNG.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;
using System.IO;

class JsonLExample
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load receipt PNG
        string imagePath = @"YOUR_DIRECTORY\receipt.png";
        OcrImage receiptImage = OcrImage.FromFile(imagePath);

        // 3️⃣ Perform OCR
        OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

        // 4️⃣ Verify we got something back
        if (ocrResult.Lines.Count == 0)
        {
            Console.WriteLine("❗ No text found – check the image quality.");
            return;
        }

        // 5️⃣ Write each line to a JSON‑L file
        string jsonlPath = @"YOUR_DIRECTORY\receipt.jsonl";
        using (StreamWriter writer = new StreamWriter(jsonlPath))
        {
            const double minConfidence = 80.0;
            foreach (var line in ocrResult.Lines)
            {
                if (line.Confidence < minConfidence) continue; // skip low‑confidence

                string json = $"{{\"text\":\"{EscapeJson(line.Text)}\",\"confidence\":{line.Confidence}}}";
                writer.WriteLine(json);
            }
        }

        Console.WriteLine($"✅ JSON‑L written to: {jsonlPath}");
    }

    // Helper to make JSON safe
    private static string EscapeJson(string s) => s.Replace("\\", "\\\\").Replace("\"", "\\\"");
}
```

**Esecuzione del codice:**  
1. Apri un terminale nella cartella del progetto.  
2. `dotnet add package Aspose.OCR` – installa la libreria.  
3. `dotnet run` – dovresti vedere il messaggio di successo e apparire un file `receipt.jsonl`.

**Risultato atteso:** Un file JSON delimitato per righe dove ogni riga rispecchia una riga dello scontrino, completa di punteggi di confidenza. Ora puoi inviare questo file a Power BI, Elastic o a qualsiasi strumento di analisi che comprenda JSON‑L.

---

## Problemi comuni & consigli professionali

| Problema | Perché succede | Soluzione rapida |
|----------|----------------|------------------|
| **Output vuoto** | Percorso immagine errato o file non PNG. | Verifica nuovamente il percorso, usa `File.Exists(imagePath)`. |
| **Caratteri spazzatura** | Bassa DPI o PNG fortemente compresso. | Usa scansioni di almeno 300 dpi; evita compressione JPEG aggressiva. |
| **Troppe righe a bassa confidenza** | Scontrino stampato su carta termica sbiadita. | Aumenta la soglia `minConfidence` o pre‑processa l'immagine (contrasto/soglia). |
| **Errori di parsing JSON** | Virgolette non escape nel testo dello scontrino. | Mantieni l'helper `EscapeJson` o passa a `System.Text.Json` per una serializzazione robusta. |

**Consiglio professionale:** Se devi estrarre campi specifici (ad esempio l'importo totale), esegui una semplice regex su ogni `line.Text` dopo aver ottenuto il file JSON‑L. Questo mantiene l'OCR separato dalla logica di business e semplifica il debug.

---

## Estendere la soluzione

- **Elaborazione batch:** Avvolgi la logica `Main` in un `foreach` su tutti i file PNG in una directory.  
- **Supporto multilingua:** Imposta `ocrEngine.Language = OcrLanguage.Spanish;` (o qualsiasi lingua supportata) prima di `Recognize`.  
- **Output strutturato:** Invece di JSON riga per riga, crea un oggetto `Receipt` con proprietà `Date`, `Merchant`, `Total`, poi serializzalo una sola volta.  

Tutte queste varianti continuano a **convert image to jsonl** al centro, così puoi cambiare il consumatore downstream senza toccare la parte OCR.

---

## Conclusione

Ti abbiamo appena mostrato come **recognize text from png** file usando Aspose OCR, **extract text from receipt**, e **convert image to jsonl** per una facile elaborazione successiva. Il programma C# completo e autonomo dimostra l'intero flusso di lavoro—dal caricamento di un PNG, alla gestione dei casi limite, fino alla scrittura di un file JSON‑L pulito—così puoi subito **process receipt with OCR** nei tuoi progetti.

Provalo con alcuni scontrini di esempio, regola la soglia di confidenza e vedrai quanto rapidamente una pila rumorosa di immagini si trasformi in dati strutturati pronti per l'analisi. Quando ti sentirai a tuo agio, esplora l'elaborazione batch o aggiungi un piccolo modello ML per classificare automaticamente le categorie di spesa.

Hai domande o hai scoperto un trucco intelligente? Lascia un commento qui sotto—buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}