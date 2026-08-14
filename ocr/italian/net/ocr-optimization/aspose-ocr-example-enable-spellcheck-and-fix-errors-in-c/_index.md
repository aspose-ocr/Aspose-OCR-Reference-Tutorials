---
category: general
date: 2026-03-07
description: Esempio di Aspose OCR che mostra come abilitare il controllo ortografico,
  aggiungere un dizionario personalizzato, caricare l'OCR di un'immagine e correggere
  rapidamente gli errori OCR.
draft: false
keywords:
- aspose ocr example
- how to enable spellcheck
- how to add dictionary
- load image ocr
- how to fix ocr errors
language: it
og_description: Esempio di Aspose OCR che ti guida nell'abilitare il controllo ortografico,
  aggiungere un dizionario personalizzato, caricare un'immagine per l'OCR e correggere
  gli errori OCR comuni.
og_title: Esempio di OCR Aspose – Abilita il controllo ortografico e correggi gli
  errori
tags:
- Aspose
- OCR
- C#
- SpellCheck
title: Esempio di OCR Aspose – Abilita il controllo ortografico e correggi gli errori
  in C#
url: /it/net/ocr-optimization/aspose-ocr-example-enable-spellcheck-and-fix-errors-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esempio Aspose OCR – Abilita il Controllo Ortografico e Correggi gli Errori in C#

Hai mai avuto bisogno di un **esempio Aspose OCR** che non solo legga il testo da un'immagine ma pulisca anche quegli fastidiosi errori ortografici? Non sei l'unico. In molti progetti reali l'output grezzo dell'OCR è pieno di refusi, soprattutto quando l'immagine di origine contiene caratteri a basso contrasto o note scritte a mano.  

La buona notizia? Con Aspose.OCR puoi **abilitare il controllo ortografico**, inserire il tuo dizionario e ottenere una stringa pulita in poche righe di codice. Di seguito vedrai esattamente **come abilitare il controllo ortografico**, **come aggiungere un dizionario** e **come caricare l'OCR dell'immagine** così potrai finalmente **correggere gli errori OCR** senza impazzire.

In questo tutorial copriremo tutto ciò di cui hai bisogno—dall'installazione di NuGet a un programma completo e eseguibile che stampa il testo corretto. Alla fine avrai un solido **esempio Aspose OCR** che potrai inserire direttamente in qualsiasi progetto .NET.

## Prerequisiti

- .NET 6.0 SDK o versioni successive (il codice funziona anche con .NET Core e .NET Framework)
- Visual Studio 2022 o qualsiasi IDE compatibile con C#
- Un file immagine (`typed_text.png`) che contiene testo inglese chiaro e digitato
- Accesso a Internet per scaricare il pacchetto NuGet Aspose.OCR

Non sono richieste altre librerie di terze parti.

---

## Passo 1 – Installa il Pacchetto NuGet Aspose.OCR (Carica OCR dell'Immagine)

Prima di poter scrivere qualsiasi codice, abbiamo bisogno della libreria che alimenta il motore OCR.

```bash
dotnet add package Aspose.OCR
```

> **Consiglio:** Se stai usando Visual Studio, fai clic destro sul progetto → *Gestisci Pacchetti NuGet* → cerca **Aspose.OCR** e premi *Installa*.  

L'installazione del pacchetto ti dà accesso a `OcrEngine`, `ImageStream` e alle utility di correzione ortografica integrate che utilizzeremo più avanti. Una volta che il pacchetto è presente, sei pronto per **caricare l'OCR dell'immagine**.

## Passo 2 – Crea l'Istanza del Motore OCR

Creare il motore è il primo passo concreto in qualsiasi **esempio Aspose OCR**. Pensa a `OcrEngine` come al cervello che analizzerà il bitmap e produrrà il testo.

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

// Step 2: Initialize the OCR engine
var ocrEngine = new OcrEngine();
```

Il costruttore `OcrEngine` non richiede parametri, il che lo rende semplice e ordinato per prototipi rapidi.

## Passo 3 – Come Abilitare il Controllo Ortografico (e Perché È Importante)

L'output grezzo dell'OCR contiene spesso parole riconosciute erroneamente come “teh” invece di “the”. Abilitare il correttore ortografico integrato permette ad Aspose di sostituire automaticamente quegli errori con l'ortografia più probabile.

```csharp
// Step 3: Turn on spell checking and set the language to English
ocrEngine.Settings.SpellCheck.Enabled = true;
ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.English;
```

> **Perché abilitare il controllo ortografico?**  
> - **Precisione:** Un controllo ortografico post‑processo può aumentare la precisione complessiva del testo del 10‑15 % per documenti stampati.  
> - **Esperienza utente:** Un testo pulito significa meno pulizia a valle quando inserisci il risultato in indici di ricerca o pipeline di analisi.

## Passo 4 – Come Aggiungere un Dizionario (Parole Personalizzate)

A volte il dizionario predefinito non conosce i nomi dei tuoi brand, i codici prodotto o il gergo specifico del dominio. È qui che entra in gioco **come aggiungere un dizionario**.

```csharp
// Step 4: Add custom words that the spell checker should accept
ocrEngine.Settings.SpellCheck.CustomDictionary.AddWords(new[]
{
    "AsposeOCR",   // our library name
    "OCRify",      // a fictional product
    "CSharpify"    // another custom term
});
```

Puoi fornire un array, una lista o anche leggere da un file se hai un ampio vocabolario personalizzato. Il correttore ortografico tratterà ora quelle voci come valide, evitando correzioni errate.

## Passo 5 – Carica l'Immagine per l'OCR (Carica OCR dell'Immagine)

Ora che il motore è configurato, dobbiamo indicargli l'immagine da leggere. L'helper `ImageStream.FromFile` astrae i dettagli di lettura del file.

```csharp
// Step 5: Load the image that contains the text to be recognized
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/typed_text.png");
```

> **Suggerimento:** Se la tua immagine si trova in una sottocartella del progetto, imposta la sua proprietà *Copy to Output Directory* su *Copy always* così il percorso verrà risolto a runtime.

## Passo 6 – Esegui il Riconoscimento e Correggi gli Errori OCR

Con tutto impostato, una singola chiamata a `Recognize()` esegue la pipeline OCR, applica il controllo ortografico e memorizza il risultato pulito in `ocrEngine.Text`.

```csharp
// Step 6: Run OCR and let the spell checker clean the output
ocrEngine.Recognize();

// Step 7: Output the corrected text to the console
Console.WriteLine("Corrected text:");
Console.WriteLine(ocrEngine.Text);
```

### Output Atteso

Supponendo che `typed_text.png` contenga la frase `The quick brown fox jumps over teh lazy dog`, la console mostrerà:

```
Corrected text:
The quick brown fox jumps over the lazy dog
```

Nota come “teh” sia stato corretto automaticamente in “the”. Se avessi aggiunto “OCRify” al dizionario personalizzato e l'immagine contenesse quella parola, il motore l'avrebbe lasciata intatta.

---

## Esempio Completo Funzionante (Pronto per Copia‑Incolla)

Di seguito trovi il programma completo che puoi inserire in un nuovo progetto console. Include tutti i passaggi sopra, più alcuni commenti per chiarezza.

```csharp
// ---------------------------------------------------------------
// Aspose OCR Example – Enable Spellcheck and Fix Errors
// ---------------------------------------------------------------

using System;
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Enable spell checking (how to enable spellcheck)
            ocrEngine.Settings.SpellCheck.Enabled = true;
            ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.English;

            // 3️⃣ Add custom words (how to add dictionary)
            ocrEngine.Settings.SpellCheck.CustomDictionary.AddWords(new[]
            {
                "AsposeOCR",
                "OCRify",
                "CSharpify"
            });

            // 4️⃣ Load the image (load image OCR)
            // Replace the path with the actual location of your image file
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/typed_text.png");

            // 5️⃣ Run OCR – this also fixes common OCR errors (how to fix ocr errors)
            ocrEngine.Recognize();

            // 6️⃣ Show the corrected result
            Console.WriteLine("Corrected text:");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

Salva questo come `Program.cs`, esegui `dotnet run` e dovresti vedere la frase corretta stampata nella console.

---

## Domande Frequenti & Casi Limite

| Question | Answer |
|----------|--------|
| **E se l'immagine è un PDF multi‑pagina?** | Aspose.OCR può gestire le pagine PDF come immagini. Usa `ocrEngine.Image = ImageStream.FromPdf("file.pdf", pageNumber: 1);` e itera sulle pagine. |
| **Posso cambiare la lingua in qualcosa di diverso dall'inglese?** | Assolutamente. Imposta `ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.French;` (o qualsiasi lingua supportata). |
| **Il mio dizionario personalizzato è enorme—influirà sulle prestazioni?** | Aggiungere migliaia di parole comporta un piccolo costo iniziale, ma la ricerca è O(1) grazie a un hash‑set sotto il cofano. Per vocabolari molto grandi, considera di caricarli una sola volta all'avvio dell'applicazione. |
| **E se il motore OCR lancia un'eccezione su un'immagine corrotta?** | Avvolgi `Recognize()` in un blocco try‑catch e controlla `ocrEngine.LastError`. Puoi anche pre‑validare le dimensioni dell'immagine con `ocrEngine.Image.Width` e `Height`. |
| **Ho bisogno di una licenza per l'uso in produzione?** | La valutazione gratuita funziona per i test, ma una licenza commerciale rimuove il watermark di valutazione e sblocca le prestazioni complete. |

## Conclusione

Ora hai un **esempio completo Aspose OCR** che dimostra **come abilitare il controllo ortografico**, **come aggiungere un dizionario**, **caricare l'OCR dell'immagine** e **come correggere gli errori OCR** in modo pulito e pronto per la produzione. Configurando il correttore ortografico e fornendo un elenco di parole personalizzate, migliori drasticamente la qualità del testo estratto senza dover scrivere alcuna logica di post‑processing.

Pronto per il passo successivo? Prova a cambiare la lingua in spagnolo, carica un PDF multi‑pagina o integra l'output in un indice ricercabile di Azure Cognitive Search. Lo stesso schema si applica—basta regolare il flag della lingua e magari ampliare il dizionario personalizzato.

Se hai trovato utile questa guida, metti una stella su GitHub, condividila con i colleghi o lascia un commento qui sotto. Buona programmazione, e che i tuoi risultati OCR siano sempre privi di errori!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}