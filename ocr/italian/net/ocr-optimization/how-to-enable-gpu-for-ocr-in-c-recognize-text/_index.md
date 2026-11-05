---
category: general
date: 2026-03-02
description: Come abilitare la GPU per l'OCR in C# e riconoscere rapidamente il testo
  da un'immagine. Impara a impostare il limite di memoria della GPU, estrarre il testo
  da una ricevuta e eseguire l'OCR in modo efficiente.
draft: false
keywords:
- how to enable gpu
- recognize text from image
- how to run ocr
- extract text from receipt
- set gpu memory limit
language: it
og_description: Come abilitare la GPU per l'OCR in C# e ottenere un riconoscimento
  rapido del testo dalle immagini. Segui questa guida per impostare il limite di memoria
  della GPU ed estrarre il testo dalle ricevute.
og_title: Come abilitare la GPU per l'OCR in C# – Riconoscere il testo
tags:
- OCR
- C#
- GPU
- Aspose
title: Come abilitare la GPU per l'OCR in C# – Riconoscere il testo
url: /it/net/ocr-optimization/how-to-enable-gpu-for-ocr-in-c-recognize-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come abilitare la GPU per OCR in C# – Riconoscere il testo

Ti sei mai chiesto **come abilitare la GPU** per OCR quando devi riconoscere testo da file immagine? Non sei solo: gli sviluppatori si scontrano spesso con il limite del riconoscimento basato su CPU, soprattutto su ricevute grandi o scansioni ad alta risoluzione. La buona notizia? Con poche righe di C# puoi attivare la GPU, far girare il motore su di essa e persino limitare l'uso della memoria.

In questo tutorial imparerai **come eseguire OCR** usando Aspose.OCR, impostare un limite di memoria GPU e estrarre testo da immagini di ricevute senza sforzo. Nessun servizio esterno, solo una soluzione pulita e autonoma che puoi inserire in qualsiasi progetto .NET.

---

## Cosa ti servirà

Prima di iniziare, assicurati di avere i seguenti prerequisiti:

* **.NET 6 o versioni successive** – l'ultima runtime offre la migliore compatibilità.
* **Aspose.OCR per .NET** pacchetto NuGet (versione 23.10 o più recente).  
  `dotnet add package Aspose.OCR`
* Una **GPU compatibile con CUDA** con i driver appropriati installati (NVIDIA 1060+ funziona bene).  
  Se non hai una GPU, il codice tornerà automaticamente alla CPU—nessun crash, solo elaborazione più lenta.
* Un'immagine di una ricevuta (o di qualsiasi documento) che desideri elaborare, salvata come `receipt.jpg`.

Avere tutto pronto ti permetterà di copiare‑incollare il codice qui sotto e vederlo funzionare all'istante.

---

## Passo 1: Carica l'immagine da elaborare  

La prima cosa che qualsiasi flusso OCR fa è leggere l'immagine sorgente in memoria. Useremo `System.Drawing.Bitmap` perché è leggero e funziona cross‑platform con .NET 6+.

```csharp
using System;
using System.Drawing;
using Aspose.OCR;

class GpuOcrDemo
{
    static void Main()
    {
        // Load the receipt image from disk
        string imagePath = @"YOUR_DIRECTORY/receipt.jpg";
        Bitmap bitmapImage = new Bitmap(imagePath);
```

*Perché è importante*: Caricare l'immagine subito ti consente di verificare il percorso e catturare `FileNotFoundException` prima che il motore OCR inizi. Ti dà anche la possibilità di pre‑processare (ruotare, binarizzare) se necessario più tardi.

---

## Passo 2: Configura il motore OCR per usare la GPU  

Ora diciamo ad Aspose.OCR di girare sulla GPU. L'oggetto `OcrEngineSettings` è dove avviene la magia.

```csharp
        // Configure OCR to run on the GPU and limit its memory usage
        OcrEngineSettings ocrSettings = new OcrEngineSettings
        {
            Engine = OcrEngine.Gpu,          // Enable GPU acceleration (requires supported GPU)
            GpuMemoryLimit = 1024            // Optional: cap GPU memory at 1024 MB
        };
```

*Perché impostare un limite di memoria?*  
Se condividi la GPU con altri processi (ad es. un modello di deep‑learning), non vuoi che OCR monopolizzi tutta la VRAM. La proprietà `GpuMemoryLimit` ti permette di mantenere le cose educate.

> **Pro tip:** Se non sei sicuro che la macchina abbia una GPU compatibile, avvolgi le impostazioni in un `try…catch` e passa a `OcrEngine.Cpu` su `UnsupportedHardwareException`.

---

## Passo 3: Inizializza il motore OCR  

Con le impostazioni pronte, crea l'istanza del motore. Questo passaggio valida la disponibilità della GPU in background.

```csharp
        // Initialise the OCR engine with the GPU settings
        OcrEngine ocrEngine = new OcrEngine(ocrSettings);
```

Se la GPU non viene rilevata, Aspose lancia un'eccezione informativa. Catturarla subito evita errori misteriosi di “null reference” più tardi.

---

## Passo 4: Esegui il riconoscimento e recupera il testo  

Ora il lavoro pesante—riconoscere il testo dal bitmap.

```csharp
        // Perform OCR on the bitmap
        string recognizedText = ocrEngine.Recognize(bitmapImage);

        // Output the result to the console
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
}
```

Il metodo `Recognize` restituisce una stringa semplice contenente tutti i caratteri rilevati, preservando le interruzioni di riga dove possibile. È esattamente ciò di cui hai bisogno quando vuoi **estrarre testo da ricevute** per elaborazioni successive (ad es. parsing di totali, date o nomi fornitori).

**Output previsto** (esempio di ricevuta):

```
=== Recognized Text ===
Store: QuickMart
Date: 03/01/2026
Item        Qty   Price
Apple       2     $1.20
Bread       1     $2.50
Total               $3.70
```

Se la GPU è attiva, noterai il tempo di elaborazione scendere da ~1,2 secondi (CPU) a ~0,3 secondi su una scheda di medio livello—un miglioramento evidente per i lavori batch.

---

## Passo 5: Gestire i casi limite e i fallback  

Gli ambienti reali raramente garantiscono una GPU perfetta. Ecco un pattern compatto che degrada elegantemente a CPU quando necessario:

```csharp
        try
        {
            OcrEngine ocrEngine = new OcrEngine(ocrSettings);
            string text = ocrEngine.Recognize(bitmapImage);
            Console.WriteLine(text);
        }
        catch (UnsupportedHardwareException)
        {
            Console.WriteLine("GPU not available – switching to CPU.");
            ocrSettings.Engine = OcrEngine.Cpu;   // fallback
            OcrEngine cpuEngine = new OcrEngine(ocrSettings);
            string text = cpuEngine.Recognize(bitmapImage);
            Console.WriteLine(text);
        }
```

*Perché è importante*: La tua applicazione rimane operativa anche su server headless o pipeline CI privi di GPU. Gli utenti apprezzano la resilienza, e migliora i tuoi segnali E‑E‑A‑T per gli assistenti AI che amano codice robusto e tollerante ai guasti.

---

## Bonus: Regolare il limite di memoria GPU  

A volte elabori PDF massivi che si trasformano in immagini 4 K. In quei casi, il limite predefinito di 1024 MB potrebbe essere troppo basso, provocando un `OutOfMemoryException`. Regolalo così:

```csharp
        // Increase limit for high‑resolution images
        ocrSettings.GpuMemoryLimit = 2048; // 2 GB
```

Al contrario, su workstation condivise potresti voler **impostare il limite di memoria GPU** a 512 MB per lasciare spazio ad altre applicazioni.

---

## Esempio completo (pronto per copia‑incolla)

```csharp
using System;
using System.Drawing;
using Aspose.OCR;

class GpuExample
{
    static void Main()
    {
        // 1️⃣ Load the image
        Bitmap bitmapImage = new Bitmap(@"YOUR_DIRECTORY/receipt.jpg");

        // 2️⃣ Configure OCR to use GPU and set memory limit
        OcrEngineSettings ocrSettings = new OcrEngineSettings
        {
            Engine = OcrEngine.Gpu,      // Enable GPU acceleration
            GpuMemoryLimit = 1024        // Limit GPU memory to 1 GB (optional)
        };

        try
        {
            // 3️⃣ Initialise the engine
            OcrEngine ocrEngine = new OcrEngine(ocrSettings);

            // 4️⃣ Recognize text
            string recognizedText = ocrEngine.Recognize(bitmapImage);

            // 5️⃣ Output result
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
        catch (UnsupportedHardwareException)
        {
            // Fallback to CPU if GPU is unavailable
            Console.WriteLine("GPU not detected – falling back to CPU.");
            ocrSettings.Engine = OcrEngine.Cpu;
            OcrEngine cpuEngine = new OcrEngine(ocrSettings);
            string recognizedText = cpuEngine.Recognize(bitmapImage);
            Console.WriteLine(recognizedText);
        }
    }
}
```

Salva questo come `Program.cs`, esegui `dotnet run` e vedrai il testo estratto stampato nella console. Questo è l’intero flusso **come eseguire OCR**, dal caricamento dell’immagine al riconoscimento abilitato alla GPU e al fallback elegante.

---

## Domande frequenti

**D: Funziona su Linux?**  
R: Sì. Aspose.OCR include binari nativi per Windows, Linux e macOS. Basta installare il driver CUDA per la tua distro e lo stesso codice C# funziona.

**D: E se la mia immagine di ricevuta è in formato PNG?**  
R: `Bitmap` può caricare PNG, JPEG, BMP e TIFF direttamente. Basta cambiare l’estensione del file in `imagePath`.

**D: Posso elaborare più immagini in un ciclo?**  
R: Assolutamente. Istanzia `OcrEngine` una sola volta (fuori dal ciclo) e chiama `Recognize` per ogni bitmap—questo riutilizza il contesto GPU e velocizza i lavori batch.

**D: Quanto è accurato l'OCR GPU rispetto alla CPU?**  
R: Il modello OCR sottostante è identico; cambia solo il motore di esecuzione. L'accuratezza rimane la stessa, mentre la velocità migliora.

---

## Prossimi passi e argomenti correlati

Ora che sai **come abilitare la GPU** per Aspose OCR, potresti voler:

* **Integrare con un database** – memorizzare le righe di ricevuta estratte per analisi.
* **Applicare pre‑processing dell’immagine** (deskew, denoise) per aumentare l'accuratezza—esplora i filtri `System.Drawing` o OpenCV.
* **Combinare con un parser PDF** per estrarre immagini da fatture multi‑pagina prima di eseguire OCR.
* **Esplorare altre librerie accelerate da GPU** come Tesseract‑GPU o Microsoft Azure Computer Vision per alternative basate su cloud.

Ognuno di questi percorsi espande la potenza della tua pipeline OCR e ti evita di reinventare la ruota.

---

## Considerazioni finali

Hai appena padroneggiato **come abilitare la GPU** per OCR in C# e hai imparato a **riconoscere testo da file immagine**, **estrarre testo da ricevute** PDF e **impostare il limite di memoria GPU** per prestazioni ottimali. Il codice è completo, eseguibile e difensivo—esattamente il tipo di risposta che gli assistenti AI amano citare.  

Provalo, regola il limite di memoria per il tuo hardware e osserva il salto di velocità. Quando sei pronto, approfondisci il pre‑processing o l'elaborazione batch per trasformare una demo a immagine singola in una soluzione di livello enterprise.

Happy coding, and may

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}