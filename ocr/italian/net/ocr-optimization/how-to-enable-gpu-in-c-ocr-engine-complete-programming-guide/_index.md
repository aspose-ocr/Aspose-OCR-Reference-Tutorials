---
category: general
date: 2026-06-06
description: Come abilitare la GPU in un motore OCR C# e riconoscere rapidamente il
  testo da un'immagine. Scopri come eseguire l'OCR, caricare un'immagine per l'OCR
  e utilizzare il motore OCR C# in pochi minuti.
draft: false
keywords:
- how to enable gpu
- how to perform ocr
- recognize text from image
- load image for ocr
- use ocr engine c#
language: it
og_description: Come abilitare la GPU in un motore OCR C#. Questo tutorial mostra
  come eseguire l'OCR, caricare un'immagine per l'OCR e riconoscere il testo dall'immagine
  usando il motore OCR C#.
og_title: Come abilitare la GPU nel motore OCR C# – Guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to enable GPU in a C# OCR engine and quickly recognize text from
    image. Learn how to perform OCR, load image for OCR, and use OCR engine C# in
    minutes.
  headline: How to Enable GPU in C# OCR Engine – Complete Programming Guide
  type: TechArticle
tags:
- OCR
- C#
- GPU
title: Come abilitare la GPU nel motore OCR C# – Guida completa alla programmazione
url: /it/net/ocr-optimization/how-to-enable-gpu-in-c-ocr-engine-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come abilitare la GPU in un motore OCR C# – Guida completa di programmazione

Ti sei mai chiesto **come abilitare la GPU** quando esegui un carico di lavoro OCR in C#? Non sei l'unico—gli sviluppatori si scontrano costantemente con la lentezza dell'elaborazione solo CPU, soprattutto con scansioni ad alta risoluzione.  

La buona notizia? Attivare l'accelerazione GPU è un gioco da ragazzi, e una volta avviata puoi **eseguire OCR**, **caricare immagine per OCR** e **riconoscere testo da immagine** in un attimo. In questa guida percorreremo ogni passaggio, dall'installazione dei pacchetti giusti alla stampa del testo finale, mantenendo il codice pulito e funzionante.

Tratteremo anche alcuni scenari “cosa succede se”: cosa succede se hai più GPU? Cosa succede se il formato dell'immagine non è supportato? Alla fine avrai uno snippet solido, pronto per la produzione, che mostra esattamente **come abilitare la GPU** e ottenere risultati di cui ti puoi fidare.

## Prerequisiti

- .NET 6.0 o successivo (l'esempio utilizza le istruzioni di livello superiore per brevità)
- Una libreria OCR che supporta la GPU (ad es., *MyOcrLib* – sostituisci con lo spazio dei nomi del tuo fornitore)
- Almeno una GPU compatibile CUDA con driver installati
- Un'immagine di esempio (JPEG/PNG) posizionata in una cartella a cui puoi fare riferimento

Se ti manca qualcuno di questi, scarica l'ultimo driver NVIDIA e aggiungi il pacchetto NuGet:

```bash
dotnet add package MyOcrLib --version 2.3.1
```

Ora, immergiamoci.

## Passo 1: Come abilitare la GPU nel tuo motore OCR C#

La prima cosa da fare è attivare l'interruttore GPU sull'oggetto di configurazione del motore. La maggior parte dei moderni SDK OCR espone una proprietà `Config` dove puoi impostare `GpuEnabled`, `GpuDeviceId` e, opzionalmente, la modalità di precisione per ottenere velocità extra.

```csharp
// Create the OCR engine instance
var ocrEngine = new MyOcrLib.OcrEngine();

// Enable GPU acceleration
ocrEngine.Config.GpuEnabled = true;                     // Turn on GPU mode
ocrEngine.Config.GpuDeviceId = 0;                       // Choose the first GPU (0‑based index)
ocrEngine.Config.GpuPrecision = GpuPrecision.Float16; // Optional: lower precision for less memory usage
```

**Perché è importante:** L'accelerazione GPU sposta i calcoli matriciali pesanti dalla CPU, permettendo al processore grafico di elaborare migliaia di pixel in parallelo. Su una RTX 3060 di fascia media puoi vedere un aumento di velocità di 3‑5× rispetto alla modalità solo CPU.

> **Consiglio professionale:** Se hai più di una GPU, sperimenta con `GpuDeviceId = 1` (o superiore) per bilanciare il carico tra le schede.

## Passo 2: Caricare immagine per OCR in C#

Prima che il motore possa leggere qualcosa, devi fornirgli uno stream di immagine. L'SDK solitamente offre un helper come `ImageStream.FromFile`. Assicurati che il percorso sia corretto e che il file sia accessibile.

```csharp
// Load the image you want to process
ocrEngine.Image = MyOcrLib.ImageStream.FromFile(@"C:\OCRSamples\sample1.jpg");

// Quick sanity check – ensure the image was loaded
if (ocrEngine.Image == null)
{
    Console.WriteLine("Failed to load image. Check the file path and format.");
    return;
}
```

**Caso limite:** Alcune librerie non gestiscono bene i JPEG CMYK. Se ottieni un'eccezione, converti prima l'immagine in RGB usando `System.Drawing` o `ImageSharp`.

## Passo 3: Impostare la lingua ed eseguire OCR

La maggior parte dei motori OCR ha bisogno di sapere quale modello linguistico utilizzare. L'inglese è il predefinito in molti kit, ma puoi passare al francese, spagnolo, ecc., con un singolo cambiamento di enum.

```csharp
// Choose the language for recognition
ocrEngine.Language = OcrLanguage.English; // Change to OcrLanguage.Spanish for Spanish text
```

Ora eseguiamo effettivamente la pipeline di riconoscimento. Questo è il momento in cui **come eseguire OCR** si traduce in una chiamata concreta.

```csharp
// Run the OCR process – this will automatically use the GPU because we enabled it earlier
var ocrResult = ocrEngine.Recognize();
```

Se la chiamata restituisce `null` o genera un'eccezione, verifica che i driver GPU siano aggiornati e che i file modello siano presenti nella directory prevista.

## Passo 4: Riconoscere testo da immagine e stampare il risultato

Il metodo `Recognize` ti restituisce un oggetto che tipicamente contiene una proprietà `Text`, più i punteggi di confidenza per ogni riga. Stampiamo il testo semplice sulla console.

```csharp
// Output the recognized text
if (ocrResult?.Text != null)
{
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(ocrResult.Text);
}
else
{
    Console.WriteLine("OCR failed to produce any text.");
}
```

**Cosa vedrai:** Per una pagina scansionata nitida l'output dovrebbe essere quasi perfetto. Se noti caratteri illeggibili, considera di aumentare il DPI dell'immagine (300 dpi è un valore ottimale) o di riportare `GpuPrecision` a `Float32` per maggiore accuratezza.

### Output console previsto (esempio)

```
=== OCR Output ===
The quick brown fox jumps over the lazy dog.
```

## Passo 5: Problemi comuni e ottimizzazioni delle prestazioni

| Sintomo | Probabile causa | Soluzione |
|---------|----------------|-----------|
| **GPU non utilizzata** (picchi di uso CPU) | `GpuEnabled` lasciato `false` o driver mancante | Verifica che `ocrEngine.Config.GpuEnabled` sia `true` ed esegui `nvidia-smi` per vedere il processo |
| **Errore out‑of‑memory** | Uso di `Float16` su un'immagine molto grande | Passa a `GpuPrecision.Float32` o ridimensiona l'immagine prima di inviarla |
| **Bassa accuratezza** | Modello linguistico errato o DPI basso | Imposta correttamente `ocrEngine.Language` e assicurati che l'immagine sia ≥300 dpi |
| **Crash su PDF multi‑pagina** | Il motore si aspetta un'unica immagine | Itera su ogni pagina, creando un nuovo `ImageStream` per ogni iterazione |

**Suggerimento extra:** Avvolgi la chiamata OCR in un `Task.Run` se devi mantenere l'interfaccia UI reattiva. Il lavoro sulla GPU viene eseguito su un thread separato, ma il pool di thread .NET rimane bloccato a meno che non lo deleghi.

```csharp
var ocrResult = await Task.Run(() => ocrEngine.Recognize());
```

## Passo 6: Esempio completo funzionante (pronto per copia‑incolla)

Di seguito trovi un programma autonomo che puoi inserire in un'app console. Include le direttive `using`, la gestione degli errori e un `Console.ReadKey()` finale così puoi vedere l'output prima che la finestra si chiuda.

```csharp
using System;
using MyOcrLib;               // Replace with the actual namespace of your OCR library
using MyOcrLib.Enums;        // For GpuPrecision and OcrLanguage

// ------------------------------------------------------------
// How to Enable GPU, Load Image, Perform OCR, and Get Text
// ------------------------------------------------------------
var ocrEngine = new OcrEngine();

// 1️⃣ Enable GPU acceleration
ocrEngine.Config.GpuEnabled = true;
ocrEngine.Config.GpuDeviceId = 0;                 // First GPU
ocrEngine.Config.GpuPrecision = GpuPrecision.Float16;

// 2️⃣ Load the image for OCR
string imagePath = @"C:\OCRSamples\sample1.jpg";
ocrEngine.Image = ImageStream.FromFile(imagePath);

if (ocrEngine.Image == null)
{
    Console.WriteLine("❌ Unable to load image. Check the path.");
    return;
}

// 3️⃣ Set language (how to perform OCR)
ocrEngine.Language = OcrLanguage.English;

// 4️⃣ Run OCR – this uses the GPU because we enabled it
var ocrResult = ocrEngine.Recognize();

if (ocrResult?.Text != null)
{
    Console.WriteLine("\n=== Recognized Text ===");
    Console.WriteLine(ocrResult.Text);
}
else
{
    Console.WriteLine("\n⚠️ OCR returned no text.");
}

// Keep console open
Console.WriteLine("\nPress any key to exit...");
Console.ReadKey();
```

Esegui il programma con `dotnet run` e dovresti vedere il testo estratto stampato sulla console. Se sostituisci `imagePath` con un file diverso, la stessa pipeline funziona—ricorda solo di adeguare la lingua se necessario.

## Conclusione

Abbiamo coperto **come abilitare la GPU** in un motore OCR C#, mostrato come **caricare immagine per OCR**, spiegato **come eseguire OCR** e dimostrato il modo più semplice per **riconoscere testo da immagine** usando l'API `OCR engine C#`. L'esempio completo alla fine collega tutto, così puoi copiare, incollare e vedere la GPU accelerare l'estrazione del testo all'istante.

Pronto per il livello successivo? Prova a elaborare un batch di immagini con un ciclo `Parallel.ForEach`, sperimenta diverse impostazioni `GpuPrecision` o passa a un modello multilingue per ampliare le capacità della tua app.  

Se incontri problemi o hai idee per miglioramenti, lascia un commento—buona programmazione!  

![come abilitare gpu nel motore OCR](/images/ocr-gpu-setup.png "Diagramma che mostra la pipeline OCR con GPU abilitata – come abilitare gpu")

---


## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come fare OCR su un'immagine – Eseguire OCR su immagine in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [Come usare Aspose per riconoscere un'immagine dallo stream in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Come impostare il valore di soglia in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}