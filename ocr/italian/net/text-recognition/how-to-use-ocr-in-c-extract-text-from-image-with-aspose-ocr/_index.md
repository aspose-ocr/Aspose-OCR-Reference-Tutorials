---
category: general
date: 2026-02-24
description: Come utilizzare l'OCR in C# per estrarre testo da file immagine. Impara
  a convertire PNG in testo, leggere le immagini in modo asincrono e gestire le insidie
  comuni.
draft: false
keywords:
- how to use OCR
- extract text from image
- convert png to text
- how to extract text
- how to read image
language: it
og_description: Come utilizzare l'OCR in C# per estrarre testo dalle immagini. Questa
  guida mostra passo‑passo l'OCR asincrono con Aspose, coprendo la conversione, la
  gestione degli errori e le migliori pratiche.
og_title: Come utilizzare OCR in C# – Guida completa
tags:
- OCR
- C#
- Aspose
title: Come utilizzare l'OCR in C# – Estrarre il testo da un'immagine con Aspose OCR
url: /it/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come usare OCR in C# – Estrarre testo da un'immagine

Ti sei mai chiesto **come usare OCR** per estrarre testo da un'immagine senza doverlo digitare manualmente? Non sei solo. Molti sviluppatori si trovano in difficoltà quando devono *estrarre testo da un'immagine* da file come PNG, e il solito approccio copia‑incolla semplicemente non è sufficiente.  

In questo tutorial percorreremo una soluzione completa e asincrona che **converte PNG in testo** usando la libreria Aspose.OCR. Alla fine saprai esattamente come leggere i file immagine, gestire gli errori e integrare il risultato nelle tue applicazioni.  

Copriremo tutto, dall'installazione del pacchetto NuGet alla messa a punto del motore OCR per una maggiore precisione, e inseriremo consigli su cosa fare quando l'immagine non è perfettamente nitida. Non è necessario inseguire link alla documentazione—tutto ciò che ti serve è qui.

## Di cosa avrai bisogno

- .NET 6.0 o versioni successive (il codice funziona anche su .NET Core e .NET Framework)  
- Visual Studio 2022 (o qualsiasi IDE preferisci)  
- Il pacchetto NuGet **Aspose.OCR** (`Install-Package Aspose.OCR`)  
- Un file immagine (PNG, JPG, BMP) che vuoi elaborare – lo chiameremo `input.png`

È tutto. Se hai spuntato queste caselle, sei pronto per iniziare.

![Diagramma che mostra il flusso di lavoro OCR – come usare OCR per estrarre testo da un'immagine](/images/ocr-workflow.png)

## Passo 1: Installa Aspose.OCR e aggiungi i namespace

Per prima cosa, aggiungi la libreria al tuo progetto. Apri la console di Package Manager e esegui:

```powershell
Install-Package Aspose.OCR
```

Quindi, nella parte superiore del tuo file C#, includi i namespace necessari:

```csharp
using Aspose.OCR;
using System;
using System.Threading.Tasks;
```

> **Consiglio professionale:** Se stai usando le API minime di .NET 6, puoi inserire queste istruzioni `using` in un file globale così da non ripeterle in più classi.

### Perché è importante

Il namespace `Aspose.OCR` ti dà accesso a `OcrEngine`, la classe principale che effettivamente legge l'immagine. Senza di esso, dovresti scrivere il tuo codice di analisi dei pixel—un buco nero enorme. Aggiungere i namespace mantiene il codice ordinato e indica al compilatore dove trovare i tipi che utilizzerai.

## Passo 2: Crea un motore OCR asincrono

Avvolgeremo la chiamata OCR in un metodo `async` così la tua UI rimane reattiva e il codice lato server può scalare. Ecco lo scheletro di un'app console:

```csharp
class AsyncExample
{
    static async Task Main()
    {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Recognize text from the image asynchronously
        OcrResult ocrResult = await ocrEngine.RecognizeImageAsync("YOUR_DIRECTORY/input.png");

        // Output the extracted text
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Spiegazione

- **`OcrEngine ocrEngine = new OcrEngine();`** – Istanzia il motore con le impostazioni predefinite. Puoi successivamente modificare lingua, modalità di rilevamento o filtri di pre‑elaborazione.  
- **`await ocrEngine.RecognizeImageAsync(...)`** – Il metodo asincrono restituisce un `Task<OcrResult>`. Attenderlo libera il thread mentre l'OCR viene eseguito in background.  
- **`ocrResult.Text`** – La rappresentazione in plain‑text di tutto ciò che il motore è riuscito a leggere. Questo è il fulcro di *come estrarre testo* da un'immagine.

## Passo 3: Ottimizza il motore per una migliore accuratezza

L'OCR pronto all'uso funziona bene su immagini pulite e ad alto contrasto, ma le foto del mondo reale spesso hanno bisogno di un piccolo aiuto. Puoi regolare alcune proprietà prima di chiamare `RecognizeImageAsync`:

```csharp
// Set language (English is default, but you can add more)
ocrEngine.Language = OcrLanguage.English;

// Enable automatic image preprocessing (deskew, despeckle)
ocrEngine.ImagePreprocessingOptions = ImagePreprocessingOptions.Auto;

// If you only need numbers, restrict the character set
ocrEngine.Characters = "0123456789";
```

### Quando usare queste impostazioni

- **Scansioni a bassa qualità** – Attiva `ImagePreprocessingOptions.Auto` per consentire ad Aspose di eliminare il rumore.  
- **PDF multilingue** – Cambia `Language` in `OcrLanguage.French` o combina lingue con una maschera di bit.  
- **Campi modulo** – Limita `Characters` a cifre o lettere maiuscole per ridurre i falsi positivi.

## Passo 4: Gestisci gli errori in modo elegante

L'OCR non è magico; può fallire se il file è mancante, corrotto o in un formato non supportato. Avvolgi la chiamata asincrona in un blocco try/catch:

```csharp
try
{
    OcrResult ocrResult = await ocrEngine.RecognizeImageAsync("YOUR_DIRECTORY/input.png");
    Console.WriteLine("Extracted Text:");
    Console.WriteLine(ocrResult.Text);
}
catch (FileNotFoundException ex)
{
    Console.Error.WriteLine($"File not found: {ex.Message}");
}
catch (OcrException ex)
{
    Console.Error.WriteLine($"OCR failed: {ex.Message}");
}
```

### Perché questo è utile

Fornire messaggi di errore chiari accelera il debug e migliora l'esperienza dell'utente finale. Invece di un arresto generico, ottieni un prompt utile che ti indica se controllare il percorso, il formato del file o la configurazione del motore OCR.

## Passo 5: Metti tutto insieme – Esempio completo funzionante

Di seguito trovi un programma console completo, pronto per l'esecuzione, che dimostra **come usare OCR**, applica la pre‑elaborazione e gestisce gli errori. Copialo e incollalo in un nuovo `.csproj` e premi F5.

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Threading.Tasks;

class AsyncOcrDemo
{
    static async Task Main()
    {
        // 1️⃣  Initialize the OCR engine with optional tweaks
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            ImagePreprocessingOptions = ImagePreprocessingOptions.Auto
        };

        // 2️⃣  Define the path to the image you want to read
        string imagePath = Path.Combine(Environment.CurrentDirectory, "input.png");

        // 3️⃣  Perform the async recognition inside a safe try/catch
        try
        {
            OcrResult result = await ocrEngine.RecognizeImageAsync(imagePath);
            Console.WriteLine("\n--- Extracted Text ---\n");
            Console.WriteLine(result.Text);
            Console.WriteLine("\n--- End of Output ---\n");
        }
        catch (FileNotFoundException fnf)
        {
            Console.Error.WriteLine($"❌ Image not found: {fnf.Message}");
        }
        catch (OcrException ocrEx)
        {
            Console.Error.WriteLine($"❌ OCR processing error: {ocrEx.Message}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Unexpected error: {ex.Message}");
        }
    }
}
```

**Output previsto** (supponendo che `input.png` contenga la frase “Hello World”):

```
--- Extracted Text ---

Hello World

--- End of Output ---
```

Se l'immagine è sfocata, potresti vedere caratteri extra o parole mancanti—ecco dove le opzioni di pre‑elaborazione del Passo 3 diventano cruciali.

## Passo 6: Estendere la soluzione – Da PNG a PDF o file di testo

A volte è necessario **convertire PNG in testo** e poi salvare il risultato in un file `.txt` o incorporarlo in un report PDF. Ecco un breve snippet che scrive l'output OCR in un file:

```csharp
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.txt");
await File.WriteAllTextAsync(outputPath, result.Text);
Console.WriteLine($"✅ Text saved to {outputPath}");
```

Oppure, se stai generando un PDF con Aspose.PDF:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// ... after OCR result is obtained
Document pdfDoc = new Document();
Page page = pdfDoc.Pages.Add();
TextFragment fragment = new TextFragment(result.Text);
page.Paragraphs.Add(fragment);
pdfDoc.Save("Result.pdf");
Console.WriteLine("✅ PDF created with extracted text.");
```

Queste estensioni illustrano come **come leggere i dati immagine** possa alimentare processi a valle—generazione di report, indicizzazione di ricerca o anche l'alimentazione di un modello linguistico.

## Domande comuni e casi limite

| Question | Answer |
|----------|--------|
| *Quali formati immagine sono supportati?* | Aspose.OCR gestisce PNG, JPEG, BMP, TIFF e GIF. Se hai un PDF, estrai prima le sue pagine come immagini. |
| *Posso elaborare più immagini in parallelo?* | Sì—avvolgi ogni chiamata `RecognizeImageAsync` in un proprio task e usa `Task.WhenAll`. Fai solo attenzione all'uso della memoria. |
| *Cosa succede se l'OCR restituisce testo vuoto?* | Controlla la qualità dell'immagine: basso contrasto o testo ruotato spesso falliscono. Abilita `ImagePreprocessingOptions.Deskew` o ruota manualmente l'immagine prima dell'OCR. |
| *C'è un limite alle dimensioni dell'immagine?* | Immagini grandi (>10 MP) possono causare `OutOfMemoryException`. Ridimensionale a una risoluzione ragionevole (ad es., 300 DPI) prima del riconoscimento. |
| *Ho bisogno di una licenza per Aspose.OCR?* | La modalità di sviluppo funziona con una licenza temporanea, ma per la produzione avrai bisogno di una licenza acquistata per rimuovere le filigrane di valutazione. |

## Suggerimenti sulle prestazioni

- **Riutilizza l'istanza `OcrEngine`** per l'elaborazione batch; creare un nuovo motore per immagine aggiunge overhead.  
- **Disattiva le lingue non utilizzate** per velocizzare il rilevamento—ogni lingua extra aggiunge un piccolo costo di elaborazione.  
- **Esegui l'OCR su un thread in background** (come mostrato) per mantenere reattivi i thread UI in applicazioni desktop o web.

## Conclusione

Abbiamo coperto **come usare OCR** in C# dall'inizio alla fine: installazione di Aspose.OCR, scrittura di un metodo asincrono, messa a punto delle impostazioni per immagini rumorose, gestione degli errori e persistenza dei risultati. Ora hai un modo affidabile per *estrarre testo da file immagine*, *convertire PNG in testo*, e persino alimentare quel testo in altri flussi di lavoro come la generazione di PDF.

Pronto per la prossima sfida? Prova a inserire l'output OCR in un indice ricercabile di Azure Cognitive Search, o sperimenta l'OCR multilingue aggiungendo `OcrLanguage.Spanish | OcrLanguage.French` al motore. Il cielo è il limite quando sai **come leggere i dati immagine** in modo programmatico.

---

*Se hai trovato utile questa guida, metti una stella su GitHub, condividila con i colleghi, o lascia un commento qui sotto con i tuoi trucchi OCR. Buon coding!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}