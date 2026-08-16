---
category: general
date: 2026-04-03
description: Scopri come eseguire l'OCR in C# ed estrarre il testo da un'immagine
  usando Aspose OCR, con il controllo ortografico per la lingua russa.
draft: false
keywords:
- how to perform OCR
- extract text from image
- convert image to text
- how to spell check
- ocr russian language
language: it
og_description: Scopri come eseguire l'OCR in C# ed estrarre il testo da un'immagine
  usando Aspose OCR, con il controllo ortografico per la lingua russa.
og_title: Come eseguire l'OCR in C# – Estrarre il testo dall'immagine
tags:
- OCR
- C#
- Aspose
- SpellCheck
title: Come eseguire OCR in C# – Estrarre testo da un'immagine
url: /it/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR in C# – Estrarre testo da immagine

Ti sei mai chiesto **come eseguire OCR** su una foto di una nota scritta a mano? Forse hai una ricevuta scansionata, un cartello in una lingua straniera, o una pagina PDF che si rifiuta di copiare‑incollare. La buona notizia? Con poche righe di C# e la libreria Aspose OCR puoi trasformare quell’immagine in testo modificabile in un attimo.  

In questa guida non solo ti mostreremo **come eseguire OCR**, ma ti guideremo anche attraverso **estrarre testo da immagine**, **convertire immagine in testo**, e persino **come controllare l'ortografia** del risultato quando lavori con documenti in lingua russa. Sembra molto? Rimani con noi – spiegheremo tutto passo dopo passo.

## Cosa imparerai

Alla fine di questo tutorial sarai in grado di:

* Configurare Aspose OCR per il supporto della lingua russa.  
* Caricare un file immagine ed eseguire il riconoscimento ottico dei caratteri per **estrarre testo da immagine**.  
* Utilizzare il correttore ortografico integrato per correggere automaticamente le parole errate – la risposta perfetta a “**come controllare l'ortografia**” dell'output OCR.  
* Stampare la stringa pulita sulla console, pronta per ulteriori elaborazioni o archiviazione.

**Prerequisiti** – avrai bisogno di:

* .NET 6.0 o successivo (il codice funziona anche con .NET Framework 4.8).  
* Una licenza valida di Aspose OCR o una chiave di valutazione temporanea.  
* Un file immagine che contiene testo russo (per la demo lo chiameremo `russian_note.jpg`).  

Se qualcuno di questi ti è sconosciuto, nessun problema. I passaggi seguenti includono il comando NuGet esatto per aggiungere Aspose OCR, e il codice è completamente autonomo.

![esempio di come eseguire OCR](/images/ocr-demo.png "esempio di come eseguire OCR in C#")

## Passo 1 – Installa Aspose OCR e aggiungi i namespace

Prima di tutto, hai bisogno della libreria. Apri un terminale nella cartella del tuo progetto ed esegui:

```bash
dotnet add package Aspose.OCR
```

Quel comando scarica l'ultima versione stabile (a partire da aprile 2026 è la 22.9). Dopo il ripristino del pacchetto, aggiungi le direttive `using` richieste all'inizio del tuo file C#:

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System.Drawing;
```

*Suggerimento:* Se usi Visual Studio, l'IDE suggerirà di aggiungerle automaticamente non appena digiti il nome della prima classe.

## Passo 2 – Inizializza il motore OCR per la lingua russa

La parte **come eseguire OCR** inizia creando un'istanza di `OcrEngine`. Specificando `OcrLanguage.Russian` indichiamo al motore di caricare il set di caratteri cirillico e le euristiche specifiche della lingua.

```csharp
// Step 2: Initialise OCR engine for Russian
OcrEngine ocrEngine = new OcrEngine
{
    Language = OcrLanguage.Russian   // Enables Russian language support
};
```

Perché è importante? Senza impostare la lingua, il motore usa l'inglese per impostazione predefinita e interpreterà erroneamente molti caratteri cirillici, producendo output confuso. Configurare esplicitamente la lingua migliora notevolmente l'accuratezza.

## Passo 3 – Carica l'immagine e **converti immagine in testo**

Ora carichiamo l'immagine in memoria. Il metodo `Image.FromFile` funziona con la maggior parte dei formati comuni (JPG, PNG, BMP). Dopo il caricamento, chiamiamo `Recognize` per **convertire immagine in testo**.

```csharp
// Step 3: Load the image that contains Russian text
Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/russian_note.jpg");

// Step 4: Perform OCR – this is the core “how to perform OCR” call
string rawText = ocrEngine.Recognize(sourceImage);
```

La variabile `rawText` ora contiene l'output grezzo dell'OCR, che può ancora contenere errori di battitura o caratteri riconosciuti in modo errato. Puoi stamparla per vedere cosa ha catturato il motore:

```csharp
Console.WriteLine("Raw OCR output:");
Console.WriteLine(rawText);
```

## Passo 4 – **Come controllare l'ortografia** del risultato OCR

L'OCR russo può essere rumoroso, soprattutto con scansioni a bassa risoluzione. Aspose fornisce una classe `SpellChecker` che comprende i dizionari russi di default. Ecco come invocarla:

```csharp
// Step 5: Initialise the spell checker
SpellChecker spellChecker = new SpellChecker();

// Step 6: Correct spelling mistakes in the recognized text
string correctedText = spellChecker.CheckAndCorrect(rawText, OcrLanguage.Russian);
```

Il metodo `CheckAndCorrect` restituisce una nuova stringa in cui le parole errate sono sostituite con le alternative più probabili. Rispetta anche la punteggiatura, così non ti ritrovi con un muro di testo.

*Caso limite:* Se l'output OCR è vuoto (ad esempio, l'immagine è completamente bianca), `CheckAndCorrect` restituirà semplicemente una stringa vuota. È consigliabile gestire questo caso se prevedi di scrivere il risultato su un file.

## Passo 5 – Visualizza il risultato pulito

Infine, stampiamo la stringa corretta. In un'applicazione reale potresti scriverla su un database, un'API JSON o un documento Word. Per questa demo, una stampa sulla console è sufficiente:

```csharp
// Step 7: Show the corrected result
Console.WriteLine("\nCorrected text:");
Console.WriteLine(correctedText);
```

Quando esegui il programma, dovresti vedere qualcosa del genere:

```
Raw OCR output:
Привeт мир! Этo тeкcт c русcкoй оcнoвнoй.

Corrected text:
Привет мир! Это текст с русской основой.
```

Nota come il correttore ortografico ha trasformato “Привeт” (e latino misto) nel corretto cirillico “Привет”. Questa è la magia di **come controllare l'ortografia** dell'output OCR.

## Esempio completo funzionante

Di seguito trovi il programma completo e eseguibile che collega tutti i passaggi. Copialo in un nuovo progetto console e premi **F5**.

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System.Drawing;

class SpellCheckDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine configured for Russian language
        OcrEngine ocrEngine = new OcrEngine { Language = OcrLanguage.Russian };

        // Step 2: Load the image that contains the text to be recognized
        Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/russian_note.jpg");

        // Step 3: Perform OCR to extract raw text from the image
        string rawText = ocrEngine.Recognize(sourceImage);

        // Optional: Show raw OCR output
        System.Console.WriteLine("Raw OCR output:");
        System.Console.WriteLine(rawText);

        // Step 4: Initialise the spell checker
        SpellChecker spellChecker = new SpellChecker();

        // Step 5: Correct spelling mistakes in the recognized text
        string correctedText = spellChecker.CheckAndCorrect(rawText, OcrLanguage.Russian);

        // Step 6: Display the corrected result
        System.Console.WriteLine("\nCorrected text:");
        System.Console.WriteLine(correctedText);
    }
}
```

### Output previsto

Eseguire il programma con una foto chiara e ad alta risoluzione di una scrittura a mano russa di solito produce una frase pulita e leggibile. Se l'immagine è sfocata, potresti comunque ottenere parole parzialmente corrette, ma il correttore ortografico eliminerà la maggior parte degli errori evidenti.

## Problemi comuni e consigli

| Problema | Perché accade | Come risolvere / evitare |
|----------|----------------|--------------------------|
| **Caratteri spazzatura** | Bassa DPI o sfondo rumoroso | Pre‑elabora l'immagine (aumenta il contrasto, ridimensiona a ≥300 dpi) prima di passarla a `Recognize`. |
| **Output vuoto** | Percorso file errato o formato non supportato | Verifica il percorso e usa `Image.FromFile` all'interno di un blocco `try/catch` per mostrare gli errori. |
| **Il correttore ortografico non rileva errori** | Parole rare non presenti nel dizionario | Estendi il dizionario caricando una lista di parole personalizzata tramite `spellChecker.AddUserDictionary("mywords.txt")`. |
| **Ritardo di prestazioni su grandi batch** | L'OCR è intensivo per la CPU | Esegui l'OCR su un thread in background o usa `Parallel.ForEach` per più immagini. |
| **Eccezione di licenza** | Uso della versione di valutazione oltre il periodo di prova | Acquista una licenza e chiama `License license = new License(); license.SetLicense("Aspose.Total.lic");` prima di creare `OcrEngine`. |

## Prossimi passi – Oltre il semplice OCR

Ora che hai padroneggiato **come eseguire OCR**, considera queste estensioni:

* **Elaborazione batch** – Scorri una cartella di immagini e scrivi ogni testo corretto in un file `.txt`.  
* **Conversione PDF** – Usa Aspose PDF per incorporare il testo estratto in un PDF ricercabile.  
* **Rilevamento della lingua** – Se devi gestire più lingue, ispeziona prima il risultato OCR e cambia `OcrLanguage` di conseguenza.  
* **Integrazione con Azure Cognitive Services** – Confronta i risultati di Aspose con l'API OCR di Microsoft per un approccio ibrido.  

All of those topics naturally involve the secondary keywords **extract text from image**, **convert image to text**, and **how to spell check**, so

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}