---
category: general
date: 2025-12-29
description: Impara come fare OCR su file PDF in C# ed estrarre il testo dalle pagine
  PDF. Questo tutorial copre anche la conversione da PDF a testo e le tecniche per
  leggere le pagine PDF in C#.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf to text
- extract pdf text c#
- read pdf page c#
language: it
og_description: Come eseguire OCR su PDF in C# spiegato in una guida concisa. Ottieni
  il codice completo per estrarre testo da PDF, convertire PDF in testo e leggere
  la pagina PDF in C#.
og_title: Come eseguire OCR su PDF in C# – Guida completa di programmazione
tags:
- OCR
- C#
- PDF processing
title: Come eseguire OCR su PDF in C# – Guida passo passo
url: /it/net/text-recognition/how-to-ocr-pdf-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come fare OCR di PDF in C# – Guida passo‑passo

Ti sei mai chiesto **how to OCR PDF** direttamente dalla tua applicazione C#? Forse hai una pila di fatture scansionate e devi estrarre il testo senza dover copiare‑incollare manualmente. È un problema comune, soprattutto quando i PDF sono basati su immagini e l'estrazione tradizionale di testo fallisce.  

In questo tutorial ti guideremo attraverso una soluzione completa, pronta all'uso, che non solo mostra **how to OCR PDF**, ma dimostra anche come *extract text from PDF*, *convert PDF to text* e *read PDF page C#* usando la libreria Aspose.OCR. Nessun riferimento vago—solo il codice che puoi inserire in Visual Studio e iniziare a sperimentare.

## Di cosa avrai bisogno

- **.NET 6.0** o versioni successive (il codice funziona anche su .NET Framework 4.7+)  
- Pacchetto NuGet **Aspose.OCR** – installa con `dotnet add package Aspose.OCR`  
- Un PDF scansionato (ad es. `invoice.pdf`) posizionato in una cartella a cui puoi fare riferimento  
- Familiarità di base con le app console C#  

Questo è tutto. Se hai già un progetto, aggiungi semplicemente il pacchetto e sei pronto per partire.

## Passo 1: Configura il progetto e aggiungi Aspose.OCR

Per prima cosa, crea un nuovo progetto console (o usa uno esistente) e includi la libreria OCR.

```csharp
// Create a new console app (run this in a terminal)
// > dotnet new console -n OcrPdfDemo
// > cd OcrPdfDemo
// > dotnet add package Aspose.OCR
```

Perché questo passo è importante: Aspose.OCR gestisce il lavoro pesante di analisi delle immagini, rilevamento del layout e riconoscimento dei caratteri. Senza di essa dovresti assemblare un rasterizzatore, un motore Tesseract e molto codice di collegamento.

## Passo 2: Importa i namespace e prepara il motore OCR

Ora apri `Program.cs` (o qualsiasi file .cs preferisci) e aggiungi le direttive `using` richieste.

```csharp
using System;
using Aspose.OCR;   // Core OCR classes
```

Creare il motore è semplice, ma configureremo anche un paio di opzioni che migliorano la precisione su scansioni tipiche di fatture.

```csharp
// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    // Enable automatic language detection (optional but handy)
    Language = Language.English,
    // Turn on deskew to correct rotated pages
    ImagePreprocessingOptions = new ImagePreprocessingOptions
    {
        Deskew = true,
        Binarization = true
    }
};
```

**Pro tip:** Se conosci la lingua in anticipo, imposta `Language` esplicitamente; velocizza il processo.

## Passo 3: Indica il file PDF

Specifica il percorso assoluto o relativo al PDF che desideri elaborare. Per questo esempio supponiamo che il file si trovi in una cartella chiamata `Samples`.

```csharp
// Path to the PDF you want to OCR
string pdfFilePath = @"Samples/invoice.pdf";

// Verify the file exists early to avoid runtime surprises
if (!System.IO.File.Exists(pdfFilePath))
{
    Console.WriteLine($"File not found: {pdfFilePath}");
    return;
}
```

Verificare l'esistenza del file è un piccolo passo, ma ti salva da eccezioni criptiche in seguito.

## Passo 4: Scegli la/e pagina/e da leggere

Un PDF può contenere decine di pagine, ma spesso ne serve solo una specifica—ad esempio la seconda pagina di una fattura dove è indicato l'importo totale. Il metodo `RecognizePdf` ti permette di puntare a una singola pagina o all'intero documento.

```csharp
// Extract text from page 2 (page numbers are 1‑based)
int pageNumber = 2;

// The method returns an OcrResult containing the recognized text
OcrResult ocrResult = ocrEngine.RecognizePdf(pdfFilePath, pageNumber);
```

Se vuoi *convert PDF to text* per l'intero documento, basta omettere l'argomento `pageNumber`:

```csharp
// OcrResult fullResult = ocrEngine.RecognizePdf(pdfFilePath);
```

## Passo 5: Visualizza o salva il testo estratto

Ora che il motore OCR ha completato il suo lavoro, puoi stampare il testo sulla console, scriverlo in un file `.txt` o inviarlo a un altro sistema (ad es. un database).

```csharp
// Show the recognized text in the console
Console.WriteLine("=== OCR Result (Page {0}) ===", pageNumber);
Console.WriteLine(ocrResult.Text);

// Optionally, save to a .txt file
string outputPath = $"output_page{pageNumber}.txt";
System.IO.File.WriteAllText(outputPath, ocrResult.Text);
Console.WriteLine($"Text saved to {outputPath}");
```

**Why this matters:** Persistendo l'output crei un artefatto riutilizzabile—perfetto per analisi successive o indicizzazione di ricerca.

## Esempio completo funzionante

Mettendo tutto insieme, ecco un programma autonomo che puoi copiare‑incollare in `Program.cs` ed eseguire subito.

```csharp
using System;
using Aspose.OCR;

namespace OcrPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine with helpful options
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English,
                ImagePreprocessingOptions = new ImagePreprocessingOptions
                {
                    Deskew = true,
                    Binarization = true
                }
            };

            // 2️⃣ Define the PDF path
            string pdfFilePath = @"Samples/invoice.pdf";
            if (!System.IO.File.Exists(pdfFilePath))
            {
                Console.WriteLine($"Error: File not found -> {pdfFilePath}");
                return;
            }

            // 3️⃣ Choose which page to OCR (change as needed)
            int pageNumber = 2; // read PDF page C# example

            // 4️⃣ Perform OCR on the selected page
            OcrResult ocrResult = ocrEngine.RecognizePdf(pdfFilePath, pageNumber);

            // 5️⃣ Output the result
            Console.WriteLine($"--- OCR Result for page {pageNumber} ---");
            Console.WriteLine(ocrResult.Text);

            // 6️⃣ Save to a text file for later use
            string outputPath = $"output_page{pageNumber}.txt";
            System.IO.File.WriteAllText(outputPath, ocrResult.Text);
            Console.WriteLine($"Extracted text saved to: {outputPath}");
        }
    }
}
```

### Output previsto

```
--- OCR Result for page 2 ---
Invoice #12345
Date: 2024‑11‑30
Total: $1,250.00
...
Extracted text saved to: output_page2.txt
```

Se il PDF contiene scansioni chiare e ad alta risoluzione, l'output sarà quasi perfetto. Immagini di qualità inferiore potrebbero richiedere pre‑elaborazione aggiuntiva (ad es. aumentare DPI o applicare filtri); le `ImagePreprocessingOptions` di Aspose.OCR possono essere regolate per questi scenari.

## Domande comuni e casi particolari

### 1️⃣ E se il PDF è protetto da password?

L'overload `RecognizePdf` di Aspose.OCR accetta un oggetto `PdfLoadOptions` dove puoi impostare la password:

```csharp
var loadOptions = new PdfLoadOptions { Password = "mySecret" };
OcrResult result = ocrEngine.RecognizePdf(pdfFilePath, pageNumber, loadOptions);
```

### 2️⃣ Posso fare OCR dell'intero documento in un'unica operazione?

Sì—basta chiamare `RecognizePdf(pdfFilePath)` senza specificare un numero di pagina. Il metodo restituisce un unico `OcrResult` contenente il testo concatenato di tutte le pagine.

### 3️⃣ In che modo differisce da “estrarre testo da PDF” usando una libreria basata su testo?

L'estrazione di testo puro (ad es. con iTextSharp) funziona solo su PDF che contengono già testo selezionabile. **How to OCR PDF** è necessario quando il PDF è essenzialmente una raccolta di immagini, come le fatture scansionate. In questi casi, il motore OCR esegue il riconoscimento ottico dei caratteri per trasformare le immagini in testo ricercabile.

### 4️⃣ E per le prestazioni su PDF di grandi dimensioni?

Il tempo di elaborazione scala approssimativamente in modo lineare con il numero di pagine e la risoluzione dell'immagine. Per lavori in batch, considera:
- Eseguire OCR in parallelo (`Parallel.ForEach`)  
- Ridurre DPI dell'immagine prima dell'OCR (`Resolution = 150`)  
- Cacheare l'istanza `OcrEngine` invece di ricrearla per ogni file

### 5️⃣ È possibile ottenere le bounding box di ogni parola?

`OcrResult` espone una collezione di oggetti `OcrRegion`, ognuno dei quali contiene le coordinate. Puoi iterare su di essi per creare PDF ricercabili o evidenziare i risultati in un'interfaccia UI.

```csharp
foreach (var region in ocrResult.Regions)
{
    Console.WriteLine($"{region.Text} – ({region.Bounds.X}, {region.Bounds.Y}, {region.Bounds.Width}, {region.Bounds.Height})");
}
```

## Consigli per implementazioni pronte per la produzione

- **Error handling:** Avvolgi le chiamate OCR in blocchi try/catch per gestire le eccezioni specifiche della libreria.  
- **Logging:** Registra numeri di pagina e tempi di elaborazione; aiutano a individuare scansioni problematiche.  
- **Memory management:** Rilascia gli oggetti `Bitmap` di grandi dimensioni se converti manualmente le pagine PDF in immagini prima dell'OCR.  
- **Security:** Non memorizzare PDF grezzi su dischi non sicuri; considera lo streaming diretto verso il motore OCR.  

## Conclusione

Ora disponi di una risposta completa, end‑to‑end, a **how to OCR PDF** usando C#. Il tutorial ha coperto tutto, dall'installazione di Aspose.OCR, alla selezione di una pagina specifica, all'estrazione del testo e alla gestione dei casi particolari più comuni. Con questa base puoi *extract text from PDF*, *convert PDF to text* e *read PDF page C#* per qualsiasi pipeline di elaborazione documenti tu stia costruendo.

Pronto per il passo successivo? Prova a inviare l'output OCR a un motore di ricerca full‑text come Lucene.NET, o genera PDF ricercabili sovrapponendo il testo riconosciuto alle immagini originali. Il cielo è il limite, e ora hai gli strumenti per arrivarci.

---

![esempio di come fare OCR di PDF](image-placeholder.png "Illustrazione dell'elaborazione OCR su una pagina PDF")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}