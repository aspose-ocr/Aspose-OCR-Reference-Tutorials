---
date: 2026-04-29
description: Migliora l'accuratezza OCR e impara a riconoscere il testo dalle immagini
  usando Aspose OCR per .NET, sfruttando il controllo ortografico e il supporto linguistico
  per correggere gli errori di battitura e personalizzare i dizionari.
keywords:
- improve ocr accuracy
- recognize text from image
- Aspose OCR spell checking
- custom OCR dictionary
linktitle: Migliora l'accuratezza OCR con il controllo ortografico nelle immagini
second_title: Aspose.OCR .NET API
title: Migliora la precisione OCR con il controllo ortografico nelle immagini
url: /it/net/ocr-optimization/result-correction-with-spell-checking/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Migliora l'accuratezza OCR con il controllo ortografico nelle immagini

Quando lavori con il riconoscimento ottico dei caratteri (OCR), l'obiettivo finale è **migliorare l'accuratezza OCR** in modo che il testo estratto corrisponda perfettamente all'immagine originale. Le parole errate sono una fonte comune di errori, soprattutto quando l'immagine di origine è rumorosa o contiene caratteri insoliti. Aspose.OCR per .NET offre funzionalità di correzione ortografica integrate che non solo correggono quegli errori, ma consentono anche di estendere il motore con dizionari personalizzati. In questo tutorial imparerai a utilizzare il controllo ortografico per potenziare i risultati OCR, vedrai l'output prima e dopo la correzione e scoprirai come personalizzare il processo di correzione in base alle tue esigenze linguistiche specifiche.

## Risposte rapide
- **Cosa fa il controllo ortografico per l'OCR?** Rileva automaticamente le parole errate nell'output OCR e le sostituisce con le alternative più probabili.  
- **Quale libreria fornisce questa funzionalità?** Aspose.OCR per .NET include un'API di controllo ortografico pronta all'uso.  
- **È necessaria una connessione internet?** No, il motore di correzione ortografica funziona interamente offline.  
- **Posso aggiungere la mia terminologia?** Sì, puoi fornire un dizionario utente personalizzato per gestire parole specifiche del dominio.  
- **Come aiuta questo a riconoscere il testo dall'immagine?** Correggendo gli errori generati dall'OCR, il testo finale diventa pulito e pronto per l'elaborazione successiva.

## Cos'è il controllo ortografico nell'OCR?
Il controllo ortografico esamina il testo grezzo restituito dal motore OCR, identifica i token che non corrispondono a parole note nel dizionario della lingua selezionata e suggerisce o applica correzioni. Questo passaggio è essenziale per **migliorare l'accuratezza OCR**, soprattutto quando si elaborano documenti scansionati, ricevute o moduli in cui l'OCR può interpretare erroneamente i caratteri.

## Perché usare il supporto linguistico di Aspose OCR?
Aspose.OCR è fornito con pacchetti linguistici completi e consente di collegare dizionari aggiuntivi. Sfruttare **il supporto linguistico di Aspose OCR** significa poter gestire documenti multilingue senza scrivere parser personalizzati e ottenere regole specifiche per lingua che migliorano ulteriormente la qualità del riconoscimento.

## Quando è più importante migliorare l'accuratezza OCR?
- **Documenti legali e di conformità** in cui un singolo errore può cambiare il significato.  
- **Pipeline di estrazione dati** che alimentano i risultati OCR in analisi o modelli di IA.  
- **Applicazioni rivolte al cliente** come scanner mobili che devono restituire testo leggibile istantaneamente.  

## Prerequisiti

Prima di immergerti nella magia del controllo ortografico, assicurati di avere i seguenti prerequisiti:

- Libreria Aspose.OCR per .NET: scarica e installa la libreria Aspose.OCR dalla [pagina di rilascio](https://releases.aspose.com/ocr/net/).
- Directory dei documenti: assicurati di avere una directory designata per i tuoi documenti. Sostituisci `"Your Document Directory"` nei frammenti di codice con il percorso reale.

## Importare gli spazi dei nomi

Iniziamo importando gli spazi dei nomi necessari nel tuo progetto .NET:

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## Passo 1: Inizializzare Aspose.OCR

Inizializza un'istanza di Aspose.OCR per avviare il processo OCR.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Passo 2: Riconoscere l'immagine

Successivamente, riconosci il testo in un'immagine usando Aspose.OCR. Ecco un frammento che dimostra questo processo:

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## Passo 3: Prima della correzione

Recupera il risultato OCR prima della correzione per confrontarlo con la versione corretta.

```csharp
// Get result
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## Passo 4: Dopo la correzione

Applica il controllo ortografico per ottenere il risultato corretto. Il seguente frammento di codice illustra questo passaggio:

```csharp
// Get corrected result
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## Passo 5: Parole errate e suggerimenti

Ottieni un elenco di parole errate insieme ai suggerimenti di correzione usando il codice seguente:

```csharp
// Get list of misspelled words with suggestions
List<SpellCheckError> errorsList = result.GetSpellCheckErrorList(SpellCheckLanguage.Eng);
foreach (var word in errorsList)
{
    Console.Write("Word:" + word.Word);
    Console.Write(" StartPosition:" + word.StartPosition);
    Console.WriteLine(" Length:" + word.Length);
    Console.WriteLine("SuggestedWords:");
    foreach (var suggest in word.SuggestedWords)
    {
        Console.Write(suggest.Word + " ");
    }
    Console.WriteLine();
}
```

## Passo 6: Correggere il testo dell'utente

Correggi il testo fornito dall'utente usando la libreria Aspose.OCR:

```csharp
// Correct user text
Console.WriteLine("recogniition -> " + api.CorrectSpelling("recogniition"));
```

## Passo 7: Correzione con dizionario utente

Migliora ulteriormente la correzione incorporando un dizionario utente personalizzato:

```csharp
// Get corrected result with user dictionary
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## Problemi comuni e soluzioni

| Problema | Perché accade | Come risolvere |
|----------|----------------|----------------|
| Nessun suggerimento restituito | Il pacchetto linguistico non è caricato o il testo è troppo corto. | Assicurati che `RecognitionSettings(Language.Eng)` corrisponda alla lingua dell'immagine di origine e che il risultato OCR contenga un numero sufficiente di caratteri. |
| Dizionario personalizzato non applicato | Percorso o formato file errato. | Verifica che `dictionary.txt` esista nella posizione specificata e utilizzi una parola per riga. |
| Il correttore ortografico rallenta su documenti grandi | L'elaborazione di ogni parola singolarmente aggiunge overhead. | Elabora le pagine in batch o aumenta l'allocazione di memoria se esegui su .NET Core. |

## Domande frequenti

**D1: Posso usare Aspose.OCR per lingue diverse dall'inglese?**  
R1: Sì, Aspose.OCR supporta più lingue. Regola le impostazioni della lingua di conseguenza.

**D2: Come integro Aspose.OCR nel mio progetto .NET?**  
R2: Consulta la [documentazione](https://reference.aspose.com/ocr/net/) per i passaggi dettagliati di integrazione.

**D3: È disponibile una versione di prova per Aspose.OCR?**  
R3: Sì, puoi esplorare le funzionalità con la [versione di prova gratuita](https://releases.aspose.com/).

**D4: Posso caricare un dizionario personalizzato per il controllo ortografico?**  
R4: Assolutamente! Il tutorial dimostra come migliorare la correzione usando un dizionario fornito dall'utente.

**D5: Dove posso trovare supporto per Aspose.OCR?**  
R5: Visita il [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) per supporto della community e indicazioni.

---

**Ultimo aggiornamento:** 2026-04-29  
**Testato con:** Aspose.OCR per .NET ultima versione  
**Autore:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}