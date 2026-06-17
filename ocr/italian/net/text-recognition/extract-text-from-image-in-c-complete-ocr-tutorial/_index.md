---
category: general
date: 2026-06-06
description: Estrai il testo da un'immagine usando OCR in C#. Scopri come caricare
  l'immagine per l'OCR, riconoscere il documento scansionato e ottenere risultati
  accurati in pochi minuti.
draft: false
keywords:
- extract text from image
- load image for OCR
- recognize scanned document
- c# OCR tutorial
language: it
og_description: Estrai il testo da un'immagine con C#. Questo tutorial mostra come
  caricare l’immagine per OCR, riconoscere un documento scansionato e padroneggiare
  un tutorial OCR in C# passo passo.
og_title: Estrai testo da immagine in C# – Guida completa all'OCR
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from image using C# OCR. Learn how to load image for OCR,
    recognize scanned document, and get accurate results in minutes.
  headline: Extract Text from Image in C# – Complete OCR Tutorial
  type: TechArticle
- description: Extract text from image using C# OCR. Learn how to load image for OCR,
    recognize scanned document, and get accurate results in minutes.
  name: Extract Text from Image in C# – Complete OCR Tutorial
  steps:
  - name: Save the code as `Program.cs` inside a new console project.
    text: Save the code as `Program.cs` inside a new console project.
  - name: Open a terminal at the project root.
    text: Open a terminal at the project root.
  - name: Run `dotnet add package Aspose.OCR` (if you haven’t already).
    text: Run `dotnet add package Aspose.OCR` (if you haven’t already).
  - name: 'Build and execute:'
    text: 'Build and execute:'
  type: HowTo
- questions:
  - answer: Yes—most OCR libraries let you load a PDF page as an image stream or expose
      a `PdfDocument` API. Convert each page to an image first, then follow the same
      steps.
    question: Can I process PDFs directly?
  - answer: The `ImageStream.FromFile` method supports JPEG, PNG, BMP, and TIFF out
      of the box. No extra conversion required.
    question: What if my image is in PNG format?
  - answer: Handwriting is a tougher nut to crack. Look for a library that offers
      a “handwriting” model, or pre‑process the image with binarization and noise
      removal before feeding it to the engine.
    question: How do I improve accuracy for handwritten notes?
  - answer: 'Absolutely. Most engines expose a `Rect` or `Region` property where you
      can limit OCR to a bounding box—great for forms with fixed fields. --- ## Next
      Steps & Related Topics Now that you’ve mastered the basics of **extract text
      from image** with a **c# OCR tutorial**, consider exploring: - **Batch p'
    question: Is there a way to extract text in a specific region?
  type: FAQPage
tags:
- OCR
- C#
- Image Processing
title: Estrai testo da immagine in C# – Tutorial completo di OCR
url: /it/net/text-recognition/extract-text-from-image-in-c-complete-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai testo da immagine in C# – Tutorial OCR completo

Ti sei mai chiesto come **estrarre testo da un'immagine** usando solo poche righe di C#? Non sei l'unico. Molti sviluppatori si trovano in difficoltà quando devono estrarre parole da una scansione rumorosa e inclinata, e i soliti trucchi di “copia‑incolla” non bastano.  

In questa guida percorreremo un pratico **c# OCR tutorial** che mostra come **load image for OCR**, abilitare un pre‑processamento intelligente e, infine, **recognize scanned document** il contenuto con precisione cristallina. Alla fine avrai un programma eseguibile da inserire in qualsiasi progetto .NET.

## Cosa copre questo tutorial

- Installare il pacchetto NuGet Aspose.OCR (o compatibile)  
- Creare e configurare un'istanza del motore OCR  
- **Load image for OCR** – gestione dei percorsi file, stream e problemi comuni  
- Abilitare il pre‑processamento automatico per correggere inclinazione, rumore e problemi di contrasto  
- **Recognize scanned document** – recuperare il risultato in testo semplice  
- Codice sorgente completo da copiare‑incollare ed eseguire immediatamente  

Non è necessaria alcuna esperienza pregressa con OCR; basta una conoscenza di base di C# e Visual Studio (o del tuo IDE preferito).  

> **Perché importa?** L'automazione dell'estrazione del testo apre porte a elaborazione di fatture, PDF ricercabili, riduzione dell'inserimento dati e persino set di dati pronti per l'AI.  

![estrarre testo da immagine usando C# OCR](/images/extract-text-from-image-csharp.png "estrarre testo da immagine")

## Prerequisiti

- .NET 6.0 SDK o successivo (il codice funziona anche con .NET Framework 4.8)  
- Visual Studio 2022 (l'edizione Community va bene)  
- Pacchetto NuGet `Aspose.OCR` (o qualsiasi libreria che espone `OcrEngine`, `OcrResult`, ecc.)  

Se non hai ancora installato il pacchetto, esegui:

```bash
dotnet add package Aspose.OCR
```

---

## Passo 1: Creare un'istanza del motore OCR

La prima cosa da fare è avviare il motore che farà il lavoro pesante. Pensa a `OcrEngine` come al cervello dell'operazione—una volta attivo, puoi fornirgli immagini e richiedere il testo.

```csharp
using Aspose.OCR;          // Namespace for OCR classes
using Aspose.OCR.Image;    // For ImageStream helper

// Step 1: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

> **Consiglio professionale:** Mantieni il motore come singleton se stai elaborando molte immagini in batch; riutilizza le risorse interne e velocizza il processo.

## Passo 2: Abilitare il Pre‑processamento Automatico

Le scansioni del mondo reale raramente sono perfette. Sono inclinate, rumorose o con scarso contrasto. Abilitare `AutoPreprocess` indica al motore di correggere automaticamente l'inclinazione, rimuovere il rumore e regolare il contrasto prima ancora di analizzare i caratteri.

```csharp
// Step 2: Enable automatic preprocessing (deskew, denoise, contrast adjustment)
ocrEngine.Config.AutoPreprocess = true;
```

Perché è importante? Senza pre‑processamento, il motore OCR potrebbe leggere “8” come “B” o perdere completamente una riga. Il passaggio automatico ti salva dallo scrivere codice personalizzato per la pulizia delle immagini.

## Passo 3: Impostare la lingua di riconoscimento

La maggior parte delle librerie OCR include pacchetti linguistici. Qui impostiamo l'inglese, ma puoi passare a `OcrLanguage.French`, `OcrLanguage.Spanish`, ecc., a seconda del tuo documento.

```csharp
// Step 3: Set the language for recognition
ocrEngine.Language = OcrLanguage.English;
```

Se il tuo documento scansionato contiene lingue miste, puoi eseguire il motore due volte o utilizzare un modello multilingue—qualcosa da esplorare in seguito.

## Passo 4: Caricare l'immagine per OCR

Ora **load image for OCR**. L'helper `ImageStream.FromFile` legge il file in un formato comprensibile dal motore. Assicurati che il percorso punti a un file reale; i percorsi relativi funzionano quando esegui dal folder del progetto.

```csharp
// Step 4: Load the image to be processed
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");
```

> **Errore comune:** Usare un percorso con spazi senza racchiuderlo tra virgolette può causare una `FileNotFoundException`. Verifica sempre che il file esista con `File.Exists` prima di passarlo al motore.

## Passo 5: Eseguire il riconoscimento OCR

Con tutto configurato, finalmente **recognize scanned document** il contenuto. Il metodo `Recognize` fa il lavoro pesante e restituisce un oggetto `OcrResult` che contiene il testo estratto e i punteggi di confidenza.

```csharp
// Step 5: Perform OCR recognition
OcrResult ocrResult = ocrEngine.Recognize();
```

Se ti serve il livello di confidenza per ogni riga, puoi ispezionare `ocrResult.Confidence` (un float tra 0 e 1). Bassa confidenza? Considera di modificare le impostazioni di pre‑processamento o fornire un'immagine a risoluzione più alta.

## Passo 6: Output del testo riconosciuto

Il modo più semplice per verificare il successo è stampare il testo sulla console. In un'app reale probabilmente lo scriveresti su un file, un database o lo invieresti a un altro servizio.

```csharp
// Step 6: Output the recognized text
Console.WriteLine(ocrResult.Text);
```

Eseguendo il programma dovrebbe stampare qualcosa del genere:

```
The quick brown fox jumps over the lazy dog.
```

Anche se l'immagine originale era leggermente inclinata o rumorosa, il pre‑processamento automatico dovrebbe averla pulita a sufficienza per un output corretto.

---

## Codice sorgente completo – Un esempio pronto all'esecuzione

Di seguito trovi il programma completo che puoi copiare in un nuovo progetto console (`dotnet new console`). Include tutti i passaggi sopra, più una piccola gestione degli errori per rendere il tutorial robusto.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Image;

namespace ExtractTextFromImageDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Validate input argument
            if (args.Length == 0)
            {
                Console.WriteLine("Usage: dotnet run <image-path>");
                return;
            }

            string imagePath = args[0];

            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found at '{imagePath}'");
                return;
            }

            try
            {
                // Step 1: Create OCR engine
                OcrEngine ocrEngine = new OcrEngine();

                // Step 2: Enable auto‑preprocess (deskew, denoise, contrast)
                ocrEngine.Config.AutoPreprocess = true;

                // Step 3: Choose language (English in this case)
                ocrEngine.Language = OcrLanguage.English;

                // Step 4: Load image for OCR
                ocrEngine.Image = ImageStream.FromFile(imagePath);

                // Step 5: Recognize scanned document
                OcrResult result = ocrEngine.Recognize();

                // Step 6: Output the extracted text
                Console.WriteLine("\n--- Extracted Text ---\n");
                Console.WriteLine(result.Text);
                Console.WriteLine("\n--- End of Output ---\n");

                // Optional: Show confidence if you need it
                Console.WriteLine($"Overall confidence: {result.Confidence:P2}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"OCR failed: {ex.Message}");
            }
        }
    }
}
```

### Come eseguire

1. Salva il codice come `Program.cs` all'interno di un nuovo progetto console.  
2. Apri un terminale nella radice del progetto.  
3. Esegui `dotnet add package Aspose.OCR` (se non l'hai già fatto).  
4. Compila ed esegui:  

   ```bash
   dotnet run "C:\Images\invoice_scanned.jpg"
   ```

Dovresti vedere il testo estratto stampato sulla console, insieme a una percentuale di confidenza complessiva.

---

## Domande frequenti (FAQ)

**D: Posso elaborare PDF direttamente?**  
R: Sì—la maggior parte delle librerie OCR ti permette di caricare una pagina PDF come stream immagine o espone un'API `PdfDocument`. Converti prima ogni pagina in immagine, poi segui gli stessi passaggi.

**D: E se la mia immagine è in formato PNG?**  
R: Il metodo `ImageStream.FromFile` supporta JPEG, PNG, BMP e TIFF nativamente. Non è necessaria alcuna conversione aggiuntiva.

**D: Come posso migliorare l'accuratezza per appunti scritti a mano?**  
R: La scrittura a mano è una sfida più difficile. Cerca una libreria che offra un modello “handwriting”, o pre‑processa l'immagine con binarizzazione e rimozione del rumore prima di passarla al motore.

**D: Esiste un modo per estrarre testo in una regione specifica?**  
R: Assolutamente. La maggior parte dei motori espone una proprietà `Rect` o `Region` dove puoi limitare l'OCR a un riquadro—ideale per moduli con campi fissi.

---

## Prossimi passi e argomenti correlati

Ora che hai padroneggiato le basi di **extract text from image** con un **c# OCR tutorial**, considera di esplorare:

- **Batch processing** – iterare su una directory di immagini e scrivere ogni risultato in un file CSV.  
- **PDF generation** – combinare il testo estratto con una libreria PDF per creare PDF ricercabili.  
- **Machine‑learning post‑processing** – utilizzare correttori ortografici o modelli linguistici per pulire gli errori OCR.  

Ognuno di questi si basa sui concetti fondamentali trattati: caricare un'immagine per OCR, configurare il motore e riconoscere un documento scansionato.

---

## Conclusione

Abbiamo appena percorso un esempio completo, end‑to‑end, che mostra come **extract text from image** in C#. Dalla creazione di `OcrEngine` all'output della stringa finale, ogni riga di codice è spiegata e pronta all'esecuzione.  

Se segui i passaggi, potrai trasformare scansioni rumorose, ricevute o appunti scritti a mano in testo ricercabile e modificabile in pochi secondi. Continua a sperimentare—modifica le impostazioni di pre‑processamento, cambia lingua o passa al motore un batch di file. Il mondo dell'elaborazione automatica dei documenti è a tua disposizione.  

Hai altre domande o un caso d'uso interessante da condividere? Lascia un commento qui sotto, e buona programmazione!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Estrarre testo da immagine usando Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Estrarre testo da immagine C# con selezione della lingua usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Estrarre testo da immagine – Ottimizzazione OCR con Aspose.OCR per .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}