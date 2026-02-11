---
date: 2025-12-19
description: Impara a eseguire l'OCR su immagini di archivio, convertire le immagini
  in testo ed estrarre il testo dai file di archivio usando Aspose.OCR per .NET.
linktitle: How to Perform OCR on Archive Images with Aspose.OCR for .NET
second_title: Aspose.OCR .NET API
title: Come eseguire l'OCR su immagini di archivio con Aspose.OCR per .NET
url: /it/net/ocr-configuration/ocr-operation-with-archive/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR su immagini archiviate con Aspose.OCR per .NET

## Introduzione

In questo tutorial completo scoprirai **come eseguire OCR** su file immagine archiviati utilizzando la libreria Aspose.OCR per .NET. Che tu debba **convertire immagini in testo** o **estrarre testo da archivi**, la guida passo‑paso qui sotto ti accompagnerà in ogni fase—dalla configurazione dell'ambiente di sviluppo al recupero del testo riconosciuto da ciascuna immagine all'interno di un archivio ZIP.

## Risposte rapide
- **Che cosa copre il tutorial?** Esecuzione di OCR su immagini archiviate (ZIP) con Aspose.OCR per .NET.  
- **Qual è la parola chiave principale?** *how to perform ocr*.  
- **È necessaria una licenza?** Una versione di prova gratuita è sufficiente per la valutazione; è necessaria una licenza commerciale per la produzione.  
- **Quali versioni di .NET sono supportate?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Posso personalizzare le impostazioni di riconoscimento?** Sì—usa `RecognitionSettings` per ottimizzare la precisione.

## Cos'è l'OCR e perché usarlo sugli archivi?

Il riconoscimento ottico dei caratteri (OCR) trasforma immagini o PDF scansionati in testo ricercabile e modificabile. Quando le immagini sono raggruppate all'interno di un archivio (ad esempio un file ZIP), estrarle e riconoscerle tutte in una volta consente di risparmiare tempo e ridurre la complessità del codice. Il metodo `RecognizeMultipleImages` di Aspose.OCR rende questo processo semplice.

## Prerequisiti

- Visual Studio 2019 o successivo (o qualsiasi IDE compatibile con .NET).  
- .NET Framework 4.5 + o .NET Core 3.1 + installato.  
- Accesso alla libreria Aspose.OCR per .NET (link per il download sotto).  
- Una licenza valida di Aspose.OCR per l'uso in produzione (disponibile una versione di prova).

## Importare gli spazi dei nomi

Nel tuo progetto .NET, assicurati di importare gli spazi dei nomi necessari per accedere alle funzionalità offerte da Aspose.OCR:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Scaricare e installare Aspose.OCR per .NET

Scarica l'ultimo pacchetto dalla pagina di rilascio **[qui](https://releases.aspose.com/ocr/net/)** e segui i passaggi standard di installazione tramite NuGet o manuale.

## Ottenere una licenza

Acquista una licenza dalla **[pagina di acquisto](https://purchase.aspose.com/buy)** o prova la **[versione di prova gratuita](https://releases.aspose.com/)**. Posiziona il file di licenza nella radice del progetto e caricalo a runtime come descritto nella documentazione di Aspose.

## Passo 1: Configurare la directory dei documenti

Inizia inizializzando il percorso alla tua directory dei documenti:

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";
// ExEnd:1
```

> **Suggerimento:** Usa `Path.Combine` per gestire i percorsi in modo cross‑platform.

## Passo 2: Inizializzare Aspose.OCR

Crea un'istanza della classe Aspose.OCR per avviare le operazioni di OCR:

```csharp
// ExStart:3
AsposeOcr api = new AsposeOcr();
// ExEnd:3
```

## Passo 3: Specificare il percorso dell'immagine

Definisci il percorso completo al tuo archivio immagine (file ZIP contenente le foto da leggere):

```csharp
// ExStart:4
string fullPath = dataDir + "OCR.zip";
// ExEnd:4
```

## Passo 4: Riconoscere l'immagine

Esegui il riconoscimento OCR sull'archivio specificato usando le impostazioni predefinite o personalizzate. Questa chiamata estrae automaticamente ogni immagine dal ZIP ed esegue l'OCR su di essa:

```csharp
// ExStart:5
RecognitionResult[] result = api.RecognizeMultipleImages(fullPath, new RecognitionSettings
{
   //default or custom settings
});
// ExEnd:5
```

> Puoi modificare `RecognitionSettings` per migliorare la precisione per lingue o qualità d'immagine specifiche.

## Passo 5: Stampare i risultati

Scorri i risultati e stampa il testo riconosciuto per ciascuna immagine all'interno dell'archivio:

```csharp
// ExStart:6
for (int i = 0; i < result.Length; i++)
{
	 Console.WriteLine($"Image: {i}\n Result:\n {result[i].RecognitionText}");
}
// ExEnd:6
```

L'output mostra l'indice di ogni immagine seguito dalla stringa estratta, convertendo efficacemente **immagini in testo** e **estrarre testo da archivi**.

## Problemi comuni e risoluzione

| Problema | Causa | Soluzione |
|----------|-------|-----------|
| Nessun testo restituito | Qualità dell'immagine troppo bassa | Pre‑processare le immagini (es., binarizzazione) o regolare `RecognitionSettings.Dpi` |
| Eccezione durante la lettura del ZIP | Percorso dell'archivio non valido | Verificare che `fullPath` punti a un file `.zip` valido e che l'app abbia i permessi di lettura |
| Licenza non applicata | File di licenza mancante o non caricato | Eseguire `License license = new License(); license.SetLicense("Aspose.OCR.lic");` prima di creare l'istanza `AsposeOcr` |

## Domande frequenti

**D: Posso usare Aspose.OCR per .NET senza una licenza?**  
R: Sì, è disponibile una versione di prova gratuita per la valutazione, ma è necessaria una versione con licenza per le distribuzioni in produzione.

**D: La libreria supporta archivi ZIP protetti da password?**  
R: Attualmente, `RecognizeMultipleImages` funziona con file ZIP standard. Per archivi crittografati, estrai prima le immagini usando una libreria di terze parti, quindi passa l'array di immagini al motore OCR.

**D: Come posso migliorare la precisione per il testo scritto a mano?**  
R: Abilita il flag `RecognitionSettings.EnableHandwritingRecognition` e imposta un valore DPI più alto (es., 300).

**D: È possibile ottenere punteggi di confidenza per ogni riga riconosciuta?**  
R: Ogni `RecognitionResult` contiene una proprietà `Confidence` che puoi registrare o usare per filtrare i risultati a bassa confidenza.

## Conclusione

Ora disponi di un flusso di lavoro completo e pronto per la produzione per **eseguire OCR su immagini archiviate**, **convertire immagini in testo** e **estrarre testo da archivi** usando Aspose.OCR per .NET. Integra questa soluzione nelle tue applicazioni per abilitare repository di documenti ricercabili, inserimento dati automatizzato o qualsiasi scenario in cui è necessario estrarre testo da un gran numero di immagini.

## Risorse aggiuntive

- **Forum Aspose.OCR:** Per supporto della community e scenari avanzati, visita il [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16).  
- **Licenza temporanea:** Se ti serve una valutazione a breve termine, richiedi una [licenza temporanea](https://purchase.aspose.com/temporary-license/).  
- **Documentazione ufficiale:** Rimani aggiornato sulle ultime modifiche API consultando la [documentazione](https://reference.aspose.com/ocr/net/).

---

**Ultimo aggiornamento:** 2025-12-19  
**Testato con:** Aspose.OCR 24.11 per .NET  
**Autore:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
