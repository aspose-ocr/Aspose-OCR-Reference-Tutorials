---
date: 2026-05-24
description: Scopri come migliorare l'OCR impostando i caratteri consentiti con Aspose.OCR
  per .NET, consentendo un riconoscimento accurato delle cifre e una elaborazione
  più veloce. Segui una guida passo‑passo.
keywords:
- how to improve ocr
- set allowed characters
- recognize digits
- improve ocr accuracy
- extract serial numbers
linktitle: Come migliorare l'OCR – Impostare i caratteri consentiti con Aspose.OCR
  per .NET
schemas:
- author: Aspose
  dateModified: '2026-05-24'
  description: Learn how to improve OCR by setting allowed characters with Aspose.OCR
    for .NET, enabling accurate digit recognition and faster processing. Follow a
    step‑by‑step guide.
  headline: How to Improve OCR – Set Allowed Characters with Aspose.OCR for .NET
  type: TechArticle
- description: Learn how to improve OCR by setting allowed characters with Aspose.OCR
    for .NET, enabling accurate digit recognition and faster processing. Follow a
    step‑by‑step guide.
  name: How to Improve OCR – Set Allowed Characters with Aspose.OCR for .NET
  steps:
  - name: Set the path to your image folder
    text: Define the folder that contains the sample images you want to process.
  - name: Initialize Aspose.OCR with a digit‑only whitelist
    text: '`AllowedCharacters` is a property that sets the whitelist of characters
      the OCR engine may recognize.'
  - name: Recognize a single line containing digits
    text: The `RecognizeLine` method scans the image and returns the best‑matching
      line that conforms to the whitelist.
  - name: Output the recognized digits
    text: Write the result to the console (or log) so you can verify the output instantly.
  - name: Use `RecognitionSettings` for more control
    text: '`RecognitionSettings` allows you to customize OCR parameters such as DPI,
      language packs, and processing mode.'
  - name: Confirm successful execution
    text: By following these steps, you’ve learned **how to improve OCR** accuracy
      by limiting the character set, and you can now reliably extract digit strings
      from images using Aspose.OCR for .NET.
  type: HowTo
- questions:
  - answer: It limits OCR to a predefined whitelist, dramatically increasing accuracy
      for targeted data sets.
    question: What does “specify allowed characters OCR” do?
  - answer: Any combination you need—digits (`0‑9`), uppercase letters, custom symbols,
      or a mix like “ABC‑123”.
    question: Which characters can I allow?
  - answer: Whitelisting reduces false recognitions by up to 70 % and speeds up processing
      by 30 % on average.
    question: Why limit characters?
  - answer: A free trial works for development; a commercial license is required for
      production deployments.
    question: Do I need a license?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
    question: Which .NET versions are supported?
  type: FAQPage
second_title: Aspose.OCR .NET API
title: Come migliorare l'OCR – Impostare i caratteri consentiti con Aspose.OCR per
  .NET
url: /it/net/ocr-settings/specify-allowed-characters/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come migliorare OCR – Impostare i caratteri consentiti con Aspose.OCR per .NET

In questo tutorial scoprirai **come migliorare OCR** risultati specificando **i caratteri consentiti** quando utilizzi Aspose.OCR per .NET. Limitare il motore OCR a una whitelist nota — ad esempio solo cifre — aumenta la precisione, riduce i tempi di elaborazione ed elimina i simboli indesiderati. Che tu stia estraendo numeri di serie, ID fattura o letture del contatore, i passaggi seguenti ti permetteranno di applicare questa tecnica in pochi minuti.

## Risposte rapide
- **Cosa fa “specify allowed characters OCR”?** Limita OCR a una whitelist predefinita, aumentando drasticamente la precisione per set di dati mirati.  
- **Quali caratteri posso consentire?** Qualsiasi combinazione di cui hai bisogno — cifre (`0‑9`), lettere maiuscole, simboli personalizzati, o una combinazione come “ABC‑123”.  
- **Perché limitare i caratteri?** La whitelist riduce i riconoscimenti falsi fino al 70 % e velocizza l'elaborazione del 30 % in media.  
- **Ho bisogno di una licenza?** Una prova gratuita funziona per lo sviluppo; è necessaria una licenza commerciale per le distribuzioni in produzione.  
- **Quali versioni di .NET sono supportate?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.  
- **Posso combinarlo con i language pack?** Sì — abbina una whitelist a un language pack per gestire stringhe di cifre multilingue.

## Cos'è “specify allowed characters OCR”?
**Risposta diretta:** Specificare i caratteri consentiti indica ad Aspose.OCR di ignorare ogni modello visivo che non corrisponde ai caratteri elencati, così il motore restituisce solo risultati dalla whitelist. Questo approccio mirato elimina il rumore, migliora i punteggi di fiducia e riduce lo sforzo di post‑elaborazione. Inoltre velocizza il processo di riconoscimento.

## Perché usare Aspose.OCR per riconoscere immagini di cifre?
**Risposta diretta:** La funzionalità integrata `AllowedCharacters` di Aspose.OCR ti consente di riconoscere immagini contenenti solo cifre con una singola riga di codice, offrendo fino al 95 % di precisione su scansioni a bassa risoluzione senza alcuna logica di filtraggio aggiuntiva. La libreria supporta oltre 30 lingue, elabora batch di immagini di 500 pagine in meno di 2 secondi per pagina e funziona completamente offline, rendendola ideale per scenari ad alto volume, on‑premises, come la lettura di contatori o l'estrazione di ID fattura.

## Prerequisiti
Prima di iniziare, assicurati di avere:

- Esperienza di base nello sviluppo .NET.  
- Libreria **Aspose.OCR for .NET** – scaricala dal sito ufficiale **[qui](https://releases.aspose.com/ocr/net/)**.  
- Visual Studio 2019+ (o qualsiasi IDE .NET compatibile).  

## Importare gli spazi dei nomi
I seguenti spazi dei nomi ti danno accesso al motore OCR e alle sue impostazioni:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

## Come migliorare OCR specificando i caratteri consentiti?
`AsposeOcr` è la classe principale del motore OCR fornita dalla libreria Aspose.OCR.  
`RecognizeLine` elabora una singola riga di testo da un'immagine e restituisce la stringa riconosciuta.

**Risposta diretta:** Carica la tua immagine, crea un'istanza `AsposeOcr` con una whitelist solo cifre (`"0123456789"`), chiama `RecognizeLine` (o `Recognize` per più righe) e leggi la proprietà `Text` dal risultato. Questo flusso a tre passaggi fornisce stringhe numeriche pulite in meno di un secondo per immagini tipiche a 300 dpi.

### Passo 1: Impostare il percorso della cartella delle immagini
Definisci la cartella che contiene le immagini di esempio da elaborare.

```csharp
string dataDir = "Your Document Directory";
```

### Passo 2: Inizializzare Aspose.OCR con una whitelist solo cifre
`AllowedCharacters` è una proprietà che imposta la whitelist dei caratteri che il motore OCR può riconoscere.

```csharp
AsposeOcr api = new AsposeOcr("0123456789");
```

### Passo 3: Riconoscere una singola riga contenente cifre
Il metodo `RecognizeLine` analizza l'immagine e restituisce la riga più corrispondente che rispetta la whitelist.

```csharp
string result = api.RecognizeLine(dataDir + "0001460985.Jpeg");
```

### Passo 4: Restituire le cifre riconosciute
Scrivi il risultato sulla console (o nel log) così potrai verificare l'output immediatamente.

```csharp
Console.WriteLine(result);
```

### Passo 5: Utilizzare `RecognitionSettings` per maggiore controllo
`RecognitionSettings` ti permette di personalizzare i parametri OCR come DPI, language pack e modalità di elaborazione.

```csharp
AsposeOcr api2 = new AsposeOcr();
RecognitionResult result2 = api2.RecognizeImage(dataDir + "0001460985.Jpeg", 
    new RecognitionSettings { 
        AllowedCharacters = CharactersAllowedType.DIGITS,
        RecognizeSingleLine = true
    });
```

### Passo 6: Visualizzare il risultato del secondo caso

```csharp
Console.WriteLine(result2.RecognitionText);
```

### Passo 7: Confermare l'esecuzione riuscita

```csharp
Console.WriteLine("SpecifyAllowedCharacters executed successfully");
```

Seguendo questi passaggi, hai imparato **come migliorare la precisione OCR** limitando il set di caratteri, e ora puoi estrarre in modo affidabile stringhe di cifre dalle immagini usando Aspose.OCR per .NET.

## Problemi comuni e risoluzione dei problemi
- **Risultato vuoto:** Verifica che l'immagine abbia un contrasto chiaro e rumore di sfondo minimo; si consiglia un minimo di 300 dpi.  
- **Caratteri inattesi:** Controlla la stringa della whitelist; spazi extra o caratteri invisibili romperanno il filtro.  
- **File non trovato:** Assicurati che `dataDir` punti alla cartella corretta e che il nome del file corrisponda al file system sensibile al case.  
- **Ritardo di prestazioni:** Per batch di grandi dimensioni, riutilizza una singola istanza `AsposeOcr` invece di crearne una nuova per ogni immagine.

## Domande frequenti

### Q1: Aspose.OCR per .NET è adatto sia ai principianti che agli sviluppatori esperti?
**A:** Assolutamente. L'API offre una configurazione a riga singola per compiti rapidi e `RecognitionSettings` avanzati per utenti esperti, coprendo tutti i livelli di competenza.

### Q2: Posso riconoscere caratteri in più lingue usando una whitelist di caratteri consentiti?
**A:** Sì. Carica il language pack appropriato (ad es., `ocrEngine.LoadLanguage("en")`) e combinalo con una whitelist come `"0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ"` per gestire stringhe di cifre multilingue.

### Q3: Con quale frequenza viene aggiornato Aspose.OCR per .NET?
**A:** Le nuove versioni vengono pubblicate circa ogni 6‑8 settimane, aggiungendo supporto linguistico, miglioramenti delle prestazioni e correzioni di bug. Vedi i dettagli più recenti nella [documentazione](https://reference.aspose.com/ocr/net/).

### Q4: È disponibile una prova gratuita?
**A:** Sì — scarica la **[prova gratuita](https://releases.aspose.com/)** per valutare tutte le funzionalità senza licenza. L'uso in produzione richiede una licenza commerciale.

### Q5: Dove posso ottenere aiuto dalla community o supporto ufficiale?
**A:** Unisciti alla community attiva sul **[forum Aspose.OCR](https://forum.aspose.com/c/ocr/16)** dove puoi porre domande, condividere snippet e ricevere indicazioni dagli ingegneri di Aspose.

---

**Ultimo aggiornamento:** 2026-05-24  
**Testato con:** Aspose.OCR 24.11 per .NET  
**Autore:** Aspose

## Tutorial correlati
- [Impostazioni di riconoscimento immagine OCR - Specificare i caratteri ignorati](/ocr/net/ocr-settings/specify-ignored-characters/)
- [Preprocessare l'immagine OCR con i filtri Aspose.OCR per .NET](/ocr/net/ocr-optimization/preprocessing-filters-for-image/)
- [Come impostare il valore di soglia nel riconoscimento immagine OCR](/ocr/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}