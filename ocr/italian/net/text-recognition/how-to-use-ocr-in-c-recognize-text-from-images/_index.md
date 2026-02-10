---
category: general
date: 2026-02-09
description: Come utilizzare l'OCR in C# per riconoscere il testo da un'immagine,
  estrarre il testo e convertire l'immagine in testo con Aspose OCR. Guida completa
  passo passo.
draft: false
keywords:
- how to use OCR
- recognize text from image
- extract text from image
- convert image to text
- load image stream
language: it
og_description: Come utilizzare l'OCR in C# per riconoscere il testo da un'immagine,
  estrarre il testo e convertire l'immagine in testo con Aspose OCR. Guida completa
  con codice.
og_title: Come usare l'OCR in C# – Riconoscere il testo dalle immagini
tags:
- C#
- Aspose OCR
- Image Processing
title: Come usare l'OCR in C# – Riconoscere il testo dalle immagini
url: /it/net/text-recognition/how-to-use-ocr-in-c-recognize-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come utilizzare OCR in C# – Riconoscere il testo dalle immagini

Ti sei mai chiesto **come usare OCR** per trasformare uno screenshot in testo modificabile? Non sei solo. Molti sviluppatori si trovano in difficoltà quando devono *riconoscere il testo da un'immagine* ma non hanno un esempio chiaro e pronto all'uso.  

In questo tutorial percorreremo l'intero processo—caricare una licenza, creare un motore, fornire uno stream di immagine e infine estrarre il testo semplice. Alla fine sarai in grado di **estrarre testo da immagine**, **convertire immagine in testo**, e comprendere le sfumature della gestione di **load image stream**.

> **Cosa otterrai:** un programma C# completo e eseguibile che utilizza Aspose.OCR, spiegazioni di ogni passaggio e consigli per evitare gli errori più comuni.

---

## Prerequisiti

- .NET 6.0 o versioni successive (l'API funziona anche con .NET Framework 4.6+)  
- Pacchetto NuGet Aspose.OCR per .NET (`Aspose.OCR`) installato  
- Un file di licenza Aspose OCR valido (`Aspose.OCR.lic`) – la versione di prova è gratuita ma aggiunge una filigrana.  
- Un'immagine (`sample.jpg`) contenente testo chiaro e leggibile da macchina.

> **Suggerimento:** Se utilizzi Visual Studio, il comando della console NuGet è  
> `Install-Package Aspose.OCR -Version 23.10` (sostituisci con l'ultima versione).

---

## Come utilizzare OCR: Caricare la licenza e inizializzare il motore

La prima cosa da fare è informare Aspose che possiedi una licenza. Saltare questo passaggio farà comunque funzionare il programma, ma una filigrana apparirà nell'output e perderai tempo prezioso in controlli della modalità di prova.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Licensing;

class LicenseExample
{
    static void Main()
    {
        // Step 1 – Load the Aspose OCR license (replace with your .lic file path)
        License ocrLicense = new License();
        ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

        // Step 2 – Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // The rest of the steps follow...
    }
}
```

**Perché è importante:** L'oggetto `License` disabilita la filigrana di prova e sblocca l'intero set di funzionalità, che include modelli ad alta precisione e supporto multilingua.  

> **Consiglio professionale:** Mantieni il file di licenza al di fuori del repository di controllo versione. Usa variabili d'ambiente o un vault sicuro per iniettare il percorso a runtime.

---

## Passo 2 – Caricare uno stream di immagine (e perché è migliore di un percorso file)

Quando *carichi lo stream di immagine* invece di passare un percorso file grezzo, ottieni flessibilità: l'immagine può provenire da un database, da una richiesta web o da un array di byte in memoria.  

```csharp
// Step 3 – Load the image you want to recognize
// Using ImageStream.FromFile is the simplest way for local files.
ImageStream imageStream = ImageStream.FromFile(@"C:\Images\sample.jpg");

// Alternative: load from a byte array (e.g., when the image is uploaded via HTTP)
// byte[] imageBytes = ... // get from request
// ImageStream imageStream = ImageStream.FromBytes(imageBytes);
```

**Spiegazione:** `ImageStream` astrae la sorgente sottostante, consentendo al motore OCR di trattare tutto in modo uniforme. Se in seguito cambi a un bucket di storage cloud, devi solo modificare il modo in cui crei `ImageStream`; il resto del codice rimane invariato.

---

## Passo 3 – Riconoscere il testo dall'immagine

Ora arriva il cuore della questione: **riconoscere il testo dall'immagine**. Il metodo `OcrEngine.Recognize` esegue i modelli di rete neurale forniti con Aspose e restituisce un oggetto `OcrResult` contenente diverse proprietà utili.

```csharp
// Step 4 – Run the OCR process on the image
OcrResult ocrResult = ocrEngine.Recognize(imageStream);
```

**Cosa contiene `OcrResult`?**  
- `PlainText` – una singola stringa con tutti i caratteri rilevati.  
- `Words` – una collezione di oggetti parola con riquadri di delimitazione (utile per evidenziare).  
- `Lines` – raggruppamento a livello di riga, utile per preservare le interruzioni di paragrafo.

Se ti serve solo il testo grezzo, `PlainText` è il percorso più veloce. Per scenari più avanzati (ad esempio sovrapporre i risultati sull'immagine originale), esplora `Words` e `Lines`.

---

## Passo 4 – Visualizzare o salvare il testo estratto

Infine, stampiamo il testo riconosciuto sulla console. In un'app reale potresti scriverlo su un database, su un file o inviarlo tramite un'API.

```csharp
// Step 5 – Display the recognized plain text (watermark omitted with a full license)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.PlainText);
Console.WriteLine("==================");

// Optional: Save to a .txt file
System.IO.File.WriteAllText(@"C:\Output\extracted.txt", ocrResult.PlainText);
```

**Output previsto:**  
Se `sample.jpg` contiene la frase *“Hello World!”*, vedrai:

```
=== OCR Output ===
Hello World!
==================
```

Quando si utilizza una licenza di prova, l'output includerà una piccola filigrana “Aspose OCR Demo” alla fine del testo. Con una licenza completa, scompare completamente.

---

## Esempio completo funzionante (pronto per copia‑incolla)

Di seguito trovi l'intero programma, pronto per la compilazione. Sostituisci i percorsi con le tue posizioni e sei pronto a partire.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Licensing;

class LicenseExample
{
    static void Main()
    {
        // 1️⃣ Load license – required for production use
        License ocrLicense = new License();
        ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

        // 2️⃣ Create OCR engine – the core processing object
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Load image – you can also use ImageStream.FromBytes for in‑memory data
        ImageStream imageStream = ImageStream.FromFile(@"C:\Images\sample.jpg");

        // 4️⃣ Recognize text – this is where the magic happens
        OcrResult ocrResult = ocrEngine.Recognize(imageStream);

        // 5️⃣ Output the plain text – perfect for further processing
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.PlainText);
        Console.WriteLine("==================");

        // Optional: persist the result
        System.IO.File.WriteAllText(@"C:\Output\extracted.txt", ocrResult.PlainText);
    }
}
```

> **Ricorda:** Il codice sopra **estrae testo da immagine** e **converte immagine in testo** in una singola chiamata. Nessun ciclo extra, nessuna gestione manuale dei pixel—Aspose fa il lavoro pesante.

---

## Domande comuni e casi limite

### Cosa fare se la mia immagine è sfocata o a basso contrasto?

Aspose OCR include opzioni di pre‑elaborazione (ad esempio `ocrEngine.ImagePreprocessor`). Puoi abilitare la binarizzazione o la correzione dell'inclinazione prima del riconoscimento:

```csharp
ocrEngine.ImagePreprocessor = new ImagePreprocessor
{
    Binarization = true,
    Deskew = true
};
```

### Come gestire più lingue?

Imposta la proprietà `Language` sul motore:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

Il motore cercherà quindi di rilevare entrambe le lingue automaticamente.

### Posso elaborare PDF invece di JPEG?

Sì—Aspose OCR può leggere i PDF direttamente, ma avrai bisogno della libreria Aspose.PDF per estrarre ogni pagina come immagine, quindi fornire lo stream di immagine al motore OCR.

### E per grandi batch?

Racchiudi la logica di riconoscimento in un ciclo e riutilizza la stessa istanza di `OcrEngine`. Creare un nuovo motore per immagine aggiunge un overhead non necessario.

## Consigli professionali per OCR pronto alla produzione

- **Cache l'oggetto licenza**: caricalo una sola volta all'avvio dell'applicazione, non per ogni richiesta.  
- **Riutilizza `OcrEngine`**: il motore mantiene buffer interni; riutilizzarlo riduce la pressione sul GC.  
- **Limita la dimensione dell'immagine**: immagini molto grandi (>5 MP) aumentano notevolmente il tempo di elaborazione. Ridimensiona a 150‑300 DPI se l'alta risoluzione non è necessaria.  
- **Convalida l'output**: OCR non è perfetto; implementa un semplice controllo di confidenza (`ocrResult.Words.Average(w => w.Confidence)`) e segnala i risultati a bassa confidenza per una revisione manuale.  
- **Sicurezza dei thread**: `OcrEngine` non è thread‑safe. Crea istanze separate per thread o utilizza un pattern di pool.

## Conclusione

Abbiamo coperto **come usare OCR** in C# dal caricamento di una licenza all'estrazione di testo pulito e ricercabile. Seguendo i passaggi sopra potrai **riconoscere il testo dall'immagine**, **estrarre testo da immagine**, e convertire facilmente **immagine in testo** mentre domini il pattern **load image stream** che rende il tuo codice flessibile per future fonti di dati.

Pronto per la prossima sfida? Prova ad aggiungere il ritaglio di regioni di interesse, integrare con Azure Blob storage, o alimentare l'output OCR in una pipeline di elaborazione del linguaggio naturale. Il cielo è il limite, e ora hai una solida base su cui costruire.

![Diagramma che mostra il flusso OCR: carica licenza → crea motore → carica stream di immagine → riconosci → output testo](image-placeholder.png "come usare OCR per riconoscere il testo da immagine")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}