---
category: general
date: 2026-01-10
description: Come eseguire rapidamente l'OCR e estrarre testo arabo da un'immagine.
  Impara a convertire l'immagine in testo, leggere il testo da PNG e scopri come estrarre
  il testo con Aspose OCR.
draft: false
keywords:
- how to run OCR
- extract arabic text
- convert image to text
- read text from png
- how to extract text
language: it
og_description: Come eseguire l'OCR in C# ed estrarre testo arabo da un'immagine PNG.
  Questa guida ti mostra come convertire l'immagine in testo e leggere il testo da
  PNG passo passo.
og_title: Come eseguire OCR in C# – Estrarre testo arabo da PNG
tags:
- OCR
- C#
- Aspose
title: Come eseguire OCR in C# – Estrarre testo arabo da PNG
url: /it/net/text-recognition/how-to-run-ocr-in-c-extract-arabic-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR in C# – Estrarre testo arabo da PNG

Ti sei mai chiesto **come eseguire OCR** su un'immagine che contiene caratteri arabi? Non sei solo. Molti sviluppatori si trovano in difficoltà quando devono **estrarre testo arabo** da un PNG ma non sanno quale libreria gestisca gli script da destra a sinistra senza problemi.  

In questo tutorial ti guideremo passo passo su tutto ciò che devi sapere per **convertire immagine in testo**, **leggere testo da PNG**, e infine **come estrarre testo** usando Aspose.OCR in una pulita app console C#. Alla fine avrai un programma pronto all'uso che stampa la stringa araba direttamente nel terminale.

## Cosa imparerai

- Installare e referenziare il pacchetto NuGet Aspose.OCR.  
- Configurare il motore OCR per il supporto della lingua araba.  
- Caricare un'immagine PNG ed eseguire il processo di riconoscimento.  
- Recuperare e visualizzare il testo estratto.  
- Regolare le impostazioni per una migliore accuratezza e gestire le difficoltà più comuni.

Non è necessaria alcuna esperienza pregressa con OCR, basta una conoscenza di base di C# e un ambiente di sviluppo .NET (Visual Studio, Rider o la CLI `dotnet` vanno bene).

---

## Come eseguire OCR – Configurare Aspose OCR

### Step 1: Add the Aspose.OCR NuGet Package

La prima cosa di cui abbiamo bisogno è la libreria OCR stessa. Aspose.OCR è un prodotto commerciale, ma offre una versione di prova gratuita che funziona perfettamente per scopi didattici.

```bash
# Using the .NET CLI
dotnet add package Aspose.OCR
```

In alternativa, apri il **NuGet Package Manager** in Visual Studio, cerca **Aspose.OCR** e fai clic su **Install**.

> **Pro tip:** Se prevedi di usare la libreria in una pipeline CI, aggiungi il flag `-v` per bloccare la versione, ad esempio `dotnet add package Aspose.OCR -v 23.10`.

### Step 2: Create a New Console Project (if you don’t have one)

```bash
dotnet new console -n ArabicOcrDemo
cd ArabicOcrDemo
```

Ora hai un file `Program.cs` fresco pronto per il nostro codice.

---

## Estrarre testo arabo – Scrivere il codice OCR

Di seguito trovi il programma completo, pronto all'uso. Salvalo come `Program.cs` (oppure sostituisci il file auto‑generato).

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Config;

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine instance
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // Step 2: Choose the language for recognition.
            // Here we use Arabic. You can swap this for
            // OcrLanguage.Korean, OcrLanguage.SerbianCyrillic, etc.
            // -------------------------------------------------
            ocrEngine.Language = OcrLanguage.Arabic;

            // -------------------------------------------------
            // Step 3: Load the image containing the text.
            // Replace the path with the location of your PNG.
            // -------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/arabic_sample.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // Step 4: Run the OCR process.
            // -------------------------------------------------
            ocrEngine.Recognize();

            // -------------------------------------------------
            // Step 5: Display the extracted text.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Arabic Text ===");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

#### Perché ogni riga è importante

- **`OcrEngine`**: La classe centrale che coordina il caricamento dell'immagine, la selezione della lingua e il riconoscimento.  
- **`Language = OcrLanguage.Arabic`**: L'arabo utilizza uno script da destra a sinistra e glifi unici; impostare la lingua indica al motore di applicare i modelli di caratteri corretti.  
- **`ImageStream.FromFile`**: Gestisce PNG, JPEG, BMP e molti altri formati. Se devi leggere da un `MemoryStream` (ad esempio, un file caricato), sostituisci questa chiamata di conseguenza.  
- **`Recognize()`**: Esegue il lavoro pesante—analisi dei pixel, segmentazione e classificazione dei caratteri.  
- **`ocrEngine.Text`**: La stringa Unicode finale, pronta per ulteriori elaborazioni, archiviazione o visualizzazione.

### Output previsto

Se `arabic_sample.png` contiene la frase “مرحبا بالعالم” (Hello World), la console stamperà:

```
=== Extracted Arabic Text ===
مرحبا بالعالم
```

Se l'output appare illeggibile, verifica che l'immagine sia chiara, che la lingua sia impostata su Arabo e che la versione del motore OCR corrisponda alla documentazione.

---

## Convertire immagine in testo – Ottimizzare l'accuratezza

Mentre le impostazioni predefinite funzionano per la maggior parte delle scansioni pulite, le immagini del mondo reale spesso richiedono un po' di attenzione in più.

| Impostazione | Cosa fa | Quando usarla |
|--------------|---------|---------------|
| `ocrEngine.Config.Preprocess = true` | Abilita la binarizzazione automatica e la rimozione del rumore. | Documenti scansionati con ombre. |
| `ocrEngine.Config.Deskew = true` | Ruota l'immagine per correggere una leggera inclinazione. | Foto scattate con angolo. |
| `ocrEngine.Config.PageSegMode = PageSegMode.SingleBlock` | Tratta l'intera immagine come un unico blocco di testo. | Didascalie semplici o etichette a riga singola. |
| `ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزس شصضطظعغفقكلمنهوية"` | Limita il riconoscimento solo ai caratteri arabi. | Riduce i falsi positivi su pagine multilingue. |

Puoi aggiungere queste righe subito dopo aver creato il motore:

```csharp
ocrEngine.Config.Preprocess = true;
ocrEngine.Config.Deskew = true;
ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزسشصضطظعغفقكلمنهوية";
```

---

## Leggere testo da PNG – Gestire diverse fonti di immagine

A volte il PNG si trova in un database o proviene da una richiesta web. Ecco una variante rapida che legge da un `byte[]`:

```csharp
byte[] pngBytes = File.ReadAllBytes("YOUR_DIRECTORY/arabic_sample.png");
using var ms = new MemoryStream(pngBytes);
ocrEngine.Image = ImageStream.FromStream(ms);
ocrEngine.Recognize();
Console.WriteLine(ocrEngine.Text);
```

Il resto del flusso rimane identico, il che significa che **come estrarre testo** resta coerente indipendentemente dalla fonte.

---

## Come estrarre testo – Opzioni avanzate e casi particolari

### 1. PDF o TIFF multi‑pagina

Se devi fare OCR su un documento multi‑pagina, itera su ogni pagina:

```csharp
var pdfDoc = new Aspose.Pdf.Document("multi_page.pdf");
foreach (var page in pdfDoc.Pages)
{
    using var img = page.ConvertToImage();
    ocrEngine.Image = ImageStream.FromBitmap(img);
    ocrEngine.Recognize();
    Console.WriteLine($"Page {page.Number}: {ocrEngine.Text}");
}
```

> **Nota:** Per questo snippet avrai bisogno del pacchetto `Aspose.PDF`.

### 2. Rilevamento automatico della lingua

Aspose.OCR offre anche l'auto‑rilevamento, ma è più lento. Se non sei sicuro se l'immagine contenga arabo o un altro script, abilitalo:

```csharp
ocrEngine.Language = OcrLanguage.AutoDetect;
```

Il motore proverà ogni modello linguistico e sceglierà quello più adatto.

### 3. Consigli sulle prestazioni

- **Riutilizza l'oggetto `OcrEngine`** per più immagini; creare una nuova istanza ogni volta aggiunge overhead.  
- **Esegui in parallelo** solo se hai istanze separate del motore per thread—condividere un'unica istanza causa condizioni di gara.

---

## Conclusione

Abbiamo coperto **come eseguire OCR** in C# dall'inizio alla fine, mostrandoti come **estrarre testo arabo**, **convertire immagine in testo**, **leggere testo da PNG**, e rispondere a **come estrarre testo** in una varietà di scenari. Il codice di esempio è completo, autonomo e pronto per essere incollato in qualsiasi progetto console .NET.

Passi successivi? Prova a sostituire `OcrLanguage.Arabic` con il coreano o il cirilico serbo per vedere la potenza multilingue della libreria. Sperimenta con i flag di pre‑elaborazione per migliorare l'accuratezza su scansioni rumorose, o integra la routine OCR in una API web così gli utenti possono caricare immagini e ottenere risultati testuali istantanei.

Buon coding, e che i tuoi risultati OCR siano sempre cristallini!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}