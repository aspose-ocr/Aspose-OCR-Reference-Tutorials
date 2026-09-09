---
description: Scopri come specificare i caratteri consentiti per l'OCR con Aspose.OCR
  per .NET e riconoscere le immagini di cifre in modo efficiente. Segui una guida
  passo‑passo per limitare l'OCR solo alle cifre.
linktitle: Specify Allowed Characters OCR – Using Aspose.OCR for .NET
second_title: Aspose.OCR .NET API
title: Specifica i caratteri consentiti per OCR – Utilizzo di Aspose.OCR per .NET
url: /it/net/ocr-settings/specify-allowed-characters/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Specifica i caratteri consentiti OCR – Utilizzo di Aspose.OCR per .NET

In questo tutorial imparerai come **specify allowed characters ocr** con Aspose.OCR per .NET, consentendoti di limitare l'output OCR solo ai caratteri di cui hai bisogno. Questo è particolarmente utile quando devi **recognize digits image** file come numeri di serie, ID fatture o stringhe simili a codici a barre. Ti guideremo attraverso la configurazione, il codice e un paio di scenari pratici in modo che tu possa applicare subito la tecnica.

## Risposte rapide
- **Cosa fa “specify allowed characters ocr”?** Limita l'OCR a un insieme predefinito di caratteri, migliorando l'accuratezza per i dati mirati.  
- **Quali caratteri posso consentire?** Qualsiasi combinazione di cui hai bisogno—cifre, lettere o simboli personalizzati (ad esempio “0123456789”).  
- **Perché limitare i caratteri?** Riduce i riconoscimenti falsi e velocizza l'elaborazione quando il set di caratteri previsto è noto.  
- **Ho bisogno di una licenza?** Una prova gratuita è sufficiente per lo sviluppo; è necessaria una licenza commerciale per la produzione.  
- **Quali versioni .NET sono supportate?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Cos'è “specify allowed characters ocr”?
Quando l'OCR analizza un'immagine, tenta di far corrispondere ogni modello visivo all'intero alfabeto di possibili caratteri. Con **specify allowed characters ocr**, indichi al motore di ignorare tutto ciò che non è nella tua whitelist, migliorando notevolmente l'accuratezza del riconoscimento per set di dati limitati.

## Perché usare Aspose.OCR per riconoscere digits image?
Aspose.OCR offre un'API pulita e fluida per gli sviluppatori .NET. La sua opzione integrata `AllowedCharacters` ti consente di concentrarti su scenari solo numerici senza scrivere logica di post‑processing personalizzata. È perfetto per:
- Lettura di contatori, numeri di fattura o codici prodotto.  
- Convalida dei dati inseriti dall'utente catturati da moduli scansionati.  
- Accelerare l'elaborazione batch quando il set di caratteri è noto in anticipo.

## Prerequisiti

Prima di immergerti nel codice, assicurati di avere:

- Una buona conoscenza dello sviluppo .NET.  
- Libreria **Aspose.OCR for .NET**. Puoi scaricarla [qui](https://releases.aspose.com/ocr/net/).  
- Visual Studio (o qualsiasi IDE .NET preferito).  

## Importa gli spazi dei nomi

Nel tuo progetto .NET, importa gli spazi dei nomi necessari per sfruttare le funzionalità di Aspose.OCR:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

Ora, suddividiamo il tutorial in una serie di passaggi completi:

## Come specificare i caratteri consentiti OCR – Guida passo‑passo

### Passo 1: Imposta il percorso della cartella delle immagini

Per prima cosa, definisci dove sono archiviate le tue immagini di esempio.

```csharp
string dataDir = "Your Document Directory";
```

### Passo 2: Inizializza Aspose.OCR con una whitelist solo cifre

Crea un'istanza `AsposeOcr` e passa i caratteri che desideri consentire—in questo caso, tutte le cifre.

```csharp
AsposeOcr api = new AsposeOcr("0123456789");
```

### Passo 3: Riconosci una singola riga contenente cifre

Usa il metodo `RecognizeLine` per estrarre il testo da un'immagine che contiene solo numeri.

```csharp
string result = api.RecognizeLine(dataDir + "0001460985.Jpeg");
```

### Passo 4: Visualizza le cifre riconosciute

Stampa il risultato sulla console così puoi verificare l'output.

```csharp
Console.WriteLine(result);
```

### Passo 5: Usa RecognitionSettings per maggiore controllo

Se hai bisogno di un controllo più fine—ad esempio forzare il riconoscimento a singola riga—puoi usare la sovraccarico che accetta `RecognitionSettings`.

```csharp
AsposeOcr api2 = new AsposeOcr();
RecognitionResult result2 = api2.RecognizeImage(dataDir + "0001460985.Jpeg", 
    new RecognitionSettings { 
        AllowedCharacters = CharactersAllowedType.DIGITS,
        RecognizeSingleLine = true
    });
```

### Passo 6: Visualizza il risultato del secondo caso

```csharp
Console.WriteLine(result2.RecognitionText);
```

### Passo 7: Conferma l'esecuzione riuscita

```csharp
Console.WriteLine("SpecifyAllowedCharacters executed successfully");
```

Seguendo questi passaggi, hai imparato come **specify allowed characters ocr** e riconoscere in modo efficiente contenuti **recognize digits image** usando Aspose.OCR per .NET.

## Problemi comuni e risoluzione

- **Risultato vuoto:** Assicurati che la qualità dell'immagine sia sufficiente (contrasto chiaro, rumore minimo).  
- **Caratteri errati restituiti:** Verifica che la stringa della whitelist corrisponda esattamente ai caratteri attesi.  
- **File non trovato:** Verifica che `dataDir` punti alla cartella corretta e che il nome del file corrisponda esattamente al caso.

## Domande frequenti

### Q1: Aspose.OCR per .NET è adatto sia ai principianti che agli sviluppatori esperti?
**A:** Assolutamente! L'API è progettata per essere intuitiva per i nuovi arrivati, offrendo al contempo opzioni avanzate per gli utenti esperti.

### Q2: Posso usare Aspose.OCR per .NET per riconoscere caratteri in più lingue?
**A:** Sì, Aspose.OCR supporta un'ampia gamma di lingue. Puoi combinare i language pack con la funzionalità allowed‑characters per scenari multilingue.

### Q3: Con quale frequenza viene aggiornato Aspose.OCR per .NET?
**A:** Gli aggiornamenti vengono rilasciati regolarmente per aggiungere nuove funzionalità, migliorare l'accuratezza e garantire la compatibilità. Consulta la [documentazione](https://reference.aspose.com/ocr/net/) per i dettagli dell'ultima versione.

### Q4: È disponibile una prova gratuita per Aspose.OCR per .NET?
**A:** Sì, puoi esplorare le funzionalità scaricando la [prova gratuita](https://releases.aspose.com/).

### Q5: Dove posso cercare assistenza o entrare in contatto con la community per supporto?
**A:** Visita il [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) per fare domande, condividere esperienze e ottenere aiuto sia dagli ingegneri Aspose sia da altri sviluppatori.

---

**Ultimo aggiornamento:** 2026-02-15  
**Testato con:** Aspose.OCR 24.11 per .NET  
**Autore:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}