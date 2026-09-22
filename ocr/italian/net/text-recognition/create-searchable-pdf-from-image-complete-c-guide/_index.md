---
category: general
date: 2026-02-13
description: Crea PDF ricercabile da un'immagine usando Aspose.OCR. Impara a convertire
  l'immagine in PDF, estrarre il testo dall'immagine, incorporare i font nel PDF e
  riconoscere il testo da PNG.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- embed fonts in pdf
- recognize text from png
language: it
og_description: Crea PDF ricercabile da immagine con Aspose.OCR. Questa guida mostra
  come convertire un'immagine in PDF, incorporare i font ed estrarre il testo da PNG
  senza sforzo.
og_title: Crea PDF ricercabile da immagine – Tutorial C# passo‑passo
tags:
- C#
- OCR
- Aspose
- PDF generation
title: Crea PDF Ricercabile da Immagine – Guida Completa a C#
url: /it/net/text-recognition/create-searchable-pdf-from-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea PDF Ricercabile da Immagine – Guida Completa C#

Hai mai avuto bisogno di **creare PDF ricercabili** da un PNG scansionato ma non sapevi da dove cominciare? Non sei il solo. In molti progetti—pensa alla digitalizzazione di fatture o all'archiviazione di vecchi manuali—essere in grado di trasformare un'immagine in un PDF che puoi effettivamente cercare è una svolta.  

In questo tutorial percorreremo i passaggi esatti per **convertire un'immagine in PDF**, **estrarre testo dall'immagine**, incorporare i font necessari e, infine, ottenere un file PDF completamente ricercabile. Niente riferimenti vaghi, solo un esempio completo e eseguibile che puoi copiare‑incollare in Visual Studio oggi.

> **Cosa otterrai:** un'app console C# che legge `input.png`, esegue OCR, incorpora i font, mantiene l'immagine raster originale come sfondo e scrive `output.pdf`. Alla fine comprenderai *perché* ogni riga è importante e come modificarla per i tuoi scenari.

---

## Prerequisiti

- .NET 6.0 SDK o versioni successive (il codice funziona anche con .NET Framework 4.7+).  
- Aspose.OCR per .NET – puoi scaricarlo da NuGet (`Install-Package Aspose.OCR`).  
- Un'immagine PNG di esempio (`input.png`) posizionata in una cartella a tua scelta.  
- Familiarità di base con i progetti console C# (se non ne hai mai creato uno, apri Visual Studio → **Create a new project** → **Console App** → **C#**).

> **Suggerimento:** Aspose offre una licenza di prova gratuita; basta posizionare il file `.lic` accanto all'eseguibile e la libreria funzionerà senza filigrane.

---

## Passo 1: Configura il Motore OCR – Riconosci il Testo da PNG

La prima cosa di cui abbiamo bisogno è un motore OCR in grado di leggere effettivamente i caratteri in un file PNG. Aspose.OCR rende questo semplice.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;

// Initialize the OCR engine with English language support
OcrEngine ocrEngine = new OcrEngine
{
    // Primary language – you can add more if needed
    Language = OcrLanguage.English
};
```

**Perché è importante:**  
Impostare `Language` indica al motore quale set di caratteri aspettarsi. Se lo ometti, il motore utilizza una modalità generica che può interpretare erroneamente i caratteri accentati o i numeri. Per documenti multilingue, puoi passare un elenco separato da virgole come `OcrLanguage.English | OcrLanguage.French`.

---

## Passo 2: Carica e Riconosci l'Immagine – Estrai il Testo dall'Immagine

Ora che il motore è pronto, lo alimentiamo con il PNG che desideriamo elaborare.

```csharp
// Path to the source image; adjust as needed
string inputPath = @"YOUR_DIRECTORY/input.png";

// Perform OCR – this populates the engine's internal text representation
ocrEngine.RecognizeImage(inputPath);
```

**Cosa succede dietro le quinte?**  
`RecognizeImage` scansiona il bitmap, identifica i blocchi di testo e memorizza il risultato in `ocrEngine`. Puoi successivamente accedere a `ocrEngine.Text` se ti serve solo la stringa grezza, ma per un PDF ricercabile lasceremo che sia Aspose a gestire direttamente la conversione.

> **Caso limite:** Se il tuo PNG è molto grande (oltre 10 MB) potresti esaurire la memoria. In tal caso, considera di ridimensionare l'immagine prima o di usare `OcrEngine.RecognizeImage(Stream)` per trasmettere i dati in streaming.

---

## Passo 3: Configura le Opzioni di Esportazione PDF – Incorpora i Font nel PDF

Un PDF ricercabile non è utile se i font non sono incorporati; il documento apparirebbe corrotto su macchine che non hanno i caratteri richiesti. Aspose ci permette di attivare questa opzione con un semplice oggetto di configurazione.

```csharp
// Define how the searchable PDF should be built
SearchablePdfOptions pdfOptions = new SearchablePdfOptions
{
    // Guarantees the PDF renders correctly everywhere
    EmbedFonts = true,

    // Keeps the original raster image as a visual background
    KeepOriginalImage = true
};
```

**Perché incorporare i font?**  
Quando `EmbedFonts` è `true`, il PDF contiene i dati del font all'interno del file. Questo garantisce che qualsiasi visualizzatore—Chrome, Adobe Reader o un'app mobile—mostri il testo esattamente come previsto, anche se il sistema di destinazione non dispone del font.

**Quando imposteresti `KeepOriginalImage` a `false`?**  
Se ti serve solo il testo estratto e desideri un file più piccolo, disattivare questa opzione rimuove l'immagine di sfondo, lasciando un PDF “pulito” solo con il testo.

---

## Passo 4: Esporta in PDF Ricercabile – Converti Immagine in PDF

Con i risultati OCR e le opzioni PDF pronti, l'ultimo passo è una singola riga di codice che scrive il PDF ricercabile su disco.

```csharp
// Destination path for the generated PDF
string outputPath = @"YOUR_DIRECTORY/output.pdf";

// Export the OCR result as a searchable PDF
ocrEngine.ExportToSearchablePdf(outputPath, pdfOptions);

// Let the user know we’re done
Console.WriteLine("Searchable PDF created.");
```

**Ciò che vedrai:**  
Aprendo `output.pdf` in qualsiasi visualizzatore, puoi selezionare il testo, copiarlo e incollarlo, e persino eseguire una ricerca (`Ctrl + F`) per trovare parole che originariamente esistevano solo come pixel nel PNG.

---

## Esempio Completo Funzionante

Di seguito trovi il programma completo che puoi compilare ed eseguire subito. Sostituisci `YOUR_DIRECTORY` con la cartella che contiene `input.png`.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine – set language to English
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English
        };

        // 2️⃣ Recognize text from the PNG image
        string inputPath = @"YOUR_DIRECTORY/input.png";
        ocrEngine.RecognizeImage(inputPath);

        // 3️⃣ Prepare PDF options – embed fonts & keep raster background
        SearchablePdfOptions pdfOptions = new SearchablePdfOptions
        {
            EmbedFonts = true,
            KeepOriginalImage = true
        };

        // 4️⃣ Export to a searchable PDF file
        string outputPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.ExportToSearchablePdf(outputPath, pdfOptions);

        // 5️⃣ Notify the user
        Console.WriteLine("Searchable PDF created.");
    }
}
```

**Output previsto nella console:**  

```
Searchable PDF created.
```

Apri `output.pdf` e prova a cercare una parola che sai appare in `input.png`. Se viene evidenziata, hai creato con successo **un PDF ricercabile** da un'immagine.

---

## Domande Frequenti & Consigli Pro

### “Posso elaborare più immagini in un'unica esecuzione?”

Assolutamente. Avvolgi la logica di riconoscimento ed esportazione in un ciclo, magari usando `Directory.GetFiles(..., "*.png")`. Ricorda solo di dare a ciascun PDF un nome univoco, ad esempio `Path.GetFileNameWithoutExtension(img) + ".pdf"`.

### “E se il mio documento contiene sia testo in inglese che in spagnolo?”

Imposta la proprietà della lingua a una combinazione di flag:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

Aspose cercherà quindi di rilevare i caratteri di entrambi gli alfabeti.

### “Il file PDF è enorme—come posso ridurlo?”

Due trucchi rapidi:

1. Imposta `pdfOptions.KeepOriginalImage = false` per rimuovere lo sfondo raster.  
2. Usa `pdfOptions.ImageCompression = ImageCompression.Jpeg;` (dovrai aggiungere la proprietà) per comprimere l'immagine incorporata.

### “È necessaria una licenza per l'uso in produzione?”

La versione di prova funziona bene per i test, ma per il deployment commerciale devi acquistare una licenza e registrarla all'inizio della tua app:

```csharp
Aspose.OCR.License license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

---

## Estendere la Soluzione

Ora che sai come **creare PDF ricercabili**, potresti voler:

- **Aggiungere una filigrana** – usa `PdfDocument` di Aspose.PDF per sovrapporre testo dopo l'OCR.  
- **Elaborare PDF in batch** – combina più PDF ricercabili in uno usando `PdfFileEditor`.  
- **Integrare con Azure Blob Storage** – leggi/scrivi i flussi di immagine e PDF direttamente dal cloud, eliminando I/O locale dei file.

Ciascuna di queste estensioni segue lo stesso schema: ottieni il risultato OCR, configura la libreria successiva e concatenare le operazioni.

---

## Conclusione

Hai appena imparato come **creare PDF ricercabili** da un'immagine PNG usando Aspose.OCR in C#. Inizializzando il motore OCR, riconoscendo il testo, configurando `SearchablePdfOptions` per **incorporare i font nel PDF** e esportando, ottieni un file che è sia visivamente identico all'originale sia completamente ricercabile.  

Da qui, sentiti libero di sperimentare con conversioni batch, lingue diverse o compressioni più aggressive—qualunque cosa si adatti al tuo flusso di lavoro. Se incontri problemi, i forum di Aspose e la documentazione API sono ottime risorse, ma i passaggi fondamentali sopra coprono il 90 % dei casi d'uso tipici.

Buon coding, e che i tuoi PDF siano sempre ricercabili!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}