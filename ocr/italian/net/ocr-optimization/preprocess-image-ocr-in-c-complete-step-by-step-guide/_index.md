---
category: general
date: 2026-02-20
description: Preprocessare l'OCR delle immagini con Aspose.OCR in C#. Scopri come
  applicare il filtro mediano, ridurre il rumore dell'immagine e estrarre il testo
  dall'immagine in modo efficiente.
draft: false
keywords:
- preprocess image OCR
- apply median filter
- extract text image
- reduce image noise
- c# ocr example
language: it
og_description: Preprocessa l'OCR delle immagini con Aspose.OCR. Questo tutorial mostra
  come applicare il filtro mediano, ridurre il rumore dell'immagine ed estrarre il
  testo dall'immagine usando C#.
og_title: Preprocessare l'OCR delle immagini in C# – Guida completa
tags:
- OCR
- C#
- Image Processing
title: Preprocessare l'OCR delle Immagini in C# – Guida Completa Passo‑Passo
url: /it/net/ocr-optimization/preprocess-image-ocr-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Preprocessare l'OCR di Immagini in C# – Guida Completa Passo‑Passo

Ti è mai capitato di dover **preprocessare l'OCR di immagini** perché le tue foto scansionate restituiscono testo incomprensibile? Non sei solo. In molti progetti reali—pensiamo a ricevute, carte d'identità o appunti scritti a mano—l'immagine grezza raramente è pronta per il riconoscimento immediato. La buona notizia? Alcuni semplici passaggi di preprocessing possono aumentare drasticamente l'accuratezza, e puoi fare tutto in C# con Aspose.OCR.

In questo tutorial percorreremo un esempio pratico che mostra come **applicare il filtro mediano**, **ridurre il rumore dell'immagine**, e infine **estrarre il testo dall'immagine** con un risultato pulito e leggibile. Alla fine avrai un'app console C# completamente eseguibile che potrai inserire in qualsiasi soluzione .NET. Nessun riferimento vago, solo il codice di cui hai bisogno e il “perché” dietro ogni riga.

---

## Cosa Ti Serve

- **Aspose.OCR per .NET** (ultima versione al momento della scrittura, 23.12). Puoi ottenerlo via NuGet: `Install-Package Aspose.OCR`.
- .NET 6.0 o successivo (l'esempio utilizza un'app console, ma la stessa logica funziona in ASP.NET, WPF, ecc.).
- Un'immagine di esempio che necessita di pulizia—ad esempio `skewed_photo.jpg`.  
- Una discreta esperienza in C#; i concetti sono semplici anche per sviluppatori junior.

> **Suggerimento professionale:** Se stai usando una macchina aziendale, assicurati che il tuo feed NuGet sia configurato per consentire pacchetti esterni, altrimenti l'installazione fallirà.

---

## Passo 1 – Creare l'Istanza del Motore OCR  

La prima cosa da fare è istanziare un `OcrEngine`. Questo oggetto contiene le impostazioni di riconoscimento e in seguito elaborerà il bitmap pre‑processato.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System.Drawing;   // For Image handling
using System;

class PreprocessExample
{
    static void Main()
    {
        // Initialize the OCR engine – this is the core component that will read text.
        OcrEngine ocrEngine = new OcrEngine();

        // ... we’ll continue with loading and preprocessing the image below.
```

**Perché?**  
Creare il motore una sola volta e riutilizzarlo su più immagini riduce l'overhead. Inoltre ti permette di modificare lingua o modalità di riconoscimento in seguito senza ricostruire l'intera pipeline.

---

## Passo 2 – Caricare l'Immagine Sorgente  

Hai bisogno di un oggetto `System.Drawing.Image` che punti al tuo file grezzo. In un progetto reale potresti accettare uno stream, ma per chiarezza leggeremo dal disco.

```csharp
        // Load the image that requires preprocessing.
        Image sourceImage = Image.FromFile("YOUR_DIRECTORY/skewed_photo.jpg");
```

> **Nota:** Sostituisci `YOUR_DIRECTORY` con il percorso reale della cartella. Se il file non viene trovato, verrà sollevata una `FileNotFoundException`—catturala se desideri una gestione degli errori più elegante.

---

## Passo 3 – Correggere l'Inclinazione e Ruotare l'Immagine  

La maggior parte dei documenti scansionati è leggermente inclinata. Il filtro `DeskewAndRotate` rileva automaticamente l'angolo di inclinazione e ruota l'immagine in orientamento verticale.

```csharp
        // Correct orientation – crucial for accurate OCR.
        Image processedImage = sourceImage.Apply(Preprocess.DeskewAndRotate());
```

**Perché è importante?**  
I motori OCR presumono che le linee di testo siano orizzontali. Anche una inclinazione di 2 gradi può ridurre l'accuratezza del riconoscimento del 15‑20 %. Correggere l'inclinazione è il modo più semplice per ottenere un grande miglioramento.

---

## Passo 4 – Applicare il Filtro Mediano per Ridurre il Rumore dell'Immagine  

Il rumore appare come macchie o pixel casuali, specialmente in foto con scarsa illuminazione. Un filtro mediano li smussa mantenendo i bordi, esattamente ciò di cui abbiamo bisogno prima dell'OCR.

```csharp
        // Reduce noise – radius of 2 is a good balance for most photos.
        processedImage = processedImage.Apply(Preprocess.MedianFilter(radius: 2));
```

**Perché un filtro mediano?**  
A differenza di un filtro medio (average), il filtro mediano sostituisce ogni pixel con il valore mediano del suo intorno. Questo significa che il rumore isolato viene eliminato senza sfocare i tratti del testo—una tecnica classica per **ridurre il rumore dell'immagine**.

---

## Passo 5 – Aumentare il Contrasto con lo Stretching  

Dopo la rimozione del rumore, il passo successivo è aumentare la differenza tra testo e sfondo. Lo stretching del contrasto distribuisce le intensità dei pixel sull'intero intervallo 0‑255.

```csharp
        // Stretch contrast to make dark text pop against a light background.
        processedImage = processedImage.Apply(Preprocess.ContrastStretch());
```

**Perché fare lo stretch?**  
I motori OCR si basano su una chiara separazione primo piano‑sfondo. Se l'immagine è sbiadita, il motore può interpretare il testo come sfondo. Lo stretching del contrasto risolve il problema senza dover impostare manualmente una soglia.

---

## Passo 6 – Eseguire l'OCR sull'Immagine Preprocessata  

Ora che l'immagine è dritta, pulita e ad alto contrasto, la passiamo al motore OCR.

```csharp
        // Recognize the text from the cleaned image.
        string extractedText = ocrEngine.Recognize(processedImage);
```

**Cosa ottieni:**  
`extractedText` contiene la stringa Unicode grezza rilevata da Aspose.OCR. Puoi ulteriormente post‑processarla (trim, regex, ecc.) se necessario.

---

## Passo 7 – Restituire il Testo Riconosciuto  

Infine, scrivi il risultato sulla console o su un file—qualunque cosa si adatti al tuo flusso di lavoro.

```csharp
        // Show the result in the console.
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(extractedText);
    }
}
```

### Output Atteso

Se `skewed_photo.jpg` contiene la frase “Hello World”, vedrai qualcosa di simile:

```
=== Extracted Text ===
Hello World
```

Se l'immagine è ancora rumorosa, potresti notare caratteri incomprensibili—torna al Passo 4 e aumenta il raggio del filtro mediano, oppure sperimenta filtri aggiuntivi come `GaussianBlur`.

---

## Esempio Completo Funzionante (Pronto per Copia‑Incolla)

Di seguito trovi l'intero programma, pronto per la compilazione. Nessun pezzo mancante—basta sostituire il percorso del file.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System.Drawing;
using System;

class PreprocessExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the source image that needs preprocessing
        Image sourceImage = Image.FromFile("YOUR_DIRECTORY/skewed_photo.jpg");

        // Step 3: Deskew and rotate the image to correct orientation
        Image processedImage = sourceImage.Apply(Preprocess.DeskewAndRotate());

        // Step 4: Reduce noise with a median filter (radius = 2)
        processedImage = processedImage.Apply(Preprocess.MedianFilter(radius: 2));

        // Step 5: Enhance contrast using contrast stretching
        processedImage = processedImage.Apply(Preprocess.ContrastStretch());

        // Step 6: Perform OCR on the preprocessed image
        string extractedText = ocrEngine.Recognize(processedImage);

        // Step 7: Output the recognized text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(extractedText);
    }
}
```

> **Suggerimento per casi limite:** Se la tua immagine contiene testo colorato su uno sfondo colorato, considera di convertirla in scala di grigi prima di applicare `ContrastStretch`. Puoi farlo con `Preprocess.Grayscale()` nella pipeline.

---

## Domande Frequenti e Varianti  

### Cosa fare se l'immagine è capovolta?

`DeskewAndRotate` rileva automaticamente rotazioni di 180 gradi, ma puoi forzare una rotazione con `Preprocess.Rotate(angle: 180)` prima della correzione dell'inclinazione.

### Posso saltare il filtro mediano?

Sì, ma probabilmente vedrai diminuire i benefici di **ridurre il rumore dell'immagine**. In scansioni ad alta risoluzione, il filtro può essere superfluo; in foto telefoniche con scarsa illuminazione, è solitamente indispensabile.

### In che modo questo differisce da un semplice `Apply(Preprocess.Binarize())`?

La binarizzazione converte l'immagine in puro bianco e nero, il che può risultare duro per caratteri sottili. Il nostro approccio mantiene i dettagli in scala di grigi, poi effettua lo stretching del contrasto—spesso produce risultati migliori per caratteri di dimensioni miste.

### Esiste un modo per **applicare il filtro mediano** solo a una regione di interesse?

`Apply` di Aspose.OCR funziona sull'intero bitmap, ma puoi ritagliare prima l'immagine (`sourceImage.Clone(new Rectangle(...), sourceImage.PixelFormat)`) e poi applicare il filtro a quella sotto‑immagine.

---

## Prossimi Passi – Oltre il Preprocessamento Base  

- **Language Packs:** Se hai bisogno di estrarre caratteri francesi o giapponesi, carica il modello linguistico appropriato tramite `ocrEngine.Language = Language.French;`.
- **Custom Thresholding:** Per scansioni a contrasto estremamente basso, sperimenta `Preprocess.AdaptiveThreshold()` dopo il filtro mediano.
- **Batch Processing:** Avvolgi i passaggi all'interno di un ciclo `foreach (string file in Directory.GetFiles(...))` e scrivi ogni risultato in un file `.txt`.  
- **Performance Tuning:** Riutilizza una singola istanza di `OcrEngine` e pre‑alloca un buffer `Bitmap` per evitare picchi di GC durante l'elaborazione di migliaia di immagini.

---

## Conclusione  

Abbiamo appena mostrato come **preprocessare l'OCR di immagini** in C# dall'inizio alla fine: caricare l'immagine, correggere l'inclinazione, **applicare il filtro mediano**, aumentare il contrasto e infine **estrarre il testo dall'immagine** con Aspose.OCR. Lo snippet di codice completo è pronto per essere inserito in qualsiasi progetto, e le spiegazioni ti forniscono il “perché” dietro ogni trasformazione—così potrai regolare i parametri per i tuoi casi particolari.

Provalo con alcune foto diverse, gioca con il raggio del filtro e osserva l'accuratezza del riconoscimento aumentare. Quando ti sentirai a tuo agio, esplora le ottimizzazioni di livello superiore menzionate sopra, e diventerai la persona di riferimento per pipeline OCR pulite nel tuo team.

Buon coding, e che il tuo OCR legga sempre correttamente! 

![esempio di preprocessamento OCR immagine](/images/preprocess-image-ocr.png "preprocess OCR immagine – prima e dopo l'elaborazione")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}