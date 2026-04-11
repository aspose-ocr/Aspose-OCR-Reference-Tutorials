---
category: general
date: 2026-04-11
description: Scopri come disabilitare l'OCR in Aspose OCR per C# per eseguirlo offline,
  estrarre il testo da un'immagine senza internet e caricare correttamente l'immagine
  per l'OCR.
draft: false
keywords:
- how to disable OCR
- extract text from image
- load image for OCR
- offline OCR C#
- Aspose OCR resources
language: it
og_description: Come disabilitare l'OCR in Aspose OCR per C# e farlo funzionare offline,
  estrarre testo da un'immagine senza necessità di internet e caricare l'immagine
  per l'OCR facilmente.
og_title: Come disabilitare l'OCR in C# – Guida offline di Aspose OCR
tags:
- C#
- OCR
- Aspose
- Offline Processing
title: Come disabilitare l'OCR in C# – Guida offline a Aspose OCR
url: /it/net/ocr-configuration/how-to-disable-ocr-in-c-offline-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come disabilitare OCR in C# – Guida offline Aspose OCR

Ti sei mai chiesto **come disabilitare OCR** quando hai bisogno di una soluzione veramente offline? Forse stai creando un'app desktop sicura che non può fare affidamento su una connessione di rete, o semplicemente vuoi evitare download inaspettati. In ogni caso, la buona notizia è che Aspose OCR ti permette di disattivare il recupero automatico delle risorse, puntare a una cartella locale e mantenere tutto on‑premises. In questo tutorial vedrai anche come **estrarre testo da immagine** e correttamente **caricare immagine per OCR** senza intoppi.

Percorreremo un esempio completo, pronto‑da‑eseguire, che mostra ogni passaggio—dall’inizializzazione del motore alla stampa del testo giapponese riconosciuto. Nessuna documentazione esterna, nessuna magia nascosta; solo codice C# puro che puoi inserire nel tuo progetto oggi. Alla fine saprai perché è importante disabilitare la funzione di auto‑download, come impostare il percorso delle risorse e quali insidie evitare.

## Prerequisiti

- .NET 6.0 (o qualsiasi versione recente di .NET) installato sulla tua macchina.  
- Pacchetto NuGet Aspose.OCR per .NET (`Install-Package Aspose.OCR`).  
- Una cartella che contiene già le risorse linguistiche di cui hai bisogno (ad esempio il modello giapponese).  
- Un file immagine (`japan_doc.png`) su cui vuoi eseguire l’OCR.  

Se ti mancano i language pack, scaricali una volta dal portale Aspose, estraili in una cartella come `AsposeOCRResources` e sei pronto. Nessun ulteriore download avverrà una volta disabilitata la funzione di auto‑download.

![Come disabilitare OCR offline](/images/how-to-disable-ocr.png "illustrazione su come disabilitare OCR")

## Passo 1 – Crea l'istanza del motore OCR  

La prima cosa da fare è istanziare `OcrEngine`. Pensa a questo oggetto come al cervello che leggerà la tua immagine.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class OfflineDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **Perché è importante:** Senza un motore non puoi configurare nulla. L'oggetto contiene tutte le impostazioni, incluso il flag cruciale che indica alla libreria se può accedere a Internet.

## Passo 2 – Disabilita il download automatico delle risorse  

Per impostazione predefinita Aspose OCR tenta di recuperare i file linguistici mancanti al volo. Per mantenere tutto offline, imposta lo switch `AutoDownloadResources` su `false`.

```csharp
        // Step 2: Disable automatic resource download to work offline
        ocrEngine.Settings.AutoDownloadResources = false;
```

> **Consiglio professionale:** Disattivarlo non solo garantisce la privacy, ma velocizza anche la prima esecuzione del riconoscimento perché il motore non perde tempo a controllare gli aggiornamenti.

## Passo 3 – Indica la cartella locale delle risorse  

Ora indica al motore dove vivono i language pack pre‑scaricati. Questo è il percorso che hai configurato nei prerequisiti.

```csharp
        // Step 3: Point the engine to the folder containing pre‑downloaded resources
        ocrEngine.Settings.ResourcesPath = @"YOUR_DIRECTORY/AsposeOCRResources";
```

> **Cosa potrebbe andare storto?** Se il percorso è errato o il file linguistico richiesto è mancante, il motore lancerà una `ResourceNotFoundException`. Controlla l'ortografia della cartella e verifica che il modello giapponese (`jpn.traineddata`) sia presente.

## Passo 4 – Seleziona il modello linguistico locale  

Scegli la lingua che hai effettivamente sul disco. Nel nostro esempio usiamo il giapponese, ma puoi sostituire `Language.Japanese` con qualsiasi altra lingua che hai scaricato.

```csharp
        // Step 4: Select the language model that is available locally
        ocrEngine.Settings.Language = Language.Japanese;
```

> **Caso limite:** Alcune lingue richiedono dizionari aggiuntivi (ad esempio il cinese). Assicurati che quei file ausiliari siano anch'essi nella stessa cartella delle risorse.

## Passo 5 – Carica l'immagine per OCR  

Ecco dove **carichiamo l'immagine per OCR**. Il metodo `ImageStream.FromFile` legge il file in uno stream che Aspose può elaborare.

```csharp
        // Step 5: Load the image you want to recognize
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/japan_doc.png");
```

> **Suggerimento:** I formati supportati includono PNG, JPEG, BMP e TIFF. Se devi gestire PDF, converti ogni pagina in un'immagine prima.

## Passo 6 – Esegui il processo di riconoscimento  

Ora il motore legge effettivamente i pixel e tenta di trasformarli in testo.

```csharp
        // Step 6: Run the OCR process
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

> **Perché questo passaggio può essere lento:** L'OCR è intensivo per la CPU, soprattutto per immagini ad alta risoluzione. Se le prestazioni sono un problema, considera di ridimensionare l'immagine prima del riconoscimento.

## Passo 7 – Stampa il testo estratto  

Infine, **estraiamo testo da immagine** e lo stampiamo sulla console.

```csharp
        // Step 7: Output the recognized text
        Console.WriteLine(ocrResult.Text);
    }
}
```

Eseguire il programma dovrebbe visualizzare i caratteri giapponesi presenti in `japan_doc.png`. Se tutto è configurato correttamente, vedrai un blocco pulito di testo Unicode sulla console.

### Output previsto

```
これはサンプルの日本語テキストです。
```

(Il tuo output effettivo dipenderà dal contenuto dell'immagine.)

## Problemi comuni e come evitarli  

| Problema | Perché accade | Soluzione |
|----------|----------------|-----------|
| **File linguistico mancante** | `AutoDownloadResources` è false, quindi il motore non può scaricarlo. | Verifica che `ResourcesPath` punti alla cartella contenente `jpn.traineddata`. |
| **Percorso immagine errato** | `ImageStream.FromFile` lancia `FileNotFoundException`. | Usa percorsi assoluti o assicurati che la directory di lavoro sia impostata correttamente. |
| **Formato immagine non supportato** | Aspose legge solo alcuni formati. | Converti la tua immagine in PNG o JPEG prima di chiamare `FromFile`. |
| **Out‑of‑memory con immagini grandi** | L'OCR carica l'intera immagine in memoria. | Ridimensiona o suddividi l'immagine, oppure aumenta il limite di memoria del processo. |

## Estendere l'esempio  

- **Elaborazione batch:** Scorri una directory di immagini, chiama lo stesso codice di riconoscimento e scrivi ogni risultato in un file `.txt` separato.  
- **Lingue diverse:** Sostituisci `Language.Japanese` con `Language.English` (o qualsiasi altra) dopo aver posizionato i file di risorsa corrispondenti.  
- **Pre‑elaborazione personalizzata:** Usa Aspose.Imaging per correggere l'inclinazione o migliorare il contrasto prima dell'OCR per una maggiore precisione.

## Conclusione  

Ora sai **come disabilitare OCR** in Aspose OCR per C# e farlo funzionare completamente offline. Impostando `AutoDownloadResources` su `false`, indicando al motore una cartella locale delle risorse e correttamente **caricando l'immagine per OCR**, puoi affidabilmente **estrarre testo da immagine** senza mai toccare Internet. Questo approccio è ideale per ambienti sicuri, pipeline CI o qualsiasi scenario in cui l'accesso alla rete è limitato.

Pronto per il passo successivo? Prova a elaborare un'intera cartella di PDF scansionati, sperimenta con diversi language pack o integra il risultato OCR in un database ricercabile. La configurazione offline che hai costruito oggi è una solida base per qualsiasi flusso di lavoro di elaborazione documenti on‑premises.

Buona programmazione, e sentiti libero di lasciare un commento se incontri difficoltà!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}