---
date: 2025-12-25
description: Migliora l'accuratezza OCR con Aspose OCR per .NET, sfruttando il controllo
  ortografico e il supporto linguistico per correggere gli errori di battitura e personalizzare
  i dizionari per un riconoscimento del testo senza errori.
linktitle: Improve OCR Accuracy with Spell Checking in Images
second_title: Aspose.OCR .NET API
title: Migliora la precisione OCR con il controllo ortografico nelle immagini
url: /it/net/ocr-optimization/result-correction-with-spell-checking/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Migliora l'accuratezza OCR con il controllo ortografico nelle immagini

## Introduzione

Quando lavori con il riconoscimento ottico dei caratteri (OCR), l'obiettivo finale è **migliorare l'accuratezza OCR** in modo che il testo estratto corrisponda perfettamente all'immagine originale. Le parole scritte in modo errato sono una fonte comune di errori, specialmente quando l'immagine di origine è rumorosa o contiene caratteri insoliti. Aspose.OCR per .NET offre funzionalità di controllo ortografico integrate che non solo correggono quegli errori ma consentono anche di estendere il motore con dizionari personalizzati. In questo tutorial imparerai come utilizzare il controllo ortografico per potenziare i risultati OCR, vedere l'output prima e dopo, e scoprire come personalizzare il processo di correzione in base alle tue esigenze linguistiche specifiche.

## Risposte rapide
- **Che cosa fa il controllo ortografico per l'OCR?** Rileva automaticamente le parole errate nell'output OCR e le sostituisce con le alternative più probabili.  
- **Quale libreria fornisce questa funzionalità?** Aspose.OCR per .NET include un'API di controllo ortografico pronta all'uso.  
- **È necessaria una connessione internet?** No, il motore di controllo ortografico funziona interamente offline.  
- **Posso aggiungere la mia terminologia?** Sì, puoi fornire un dizionario utente personalizzato per gestire parole specifiche del dominio.  
- **Quali lingue sono supportate?** Vedi la sezione “aspose ocr language support” per i dettagli.

## Cos'è il controllo ortografico nell'OCR?

Il controllo ortografico esamina il testo grezzo restituito dal motore OCR, identifica i token che non corrispondono a parole conosciute nel dizionario della lingua selezionata e suggerisce o applica correzioni. Questo passaggio è essenziale per **migliorare l'accuratezza OCR**, specialmente durante l'elaborazione di documenti scansionati, ricevute o moduli in cui l'OCR può interpretare erroneamente i caratteri.

## Perché utilizzare il supporto linguistico di Aspose OCR?

Aspose.OCR viene fornito con pacchetti linguistici completi e consente di collegare dizionari aggiuntivi. Sfruttare **aspose ocr language support** significa poter gestire documenti multilingue senza scrivere parser personalizzati, e ottenere l'accesso a regole specifiche della lingua che migliorano ulteriormente la qualità del riconoscimento.

## Prerequisiti

Prima di immergerci nella magia del controllo ortografico, assicurati di avere i seguenti prerequisiti:

- Libreria Aspose.OCR per .NET: Scarica e installa la libreria Aspose.OCR dalla [pagina di rilascio](https://releases.aspose.com/ocr/net/).
- Directory dei documenti: Assicurati di avere una directory designata per i tuoi documenti. Sostituisci `"Your Document Directory"` nei frammenti di codice con il percorso reale.

## Importa gli spazi dei nomi

Iniziamo importando gli spazi dei nomi necessari nel tuo progetto .NET:

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## Passo 1: Inizializza Aspose.OCR

Inizializza un'istanza di Aspose.OCR per avviare il processo OCR.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Passo 2: Riconosci l'immagine

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

Applica il controllo ortografico per ottenere il risultato corretto. Il frammento di codice seguente illustra questo passaggio:

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

## Passo 6: Correggi il testo dell'utente

Correggi il testo specifico fornito dall'utente usando la libreria Aspose.OCR:

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

| Problema | Perché accade | Come risolverlo |
|----------|----------------|-----------------|
| Nessun suggerimento restituito | Il pacchetto linguistico non è caricato o il testo è troppo corto. | Assicurati che `RecognitionSettings(Language.Eng)` corrisponda alla lingua dell'immagine di origine e che il risultato OCR contenga un numero sufficiente di caratteri. |
| Dizionario personalizzato non applicato | Percorso o formato file errato. | Verifica che `dictionary.txt` esista nella posizione specificata e utilizzi una parola per riga. |
| Il correttore ortografico rallenta documenti di grandi dimensioni | Elaborare ogni parola singolarmente aggiunge overhead. | Elabora le pagine in batch o aumenta l'allocazione di memoria se esegui su .NET Core. |

## Domande frequenti

### Q1: Posso usare Aspose.OCR per lingue diverse dall'inglese?

A1: Sì, Aspose.OCR supporta più lingue. Regola le impostazioni della lingua di conseguenza.

### Q2: Come integro Aspose.OCR nel mio progetto .NET?

A2: Consulta la [documentazione](https://reference.aspose.com/ocr/net/) per i passaggi dettagliati di integrazione.

### Q3: È disponibile una versione di prova per Aspose.OCR?

A3: Sì, puoi esplorare le funzionalità con la [versione di prova gratuita](https://releases.aspose.com/).

### Q4: Posso caricare un dizionario personalizzato per il controllo ortografico?

A4: Assolutamente! Il tutorial dimostra come migliorare la correzione usando un dizionario fornito dall'utente.

### Q5: Dove posso cercare supporto per Aspose.OCR?

A5: Visita il [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) per supporto della community e indicazioni.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Ultimo aggiornamento:** 2025-12-25  
**Testato con:** Aspose.OCR per .NET latest version  
**Autore:** Aspose