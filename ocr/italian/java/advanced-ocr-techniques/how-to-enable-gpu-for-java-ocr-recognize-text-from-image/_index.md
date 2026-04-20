---
category: general
date: 2026-02-22
description: Scopri come abilitare la GPU in Java OCR per riconoscere il testo dalle
  immagini ed estrarre rapidamente il testo dalle fatture usando Aspose OCR.
draft: false
keywords:
- how to enable gpu
- recognize text from image
- extract text from invoice
- java ocr example
- load image for ocr
language: it
og_description: Come abilitare la GPU in Java OCR, riconoscere il testo da un'immagine
  ed estrarre il testo da una fattura con un esempio completo di Java OCR.
og_title: Come abilitare la GPU per OCR Java – Guida rapida
tags:
- Java
- OCR
- GPU
- Aspose
title: Come abilitare la GPU per OCR Java – Riconoscere il testo da un'immagine
url: /it/java/advanced-ocr-techniques/how-to-enable-gpu-for-java-ocr-recognize-text-from-image/
---

to keep code block placeholders unchanged.

Also ensure markdown formatting preserved.

Let's craft final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come abilitare la GPU per Java OCR – Riconoscere il testo da un'immagine

Ti sei mai chiesto **come abilitare la GPU** quando fai OCR in Java? Non sei solo—molti sviluppatori incontrano un collo di bottiglia di prestazioni durante l'elaborazione di documenti grandi e ad alta risoluzione come le fatture. La buona notizia? Con Aspose OCR puoi attivare un unico interruttore e lasciare che la scheda grafica faccia il lavoro pesante. In questo tutorial percorreremo un **java ocr example** che carica un'immagine, abilita l'elaborazione GPU e estrae il testo da una fattura in un attimo.

Copriamo tutto, dall'installazione della libreria alla gestione dei casi limite come driver GPU mancanti. Alla fine sarai in grado di **riconoscere il testo da un'immagine** file al volo, e avrai un modello solido per qualsiasi progetto OCR futuro. Nessun riferimento esterno necessario—solo codice puro e eseguibile.

## Prerequisiti

- **Java Development Kit (JDK) 11** o versioni più recenti installate sulla tua macchina.  
- **Maven** (o Gradle) per la gestione delle dipendenze.  
- Un sistema **GPU‑capable** con driver aggiornati (NVIDIA, AMD o Intel).  
- Un file immagine di una fattura (ad es., `large_invoice_300dpi.png`).  

Se ti manca qualcuno di questi, sistemalo prima; il resto della guida presuppone che siano presenti.

## Passo 1: Aggiungi Aspose OCR al tuo progetto

La prima cosa di cui abbiamo bisogno è la libreria Aspose OCR. Con Maven, basta inserire il seguente snippet nel tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Use the latest version available -->
</dependency>
```

> **Consiglio:** Il numero di versione cambia regolarmente; controlla Maven Central per l'ultima release per rimanere aggiornato.

Se preferisci Gradle, l'equivalente è:

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

Una volta risolta la dipendenza, sei pronto a scrivere codice che comunica con il motore OCR.

## Passo 2: Come abilitare la GPU nel motore Aspose OCR

Ora arriva la star dello spettacolo—attivare l'elaborazione GPU. Aspose OCR offre tre modalità di elaborazione:

| Modalità | Descrizione |
|----------|-------------|
| `CPU_ONLY` | Pure CPU, safe for any machine. |
| `GPU_ONLY` | Forces GPU, fails if no compatible device. |
| `AUTO_GPU` | Detects a GPU and uses it when available, otherwise falls back to CPU. |

Per la maggior parte degli scenari consigliamo **`AUTO_GPU`** perché ti offre il meglio di entrambi i mondi. Ecco come abilitarla:

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

## Passo 3: Carica l'immagine per OCR – Riconoscere il testo da un'immagine

Prima che il motore possa leggere qualcosa, devi fornirgli un'immagine. La classe `OcrInput` di Aspose OCR accetta percorsi di file, stream o anche oggetti `BufferedImage`. Per semplicità useremo un percorso di file:

```java
// Step 3.1: Prepare the input image
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/large_invoice_300dpi.png"); // <-- replace with your actual path
```

> **Caso limite:** Se l'immagine è più grande di 5 MB, considera di ridurne la risoluzione prima per evitare errori di out‑of‑memory sulla GPU.

## Passo 4: Esegui OCR ed estrai il testo dalla fattura

Ora chiediamo al motore di fare la sua magia. Il metodo `recognize` restituisce un oggetto `OcrResult` che contiene il testo estratto, i punteggi di confidenza e le informazioni di layout.

```java
// Step 4.1: Run the recognition
OcrResult ocrResult = ocrEngine.recognize(ocrInput);

// Step 4.2: Print the extracted text to console
System.out.println("=== Extracted Text ===");
System.out.println(ocrResult.getText());
```

Quando esegui il programma, dovresti vedere qualcosa di simile:

```
=== Extracted Text ===
Invoice #12345
Date: 2026-02-20
Total: $1,245.67
...
```

Se l'output appare confuso, verifica che l'immagine sia chiara e che la lingua OCR sia impostata correttamente (Aspose usa l'inglese per default, ma puoi cambiarla tramite `ocrEngine.setLanguage(OcrEngine.Language.SPANISH)` ecc.).

## Passo 5: Esempio completo funzionante (pronto per copia‑incolla)

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

Eseguire il codice su una fattura chiara a 300 dpi produce tipicamente una rappresentazione di testo semplice di ogni riga del documento. L'output esatto dipende dal layout della fattura, ma vedrai campi come *Invoice Number*, *Date*, *Total Amount* e descrizioni delle righe.

## Problemi comuni e come risolverli

| Sintomo | Probabile causa | Soluzione |
|---------|-----------------|-----------|
| **`java.lang.UnsatisfiedLinkError`** | Driver GPU mancante o incompatibile | Installa l'ultimo driver da NVIDIA/AMD/Intel. |
| **Very slow processing** | GPU fallback to CPU silently | Verifica che `ocrEngine.getProcessingMode()` restituisca `AUTO_GPU` e che `SystemInfo.isGpuAvailable()` sia true. |
| **Blank output** | Image too dark or low contrast | Pre‑processa l'immagine (aumenta contrasto, binarizza) prima di passarla a OCR. |
| **Out‑of‑Memory** | Very large image (>10 MP) | Ridimensiona o suddividi l'immagine in tasselli; elabora ogni tassello separatamente. |

## Riepilogo passo‑passo (riferimento rapido)

| Passo | Cosa hai fatto |
|-------|-----------------|
| 1 | Aggiunta dipendenza Aspose OCR |
| 2 | Creato `OcrEngine` e impostato `AUTO_GPU` |
| 3 | Caricata un'immagine di fattura tramite `OcrInput` |
| 4 | Chiamato `recognize` e stampato `ocrResult.getText()` |
| 5 | Gestiti errori comuni e verificato l'output |

## Approfondimenti – Prossimi passi

- **Elaborazione batch:** Scorri una cartella di fatture e memorizza ogni risultato in un database.  
- **Supporto linguistico:** Cambia `ocrEngine.setLanguage(OcrEngine.Language.FRENCH)` per fatture multilingue.  
- **Post‑processing:** Usa espressioni regolari per estrarre campi come *Invoice Number* o *Total Amount* dal testo grezzo.  
- **Ottimizzazione GPU:** Se hai più GPU, esplora `ocrEngine.setGpuDeviceId(int id)` per scegliere la più veloce.

## Conclusione

Abbiamo mostrato **come abilitare la GPU** per Java OCR, dimostrato un **java ocr example** pulito, e percorso l'intero flusso da **carica l'immagine per OCR** a **estrai il testo dalla fattura**. Sfruttando la modalità `AUTO_GPU` di Aspose ottieni un boost di prestazioni senza sacrificare la compatibilità—perfetto sia per macchine di sviluppo che per server di produzione.

Provalo, regola il pre‑processing dell'immagine e sperimenta con lavori batch. Il cielo è il limite quando combini l'accelerazione GPU con una libreria OCR robusta.

---

![Diagramma che mostra la pipeline OCR accelerata dalla GPU – come abilitare la GPU per Java OCR](https://example.com/images/gpu-ocr-pipeline.png "come abilitare gpu per Java OCR")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}