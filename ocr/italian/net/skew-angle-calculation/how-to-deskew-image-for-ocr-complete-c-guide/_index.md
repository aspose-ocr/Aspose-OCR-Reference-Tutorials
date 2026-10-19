---
category: general
date: 2026-01-06
description: Impara come correggere l'inclinazione dell'immagine, rimuovere il rumore
  ed estrarre il testo con Aspose OCR. La guida passo‑passo mostra anche come caricare
  l'immagine per l'OCR.
draft: false
keywords:
- how to deskew image
- how to extract text
- how to remove noise
- recognize text from image
- load image for ocr
language: it
og_description: Scopri come correggere l'inclinazione delle immagini, rimuovere il
  rumore ed estrarre il testo con Aspose OCR. La guida passo‑passo mostra anche come
  caricare l'immagine per l'OCR.
og_title: Come correggere l'inclinazione dell'immagine per OCR – Guida completa in
  C#
tags:
- OCR
- C#
- Image Processing
title: Come raddrizzare l'immagine per OCR – Guida completa C#
url: /it/net/skew-angle-calculation/how-to-deskew-image-for-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come correggere l'inclinazione di un'immagine per OCR – Guida completa in C#

Ti sei mai chiesto **come correggere l'inclinazione di un'immagine** prima di passarla a un motore OCR? Non sei solo: la maggior parte degli sviluppatori si imbatte nello stesso ostacolo quando una foto scansionata è leggermente inclinata, rumorosa o semplicemente difficile da leggere. La buona notizia? Con Aspose OCR puoi raddrizzare, pulire e poi estrarre il testo in poche righe di C#.

In questo tutorial vedremo **come estrarre il testo**, **come rimuovere il rumore** e, naturalmente, **come correggere l'inclinazione dell'immagine** affinché i risultati OCR siano perfetti. Alla fine saprai anche **come caricare un'immagine per OCR** e otterrai stringhe pulite e ricercabili pronte per la tua applicazione.

---

## Cosa ti serve

- **Aspose.OCR per .NET** (v23.12 o successiva). Il pacchetto NuGet è `Aspose.OCR`.
- .NET 6+ (qualsiasi runtime recente va bene).
- Un'immagine di esempio inclinata o macchiata, ad es. `skewed_photo.jpg`.
- Visual Studio, Rider o il tuo editor preferito.

Nessuna libreria nativa aggiuntiva: Aspose gestisce tutto in‑processo.

---

## Passo 1 – Configura il motore OCR (Riconoscere testo da immagine)

Prima di poter **caricare un'immagine per OCR**, abbiamo bisogno di un'istanza del motore e della lingua che vogliamo leggere.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Create the OCR engine and tell it we’re reading English text.
OcrEngine ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English
};
```

**Perché è importante:** `OcrEngine` è il cuore del processo. Impostare `Language` fin da subito garantisce che l'algoritmo di riconoscimento utilizzi il set di caratteri corretto, migliorando drasticamente l'accuratezza.

---

## Passo 2 – Carica la tua immagine (Caricare immagine per OCR)

Ora puntiamo il motore al file sul disco. Questo è il momento in cui molti tutorial si fermano, ma noi parleremo anche delle insidie più comuni.

```csharp
// Load the image you want to process.
ocrEngine.Image = ImageStream.FromFile(@"C:\Images\skewed_photo.jpg");
```

> **Consiglio pratico:** Usa un percorso assoluto durante i test, poi passa a un percorso relativo o a una risorsa incorporata per la produzione. Inoltre, assicurati che l'immagine sia in un formato supportato (JPEG, PNG, BMP, TIFF). Se ricevi un errore “Unsupported format”, ricontrolla l'estensione del file e il tipo MIME.

---

## Passo 3 – Pre‑processo: Correggi l'inclinazione e rimuovi i punti (Come correggere l'inclinazione dell'immagine & Come rimuovere il rumore)

Un documento inclinato è un classico incubo per l'OCR. Aspose offre un `DeskewFilter` che rileva automaticamente la rotazione fino a un angolo configurabile. Abbinalo a `DespeckleFilter` per pulire il rumore sale‑e‑pepe.

```csharp
// 1️⃣ Deskew – correct rotation up to 15° (adjust as needed)
ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 15 });

// 2️⃣ Despeckle – reduce noise; Strength 1‑5 (3 is moderate)
ocrEngine.Filters.Add(new DespeckleFilter { Strength = 3 });
```

### Come funziona il Deskew Filter
Il filtro analizza l'immagine alla ricerca delle linee di base del testo predominanti, calcola l'angolo di inclinazione e ruota il bitmap di conseguenza. Se l'immagine è già livellata, il filtro non fa nulla—quindi puoi aggiungerlo in sicurezza a qualsiasi pipeline.

### Come aiuta il Despeckle Filter
Il rumore appare spesso come pixel scuri o chiari isolati. L'algoritmo di despeckle applica un filtro mediano, preservando i bordi (come i tratti dei caratteri) mentre smussa i granelli. Troppa intensità può sfocare i dettagli fini, quindi inizia con `Strength = 3` e regola in base al materiale di partenza.

> **Nota a margine:** Se le tue immagini hanno una rotazione estrema (>15°), aumenta `MaxAngle`. Per documenti scansionati capovolti, potresti aver bisogno di un passaggio di rotazione personalizzato prima del filtro di correzione dell'inclinazione.

---

## Passo 4 – Esegui il riconoscimento (Riconoscere testo da immagine)

Con il pre‑processo pronto, chiediamo finalmente al motore di leggere il testo.

```csharp
if (ocrEngine.Recognize())
{
    // The recognized text is now stored in ocrEngine.Text
    Console.WriteLine("=== Extracted Text ===");
    Console.WriteLine(ocrEngine.Text);
}
else
{
    Console.WriteLine("Recognition failed – check the image quality.");
}
```

### Cosa succede dietro le quinte?
1. **Binarizzazione:** Converte l'immagine in bianco‑e‑nero, aumentando il contrasto.
2. **Segmentazione:** Divide il bitmap in linee, parole e caratteri.
3. **Classificazione:** Confronta ogni carattere con un modello addestrato (alfabeto inglese, cifre, punteggiatura).
4. **Post‑processing:** Applica regole linguistiche (ad es. correzione ortografica) per migliorare la leggibilità.

Poiché abbiamo già **corretto l'inclinazione dell'immagine** e **rimosso il rumore**, ciascuna di queste fasi riceve dati più puliti, il che si traduce in meno errori di riconoscimento.

---

## Passo 5 – Verifica e pulisci l'output (Come estrarre il testo in modo efficace)

La stringa grezza può contenere interruzioni di riga indesiderate o spazi extra. Una rapida pulizia rende i dati pronti per l'elaborazione successiva.

```csharp
string raw = ocrEngine.Text;

// Trim leading/trailing whitespace and collapse multiple newlines.
string cleaned = System.Text.RegularExpressions.Regex
    .Replace(raw, @"\s+", " ")
    .Trim();

Console.WriteLine("\n=== Cleaned Text ===");
Console.WriteLine(cleaned);
```

**Perché pulirla?** Molte librerie OCR preservano il layout originale, il che è ottimo per i PDF ma rumoroso per le pipeline di testo semplice. Normalizzare gli spazi assicura che tu possa memorizzare il risultato in un database o inviarlo a un indice di ricerca senza ulteriori lavori.

---

## Esempio completo funzionante

Di seguito trovi il programma completo, pronto per il copia‑incolla, che unisce tutti i passaggi. Salvalo come `Program.cs`, aggiungi il pacchetto NuGet Aspose.OCR e avvialo.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English
        };

        // 2️⃣ Load the image you want to process
        //    (this demonstrates how to load image for OCR)
        ocrEngine.Image = ImageStream.FromFile(@"C:\Images\skewed_photo.jpg");

        // 3️⃣ Add preprocessing filters
        //    - Deskew up to 15° (how to deskew image)
        //    - Despeckle with moderate strength (how to remove noise)
        ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 15 });
        ocrEngine.Filters.Add(new DespeckleFilter { Strength = 3 });

        // 4️⃣ Perform recognition (recognize text from image)
        if (ocrEngine.Recognize())
        {
            // 5️⃣ Output raw and cleaned text (how to extract text)
            Console.WriteLine("=== Raw OCR Output ===");
            Console.WriteLine(ocrEngine.Text);

            string cleaned = System.Text.RegularExpressions.Regex
                .Replace(ocrEngine.Text, @"\s+", " ")
                .Trim();

            Console.WriteLine("\n=== Cleaned OCR Output ===");
            Console.WriteLine(cleaned);
        }
        else
        {
            Console.WriteLine("OCR failed – verify the image path and quality.");
        }
    }
}
```

**Output previsto** (supponendo che l'immagine di esempio contenga la frase “Hello World”):

```
=== Raw OCR Output ===
Hello World

=== Cleaned OCR Output ===
Hello World
```

Se l'immagine è fortemente inclinata, noterai che l'output grezzo contiene caratteri distorti prima di aggiungere il `DeskewFilter`. Dopo il filtro, il testo diventa leggibile—esattamente ciò che volevamo ottenere.

---

## Domande frequenti & casi particolari

| Domanda | Risposta |
|----------|--------|
| *Cosa fare se la mia immagine è ruotata più di 15°?* | Aumenta `MaxAngle` in `DeskewFilter`. Valori fino a 45° sono sicuri, ma angoli estremi potrebbero richiedere una rotazione manuale prima (`Image.Rotate(angle)`). |
| *Il mio OCR continua a perdere lettere dopo il despeckle.* | Prova una `Strength` più alta (4‑5) o aggiungi un `ContrastFilter` prima del despeckle. |
| *Posso elaborare direttamente i PDF?* | Sì—usa `PdfDocument` per renderizzare ogni pagina in un'immagine, poi passa ogni bitmap alla stessa pipeline. |
| *Il motore è thread‑safe?* | Crea un `OcrEngine` separato per ogni thread; la classe di per sé non garantisce la thread‑safety. |
| *Come gestire documenti multilingua?* | Imposta `ocrEngine.Language = OcrLanguage.Multilingual` o cambia lingua per pagina. |

---

## Consigli per un OCR pronto per la produzione

1. **Elaborazione batch:** Scorri una cartella di immagini, riutilizzando la stessa istanza di `OcrEngine` per ridurre l'overhead.
2. **Logging:** Controlla `ocrEngine.LastError` quando `Recognize()` restituisce false; spesso indica formati non supportati o file corrotti.
3. **Performance:** Il passaggio di correzione dell'inclinazione è il più dispendioso in CPU. Se sai che le tue immagini sono già livellate, puoi omettere il filtro.
4. **Gestione della memoria:** Dispone degli oggetti `ImageStream` dopo l'uso (`ocrEngine.Image.Dispose()`) per evitare perdite di memoria in servizi a lungo termine.

---

## Conclusione

Abbiamo coperto **come correggere l'inclinazione di un'immagine**, **come rimuovere il rumore**, **come caricare un'immagine per OCR** e **come estrarre il testo** usando Aspose OCR in C#. Pre‑processando con `DeskewFilter` e `DespeckleFilter`, migliori notevolmente le probabilità che `Recognize()` restituisca stringhe pulite e ricercabili.

Dalla prima riga di codice all'output finale pulito, i passaggi sono semplici ma sufficientemente potenti per scenari reali—che tu stia costruendo un servizio di archiviazione documenti, un'app mobile per la scansione di ricevute o un backend di elaborazione batch.

Pronto per la prossima sfida? Prova ad aggiungere un **passo di rilevamento della lingua**, o sperimenta con **dizionari OCR personalizzati** per aumentare l'accuratezza su vocabolari specifici di settore. Il cielo è il limite, e ora hai una solida base su cui costruire.

Buona programmazione, e che le tue immagini siano sempre perfettamente dritte! 

![Illustration of a corrected document after deskewing](deskewed_example.png "how to deskew image")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}