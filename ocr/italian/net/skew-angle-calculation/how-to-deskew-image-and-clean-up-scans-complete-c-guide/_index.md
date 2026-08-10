---
category: general
date: 2026-03-18
description: Come correggere l'inclinazione dell'immagine e ridurre il rumore nei
  file scansionati. Impara a caricare l'immagine da file, estrarre il testo da TIFF
  e riconoscere il testo dall'immagine con Aspose OCR.
draft: false
keywords:
- how to deskew image
- how to reduce noise
- recognize text from image
- load image from file
- extract text from tiff
language: it
og_description: Come correggere rapidamente l'inclinazione di un'immagine usando Aspose
  OCR. Questa guida ti mostra come ridurre il rumore, caricare l'immagine da file
  ed estrarre il testo da un TIFF in C#.
og_title: Come correggere l'inclinazione di un'immagine – Tutorial completo OCR in
  C#
tags:
- OCR
- C#
- Image Processing
title: Come correggere l'inclinazione delle immagini e pulire le scansioni – Guida
  completa in C#
url: /it/net/skew-angle-calculation/how-to-deskew-image-and-clean-up-scans-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come raddrizzare un'immagine – Tutorial completo OCR in C#

Ti sei mai chiesto **come raddrizzare un'immagine** che sembra sia stata scattata da uno scanner traballante? Non sei solo. La maggior parte degli sviluppatori si imbatte in questo problema quando il TIFF di origine è un po' storto e i risultati OCR diventano un caos. La buona notizia? Con un paio di righe di C# puoi raddrizzare l'immagine, eliminare lo sfondo granuloso e estrarre testo pulito e ricercabile direttamente dal file.

In questa guida vedremo **come ridurre il rumore**, **caricare l'immagine da file**, e infine **riconoscere il testo dall'immagine** usando Aspose OCR. Alla fine sarai in grado di **estrarre testo da documenti TIFF** senza sforzo.

> **Consiglio professionale:** Se stai già usando Aspose OCR per altri progetti, puoi inserire questi filtri senza ulteriori problemi di licenza.

---

## Cosa ti serve

- .NET 6 o versioni successive (il codice funziona anche su .NET Core)  
- Pacchetto NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- Un TIFF scansionato leggermente ruotato o rumoroso (useremo `skewed_scanned_doc.tif` come esempio)  
- Un editor di testo o IDE (Visual Studio, VS Code, Rider – scegli il tuo preferito)

Non sono richieste librerie aggiuntive; i filtri che utilizzeremo sono integrati in Aspose OCR.

## Passo 1 – Creare il motore OCR (Come raddrizzare un'immagine)

La prima cosa da fare è istanziare un `OcrEngine`. Pensalo come il cervello che in seguito leggerà i caratteri per te.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Initialize the OCR engine – this object holds all settings
        var ocrEngine = new OcrEngine();
```

Perché creare il motore in anticipo? Ti offre un unico punto dove collegare filtri di pre‑elaborazione, pacchetti lingua e opzioni di output. Se salti questo passo e chiami direttamente `OcrEngine.Recognize`, perdi l'opportunità di pulire l'immagine prima, ed è proprio per questo che ci interessa il deskew.

## Passo 2 – Aggiungere i filtri Deskew e Riduzione del Rumore (Come ridurre il rumore)

Now we attach two filters:

| Filtro | Cosa fa | Perché è importante |
|--------|---------|----------------------|
| `AutoDeskewFilter` | Rileva e corregge la rotazione | Allinea le linee di testo affinché il motore OCR possa leggerle correttamente |
| `NoiseReductionFilterV2` | Rimuove macchie e granulosità di sfondo | Pixel più puliti significano meno errori di riconoscimento |

```csharp
        // Add filters to improve OCR accuracy
        ocrEngine.Settings.Filters.Add(new AutoDeskewFilter());          // corrects rotation
        ocrEngine.Settings.Filters.Add(new NoiseReductionFilterV2());   // reduces background noise
```

Puoi sostituire `NoiseReductionFilterV2` con la versione più vecchia, ma l'algoritmo v2 gestisce meglio gli scanner moderni. Se il tuo documento è già perfettamente piatto, il filtro deskew passerà semplicemente l'immagine senza modificarla—nessun danno.

## Passo 3 – Caricare l'immagine da file (Caricare immagine da file)

Aspose fornisce un comodo helper `ImageStream.FromFile` che legge una varietà di formati, inclusi TIFF, JPEG, PNG e BMP. Ecco come carichiamo il file in memoria:

```csharp
        // Load the scanned image you want to preprocess
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_scanned_doc.tif");
```

Sostituisci `YOUR_DIRECTORY` con il percorso reale sulla tua macchina. Se lavori con un percorso relativo, assicurati che il file si trovi accanto al tuo eseguibile o imposta la directory di lavoro di conseguenza.

## Passo 4 – Eseguire OCR sull'immagine pre‑elaborata (Riconoscere testo dall'immagine)

Con i filtri in posizione e l'immagine caricata, chiediamo finalmente ad Aspose di leggere i caratteri:

```csharp
        // Perform OCR – the engine will automatically apply the filters first
        var ocrResult = ocrEngine.Recognize(image);
```

Dietro le quinte il motore esegue l'algoritmo deskew, elimina il rumore e poi utilizza un riconoscitore basato su rete neurale. Il risultato è incapsulato in un oggetto `OcrResult` che fornisce il testo grezzo, i punteggi di confidenza e persino le bounding box se ti servono in seguito.

## Passo 5 – Visualizzare o salvare il testo estratto (Estrarre testo da TIFF)

Per una demo rapida stampiamo semplicemente il testo sulla console, ma potresti scriverlo su un file, un database o inserirlo in un flusso di lavoro successivo.

```csharp
        // Show the recognized text in the console
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Output previsto** (esempio, varierà con il tuo documento):

```
Invoice #12345
Date: 2023‑04‑01
Total: $1,250.00
Thank you for your business!
```

Se l'output contiene ancora caratteri illeggibili, verifica che il TIFF originale non sia a risoluzione troppo bassa (si consiglia almeno 300 dpi) e che la lingua sia impostata correttamente in `ocrEngine.Settings.Language`.

## Esempio completo funzionante (Tutti i passi in un unico posto)

Di seguito il programma completo che puoi copiare‑incollare in un nuovo progetto console e eseguire subito.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Add preprocessing filters
        ocrEngine.Settings.Filters.Add(new AutoDeskewFilter());          // deskew image
        ocrEngine.Settings.Filters.Add(new NoiseReductionFilterV2());   // reduce noise

        // 3️⃣ Load the image file (TIFF, JPEG, etc.)
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_scanned_doc.tif");

        // 4️⃣ Recognize text – filters run automatically
        var ocrResult = ocrEngine.Recognize(image);

        // 5️⃣ Output the extracted text
        Console.WriteLine(ocrResult.Text);
    }
}
```

Salva il file come `Program.cs`, esegui `dotnet run` e dovresti vedere il testo pulito apparire nel tuo terminale.

## Domande frequenti e casi particolari

### E se il mio TIFF ha più pagine?

Aspose OCR può elaborare immagini multipagina iterando su `image.GetPages()` (o usando `image.Pages`). Ogni pagina restituisce il proprio `OcrResult`. Combinali con `StringBuilder` se ti serve una singola stringa.

### Il filtro deskew funziona su immagini fortemente ruotate?

Gestisce rotazioni fino a circa ±15°. Oltre questo potresti dover pre‑ruotare l'immagine manualmente usando una libreria grafica (ad esempio `System.Drawing` o `SkiaSharp`) prima di passarla ad Aspose.

### Come posso migliorare l'accuratezza per testi non‑inglesi?

Imposta la lingua esplicitamente:

```csharp
ocrEngine.Settings.Language = Language.English; // or Language.French, etc.
```

Puoi anche caricare pacchetti lingua personalizzati se quelli integrati non coprono il tuo alfabeto.

### Posso eseguire questo su Linux?

Assolutamente. Aspose OCR è cross‑platform; assicurati solo che le dipendenze native siano presenti (di solito nessuna per la versione .NET pura). Usa `dotnet publish -r linux-x64` per un binario autonomo.

## Bonus: Visualizzare l'immagine deskewed

Se vuoi vedere l'immagine corretta prima dell'OCR, puoi salvarla nuovamente su disco:

```csharp
// After OCR, the filtered image is stored in ocrEngine.Settings.FiltersResult
var corrected = ocrEngine.Settings.FiltersResult;
corrected.Save(@"output/deskewed_cleaned.tif");
```

![esempio di come raddrizzare un'immagine](https://example.com/deskew-demo.png "esempio di come raddrizzare un'immagine")

*Testo alternativo dell'immagine:* **esempio di come raddrizzare un'immagine** – mostra un prima/dopo di un TIFF ruotato corretto da AutoDeskewFilter.

## Conclusione

Abbiamo coperto **come raddrizzare un'immagine**, **come ridurre il rumore**, e l'intera pipeline per **riconoscere il testo dall'immagine**, **caricare l'immagine da file**, ed **estrarre testo da TIFF** usando Aspose OCR in C#. La conclusione principale? Aggiungere solo due filtri di pre‑elaborazione può trasformare una scansione traballante e granulosa in un documento nitido e ricercabile senza strumenti esterni.

Pronto per il passo successivo? Prova a sostituire `AutoDeskewFilter` con `AutoRotateFilter` se i tuoi documenti sono capovolti, o sperimenta con `ContrastEnhancementFilter` per stampe sbiadite. Lo stesso schema—engine → filtri → load → recognize—vale per tutti gli scenari Aspose OCR, così puoi riutilizzare questa struttura per PDF, PNG o anche foto scattate con la fotocamera.

Buona programmazione, e che il tuo OCR sia sempre preciso!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}