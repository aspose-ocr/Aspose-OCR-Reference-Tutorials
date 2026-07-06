---
category: general
date: 2026-02-13
description: Come utilizzare l'OCR in C# per estrarre testo da un'immagine, riconoscere
  il testo da una foto o JPG e eseguire l'OCR su un'immagine senza internet.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from photo
- recognize text from jpg
- run OCR on image
language: it
og_description: Come utilizzare l'OCR in C# per estrarre testo da un'immagine, riconoscere
  il testo da una foto e eseguire l'OCR su un'immagine con un esempio completo e funzionante.
og_title: Come usare l'OCR in C# – Estrarre il testo dall'immagine
tags:
- OCR
- C#
- Image Processing
title: Come usare l'OCR in C# – Estrarre testo da un'immagine e riconoscere il testo
  da una foto
url: /it/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-and-recognize-te/
---

final output.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come utilizzare l'OCR in C# – Estrarre testo da un'immagine e riconoscere testo da una foto

Ti sei mai chiesto **come usare l'OCR** per estrarre parole da uno screenshot, da una ricevuta scansionata o da una foto casuale scattata con il tuo telefono? Non sei il solo. In molte applicazioni reali dobbiamo trasformare le immagini in testo ricercabile, e farlo localmente—senza una connessione internet instabile—può sembrare un rompicapo.

Ecco perché questa guida ti mostra un metodo passo‑a‑passo per **estrarre testo da immagine** usando un motore OCR in C#, e copre anche come **riconoscere testo da foto**, **riconoscere testo da JPG**, e **eseguire OCR su immagine** per file che si trovano direttamente sul tuo disco. Alla fine avrai un programma completo, pronto da copiare‑incollare, che funziona subito.

## Cosa imparerai

- Come configurare un motore OCR per il cinese semplificato (o qualsiasi lingua tu inserisca).  
- Il codice esatto necessario per **caricare le risorse** da una cartella locale—senza chiamate di rete.  
- Come **riconoscere testo da foto** in file come JPEG, PNG o BMP.  
- Suggerimenti per gestire casi limite comuni come file di modello mancanti o formati immagine non supportati.  
- Un esempio completo, eseguibile, che puoi inserire in Visual Studio e vedere i risultati immediatamente.

### Prerequisiti

- .NET 6.0 o successivo (l'API usata qui punta a .NET Standard 2.0, quindi funzionano anche versioni più vecchie).  
- Familiarità di base con C# e Visual Studio (o qualsiasi IDE tu preferisca).  
- La libreria OCR che stai usando (il frammento presume una classe fittizia `OcrEngine` che viene fornita con i modelli linguistici).  
- Una cartella contenente i file modello linguistici richiesti—pensala come il “cervello” che il motore usa per leggere i caratteri cinesi.

> **Consiglio professionale:** se non hai ancora i file modello cinesi, scaricali una volta dal sito del fornitore e posizionali in una cartella come `C:\OcrResources`. Il motore non avrà più bisogno di andare online.

---

![Diagramma che mostra il processo OCR su una foto](path/to/ocr-diagram.png "Diagramma che mostra il processo OCR su una foto")

## Come usare l'OCR: Configurare il motore

La prima cosa di cui hai bisogno è un'istanza del motore OCR, configurata per la lingua di tuo interesse. In questo tutorial puntiamo al **cinese semplificato**, ma sostituire `OcrLanguage.ChineseSimplified` con `OcrLanguage.English` (o qualsiasi altro valore enum) è solo una modifica di una riga.

```csharp
using System;
using YourOcrLibrary;   // Replace with the actual namespace of your OCR SDK

// Step 1: Create and configure the OCR engine for Simplified Chinese
var ocrEngine = new OcrEngine
{
    // Primary keyword appears here naturally
    Language = OcrLanguage.ChineseSimplified,

    // Point to a folder that already contains the Chinese model files
    ResourceFolder = @"C:\OcrResources"
};
```

**Perché è importante:**  
Impostare la proprietà `Language` indica al motore quale set di caratteri aspettarsi. `ResourceFolder` è la cartella dove il motore cerca i pesi della rete neurale e i dizionari linguistici—pensala come la memoria del cervello. Se la punti alla cartella sbagliata, il motore lancerà una `FileNotFoundException` e rimarrai bloccato.

## Estrarre testo da immagine – Caricare le risorse

Prima che il motore possa effettivamente leggere qualcosa, devi caricare quei file modello in memoria. Questo passaggio è **cruciale** perché evita una chiamata di rete ogni volta che elabori un'immagine.

```csharp
// Step 2: Load the language resources from the specified folder (no internet required)
try
{
    ocrEngine.LoadResources();
    Console.WriteLine("Resources loaded successfully.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to load OCR resources: {ex.Message}");
    // In a real app you might fallback to a default language or abort gracefully
}
```

**Cosa potrebbe andare storto?**  
Se il percorso della cartella è errato o i file sono corrotti, `LoadResources()` solleverà un'eccezione. Il blocco `try/catch` sopra dimostra una gestione degli errori elegante—qualcosa di cui avrai spesso bisogno in produzione.

## Riconoscere testo da foto – Eseguire l'OCR

Ora la parte divertente: fornire un file immagine al motore e ottenere indietro il testo riconosciuto. Questo è il fulcro degli scenari **eseguire OCR su immagine**, sia che l'immagine sia un JPEG, PNG o anche un BMP.

```csharp
// Step 3: Recognize text from an image file
string imagePath = @"C:\OcrResources\photo.jpg";

try
{
    var recognitionResult = ocrEngine.RecognizeImage(imagePath);
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(recognitionResult.Text);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
}
```

Il metodo `RecognizeImage` restituisce un `RecognitionResult` (o qualunque sia il nome nella tua SDK) che tipicamente contiene:

- `Text` – la trascrizione in testo semplice.  
- `Confidence` – un punteggio numerico che indica quanto il motore è sicuro di ogni riga.  
- `BoundingBoxes` – coordinate opzionali per la posizione di ogni parola nell'immagine.

**Perché potresti interessarti alla confidenza:**  
Se stai costruendo uno strumento di automazione per l'inserimento dati, puoi impostare una soglia (ad esempio 0.85) e chiedere all'utente di confermare le righe a bassa confidenza. Questo migliora drasticamente l'accuratezza complessiva.

## Riconoscere testo da JPG – Gestire formati diversi

Molti sviluppatori presumono che l'OCR funzioni solo con PNG, ma i motori moderni gestiscono perfettamente i file **JPG**. L'unica pecca è che la compressione JPEG può introdurre artefatti che confondono il modello.

```csharp
// Bonus: Recognize text from a JPG with optional preprocessing
string jpgPath = @"C:\OcrResources\scanned_doc.jpg";

// Optional: use a simple image‑preprocess step to improve accuracy
var preprocessed = ImageHelper.DenoiseAndDeskew(jpgPath); // pseudo‑method
var result = ocrEngine.RecognizeImage(preprocessed);
Console.WriteLine($"Detected text ({result.Confidence:P0} confidence):");
Console.WriteLine(result.Text);
```

Se non disponi di un helper `DenoiseAndDeskew`, molte librerie (ad es. OpenCvSharp) forniscono quelle funzioni. Il punto chiave è: **eseguire OCR su immagine** dopo una piccola pulizia se provengono da uno scanner o da una fotocamera del telefono.

## Eseguire OCR su immagine – Suggerimenti, casi limite e migliori pratiche

### 1. Gestione della memoria
Caricare modelli linguistici di grandi dimensioni può consumare centinaia di megabyte. Disporre del motore quando hai finito:

```csharp
ocrEngine.Dispose(); // or using statement if the SDK implements IDisposable
```

### 2. Elaborazione batch
Se devi elaborare decine di foto, carica le risorse una sola volta, poi itera:

```csharp
string[] files = Directory.GetFiles(@"C:\BatchPhotos", "*.jpg");
foreach (var file in files)
{
    var res = ocrEngine.RecognizeImage(file);
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), res.Text);
}
```

### 3. Scenari multilingua
Puoi cambiare lingua al volo riassegnando `ocrEngine.Language` e chiamando nuovamente `LoadResources()`. Attento però al tempo extra di caricamento.

### 4. Gestione di risultati vuoti
A volte il motore restituisce una stringa vuota. Questo di solito significa che l'immagine è troppo sfocata o il colore del testo si confonde con lo sfondo. Un rapido controllo:

```csharp
if (string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text detected – consider increasing image contrast.");
}
```

### 5. Considerazioni sulla sicurezza
Non alimentare mai file caricati dagli utenti direttamente nel motore OCR senza una validazione. Al minimo, verifica l'estensione e la dimensione del file, e considera una scansione anti‑malware.

## Esempio completo funzionante

Di seguito trovi un programma unico e autonomo che puoi copiare in un nuovo progetto Console App. Dimostra **come usare l'OCR**, **estrarre testo da immagine**, **riconoscere testo da foto**, **riconoscere testo da JPG** e **eseguire OCR su immagine**—tutto in un unico flusso.

```csharp
// File: Program.cs
using System;
using System.IO;
using YourOcrLibrary; // Replace with actual namespace

namespace OcrDemo
{
    class Program
    {
        static void Main()
        {
            // ------------------------------
            // 1️⃣ Configure the OCR engine
            // ------------------------------
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.ChineseSimplified,
                ResourceFolder = @"C:\OcrResources"
            };

            // Load language resources (no internet needed)
            try
            {
                ocrEngine.LoadResources();
                Console.WriteLine("Resources loaded.");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Failed to load resources: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Recognize text from a photo (JPG in this case)
            // -------------------------------------------------
            string imagePath = @"C:\OcrResources\photo.jpg";

            if (!File.Exists(imagePath))
            {
                Console.Error.WriteLine($"Image not found: {imagePath}");
                return;
            }

            try
            {
                var result = ocrEngine.RecognizeImage(imagePath);
                Console.WriteLine("\n=== OCR Output ===");
                Console.WriteLine(result.Text);
                Console.WriteLine($"\nConfidence: {result.Confidence:P2}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"OCR error: {ex.Message}");
            }

            // Clean up
            ocrEngine.Dispose();
        }
    }
}
```

**Output previsto (esempio):**

```
Resources loaded.

=== OCR Output ===
中华人民共和国
北京
2026年02月13日

Confidence: 92.45%
```

Il tuo testo reale varierà in base al contenuto dell'immagine, ma dovresti vedere un blocco di caratteri Unicode stampato sulla console insieme a una percentuale di confidenza.

## Conclusione

Abbiamo percorso **come usare l'OCR** in C# dall'inizio alla fine—configurando il motore, caricando le risorse linguistiche e infine **riconoscendo testo da foto** o **JPG** senza mai toccare internet. Seguendo i passaggi sopra potrai **estrarre testo da immagine**, **eseguire OCR su immagine** e gestire le insidie più comuni che ostacolano i principianti.

Pronto per la prossima sfida? Prova a fornire al motore una pagina PDF convertita in immagine, o sperimenta con un pacchetto linguistico diverso per vedere come cambiano i punteggi di confidenza. Potresti

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}