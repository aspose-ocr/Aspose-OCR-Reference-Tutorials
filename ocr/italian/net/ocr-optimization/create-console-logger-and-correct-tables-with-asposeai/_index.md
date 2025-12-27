---
category: general
date: 2025-12-27
description: Crea un logger console in C# e abilita il download automatico nelle tabelle
  corrette usando AsposeAI. Scopri come visualizzare l'output della tabella corretta
  in pochi passaggi.
draft: false
keywords:
- create console logger
- enable auto download
- how to correct tables
- setup console logger
- display corrected table
language: it
og_description: Crea un logger console in C# e abilita il download automatico nelle
  tabelle corrette usando AsposeAI. Segui questa guida per visualizzare rapidamente
  l'output della tabella corretta.
og_title: Crea logger della console e tabelle corrette con AsposeAI
tags:
- AsposeAI
- C#
- OCR
- Table processing
title: Crea logger console e tabelle corrette con AsposeAI
url: /it/net/ocr-optimization/create-console-logger-and-correct-tables-with-asposeai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea logger per console e correggi tabelle con AsposeAI

Hai mai avuto bisogno di **creare logger per console** in una pipeline AI C# ma non sapevi da dove cominciare? In questa guida percorreremo l’intero processo—come creare un logger per console, abilitare il download automatico dei file modello e, infine, **come correggere le tabelle** generate dall’OCR. Alla fine sarai in grado di **visualizzare le tabelle corrette** nella tua console con poche righe di codice.

Copriamo tutto, dall’impostazione iniziale del logger alla pulizia finale, così non dovrai cercare tra documenti sparsi. Non è necessaria alcuna esperienza pregressa con AsposeAI; basta una conoscenza di base di C# e .NET. Lungo il percorso inseriremo consigli sulle **best practice per impostare logger per console**, parleremo di casi limite e mostreremo come dovrebbe apparire l’output.

---

## Prerequisiti

Prima di iniziare, assicurati di avere a disposizione quanto segue:

- .NET 6.0 o successivo (il codice utilizza funzionalità linguistiche moderne)
- Visual Studio 2022 o qualsiasi IDE che supporti progetti C#
- Pacchetto NuGet **Aspose.AI** installato (`Install-Package Aspose.AI`)
- Pacchetto NuGet **Aspose.OCR** installato (`Install-Package Aspose.OCR`)
- Un oggetto risultato OCR di esempio (`ocrResult`) ottenuto da una precedente chiamata Aspose.OCR

Se manca qualcosa, fermati ora e procuratelo—ti ringrazierai più tardi.

---

## Passo 1: Crea logger per console e inizializza AsposeAI

La prima cosa di cui abbiamo bisogno è un logger che scriva direttamente sulla console. Questo rende il debug un gioco da ragazzi e fornisce feedback in tempo reale mentre il motore AI è in esecuzione.

```csharp
using Aspose.AI;
using Aspose.AI.PostProcessor;
using Aspose.OCR;

// Step 1: Create a logger that writes to the console
ILogger consoleLogger = new ConsoleLogger();

// Step 2: Initialise the AsposeAI engine with the logger
AsposeAI asposeAI = new AsposeAI(consoleLogger);
```

**Perché è importante:**  
`ConsoleLogger` implementa l’interfaccia `ILogger`, quindi tutti i messaggi interni di AsposeAI (caricamento modello, stato del post‑processor, errori) appaiono immediatamente nel tuo terminale. È il modo più semplice per **impostare logger per console** senza introdurre framework di logging esterni.

> **Pro tip:** Se in seguito ti serve il logging su file, basta sostituire `ConsoleLogger` con un logger personalizzato che implementi `ILogger`—il resto del codice rimane invariato.

---

## Passo 2: Abilita il download automatico per i modelli AI

AsposeAI può recuperare i file modello necessari al volo. Attivare questa opzione ti salva dal dover scaricare manualmente grandi blob binari.

```csharp
// Step 3: (Optional) Configure automatic model download and set the model directory
AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
{
    AllowAutoDownload = true,               // <‑‑ enable auto download
    DirectoryModelPath = "YOUR_DIRECTORY"   // change to a writable folder
};
```

**Cosa potrebbe andare storto?**  
Se `DirectoryModelPath` punta a una posizione di sola lettura, il download automatico fallirà e vedrai un’eccezione nella console. Assicurati che la cartella esista e che l’app abbia i permessi di scrittura.

---

## Passo 3: Crea un post‑processor per tabelle (come correggere le tabelle)

Le tabelle estratte dall’OCR sono spesso disordinate—celle fuse, bordi mancanti o testo disallineato. `TableAIProcessor` di AsposeAI può pulirle automaticamente.

```csharp
// Step 4: Create a table post‑processor that lets the engine decide when to run correction
TableAIProcessor tableProcessor = new TableAIProcessor(AITableDetectionMode.AUTO);
```

**Perché la modalità AUTO?**  
`AITableDetectionMode.AUTO` consente al motore di analizzare l’output OCR e decidere se è necessaria una correzione. Se preferisci il controllo manuale, puoi usare `MANUAL` e invocare `RunCorrection()` da solo.

---

## Passo 4: Collega il post‑processor e la sua configurazione

Ora uniamo tutto—logger, configurazione modello e processore di tabelle.

```csharp
// Step 5: Attach the post‑processor and its configuration to the AI engine
asposeAI.SetPostProcessor(tableProcessor, modelConfig);
```

A questo punto il motore AI sa *dove* memorizzare i modelli, *come* loggare e *qual*e post‑processing applicare. È una chiara separazione delle responsabilità che rende le modifiche future indolori.

---

## Passo 5: Esegui il post‑processor sul risultato OCR

Supponendo di avere già un `ocrResult` da Aspose.OCR, basta passarne il riferimento al motore.

```csharp
// Step 6: Run the post‑processor on the OCR result returned by Aspose.OCR
asposeAI.RunPostprocessor(ocrResult);
```

**Attenzione a casi limite:**  
Se `ocrResult` non contiene tabelle, il processore salterà silenziosamente la correzione. Puoi verificare `tableProcessor.GetResult().Count` in seguito per accertarti che qualcosa sia stato effettivamente processato.

---

## Passo 6: Recupera e **visualizza l'output della tabella corretta**

Infine, estraiamo il testo della tabella pulita e lo stampiamo sulla console.

```csharp
// Step 7: Retrieve and display the corrected table text
Console.WriteLine("Corrected table output:");
Console.WriteLine(tableProcessor.GetResult()[0].RecognitionText);
```

L’output avrà un aspetto simile a questo (a seconda dell’immagine di origine):

```
Corrected table output:
| Item   | Quantity | Price |
|--------|----------|-------|
| Apple  | 10       | $1.20 |
| Banana | 5        | $0.80 |
```

Se vedi una stringa vuota, ricontrolla che l’OCR abbia effettivamente rilevato una tabella e che `AllowAutoDownload` sia riuscito.

---

## Passo 7: Pulisci le risorse

Buona cittadinanza significa rilasciare gli oggetti pesanti quando hai finito.

```csharp
// Step 8: Release resources used by the AI engine
asposeAI.Dispose();
```

Saltare questo passo può lasciare handle di file aperti, specialmente su Windows dove i file modello rimangono bloccati.

---

## Esempio completo funzionante

Di seguito trovi il programma completo da copiare‑incollare in un nuovo progetto console. Sostituisci `"YOUR_DIRECTORY"` con un percorso reale e assicurati che `ocrResult` sia popolato prima di chiamare `RunPostprocessor`.

```csharp
using System;
using Aspose.AI;
using Aspose.AI.PostProcessor;
using Aspose.OCR;

namespace AsposeAITableCorrection
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create a console logger
            ILogger consoleLogger = new ConsoleLogger();

            // 2️⃣ Initialise AsposeAI with the logger
            AsposeAI asposeAI = new AsposeAI(consoleLogger);

            // 3️⃣ Configure auto‑download (optional but recommended)
            AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
            {
                AllowAutoDownload = true,
                DirectoryModelPath = @"C:\AsposeModels" // <-- change this
            };

            // 4️⃣ Create the table processor (auto‑detect mode)
            TableAIProcessor tableProcessor = new TableAIProcessor(AITableDetectionMode.AUTO);

            // 5️⃣ Attach processor and config
            asposeAI.SetPostProcessor(tableProcessor, modelConfig);

            // 6️⃣ Obtain OCR result (replace with your own OCR call)
            // Example placeholder – you should have this from Aspose.OCR already
            OcrResult ocrResult = GetOcrResultSomehow();

            // 7️⃣ Run post‑processor on the OCR output
            asposeAI.RunPostprocessor(ocrResult);

            // 8️⃣ Display corrected table
            Console.WriteLine("Corrected table output:");
            if (tableProcessor.GetResult().Count > 0)
            {
                Console.WriteLine(tableProcessor.GetResult()[0].RecognitionText);
            }
            else
            {
                Console.WriteLine("No tables were detected or corrected.");
            }

            // 9️⃣ Clean up
            asposeAI.Dispose();
        }

        // Dummy method – replace with your actual OCR logic
        static OcrResult GetOcrResultSomehow()
        {
            // For illustration only
            OcrEngine engine = new OcrEngine();
            engine.Image = ImageStream.FromFile("sample-table.png");
            return engine.Recognize();
        }
    }
}
```

**Output console previsto** (supponendo un’immagine di tabella semplice):

```
Corrected table output:
| Name   | Age | City      |
|--------|-----|-----------|
| Alice  | 30  | New York  |
| Bob    | 25  | Seattle   |
```

---

## Domande frequenti

- **È necessaria una connessione internet per il download automatico?**  
  Sì. La prima volta che il modello viene richiesto, AsposeAI si collega al suo CDN. Dopo che il file è stato salvato in `DirectoryModelPath`, le esecuzioni successive funzionano offline.

- **Cosa succede se la mia tabella ha celle fuse?**  
  Il modello AI tenta di separare le celle fuse basandosi su indizi visivi. Se il risultato non è corretto, considera di pre‑elaborare l’immagine (aumentare contrasto, raddrizzare rotazione) prima dell’OCR.

- **Posso elaborare più tabelle contemporaneamente?**  
  Assolutamente. `tableProcessor.GetResult()` restituisce una lista; itera su di essa per stampare ogni tabella.

- **`ConsoleLogger` è thread‑safe?**  
  Scrive direttamente su `System.Console`, che è thread‑safe per scritture semplici. In scenari multi‑thread pesanti, potrebbe convenire un logger personalizzato con sincronizzazione.

---

## Prossimi passi e argomenti correlati

Ora che sai **come correggere le tabelle**, potresti voler:

- **Abilitare il download automatico** per altri modelli AsposeAI (ad esempio traduzione linguistica).
- **Impostare logger per console** con livelli di log diversi (Info, Warning, Error) per un controllo più fine.
- Esplorare **visualizzare la tabella corretta** in una GUI (WinForms o WPF) anziché nella console.
- Combinare la correzione delle tabelle con **l'estrazione dei dati** per inserirli direttamente in un database.

Ognuno di questi si basa sulle fondamenta appena gettate, quindi sentiti libero di sperimentare.

---

## Conclusione

Abbiamo percorso l’intero ciclo di vita di **creare logger per console**, abilitare il download automatico e **correggere le tabelle** con AsposeAI, terminando con un modo pulito per **

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}