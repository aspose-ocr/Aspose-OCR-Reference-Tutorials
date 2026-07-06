---
category: general
date: 2026-02-22
description: come eseguire OCR su un'immagine con Aspose OCR – rimuovere il rumore
  dell'immagine, aumentare il contrasto e estrarre il testo dell'immagine in C# rapidamente.
draft: false
keywords:
- how to ocr image
- remove image noise
- boost image contrast
- extract text image
- recognize image text
language: it
og_description: Scopri come eseguire l'OCR di un'immagine con Aspose OCR, rimuovere
  il rumore, aumentare il contrasto ed estrarre il testo dall'immagine in C# con un
  esempio completo, pronto all'uso.
og_title: come fare OCR su un'immagine – aumenta il contrasto e rimuovi il rumore
tags:
- OCR
- C#
- Image Processing
title: 'Come fare OCR su un''immagine: aumentare il contrasto, rimuovere il rumore'
url: /it/net/ocr-optimization/how-to-ocr-image-boost-contrast-remove-noise/
---

placeholders unchanged.

Let's craft translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# come fare OCR su immagine – Aumenta il contrasto e rimuovi il rumore in C#

Ti sei mai chiesto **come fare OCR su immagine** quando i file sono inclinati, granulosi o semplicemente difficili da leggere? Non sei solo. In molti progetti reali—ad esempio la scansione di ricevute o la digitalizzazione di documenti vecchi—l’immagine grezza raramente è perfetta. La buona notizia? Con poche righe di C# e Aspose OCR puoi **rimuovere il rumore dell’immagine**, **aumentare il contrasto dell’immagine** e infine **estrarre il testo dall’immagine** senza sforzo.

In questo tutorial percorreremo una soluzione completa, end‑to‑end. Alla fine saprai esattamente come configurare il motore OCR, pulire un’immagine rumorosa e **riconoscere il testo dell’immagine** così da poter inviare il risultato dove ti serve. Niente riferimenti vaghi, solo un esempio di codice eseguibile e la motivazione dietro ogni scelta.

## Cosa ti serve

- .NET 6+ (o .NET Core 3.1+ – l’API è la stessa)
- Pacchetto NuGet Aspose.OCR (`Install-Package Aspose.OCR`)
- Un’immagine di esempio che sia inclinata e rumorosa (ad es., `skewed_noisy.jpg`)
- Qualsiasi IDE ti piaccia – Visual Studio, Rider o VS Code vanno bene

Tutto qui. Se hai questi elementi, possiamo passare subito al codice.

![how to ocr image example](/images/ocr-demo.png){alt="esempio di come fare OCR su immagine"}

## Passo 1: Inizializzare il motore OCR – come fare OCR su immagine correttamente  

La prima cosa da fare è creare un’istanza di `OcrEngine` e indicare quale lingua ci si aspetta. L’inglese è la più comune, ma Aspose supporta decine di lingue out of the box.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // Create the OCR engine and set the language to English.
        var ocrEngine = new OcrEngine { Language = Language.English };
```

**Perché è importante:** Il motore deve conoscere il set di caratteri; altrimenti sprecherà cicli a indovinare e la precisione diminuirà. Impostare la lingua in anticipo riduce anche l’uso di memoria perché il motore carica solo i dati linguistici necessari.

## Passo 2: Caricare l’immagine e iniziare a rimuovere il rumore  

Successivamente carichiamo l’immagine dal disco. Nella maggior parte dei casi il file è un JPEG o PNG che contiene molto granulo. Caricarla in un oggetto `Image` ci fornisce un handle da passare attraverso i filtri.

```csharp
        // Load the input image (skewed and noisy)
        var inputImage = Image.Load(@"YOUR_DIRECTORY/skewed_noisy.jpg");
```

**Consiglio professionale:** Se la tua immagine si trova in un bucket cloud, puoi streammarla direttamente con `Image.Load(Stream)`. In questo modo eviti di scrivere un file temporaneo.

## Passo 3: Applicare una catena di filtri – aumentare il contrasto e pulire il rumore  

Aspose OCR fornisce una comoda pipeline di filtri. Qui concatenamo tre filtri:

1. **DeskewFilter** – corregge la rotazione così il testo è orizzontale.  
2. **DenoiseFilter** – rimuove il granulo senza sfocare le lettere.  
3. **ContrastFilter** – amplifica la differenza tra primo piano e sfondo, facendo risaltare i caratteri più deboli.

```csharp
        // Pre‑process the image with a chain of filters
        var processedImage = inputImage
            .Apply(new DeskewFilter())          // correct rotation
            .Apply(new DenoiseFilter())         // reduce grain
            .Apply(new ContrastFilter(1.5f));   // boost contrast
```

**Perché questi filtri?**  
- **Deskew** è essenziale per un OCR accurato; anche pochi gradi di inclinazione possono dimezzare il tasso di riconoscimento.  
- **Denoise** affronta il problema del “rimuovere il rumore dell’immagine” tipico delle scansioni con fotocamera dello smartphone.  
- **Contrast** è il segreto per documenti a basso contrasto—pensa a ricevute sbiadite.  

Puoi regolare il fattore di `ContrastFilter` (il valore predefinito è `1.0f`). Valori superiori a `1.5f` possono sovra‑esporre l’immagine, quindi sperimenta con qualche prova.

## Passo 4: Riconoscere il testo dell’immagine – il cuore di come fare OCR su immagine  

Ora che l’immagine è pulita, la passiamo al motore OCR.

```csharp
        // Recognize text from the processed image
        var ocrResult = ocrEngine.Recognize(processedImage);
```

Il metodo `Recognize` restituisce un oggetto `OcrResult` contenente la stringa estratta, i punteggi di confidenza e persino le bounding box se ti servono per evidenziare.

**Caso limite:** Se l’immagine contiene più lingue, puoi impostare `ocrEngine.Language = Language.English | Language.Spanish;`. Il motore proverà entrambe le dizioni.

## Passo 5: Visualizzare e verificare – estrarre il testo dall’immagine per la tua app  

Infine, stampiamo il testo sulla console. In un’app reale potresti scriverlo in un database, in un file o alimentarlo a una pipeline NLP a valle.

```csharp
        // Display the extracted text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Output previsto:**  

```
=== OCR Result ===
Invoice #12345
Date: 2024‑01‑15
Total: $256.78
Thank you for your business!
```

Se vedi caratteri incomprensibili, torna al Passo 3 e regola i parametri dei filtri. Spesso un fattore di contrasto più alto o un ulteriore `SharpenFilter` risolve il problema.

## Domande frequenti e consigli  

### E se la mia immagine è già in bianco‑nero?  
Puoi saltare il `ContrastFilter` e usare solo `DenoiseFilter`. Un contrasto eccessivo su un’immagine binaria può creare artefatti.

### Come gestire file molto grandi (>10 MB)?  
Carica l’immagine a una risoluzione inferiore (`Image.Load(path, new LoadOptions { DesiredWidth = 2000 })`) prima di filtrare. Il motore OCR funziona bene con versioni ridotte finché il testo rimane leggibile.

### Posso eseguire questo in una Web API?  
Assolutamente. Avvolgi la stessa logica in un controller ASP.NET Core, accetta un `IFormFile` e restituisci il risultato OCR come JSON. Ricorda di rilasciare gli oggetti `Image` per

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}