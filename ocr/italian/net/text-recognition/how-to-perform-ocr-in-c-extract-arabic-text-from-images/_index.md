---
category: general
date: 2026-03-17
description: Impara come eseguire l'OCR in C# per estrarre testo arabo, riconoscere
  il testo da un'immagine e convertire l'immagine in testo con un esempio di codice
  completo.
draft: false
keywords:
- how to perform OCR
- extract arabic text
- recognize text from image
- convert image to text
- extract text from image
language: it
og_description: Come eseguire l'OCR in C#? Questa guida ti mostra come estrarre testo
  arabo, riconoscere il testo da un'immagine e convertire l'immagine in testo in pochi
  passaggi.
og_title: Come eseguire OCR in C# – Estrarre testo arabo
tags:
- OCR
- C#
- Arabic
- ImageProcessing
title: Come eseguire OCR in C# – Estrarre testo arabo dalle immagini
url: /it/net/text-recognition/how-to-perform-ocr-in-c-extract-arabic-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR in C# – Estrarre testo arabo da immagini

Ti sei mai chiesto **come eseguire OCR** su una fattura araba o su un documento scansionato? Non sei l'unico: molti sviluppatori si trovano in difficoltà quando devono estrarre caratteri arabi da un bitmap. La buona notizia è che, con poche righe di C#, puoi riconoscere il testo da file immagine, convertire l'immagine in testo e, infine, **estrarre testo arabo** per l'elaborazione successiva.

In questo tutorial percorreremo un esempio completo e funzionante che mostra esattamente come eseguire OCR, perché ogni passaggio è importante e a cosa fare attenzione quando si lavora con script da destra a sinistra. Alla fine sarai in grado di **estrarre testo da immagine** in arabo, urdu, curdo o qualsiasi lingua supportata dal motore OCR.

## Prerequisiti

- .NET 6.0 o successivo (il codice si compila anche con .NET Core)  
- Un riferimento alla libreria OCR che fornisce `OcrEngine` (ad es., `MyOcrSdk.dll`).  
- Un file immagine che contiene testo arabo, come `invoice_arabic.png`.  
- Familiarità di base con le applicazioni console C#.

> **Consiglio:** Se non hai a disposizione un SDK OCR, l'edizione community gratuita di *MyOcrSdk* funziona per i test e supporta le lingue che utilizzeremo.

---

## Passo 1 – Configurare il progetto e importare lo spazio dei nomi OCR

Prima di poter **riconoscere testo da immagine** abbiamo bisogno di uno scheletro di progetto e delle direttive `using` corrette.

```csharp
using System;
using MyOcrSdk;          // <-- Replace with the actual namespace of your OCR library
using MyOcrSdk.IO;       // For ImageStream helper class

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // The rest of the OCR workflow will go here
        }
    }
}
```

*Perché è importante:* L'importazione dei namespace corretti ti dà accesso a `OcrEngine`, `Language` e `ImageStream`. Saltare questo passaggio genera errori di compilazione frustranti per i principianti.

---

## Passo 2 – Creare un'istanza del motore OCR (Parola chiave primaria inclusa)

Ora eseguiamo effettivamente **OCR** istanziando il motore.

```csharp
// Step 2: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

L'oggetto `OcrEngine` è il cuore dell'operazione; contiene la configurazione, esegue il lavoro pesante e restituisce l'oggetto risultato contenente la stringa estratta. Pensalo come il “cervello” che **convertirà immagine in testo**.

---

## Passo 3 – Scegliere la lingua per il riconoscimento

Arabo, Urdu, Curdo… condividono la stessa famiglia di script, quindi dobbiamo indicare al motore quale lingua aspettarsi. Questo migliora drasticamente la precisione.

```csharp
// Step 3: Choose the language for recognition (Arabic, Urdu, Kurdish, etc.)
ocrEngine.Config.Language = Language.Arabic;   // You can switch to Language.Urdu, etc.
```

*Perché è importante:* I motori OCR si basano su modelli linguistici. Selezionare il modello corretto riduce gli errori di riconoscimento di caratteri simili, soprattutto per gli script da destra a sinistra.

---

## Passo 4 – Caricare l'immagine contenente il testo

Ci serve un bitmap che il motore possa analizzare. L'helper `ImageStream.FromFile` astrae i dettagli di I/O del file.

```csharp
// Step 4: Load the image that contains the text to be recognized
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/invoice_arabic.png");
```

Assicurati che il percorso punti a un'**immagine valida**. Se il file è mancante o corrotto, il motore lancerà un'eccezione e non potrai **estrarre testo da immagine** con successo.

---

## Passo 5 – Eseguire il processo OCR e recuperare il risultato

Infine, chiamiamo `Recognize()` e mostriamo la stringa estratta.

```csharp
// Step 5: Perform the OCR operation
var ocrResult = ocrEngine.Recognize();

// Step 6: Display the extracted text
Console.WriteLine("=== Extracted Arabic Text ===");
Console.WriteLine(ocrResult.Text);
```

La proprietà `ocrResult.Text` contiene la rappresentazione in testo semplice di tutto ciò che il motore è riuscito a leggere. Nella maggior parte dei casi vedrai una combinazione di caratteri arabi e numeri, perfetta per ulteriori elaborazioni come inserimento in database o traduzione.

### Output previsto

```
=== Extracted Arabic Text ===
فاتورة رقم: 12345
التاريخ: 2026/03/15
المبلغ: 2500.00 ريال
...
```

Se vedi caratteri illeggibili, ricontrolla l'impostazione della lingua e assicurati che l'immagine sia ad alta risoluzione (300 dpi o più è l'ideale).

---

## Esempio completo funzionante

Di seguito trovi il **programma completo e autonomo** che puoi copiare‑incollare in un nuovo progetto console e avviare subito.

```csharp
// Full OCR demo – extracts Arabic text from an image
using System;
using MyOcrSdk;
using MyOcrSdk.IO;

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Set language – Arabic (change to Urdu or Kurdish if needed)
            ocrEngine.Config.Language = Language.Arabic;

            // 3️⃣ Load the source image
            // Replace YOUR_DIRECTORY with the folder that holds your PNG/JPG
            string imagePath = @"YOUR_DIRECTORY/invoice_arabic.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            try
            {
                // 4️⃣ Run OCR
                var result = ocrEngine.Recognize();

                // 5️⃣ Output the text
                Console.WriteLine("=== Extracted Arabic Text ===");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                // Graceful error handling – useful when you need to **extract text from image** in batch jobs
                Console.Error.WriteLine($"OCR failed: {ex.Message}");
            }
        }
    }
}
```

> **Nota:** Se il tuo SDK OCR richiede una licenza, assicurati di inizializzarla prima del passo 1 (ad es., `OcrEngine.SetLicense("YOUR_LICENSE_KEY");`). Questa riga è stata omessa per brevità.

---

## Gestione dei casi limite più comuni

| Situazione | Perché accade | Soluzione rapida |
|------------|---------------|------------------|
| **Immagine sfocata o a bassa risoluzione** | La precisione OCR scende sotto il 70 % | Scansiona a 300 dpi, oppure ingrandisci usando un algoritmo bicubico prima di passare al motore. |
| **Lingue miste (Arabo + Inglese)** | Il motore può fermarsi al primo blocco linguistico | Abilita la modalità multilingua: `ocrEngine.Config.Language = Language.Arabic \| Language.English;` |
| **Problemi di visualizzazione da destra a sinistra** | La console stampa i caratteri da sinistra a destra, facendo apparire l'arabo invertito | Usa `Console.OutputEncoding = System.Text.Encoding.UTF8;` e un terminale che supporti script RTL. |
| **PDF di grandi dimensioni suddivisi in molte pagine** | Il consumo di memoria aumenta | Processa una pagina alla volta: carica ogni pagina come immagine separata e ripeti il flusso OCR. |
| **Simboli speciali (valuta, date)** | Alcuni modelli OCR li trattano come rumore | Post‑processa `ocrResult.Text` con una regex per normalizzare i pattern noti. |

---

## Estendere la soluzione – Da OCR a estrazione dati

Ora che **sai come eseguire OCR**, potresti chiederti: *Cosa posso fare con il testo arabo estratto?* Ecco alcune idee che nascono naturalmente:

1. **Analizzare fatture** – Usa espressioni regolari per estrarre numeri di fattura, date e totali.  
2. **Inviare a un'API di traduzione** – Invia la stringa araba a Azure Translator o Google Cloud Translate.  
3. **Memorizzare in un database** – Inserisci il testo pulito in una tabella SQL per reportistica.  
4. **Attivare workflow** – Combinalo con una coda di messaggi (ad es., RabbitMQ) per avviare elaborazioni successive.

Tutti questi scenari ruotano attorno alla stessa operazione di base: **convertire immagine in testo**, poi manipolare il risultato.

---

## Conclusione

Abbiamo coperto tutto ciò che serve per **eseguire OCR** in C# e **estrarre testo arabo** da un'immagine. Dalla configurazione del progetto, abbiamo istanziato un `OcrEngine`, impostato la lingua, caricato un bitmap, eseguito il riconoscimento e stampato il risultato. Abbiamo anche discusso le difficoltà più comuni e mostrato come estendere il flusso di base in pipeline reali.

Provalo – cambia il percorso dell'immagine, imposta la lingua su Urdu, o collega l'output a un database. Il cielo è il limite una volta che riesci a **riconoscere testo da immagine** e **convertire immagine in testo** in modo affidabile.

---

### Argomenti correlati da esplorare

- **Estrarre testo da immagine** usando Tesseract OCR (alternativa open‑source)  
- **Elaborazione OCR batch** per migliaia di PDF scansionati  
- **Migliorare la precisione OCR** con pre‑elaborazione dell'immagine (soglia, rimozione rumore)  
- **Gestire script da destra a sinistra** nei framework UI .NET (WPF, WinForms)

Sentiti libero di lasciare un commento se incontri problemi, o di condividere come hai adattato questo modello ai tuoi progetti. Buon coding!  

![esempio di come eseguire OCR](images/ocr_flow.png "esempio di come eseguire OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}