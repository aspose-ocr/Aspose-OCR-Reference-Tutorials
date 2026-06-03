---
category: general
date: 2026-06-03
description: Esegui OCR su un'immagine ed estrai il testo dall'immagine usando Aspose.OCR.
  Scopri come rilevare parole errate e ottenere suggerimenti ortografici in una singola
  demo C#.
draft: false
keywords:
- perform OCR on image
- extract text from image
- detect misspelled words
- get spelling suggestions
- how to extract text
language: it
og_description: Esegui OCR sull'immagine per estrarre il testo dall'immagine, quindi
  rileva le parole errate e ottieni suggerimenti ortografici con Aspose.OCR in C#.
og_title: Esegui OCR su un'immagine e rileva parole errate in C#
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Perform OCR on image and extract text from image using Aspose.OCR.
    Learn how to detect misspelled words and get spelling suggestions in a single
    C# demo.
  headline: Perform OCR on Image and Detect Misspelled Words in C#
  type: TechArticle
tags:
- Aspose OCR
- C#
- Spell Checking
title: Esegui OCR su immagine e rileva parole errate in C#
url: /it/net/text-recognition/perform-ocr-on-image-and-detect-misspelled-words-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Eseguire OCR su Immagine e Rilevare Parole Sbagliate in C#

Ti sei mai chiesto come **eseguire OCR su immagine** senza impazzire? Non sei l'unico. Che tu stia digitalizzando vecchie lettere, scannerizzando ricevute o costruendo un flusso di lavoro intelligente per documenti, estrarre testo pulito dalle foto è il primo ostacolo. La buona notizia? Con Aspose.OCR puoi creare una soluzione in pochi minuti, e in più puoi anche **rilevare parole sbagliate** e **ottenere suggerimenti ortografici** nella stessa esecuzione.

In questo tutorial ti guideremo passo passo attraverso un’app console C# completa e pronta all’uso che **estrae testo da immagine**, esegue un correttore ortografico inglese e stampa ogni errore con utili idee di correzione. Alla fine saprai esattamente **come estrarre testo**, come collegare l’API di spell‑check e quale aspetto avrà l’output previsto sulla console.

## Cosa Costruirai

- Caricherai un bitmap (o PNG) che contiene errori tipografici.  
- Eseguirai Aspose.OCR per **eseguire OCR su immagine** e otterrai dati di stringa grezzi.  
- Inizializzerai il correttore ortografico inglese integrato.  
- **Rileverai parole sbagliate** e **otterrai suggerimenti ortografici** per ciascuna.  
- Stamperai un rapporto ordinato sulla console.

Nessun servizio esterno, nessuna chiamata HTTP complicata—solo un singolo pacchetto NuGet e poche righe di codice.

## Prerequisiti

- .NET 6.0 SDK o versioni successive (il codice funziona anche su .NET Framework 4.7+).  
- Visual Studio 2022 (o qualsiasi editor tu preferisca).  
- Pacchetto NuGet Aspose.OCR per .NET (`Aspose.OCR`).  
- Un file immagine (`letter_with_typos.png`) posizionato in una cartella a cui il progetto possa fare riferimento.

Se non hai mai usato Aspose, non preoccuparti—installare il pacchetto è semplice come eseguire:

```bash
dotnet add package Aspose.OCR
```

Ora immergiamoci nell’implementazione.

## Passo 1: Configurare il Progetto e Installare Aspose.OCR

Crea un nuovo progetto console e aggiungi la libreria OCR:

```bash
dotnet new console -n OcrSpellDemo
cd OcrSpellDemo
dotnet add package Aspose.OCR
```

Al termine del restore, apri `Program.cs`. Sostituiremo il contenuto predefinito con il codice demo completo più avanti, ma prima spieghiamo perché ogni spazio dei nomi è importante.

- `Aspose.OCR` – Motore OCR principale e gestione delle immagini.  
- `Aspose.OCR.SpellCheck` – Utility di correzione ortografica incluse nella libreria.  
- `System` – Classi base standard di .NET (es. `Console`).

## Passo 2: Caricare l'Immagine ed Eseguire OCR su Immagine

Il primo lavoro reale è fornire l’immagine al motore OCR. Aspose.OCR legge molti formati (PNG, JPEG, TIFF). Ecco lo snippet che fa il lavoro pesante:

```csharp
// Step 2: Load the image that contains the text to be recognized
var image = OcrImage.FromFile(@"YOUR_DIRECTORY/letter_with_typos.png");

// Step 3: Perform OCR to extract the raw text from the image
var ocrEngine = new OcrEngine();
var ocrResult = ocrEngine.Recognize(image);
```

> **Perché è importante:** `OcrImage.FromFile` astrae i dettagli a livello di pixel, mentre `OcrEngine.Recognize` esegue il modello neurale addestrato che traduce i glifi visivi in caratteri Unicode. La proprietà `ocrResult.Text` ora contiene la stringa grezza—esattamente ciò di cui hai bisogno per **estrarre testo da immagine**.

> **Consiglio professionale:** Se la tua immagine contiene più lingue, puoi impostare `ocrEngine.Language = OcrLanguage.Multilingual;` prima di chiamare `Recognize`.

## Passo 3: Inizializzare il Corretti Ortografico Inglese

Aspose.OCR fornisce un motore di correzione ortografica integrato che comprende l’inglese fin da subito. Inizializzarlo è una riga di codice:

```csharp
// Step 4: Initialise the English spell‑checker
var spellChecker = new SpellChecker(OcrLanguage.English);
```

> **Perché questo passo è cruciale:** L’output OCR può includere caratteri riconosciuti in modo errato (es. “l” vs “1”) o veri errori di battitura dal documento originale. Il correttore ortografico scannerizzerà la stringa, individuerà i token sospetti e suggerirà alternative.

## Passo 4: Rilevare Parole Sbagliate e Ottenere Suggerimenti Ortografici

Ora passiamo il testo OCR al correttore:

```csharp
// Step 5: Check the recognized text for misspelled words and obtain suggestions
var misspellings = spellChecker.Check(ocrResult.Text);
```

`misspellings` è una collezione in cui ogni voce contiene la parola errata e un array di possibili correzioni.

## Passo 5: Stampare i Risultati

Infine, iteriamo sulla collezione e stampiamo un rapporto leggibile:

```csharp
// Step 6: Output each misspelled word together with its suggested corrections
foreach (var entry in misspellings)
{
    Console.WriteLine($"Misspelled: {entry.Word}");
    Console.WriteLine("  Suggestions: " + string.Join(", ", entry.Suggestions));
}
```

### Output Atteso sulla Console

Supponendo che `letter_with_typos.png` contenga la frase:

```
Ths is an exampel of a lettter with som misspelled wrds.
```

L’esecuzione della demo produrrà qualcosa di simile a:

```
Misspelled: Ths
  Suggestions: This, Thus, The
Misspelled: exampel
  Suggestions: example, exemplar, exampell
Misspelled: lettter
  Suggestions: letter, litter, lett
Misspelled: som
  Suggestions: some, sum, son
Misspelled: wrds
  Suggestions: words, wards, wryds
```

Nota come ogni errore è accompagnato da una serie di correzioni plausibili—esattamente ciò che ti serve quando costruisci un’interfaccia utente di correzione amichevole.

## Esempio Completo Funzionante

Di seguito trovi il programma **completo, pronto da copiare e incollare**. Sostituisci `YOUR_DIRECTORY` con il percorso reale del tuo file immagine.

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System;

class SpellCheckDemo
{
    static void Main()
    {
        // Step 1: Load the image that contains the text to be recognized
        var image = OcrImage.FromFile(@"YOUR_DIRECTORY/letter_with_typos.png");

        // Step 2: Perform OCR to extract the raw text from the image
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(image);

        // Step 3: Initialise the English spell‑checker
        var spellChecker = new SpellChecker(OcrLanguage.English);

        // Step 4: Check the recognized text for misspelled words and obtain suggestions
        var misspellings = spellChecker.Check(ocrResult.Text);

        // Step 5: Output each misspelled word together with its suggested corrections
        foreach (var entry in misspellings)
        {
            Console.WriteLine($"Misspelled: {entry.Word}");
            Console.WriteLine("  Suggestions: " + string.Join(", ", entry.Suggestions));
        }

        // Optional: Keep console window open when debugging
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

> **Casi Limite da Considerare**  
> - **Immagine Vuota:** Se il motore OCR restituisce una stringa vuota, `spellChecker.Check` restituirà semplicemente una collezione vuota—nessun crash.  
> - **Testo Non Inglese:** Sostituisci `OcrLanguage.English` con `OcrLanguage.French` (o qualsiasi lingua supportata) per **rilevare parole sbagliate** in altre localizzazioni.  
> - **Documenti Grandi:** Per PDF multi‑pagina, dovresti iterare su ogni pagina, eseguire OCR, quindi aggregare i risultati prima del controllo ortografico.

## Panoramica Visiva (Testo Alternativo)

![Diagram showing the flow to perform OCR on image, extract text from image, and then detect misspelled words with spelling suggestions](perform-ocr-on-image-flow.png)

*Il diagramma sopra illustra la pipeline end‑to‑end: immagine → motore OCR → testo grezzo → correttore ortografico → suggerimenti.*

## Domande Frequenti & Consigli Pro

| Domanda | Risposta |
|----------|--------|
| **È necessaria una connessione a Internet?** | No. Aspose.OCR funziona interamente in locale; ideale per ambienti offline o sicuri. |
| **Quanto è accurato il correttore ortografico?** | Utilizza un dizionario di circa 150 000 parole inglesi e matching fuzzy, quindi la maggior parte dei typo comuni viene rilevata. |
| **Posso personalizzare il dizionario?** | Sì. `SpellChecker.AddUserDictionary("custom.txt")` ti permette di caricare termini specifici del dominio (es. nomi di prodotto). |
| **Cosa succede se l’immagine è inclinata?** | Il motore OCR rileva automaticamente l’orientamento, ma puoi chiamare manualmente `ocrEngine.ImagePreprocessing.Rotate(angle)` per i casi più ostinati. |
| **C’è un modo per evidenziare i suggerimenti nell’interfaccia?** | Dopo aver ottenuto la collezione `misspellings`, puoi mappare ogni `entry.Word` alla sua posizione in `ocrResult.Text` e sottolinearlo in un RichTextBox o in una vista web. |

## Conclusione

Ti abbiamo appena mostrato **come eseguire OCR su immagine**, **estrarre testo da immagine**, e poi **rilevare parole sbagliate** ottenendo **suggerimenti ortografici**—tutto con una concisa app console C#. L’idea di base è semplice: lascia che Aspose.OCR faccia il lavoro pesante di riconoscere i caratteri, poi usa il suo correttore ortografico integrato per pulire l’output. Da qui puoi espandere la demo in un servizio di elaborazione documenti completo, integrarlo con un’API web, o collegarlo a un editor desktop.

Pronto per il passo successivo? Prova a cambiare lingua in spagnolo, usa un PDF multi‑pagina, o costruisci un piccolo front‑end WPF che permetta agli utenti di cliccare su una parola per accettare un suggerimento. I mattoni di base sono già pronti—basta continuare a sperimentare.

Se hai incontrato difficoltà o hai idee per estensioni, lascia un commento qui sotto. Buona programmazione!

## Cosa Dovresti Imparare Dopo

I tutorial seguenti trattano argomenti strettamente correlati che approfondiscono le tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell’API e a esplorare approcci alternativi nei tuoi progetti.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image Using Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}