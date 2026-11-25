---
category: general
date: 2026-10-19
description: Scopri come abilitare la GPU in Java OCR per riconoscere il testo da
  un'immagine ed estrarre rapidamente il testo da una fattura usando Aspose OCR.
draft: false
keywords:
- recognize text from image
- load image for ocr
- java ocr example aspose
- enable gpu java ocr
- aspose ocr performance
lastmod: 2026-10-19
og_description: Scopri come riconoscere il testo da un'immagine con accelerazione
  GPU in Java OCR usando Aspose. Questa guida mostra un esempio completo di java ocr,
  consigli sulle prestazioni e risoluzione dei problemi.
og_image_alt: Diagram of GPU‑accelerated OCR pipeline for Java showing image loading,
  GPU processing, and text extraction
og_title: Riconoscere il testo da un'immagine con Java OCR accelerato da GPU – Guida
  rapida
schemas:
- author: Aspose
  dateModified: '2026-10-19'
  description: Learn how to enable GPU in Java OCR to recognize text from image and
    extract text from invoice fast using Aspose OCR.
  headline: How to Enable GPU for Java OCR – Recognize Text from Image
  type: TechArticle
- questions:
  - answer: Yes, Aspose OCR runs in a headless environment as long as the GPU drivers
      are installed.
    question: Does this work on headless servers?
  - answer: Convert each PDF page to an image (e.g., using Aspose.PDF) and feed the
      images to the OCR engine.
    question: Can I process PDFs directly?
  - answer: The engine will automatically fall back to `CPU_ONLY` mode; you can also
      force CPU mode to avoid unexpected errors.
    question: What if my GPU is older and not supported?
  - answer: Load each page as a separate `OcrInput` instance, run `recognize` on each,
      and concatenate the results.
    question: How do I handle multi‑page invoices?
  - answer: There is no hard limit, but processing extremely large batches may require
      streaming to keep memory usage low.
    question: Is there a limit on the number of pages I can process in one run?
  type: FAQPage
tags:
- Java
- OCR
- GPU
- Aspose
- image processing
title: Come abilitare la GPU per Java OCR – Riconoscere il testo da un'immagine
url: /it/java/advanced-ocr-techniques/how-to-enable-gpu-for-java-ocr-recognize-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come abilitare la GPU per Java OCR – riconoscere il testo da immagine

Ti sei mai chiesto **come abilitare la GPU** quando fai OCR in Java? Non sei solo—molti sviluppatori incontrano un collo di bottiglia di prestazioni durante l'elaborazione di documenti grandi e ad alta risoluzione come le fatture. La buona notizia? Con Aspose OCR puoi attivare un unico interruttore e lasciare che la scheda grafica faccia il lavoro pesante. In questo tutorial percorreremo un **esempio java ocr** che carica un'immagine, abilita l'elaborazione GPU e estrae il testo da una fattura in un attimo.

Copriamo tutto, dall'installazione della libreria alla gestione dei casi limite come driver GPU mancanti. Alla fine sarai in grado di **riconoscere il testo da immagine** in tempo reale, e avrai un modello solido per qualsiasi progetto OCR futuro. Nessun riferimento esterno necessario—solo codice puro e eseguibile.

## Risposte rapide
- **Posso eseguirlo su una macchina solo CPU?** Sì, imposta la modalità di elaborazione su `CPU_ONLY` e il codice funzionerà senza GPU.  
- **Quali marche di GPU sono supportate?** Le GPU NVIDIA, AMD e Intel sono tutte supportate purché il driver sia aggiornato.  
- **Quanto è più veloce la modalità GPU?** Su una fattura tipica a 300 dpi, la GPU può ridurre il tempo di elaborazione da ~4 secondi a <1 secondo.  
- **È necessaria una licenza per Aspose OCR?** Una prova gratuita funziona per lo sviluppo; è necessaria una licenza commerciale per la produzione.  
- **È richiesto il pre‑processing dell'immagine?** Solo per immagini a basso contrasto o rumorose; altrimenti il motore gestisce automaticamente la maggior parte dei casi.

## Cos'è riconoscere il testo da immagine?
**Riconoscere il testo da immagine** significa convertire i caratteri visivi in una bitmap (PNG, JPEG, ecc.) in testo Unicode modificabile e ricercabile usando il riconoscimento ottico dei caratteri (OCR).  

Il motore di Aspose OCR analizza i pattern dei pixel, li confronta con i modelli linguistici e restituisce stringhe di testo semplice insieme a punteggi di confidenza. Questa capacità è essenziale per digitalizzare fatture, ricevute e moduli scansionati.

## Perché usare OCR accelerato da GPU in Java?
Usare la GPU scarica le operazioni di convoluzione intensamente computazionali sull'hardware dedicato. Aspose OCR può elaborare **oltre 50 pagine al secondo su una RTX 3060 di fascia media**, rispetto a 12 pagine al secondo su una CPU di alta gamma. L'incremento di velocità riduce la latenza nelle pipeline batch e consente scenari di scansione in tempo reale come i terminali point‑of‑sale.

## Prerequisiti

- **Java Development Kit (JDK) 11** o versioni successive installate sulla tua macchina.  
- **Maven** (o Gradle) per la gestione delle dipendenze.  
- Un **sistema con GPU** e driver aggiornati (NVIDIA, AMD o Intel).  
- Un file immagine di una fattura (ad es., `large_invoice_300dpi.png`).  

Se ti manca qualcuno di questi, procurateli prima; il resto della guida presuppone che siano presenti.

## Passo 1: Aggiungi Aspose OCR al tuo progetto

La prima cosa di cui abbiamo bisogno è la libreria Aspose OCR. Con Maven, inserisci semplicemente il seguente frammento nel tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Use the latest version available -->
</dependency>
```

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Use the latest version available -->
</dependency>
```

> **Suggerimento:** Il numero di versione cambia regolarmente; controlla Maven Central per l'ultima release per rimanere aggiornato.

Se preferisci Gradle, l'equivalente è:

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

Una volta risolta la dipendenza, sei pronto a scrivere il codice che interagisce con il motore OCR.

## Come abilitare la GPU in Aspose OCR?

`OcrEngine` è la classe principale che controlla l'elaborazione e la configurazione dell'OCR. Carica il motore OCR, imposta la modalità di elaborazione su `AUTO_GPU` e, facoltativamente, seleziona un dispositivo GPU specifico. Il motore rileverà automaticamente le GPU disponibili e assegnerà le risorse di conseguenza. Questa singola configurazione indica alla libreria di preferire la GPU ma di ricorrere alla CPU se non viene trovato alcun dispositivo compatibile.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2.1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2.2: Enable GPU processing (AUTO_GPU uses GPU when available)
        ocrEngine.setProcessingMode(OcrEngine.ProcessingMode.AUTO_GPU);

        // The rest of the steps follow...
    }
}
```

> **Perché è importante:** Abilitare la GPU può ridurre il tempo di elaborazione di una fattura a 300 dpi da diversi secondi a meno di un secondo, a seconda dell'hardware.

## Come caricare un'immagine per OCR – riconoscere il testo da immagine

`OcrInput` rappresenta la sorgente di input per il motore OCR, supportando file, stream e immagini. Prima che il motore possa leggere qualcosa, devi fornirgli un'immagine. La classe `OcrInput` di Aspose OCR accetta percorsi di file, stream o anche oggetti `BufferedImage`. Per semplicità utilizzeremo un percorso di file. Questo metodo funziona per la maggior parte dei formati immagine comuni e garantisce un uso efficiente della memoria.

```java
// Step 3.1: Prepare the input image
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/large_invoice_300dpi.png"); // <-- replace with your actual path
```

> **Caso limite:** Se l'immagine è più grande di 5 MB, considera di ridurne la risoluzione prima per evitare errori di out‑of‑memory sulla GPU.

## Come eseguire OCR ed estrarre il testo dalla fattura

`recognize` esegue l'analisi OCR sull'input fornito e restituisce un `OcrResult`. Il metodo `recognize` restituisce un oggetto `OcrResult` che contiene il testo estratto, i punteggi di confidenza e le informazioni di layout. `OcrResult` contiene il testo estratto, i punteggi di confidenza e le informazioni di layout. Puoi quindi iterare sul risultato per recuperare il testo semplice o i dati strutturati secondo necessità.

```java
// Step 4.1: Run the recognition
OcrResult ocrResult = ocrEngine.recognize(ocrInput);

// Step 4.2: Print the extracted text to console
System.out.println("=== Extracted Text ===");
System.out.println(ocrResult.getText());
```

Quando esegui il programma, dovresti vedere qualcosa del genere:

```
=== Extracted Text ===
Invoice #12345
Date: 2026-02-20
Total: $1,245.67
...
```

Se l'output appare confuso, ricontrolla che l'immagine sia chiara e che la lingua OCR sia impostata correttamente (Aspose usa l'inglese per default, ma puoi cambiarla tramite `ocrEngine.setLanguage(OcrEngine.Language.SPANISH)` ecc.).

## Esempio completo funzionante (pronto per copia‑incolla)

Di seguito trovi la classe Java completa e autonoma. Incollala nel tuo IDE, regola il percorso dell'immagine e premi **Run**.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU (auto‑detect)
        ocrEngine.setProcessingMode(OcrEngine.ProcessingMode.AUTO_GPU);

        // 3️⃣ Load the image you want to process
        OcrInput ocrInput = new OcrInput();
        // 👉 Replace with the absolute or relative path to your invoice image
        ocrInput.add("YOUR_DIRECTORY/large_invoice_300dpi.png");

        // 4️⃣ Run OCR
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // 5️⃣ Output the text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

### Output previsto

Eseguire il codice su una fattura chiara a 300 dpi solitamente produce una rappresentazione in testo semplice di ogni riga del documento. L'output esatto dipende dal layout della fattura, ma vedrai campi come *Numero Fattura*, *Data*, *Importo Totale* e descrizioni delle righe.

## Problemi comuni e come risolverli

| Sintomo | Probabile causa | Soluzione |
|---------|-----------------|----------|
| **`java.lang.UnsatisfiedLinkError`** | Driver GPU mancante o incompatibile | Installa l'ultimo driver da NVIDIA/AMD/Intel. |
| **Elaborazione molto lenta** | La GPU è ricaduta silenziosamente sulla CPU | Verifica che `ocrEngine.getProcessingMode()` restituisca `AUTO_GPU` e che `SystemInfo.isGpuAvailable()` sia true. |
| **Output vuoto** | Immagine troppo scura o a basso contrasto | Pre‑processa l'immagine (aumenta il contrasto, binarizza) prima di passarla a OCR. |
| **Out‑of‑Memory** | Immagine molto grande (>10 MP) | Ridimensiona o dividi l'immagine in tasselli; elabora ogni tassello separatamente. |

## Riepilogo passo‑passo (riferimento rapido)

| Passo | Cosa hai fatto |
|------|----------------|
| 1 | Aggiunta la dipendenza Aspose OCR |
| 2 | Creato `OcrEngine` e impostato `AUTO_GPU` |
| 3 | Caricata un'immagine di fattura tramite `OcrInput` |
| 4 | Chiamato `recognize` e stampato `ocrResult.getText()` |
| 5 | Gestiti errori comuni e verificato l'output |

## Approfondimenti – prossimi passi

- **Elaborazione batch:** Scorri una cartella di fatture e salva ogni risultato in un database.  
- **Supporto linguistico:** Cambia `ocrEngine.setLanguage(OcrEngine.Language.FRENCH)` per fatture multilingue.  
- **Post‑processing:** Usa espressioni regolari per estrarre campi come *Numero Fattura* o *Importo Totale* dal testo grezzo.  
- **Ottimizzazione GPU:** Se disponi di più GPU, esplora `ocrEngine.setGpuDeviceId(int id)` per scegliere la più veloce.

## Conclusione

Abbiamo mostrato **come abilitare la GPU** per Java OCR, presentato un chiaro **esempio java ocr**, e percorso l'intero flusso da **caricare un'immagine per OCR** a **estrarre il testo dalla fattura**. Sfruttando la modalità `AUTO_GPU` di Aspose ottieni un aumento di prestazioni senza sacrificare la compatibilità—perfetto sia per le macchine di sviluppo che per i server di produzione.

Provalo, modifica il pre‑processing dell'immagine e sperimenta con lavori batch. Il cielo è il limite quando combini l'accelerazione GPU con una libreria OCR robusta.

---

![Diagramma che mostra la pipeline OCR accelerata da GPU – come abilitare la GPU per Java OCR](https://example.com/images/gpu-ocr-pipeline.png "come abilitare gpu per Java OCR")

[Diagramma che mostra la pipeline OCR accelerata da GPU – come abilitare la GPU per Java OCR](https://example.com/images/gpu-ocr-pipeline.png "come abilitare gpu per Java OCR")

---

## Domande frequenti

**Q: Funziona su server headless?**  
A: Sì, Aspose OCR funziona in un ambiente headless purché i driver GPU siano installati.

**Q: Posso elaborare direttamente i PDF?**  
A: Converti ogni pagina PDF in un'immagine (ad es., usando Aspose.PDF) e passa le immagini al motore OCR.

**Q: Cosa succede se la mia GPU è vecchia e non supportata?**  
A: Il motore ricadrà automaticamente in modalità `CPU_ONLY`; puoi anche forzare la modalità CPU per evitare errori inaspettati.

**Q: Come gestire fatture multi‑pagina?**  
A: Carica ogni pagina come una distinta istanza `OcrInput`, esegui `recognize` su ciascuna e concatena i risultati.

**Q: Esiste un limite al numero di pagine che posso elaborare in un'unica esecuzione?**  
A: Non c'è un limite rigido, ma elaborare batch estremamente grandi potrebbe richiedere lo streaming per mantenere basso l'uso di memoria.

**Ultimo aggiornamento:** 2026-10-19  
**Testato con:** Aspose.OCR 24.11 for Java  
**Autore:** Aspose

## Tutorial correlati

- [Estrarre testo da immagine Java Guida OCR completa](/ocr/java/advanced-ocr-techniques/extract-text-from-image-java-complete-ocr-guide/)
- [Estrarre testo da immagine con Aspose OCR Java Guida rapida](/ocr/java/ocr-basics/extract-text-from-image-with-aspose-ocr-java-quick-guide/)
- [Come estrarre testo da immagine da URL usando Aspose.OCR per Java](/ocr/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}