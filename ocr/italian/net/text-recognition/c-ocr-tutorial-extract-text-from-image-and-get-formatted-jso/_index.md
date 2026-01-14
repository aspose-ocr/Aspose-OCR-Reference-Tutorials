---
category: general
date: 2026-01-13
description: Tutorial OCR in C# che mostra come estrarre testo da un'immagine, caricare
  l'immagine per l'OCR e formattare l'output JSON usando Aspose OCR. Impara a serializzare
  un oggetto in JSON.
draft: false
keywords:
- c# ocr tutorial
- extract text from image
- format json output
- serialize object to json
- load image for ocr
language: it
og_description: Tutorial OCR in C# che ti guida nell'estrazione del testo da un'immagine,
  nel caricamento dell'immagine per l'OCR e nella formattazione dell'output JSON con
  Aspose OCR.
og_title: c# tutorial OCR – Estrai testo e formatta JSON
tags:
- OCR
- C#
- JSON
title: c# tutorial OCR – Estrai testo dall'immagine e ottieni JSON formattato
url: /it/net/text-recognition/c-ocr-tutorial-extract-text-from-image-and-get-formatted-jso/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tutorial c# ocr – Estrarre testo da immagine e formattare output JSON

Ti sei mai chiesto come **estrarre testo da immagine** in un progetto C# senza dover combattere con l'elaborazione a livello di pixel? Questo è il problema che risolve questo *c# ocr tutorial*. In pochi minuti vedrai come **caricare immagine per ocr**, eseguire Aspose OCR e **formattare output json** così da poter inviare i dati direttamente alla tua API o al tuo database.

Passeremo in rassegna ogni riga di codice, spiegheremo perché ogni parte è importante e mostreremo anche il JSON esatto che dovresti ottenere. Alla fine avrai un'app console pronta all'uso che trasforma un PNG di fattura in JSON pulito e indentato. Nessun superfluo, solo una soluzione pratica da inserire in qualsiasi progetto .NET 6+.

## Cosa copre questo c# ocr tutorial

- Installazione del pacchetto NuGet Aspose.OCR  
- Caricamento di un file immagine per l'elaborazione OCR  
- Riconoscimento del testo in inglese (o in qualsiasi lingua supportata)  
- **Serializzare il risultato OCR in JSON** con stampa formattata  
- Visualizzare il JSON nella console e salvarlo, se lo desideri  

Hai bisogno solo di una conoscenza di base di C# e di un SDK .NET recente. Nient'altro. Se sei curioso di sapere come **estrarre testo da immagine** per fatture, ricevute o moduli scansionati, continua a leggere.

---

## Passo 1: Configurare l'ambiente del c# ocr tutorial

Prima di scrivere codice, assicurati di avere gli strumenti giusti:

1. **.NET 6 SDK o successivo** – puoi scaricarlo dal sito di Microsoft.  
2. **Visual Studio 2022** (la versione Community va benissimo) o qualsiasi editor tu preferisca.  
3. **Pacchetto NuGet Aspose.OCR** – esegui `dotnet add package Aspose.OCR` nella cartella del tuo progetto.

> **Suggerimento:** Se usi una pipeline CI, aggiungi il riferimento al pacchetto nel tuo file `.csproj` così la build lo ripristinerà automaticamente.

---

## Passo 2: Caricare immagine per OCR

Il primo vero passo del tutorial è prendere l'immagine che vuoi elaborare. Aspose OCR funziona con formati comuni come PNG, JPEG e TIFF.

```csharp
using Aspose.OCR;
using System.Text.Json;

// Replace this with the actual path to your invoice image
string imagePath = @"C:\Invoices\invoice.png";

// Create an OcrImage instance from the file system
OcrImage inputImage = OcrImage.FromFile(imagePath);
```

> **Perché è importante:** Caricare l'immagine come `OcrImage` fornisce al motore l'accesso ai dati bitmap e a eventuali informazioni DPI, migliorando l'accuratezza del riconoscimento. Saltare questo passaggio o fornire un file corrotto causerà un'eccezione a runtime.

---

## Passo 3: Estrarre testo da immagine

Ora eseguiamo effettivamente il motore OCR. Il metodo `Recognize` restituisce un ricco oggetto `OcrResult` contenente il testo grezzo, i punteggi di confidenza e i dettagli del layout.

```csharp
// Initialize the OCR engine – no license needed for a trial run
OcrEngine ocrEngine = new OcrEngine();

// Recognize English text (you can change the language enum if needed)
OcrResult ocrResult = ocrEngine.Recognize(inputImage, OcrLanguage.English);
```

> **Caso limite:** Se devi elaborare un documento multilingue, chiama `Recognize` due volte con valori diversi di `OcrLanguage` e concatena i risultati. Il motore è thread‑safe, quindi puoi anche parallelizzare grandi lotti.

---

## Passo 4: Serializzare l'oggetto in JSON – Formattare output JSON

L'oggetto `OcrResult` è una semplice classe C#, il che significa che possiamo passarla a `System.Text.Json`. Abilitando `WriteIndented`, l'output diventa leggibile dall'uomo.

```csharp
// Serialize the OCR result with pretty printing
string json = JsonSerializer.Serialize(ocrResult, new JsonSerializerOptions
{
    WriteIndented = true
});
```

> **Cosa ottieni:** Una stringa JSON ben indentata che include il testo riconosciuto, la confidenza e il layout della pagina. È perfetta per il logging, l'invio a un servizio web o la memorizzazione in un database NoSQL.

---

## Passo 5: Visualizzare e (facoltativamente) salvare il JSON formattato

Infine, stampiamo il JSON nella console. Puoi anche scriverlo su file con `File.WriteAllText` se preferisci.

```csharp
// Show the JSON in the console
Console.WriteLine(json);

// Optional: Save to a .json file next to the image
string jsonPath = Path.ChangeExtension(imagePath, ".json");
File.WriteAllText(jsonPath, json);
Console.WriteLine($"\nJSON saved to: {jsonPath}");
```

**Output console previsto (troncato per brevità):**

```json
{
  "Text": "Invoice #12345\nDate: 2025‑12‑01\nTotal: $250.00",
  "Confidence": 0.97,
  "Pages": [
    {
      "PageNumber": 1,
      "Blocks": [
        {
          "Text": "Invoice #12345",
          "Confidence": 0.99,
          "Rectangle": { "X": 50, "Y": 30, "Width": 200, "Height": 30 }
        }
        // …more blocks…
      ]
    }
  ]
}
```

Se il motore OCR non riesce a trovare alcun testo, il campo `Text` sarà una stringa vuota e `Confidence` sarà `0`. È un buon segnale per ricontrollare la qualità dell'immagine.

---

## Passo 6: Esempio completo funzionante

Mettendo tutto insieme, ecco il programma completo che puoi copiare‑incollare in una nuova app console:

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonResultDemo
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the source image (replace with your own path)
        string imagePath = @"C:\Invoices\invoice.png";
        OcrImage inputImage = OcrImage.FromFile(imagePath);

        // 3️⃣ Recognize text – this is the core of our c# ocr tutorial
        OcrResult ocrResult = ocrEngine.Recognize(inputImage, OcrLanguage.English);

        // 4️⃣ Serialize the result with pretty formatting
        string json = JsonSerializer.Serialize(ocrResult, new JsonSerializerOptions
        {
            WriteIndented = true
        });

        // 5️⃣ Output to console and optionally write to a file
        Console.WriteLine(json);
        string jsonPath = Path.ChangeExtension(imagePath, ".json");
        File.WriteAllText(jsonPath, json);
        Console.WriteLine($"\nJSON saved to: {jsonPath}");
    }
}
```

Esegui il programma (`dotnet run` dalla cartella del progetto) e osserva la console stampare una rappresentazione JSON ben formattata della tua fattura scansionata.

---

## Problemi comuni & consigli (c# ocr tutorial Extras)

| Problema | Perché accade | Soluzione |
|----------|----------------|-----------|
| **Campo `Text` vuoto** | Immagine a basso contrasto o ruotata. | Pre‑elabora l'immagine (aumenta contrasto, correggi inclinazione) o usa `OcrEngine.ImagePreprocess`. |
| **`System.DllNotFoundException`** | Binari nativi di Aspose OCR mancanti. | Verifica che il pacchetto NuGet sia stato ripristinato correttamente e che l'architettura runtime (x64/x86) corrisponda al tuo OS. |
| **Ritardo di prestazioni su PDF grandi** | OCR elabora ogni pagina in modo sequenziale. | Parallelizza creando istanze separate di `OcrEngine` per pagina (il motore è thread‑safe). |
| **JSON troppo grande** | Stai serializzando tutti i dettagli, inclusi i bounding box. | Usa un DTO che contenga solo `Text` e `Confidence` prima della serializzazione. |

> **Ricorda:** Lo scopo di questo tutorial è mostrare un flusso pulito, end‑to‑end. Puoi sempre ridurre il JSON o aggiungere più metadati in seguito.

---

## Conclusione

Hai appena completato un **c# ocr tutorial** che carica un'immagine, **estrae testo da immagine**, e produce un **output json formattato** **serializzando l'oggetto in json**. I passaggi sono semplici, il codice è pronto per l'esecuzione e il JSON è perfettamente indentato per il consumo a valle.

Qual è il prossimo passo? Prova a sostituire `OcrLanguage.English` con `OcrLanguage.French` o a elaborare una cartella di ricevute in un ciclo. Potresti anche esplorare il salvataggio del JSON direttamente su Azure Blob Storage o l'invio a un modello di machine‑learning.

Se incontri difficoltà, ricontrolla che il percorso dell'immagine sia corretto e che la licenza Aspose OCR (se ne possiedi una) sia caricata prima di chiamare `Recognize`. Buona programmazione, e che i risultati OCR siano sempre nitidi! 

--- 

*Image illustrating the OCR flow (alt text: "c# ocr tutorial diagram showing load image, recognize text, serialize to JSON")*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}