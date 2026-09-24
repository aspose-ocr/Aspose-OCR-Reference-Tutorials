---
category: general
date: 2026-02-13
description: Scopri come utilizzare l'OCR in C# per estrarre testo da file immagine,
  abilitare l'elaborazione GPU e convertire rapidamente le scansioni in testo.
draft: false
keywords:
- how to use OCR
- extract text from image
- how to extract text
- convert scan to text
- enable gpu processing
language: it
og_description: Come usare l'OCR in C#? Questa guida ti mostra come estrarre testo
  da file immagine, abilitare l'elaborazione GPU e convertire le scansioni in testo.
og_title: Come utilizzare l'OCR in C# – Estrarre testo dalle immagini con GPU
tags:
- OCR
- C#
- Aspose
- GPU
- Image Processing
title: Come utilizzare l'OCR in C# – Estrarre testo dalle immagini con GPU
url: /it/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-with-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come utilizzare OCR in C# – Estrarre testo dalle immagini con GPU

Ti sei mai chiesto **come usare OCR** per estrarre testo da un documento scansionato senza sforzo? Non sei l'unico—gli sviluppatori chiedono continuamente, “Come posso estrarre testo da file immagine in modo efficiente?” La buona notizia è che con Aspose.OCR puoi fare esattamente questo, e puoi persino **abilitare l'elaborazione GPU** per un notevole aumento di velocità sull'hardware supportato.

In questo tutorial percorreremo un esempio completo, end‑to‑end, che ti mostra **come usare OCR**, come **estrarre testo da un'immagine**, come **convertire una scansione in testo**, e cosa fare se la GPU non è disponibile. Alla fine avrai un'app console C# pronta all'uso che stampa il testo riconosciuto e indica se la GPU è stata effettivamente utilizzata.

## Cosa ti serve

- .NET 6 SDK o versioni successive (il codice funziona anche con .NET Core)  
- Visual Studio 2022 o qualsiasi editor tu preferisca  
- Pacchetto Aspose.OCR per .NET (disponibile via NuGet)  
- Un file immagine ad alta risoluzione (ad es. `highres_scan.tif`) per i test  

Nessuna configurazione complicata richiesta—basta qualche comando NuGet e sei pronto.

## Passo 1: Installa Aspose.OCR e prepara il progetto

Prima di tutto. Devi aggiungere la libreria OCR al tuo progetto. Apri un terminale nella cartella della soluzione e esegui:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

Questo crea un nuovo progetto console chiamato **OcrDemo** e aggiunge il pacchetto NuGet `Aspose.OCR`. La libreria contiene la classe `OcrEngine` che utilizzeremo.

> **Consiglio professionale:** Se sei su una macchina con GPU dedicata, assicurati che il driver grafico più recente sia installato; altrimenti la libreria tornerà automaticamente alla modalità CPU.

## Passo 2: Scrivi il codice OCR completo

Ora apri `Program.cs` e sostituisci il suo contenuto con il seguente. Ogni riga è commentata così puoi vedere *perché* facciamo quello che facciamo.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Create an OCR engine and request GPU processing.
            //    If the GPU isn’t present, Aspose.OCR will silently
            //    switch to CPU mode – no crash, no extra code needed.
            // -------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                ProcessingMode = OcrProcessingMode.Gpu
            };

            // -------------------------------------------------
            // 2️⃣  Define the path to the image you want to process.
            //    Replace the placeholder with the actual file location.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/highres_scan.tif";

            // -------------------------------------------------
            // 3️⃣  Perform the recognition. The method returns an
            //    OcrResult object that contains the extracted text,
            //    confidence scores, and more.
            // -------------------------------------------------
            OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

            // -------------------------------------------------
            // 4️⃣  Report whether the GPU was really used.
            //    This is handy for debugging performance issues.
            // -------------------------------------------------
            Console.WriteLine($"GPU used: {ocrEngine.IsGpuEnabled}");

            // -------------------------------------------------
            // 5️⃣  Output the recognized text to the console.
            //    In a real app you might write this to a file,
            //    a database, or feed it into another workflow.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### Perché funziona

- **ProcessingMode = Gpu** indica al motore di provare prima la GPU. La libreria astrae le chiamate a basso livello CUDA/OpenCL, quindi non è necessario gestire i contesti del dispositivo manualmente.  
- **IsGpuEnabled** è un booleano che conferma se il percorso GPU è riuscito. Se vedi `false`, il motore è tornato automaticamente alla CPU—nessun motivo di panico.  
- **RecognizeImage** esegue tutto il lavoro pesante: carica l'immagine, esegue il modello OCR e restituisce il risultato in plain‑text. Non è necessario pre‑elaborare manualmente il bitmap a meno che tu non abbia requisiti speciali (ad es. correzione di inclinazione).

## Passo 3: Esegui l'applicazione e verifica l'output

Compila ed esegui:

```bash
dotnet run
```

Se tutto è configurato correttamente, vedrai qualcosa del genere:

```
GPU used: True
=== Extracted Text ===
This is the first line of the scanned document.
Here is the second line, and so on…
```

Se la GPU non è disponibile, la prima riga mostrerà `GPU used: False`, ma il testo estratto apparirà comunque—grazie al fallback elegante.

> **Domanda comune:** *E se la mia immagine è un JPEG invece di un TIFF?*  
> Il metodo `RecognizeImage` accetta qualsiasi formato supportato da `System.Drawing` di .NET (JPEG, PNG, BMP, ecc.). Basta cambiare l'estensione del file in `imagePath`.

## Passo 4: Opzionale – Regola le impostazioni per una migliore precisione

Aspose.OCR offre alcune impostazioni che puoi modificare:

| Impostazione | Cosa fa | Quando usarla |
|--------------|----------|---------------|
| `ocrEngine.Language` | Forza una lingua specifica (ad es., `OcrLanguage.English`) | Se conosci la lingua del documento |
| `ocrEngine.PageSegMode` | Controlla come il motore suddivide le pagine in blocchi | Per layout a più colonne |
| `ocrEngine.DetectOrientation` | Ruota automaticamente il testo non verticale | Scansioni che potrebbero essere capovolte |

Puoi impostare queste proprietà prima di chiamare `RecognizeImage`. Ad esempio:

```csharp
ocrEngine.Language = OcrLanguage.English;
ocrEngine.DetectOrientation = true;
```

## Passo 5: Visualizza il flusso (Immagine con testo alternativo)

Di seguito è riportato un semplice diagramma che illustra **come usare OCR** con accelerazione GPU opzionale. Non è necessario per l'esecuzione del codice, ma aiuta a vedere il quadro generale.

![Diagramma che mostra come usare OCR con elaborazione GPU](/images/ocr-gpu-flow.png)

*Testo alternativo:* *Diagramma che mostra come usare OCR con elaborazione GPU, evidenziando il fallback alla CPU quando necessario.*

## Casi limite e risoluzione dei problemi

1. **Out‑of‑Memory on GPU** – Immagini molto grandi possono superare la memoria della GPU. In tal caso, la libreria tornerà automaticamente alla CPU. Puoi ridimensionare l'immagine in anticipo per mantenere basso l'uso di memoria.  
2. **Unsupported Image Format** – Se `RecognizeImage` genera *NotSupportedException*, verifica l'estensione del file e assicurati che l'immagine non sia corrotta. Convertire in PNG spesso risolve il problema.  
3. **Low Confidence Scores** – Quando il risultato OCR contiene molti caratteri illeggibili, considera la pre‑elaborazione (binarizzazione, rimozione del rumore) o passa a una scansione a risoluzione più alta.  

## Conclusione: cosa abbiamo realizzato

Abbiamo appena coperto **come usare OCR** in un'app console C#, dimostrato come **estrarre testo da file immagine**, e mostrato come **abilitare l'elaborazione GPU** per risultati più rapidi. Ora sai come **convertire una scansione in testo**, verificare se la GPU è stata effettivamente utilizzata e regolare alcune impostazioni per scenari limite.

### Prossimi passi

- Prova a inserire l'output in un **indice di ricerca** (ad es., Elasticsearch) così i tuoi PDF scansionati diventano ricercabili.  
- Sperimenta con **elaborazione batch**—itera su una cartella di immagini e scrivi ogni risultato in un file `.txt`.  
- Combina OCR con **API di traduzione** per tradurre automaticamente documenti scansionati in lingue straniere.  

Hai altre domande? Lascia un commento, e buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}