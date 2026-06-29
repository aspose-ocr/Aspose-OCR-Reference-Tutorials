---
category: general
date: 2026-06-28
description: Esegui OCR su un'immagine usando Aspose.OCR in C#. Impara a riconoscere
  il testo dall'immagine, estrarre il testo da una fattura, caricare l'immagine per
  l'OCR e scrivere JSON su file.
draft: false
keywords:
- perform OCR on image
- recognize text from image
- write JSON to file
- extract text from invoice
- load image for OCR
language: it
og_description: Esegui OCR su un'immagine con Aspose.OCR in C#. Questa guida mostra
  come riconoscere il testo da un'immagine, estrarre il testo da una fattura e scrivere
  JSON su un file.
og_title: Esegui OCR su un'immagine in C# – Tutorial OCR di Aspose
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Perform OCR on image using Aspose.OCR in C#. Learn to recognize text
    from image, extract text from invoice, load image for OCR and write JSON to file.
  headline: Perform OCR on Image in C# – Complete Aspose Guide
  type: TechArticle
- description: Perform OCR on image using Aspose.OCR in C#. Learn to recognize text
    from image, extract text from invoice, load image for OCR and write JSON to file.
  name: Perform OCR on Image in C# – Complete Aspose Guide
  steps:
  - name: What if the image contains multiple languages?
    text: 'Aspose.OCR automatically detects the language based on the character set.
      If you need to force a specific language (e.g., English for most invoices),
      set the `Language` property on the engine:'
  - name: How do I handle large PDFs with many pages?
    text: Convert each page to an image first (using a PDF‑to‑image library) and then
      loop through the images, applying the same **perform OCR on image** routine.
      Aggregate the JSON results into a single array if you want a consolidated output.
  - name: Can I stream the JSON instead of writing a whole file?
    text: 'Yes. If you’re building a web API, you can return `json` directly as the
      response body:'
  - name: What about performance?
    text: The OCR engine runs synchronously in the example above. For high‑throughput
      scenarios, wrap the recognition call in `Task.Run` or use the asynchronous versions
      (if available) to keep your UI responsive or to parallelize batch processing.
  type: HowTo
tags:
- Aspose.OCR
- C#
- JSON
- ImageProcessing
title: Esegui OCR su immagine in C# – Guida completa Aspose
url: /it/net/text-recognition/perform-ocr-on-image-in-c-complete-aspose-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esegui OCR su Immagine in C# – Guida Completa Aspose

Hai mai avuto bisogno di **perform OCR on image** file ma non eri sicuro quale libreria .NET ti avrebbe fornito risultati puliti e strutturati? Non sei solo—gli sviluppatori chiedono costantemente come **recognize text from image** asset, soprattutto quando si tratta di fatture o ricevute. In questo tutorial percorreremo un esempio pratico che non solo **loads image for OCR**, ma anche **extracts text from invoice** data e **writes JSON to file** per l'elaborazione a valle.

Al termine di questa guida avrai un'app console pronta‑all'uso che:

* Istanzia un motore Aspose OCR,
* Carica un'immagine PNG (o JPG),
* Riconosce il contenuto testuale,
* Serializza il risultato come JSON formattato in modo leggibile,
* Salva quel JSON su disco.

Nessun servizio esterno, nessuna magia nascosta—solo puro codice C# che puoi copiare, incollare ed eseguire.

## Prerequisiti

Prima di immergerci, assicurati di avere:

* .NET 6 SDK o versioni successive (il codice funziona sia con .NET Core che con .NET Framework).
* Una licenza valida di Aspose.OCR o una chiave di valutazione temporanea (la prova gratuita è sufficiente per i test).
* Visual Studio 2022, VS Code, o qualsiasi IDE preferisci.
* Un file immagine—ad esempio `invoice.png`—posizionato in un percorso a cui puoi fare riferimento con un percorso assoluto o relativo.

> **Consiglio professionale:** Se stai gestendo fatture scansionate, considera la pre‑elaborazione dell'immagine (raddrizzamento, aumento del contrasto) prima di passarla al motore OCR. Aspose.OCR gestisce automaticamente molte di queste operazioni, ma un'immagine sorgente pulita fornisce sempre risultati migliori.

---

## Passo 1: Configura il Progetto e Installa Aspose.OCR

Per prima cosa, crea un nuovo progetto console e aggiungi il pacchetto NuGet Aspose.OCR.

```bash
dotnet new console -n OcrInvoiceDemo
cd OcrInvoiceDemo
dotnet add package Aspose.OCR
```

> **Perché questo passo è importante:** L'assembly `Aspose.OCR` fornisce la classe `OcrEngine` che useremo per **perform OCR on image** data. Senza il pacchetto, il compilatore non riconoscerà alcun tipo relativo all'OCR.

---

## Passo 2: Carica Immagine per OCR

Ora scriveremo il codice che **load image for OCR**. Il metodo `OcrImage.FromFile` accetta un percorso assoluto o relativo e avvolge il bitmap in un formato comprensibile al motore.

```csharp
using Aspose.OCR;
using System.IO;

// Replace with the actual path to your invoice image
string imagePath = @"YOUR_DIRECTORY\invoice.png";

// Step 2: Load the image
OcrImage image = OcrImage.FromFile(imagePath);
```

> **Spiegazione:** Separando il percorso in una sua variabile manteniamo il codice ordinato e lo rendiamo facile da riutilizzare in seguito (ad esempio, durante il logging o il debug). Se il file non viene trovato, `FromFile` lancia una `FileNotFoundException`, che puoi catturare per fornire un messaggio di errore amichevole.

---

## Passo 3: Esegui OCR su Immagine e Riconosci Testo

Con l'immagine a disposizione, creiamo un'istanza di `OcrEngine` e le chiediamo di **recognize text from image**. Questo passo è il cuore del tutorial—qui avviene la vera magia dell'OCR.

```csharp
// Step 3: Create OCR engine and recognize text
using var ocrEngine = new OcrEngine();   // IDisposable, so we use 'using'
OcrResult ocrResult = ocrEngine.Recognize(image);
```

> **Perché usiamo `using var`:** L'`OcrEngine` contiene risorse non gestite (librerie native). Avvolgerlo in un blocco `using` garantisce una corretta disposizione, prevenendo perdite di memoria—specialmente importante nei servizi a lungo termine.

> **Cosa ottieni:** `ocrResult` contiene il testo grezzo, i punteggi di confidenza e le informazioni di layout (linee, parole, riquadri). Per la maggior parte delle pipeline di elaborazione fatture, la proprietà `Text` è sufficiente, ma i metadati aggiuntivi possono aiutare nella validazione o nel debug visivo.

---

## Passo 4: Converti il Risultato in JSON Formattato

Aspose.OCR rende banale **write JSON to file** perché `OcrResult` offre il metodo `ToJson`. Passando `indent: true` otteniamo un output leggibile dall'uomo, utile quando devi **extract text from invoice** record in seguito.

```csharp
// Step 4: Serialize OCR result to JSON
string json = ocrResult.ToJson(indent: true);
```

> **Esempio di snippet JSON** (troncato per brevità):

```json
{
  "Text": "Invoice #12345\nDate: 2026-06-01\nTotal: $1,250.00",
  "Confidence": 0.97,
  "Regions": [...]
}
```

> **Nota caso limite:** Se il motore OCR non rileva alcun testo, `ocrResult.Text` sarà una stringa vuota, ma il JSON conterrà comunque metadati come le dimensioni dell'immagine. Puoi proteggerti da risultati vuoti prima di scrivere il file.

---

## Passo 5: Scrivi JSON su File

Ora finalmente **write JSON to file**. Usare `File.WriteAllText` garantisce che l'intera stringa venga scritta su disco in un'unica operazione atomica.

```csharp
// Step 5: Save JSON output
string jsonPath = @"YOUR_DIRECTORY\invoice.json";
File.WriteAllText(jsonPath, json);
Console.WriteLine($"JSON saved to {jsonPath}");
```

> **Consigli per la produzione:** Considera di aggiungere un timestamp al nome del file (`invoice_20260628_1500.json`) per evitare di sovrascrivere esecuzioni precedenti. Inoltre, avvolgi l'operazione di scrittura in un blocco try/catch per gestire i problemi di permessi in modo elegante.

---

## Passo 6: Esempio Completo Funzionante

Mettendo insieme tutti i pezzi, ecco il programma completo che puoi compilare ed eseguire subito. Sostituisci `YOUR_DIRECTORY` con la cartella che contiene `invoice.png`.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonExportExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        using var ocrEngine = new OcrEngine();

        // Step 2: Load the image for OCR
        string imagePath = @"YOUR_DIRECTORY\invoice.png";
        OcrImage image = OcrImage.FromFile(imagePath);

        // Step 3: Perform OCR and recognize text from image
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Step 4: Convert the recognition result to pretty‑printed JSON
        string json = ocrResult.ToJson(indent: true);

        // Step 5: Write JSON to file
        string jsonPath = @"YOUR_DIRECTORY\invoice.json";
        File.WriteAllText(jsonPath, json);

        // Step 6: Inform the user
        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

**Output previsto** quando esegui il programma:

```
JSON saved to C:\Invoices\invoice.json
```

---

## Domande Frequenti & Casi Limite

### E se l'immagine contiene più lingue?

Aspose.OCR rileva automaticamente la lingua in base al set di caratteri. Se devi forzare una lingua specifica (ad esempio, English per la maggior parte delle fatture), imposta la proprietà `Language` sul motore:

```csharp
ocrEngine.Language = OcrLanguage.English;
```

### Come gestire PDF di grandi dimensioni con molte pagine?

Converti prima ogni pagina in un'immagine (usando una libreria PDF‑to‑image) e poi itera le immagini, applicando la stessa routine **perform OCR on image**. Aggrega i risultati JSON in un unico array se desideri un output consolidato.

### Posso trasmettere lo JSON invece di scrivere un intero file?

Sì. Se stai costruendo un'API web, puoi restituire `json` direttamente come corpo della risposta:

```csharp
return Results.Json(ocrResult);
```

### E per le prestazioni?

Il motore OCR viene eseguito in modo sincrono nell'esempio sopra. Per scenari ad alto throughput, avvolgi la chiamata di riconoscimento in `Task.Run` o usa le versioni asincrone (se disponibili) per mantenere l'interfaccia reattiva o per parallelizzare l'elaborazione batch.

---

## Conclusione

Abbiamo illustrato una soluzione concisa, end‑to‑end, che **perform OCR on image** file, **recognize text from image**, **extract text from invoice** e infine **write JSON to file** usando Aspose.OCR in C#. Il codice è deliberatamente semplice così da poterlo adattare a flussi di lavoro più complessi—che si tratti di aggiungere pre‑elaborazione dell'immagine, inserire il JSON in un database o esporre il risultato tramite un endpoint REST.

Pronto per il passo successivo? Prova a sostituire il PNG con un JPEG, sperimenta impostazioni OCR diverse (come `ocrEngine.Dpi`) o integra una fase di conversione PDF‑to‑image per gestire interi pacchetti di fatture. Il cielo è il limite una volta che avrai padroneggiato le basi.

Buon coding, e che i tuoi risultati OCR siano sempre nitidi e precisi!

## Cosa Dovresti Imparare Dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell'API ed esplorare approcci alternativi di implementazione nei tuoi progetti.

- [Come utilizzare Aspose OCR per risultato JSON nel riconoscimento di immagini](/ocr/english/net/text-recognition/get-result-as-json/)
- [Estrai testo da immagine C# con selezione della lingua usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Estrai testo da immagine – Riconosci linea con Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}