---
category: general
date: 2026-02-28
description: come eseguire OCR in C# usando Aspose OCR – scopri come estrarre testo
  da un'immagine, convertire l'immagine in JSON o XML in pochi passaggi.
draft: false
keywords:
- how to run OCR
- extract text from image
- convert image to json
- convert image to xml
- how to extract text
language: it
og_description: come eseguire OCR in C# usando Aspose OCR – scopri come estrarre testo
  da un’immagine e convertire l’immagine in JSON o XML con un esempio pronto all’uso.
og_title: Come eseguire l'OCR con Aspose OCR in C# – Guida completa
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Come eseguire OCR con Aspose OCR in C# – Guida completa
url: /it/net/text-recognition/how-to-run-ocr-with-aspose-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# come eseguire OCR con Aspose OCR in C# – Guida completa

Se ti chiedi **come eseguire OCR** su un'immagine di una ricevuta usando C#, sei nel posto giusto. In questo tutorial vedremo come **estrarre testo da immagine** e poi **convertire immagine in JSON** o **convertire immagine in XML** con Aspose OCR—tutto in un unico programma autonomo.

Immagina di stare costruendo un'app di monitoraggio delle spese e di dover estrarre le voci di spesa da ricevute fotografate. Digitare manualmente ogni voce è una seccatura, vero? Alla fine di questa guida avrai uno snippet riutilizzabile che legge qualsiasi immagine, restituisce testo strutturato e fornisce sia rappresentazioni JSON che XML pronte per l'elaborazione successiva.

## Prerequisiti

Prima di immergerci, assicurati di avere:

- .NET 6.0 SDK o versioni successive (il codice funziona anche su .NET Framework 4.8)
- Visual Studio 2022 (o qualsiasi editor tu preferisca)
- Un pacchetto NuGet **Aspose.OCR** attivo (`Install-Package Aspose.OCR`)
- Un'immagine di esempio (ad es., `receipt.png`) posizionata in una cartella a cui puoi fare riferimento

Non è necessaria alcuna configurazione aggiuntiva; la libreria include tutti i modelli OCR necessari.

![Immagine della ricevuta per l'elaborazione OCR – come eseguire OCR](receipt.png)

> *Testo alternativo: Immagine della ricevuta per l'elaborazione OCR – come eseguire OCR*

## Implementazione passo‑a‑passo

Di seguito suddividiamo la soluzione in blocchi logici. Ogni passaggio spiega **perché** lo facciamo, non solo **cosa** fa il codice.

### 1️⃣ Inizializzare il motore OCR – la base di **come eseguire OCR**

La classe `OcrEngine` è il punto di ingresso. Istanziandola vengono caricati i modelli linguistici interni e il motore viene preparato per il riconoscimento.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class StructuredOutputDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        // This object holds the OCR model and settings.
        var ocrEngine = new OcrEngine();
```

> **Consiglio:** Riutilizzare lo stesso `OcrEngine` per più immagini riduce il consumo di memoria e velocizza l'elaborazione batch.

### 2️⃣ Caricare l'immagine – il fulcro di **estrarre testo da immagine**

Aspose OCR lavora con il proprio wrapper `Image`. L'uso di una dichiarazione `using` garantisce che il handle del file venga rilasciato prontamente.

```csharp
        // Step 2: Load the image you want to analyze
        // Replace YOUR_DIRECTORY with the actual path on your machine.
        using var image = Image.Load(@"YOUR_DIRECTORY/receipt.png");
```

Se l'immagine è in un formato diverso (BMP, TIFF, PDF), lo stesso metodo `Load` la gestisce—nessuna conversione aggiuntiva è necessaria.

### 3️⃣ Eseguire il riconoscimento OCR – il cuore di **come eseguire OCR**

Chiamare `Recognize` esegue il lavoro pesante: analisi del layout, segmentazione dei caratteri e classificazione specifica per lingua.

```csharp
        // Step 3: Run OCR recognition on the loaded image
        var ocrResult = ocrEngine.Recognize(image);
```

Il risultato restituito `OcrResult` contiene testo grezzo, punteggi di confidenza e un albero di layout dettagliato che può essere serializzato.

### 4️⃣ Convertire l'immagine in JSON – il modo diretto per **convertire immagine in json**

JSON è perfetto per API web o archivi NoSQL. Il metodo `ToJson` fornisce una stringa formattata, rendendo il debug un gioco da ragazzi.

```csharp
        // Step 4: Retrieve the detailed layout as pretty‑printed JSON
        string jsonOutput = ocrResult.ToJson(prettyPrint: true);
        Console.WriteLine("=== JSON Output ===");
        Console.WriteLine(jsonOutput);
```

Un tipico output JSON appare così (troncato per brevità):

```json
{
  "Text": "Total 12.34",
  "Blocks": [
    {
      "Text": "Total",
      "Confidence": 0.98,
      "Bounds": { "X": 10, "Y": 150, "Width": 45, "Height": 15 }
    },
    {
      "Text": "12.34",
      "Confidence": 0.97,
      "Bounds": { "X": 60, "Y": 150, "Width": 30, "Height": 15 }
    }
  ]
}
```

Ora puoi inviare questo JSON direttamente a un endpoint REST o archiviarlo in Azure Cosmos DB.

### 5️⃣ Convertire l'immagine in XML – quando è necessario **convertire immagine in xml**

Alcuni sistemi legacy consumano ancora XML. Aspose fornisce `ToXml` per una rappresentazione pulita e compatibile con lo schema.

```csharp
        // Step 5: Retrieve the same information in XML format (optional)
        string xmlOutput = ocrResult.ToXml();
        Console.WriteLine("\n=== XML Output ===");
        Console.WriteLine(xmlOutput);
    }
}
```

Esempio di snippet XML:

```xml
<OcrResult>
  <Text>Total 12.34</Text>
  <Blocks>
    <Block>
      <Text>Total</Text>
      <Confidence>0.98</Confidence>
      <Bounds X="10" Y="150" Width="45" Height="15" />
    </Block>
    <Block>
      <Text>12.34</Text>
      <Confidence>0.97</Confidence>
      <Bounds X="60" Y="150" Width="30" Height="15" />
    </Block>
  </Blocks>
</OcrResult>
```

Entrambi i formati preservano gli stessi dati gerarchici, così puoi scegliere quello più adatto al tuo flusso di lavoro.

## Problemi comuni e come estrarre testo in modo affidabile

Anche con una libreria robusta, le immagini del mondo reale possono creare problemi. Ecco tre situazioni che potresti incontrare e le relative soluzioni.

### 📏 Immagini a bassa risoluzione

**Perché è importante:** I caratteri piccoli si fondono, riducendo i punteggi di confidenza.  
**Soluzione:** Pre‑elabora l'immagine—ingrandiscila con `Image.Resize` o applica un filtro di nitidezza prima di passare a `Recognize`.

```csharp
using var highRes = image.Resize(2.0, InterpolationMode.HighQualityBicubic);
var result = ocrEngine.Recognize(highRes);
```

### 🌈 Scarsa differenza di contrasto

**Perché è importante:** Il testo chiaro su sfondo scuro confonde l'algoritmo di segmentazione.  
**Soluzione:** Inverti i colori o regola luminosità/contrasto tramite `Image.AdjustBrightnessContrast`.

```csharp
image.AdjustBrightnessContrast(brightness: 30, contrast: 40);
```

### 📄 Documenti multilingue

**Perché è importante:** Il modello linguistico predefinito è l'inglese; le lingue miste producono output confuso.  
**Soluzione:** Imposta `ocrEngine.Language = OcrLanguage.Multilingual;` prima del riconoscimento.

```csharp
ocrEngine.Language = OcrLanguage.Multilingual;
```

Affrontare questi casi limite garantisce che **estrarre testo** da qualsiasi immagine diventi una routine affidabile e non un azzardo.

## Esempio completo funzionante (pronto per copia‑incolla)

Di seguito trovi il programma completo, pronto per essere compilato ed eseguito. Sostituisci semplicemente `YOUR_DIRECTORY` con il percorso della tua immagine e premi F5.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class StructuredOutputDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Optional: improve accuracy for low‑contrast images
        // ocrEngine.Language = OcrLanguage.Multilingual;

        // Step 2: Load the image you want to analyze
        using var image = Image.Load(@"YOUR_DIRECTORY/receipt.png");

        // Step 3: Run OCR recognition on the loaded image
        var ocrResult = ocrEngine.Recognize(image);

        // Step 4: Retrieve the detailed layout as pretty‑printed JSON
        string jsonOutput = ocrResult.ToJson(prettyPrint: true);
        Console.WriteLine("=== JSON Output ===");
        Console.WriteLine(jsonOutput);

        // Step 5: Retrieve the same information in XML format (optional)
        string xmlOutput = ocrResult.ToXml();
        Console.WriteLine("\n=== XML Output ===");
        Console.WriteLine(xmlOutput);
    }
}
```

**Output console previsto** (formattato per leggibilità) mostra sia le strutture JSON che XML contenenti il testo estratto e le bounding box.

## Riepilogo – Cosa abbiamo coperto

- **come eseguire OCR** con Aspose OCR in C#
- Il processo passo‑a‑passo per **estrarre testo da immagine**
- Due opzioni di serializzazione: **convertire immagine in json** e **convertire immagine in xml**
- Suggerimenti per gestire scenari a bassa risoluzione, basso contrasto e multilingue
- Un esempio di codice completo, pronto per il copia‑incolla, che puoi inserire in qualsiasi progetto .NET

## Prossimi passi

Ora che puoi **estrarre testo** e ottenere dati strutturati, considera queste idee successive:

- Invia il JSON a una Azure Function che archivia le ricevute in Cosmos DB.
- Usa l'output XML per popolare un sistema contabile basato su SOAP esistente.
- Combina Aspose OCR con un modello di machine learning per categorizzare automaticamente i tipi di spesa.

Sentiti libero di sperimentare—sostituisci `receipt.png` con fatture, biglietti da visita o note scritte a mano. Lo stesso schema funziona across

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}