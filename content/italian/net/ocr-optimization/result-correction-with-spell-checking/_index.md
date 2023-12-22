---
title: Correzione dei risultati con controllo ortografico nel riconoscimento delle immagini OCR
linktitle: Correzione dei risultati con controllo ortografico nel riconoscimento delle immagini OCR
second_title: API Aspose.OCR .NET
description: Migliora la precisione dell'OCR con Aspose.OCR per .NET. Correggi l'ortografia, personalizza i dizionari e ottieni facilmente un riconoscimento del testo senza errori.
type: docs
weight: 13
url: /it/net/ocr-optimization/result-correction-with-spell-checking/
---
## introduzione

Nel campo del riconoscimento ottico dei caratteri (OCR), ottenere risultati accurati è fondamentale per estrarre informazioni significative dalle immagini. Una sfida comune riguarda la gestione delle parole errate nel processo di riconoscimento. Fortunatamente, Aspose.OCR per .NET fornisce una potente soluzione per migliorare i risultati dell'OCR attraverso il controllo ortografico.

Questo tutorial ti guiderà attraverso il processo di correzione dei risultati con il controllo ortografico utilizzando Aspose.OCR per .NET. Alla fine, sarai in grado di migliorare la precisione del testo derivato dall'OCR, garantendo un output più rifinito e privo di errori.

## Prerequisiti

Prima di immergerci nella magia del controllo ortografico, assicurati di avere i seguenti prerequisiti:

-  Libreria Aspose.OCR per .NET: scarica e installa la libreria Aspose.OCR da[pagina di rilascio](https://releases.aspose.com/ocr/net/).

- Directory dei documenti: assicurati di avere una directory designata per i tuoi documenti. Sostituisci "La tua directory dei documenti" negli snippet di codice con il percorso effettivo.

## Importa spazi dei nomi

Iniziamo importando gli spazi dei nomi necessari nel tuo progetto .NET:

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## Passaggio 1: inizializzare Aspose.OCR

Inizializza un'istanza di Aspose.OCR per avviare il processo OCR.

```csharp
// Il percorso della directory dei documenti.
string dataDir = "Your Document Directory";

// Inizializza un'istanza di AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Passaggio 2: riconoscere l'immagine

Successivamente, riconosci il testo in un'immagine utilizzando Aspose.OCR. Ecco uno snippet che mostra questo processo:

```csharp
// Riconoscere l'immagine
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## Passaggio 3: prima della correzione

Recupera il risultato OCR prima della correzione per confrontarlo con la versione corretta.

```csharp
// Ottieni risultato
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## Passaggio 4: dopo la correzione

Applicare il controllo ortografico per ottenere il risultato corretto. Il seguente frammento di codice illustra questo passaggio:

```csharp
// Ottieni il risultato corretto
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## Passaggio 5: parole e suggerimenti con errori di ortografia

Ottieni un elenco di parole con errori di ortografia insieme alle correzioni suggerite utilizzando il seguente codice:

```csharp
// Ottieni l'elenco delle parole con errori di ortografia con suggerimenti
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

## Passaggio 6: correggere il testo utente

Correggere il testo specifico fornito dall'utente utilizzando la libreria Aspose.OCR:

```csharp
// Testo utente corretto
Console.WriteLine("recogniition -> " + api.CorrectSpelling("recogniition"));
```

## Passaggio 7: correzione con dizionario utente

Migliora ulteriormente la correzione incorporando un dizionario utente personalizzato:

```csharp
// Ottieni il risultato corretto con il dizionario utente
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## Conclusione

Congratulazioni! Hai esplorato con successo le funzionalità di controllo ortografico di Aspose.OCR per .NET. Questa funzionalità consente di perfezionare i risultati dell'OCR, garantendo la precisione ed eliminando gli errori.

## Domande frequenti

### Q1: Posso utilizzare Aspose.OCR per lingue diverse dall'inglese?

A1: Sì, Aspose.OCR supporta più lingue. Regolare di conseguenza le impostazioni della lingua.

### Q2: Come integro Aspose.OCR nel mio progetto .NET?

 A2: Fare riferimento a[documentazione](https://reference.aspose.com/ocr/net/) per le fasi dettagliate di integrazione.

### Q3: È disponibile una versione di prova per Aspose.OCR?

 R3: Sì, puoi esplorare le funzionalità con[versione di prova gratuita](https://releases.aspose.com/).

### Q4: Posso caricare un dizionario personalizzato per il controllo ortografico?

A4: Assolutamente! Il tutorial dimostra come migliorare la correzione utilizzando un dizionario fornito dall'utente.

### Q5: Dove posso chiedere supporto per Aspose.OCR?

 A5: Visita il[Forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) per il supporto e l’orientamento della comunità.