---
category: general
date: 2026-04-08
description: Scopri come eseguire l'OCR su un'immagine e scrivere un file JSON in
  C# usando Aspose OCR. Questo tutorial Aspose OCR C# mostra la conversione da immagine
  OCR a JSON con i valori di confidenza.
draft: false
keywords:
- perform OCR on image
- write JSON file C#
- OCR image to JSON
- Aspose OCR C# tutorial
language: it
og_description: Esegui OCR su un'immagine ed esporta i risultati in un file JSON in
  C#. Questo tutorial copre l'intero flusso di lavoro di Aspose OCR in C#, inclusi
  i punteggi di confidenza.
og_title: Esegui OCR su immagine e converti in JSON in C# – Guida OCR di Aspose
tags:
- Aspose
- OCR
- C#
- JSON
title: Esegui OCR su immagine e ottieni JSON in C# con Aspose
url: /it/net/text-recognition/perform-ocr-on-image-to-json-in-c-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esegui OCR su Immagine in JSON con C# e Aspose

Hai mai dovuto **eseguire OCR su file immagine** ma non sapevi come ottenere i risultati in un formato strutturato? Non sei solo: gli sviluppatori chiedono spesso, “Come trasformo un'immagine scansionata in dati utilizzabili?” La buona notizia è che Aspose.OCR rende tutto questo un gioco da ragazzi, e puoi persino **scrivere file JSON in C#**‑style includendo i punteggi di confidenza.

In questa guida percorreremo un **tutorial Aspose OCR C#** completo che copre tutto, dal caricamento dell’immagine all’esportazione del testo riconosciuto in JSON. Alla fine avrai un’app console eseguibile che **esegue OCR su immagine**, converte l’output in JSON (inclusi i valori di confidenza) e lo salva con una singola riga di codice. Nessun passaggio nascosto, nessuno script esterno—solo puro C#.

## Prerequisiti

Prima di iniziare, assicurati di avere:

- .NET 6.0 SDK o successivo (il codice funziona anche con .NET Core e .NET Framework)
- Visual Studio 2022 (o qualsiasi editor tu preferisca)
- Una licenza valida di **Aspose.OCR for .NET** o una licenza temporanea gratuita (la versione di prova è sufficiente per i test)
- Un file immagine (`input.png`) che desideri elaborare (qualsiasi formato comune—PNG, JPG, BMP—va bene)

Questo è tutto. Se ti manca qualcosa, procuratela ora; il resto del tutorial presuppone che sia già a posto.

## Passo 1: Installa il Pacchetto NuGet Aspose.OCR

Prima di tutto—aggiungi la libreria al tuo progetto. Apri un terminale nella cartella del progetto ed esegui:

```bash
dotnet add package Aspose.OCR
```

Questo scarica l’ultima versione (a partire da aprile 2026 è la 23.12) e aggiunge i DLL necessari nella cartella `bin`. Nessuna configurazione aggiuntiva è richiesta.

## Passo 2: Inizializza il Motore OCR (Perform OCR on Image)

Ora creiamo un’istanza di `OcrEngine` e indichiamo quale lingua utilizzare. L’inglese (`"en"`) è la più comune, ma puoi sostituirla con `"fr"`, `"de"` o qualsiasi lingua supportata.

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Path to your input image – change as needed
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        // Path where the JSON will be saved
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // Step 2: Initialize the OCR engine – this is where we **perform OCR on image**
        var ocrEngine = new OcrEngine
        {
            Language = "en"               // Set language; you can use ISO‑639‑1 codes
        };

        // Optional: tweak recognition options (speed vs. accuracy)
        // ocrEngine.RecognitionMode = RecognitionMode.LargeText; // Uncomment for large blocks
```

**Perché lo inizializziamo qui:** `OcrEngine` contiene tutta la configurazione necessaria al processo di riconoscimento. Impostare la lingua in anticipo garantisce che il motore utilizzi il set di caratteri corretto, migliorando notevolmente la precisione.

## Passo 3: Riconosci l’Immagine e Cattura la Confidenza

Con il motore pronto, gli forniamo il file immagine. Il metodo `RecognizeImage` restituisce un oggetto `OcrResult` che contiene sia il testo estratto sia un punteggio di confidenza per ogni parola.

```csharp
        // Step 3: Perform OCR on the image file
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        // Verify that the result is not null
        if (ocrResult == null)
        {
            Console.WriteLine("OCR failed – check the file path and format.");
            return;
        }

        // For debugging: print the plain text to the console
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
```

**Cosa succede dietro le quinte?** Aspose utilizza un riconoscitore basato su rete neurale che analizza ogni blocco di pixel, lo confronta con il modello linguistico e assegna un valore di confidenza (0‑100) che indica quanto è sicuro su ciascuna parola.

## Passo 4: Converti il Risultato in JSON (OCR Image to JSON)

Aspose rende la conversione indolore. Passando `includeConfidence: true` otteniamo un payload JSON che appare così:

```json
{
  "Text": "Hello world",
  "Words": [
    { "Value": "Hello", "Confidence": 97.3 },
    { "Value": "world", "Confidence": 95.8 }
  ]
}
```

Ecco il codice che genera la stringa JSON:

```csharp
        // Step 4: Convert OCR result to JSON, including confidence values
        string jsonResult = ocrResult.ToJson(includeConfidence: true);
```

**Perché includere la confidenza?** Se prevedi di inviare i dati a processi a valle (ad esempio convalida, evidenziazione UI), sapere quali parole sono incerte ti permette di decidere se chiedere conferma all’utente.

## Passo 5: Scrivi il File JSON in Stile C#

Ora **scriviamo il file JSON in C#**. Il metodo `File.WriteAllText` è atomico e funziona su più piattaforme, rendendolo perfetto per le app console.

```csharp
        // Step 5: Save the JSON output to a file
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

Questo è l’intero flusso di lavoro—cinque passaggi concisi che **eseguono OCR su immagine**, trasformano l’output in JSON e lo persistono.

## Esempio Completo Funzionante

Di seguito trovi il programma completo da copiare‑incollare in `Program.cs`. Assicurati che `input.png` si trovi nella stessa cartella dell’eseguibile compilato o modifica i percorsi di conseguenza.

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------------
        // 1️⃣ Set up file locations (feel free to change paths)
        // -------------------------------------------------------
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // -------------------------------------------------------
        // 2️⃣ Initialize the OCR engine – this is where we **perform OCR on image**
        // -------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Language = "en" // English – replace with "fr", "es", etc. as needed
        };

        // -------------------------------------------------------
        // 3️⃣ Recognize the image and obtain confidence values
        // -------------------------------------------------------
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        if (ocrResult == null)
        {
            Console.WriteLine("❌ OCR failed – verify the image path and format.");
            return;
        }

        // Show plain text (optional)
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine();

        // -------------------------------------------------------
        // 4️⃣ Convert the result to JSON – **OCR image to JSON**
        // -------------------------------------------------------
        string jsonResult = ocrResult.ToJson(includeConfidence: true);

        // -------------------------------------------------------
        // 5️⃣ Write the JSON file – **write JSON file C#** style
        // -------------------------------------------------------
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

### Output Atteso

Quando esegui il programma (`dotnet run`), vedrai qualcosa di simile:

```
=== Extracted Text ===
Hello world

✅ JSON with confidence saved to: C:\YourProject\output.json
```

E `output.json` conterrà il JSON strutturato mostrato in precedenza, completo di percentuali di confidenza per ogni parola.

## Consigli Pro & Casi Limite

- **Gestione file mancante:** Avvolgi la chiamata a `RecognizeImage` in un `try/catch` per `FileNotFoundException` se ti aspetti percorsi dinamici.
- **Lingue diverse:** Imposta `ocrEngine.Language = "fr"` per il francese, oppure carica un pacchetto lingua personalizzato con `ocrEngine.LoadLanguage("custom.lang")`.
- **Documenti di grandi dimensioni:** Per PDF multi‑pagina, converti prima ogni pagina in immagine (ad esempio con `Aspose.PDF`) e poi cicla sui passaggi OCR.
- **Ottimizzazione delle prestazioni:** Se ti servono risultati rapidi, passa a `RecognitionMode.Fast`—perdi un po’ di precisione ma guadagni velocità.
- **Formattazione JSON:** Vuoi un JSON formattato? Usa `JsonConvert.SerializeObject` di Newtonsoft con `Formatting.Indented` dopo aver deserializzato la stringa JSON di Aspose.

## Domande Frequenti

**D: Funziona con .NET Framework?**  
R: Assolutamente. Lo stesso pacchetto NuGet punta a .NET Standard 2.0, quindi può essere referenziato da .NET Framework 4.6.1 e versioni successive.

**D: E se ho bisogno della confidenza per l’intero documento, non per parola?**  
R: `OcrResult` espone anche `OverallConfidence`. Puoi aggiungerla manualmente al JSON:

```csharp
var customObj = new
{
    Text = ocrResult.Text,
    OverallConfidence = ocrResult.OverallConfidence,
    Words = ocrResult.Words
};
string json = JsonConvert.SerializeObject(customObj, Formatting.Indented);
```

**D: Posso inviare lo JSON direttamente a un’API web?**  
R: Sì. Sostituisci `File.WriteAllText` con una chiamata POST di `HttpClient` che invia `jsonResult

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}