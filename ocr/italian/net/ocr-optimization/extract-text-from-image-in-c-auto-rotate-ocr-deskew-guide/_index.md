---
category: general
date: 2026-03-29
description: Estrai il testo da un'immagine con Aspose OCR in C#. Scopri l'OCR con
  rotazione automatica e come correggere l'inclinazione dell'immagine scansionata
  per risultati perfetti.
draft: false
keywords:
- extract text from image
- auto rotate ocr
- how to deskew scanned image
- Aspose OCR C#
- image preprocessing OCR
language: it
og_description: Estrai il testo da un'immagine usando Aspose OCR. Questa guida mostra
  l'OCR con rotazione automatica e come correggere l'inclinazione di un'immagine scansionata
  in C#.
og_title: Estrai testo da immagine in C# – OCR con rotazione automatica e correzione
  dell'inclinazione
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Estrai testo da un'immagine in C# – Guida all'OCR con rotazione automatica
  e correzione dell'inclinazione
url: /it/net/ocr-optimization/extract-text-from-image-in-c-auto-rotate-ocr-deskew-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai testo da immagine in C# – Guida all'OCR con rotazione automatica e correzione dell'inclinazione

Ti è mai capitato di dover **estrarre testo da immagine** ma il file arrivava con un angolo strano? È un fastidio comune—soprattutto quando si tratta di fatture scannerizzate, ricevute fotografate o PDF storti. La buona notizia è che non devi scrivere un algoritmo di rotazione personalizzato. Usando la funzione integrata *auto rotate OCR* di Aspose OCR puoi far ruotare l’immagine al motore e poi **estrarre testo da immagine** in un unico passaggio fluido.

In questo tutorial vedremo un programma C# completo, pronto‑da‑eseguire, che:

* Inizializza il motore OCR con orientamento automatico e correzione dell’inclinazione,
* Riconosce un’immagine ruotata o inclinata,
* Restituisce sia l’angolo di rotazione rilevato sia il testo estratto.

Nessun servizio esterno, nessun calcolo complicato—solo poche righe di codice e una spiegazione chiara di *how to deskew scanned image* quando necessario.

## What You’ll Need

| Prerequisito | Perché è importante |
|--------------|---------------------|
| .NET 6.0 o versioni successive (o .NET Framework 4.6+) | Aspose OCR è distribuito come pacchetto NuGet che supporta questi runtime. |
| Visual Studio 2022 (o qualsiasi editor C#) | Rende semplice aggiungere pacchetti NuGet ed eseguire l’app console. |
| Un’immagine di esempio (`rotated_document.jpg`) | Il file deve essere JPEG, PNG, BMP o TIFF e non perfettamente verticale. |
| Pacchetto NuGet Aspose.OCR (`Install-Package Aspose.OCR`) | Fornisce `OcrEngine`, `PreprocessingFilters` e i tipi correlati. |

Se hai spuntato tutte queste caselle, sei pronto a partire. Altrimenti, scarica l’ultima versione di Aspose OCR da NuGet—​l’installazione è a un click.

---

## Step 1 – Initialise the OCR Engine (Primary Keyword in Action)

La prima cosa che facciamo è creare un’istanza di `OcrEngine` e dirle di **auto rotate OCR** e **deskew** qualsiasi immagine in ingresso. Quei due flag sono combinati con un OR bit‑wise (`|`) perché `PreprocessingFilters` è un enum con l’attributo `[Flags]`.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Initialise the OCR engine with English language and preprocessing options
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            // Enable both auto‑rotate and auto‑deskew
            Preprocessing = PreprocessingFilters.AutoRotate | PreprocessingFilters.AutoDeskew
        };
```

> **Why this matters:**  
> *Auto‑rotate OCR* analizza la linea di base del testo nell’immagine, indovina l’orientamento corretto e la ruota internamente prima del riconoscimento. *Auto‑deskew* fa lo stesso per leggere inclinazioni che spesso compaiono nei documenti scannerizzati. Abilitando entrambi, garantisci i migliori risultati possibili di **extract text from image** senza dover modificare manualmente l’immagine.

---

## Step 2 – Recognise the Image and Retrieve the Result

Ora passiamo al motore il percorso del file. Il metodo `RecognizeImage` restituisce un oggetto `OcrResult` che contiene l’angolo di rotazione rilevato, i punteggi di confidenza e l’output in testo semplice.

```csharp
        // Recognise the image file and obtain the OCR result
        OcrResult ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/rotated_document.jpg");
```

> **Tip:** Se lavori con uno stream (ad es., un file caricato), usa `ocrEngine.RecognizeImage(Stream)` invece. Gli stessi flag di preprocessing si applicano, così ottieni comunque i vantaggi di **auto rotate OCR**.

---

## Step 3 – Display the Rotation Angle and the Extracted Text

Infine, stampiamo due informazioni sulla console: l’angolo che il motore ritiene necessario ruotare l’immagine e il testo effettivamente estratto.

```csharp
        // Show the detected rotation and the recognised text
        Console.WriteLine($"Detected rotation: {ocrResult.RotationAngle}°");
        Console.WriteLine("----- Extracted Text -----");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Expected output** (i tuoi numeri varieranno in base all’immagine di input):

```
Detected rotation: 12.3°
----- Extracted Text -----
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

Se l’immagine era già verticale, l’angolo di rotazione sarà `0°`, e otterrai comunque testo pulito grazie all’algoritmo *auto‑deskew*.

---

## Step 4 – Understanding How to Deskew Scanned Image (Secondary Keyword Deep‑Dive)

Potresti chiederti *how to deskew scanned image* quando il motore OCR segnala una rotazione diversa da zero. In pratica, Aspose OCR applica una **trasformata di Hough** per individuare l’orientamento dominante delle linee di testo. Poi ruota il bitmap dell’inverso di quell’angolo, raddrizzando efficacemente il testo.

**When does it matter?**  
* Scanner che alimentano la carta con un leggero angolo (comune negli ambienti d’ufficio).  
* Foto scattate con lo smartphone a mano—​l’orizzonte raramente è perfetto.  

**Edge case handling:**  
Se `RotationAngle` del risultato è insolitamente grande (es., > 45°), il motore potrebbe aver interpretato male l’immagine (forse è un logo o una grafica non testuale). In tal caso puoi:

1. Ruotare manualmente l’immagine usando `System.Drawing` prima di passarla al motore, oppure  
2. Disabilitare `AutoRotate` e mantenere solo `AutoDeskew` se sai che il documento è già verticale.

```csharp
// Example: manually rotate 90° clockwise before OCR
using (var img = Aspose.OCR.Image.Load("rotated_document.jpg"))
{
    img.Rotate(90);
    OcrResult result = ocrEngine.RecognizeImage(img);
    Console.WriteLine(result.Text);
}
```

---

## Step 5 – Common Pitfalls & Pro Tips (E‑E‑A‑T in Action)

| Problema | Perché succede | Soluzione |
|----------|----------------|-----------|
| **Immagini sfocate o a bassa risoluzione** | La precisione OCR cala drasticamente; il rilevamento della rotazione può fallire. | Usa scansioni di almeno 300 dpi; applica un filtro di nitidezza prima dell’OCR. |
| **Lingue miste** | Il motore usa l’inglese di default; i caratteri stranieri diventano illeggibili. | Imposta `Language = Language.English | Language.Spanish` (o la combinazione appropriata). |
| **File di grandi dimensioni (> 10 MB)** | La pressione sulla memoria può causare `OutOfMemoryException`. | Ridimensiona l’immagine prima, oppure elabora a tasselli usando `OcrEngine.RecognizeRegion`. |
| **Percorso file errato** | `FileNotFoundException` interrompe il programma. | Usa `Path.Combine(Environment.CurrentDirectory, "rotated_document.jpg")` per maggiore robustezza. |

> **Pro tip:** Registra sempre `ocrResult.RotationAngle` e `ocrResult.Confidence` (se disponibili). Queste metriche ti aiutano a decidere se vale la pena riprovare con impostazioni di preprocessing diverse.

---

## Step 6 – Extending the Example (What’s Next?)

Ora che puoi **extract text from image** con rotazione automatica e correzione dell’inclinazione, considera i prossimi passi:

* **Elaborazione batch** – Scorri una cartella di immagini, salva ogni risultato in un database e segnala quelli con `RotationAngle > 5°` per una revisione manuale.  
* **Conversione PDF** – Unisci il testo estratto con l’immagine originale in un PDF ricercabile usando Aspose.PDF.  
* **Rilevamento lingua** – Usa il flag `AutoDetectLanguage` di Aspose.OCR per far scegliere al motore la lingua migliore automaticamente.  

Tutti questi si basano sullo stesso principio fondamentale: lasciare che la libreria gestisca l’orientamento, mentre tu ti concentri sulla logica di business.

---

## Full Working Example (Copy‑Paste Ready)

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine with auto‑rotate and auto‑deskew
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            Preprocessing = PreprocessingFilters.AutoRotate | PreprocessingFilters.AutoDeskew
        };

        // 2️⃣ Recognise the image – replace the path with your own file
        string imagePath = "YOUR_DIRECTORY/rotated_document.jpg";
        OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 3️⃣ Output the rotation angle and the recognised text
        Console.WriteLine($"Detected rotation: {ocrResult.RotationAngle}°");
        Console.WriteLine("----- Extracted Text -----");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Salva il file come `Program.cs`, esegui `dotnet add package Aspose.OCR`, poi `dotnet run`. Dovresti vedere l’angolo e il testo pulito stampati sulla console.

---

## Conclusion

Abbiamo appena dimostrato come **extract text from image** in C# lasciando che Aspose OCR si occupi di *auto rotate OCR* e del complicato problema *how to deskew scanned image*. Abilitando i due flag di preprocessing, il motore raddrizza automaticamente le immagini storte, rileva l’orientamento corretto e fornisce testo accurato—senza necessità di modifiche manuali all’immagine.

Sentiti libero di sperimentare con batch più grandi, lingue diverse, o persino integrare l’output in un PDF ricercabile. Il cielo è il limite una volta che il motore OCR gestisce il lavoro pesante per te.

**Pronto a potenziare il tuo flusso di documenti?** Prendi il codice, puntalo alle tue scansioni e guarda gli angoli di rotazione scomparire. Se incontri difficoltà, lascia un commento qui sotto—buon coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}