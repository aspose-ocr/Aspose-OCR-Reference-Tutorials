---
category: general
date: 2026-05-28
description: Esegui OCR sull'immagine usando C# per leggere il testo dall'immagine
  ed estrarre rapidamente il testo dallo scontrino. Scopri le opzioni GPU e le tecniche
  di caricamento.
draft: false
keywords:
- run ocr on image
- read text from image
- extract text from receipt
- load image for ocr
language: it
og_description: Esegui OCR su un'immagine con C#. Questo tutorial ti mostra come leggere
  il testo da un'immagine, estrarre il testo da una ricevuta e ottimizzare l'uso della
  GPU.
og_title: Esegui OCR su immagine – Guida completa C#
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Run OCR on image using C# to read text from image and extract text
    from receipt fast. Learn GPU options and loading techniques.
  headline: Run OCR on Image – Complete C# Guide
  type: TechArticle
- description: Run OCR on image using C# to read text from image and extract text
    from receipt fast. Learn GPU options and loading techniques.
  name: Run OCR on Image – Complete C# Guide
  steps:
  - name: '**Batch processing:** Re‑use a single `OcrEngine` instance for a batch
      of images; it caches language models and reduces latency.'
    text: '**Batch processing:** Re‑use a single `OcrEngine` instance for a batch
      of images; it caches language models and reduces latency.'
  - name: '**Pre‑filtering:** Apply a simple grayscale conversion and contrast boost
      before handing the image to the engine—many libraries expose a `Preprocess`
      method.'
    text: '**Pre‑filtering:** Apply a simple grayscale conversion and contrast boost
      before handing the image to the engine—many libraries expose a `Preprocess`
      method.'
  - name: '**Error logging:** Capture `ocrEngine.LastError` (if available) after each
      `Recognize()` call to diagnose failures without crashing your service.'
    text: '**Error logging:** Capture `ocrEngine.LastError` (if available) after each
      `Recognize()` call to diagnose failures without crashing your service.'
  - name: '**Thread safety:** Most OCR engines are **not** thread‑safe. If you need
      parallelism, create a separate engine per thread or use a concurrency queue.'
    text: '**Thread safety:** Most OCR engines are **not** thread‑safe. If you need
      parallelism, create a separate engine per thread or use a concurrency queue.'
  type: HowTo
tags:
- OCR
- C#
- Image Processing
- Computer Vision
title: Esegui OCR su immagine – Guida completa C#
url: /it/net/ocr-optimization/run-ocr-on-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esegui OCR su Immagine – Guida Completa in C#

Hai mai avuto bisogno di **eseguire OCR su immagine** ma non sapevi da dove cominciare? Non sei solo; molti sviluppatori si trovano di fronte a questo ostacolo al loro primo tentativo di leggere testo da dati immagine. La buona notizia è che, con poche righe di C#, puoi estrarre testo da scansioni di ricevute, PDF o qualsiasi foto tu voglia. In questa guida percorreremo un esempio completo, pronto‑da‑eseguire, che mostra anche come **caricare immagine per OCR**, sfruttare l’accelerazione GPU e limitare in modo sicuro l’uso della memoria.

Al termine di questo tutorial sarai in grado di:

* Inizializzare un motore OCR in C#  
* **Caricare immagine per OCR** da disco o da uno stream  
* **Leggere testo da immagine** con supporto GPU opzionale  
* **Estrarre testo da ricevuta** e stamparlo sulla console  

Nessun servizio esterno richiesto—solo una libreria locale e un’immagine di esempio di una ricevuta.

---

## Cosa Ti Serve

| Prerequisito | Motivo |
|--------------|--------|
| .NET 6.0 SDK o successivo | Runtime moderno, supporta le ultime funzionalità del linguaggio |
| Una libreria OCR che espone una classe `OcrEngine` (es. IronOCR, wrapper .NET di Tesseract) | Fornisce i metodi `Configuration` e `Recognize` usati di seguito |
| Una GPU abilitata CUDA (opzionale) | Consente il flag `EnableGpu` per una elaborazione più veloce |
| Un’immagine di esempio di una ricevuta (`receipt.jpg`) | Dimostra il passaggio **estrarre testo da ricevuta** |
| Qualsiasi IDE C# (Visual Studio, Rider, VS Code) | Per compilare e fare debug rapidamente |

Se non hai una GPU, il codice tornerà semplicemente alla modalità CPU—nessun problema.

---

![Run OCR on image example output](https://example.com/ocr-output.png "Run OCR on image – sample console output")

*Testo alternativo: Esempio di output di Run OCR on image che mostra il testo della ricevuta riconosciuto.*

---

## Passo 1: Esegui OCR su Immagine – Configurazione del Motore

Prima di tutto: crea un'istanza del motore OCR. Questo oggetto è il cuore del processo; contiene tutti i dettagli di configurazione e svolge il lavoro pesante.

```csharp
using System;
using OcrLibrary;   // Replace with the actual namespace of your OCR package

// Step 1: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

*Perché è importante:* La classe `OcrEngine` incapsula il motore OCR nativo (Tesseract, IronOCR, ecc.). Instanziarla una sola volta e riutilizzarla su più immagini riduce l'overhead e ti offre un unico punto dove modificare le impostazioni.

---

## Passo 2: Carica Immagine per OCR

Prima che il motore possa leggere qualcosa, devi fornirgli un'immagine. La proprietà `Image` della libreria accetta uno stream o un percorso file, a seconda dell'implementazione.

```csharp
// Step 2: Load the image to be processed
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

*Consiglio:* Se gestisci upload da parte degli utenti, avvolgi questo codice in un `try/catch` e valida prima il tipo di file. Formati non supportati genereranno un'eccezione che può essere gestita in modo elegante.

---

## Passo 3: Abilita Accelerazione GPU (Opzionale)

Se il tuo computer dispone di un runtime CUDA o OpenCL compatibile, attivare la modalità GPU può ridurre di alcuni secondi ogni passaggio di riconoscimento.

```csharp
// Step 3: Enable GPU acceleration (requires CUDA/OpenCL runtime)
ocrEngine.Configuration.EnableGpu = true;
```

*Pro tip:* Non tutte le GPU sono uguali. Su schede più vecchie potresti notare un leggero rallentamento a causa del sovraccarico del driver. Prova entrambe le modalità (`EnableGpu = true/false`) per capire quale funziona meglio con il tuo hardware.

---

## Passo 4: Limita l'Uso della Memoria GPU (Opzionale)

A volte non vuoi che il processo OCR consumi tutta la memoria GPU, specialmente se la condividi con altri carichi di lavoro come inferenza di deep‑learning.

```csharp
// Step 4: (Optional) Limit the amount of GPU memory the engine can use (in MB)
ocrEngine.Configuration.GpuMemoryLimit = 1024; // 1 GB limit
```

*Quando usarlo:* Se gestisci un servizio web che elabora molte immagini contemporaneamente, limitare la memoria evita crash per out‑of‑memory.

---

## Passo 5: Riconosci Testo e Leggi Testo da Immagine

Ora il motore è pronto per svolgere il suo compito. Chiamare `Recognize()` avvia la pipeline OCR e restituisce la stringa estratta.

```csharp
// Step 5: Perform OCR and retrieve the recognized text
string recognizedText = ocrEngine.Recognize();
```

*Perché è il cuore:* Questa singola riga nasconde una cascata di pre‑elaborazione (binarizzazione, deskew) e la classificazione reale dei caratteri. Il `recognizedText` restituito è Unicode puro, pronto per ulteriori elaborazioni.

---

## Passo 6: Estrarre Testo da Ricevuta – Output

Infine, scrivi il risultato sulla console o salvalo dove ti serve. Per una ricevuta, potresti in seguito analizzare le righe di articoli, i totali o le date.

```csharp
// Step 6: Output the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

**Output console previsto (troncato per brevità):**

```
=== OCR Result ===
Store Name
123 Main St.
Date: 04/27/2026
Item   Qty   Price
Apple   2    1.20
Bread   1    2.50
Total          3.70
Thank you!
```

Se l'OCR fatica con un layout di ricevuta particolare, considera di regolare le opzioni di pre‑elaborazione (es. `ocrEngine.Configuration.Deskew = true`) o fornire un'immagine a risoluzione più alta.

---

## Casi Limite Comuni & Come Gestirli

| Situazione | Correzione Suggerita |
|-----------|----------------------|
| **Immagine nulla** – `ocrEngine.Image` è `null` | Valida il percorso file prima dell'assegnazione; lancia un chiaro `ArgumentException` se mancante. |
| **GPU non disponibile** – `EnableGpu = true` genera `PlatformNotSupportedException` | Avvolgi la chiamata di abilitazione GPU in un `try/catch` e passa alla modalità CPU. |
| **Ricevute grandi ( > 10 MB )** causano pressione sulla memoria | Usa `GpuMemoryLimit` o elabora l'immagine a tasselli (`ocrEngine.Configuration.TileSize`). |
| **Rilevamento lingua errato** – l'output contiene spazzatura | Imposta `ocrEngine.Configuration.Language = "eng"` (o il codice ISO appropriato) per forzare l'inglese. |

---

## Pro Tips per OCR Pronto alla Produzione

1. **Elaborazione batch:** Riutilizza una singola istanza di `OcrEngine` per un lotto di immagini; memorizza nella cache i modelli linguistici e riduce la latenza.  
2. **Pre‑filtraggio:** Applica una semplice conversione in scala di grigi e un aumento del contrasto prima di passare l'immagine al motore—molte librerie espongono un metodo `Preprocess`.  
3. **Log degli errori:** Cattura `ocrEngine.LastError` (se disponibile) dopo ogni chiamata a `Recognize()` per diagnosticare i fallimenti senza far crashare il servizio.  
4. **Sicurezza dei thread:** La maggior parte dei motori OCR **non** è thread‑safe. Se ti serve il parallelismo, crea un motore separato per thread o utilizza una coda di concorrenza.

---

## Conclusione

Abbiamo appena percorso un flusso completo di **eseguire OCR su immagine** in C#. Dalla creazione del motore, **caricare immagine per OCR**, attivare l’accelerazione GPU, fino a **estrarre testo da ricevuta**, ora disponi di una solida base per costruire pipeline di elaborazione documenti più sofisticate.

I prossimi passi potrebbero includere:

* Analizzare il testo della ricevuta in JSON strutturato (usando regex o una libreria di linguaggio naturale) – ottimo per l’automazione di **leggere testo da immagine**.  
* Integrare il passaggio OCR in un'API ASP .NET Core così gli utenti possono caricare ricevute via HTTP.  
* Sperimentare con diversi back‑end OCR (Tesseract vs SDK commerciali) per confrontare l'accuratezza.

Provalo con diversi layout di ricevute, regola la configurazione e vedrai quanto rapidamente puoi trasformare una foto sfocata in dati utili. Buon coding, e che le tue immagini siano sempre nitide!

## Tutorial Correlati

- [Estrarre testo da immagine C# con selezione della lingua usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Estrarre Testo da Immagine – Ottimizzazione OCR con Aspose.OCR per .NET](/ocr/english/net/ocr-optimization/)
- [Come Estrarre Testo da Immagine Preparando Rettangoli in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}