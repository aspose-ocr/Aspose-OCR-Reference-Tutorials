---
category: general
date: 2026-02-17
description: Esegui OCR su un'immagine usando Aspose OCR in C#. Scopri come estrarre
  testo da jpg, preelaborare l'immagine per l'OCR e caricare l'immagine per l'OCR
  con codice passo‑passo.
draft: false
keywords:
- run OCR on image
- extract text from jpg
- preprocess image for OCR
- load image for OCR
language: it
og_description: Esegui OCR su un'immagine usando Aspose OCR in C#. Questa guida ti
  mostra come estrarre il testo da un JPG, preelaborare l'immagine e caricarla per
  l'OCR.
og_title: Esegui OCR su immagine con Aspose OCR – Guida completa C#
tags:
- Aspose OCR
- C#
- Image Processing
title: Esegui OCR su immagine con Aspose OCR – Guida completa C#
url: /it/net/text-recognition/run-ocr-on-image-with-aspose-ocr-complete-c-guide/
---

? It's bold. Keep as is but translate.

We need to keep code block fences and placeholders.

Let's produce final translation.

Be careful not to translate code block placeholders.

Let's write.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esegui OCR su Immagine con Aspose OCR – Guida Completa in C#

Hai mai dovuto **eseguire OCR su file immagine** ma non sapevi da dove cominciare? In molte applicazioni reali – pensa a scanner di fatture o tracciatori di ricevute – il primo ostacolo è ottenere testo affidabile da un JPEG. La buona notizia? Con Aspose OCR puoi **eseguire OCR su file immagine** in poche righe di codice C#, e imparerai anche a **estrarre testo da jpg**, **pre‑elaborare l’immagine per OCR**, e **caricare l’immagine per OCR** senza dover setacciare documenti sparsi.

In questo tutorial percorreremo un esempio completo, pronto per il copia‑incolla, che mostra esattamente come configurare il motore, aggiungere filtri di pre‑elaborazione utili, fornire un’immagine al riconoscitore e stampare il risultato sulla console. Alla fine avrai un programma autonomo da inserire in qualsiasi progetto .NET e iniziare a estrarre testo dalle immagini immediatamente.

## Cosa Ti Serve

- .NET 6.0 o successivo (il codice funziona anche su .NET Core)  
- Pacchetto NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- Un JPEG di esempio (`input.jpg`) posizionato in una cartella a cui puoi fare riferimento  
- Una conoscenza di base della sintassi C# (nulla di esotico)

Se hai già questi elementi, ottimo – immergiamoci. Altrimenti, scarica il pacchetto NuGet e una foto di test; il resto della guida presuppone che tu l’abbia fatto.

## Passo 1: Crea il Motore OCR – Il Cuore dell’Esecuzione di OCR su Immagine

La prima cosa da fare per **eseguire OCR su dati immagine** è istanziare l’`OcrEngine`. Questo oggetto contiene tutta la configurazione e lo stato necessari per il riconoscimento.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessExample
{
    static void Main()
    {
        // Step 1 – create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **Perché è importante:** L’`OcrEngine` è il gateway al pipeline di riconoscimento di Aspose. Senza di esso non puoi accedere a filtri, pacchetti lingua o al metodo `Recognize`.

## Passo 2: Aggiungi Filtri di Pre‑Elaborazione – Migliora la Precisione Quando Estrarre Testo da JPG

Le immagini direttamente dalla fotocamera raramente sono perfette. Angoli inclinati o granulosità casuale possono ostacolare anche i migliori algoritmi OCR. Aggiungere un paio di filtri prima di **estrarre testo da jpg** può migliorare drasticamente i risultati.

```csharp
        // Step 2 – add preprocessing filters
        // Deskew corrects rotation; DenoiseGaussian reduces visual noise
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseGaussianFilter { Sigma = 1.5 });
```

> **Consiglio professionale:** Se le tue immagini di origine sono già pulite, puoi saltare il `DenoiseGaussianFilter`. Troppa levigatura potrebbe cancellare caratteri deboli.

## Passo 3: Carica l’Immagine per OCR – Fornire il JPEG al Motore

Ora arriva la parte in cui **carichi l’immagine per OCR**. Aspose fornisce un comodo helper `ImageStream.FromFile` che avvolge un percorso file in uno stream comprensibile al motore.

```csharp
        // Step 3 – specify the path to the JPEG you want to process
        var imagePath = @"YOUR_DIRECTORY/input.jpg";

        // Load the image and run OCR in one call
        var ocrResult = ocrEngine.Recognize(ImageStream.FromFile(imagePath));
```

> **Caso limite:** Se il file non esiste, `FromFile` lancia una `FileNotFoundException`. Avvolgi la chiamata in un try/catch se ti aspetti file mancanti a runtime.

## Passo 4: Recupera e Visualizza il Testo Riconosciuto

Infine, una volta che il motore ha terminato, puoi accedere al risultato in plain‑text tramite la proprietà `Text`. Stamparlo sulla console è sufficiente per una demo rapida, ma potresti anche scriverlo in un database o in un file di testo.

```csharp
        // Step 4 – output the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Output previsto**

```
=== OCR Result ===
Invoice #12345
Date: 02/15/2026
Total: $1,234.56
```

Il contenuto esatto dipenderà dall’immagine fornita, ma dovresti vedere un blocco di testo ben formattato invece di spazzatura.

![Diagramma che mostra il pipeline OCR – esegui OCR su immagine, pre‑elabora, carica, riconosci](/images/ocr-pipeline.png "diagramma del pipeline OCR")

### Perché Ogni Passo è Importante

| Passo | Scopo | Cosa Succede se Saltato |
|------|---------|--------------------------|
| **Crea motore** | Inizializza le strutture interne | Nessun riconoscitore disponibile – otterrai una `NullReferenceException`. |
| **Aggiungi filtri** | Migliora la precisione correggendo rotazione e rumore | Immagini inclinate o rumorose producono output incomprensibile. |
| **Carica immagine** | Fornisce il bitmap grezzo al motore | Il motore non ha nulla da elaborare, risultando in un campo `Text` vuoto. |
| **Leggi risultato** | Estrae la stringa di testo per ulteriori usi | Hai eseguito OCR ma non vedi il risultato – poco utile! |

## Varianti Comuni e Come Regolare il Processo

### Cambiare il Pacchetto Lingua

Aspose OCR supporta più lingue fin da subito. Se devi **eseguire OCR su file immagine** che contengono, ad esempio, testo francese o tedesco, imposta la proprietà `Language` prima di chiamare `Recognize`.

```csharp
ocrEngine.Language = OcrLanguage.French;
```

### Gestire PDF Multi‑Pagina

Se la tua sorgente è un PDF multi‑pagina anziché un singolo JPEG, puoi convertire ogni pagina in immagine prima (usando Aspose.PDF) e poi alimentare ogni immagine nello stesso pipeline. Il ciclo sulle pagine è semplice:

```csharp
foreach (var pageImage in pdfPagesAsImages)
{
    var result = ocrEngine.Recognize(ImageStream.FromMemory(pageImage));
    Console.WriteLine(result.Text);
}
```

### Gestire File di grandi dimensioni

Quando elabori foto ad alta risoluzione, il consumo di memoria può aumentare. Considera di ridurre la risoluzione dell’immagine prima di **caricare l’immagine per OCR**:

```csharp
using Aspose.Imaging;
using Aspose.Imaging.ImageOptions;

var loadOptions = new JpegLoadOptions { Width = 1024, Height = 768 };
using (var img = (Image)Image.Load(imagePath, loadOptions))
{
    var stream = new MemoryStream();
    img.Save(stream, new JpegOptions());
    var ocrResult = ocrEngine.Recognize(ImageStream.FromMemory(stream.ToArray()));
}
```

## Esempio Completo, Pronto per l’Esecuzione

Di seguito trovi il programma completo che incorpora tutto ciò di cui abbiamo parlato. Copialo in un nuovo progetto console, sostituisci `YOUR_DIRECTORY` con la cartella che contiene `input.jpg`, e premi **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessExample
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Add useful preprocessing filters
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseGaussianFilter { Sigma = 1.5 });

        // 3️⃣ Load the JPEG you want to process
        var imagePath = @"YOUR_DIRECTORY/input.jpg";

        try
        {
            // Recognize text – this is where we actually run OCR on image
            var ocrResult = ocrEngine.Recognize(ImageStream.FromFile(imagePath));

            // 4️⃣ Print the extracted text
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error processing image: {ex.Message}");
        }
    }
}
```

### Verifica il Risultato

1. Esegui il programma.  
2. Controlla la console – dovresti vedere il testo presente in `input.jpg`.  
3. Se l’output appare confuso, prova a regolare il valore `Sigma` su `DenoiseGaussianFilter` o aggiungi filtri aggiuntivi come `ContrastEnhancementFilter`.

## Riepilogo e Prossimi Passi

Abbiamo appena coperto come **eseguire OCR su file immagine** usando Aspose OCR, dalla configurazione del motore alla consegna di testo pulito e leggibile. I punti chiave:

- Crea un’istanza di `OcrEngine`.  
- **Pre‑elabora l’immagine per OCR** con filtri come `DeskewFilter` e `DenoiseGaussianFilter`.  
- **Carica l’immagine per OCR** usando `ImageStream.FromFile`.  
- Chiama `Recognize` e leggi `ocrResult.Text` per **estrarre testo da jpg**.

Vuoi andare oltre? Prova queste idee:

- **Elaborazione batch** – leggi una cartella di JPEG e salva ogni risultato in un file `.txt` separato.  
- **Integra con Azure Blob Storage** – preleva immagini dal cloud, esegui OCR, poi memorizza il testo.  
- **Combina con NLP** – invia il testo estratto a un modello di comprensione linguistica per categorizzare automaticamente le fatture.  

Sentiti libero di sperimentare con diverse combinazioni di filtri, pacchetti lingua, o anche di passare a PNG e TIFF – lo stesso pipeline funziona finché **carichi l’immagine per OCR** correttamente.

---

Se hai incontrato problemi, lascia un commento qui sotto o consulta la documentazione di Aspose OCR per impostazioni avanzate. Buona programmazione e divertiti a trasformare le immagini in testo ricercabile!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}