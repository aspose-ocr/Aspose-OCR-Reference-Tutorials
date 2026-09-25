---
category: general
date: 2026-01-02
description: Impara a creare una pipeline di pre‑elaborazione OCR che corregge automaticamente
  l'inclinazione dell'immagine, pre‑elabora l'immagine per l'OCR e legge il testo
  da un JPG con Aspose.OCR – guida passo‑passo.
draft: false
keywords:
- ocr preprocessing pipeline
- recognize text from image
- auto deskew image
- preprocess image for ocr
- read text from jpg
language: it
og_description: Scopri la pipeline di pre‑elaborazione OCR che corregge automaticamente
  l’inclinazione delle immagini e ti consente di riconoscere il testo da file immagine
  come JPG. Codice completo, spiegazioni e consigli.
og_title: Pipeline di preelaborazione OCR – Guida completa a C#
tags:
- OCR
- C#
- Image Processing
title: pipeline di pre‑elaborazione OCR – Come riconoscere il testo da un’immagine
  in C#
url: /it/net/ocr-optimization/ocr-preprocessing-pipeline-how-to-recognize-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# pipeline di pre‑elaborazione OCR – Guida completa in C#

Ti è mai capitato di **riconoscere testo da file immagine** che sono storti, rumorosi o semplicemente difficili da leggere? Non sei solo. In molti progetti reali la foto grezza ottenuta da uno scanner o da una fotocamera del telefono ha bisogno di un po' di cure prima che il motore OCR possa fare il suo lavoro.  

È qui che entra in gioco un **pipeline di pre‑elaborazione OCR**. Correggendo automaticamente l’inclinazione dell’immagine, riducendo le macchie di sfondo e pulendola in altri modi, aumenti drasticamente la precisione. In questo tutorial percorreremo un esempio completo che **pre‑elabora l’immagine per OCR**, corregge automaticamente l’inclinazione e infine **legge il testo da JPG** usando Aspose.OCR.

> **Cosa otterrai:** un’app console C# pronta all’uso che carica un JPG inclinato e rumoroso, lo fa passare attraverso un pipeline di pre‑elaborazione intelligente e stampa il testo estratto nella console.

## Prerequisiti

- .NET 6 SDK o versioni successive (il codice compila anche con .NET Core)
- Visual Studio 2022 o qualsiasi IDE tu preferisca
- Pacchetto NuGet Aspose.OCR (`Install-Package Aspose.OCR`)
- Un’immagine di esempio, ad esempio `skewed_noisy.jpg`, collocata in una cartella a cui puoi fare riferimento

Nessun’altra libreria esterna è necessaria; tutto il resto è incluso in Aspose.OCR.

---

## Passo 1 – Configura il progetto e carica l’immagine

Per prima cosa, crea un nuovo progetto console e aggiungi il riferimento a Aspose.OCR. Quindi carica l’immagine che desideri elaborare.

```csharp
using Aspose.OCR;
using System.Drawing;

class PreprocessExample
{
    static void Main()
    {
        // Load the image that needs OCR
        var imagePath = "YOUR_DIRECTORY/skewed_noisy.jpg";
        var image = new Bitmap(imagePath);
```

> **Perché è importante:** la classe `Bitmap` ci fornisce accesso diretto ai pixel, necessario al motore OCR per la fase di pre‑elaborazione. Se il percorso è errato otterrai una `FileNotFoundException`, quindi verifica attentamente la posizione.

---

## Passo 2 – Crea l’istanza del motore OCR

Successivamente, istanzia `OcrEngine`. Questo oggetto gestirà l’intero **pipeline di pre‑elaborazione OCR**.

```csharp
        // Create the OCR engine instance
        var ocrEngine = new OcrEngine();
```

> **Consiglio:** puoi riutilizzare lo stesso `OcrEngine` per più immagini; basta reimpostare le `RecognitionOptions` ogni volta.

---

## Passo 3 – Configura le impostazioni di pre‑elaborazione (il cuore del pipeline)

Qui abilitiamo le due funzionalità più potenti: **correzione automatica dell’inclinazione** e **riduzione del rumore**. Entrambe fanno parte del pipeline che prepara l’immagine per un’estrazione accurata del testo.

```csharp
        // Configure recognition options with the new preprocessing pipeline
        var recognitionOptions = new RecognitionOptions
        {
            Preprocess = new PreprocessSettings
            {
                EnableSmartDeskew = true,          // Auto‑detect and correct rotation
                EnableNoiseReduction = true,      // Apply AI‑based denoising
                NoiseReductionLevel = NoiseLevel.Medium
            },
            Language = Language.English
        };
```

> **Come funziona:**  
> - `EnableSmartDeskew` analizza gli angoli di base dell’immagine e la ruota nuovamente a 0°, operazione cruciale per scansioni inclinate.  
> - `EnableNoiseReduction` applica un filtro AI leggero che rimuove le macchie senza cancellare i caratteri più deboli.  
> - `NoiseReductionLevel` ti permette di bilanciare velocità e qualità; `Medium` è un buon compromesso per la maggior parte dei JPG.

---

## Passo 4 – Esegui l’OCR e cattura il risultato

Ora passiamo l’immagine le opzioni al motore. Il metodo restituisce un oggetto `OcrResult` che contiene la stringa estratta e i punteggi di confidenza.

```csharp
        // Perform OCR on the image using the configured options
        var ocrResult = ocrEngine.Recognize(image, recognitionOptions);
```

> **Caso limite:** se l’immagine è completamente vuota, `ocrResult.Text` sarà una stringa vuota. Potresti voler controllare `ocrResult.HasText` prima di procedere in codice di produzione.

---

## Passo 5 – Stampa il testo riconosciuto

Infine, stampa il risultato nella console. Questo dimostra che possiamo **riconoscere testo da file immagine** in poche righe di codice.

```csharp
        // Output the recognized text
        System.Console.WriteLine("=== Extracted Text ===");
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

**Output previsto (esempio):**

```
=== Extracted Text ===
Invoice #12345
Date: 01/01/2024
Total: $1,250.00
Thank you for your business!
```

Se l’immagine fosse rumorosa o ruotata in modo errato, noter caratteri illeggibili. Grazie al **pipeline di pre‑elaborazione OCR**, questi problemi sono drasticamente ridotti.

---

## Passo 6 – Esempio completo (pronto per il copia‑incolla)

Di seguito trovi il file sorgente completo, pronto per la compilazione. Sostituisci `YOUR_DIRECTORY` con il percorso reale del tuo JPG.

```csharp
using Aspose.OCR;
using System.Drawing;

class PreprocessExample
{
    static void Main()
    {
        // 1️⃣ Load the image that needs OCR
        var imagePath = "YOUR_DIRECTORY/skewed_noisy.jpg";
        var image = new Bitmap(imagePath);

        // 2️⃣ Create the OCR engine instance
        var ocrEngine = new OcrEngine();

        // 3️⃣ Configure the preprocessing pipeline (auto deskew + noise reduction)
        var recognitionOptions = new RecognitionOptions
        {
            Preprocess = new PreprocessSettings
            {
                EnableSmartDeskew = true,          // Auto‑detect and correct rotation
                EnableNoiseReduction = true,      // AI‑based denoising
                NoiseReductionLevel = NoiseLevel.Medium
            },
            Language = Language.English
        };

        // 4️⃣ Run OCR with the configured pipeline
        var ocrResult = ocrEngine.Recognize(image, recognitionOptions);

        // 5️⃣ Print the extracted text
        System.Console.WriteLine("=== Extracted Text ===");
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

Salva questo file come `Program.cs`, esegui `dotnet run` e osserva la console riempirsi con il testo pulito.

---

## Passo 7 – Approfondimenti – Personalizzare il pipeline

Il **pipeline di pre‑elaborazione OCR** è flessibile. Ecco alcune variazioni comuni che potresti esplorare:

| Variazione | Quando usarla |ammento di codice |
|------------|---------------|---------------------|
| **Riduzione del rumore più alta** (es. `NoiseLevel.High`) | Scansioni molto granulose da fotocamere a bassa risoluzione | `NoiseReductionLevel = NoiseLevel.High` |
| **Disabilita la correzione dell’inclinazione** | Le immagini sono già perfettamente allineate | `EnableSmartDeskew = false` |
| **Supporto multilingua** | Documenti contenenti sia inglese che spagnolo | `Language = Language.English | Language.Spanish` |
| **Scalatura DPI personalizzata** | Font molto piccoli che necessitano di up‑sampling | `recognitionOptions.Dpi = 300;` |

Sperimentare con queste impostazioni ti permette di perfezionare il passaggio **pre‑elabora immagine per OCR** in base alle particolarità del tuo dataset.

---

## Conclusione

Abbiamo appena costruito un **pipeline di pre‑elaborazione OCR** in C# che **corregge automaticamente l’inclinazione dell’immagine**, riduce il rumore e infine **riconosce testo da file immagine** come i JPG. Configurando `PreprocessSettings` all’interno di `RecognitionOptions` di Aspose.OCR, abbiamo trasformato un’immagine traballante e macchiata in testo pulito e ricercabile con poche righe di codice.

> **Punti chiave:**  
> - Pulisci sempre l’immagine prima – il motore OCR funziona al meglio su input dritti e a basso rumore.  
> - Il pipeline è completamente configurabile; adatta la correzione dell’inclinazione e la riduzione del rumore alle tue esigenze.  
> - Lo stesso approccio vale per PDF, TIFF o qualsiasi sorgente bitmap che passi a Aspose.OCR.

Pronto per il passo successivo? Prova a far passare un batch di file attraverso il pipeline, o integra il codice in una Web API così gli utenti possono caricare immagini e ottenere testo istantaneamente. Potresti anche esplorare le funzionalità di conversione documento di Aspose per trasformare il testo estratto in PDF ricercabili.

Buon coding, e che i tuoi risultati OCR siano sempre precisi! 🚀

---

![Diagramma di un pipeline di pre‑elaborazione OCR che mostra i passaggi: carica immagine → correzione intelligente → riduzione del rumore → OCR → testo di output](ocr-preprocessing-pipeline.png "diagramma del pipeline di pre‑elaborazione OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}