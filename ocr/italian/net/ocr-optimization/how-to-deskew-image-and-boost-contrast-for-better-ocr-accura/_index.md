---
category: general
date: 2025-12-30
description: Come correggere rapidamente l'inclinazione di un'immagine e imparare
  a migliorare il contrasto durante l'estrazione del testo dall'immagine per una maggiore
  precisione OCR.
draft: false
keywords:
- how to deskew image
- how to boost contrast
- extract text from image
- recognize text image
- improve ocr accuracy
language: it
og_description: Come correggere rapidamente l'inclinazione di un'immagine e imparare
  a aumentare il contrasto durante l'estrazione del testo dall'immagine per migliorare
  l'accuratezza OCR.
og_title: Come raddrizzare l'immagine e aumentare il contrasto per migliorare l'accuratezza
  dell'OCR
tags:
- OCR
- C#
- Image Processing
title: Come raddrizzare l'immagine e aumentare il contrasto per una migliore precisione
  OCR
url: /it/net/ocr-optimization/how-to-deskew-image-and-boost-contrast-for-better-ocr-accura/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come correggere l'inclinazione di un'immagine e aumentare il contrasto per una migliore precisione OCR

Ti sei mai chiesto **come correggere l'inclinazione di un'immagine** proveniente da uno scanner o da uno smartphone?  
Non sei l'unico: la maggior parte degli sviluppatori si imbatte in questo problema quando l'immagine di origine è leggermente inclinata o rumorosa, e l'output OCR finisce per essere un pasticcio.  

La buona notizia è che con poche righe di C# puoi raddrizzare l'immagine, pulire lo sfondo e persino aumentare il contrasto in modo che il motore legga il testo come un professionista. In questa guida ti mostreremo anche come **estrarre testo da un'immagine** e **riconoscere il contenuto di un'immagine di testo** con Aspose.OCR, mantenendo sempre **migliorare la precisione OCR** al centro dell'attenzione.

## Cosa ti serve

- **.NET 6.0** o successivo (il codice si compila anche su .NET Framework 4.7+)  
- Pacchetto NuGet **Aspose.OCR** (versione 23.12 o più recente) – installa tramite `dotnet add package Aspose.OCR`  
- Un'immagine di esempio che sia sia ruotata sia rumorosa (ad es., `noisy_rotated.jpg`)  
- Visual Studio, VS Code, o qualsiasi IDE preferisci  

È tutto—nessuna libreria nativa aggiuntiva, nessun binding pesante di OpenCV. Solo puro codice gestito.

---

## Passo 1: Configura il progetto e importa i namespace

Per prima cosa, crea una nuova app console e porta i namespace richiesti nello scope. Questo passo è la base per tutto ciò che segue.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in later
        }
    }
}
```

**Perché è importante:**  
`Aspose.OCR` ti fornisce la classe `OcrEngine`, mentre `Aspose.OCR.Filters` offre pratici filtri di pre‑processing come `DeskewFilter` e `ContrastBoostFilter`. Importarli in anticipo mantiene il codice ordinato e segnala al compilatore cosa intendiamo utilizzare.

---

## Passo 2: Inizializza il motore OCR e aggiungi un filtro Deskew

Ora effettivamente **come correggere l'inclinazione di un'immagine**. Il `DeskewFilter` rileva automaticamente l'angolo di rotazione (fino al massimo impostato) e ruota la bitmap nuovamente in orizzontale.

```csharp
// Inside Main()
var ocrEngine = new OcrEngine();

// Deskew: correct up to 15 degrees of rotation
ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 15 });
```

**Cosa succede dietro le quinte?**  
Il filtro analizza l'immagine alla ricerca della linea orizzontale più lunga di testo, stima l'inclinazione e applica una rotazione inversa. Limitando `MaxAngle` a 15°, evitiamo di correggere eccessivamente le immagini già dritte.

> **Consiglio pro:** Se le tue immagini di origine potrebbero essere capovolte, imposta `MaxAngle` a 180°—il filtro troverà comunque l'orientamento corretto.

---

## Passo 3: Riduci il rumore con un filtro Denoise

Una scansione rumorosa può ingannare anche il motore OCR più intelligente. Aggiungere un `DenoiseFilter` leviga i granelli senza cancellare i dettagli fini.

```csharp
// Denoise: strength ranges from 0 (off) to 1 (max)
ocrEngine.Filters.Add(new DenoiseFilter { Strength = 0.7 });
```

**Perché ti serve:**  
Il rumore crea bordi falsi che l'algoritmo OCR interpreta come caratteri. Una intensità di `0.7` è un punto ottimale per la maggior parte dei documenti scansionati; sentiti libero di regolarla per input molto puliti o molto sporchi.

---

## Passo 4: Aumenta il contrasto – “Come aumentare il contrasto” in pratica

Qui rispondiamo alla keyword secondaria **come aumentare il contrasto**. Il `ContrastBoostFilter` amplifica la differenza tra il testo scuro e lo sfondo chiaro, facendo risaltare le lettere.

```csharp
// Contrast boost: level > 1 increases contrast
ocrEngine.Filters.Add(new ContrastBoostFilter { Level = 1.3 });
```

**Il ragionamento:**  
Un contrasto più alto riduce la probabilità che tratti sottili vengano persi. Un livello di `1.3` funziona bene per i tipici documenti nero‑su‑bianco; per foto a colori potresti aver bisogno di `1.5` o più.

---

## Passo 5: Esegui OCR ed estrai il testo

Con l'immagine pre‑processata, finalmente **estraiamo testo da un'immagine** usando il metodo `Recognize`. Il metodo restituisce un oggetto `OcrResult` che contiene la stringa grezza e i punteggi di confidenza.

```csharp
// Perform OCR on the prepared image
var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/noisy_rotated.jpg");

// Output the recognized text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

**Cosa ottieni:**  
`ocrResult.Text` contiene la rappresentazione in plain‑text di tutto ciò che il motore è riuscito a leggere. Se ti serve la confidenza a livello di parola, esplora `ocrResult.Regions`—ogni regione include una proprietà `Confidence`.

---

## Esempio completo funzionante (pronto per copia‑incolla)

Di seguito trovi il programma completo che puoi inserire in `Program.cs`. Assicurati che il percorso dell'immagine punti a un file reale sul tuo computer.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Deskew – correct up to 15° rotation
            ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 15 });

            // 3️⃣ Denoise – smooth out speckles (strength 0.7)
            ocrEngine.Filters.Add(new DenoiseFilter { Strength = 0.7 });

            // 4️⃣ Contrast boost – make text pop (level 1.3)
            ocrEngine.Filters.Add(new ContrastBoostFilter { Level = 1.3 });

            // 5️⃣ Recognize the image
            var imagePath = @"YOUR_DIRECTORY\noisy_rotated.jpg";
            var ocrResult = ocrEngine.Recognize(imagePath);

            // 6️⃣ Show the result
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**Output previsto (esempio):**

```
=== OCR Output ===
Invoice #12345
Date: 2024-09-30
Total Amount: $1,250.00
Thank you for your business!
```

Se il risultato appare confuso, ricontrolla la qualità dell'immagine, regola `Strength` o `Level`, o aumenta `MaxAngle` per una correzione dell'inclinazione più aggressiva.

---

## Domande comuni e casi particolari

### E se l'immagine è capovolta?

Imposta `MaxAngle = 180` nel `DeskewFilter`. Il filtro rileverà la rotazione di 180° e la capovolgerà correttamente.

### Il mio documento è a colori (ad es., un modulo scansionato con evidenziazioni blu).

Prova ad aggiungere un `ColorFilter` prima dell'aumento del contrasto, o converti manualmente l'immagine in scala di grigi:

```csharp
ocrEngine.Filters.Add(new GrayscaleFilter());
```

### Devo elaborare molti file in batch.

Racchiudi la logica OCR in un ciclo `foreach` che itera su una directory:

```csharp
foreach (var file in Directory.GetFiles(@"C:\Scans", "*.jpg"))
{
    var result = ocrEngine.Recognize(file);
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), result.Text);
}
```

### Come faccio a conoscere la confidenza OCR?

Ispeziona `ocrResult.Regions`:

```csharp
foreach (var region in ocrResult.Regions)
{
    Console.WriteLine($"Text: {region.Text} – Confidence: {region.Confidence:P2}");
}
```

Valori di confidenza più alti (vicini al 100%) solitamente indicano che i passaggi di pre‑processing hanno avuto successo.

---

## Consigli per massimizzare la precisione OCR

| Consiglio | Perché aiuta |
|-----|--------------|
| **Usa formati immagine senza perdita** (PNG, TIFF) | La compressione JPEG può sfocare i bordi, compromettendo il riconoscimento. |
| **Mantieni i DPI a 300+** | Più pixel per carattere forniscono al motore più dati da elaborare. |
| **Ritaglia i margini irrilevanti** | Riduce il rumore e velocizza l'elaborazione. |
| **Applica una soglia binaria** (nero/bianco) dopo l'aumento del contrasto per documenti di solo testo | Semplifica l'immagine a due colori, cosa che la maggior parte dei motori OCR adora. |
| **Testa prima con un piccolo campione** | Ti permette di regolare finemente `Strength` e `Level` prima di scalare. |

---

## Conclusione

Abbiamo illustrato **come correggere l'inclinazione di un'immagine**, **come aumentare il contrasto**, e l'intera pipeline per **estrarre testo da un'immagine** usando Aspose.OCR. Concatenando un `DeskewFilter`, `DenoiseFilter` e `ContrastBoostFilter` prima di chiamare `Recognize`, noterai un significativo miglioramento in **migliorare la precisione OCR** per la maggior parte delle scansioni reali.  

Prova il codice, regola i parametri dei filtri per adattarli alle particolarità dei tuoi documenti, e otterrai testo pulito anche dalle foto più caotiche in pochissimo tempo. Hai bisogno di andare oltre? Prova ad aggiungere dizionari specifici per lingua, o invia l'output a un correttore ortografico per il post‑processing.  

Buon coding, e che i risultati OCR siano sempre cristallini! 

--- 

![how to deskew image example](deskew_example.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}