---
date: 2025-12-22
description: Scopri come estrarre il testo da un'immagine usando Aspose.OCR per .NET.
  Questa guida ti accompagna nella preparazione dei rettangoli per il riconoscimento
  OCR delle immagini e nell'aumento della precisione.
linktitle: Prepare Rectangles in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: Come estrarre testo da un'immagine preparando rettangoli in OCR
url: /it/net/ocr-optimization/prepare-rectangles/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Preparare i rettangoli nel riconoscimento OCR delle immagini

## Introduzione

Il riconoscimento ottico dei caratteri (OCR) è essenziale per convertire contenuti visivi in testo ricercabile e modificabile. In questo tutorial **estrarrai testo da immagine** preparando rettangoli personalizzati che focalizzano il motore OCR su regioni specifiche. Utilizzando Aspose.OCR per .NET, ti guideremo passo passo — dall'impostazione del progetto al recupero del testo riconosciuto — così potrai integrare potenti funzionalità di immagine‑a‑testo nelle tue applicazioni .NET.

## Risposte rapide
- **Cosa significa “estrarre testo da immagine”?** Significa convertire i caratteri visivi in una foto in stringhe leggibili dalla macchina.  
- **Quale libreria aiuta a fare ciò in .NET?** Aspose.OCR per .NET.  
- **È necessaria una licenza per lo sviluppo?** Una versione di prova gratuita è sufficiente per i test; è richiesta una licenza per la produzione.  
- **Posso mirare aree specifiche?** Sì, definendo rettangoli che limitano l'ambito dell'OCR.  
- **Quali versioni di .NET sono supportate?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Cos'è “estrarre testo da immagine” con i rettangoli?
Quando definisci zone rettangolari su un'immagine, il motore OCR elabora solo quelle zone. Ciò migliora l'accuratezza, riduce i tempi di elaborazione e ti consente di ignorare sfondi rumorosi o sezioni irrilevanti.

## Perché preparare i rettangoli prima dell'OCR?
- **Concentrarsi sul contenuto rilevante:** Ignora intestazioni, piè di pagina o grafiche decorative.  
- **Migliorare le prestazioni:** Regioni più piccole significano riconoscimento più veloce.  
- **Aumentare l'accuratezza:** Meno rumore visivo porta a risultati più puliti.

## Prerequisiti

- Familiarità con C# e lo sviluppo .NET.  
- Libreria Aspose.OCR per .NET installata – puoi scaricarla **[qui](https://releases.aspose.com/ocr/net/)**.  
- Un'immagine di esempio (ad es. `sample.png`) che contiene il testo che desideri estrarre.

## Importa gli spazi dei nomi

First, bring the required namespaces into scope:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Passo 1: Configura la directory dei documenti

Specify where your image files live and create an instance of the OCR engine.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Come estrarre testo da immagine usando più rettangoli

### Passo 2: Riconosci l'immagine con più rettangoli

#### 2.1 Definisci i rettangoli

Create a list of `Rectangle` objects that outline the areas you want the OCR engine to scan.

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

#### 2.2 Esegui il riconoscimento OCR

Pass the image path and the rectangle list to `RecognizeImage`. The method returns a collection of strings—each entry corresponds to one rectangle.

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

### Passo 3: Riconosci l'immagine con le impostazioni di riconoscimento (approccio alternativo)

If you prefer using `RecognitionSettings`, you can achieve the same result with a slightly different API call.

#### 3.1 Define recognition settings

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

#### 3.2 Display recognized text

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## Problemi comuni e consigli

- **Coordinate del rettangolo errate:** Assicurati che i valori `X`, `Y`, `Width` e `Height` corrispondano correttamente alla regione desiderata.  
- **Qualità dell'immagine:** Immagini a bassa risoluzione possono produrre risultati OCR scadenti; considera un pre‑processing (ad es., binarizzazione).  
- **Risultati vuoti:** Verifica che i rettangoli contengano effettivamente testo; altrimenti il motore restituisce stringhe vuote.

## Conclusione

Adesso hai imparato come **estrarre testo da immagine** preparando rettangoli personalizzati con Aspose.OCR per .NET. Questa tecnica ti offre un controllo dettagliato sul processo OCR, aiutandoti a creare funzionalità di estrazione del testo più rapide e precise nelle tue applicazioni.

## Domande frequenti

**D:** Posso usare Aspose.OCR per .NET con altri framework .NET?  
**R:** Sì, Aspose.OCR per .NET è compatibile con vari framework .NET.

**D:** È disponibile una versione di prova gratuita per Aspose.OCR per .NET?  
**R:** Assolutamente! Puoi accedere alla versione di prova gratuita **[qui](https://releases.aspose.com/)**.

**D:** Come posso ottenere supporto per Aspose.OCR per .NET?  
**R:** Visita il **[forum Aspose.OCR](https://forum.aspose.com/c/ocr/16)** per supporto dedicato.

**D:** Posso ottenere una licenza temporanea per scopi di test?  
**R:** Sì, puoi acquisire una licenza temporanea **[qui](https://purchase.aspose.com/temporary-license/)**.

**D:** Dove posso trovare la documentazione per Aspose.OCR per .NET?  
**R:** La documentazione è disponibile **[qui](https://reference.aspose.com/ocr/net/)**.

---

**Ultimo aggiornamento:** 2025-12-22  
**Testato con:** Aspose.OCR 24.11 per .NET  
**Autore:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}