---
category: general
date: 2026-03-04
description: Impara a raddrizzare l'immagine e a riconoscere il testo dall'immagine
  con regolazioni del contrasto per migliorare l'accuratezza dell'OCR e ottimizzare
  l'immagine per l'OCR.
draft: false
keywords:
- how to deskew image
- recognize text from image
- how to apply contrast
- improve OCR accuracy
- enhance image for OCR
language: it
og_description: Come correggere l'inclinazione di un'immagine e migliorare i risultati
  OCR. Impara ad applicare il contrasto, aumentare la precisione OCR e riconoscere
  il testo da un'immagine con pipeline riutilizzabili.
og_title: Come raddrizzare un'immagine – Tutorial completo OCR in C#
tags:
- OCR
- C#
- image‑processing
title: Come raddrizzare l'immagine per OCR – Guida passo‑passo C#
url: /it/net/ocr-optimization/how-to-deskew-image-for-ocr-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come correggere l'inclinazione di un'immagine – Tutorial completo OCR in C#

Ti sei mai chiesto **come correggere l'inclinazione di un'immagine** affinché il tuo motore OCR legga realmente il testo? Non sei l'unico. In molti progetti reali—ricevute scannerizzate, contratti fotografati o ricevute sfocate scattate con la fotocamera del telefono—l'immagine non è perfettamente verticale. Una pagina inclinata confonde il riconoscitore di caratteri e il risultato è un mucchio di nonsense.

La buona notizia? Correggendo l'inclinazione dell'immagine **e** regolando il contrasto puoi migliorare notevolmente **l'accuratezza OCR**. In questo tutorial vedremo un esempio completo in C# che mostra esattamente come **riconoscere il testo da un'immagine** dopo aver applicato un filtro di correzione dell'inclinazione e un potenziamento del contrasto. Spiegheremo anche **come applicare il contrasto** nel modo corretto, discuteremo i casi limite e ti forniremo una pipeline riutilizzabile da inserire in qualsiasi progetto.

## Cosa otterrai da questa guida

- Una spiegazione chiara del perché la correzione dell'inclinazione e il contrasto sono importanti per l'OCR.
- Un esempio di codice C# pronto all'uso che costruisce una pipeline di filtri, la collega a un motore OCR e legge più immagini.
- Suggerimenti su come riutilizzare la stessa pipeline per molti file, gestire i casi di errore e misurare il miglioramento di accuratezza.
- Link a argomenti correlati come binarizzazione dell'immagine, rimozione del rumore e OCR multilingua (tutto senza lasciare la pagina).

**Prerequisiti** – è necessario un ambiente .NET 6+ , una libreria OCR che supporti una pipeline di filtri (ad es. Tesseract‑.NET, IronOCR o qualsiasi SDK commerciale) e un paio di PNG di esempio. Nessun servizio esterno richiesto.

---

## Passo 1 – Perché la correzione dell'inclinazione è la prima cosa da fare

Quando una pagina scannerizzata è ruotata anche solo di pochi gradi, il motore OCR vede la linea di base di ogni riga inclinata. La maggior parte dei riconoscitori assume testo orizzontale; qualsiasi deviazione riduce i punteggi di confidenza e introduce errori di sostituzione.

> **Consiglio esperto:** Se possibile, cattura l'immagine su una superficie piana e con buona illuminazione; le correzioni software non possono sostituire dati di buona qualità.

In termini di codice, “come correggere l'inclinazione di un'immagine” di solito significa rilevare l'orientamento dominante delle linee di testo e ruotare il bitmap a 0°. La maggior parte degli SDK OCR espone un `DeskewFilter` che lo fa automaticamente.

```csharp
// Create a deskew filter – it analyses the image and rotates it back.
var deskew = new DeskewFilter();
```

Il filtro parte dal presupposto che la pagina contenga più testo che sfondo, cosa vera per la maggior parte dei documenti. Se hai una foto con molto spazio bianco, potresti aver bisogno di un algoritmo di fallback—ma per la maggior parte dei PDF scannerizzati il valore predefinito funziona bene.

---

## Passo 2 – Aumentare il contrasto per far risaltare i caratteri

Il contrasto è la differenza tra i pixel più scuri e quelli più chiari. Scansioni a basso contrasto appaiono sbiadite e il motore OCR non riesce a capire dove inizia o finisce un carattere. Incrementando il contrasto “affiniamo” la separazione visiva, il che **migliora l'accuratezza OCR**.

```csharp
// Set the contrast level – 1.0 is neutral, >1.0 brightens the darks and whites.
var contrast = new ContrastFilter { Level = 1.2 };
```

Perché 1.2? In pratica un aumento moderato (10‑30 %) è sufficiente. Spingerlo troppo oltre fa perdere dettagli sottili, soprattutto su font sottili. Sentiti libero di sperimentare; la pipeline che costruiremo più avanti ti permette di regolare il livello senza ricompilare l'intera app.

---

## Passo 3 – Costruire una pipeline di filtri riutilizzabile

Ora combiniamo i due filtri in un'unica pipeline. In questo modo **riconosci il testo da un'immagine** con lo stesso preprocessing ogni volta, garantendo risultati coerenti.

```csharp
using YourOcrLibrary;          // Replace with the actual namespace of your OCR SDK
using YourOcrLibrary.Filters; // Namespace where DeskewFilter & ContrastFilter live

// Step 3: Build a filter pipeline that deskews the image and enhances contrast
var filterPipeline = new FilterBuilder()
    .Add(new DeskewFilter())                 // First: straighten the page
    .Add(new ContrastFilter { Level = 1.2 }) // Then: make the text pop
    .Build();
```

**Perché una pipeline?**  
- **Modularità:** aggiungi o rimuovi filtri senza toccare la chiamata OCR.  
- **Prestazioni:** la libreria può batchare le operazioni, riducendo il churn di memoria.  
- **Riutilizzabilità:** collega la stessa pipeline a più chiamate `engine.Recognize`.

---

## Passo 4 – Collegare la pipeline al motore OCR

La maggior parte dei motori OCR espone una proprietà `Filters` o un metodo `SetFilters`. Assegnando qui la nostra pipeline, ogni immagine successiva passa attraverso correzione dell'inclinazione + contrastò prima che inizi l'analisi dei caratteri.

```csharp
// Step 4: Attach the pipeline to the OCR engine so it processes images using these filters
var engine = new OcrEngine(); // Instantiate your OCR engine (configure language, etc.)
engine.Filters = filterPipeline;
```

Se devi cambiare il modello linguistico (ad es. Inglese → Spagnolo) puoi farlo **prima** di collegare i filtri; l'ordine non importa per la fase di preprocessing.

---

## Passo 5 – Riconoscere il testo dalla prima immagine

Mettiamo la pipeline al lavoro. Carichiamo un PNG, eseguiamo l'OCR e stampiamo il risultato. Nota come utilizziamo la stessa istanza `engine`—non è necessario ricostruire i filtri.

```csharp
// Step 5: Recognize text from the first image using the configured engine
var firstImagePath = @"C:\Images\doc1.png";
var firstResult = engine.Recognize(ImageInfo.Load(firstImagePath));

Console.WriteLine("=== First Document ===");
Console.WriteLine(firstResult.Text);
```

**Cosa dovresti vedere:** testo pulito, correttamente orientato e con molti meno caratteri confusi rispetto a una scansione grezza. Se noti ancora errori, considera di aggiungere un `BinarizeFilter` (conversione in bianco‑nero puro) dopo il passaggio di contrasto.

---

## Passo 6 – Riutilizzare la stessa pipeline per file aggiuntivi

Uno dei maggiori vantaggi di una pipeline di filtri è che puoi riutilizzarla su decine di file senza overhead aggiuntivo.

```csharp
// Step 6: Recognize text from a second image to demonstrate reuse of the same pipeline
var secondImagePath = @"C:\Images\doc2.png";
var secondResult = engine.Recognize(ImageInfo.Load(secondImagePath));

Console.WriteLine("\n=== Second Document ===");
Console.WriteLine(secondResult.Text);
```

Se hai una cartella piena di PDF scannerizzati, basta iterare su `Directory.GetFiles(...)` e chiamare `engine.Recognize` ogni volta. I passaggi di correzione dell'inclinazione e contrasto rimangono coerenti, il che è fondamentale per **migliorare l'immagine per l'OCR** in lavori batch.

---

## Esempio completo – Metti tutto insieme

Di seguito trovi il programma completo e autonomo. Copialo‑incollalo in un nuovo progetto console, aggiungi il pacchetto NuGet appropriato per il tuo SDK OCR e avvialo. Restituirà il testo riconosciuto per due immagini di esempio.

```csharp
// ------------------------------------------------------------
// Complete C# OCR Example – Deskew + Contrast Pipeline
// ------------------------------------------------------------
using System;
using System.IO;
using YourOcrLibrary;          // e.g., IronOcr, Tesseract.NET, etc.
using YourOcrLibrary.Filters; // Filters live here

class Program
{
    static void Main()
    {
        // 1️⃣ Build the filter pipeline (deskew + contrast)
        var filterPipeline = new FilterBuilder()
            .Add(new DeskewFilter())                 // Straighten the page
            .Add(new ContrastFilter { Level = 1.2 }) // Boost contrast a bit
            .Build();

        // 2️⃣ Create and configure the OCR engine
        var engine = new OcrEngine
        {
            // Example: set language to English (adjust as needed)
            Language = OcrLanguage.English,
            Filters = filterPipeline
        };

        // 3️⃣ Define image paths (replace with your own)
        string[] imagePaths = {
            @"C:\Images\doc1.png",
            @"C:\Images\doc2.png"
        };

        // 4️⃣ Process each image
        foreach (var path in imagePaths)
        {
            if (!File.Exists(path))
            {
                Console.WriteLine($"⚠️ File not found: {path}");
                continue;
            }

            var result = engine.Recognize(ImageInfo.Load(path));

            Console.WriteLine($"\n=== {Path.GetFileName(path)} ===");
            Console.WriteLine(result.Text);
        }

        Console.WriteLine("\n✅ All done – you have successfully deskewed and enhanced contrast for OCR!");
    }
}
```

### Output previsto

```
=== doc1.png ===
Invoice #12345
Date: 2024‑02‑15
Total: $1,250.00
...

=== doc2.png ===
Meeting Minutes
1. Project kickoff...
2. Budget approval...
...
```

Se confronti questo output con un'esecuzione **senza** la pipeline di filtri, noterai probabilmente caratteri mancanti, numeri fuori posto o linee completamente confuse. Questo è l'impatto misurabile dell'apprendere **come correggere l'inclinazione di un'immagine** e **come applicare il contrasto** correttamente.

---

## Domande frequenti & casi limite

| Domanda | Risposta |
|----------|--------|
| *E se l'immagine è già dritta?* | Il `DeskewFilter` rileva una rotazione di 0° e restituisce il bitmap originale, quindi praticamente non c'è overhead. |
| *Posso usarlo con i PDF?* | Sì. La maggior parte degli SDK OCR ti permette di caricare una pagina PDF come `ImageInfo`. La stessa pipeline funziona perché il bitmap sottostante viene processato allo stesso modo. |
| *I miei documenti hanno testo colorato—il contrasto rovinerà i colori?* | Il filtro di contrasto agisce sulla luminanza, quindi i colori vengono preservati ma diventano più distinguibili. Se ti serve un bianco‑nero puro, aggiungi un `BinarizeFilter` dopo il passaggio di contrasto. |
| *Come misuro il miglioramento di accuratezza?* | Esegui l'OCR su un set di test prima e dopo la pipeline, poi calcola il tasso di errore dei caratteri (CER) o delle parole (WER). Di solito si osserva una riduzione degli errori del 10‑30 %. |
| *C'è un impatto sulle prestazioni?* | La correzione dell'inclinazione aggiunge un piccolo costo CPU (di solito < 100 ms per pagina). Il contrasto è un'operazione pixel‑wise semplice, quindi l'impatto complessivo è minimo rispetto al passo OCR stesso. |

---

## Prossimi passi – Porta il tuo OCR al livello successivo

Ora che sai **come correggere l'inclinazione di un'immagine**, **come applicare il contrasto** e come **riconoscere il testo da un'immagine** con una pipeline riutilizzabile, considera di approfondire questi argomenti correlati:

- **Riduzione del rumore** – aggiungi un `MedianFilter` prima della correzione dell'inclinazione per pulire i granelli.  
- **Binarizzazione** – converti in bianco‑nero puro per lingue con script complessi.  
- **Elaborazione multipagina** – itera sulle pagine PDF e archivia i risultati in un indice ricercabile.  
- **Modelli linguistici** – passa da `OcrLanguage.English` a `OcrLanguage.French` al volo.  
- **Post‑processing** – usa il controllo ortografico o regex per correggere letture OCR comuni (es. “0” vs “O”).

Ognuno di questi può essere inserito nella stessa catena `FilterBuilder`, offrendoti una soluzione modulare e manutenibile che **migliora l'immagine per l'OCR** in qualsiasi pipeline di produzione.

---

## Conclusione

Abbiamo coperto tutto ciò che devi sapere su **come correggere l'inclinazione di un'immagine** per l'OCR, perché regolare il contrasto è un modo economico ma potente per **migliorare l'accuratezza OCR**, e come **riconoscere il testo da un'immagine** usando una pipeline pulita e riutilizzabile.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}