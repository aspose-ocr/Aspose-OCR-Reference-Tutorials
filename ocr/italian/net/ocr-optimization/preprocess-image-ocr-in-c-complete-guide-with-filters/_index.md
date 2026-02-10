---
category: general
date: 2026-02-09
description: Scopri come pre‑elaborare le immagini OCR e riconoscere il testo delle
  immagini usando Aspose OCR. Riduci il rumore dell'immagine, aggiungi filtri e estrai
  il testo semplice in pochi minuti.
draft: false
keywords:
- preprocess image OCR
- recognize text image
- extract plain text
- reduce image noise
- how to add filters
language: it
og_description: Preprocessa rapidamente l'OCR delle immagini. Questa guida mostra
  come aggiungere filtri, ridurre il rumore dell'immagine ed estrarre testo semplice
  da qualsiasi foto.
og_title: Preprocessare OCR di immagini in C# – Tutorial passo passo
tags:
- OCR
- C#
- Image Processing
title: Preprocessare l'OCR delle immagini in C# – Guida completa con filtri
url: /it/net/ocr-optimization/preprocess-image-ocr-in-c-complete-guide-with-filters/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Preprocess Image OCR in C# – Guida completa con filtri

Hai mai avuto difficoltà a **preprocessare l'OCR delle immagini** perché le tue scansioni sono storte, granulose o semplicemente difficili da leggere? Non sei l'unico. In molti progetti reali, una foto traballante di una ricevuta o un modulo scansionato rumoroso può far restituire al motore OCR una serie di caratteri incomprensibili invece di dati utili.  

La buona notizia? Puoi pulire quelle immagini prima di passarle al motore, e il risultato è una precisione drasticamente più alta quando **riconosci il testo dell'immagine**. In questo tutorial vedremo passo passo **come aggiungere filtri**, ridurre il rumore e infine **estrarre il testo semplice** con Aspose.OCR in C#.

Copriamo tutto ciò di cui hai bisogno—dall'installazione della libreria all'esecuzione del codice e alla verifica dell'output—così potrai copiare‑incollare una soluzione funzionante subito.

---

## Cosa ti servirà

- **.NET 6+** (o qualsiasi runtime .NET recente; l'API funziona allo stesso modo)
- **Aspose.OCR for .NET** pacchetto NuGet  
  ```bash
  dotnet add package Aspose.OCR
  ```
- Un'immagine di esempio che presenta rotazione, rumore o basso contrasto (ad esempio `skewed_noisy.jpg`)
- Un IDE o editor a tua scelta (Visual Studio, VS Code, Rider—scegli quello che preferisci)

Questo è tutto. Nessuna libreria nativa aggiuntiva, nessun framework di elaborazione immagini pesante. Aspose fornisce già i filtri di cui abbiamo bisogno.

---

## Passo 1 – Creare l'istanza del motore OCR  

La prima cosa da fare è istanziare un `OcrEngine`. Pensalo come il cervello che leggerà i caratteri dopo che avremo pulito l'immagine.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;

class FilterExample
{
    static void Main()
    {
        // Initialize the OCR engine – this object will hold our filters and settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **Perché è importante:** Il motore contiene una **pipeline di preprocessing**. Aggiungere filtri in seguito li applicherà automaticamente ogni volta che chiami `Recognize`.

---

## Passo 2 – Aggiungere filtri per ridurre il rumore dell'immagine e migliorare la leggibilità  

Ora **aggiungiamo i filtri**. Ogni filtro affronta un difetto specifico:

| Filtro | Cosa corregge | Valori tipici usati |
|--------|---------------|---------------------|
| `DeskewFilter` | Testo ruotato (skew) | `MaxAngle = 12` (gradi) |
| `DenoiseFilter` | Macchie casuali, granulosità | `Strength = 0.6` (0‑1) |
| `ContrastBoostFilter` | Lettere sbiadite | `Level = 1.3` (1‑2) |
| `BinarizeAdaptiveFilter` | Illuminazione non uniforme | i valori predefiniti funzionano bene |

```csharp
        // Step 2: Add preprocessing filters to improve image quality
        //   • Deskew to correct rotation (max 12°)
        //   • Denoise to reduce noise (strength 0.6)
        //   • Contrast boost to enhance visibility (level 1.3)
        //   • Adaptive binarization for better binarization
        ocrEngine.Preprocessing.Add(new DeskewFilter { MaxAngle = 12 });
        ocrEngine.Preprocessing.Add(new DenoiseFilter { Strength = 0.6 });
        ocrEngine.Preprocessing.Add(new ContrastBoostFilter { Level = 1.3 });
        ocrEngine.Preprocessing.Add(new BinarizeAdaptiveFilter());
```

> **Consiglio esperto:** Se le tue immagini sono già dritte, puoi saltare il passo di deskew. Rimuovere filtri non necessari velocizza l'elaborazione.

---

## Passo 3 – Caricare l'immagine da processare  

Successivamente, indichiamo al motore quale immagine pulire. `ImageStream.FromFile` legge il file in un formato comprensibile al motore OCR.

```csharp
        // Step 3: Load the image that needs OCR processing
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_noisy.jpg");
```

> **Caso limite:** Quando lavori con stream provenienti da un'API web, sostituisci `FromFile` con `FromStream` per evitare di accedere al file system.

---

## Passo 4 – Eseguire il motore OCR e riconoscere il testo dell'immagine  

Ora avviene la magia. Il motore applica tutti i filtri aggiunti, poi esegue il riconoscimento dei caratteri.

```csharp
        // Step 4: Run the OCR engine on the prepared image
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

> **Perché funziona:** La pipeline di preprocessing garantisce che l'immagine fornita al riconoscitore sia il più pulita possibile, aumentando direttamente la precisione del **recognize text image**.

---

## Passo 5 – Estrarre il testo semplice e visualizzarlo  

Infine, estraiamo il risultato in testo semplice e lo stampiamo sulla console. Questa è la parte **extract plain text** del flusso di lavoro.

```csharp
        // Step 5: Output the recognized plain text
        Console.WriteLine(ocrResult.PlainText);
    }
}
```

### Output previsto

Se `skewed_noisy.jpg` contiene una semplice riga di fattura come `Total: $123.45`, dovresti vedere:

```
Total: $123.45
```

Anche se il file originale era ruotato di 10°, presentava macchie e basso contrasto, i filtri dovrebbero pulirlo a sufficienza perché il motore OCR lo legga correttamente.

---

## Panoramica visiva  

Di seguito trovi una rapida illustrazione della pipeline di preprocessing. Il diagramma non è necessario per far funzionare il codice, ma aiuta a visualizzare il flusso.

![preprocess image OCR diagram](https://example.com/ocr-pipeline.png "preprocess image OCR pipeline")

*Testo alternativo: pipeline di preprocessamento OCR delle immagini che mostra i passaggi di deskew, denoise, contrast boost e adaptive binarization.*

---

## Domande frequenti e insidie  

- **E se il risultato OCR è ancora incomprensibile?**  
  Prova ad aumentare `DenoiseFilter.Strength` a `0.8` o a ridurre `ContrastBoostFilter.Level` a `1.1`. Un eccessivo boost del contrasto può a volte creare aloni che confondono il riconoscitore.

- **Posso aggiungere un filtro personalizzato?**  
  Sì. Aspose.OCR ti permette di implementare `IFilter` e iniettarlo in `ocrEngine.Preprocessing`. È un argomento avanzato, ma utile quando hai esigenze di preprocessing specifiche per il dominio.

- **Funziona con i PDF?**  
  Solo se prima converti ogni pagina PDF in un'immagine (ad esempio usando Aspose.PDF). Una volta ottenuta la bitmap, la stessa catena di filtri si applica.

- **La libreria è thread‑safe?**  
  L'istanza `OcrEngine` **non** è thread‑safe. Crea un motore separato per ogni thread o avvolgi le chiamate in un lock.

---

## Estendere l'esempio  

Ora che hai una solida base, considera i seguenti passi successivi:

1. **Elaborazione batch** – Scorri una cartella di immagini, applica la stessa catena di filtri e scrivi ogni risultato in un file `.txt`.  
2. **Pacchetti linguistici** – Se devi riconoscere francese o tedesco, carica i dati linguistici appropriati tramite `ocrEngine.Language = "fra"` (o `"deu"`).  
3. **Regione di interesse (ROI)** – Usa `ocrEngine.Recognize(image, new Rectangle(x, y, width, height))` per concentrarti su un'area specifica, il che può velocizzare la scansione di documenti grandi.

---

## Conclusione  

In questa guida abbiamo **preprocessato l'OCR delle immagini** aggiungendo una serie di filtri integrati, poi **riconosciuto il testo dell'immagine** e infine **estratto il testo semplice** da una foto rumorosa e inclinata. Il codice completo, eseguibile, è mostrato sopra e può essere adattato a qualsiasi progetto C# che richieda risultati OCR affidabili.  

Ricorda, la chiave per un OCR eccellente non è solo un motore potente—è un input pulito. Riducendo il rumore dell'immagine e allineando correttamente il testo, offri al riconoscitore le migliori possibilità di successo.  

Sentiti libero di sperimentare con i valori dei filtri, provare formati di immagine diversi o combinare questo approccio con altre librerie Aspose. Se incontri difficoltà, lascia un commento qui sotto o consulta la documentazione ufficiale di Aspose per approfondimenti su ciascuna classe di filtro. Buon coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}