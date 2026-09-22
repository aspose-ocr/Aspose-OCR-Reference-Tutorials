---
category: general
date: 2026-02-11
description: Estrai testo da un'immagine in C# usando Aspose OCR. Scopri come caricare
  l'immagine per l'OCR, migliorare l'accuratezza dell'OCR e correggere gli errori
  di OCR con il controllo ortografico.
draft: false
keywords:
- extract text from image
- image to text c#
- improve ocr accuracy
- load image for ocr
- fix ocr errors
language: it
og_description: Estrai il testo da un'immagine in C# con Aspose OCR. Questa guida
  mostra come caricare l'immagine per l'OCR, migliorare l'accuratezza dell'OCR e correggere
  gli errori dell'OCR.
og_title: Estrai testo da immagine in C# – Guida completa all'OCR
tags:
- C#
- OCR
- Aspose
- Text Extraction
title: Estrai testo da un'immagine in C# – Guida completa all'OCR
url: /it/net/ocr-optimization/extract-text-from-image-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai testo da immagine in C# – Guida completa OCR

Hai mai avuto bisogno di **estrarre testo da immagine** ma i risultati sembravano incomprensibili? Non sei l'unico. In molte applicazioni reali — pensa alla scansione di ricevute, alla digitalizzazione di appunti o alla migrazione di documenti legacy — ottenere testo pulito da una foto è il primo, e spesso più difficile, ostacolo.

Fortunatamente, con Aspose OCR puoi **caricare immagine per OCR**, eseguire un controllo ortografico e ottenere testo ordinato e ricercabile. In questo tutorial percorreremo l'intera pipeline, dalla lettura di un JPEG alla rifinitura dell'output, e vedrai esattamente come **migliorare l'accuratezza OCR** mentre ci sei.

> **Cosa otterrai:** un programma console C# pronto all'uso che estrae testo da immagine, corregge gli errori OCR comuni e stampa sia i risultati grezzi che quelli puliti.

---

## Di cosa avrai bisogno

- .NET 6 o successivo (il codice funziona anche su .NET Framework 4.7+)
- Visual Studio 2022 (o qualsiasi IDE preferisci)
- Una chiave di prova gratuita per Aspose OCR o una versione con licenza
- Un file immagine contenente testo digitato o stampato (ad es., `typed_note.jpg`)

Non sono necessarie altre librerie di terze parti — Aspose gestisce automaticamente i modelli linguistici e il controllo ortografico.

---

## Passo 1 – Installa il pacchetto NuGet Aspose  OCR

Prima di poter **estrarre testo da immagine**, il motore OCR deve essere disponibile sulla macchina.

```powershell
# From the Package Manager Console
Install-Package Aspose.OCR
```

Oppure, se preferisci la riga di comando:

```bash
dotnet add package Aspose.OCR
```

Il pacchetto include i dati linguistici, ma impostare `AutomaticResourceDownload = true` (come faremo più avanti) garantisce che eventuali dizionari mancanti vengano scaricati a runtime.

---

## Passo 2 – Carica immagine per OCR

La prima cosa di cui il motore ha bisogno è un bitmap. Puoi fornirgli qualsiasi formato supportato da `System.Drawing.Image`, come PNG, JPEG, BMP o TIFF.

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

// Path to your source picture – change this to your own folder
string imagePath = @"C:\MyImages\typed_note.jpg";

// Load the image inside a using block so the file handle is released promptly
using (Image image = Image.FromFile(imagePath))
{
    // The rest of the OCR pipeline lives inside this block
}
```

> **Perché il blocco `using`?** Dispone automaticamente l'oggetto `Image`, evitando problemi di blocco del file che spesso colpiscono gli sviluppatori che dimenticano di rilasciare le risorse.

---

## Passo 3 – Esegui OCR – “Immagine a Testo C#” in azione

Ora effettuiamo realmente **estrarre testo da immagine**. La classe `OcrEngine` fa il lavoro pesante.

```csharp
// Step 3: Initialise the OCR engine
var ocrEngine = new OcrEngine
{
    AutomaticResourceDownload = true, // pulls language packs if missing
    Language = OcrLanguage.English    // set to your document's language
};

// Inside the using block from Step 2
var ocrResult = ocrEngine.Recognize(image);
string rawText = ocrResult.Text;
Console.WriteLine("Raw OCR output:");
Console.WriteLine(rawText);
```

A questo punto hai una stringa che rispecchia ciò che il motore vede nell'immagine. In pratica, l'output può contenere caratteri erranti, parole riconosciute in modo errato o stranezze di interruzioni di riga — da qui il passo successivo.

---

## Passo 4 – Migliora l'accuratezza OCR con il controllo ortografico

Aspose fornisce un `SpellChecker` dedicato che conosce la lingua che stai elaborando. Eseguirlo sulla stringa grezza spesso corregge gli errori più evidenti.

```csharp
// Step 4: Initialise spell‑check (resources are auto‑downloaded)
var spellChecker = new SpellChecker(OcrLanguage.English);

// Correct the OCR output
string correctedText = spellChecker.Correct(rawText);
Console.WriteLine("\nCorrected OCR output:");
Console.WriteLine(correctedText);
```

> **Consiglio pro:** Se lavori con vocabolari specifici di dominio (ad es., termini medici), puoi fornire un dizionario personalizzato a `SpellChecker` tramite i suoi overload.

---

## Passo 5 – Correggi manualmente gli errori OCR (Opzionale)

Anche il miglior correttore ortografico può perdere errori contestuali. Un rapido passaggio di post‑elaborazione può catturare cose come “l” vs “1” o “O” vs “0”.

```csharp
// Simple regex to replace common OCR confusions
string finalText = System.Text.RegularExpressions.Regex.Replace(
    correctedText,
    @"\b([lI])\b", // isolated l or I
    "1");

// Additional custom rules can be added here
Console.WriteLine("\nFinal cleaned text:");
Console.WriteLine(finalText);
```

Sentiti libero di ampliare questa sezione con le tue euristiche — magari una tabella di ricerca per codici prodotto o un elenco di acronimi noti.

---

## Esempio completo funzionante

Di seguito trovi il programma completo che puoi copiare‑incollare in un nuovo progetto Console App. Include tutti i passaggi discussi, più commenti utili.

```csharp
// ------------------------------------------------------------
// Extract Text from Image in C# – Full Example
// ------------------------------------------------------------
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure OCR engine – automatic download ensures language data is present
        var ocrEngine = new OcrEngine
        {
            AutomaticResourceDownload = true,
            Language = OcrLanguage.English
        };

        // 2️⃣ Load the image you want to analyse
        string imagePath = @"C:\MyImages\typed_note.jpg";
        using (Image image = Image.FromFile(imagePath))
        {
            // 3️⃣ Run OCR – this is where we *extract text from image*
            var ocrResult = ocrEngine.Recognize(image);
            string rawText = ocrResult.Text;
            Console.WriteLine("Before (raw OCR):");
            Console.WriteLine(rawText);
            Console.WriteLine(new string('-', 40));

            // 4️⃣ Spell‑check to *improve OCR accuracy*
            var spellChecker = new SpellChecker(OcrLanguage.English);
            string correctedText = spellChecker.Correct(rawText);
            Console.WriteLine("After (spell‑checked):");
            Console.WriteLine(correctedText);
            Console.WriteLine(new string('-', 40));

            // 5️⃣ Optional custom clean‑up – *fix OCR errors* that the spell‑checker missed
            string finalText = Regex.Replace(correctedText,
                @"\b([lI])\b", // replace isolated 'l' or 'I' with '1'
                "1");

            Console.WriteLine("Final (post‑processed):");
            Console.WriteLine(finalText);
        }
    }
}
```

### Output previsto

Assumendo che `typed_note.jpg` contenga la frase “Hello world, this is a test 123”, la console mostrerà qualcosa del genere:

```
Before (raw OCR):
H3llo w0rld, th1s is a test 123

After (spell‑checked):
Hello world, this is a test 123

Final (post‑processed):
Hello world, this is a test 123
```

Nota come il correttore ortografico ha trasformato “H3llo” in “Hello”, e la regex ha pulito il “1” errante che appariva in “th1s”.

---

## Domande frequenti e casi particolari

| Domanda | Risposta |
|----------|--------|
| **Posso usare una lingua diversa?** | Sì. Imposta `ocrEngine.Language = OcrLanguage.Spanish` (o qualsiasi enum supportato) e passa la stessa lingua a `SpellChecker`. |
| **E se la mia immagine è molto grande?** | Ridimensionala prima di passarla a OCR; `Image` dispone di `GetThumbnailImage` per un ridimensionamento rapido. |
| **Ho bisogno di una connessione internet?** | Solo la prima volta che manca un pacchetto linguistico; dopo di che le risorse sono memorizzate nella cache localmente. |
| **Come gestire PDF multi‑pagina?** | Converti ogni pagina in un'immagine (ad es., usando `PdfRenderer`) ed esegui la stessa pipeline per pagina. |
| **Il correttore ortografico è consapevole della lingua?** | Assolutamente. Usa lo stesso modello linguistico fornito al motore OCR, garantendo coerenza. |

---

## Prossimi passi e argomenti correlati

- **Elaborazione batch:** Avvolgi il codice in un ciclo `foreach` per gestire una cartella di immagini.
- **Testo scritto a mano:** Sostituisci `OcrLanguage.EnglishHandwritten` per risultati migliori su note cursive.
- **Parallelismo:** Usa `Parallel.ForEach` per accelerare carichi di lavoro grandi su macchine multi‑core.
- **Esporta in JSON/CSV:** Serializza `finalText` insieme ai metadati (nome file, punteggi di confidenza) per analisi successive.

Se sei curioso di trasformare le stringhe estratte in PDF ricercabili, dai un'occhiata alla nostra guida su **“Create searchable PDF from image in C#”**. Si basa direttamente sulla stessa pipeline OCR che abbiamo appena trattato.

---

## Conclusione

Abbiamo appena dimostrato un modo pragmatico per **estrarre testo da immagine** in C# usando Aspose OCR, mostrando anche come **caricare immagine per OCR**, **migliorare l'accuratezza OCR** e **correggere gli errori OCR** con un correttore ortografico integrato e una piccola pulizia regex. L'esempio completo funziona subito, richiede solo un singolo pacchetto NuGet e può essere esteso per adattarsi a praticamente qualsiasi scenario di digitalizzazione dei documenti

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}