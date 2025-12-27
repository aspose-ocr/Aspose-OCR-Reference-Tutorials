---
date: 2025-12-27
description: Scopri come utilizzare la conversione OCR da immagine a testo con Aspose.OCR
  per .NET, specificando i caratteri consentiti e affinando le impostazioni di riconoscimento
  OCR. Include il codice per il riconoscimento di immagini di cifre.
linktitle: 'ocr image to text: Specify Allowed Characters in OCR'
second_title: Aspose.OCR .NET API
title: 'OCR immagine in testo: specifica i caratteri consentiti nell''OCR'
url: /it/net/ocr-settings/specify-allowed-characters/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ocr image to text: Specificare i caratteri consentiti in OCR

## Introduzione

Nel panorama in continua evoluzione della tecnologia, il riconoscimento ottico dei caratteri (OCR) – o la conversione **ocr image to text** – è emerso come uno strumento trasformativo, consentendo alle macchine di comprendere il testo dalle immagini. Aspose.OCR per .NET si distingue come una soluzione potente, offrendo un'integrazione senza soluzione di continuità per gli sviluppatori che cercano capacità OCR robuste nelle loro applicazioni .NET.

## Risposte rapide
- **Che cosa fa “Specify Allowed Characters”?** Limita l'output OCR a un insieme definito di simboli, ad esempio solo cifre.  
- **Quale metodo estrae una singola riga di testo?** `RecognizeLine` restituisce la prima riga rilevata.  
- **Posso modificare le impostazioni di riconoscimento OCR al volo?** Sì – usa `RecognitionSettings` per regolare opzioni come `AllowedCharacters`.  
- **È disponibile una versione di prova?** Assolutamente, scarica la versione di prova gratuita dal sito Aspose.  
- **Quali versioni di .NET sono supportate?** Tutte le versioni moderne di .NET Framework e .NET Core/5/6.

## Prerequisiti

Prima di immergerti nel tutorial, assicurati di avere i seguenti prerequisiti:

- Una buona conoscenza dello sviluppo .NET.  
- Libreria Aspose.OCR per .NET. Puoi scaricarla [qui](https://releases.aspose.com/ocr/net/).  
- Familiarità con Visual Studio o qualsiasi altro ambiente di sviluppo .NET preferito.

## Importare gli spazi dei nomi

Nel tuo progetto .NET, importa gli spazi dei nomi necessari per sfruttare efficacemente le funzionalità di Aspose.OCR per .NET:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

Ora, suddividiamo il tutorial in una serie di passaggi completi:

## Passo 1: Specificare i caratteri consentiti in ocr image to text

Per iniziare, imposta il percorso della tua directory dei documenti:

```csharp
string dataDir = "Your Document Directory";
```

## Passo 2: Inizializzare Aspose.OCR con i simboli consentiti (riconoscere immagine di cifre)

Crea un'istanza di `AsposeOcr`, specificando i simboli consentiti. In questo caso, consentiamo solo le cifre (0‑9):

```csharp
AsposeOcr api = new AsposeOcr("0123456789");
```

## Passo 3: Riconoscere l'immagine

Utilizza l'istanza `AsposeOcr` per riconoscere il testo da un'immagine:

```csharp
string result = api.RecognizeLine(dataDir + "0001460985.Jpeg");
```

## Passo 4: Visualizzare il testo riconosciuto

Stampa il testo riconosciuto sulla console:

```csharp
Console.WriteLine(result);
```

## Passo 5: Secondo caso – Riconoscere l'immagine con impostazioni specifiche di riconoscimento OCR

Inizializza un'altra istanza di `AsposeOcr`, questa volta con impostazioni più specifiche che dimostrano l'uso delle **ocr recognition settings**:

```csharp
AsposeOcr api2 = new AsposeOcr();
RecognitionResult result2 = api2.RecognizeImage(dataDir + "0001460985.Jpeg", 
    new RecognitionSettings { 
        AllowedCharacters = CharactersAllowedType.DIGITS,
        RecognizeSingleLine = true
    });
```

## Passo 6: Visualizzare il testo riconosciuto del secondo caso

Stampa il testo riconosciuto del secondo caso sulla console:

```csharp
Console.WriteLine(result2.RecognitionText);
```

## Passo 7: Esecuzione riuscita

Infine, conferma l'esecuzione riuscita del tutorial **SpecifyAllowedCharacters**:

```csharp
Console.WriteLine("SpecifyAllowedCharacters executed successfully");
```

Seguendo questi passaggi, hai sbloccato la capacità di **specificare i caratteri consentiti** nel riconoscimento di immagini OCR usando Aspose.OCR per .NET, consentendo una conversione precisa **ocr image to text** per scenari con sole cifre.

## Perché utilizzare il filtraggio dei caratteri consentiti?

- **Maggiore precisione:** Limitare il set di caratteri riduce i falsi riconoscimenti, soprattutto nelle immagini rumorose.  
- **Aumento delle prestazioni:** Il motore OCR salta i glifi irrilevanti, accelerando l'elaborazione.  
- **Conformità:** Impone formati di dati (ad esempio numeri di fattura, codici seriali) direttamente nella fase OCR.

## Problemi comuni e consigli

- **Problema:** Fornire una stringa vuota per i caratteri consentiti disabilita il filtraggio.  
  **Consiglio:** Passa sempre una stringa non vuota o utilizza l'enum `CharactersAllowedType`.  
- **Problema:** Usare `RecognizeLine` su documenti multilinea può far perdere dati.  
  **Consiglio:** Passa a `RecognizeImage` con `RecognizeSingleLine = false` per l'estrazione dell'intera pagina.  
- **Problema:** Dimenticare di combinare correttamente il percorso della directory può causare `FileNotFoundException`.  
  **Consiglio:** Usa `Path.Combine(dataDir, "file.jpg")` per percorsi indipendenti dalla piattaforma.

## Domande frequenti

**Q: Aspose.OCR per .NET è adatto sia ai principianti che agli sviluppatori esperti?**  
A: Assolutamente! L'API è intuitiva per i nuovi arrivati e offre impostazioni avanzate per gli utenti esperti.

**Q: Posso usare Aspose.OCR per .NET per riconoscere caratteri in più lingue?**  
A: Sì, Aspose.OCR supporta un'ampia gamma di lingue; è possibile combinare i language pack per progetti multilingue.

**Q: Con quale frequenza viene aggiornato Aspose.OCR per .NET?**  
A: Gli aggiornamenti vengono rilasciati regolarmente per tenere il passo con le nuove versioni .NET e i miglioramenti OCR. Consulta la [documentazione](https://reference.aspose.com/ocr/net/) per la versione più recente.

**Q: È disponibile una versione di prova gratuita per Aspose.OCR per .NET?**  
A: Sì, puoi esplorare le funzionalità scaricando la [versione di prova gratuita](https://releases.aspose.com/).

**Q: Dove posso cercare assistenza o entrare in contatto con la community per supporto?**  
A: Visita il [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) per interagire con esperti e altri sviluppatori.

---

**Ultimo aggiornamento:** 2025-12-27  
**Testato con:** Aspose.OCR 24.11 per .NET  
**Autore:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}