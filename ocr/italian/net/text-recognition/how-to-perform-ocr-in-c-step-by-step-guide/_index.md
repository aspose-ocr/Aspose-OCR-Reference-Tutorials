---
category: general
date: 2026-02-14
description: Come eseguire OCR in C# usando Aspose.OCR – impara a estrarre testo da
  un'immagine, caricare l'immagine da file ed eseguire OCR sull'immagine rapidamente.
draft: false
keywords:
- how to perform OCR
- extract text from image
- load image from file
- recognize text from jpg
- run OCR on image
language: it
og_description: Come eseguire l'OCR in C# con Aspose.OCR. Questa guida ti mostra come
  estrarre il testo da un'immagine, caricare l'immagine da un file ed eseguire l'OCR
  sull'immagine in modo efficiente.
og_title: Come eseguire l'OCR in C# – Tutorial completo di programmazione
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Come eseguire OCR in C# – Guida passo passo
url: /it/net/text-recognition/how-to-perform-ocr-in-c-step-by-step-guide/
---

to Check -> "Cosa controllare", Fix -> "Correzione". Keep content but translate.

Now produce final.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR in C# – Tutorial di programmazione completo

Ti sei mai chiesto **come eseguire OCR** su una foto appena scattata con il tuo telefono? Forse devi estrarre il testo di un cartello stradale da un JPEG per un'app di navigazione, oppure hai una serie di contratti scansionati e vuoi trasformarli in testo ricercabile. In breve, vuoi *estrarre testo da immagine* senza inviare nulla al cloud.

La buona notizia è che puoi fare tutto questo localmente con Aspose.OCR per .NET. In questo tutorial vedremo come caricare un’immagine da file, riconoscere il testo da un JPG e, infine, **eseguire OCR su file immagine** completamente offline. Alla fine avrai uno snippet pronto all’uso che stampa il testo arabo riconosciuto sulla console.

> **Cosa otterrai:** un programma C# autonomo e eseguibile, spiegazioni sul perché ogni riga è importante e consigli per gestire casi particolari comuni, come risorse mancanti o lingue non supportate.

## Prerequisiti

Prima di iniziare, assicurati di avere:

| Requisito | Motivo |
|-----------|--------|
| .NET 6.0 o successivo (o .NET Framework 4.7+) | Aspose.OCR mira a .NET Standard 2.0, quindi qualsiasi runtime moderno funziona. |
| Visual Studio 2022 (o VS Code con estensione C#) | Un IDE semplifica la gestione dei pacchetti NuGet e l’esecuzione dell’app console. |
| Pacchetto NuGet Aspose.OCR (`Aspose.OCR`) | Questa è la libreria che effettua realmente il lavoro di OCR. |
| Una cartella contenente le risorse OCR offline (scaricabili da Aspose) | Le risorse offline evitano chiamate HTTP durante il riconoscimento. |
| Un file immagine (es. `arabic_sign.jpg`) | Useremo un JPEG che contiene testo arabo, ma funziona con qualsiasi lingua. |

Se ti manca qualcosa, procuratelo subito—non ha senso iniziare un tutorial per poi bloccarsi a metà per una dipendenza mancante.

## Passo 1: Installa Aspose.OCR e prepara le risorse

Per prima cosa, aggiungi il pacchetto Aspose.OCR al tuo progetto:

```bash
dotnet add package Aspose.OCR
```

Dopo l’installazione, scarica il **pacchetto di risorse OCR offline** dal sito Aspose. Estrailo in una cartella sul tuo computer, ad esempio:

```
C:\OCRResources\
```

> **Perché è importante:** Caricare le risorse una sola volta all’avvio elimina la latenza di rete e mantiene la tua soluzione conforme al GDPR perché nulla lascia la macchina.

## Passo 2: Crea il motore OCR e indica la cartella delle risorse

Ora istanzieremo la classe `Engine` e le diremo dove si trovano le risorse. Questo è il cuore di **come eseguire OCR** localmente.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Step 2: Initialize the OCR engine with the offline resource folder
Engine ocrEngine = new Engine
{
    // Replace with the path you used in the previous step
    ResourceFolder = @"C:\OCRResources"
};

// Load the resources into memory – this prevents any hidden HTTP calls
ocrEngine.LoadResources();
```

> **Consiglio:** Avvolgi la chiamata `LoadResources` in un blocco try‑catch se pensi che il percorso della cartella possa essere errato. L’eccezione ti indicherà esattamente quale file manca.

## Passo 3: Carica l’immagine da file

Successivamente dobbiamo **caricare immagine da file** affinché il motore possa analizzarla. Aspose.OCR lavora con il proprio wrapper `ImageStream`.

```csharp
// Step 3: Load the JPEG you want to recognize
ImageStream image = ImageStream.FromFile(@"C:\OCRResources\arabic_sign.jpg");
```

Se la tua immagine si trova altrove, modifica semplicemente il percorso. La classe `ImageStream` astrae la gestione del bitmap sottostante, così non devi preoccuparti della compatibilità GDI+.

## Passo 4: Riconosci il testo dal JPG usando le impostazioni della lingua

Ora arriva il nucleo di **come eseguire OCR**—il riconoscimento vero e proprio dei caratteri. Richiederemo il riconoscimento arabo, ma puoi sostituire `Language.Arabic` con qualsiasi altra lingua supportata.

```csharp
// Step 4: Run OCR specifying the desired language (Arabic in this example)
OcrResult ocrResult = ocrEngine.Recognize(
    image,
    new OcrOptions { Language = Language.Arabic }
);
```

> **Perché specificare una lingua?** Il motore OCR utilizza dizionari e modelli di caratteri specifici per lingua. Fornire la lingua corretta migliora notevolmente l’accuratezza, soprattutto per script con forme complesse come l’arabo.

## Passo 5: Visualizza il testo estratto

Infine, **estrai testo da immagine** e stampalo. È il modo più semplice per verificare che l’OCR abbia avuto successo.

```csharp
// Step 5: Output the recognized text to the console
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(ocrResult.Text);
```

Quando esegui il programma, dovresti vedere la frase araba presente sul cartello stampata nella console. Se l’output appare confuso, ricontrolla che la lingua corretta sia stata selezionata e che la cartella delle risorse contenga i file dati arabi.

## Esempio completo funzionante

Di seguito trovi il programma completo, pronto per la compilazione, che unisce tutti i passaggi. Copialo in un nuovo progetto console (`dotnet new console`) e premi **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Configure the OCR engine with offline resources
            // -------------------------------------------------
            Engine ocrEngine = new Engine
            {
                ResourceFolder = @"C:\OCRResources" // <-- change to your folder
            };
            ocrEngine.LoadResources(); // Loads language packs, fonts, etc.

            // -------------------------------------------------
            // Step 2: Load the image you want to process
            // -------------------------------------------------
            ImageStream image = ImageStream.FromFile(@"C:\OCRResources\arabic_sign.jpg");

            // -------------------------------------------------
            // Step 3: Recognize text – specify language to improve accuracy
            // -------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(
                image,
                new OcrOptions { Language = Language.Arabic } // Change as needed
            );

            // -------------------------------------------------
            // Step 4: Output the result
            // -------------------------------------------------
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**Output previsto (esempio):**

```
=== OCR Result ===
مطار القاهره الدولي
```

Se sostituisci l’immagine con un cartello in inglese e imposti `Language.English`, lo stesso codice produrrà il testo inglese. Questo dimostra quanto sia flessibile **eseguire OCR su immagine**.

## Estrarre testo da immagine – Gestione degli scenari comuni

### 1. Pagine multiple o immagini multi‑frame

Alcuni formati (come TIFF) possono contenere più pagine. Per **estrarre testo da immagine** in questi casi, itera su ogni frame:

```csharp
for (int i = 0; i < image.FramesCount; i++)
{
    image.CurrentFrame = i;
    OcrResult pageResult = ocrEngine.Recognize(image, new OcrOptions { Language = Language.English });
    Console.WriteLine($"Page {i + 1}: {pageResult.Text}");
}
```

### 2. Immagini a bassa risoluzione

L’accuratezza dell’OCR cala drasticamente sotto i 70 dpi. Se ottieni risultati sfocati, considera di ingrandire l’immagine prima:

```csharp
using System.Drawing;
using System.Drawing.Drawing2D;

// Load as Bitmap, resize, then wrap back into ImageStream
Bitmap bmp = new Bitmap(@"C:\OCRResources\lowres.jpg");
Bitmap highRes = new Bitmap(bmp, new Size(bmp.Width * 2, bmp.Height * 2));
ImageStream highResStream = ImageStream.FromBitmap(highRes);
```

### 3. Pacchetto lingua mancante

Se ricevi un’eccezione tipo *“Language data not found”*, verifica che i file `.dat` corrispondenti esistano nella tua `ResourceFolder`. Aspose fornisce un zip separato per ogni lingua.

## Eseguire OCR su immagine – Suggerimenti sulle prestazioni

- **Cache del motore:** Creare un nuovo `Engine` per ogni immagine aggiunge overhead. Mantieni un’unica istanza viva per l’elaborazione batch.
- **Parallelismo sicuro:** `Engine` è thread‑safe per operazioni di sola lettura dopo `LoadResources`. Puoi avviare più task che chiamano `Recognize` su immagini diverse.
- **Dispose quando finito:** Sebbene `Engine` implementi `IDisposable`, il GC di .NET pulirà comunque. Chiamare esplicitamente `ocrEngine.Dispose()` in un blocco `using` è una buona abitudine.

```csharp
using (Engine ocrEngine = new Engine { ResourceFolder = @"C:\OCRResources" })
{
    ocrEngine.LoadResources();
    // run recognitions here
}
```

## Riconoscere testo da JPG – Casi limite da tenere d’occhio

| Situazione | Cosa controllare | Correzione |
|------------|------------------|------------|
| **JPEG corrotto** | `ImageStream.FromFile` lancia `FileNotFoundException` o `ArgumentException`. | Verifica l’integrità del file, magari risalvandolo con un editor grafico. |
| **Lingua non supportata** | L’enum `Language` non contiene la lingua desiderata. | Aggiorna Aspose.OCR all’ultima versione; le nuove lingue vengono aggiunte regolarmente. |
| **Immagini a script misti** (es. inglese + arabo) | Un’unica opzione lingua può perdere lo script secondario. | Esegui OCR due volte con opzioni di lingua diverse e concatena i risultati. |

## Riepilogo – Ora sai come eseguire OCR in C#

In questa guida abbiamo coperto **come eseguire OCR** usando Aspose.OCR, dall’installazione del pacchetto NuGet alla stampa del testo riconosciuto. Hai imparato a **caricare immagine da file**, **estrarre testo da immagine**, **riconoscere testo da jpg** e a **eseguire OCR su immagine** in modo pronto per la produzione.

### Qual è il prossimo passo?

- **Sperimenta con altri formati** come PNG o BMP—basta cambiare l’estensione del file.
- **Integra con un database** per archiviare i risultati OCR e renderli ricercabili.
- **Combina con computer‑vision** (es. rilevare regioni di testo prima dell’OCR) per guadagnare velocità.

Sentiti libero di modificare le impostazioni della lingua, elaborare cartelle in batch o collegare l’output a un’API web. L’OCR è un blocco costitutivo; il vero potere nasce quando lo integri in flussi di lavoro più ampi.

Buona programmazione, e che le tue immagini siano sempre cristalline!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}