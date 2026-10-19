---
category: general
date: 2026-03-21
description: Scopri come correggere l'inclinazione dei file immagine e riconoscere
  il testo con Aspose OCR. Converti JPG in testo e correggi la rotazione dell'immagine
  in poche righe di codice C#.
draft: false
keywords:
- how to deskew image
- recognize text image
- convert jpg to text
- correct image rotation
- recognize text jpg
language: it
og_description: Come correggere l'inclinazione di un'immagine ed estrarre il testo
  da JPEG usando Aspose OCR. Segui questa guida passo‑passo per convertire jpg in
  testo e correggere la rotazione dell'immagine.
og_title: Come raddrizzare un'immagine in C# – Rapido tutorial OCR di Aspose
tags:
- OCR
- C#
- Aspose
title: Come rimuovere l'inclinazione di un'immagine in C# – Guida completa all'uso
  di Aspose OCR
url: /it/net/skew-angle-calculation/how-to-deskew-image-in-c-complete-guide-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come correggere l'inclinazione di un'immagine in C# – Guida completa con Aspose OCR

Ti sei mai chiesto **come correggere l'inclinazione di un'immagine** quando i file scannerizzati risultano inclinati di un angolo strano? Non sei l'unico: molti sviluppatori incontrano questo problema quando cercano di estrarre testo da ricevute, fatture o appunti scritti a mano. La buona notizia è che con Aspose OCR puoi correggere la rotazione dell'immagine e ottenere testo pulito e ricercabile in poche righe di codice.

In questo tutorial percorreremo l'intero processo: dall'installazione della libreria, all'abilitazione della correzione automatica dell'inclinazione, al riconoscimento dell'immagine di testo e infine alla conversione di un JPG in testo. Alla fine avrai un'app console pronta all'uso che **recognize text jpg** file senza doverli ruotare manualmente prima.

## Cosa ti serve

- **.NET 6.0** o successivo (il codice funziona sia su .NET Core che su .NET Framework)  
- Pacchetto NuGet **Aspose.OCR for .NET** – è consigliata la versione 23.12 o più recente  
- Un esempio di **JPEG inclinato** (ad es., `skewed_receipt.jpg`) posizionato in una cartella leggibile dall'app  
- Visual Studio, VS Code o qualsiasi editor C# tu preferisca  

Non sono necessari altri strumenti di terze parti. La libreria gestisce la correzione dell'inclinazione, l'OCR e persino il rilevamento della lingua internamente.

![esempio di correzione dell'inclinazione dell'immagine](/images/deskew-example.png "how to deskew image using Aspose OCR")

## Passo 1: Configurare il progetto e installare Aspose.OCR

Per mantenere le cose ordinate, avvia un nuovo progetto console:

```bash
dotnet new console -n DeskewDemo
cd DeskewDemo
dotnet add package Aspose.OCR --version 23.12.0
```

La riga `dotnet add package` scarica i binari **Aspose.OCR** più tutte le dipendenze native. Se sei su Windows otterrai automaticamente le DLL native; su Linux/macOS potresti dover installare il pacchetto `libgdiplus`, ma è un'installazione una tantum.

## Passo 2: Abilitare la correzione automatica dell'inclinazione (Correggere la rotazione dell'immagine)

Ora apri `Program.cs` e sostituisci il contenuto con il codice qui sotto. La riga chiave è `ocrEngine.Settings.Deskew = true;` – è il flag che indica al motore **come correggere l'inclinazione di un'immagine** automaticamente.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Create an OCR engine (CPU mode is fine for most desktop apps)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine();

            // ---------------------------------------------------------------
            // 2️⃣ Turn on deskewing – this corrects image rotation for us
            // ---------------------------------------------------------------
            ocrEngine.Settings.Deskew = true;   // <-- how to deskew image is handled here

            // ---------------------------------------------------------------
            // 3️⃣ Point the engine at the JPEG you want to process
            // ---------------------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/skewed_receipt.jpg";

            // ---------------------------------------------------------------
            // 4️⃣ Run OCR – the result already contains the corrected text
            // ---------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(imagePath);

            // ---------------------------------------------------------------
            // 5️⃣ Output the text – this is your “convert jpg to text” step
            // ---------------------------------------------------------------
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### Perché abilitare la correzione dell'inclinazione?

Quando uno scanner alimenta una pagina con un angolo, la linea di base del testo è inclinata. I motori OCR tradizionali leggerebbero ogni carattere come una versione inclinata, riducendo drasticamente l'accuratezza. Impostando `Deskew = true`, Aspose OCR esegue una rapida trasformata di Hough in background, ruota il bitmap in orizzontale e poi procede al riconoscimento. Il risultato è lo stesso di una rotazione manuale dell'immagine in Photoshop—ma più veloce e completamente automatizzato.

## Passo 3: Riconoscere l'immagine di testo e convertire JPG in testo

La chiamata `Recognize` fa due cose contemporaneamente:

1. **Corregge l'inclinazione** dell'immagine (perché abbiamo attivato il flag).  
2. **Estrae** il contenuto testuale, restituendolo in un oggetto `OcrResult`.

Puoi trattare `ocrResult.Text` come una semplice stringa, scriverla su file o passarla a pipeline di elaborazione successive. Se ti servono i punteggi di confidenza grezzi per parola, `ocrResult.Words` fornisce una collezione con valori `Confidence`.

### Esempio di output

Supponendo che `skewed_receipt.jpg` contenga una semplice ricevuta, potresti vedere qualcosa del genere:

```
=== Recognized Text ===
Store: Coffee Corner
Date: 2026-03-20
Item   Qty   Price
Latte   2    5.00
Bagel   1    2.50
Total          12.50
```

Nota come i numeri siano allineati correttamente nonostante l'immagine originale fosse ruotata di circa 7°. È la magia della **correzione della rotazione dell'immagine** integrata nella libreria.

## Passo 4: Eseguire l'esempio e verificare i risultati

Compila ed esegui:

```bash
dotnet run
```

Se tutto è configurato correttamente vedrai il testo estratto stampato sulla console. Se ottieni un'eccezione come `FileNotFoundException`, ricontrolla il percorso del tuo JPEG e assicurati che il file sia leggibile.

### Problemi comuni e consigli esperti

- **Immagini di grandi dimensioni** – L'uso di memoria dell'OCR cresce con le dimensioni dell'immagine. Ridimensiona file troppo grandi (ad es., > 3000 px di larghezza) prima di passarli al motore.  
- **Script non latini** – Per impostazione predefinita il motore assume l'inglese. Imposta `ocrEngine.Settings.Language = OcrLanguage.French;` (o qualsiasi lingua supportata) se devi **recognize text image** in altri alfabeti.  
- **Elaborazione batch** – Per molti file, riutilizza la stessa istanza di `OcrEngine`; creare un nuovo motore per ogni file introduce overhead inutile.  
- **Controllo di qualità** – Dopo la correzione dell'inclinazione puoi esportare il bitmap corretto con `ocrEngine.Settings.DeskewedImage.Save("corrected.jpg");` per verificare visivamente la rotazione.

## Esempio completo funzionante (tutto insieme)

Di seguito trovi il programma completo, autonomo, che puoi copiare‑incollare in `Program.cs`. Include commenti, gestione degli errori e un passaggio opzionale per salvare l'immagine corretta.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the input JPEG – change this to your actual file location
            string inputPath = @"YOUR_DIRECTORY\skewed_receipt.jpg";

            if (!File.Exists(inputPath))
            {
                Console.WriteLine($"Error: File not found – {inputPath}");
                return;
            }

            try
            {
                // 1️⃣ Create OCR engine (CPU mode is sufficient for most scenarios)
                var ocrEngine = new OcrEngine();

                // 2️⃣ Enable automatic deskewing – this is the core of how to deskew image
                ocrEngine.Settings.Deskew = true;

                // Optional: Save the corrected image to verify the rotation fix
                // ocrEngine.Settings.DeskewedImagePath = "corrected.jpg";

                // 3️⃣ Perform OCR – this simultaneously deskews and extracts text
                OcrResult result = ocrEngine.Recognize(inputPath);

                // 4️⃣ Output the recognized text – effectively convert jpg to text
                Console.WriteLine("=== Recognized Text ===");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                Console.WriteLine("An unexpected error occurred:");
                Console.WriteLine(ex.Message);
            }
        }
    }
}
```

Eseguendo il programma **recognize text jpg** file, correggerà automaticamente qualsiasi inclinazione e stamperà testo pulito e ricercabile sulla console.

## Conclusioni

Ora disponi di uno snippet solido, pronto per la produzione, che mostra **come correggere l'inclinazione di un'immagine** e estrarne il contenuto usando Aspose OCR. L'approccio funziona per ricevute, fatture, contratti scannerizzati o qualsiasi JPEG in cui il testo non è perfettamente orizzontale. 

Prossimi passi da esplorare:

- **Elaborazione batch** di una cartella di JPEG e scrittura di ogni risultato in un file `.txt` (collegato a *convert jpg to text*).  
- Integrazione del passaggio OCR in un'API ASP.NET Core così che i client possano caricare immagini e ricevere testo in formato JSON.  
- Sperimentare con diverse impostazioni OCR come `ocrEngine.Settings.Language` o `ocrEngine.Settings.RecognitionMode` per migliorare l'accuratezza su documenti non inglesi.  

Provalo, modifica le impostazioni e lascia che il motore faccia il lavoro pesante. Come sempre, se incontri difficoltà o vuoi condividere un'ottimizzazione intelligente, lascia un commento qui sotto. Buon coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}