---
category: general
date: 2026-03-05
description: Come usare l'OCR in C# per estrarre testo da un'immagine. Impara a convertire
  l'immagine in testo, leggere i caratteri coreani e caricare l'immagine per l'OCR
  rapidamente.
draft: false
keywords:
- how to use OCR
- extract text from image
- convert image to text
- read korean characters
- load image for OCR
language: it
og_description: Come utilizzare l'OCR in C# ed estrarre istantaneamente il testo da
  un'immagine. Questa guida mostra come convertire un'immagine in testo, leggere i
  caratteri coreani e caricare l'immagine per l'OCR.
og_title: Come usare OCR in C# – Estrarre testo da un'immagine
tags:
- OCR
- C#
- Aspose
title: Come utilizzare l'OCR in C# – Estrarre testo da un'immagine
url: /it/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come utilizzare OCR in C# – Estrarre testo da un'immagine

Ti sei mai chiesto **come utilizzare OCR** quando hai uno screenshot pieno di testo coreano e ti serve la stringa semplice? Non sei l'unico a grattarsi la testa per questo. In questo tutorial passeremo in rassegna un esempio completo, pronto‑da‑eseguire, che **estrae testo da un'immagine**, **converte immagine in testo**, e mostra anche come **leggere caratteri coreani** con Aspose.OCR.

Tratteremo anche il passaggio spesso trascurato di **caricare l'immagine per OCR** così non ti troverai di fronte a un “file non trovato” in seguito. Alla fine avrai un programma autonomo da inserire in qualsiasi progetto .NET.

## Di cosa avrai bisogno

- .NET 6+ (o .NET Framework 4.7.2 e versioni successive) – il codice funziona su entrambi.  
- Aspose.OCR per .NET – puoi scaricare una versione di prova gratuita dal sito di Aspose.  
- Un'immagine di esempio (`korean_doc.png`) che contiene testo coreano.  
- Il tuo IDE preferito (Visual Studio, Rider, VS Code – quello che preferisci).  

Nessuna altra libreria di terze parti è necessaria.

## Passo 1: Configura il progetto e aggiungi Aspose.OCR

First, create a new console app:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Then add the Aspose.OCR NuGet package:

```bash
dotnet add package Aspose.OCR
```

> **Consiglio professionale:** Se hai un file di licenza, posizionalo nella radice del progetto; altrimenti la versione di prova funzionerà ma aggiungerà una filigrana all'output.

## Passo 2: Come utilizzare OCR – Inizializzare il motore

Ora scriveremo il codice C#. La prima cosa da fare quando **come utilizzare OCR** è istanziare `OcrEngine`. Questo oggetto è il cuore della libreria; contiene tutte le impostazioni di cui avrai bisogno più avanti.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: apply your license to remove trial limitations
            // Replace the path with the actual location of your .lic file
            ocrEngine.SetLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

**Perché è importante:** Senza un'istanza corretta del motore non puoi impostare la lingua, caricare immagini o recuperare i risultati. Il motore gestisce anche le risorse interne, quindi crearne uno una sola volta e riutilizzarlo è più efficiente che costruire nuovi oggetti ripetutamente.

## Passo 3: Scegliere la lingua – Leggere i caratteri coreani

La riga successiva indica al motore quale lingua cercare. Poiché il nostro obiettivo è **leggere i caratteri coreani**, impostiamo `OcrLanguage.Korean`. Puoi sostituirla con Arabo, Thai, Gujarati, ecc., a seconda del tuo caso d'uso.

```csharp
            // Step 3: Tell the engine which language to recognize
            ocrEngine.Language = OcrLanguage.Korean; // alternatives: Arabic, Thai, Gujarati, etc.
```

**Perché è importante:** La selezione della lingua migliora notevolmente l'accuratezza. Il motore OCR utilizza dizionari e modelli di caratteri specifici per lingua; fornire la lingua sbagliata può produrre output incomprensibili.

## Passo 4: Caricare l'immagine per OCR – Convertire immagine in testo

Prima che il motore possa fare qualsiasi lavoro, devi **caricare l'immagine per OCR**. Il metodo `ImageStream.FromFile` legge il file in un formato che il motore comprende.

```csharp
            // Step 4: Load the image that contains the text
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/korean_doc.png");
```

Se l'immagine si trova in una cartella diversa, basta modificare il percorso. Ricorda di impostare l'*Azione di compilazione* del file su “Copy if newer” così l'eseguibile può trovarla a runtime.

> **Errore comune:** Fornire un percorso con backslash (`\`) in una stringa letterale senza escape causerà un errore di compilazione. Usa doppi backslash (`\\`) o una stringa verbatim (`@"C:\path\file.png"`).

## Passo 5: Eseguire OCR – Estrarre testo dall'immagine

Ora avviene il lavoro pesante. Chiamare `Recognize()` esegue l'algoritmo OCR, e la proprietà `Text` ti restituisce la stringa grezza.

```csharp
            // Step 5: Run OCR and get the recognized text
            string recognizedText = ocrEngine.Recognize().Text;
```

A questo punto hai **estratto testo dall'immagine** e, in pratica, **convertito immagine in testo**. Il risultato può contenere caratteri di nuova riga se il layout originale aveva interruzioni di linea.

## Passo 6: Mostrare il risultato – Verificare l'output

Infine, stampiamo il risultato sulla console così puoi verificare che funzioni.

```csharp
            // Step 6: Output the result to the console
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

Run the program:

```bash
dotnet run
```

### Output previsto

```
=== Recognized Text ===
안녕하세요. 이것은 OCR 테스트 문서입니다.
```

Se vedi caratteri coreani simili a quelli dell'immagine, congratulazioni—hai padroneggiato **come utilizzare OCR** con Aspose.OCR!

![how to use OCR example diagram](image.png)

*Testo alternativo immagine: diagramma di esempio su come utilizzare OCR che mostra il flusso dal caricamento di un'immagine alla stampa del testo riconosciuto.*

## Casi limite e variazioni

### 1. Gestire più pagine

Se devi **estrarre testo da un'immagine** che contiene più pagine (ad esempio un TIFF multi‑pagina), itera su ogni pagina e chiama `Recognize()` per ogni istanza di `ImageStream`.

### 2. Gestire scansioni di bassa qualità

Le immagini a bassa risoluzione possono ridurre l'accuratezza. Prima di chiamare `Recognize()`, puoi migliorare l'immagine con gli strumenti di pre‑elaborazione di Aspose:

```csharp
ocrEngine.Image = ImageProcessing.Preprocess(ocrEngine.Image, ImageProcessingOptions.Deskew);
```

### 3. Cambiare lingua al volo

Supponiamo tu abbia un documento multilingua. Puoi cambiare `ocrEngine.Language` tra le riconoscimenti:

```csharp
ocrEngine.Language = OcrLanguage.English;
string english = ocrEngine.Recognize().Text;

ocrEngine.Language = OcrLanguage.Korean;
string korean = ocrEngine.Recognize().Text;
```

### 4. Salvare il risultato su file

Se preferisci **convertire immagine in testo** e salvarlo, basta scrivere la stringa in un file `.txt`:

```csharp
System.IO.File.WriteAllText("output.txt", recognizedText);
```

## Domande frequenti

- **Ho bisogno di una licenza per eseguire questo codice?**  
  No. La versione di prova funziona bene per sperimentare, ma aggiunge una filigrana all'output. Una licenza acquistata rimuove la filigrana e sblocca le prestazioni complete.

- **Posso usarlo su Linux?**  
  Assolutamente. Aspose.OCR è cross‑platform; basta assicurarsi di avere le dipendenze native richieste (libgdiplus per .NET Core su Linux).

- **E se la mia immagine è in uno stream invece che in un file?**  
  Usa `ImageStream.FromStream(yourStream)` – l'API accetta qualsiasi `System.IO.Stream`.

## Conclusione

Ti abbiamo guidato passo dopo passo su **come utilizzare OCR** in C# per **estrarre testo da un'immagine**, **convertire immagine in testo**, e **leggere caratteri coreani** caricando correttamente **l'immagine per OCR**. L'esempio completo e eseguibile sopra dovrebbe funzionare subito, e i consigli aggiuntivi ti offrono una roadmap per scenari più avanzati.

Pronto per la prossima sfida? Prova a sostituire con un'altra lingua, elaborare PDF pagina per pagina, o integrare la chiamata OCR in una web API così gli utenti possono caricare immagini e ottenere risultati di testo istantanei. Le possibilità sono infinite, e ora hai una solida base su cui costruire.

Buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}