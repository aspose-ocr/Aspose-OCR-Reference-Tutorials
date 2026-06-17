---
category: general
date: 2026-05-06
description: Crea PDF ricercabile da un'immagine usando Aspose OCR in Java. Impara
  a convertire l'immagine in PDF, attivare la correzione ortografica e utilizzare
  la GPU OCR per risultati rapidi.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- enable spell correction
- use ocr gpu
- process image ocr
language: it
og_description: Crea PDF ricercabile da un'immagine usando Aspose OCR in Java. Questa
  guida mostra come convertire un'immagine in PDF, abilitare la correzione ortografica
  e utilizzare la GPU per l'OCR.
og_title: Crea PDF ricercabile da immagine con OCR Java
tags:
- OCR
- Java
- PDF
title: Crea PDF ricercabile da immagine con Java OCR
url: /it/java/ocr-operations/create-searchable-pdf-from-image-with-java-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea PDF Ricercabile da Immagine con Java OCR

Hai mai dovuto **creare un PDF ricercabile** da un'immagine scansionata senza sapere da dove cominciare? Non sei solo: la maggior parte degli sviluppatori si imbatte in questo ostacolo al primo approccio ai PDF basati su immagine. Fortunatamente, con Aspose OCR per Java puoi **convertire l'immagine in PDF**, trasformare il testo in contenuto selezionabile e persino aggiungere la correzione ortografica per un risultato curato.

In questo tutorial percorreremo un esempio completo, pronto da eseguire, che mostra come **usare OCR GPU** quando è disponibile, come **processare l'OCR dell'immagine** in modo efficiente e perché abilitare la correzione ortografica è importante per la ricerca successiva. Alla fine avrai un modo a un click per generare un PDF ricercabile da distribuire agli utenti o archiviare per conformità.

> **Consiglio professionale:** Se esegui il codice su una macchina senza GPU, il programma ricade automaticamente sulla CPU, così non dovrai riscrivere nulla.

---

## Cosa Ti Serve

- **Java 8+** (il codice compila con JDK 8 e versioni successive)
- Libreria **Aspose OCR per Java** (scarica l'ultimo JAR dal sito Aspose)
- Un'**immagine di input** (JPEG, PNG, TIFF, ecc.) che desideri trasformare in PDF ricercabile
- (Opzionale) Una **GPU** con supporto CUDA se vuoi il riconoscimento più veloce possibile

Nessun framework aggiuntivo, nessuna magia Maven/Gradle—solo un singolo JAR nel classpath e sei pronto a partire.

---

## Passo 1: Inizializzare il Motore OCR – Il Cuore del Processo  

Per prima cosa creiamo un'istanza di `OcrEngine` e la puntiamo al file sorgente. Questo oggetto è il cavallo di battaglia che leggerà l'immagine, eseguirà la rete neurale e ci restituirà il testo.

```java
import com.aspose.ocr.*;

public class QuickStart {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image you want to convert
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));
```

*Perché è importante:* Inizializzare il motore una sola volta e riutilizzarlo evita il sovraccarico di caricare ripetutamente le librerie native—un piccolo vantaggio di prestazioni che si somma quando si elaborano decine di file in batch.

---

## Passo 2: Scegliere il Dispositivo di Elaborazione – Usa OCR GPU Quando Possibile  

Se la tua workstation dispone di una GPU compatibile, puoi dire ad Aspose di eseguire il lavoro pesante su di essa. Altrimenti il motore passa automaticamente alla CPU.

```java
        // Prefer GPU; fall back to CPU if no compatible device is found
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);
```

*Qual è il beneficio?* L'accelerazione GPU può ridurre di alcuni secondi il tempo di elaborazione per ogni pagina, soprattutto per scansioni ad alta risoluzione. Il fallback garantisce che lo stesso codice funzioni ovunque, ed è per questo che consigliamo **use OCR GPU** come impostazione predefinita.

---

## Passo 3: Accelerare la Scansione – Sfruttare Tutti i Core CPU  

Anche quando la GPU è occupata, le fasi di pre‑elaborazione circostanti possono essere parallelizzate. Impostare il conteggio dei thread al numero di processori disponibili dà al motore la possibilità di elaborare più blocchi contemporaneamente.

```java
        // Use all logical cores for preprocessing and language detection
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());
```

*Nota:* Su un laptop a 4 core questo avvierà quattro thread; su una workstation a 16 core otterrai il pieno beneficio. Tieni presente che più thread significano un maggior utilizzo di memoria.

---

## Passo 4: Pulire l'Immagine – Filtri di Pre‑elaborazione  

Una scansione sfocata o rumorosa produrrà testo spazzatura. Aggiungere un paio di filtri integrati migliora drasticamente l'accuratezza.

```java
        // Deskew the image so text lines are horizontal
        ocrEngine.getPreprocessing().add(new DeskewFilter());

        // Remove speckles and background noise
        ocrEngine.getPreprocessing().add(new NoiseRemovalFilter());
```

*Perché questi filtri?* `DeskewFilter` corregge la rotazione che spesso si verifica quando un documento viene alimentato allo scanner con un angolo. `NoiseRemovalFilter` elimina i pixel erranti che altrimenti verrebbero interpretati come caratteri. È come dare al motore OCR un foglio di carta pulito da leggere.

---

## Passo 5: Attivare le Funzionalità Intelligenti – Abilita Correzione Ortografica e Rilevamento Automatico della Lingua  

Se lavori con documenti multilingue, o semplicemente vuoi meno errori, attiva il correttore ortografico integrato e lascia che il motore indovini la lingua.

```java
        // Activate spell correction to fix common OCR mistakes
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Let the engine automatically detect the language of the input
        ocrEngine.getSettings().setAutoDetectLanguage(true);
```

*Quando è utile?* Immagina che la tua scansione contenga sezioni sia in inglese che in spagnolo. La funzione di auto‑rilevamento cambia i dizionari al volo, mentre la correzione ortografica pulisce caratteri letti erroneamente come “0” al posto di “O”. Questo passaggio è essenziale per produrre un **PDF ricercabile** che restituisca risultati corretti.

---

## Passo 6: Salvare il Risultato – Converti Immagine in PDF e Rendilo Ricercabile  

Infine chiediamo al motore di scrivere un PDF in cui l'immagine originale rimane dietro a uno strato di testo invisibile. Questo è il classico flusso **convert image to PDF**, ma ora il PDF è ricercabile.

```java
        // Generate a searchable PDF – the text layer sits behind the original image
        ocrEngine.save("YOUR_DIRECTORY/output-searchable.pdf", OcrSaveFormat.PDF_SEARCHABLE);

        System.out.println("Searchable PDF generated successfully.");
    }
}
```

Il file di output (`output-searchable.pdf`) può essere aperto con qualsiasi visualizzatore PDF; potrai selezionare, copiare e cercare il testo come in un PDF nativo. Nessuno strumento aggiuntivo necessario.

---

## Esempio Completo – Copia‑e‑Incolla  

Di seguito trovi l'intero programma, pronto per la compilazione. Sostituisci `YOUR_DIRECTORY` con la cartella che contiene `input.jpg`.

```java
import com.aspose.ocr.*;

public class QuickStart {
    public static void main(String[] args) throws Exception {
        // Step 1: Create the OCR engine and load the source image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));

        // Step 2: Select the processing device (GPU if available, otherwise CPU)
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);

        // Step 3: Use all available CPU cores to speed up recognition
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Step 4: Add preprocessing filters to improve image quality
        ocrEngine.getPreprocessing().add(new DeskewFilter());
        ocrEngine.getPreprocessing().add(new NoiseRemovalFilter());

        // Step 5: Enable spell correction and automatic language detection
        ocrEngine.getSettings().setEnableSpellCorrection(true);
        ocrEngine.getSettings().setAutoDetectLanguage(true);

        // Step 6: Perform OCR and save the result as a searchable PDF
        ocrEngine.save("YOUR_DIRECTORY/output-searchable.pdf", OcrSaveFormat.PDF_SEARCHABLE);

        System.out.println("Searchable PDF generated successfully.");
    }
}
```

**Output previsto:** Quando esegui il programma vedrai la riga di console *“Searchable PDF generated successfully.”* Aprendo `output-searchable.pdf` in Adobe Reader potrai digitare una parola dell'immagine originale nella casella di ricerca e saltare immediatamente alla sua posizione.

---

## Domande Frequenti & Casi Limite  

- **E se la GPU non viene rilevata?**  
  La chiamata `setDeviceType(OcrDeviceType.GPU)` non genera eccezioni; indica semplicemente al motore di provare prima la GPU. Se fallisce, il motore passa silenziosamente alla CPU.

- **Posso elaborare più immagini in un'unica esecuzione?**  
  Sì. Avvolgi il codice in un ciclo, cambia il nome del file a ogni iterazione e riutilizza la stessa istanza di `OcrEngine` per mantenere basso l'uso di memoria.

- **Il mio PDF è enorme—come lo riduco?**  
  Dopo l'OCR puoi usare le API di ottimizzazione PDF di Aspose, oppure semplicemente ridimensionare l'immagine di origine prima di passarla al motore (`ImageStream.fromFile(...).setResolution(150)` per 150 DPI).

- **Devo conservare la risoluzione originale dell'immagine per conformità legale.**  
  Il formato `PDF_SEARCHABLE` preserva il bitmap originale esattamente; lo strato di testo invisibile viene aggiunto sopra senza alterare la qualità visiva.

---

## Riepilogo Visivo  

![crea esempio pdf ricercabile](placeholder-image.png "crea esempio pdf ricercabile")

*Testo alternativo:* *crea esempio pdf ricercabile – motore OCR Java che trasforma un JPG scansionato in un PDF ricercabile.*

---

## Conclusione  

Ora disponi di una **soluzione completa, end‑to‑end** per trasformare qualsiasi immagine in un **PDF ricercabile** usando Aspose OCR per Java. **Convertendo l'immagine in PDF**, **abilitando la correzione ortografica** e **usando OCR GPU** quando possibile, ottieni risultati rapidi, accurati e ricercabili su tutte le piattaforme.

Qual è il prossimo passo? Prova a sperimentare con:

- **Formati di output diversi** (`PDF`, `DOCX`, `HTML`) per vedere come si comporta lo strato di testo.
- **Dizionari personalizzati** se elabori gergo specifico di dominio.
- **Elaborazione batch** per gestire migliaia di scansioni automaticamente.

Sentiti libero di modificare il conteggio dei thread, scambiare i filtri o inserire la tua pipeline di pre‑elaborazione. Il modello di base rimane lo stesso: carica → pre‑elabora → configura → OCR → salva.

Buona programmazione, e che i tuoi PDF siano sempre ricercabili!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}