---
category: general
date: 2026-10-30
description: Scopri come estrarre rapidamente testo da un'immagine con il supporto
  Aspose OCR GPU in Java. Questa guida mostra come impostare l'ID del dispositivo
  GPU e ottenere OCR ad alte prestazioni.
draft: false
keywords:
- extract text from image
- how to extract text
- aspose ocr gpu
- recognize text image java
- gpu acceleration OCR
lastmod: 2026-10-30
og_description: Scopri come estrarre rapidamente testo da un'immagine con il supporto
  Aspose OCR GPU in Java. Questa guida mostra come impostare l'ID del dispositivo
  GPU per prestazioni ottimali.
og_image_alt: 'Developer guide: extract text from image using Aspose OCR GPU in Java'
og_title: Come estrarre testo da un'immagine con Aspose OCR GPU in Java
schemas:
- author: Aspose
  dateModified: '2026-10-30'
  description: Learn how to extract text from image quickly with Aspose OCR GPU support
    in Java. This guide shows how to set GPU device ID and achieve high‑performance
    OCR.
  headline: How to extract text from image with Aspose OCR GPU in Java
  type: TechArticle
- questions:
  - answer: Yes—just install a valid Aspose OCR license. The free trial is for evaluation
      only.
    question: Can I use this in a commercial application?
  - answer: Absolutely; as long as the NVIDIA driver and CUDA toolkit are installed,
      the library runs on headless Linux environments.
    question: Does the GPU version work on Linux servers?
  - answer: Aspose OCR can process images up to **5000 × 5000 px** without loading
      the whole file into memory.
    question: What is the maximum image size supported?
  - answer: Replace the old JAR with the new one and update your Maven/Gradle dependency
      version number.
    question: How do I upgrade to the latest Aspose OCR version?
  - answer: Yes—`OcrResult` provides layout information, including word‑level bounding
      boxes, when you enable the `setIncludeLayout(true)` option.
    question: Is there a way to get bounding‑box coordinates for each word?
  type: FAQPage
tags:
- Java
- OCR
- Aspose
- GPU
title: Come estrarre testo da un'immagine con Aspose OCR GPU in Java
url: /it/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come estrarre testo da immagine con Aspose OCR GPU in Java

Se hai mai provato a **estrarre testo da immagine** in un'applicazione Java e hai riscontrato che la CPU si blocca con scansioni ad alta risoluzione, non sei solo. Molti sviluppatori incontrano colli di bottiglia di prestazioni durante l'elaborazione di documenti di grandi dimensioni. Aspose OCR per Java rimuove questo ostacolo consentendoti di eseguire l'OCR sulla GPU, riducendo drasticamente i tempi di elaborazione. In questo tutorial vedrai un esempio completo, pronto per l'esecuzione, che mostra come impostare la licenza, abilitare l'accelerazione GPU e **impostare l'ID del dispositivo GPU** quando sono presenti più schede grafiche.

## Risposte rapide
- **Qual è il modo più veloce per estrarre testo da immagine in Java?** Usa Aspose OCR con accelerazione GPU e imposta l'ID del dispositivo GPU appropriato.  
- **Quale versione di Java è richiesta?** Java 17 o superiore è consigliata per le migliori prestazioni.  
- **Ho bisogno di una licenza per il supporto GPU?** Sì—le funzionalità GPU sono sbloccate solo con una licenza valida di Aspose OCR.  
- **Posso eseguire questo su un server headless?** Assolutamente; sono richiesti solo il driver GPU e il toolkit CUDA.  
- **Quante lingue sono supportate?** Oltre 30 lingue, tra cui Inglese, Cinese, Arabo e Hindi.

## Cos'è l'estrazione di testo da immagine?
Estrarre testo da un'immagine significa convertire la rappresentazione visiva dei caratteri memorizzata in formati bitmap come PNG, JPG o TIFF in testo Unicode modificabile e ricercabile. Questo processo, noto come Riconoscimento Ottico dei Caratteri (OCR), consente attività successive come indicizzazione, traduzione ed estrazione dei dati.

## Perché usare Aspose OCR GPU?
Aspose OCR sfrutta l'accelerazione GPU per gestire immagini grandi e ad alta risoluzione in modo molto più efficiente rispetto all'elaborazione solo CPU. Supporta oltre 30 formati di input e può elaborare immagini fino a 5000 × 5000 px mantenendo un basso utilizzo di memoria, offrendo un riconoscimento fino a cinque volte più veloce su GPU NVIDIA moderne.

## Di cosa avrai bisogno
- **Java 17** o superiore (compatibile con Java 8+, ma le versioni LTS offrono migliori prestazioni JIT).  
- **Libreria Aspose OCR per Java** (scarica il JAR dal sito Aspose).  
- Un valido **file di licenza Aspose OCR** (`Aspose.OCR.lic`). La versione di prova funziona, ma le funzionalità GPU richiedono una versione con licenza.  
- Un file immagine (`sample-image.png`) che contiene testo chiaro e leggibile dalla macchina.  
- Una GPU NVIDIA compatibile con CUDA (o equivalente) con il driver appropriato installato.

Se qualcuno di questi termini ti è sconosciuto, non preoccuparti—ogni punto verrà spiegato man mano.

## Passo 1: aggiungere Aspose OCR al tuo progetto
Per prima cosa, includi il JAR di Aspose OCR nel tuo classpath. Se usi Maven, aggiungi la seguente dipendenza a `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

Per Gradle, usa:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

Se preferisci il metodo manuale, copia il JAR in una cartella `libs/` e aggiungilo al percorso dei moduli dell'IDE.

> **Suggerimento:** Mantieni il numero di versione allineato alle note di rilascio; le versioni più recenti spesso includono miglioramenti delle prestazioni per l'elaborazione GPU.

## Passo 2: caricare la licenza Aspose OCR (necessario per l'uso della GPU)
Senza licenza la chiamata `setEnableGpu(true)` tornerà silenziosamente alla modalità CPU. Carica la licenza all'inizio di `main`:

```java
import com.aspose.ocr.License;

// ...

License ocrLicense = new License();
ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

Sostituisci `YOUR_DIRECTORY` con il percorso assoluto o relativo dove hai salvato il file `.lic`. Un percorso errato genera una `FileNotFoundException`, quindi verifica attentamente l'ortografia.

## Passo 3: creare il motore OCR e abilitare l'accelerazione GPU
La classe `OcrEngine` è il componente principale che esegue le operazioni OCR sulle immagini.

```java
import com.aspose.ocr.OcrEngine;

// ...

OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getDevice().setEnableGpu(true);       // activate GPU support
ocrEngine.getDevice().setGpuDeviceId(0);        // optional: choose GPU index (0 = first card)
```

Perché preoccuparsi dell'ID del dispositivo? In un ambiente multi‑GPU puoi dedicare una scheda al preprocessing e un'altra all'OCR. Impostare l'ID garantisce che il lavoro pesante venga eseguito sull'hardware previsto.

## Passo 4: preparare l'immagine di input
La classe `OcrInput` rappresenta la collezione di immagini che desideri elaborare.

```java
import com.aspose.ocr.OcrInput;

// ...

OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/sample-image.png"); // path to the image you want to process
```

Se devi elaborare uno stream (ad esempio, un file caricato), usa `ocrInput.add(InputStream)` al suo posto.

## Passo 5: eseguire il processo di riconoscimento e recuperare il risultato
La classe `OcrResult` incapsula il testo semplice, i punteggi di confidenza e le informazioni di layout opzionali restituite dal motore.

```java
import com.aspose.ocr.OcrResult;

// ...

OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("Recognized text:\n" + ocrResult.getText());
```

La console mostrerà qualcosa del genere:

```
Recognized text:
Hello, world!
This is a sample image.
```

Se l'immagine è sfocata o la lingua non è supportata, il risultato potrebbe essere vuoto. In tal caso, controlla il valore `ocrResult.getConfidence()` (0‑100) per decidere se riprovare con il preprocessing.

## Esempio completo, eseguibile
Unendo tutti i pezzi ottieni una singola classe Java che puoi copiare‑incollare nel tuo IDE:

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license – required for GPU usage
        License ocrLicense = new License();
        ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");

        // 2️⃣ Create OCR engine and turn on GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getDevice().setEnableGpu(true);      // enable GPU acceleration
        ocrEngine.getDevice().setGpuDeviceId(0);       // optional: select GPU index

        // 3️⃣ Load the image you want to process
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/sample-image.png");

        // 4️⃣ Perform recognition
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // 5️⃣ Output the recognized text
        System.out.println("Recognized text:\n" + ocrResult.getText());
    }
}
```

> **Output previsto:** La console stampa il testo esatto che appare in `sample-image.png`. Quando la GPU è attiva, il tempo di elaborazione tipicamente scende da diversi secondi (CPU) a meno di un secondo per una scansione tipica a 300 dpi.

## Domande comuni e casi particolari

### Funziona su un server headless?
Sì. Il driver GPU deve essere installato, ma non è necessario alcun display. Assicurati che il toolkit `CUDA` (o l'equivalente per la tua GPU) sia disponibile nel `PATH` di sistema. Questa configurazione consente all'OCR di funzionare in ambienti cloud o containerizzati senza interfaccia grafica.

### Cosa fare se ho più di una GPU e voglio usare GPU 1?
Cambia l'ID del dispositivo come mostrato:

```java
ocrEngine.getDevice().setGpuDeviceId(1); // selects the second GPU (zero‑based index)
```

Impostare l'ID a `1` indirizza il motore OCR a utilizzare la seconda GPU del sistema, utile quando la prima GPU è riservata ad altri carichi di lavoro.

### Come estrarre testo da immagine in una lingua diversa?
Imposta la lingua prima di chiamare `recognize`:

```java
ocrEngine.setLanguage(OcrLanguage.FRENCH);
```

Aspose OCR supporta **oltre 30 lingue**, inclusi script da destra a sinistra come Arabo e Ebraico. Selezionare la lingua corretta migliora notevolmente l'accuratezza.

### Cosa fare se l'immagine contiene più pagine (ad esempio, un PDF convertito in immagini)?
Crea una voce `OcrInput` separata per ogni pagina, o itera sui file:

```java
for (String path : imagePaths) {
    ocrInput.add(path);
}
```

Il motore concatena i risultati in ordine, preservando la sequenza delle pagine nell'output finale.

### Come gestire risultati a bassa confidenza?
Controlla il punteggio di confidenza:

```java
if (ocrResult.getConfidence() < 70) {
    System.out.println("Low confidence – consider preprocessing the image.");
}
```

Le tipiche operazioni di preprocessing includono binarizzazione, riduzione del rumore o ridimensionamento a 300 dpi. Rieseguire l'OCR dopo tale preprocessing spesso aumenta i livelli di confidenza.

## Suggerimenti sulle prestazioni
- **Elaborazione batch:** Aggiungere molte immagini a un unico `OcrInput` riduce l'overhead di inizializzare ripetutamente il contesto GPU.  
- **Warm‑up:** Esegui un riconoscimento fittizio una volta dopo l'avvio della JVM; la prima chiamata subisce la latenza di inizializzazione del driver.  
- **Gestione della memoria:** Disporre dei grandi oggetti `OcrInput` (`ocrInput.clear()`) una volta terminato per liberare la memoria GPU.  

## Conclusione
Ora sai come **estrarre testo da immagine** in modo efficiente con il motore GPU di Aspose OCR in Java, come **impostare l'ID del dispositivo GPU** quando lavori con più schede grafiche e come gestire scenari multilingue. Il codice completo e eseguibile sopra dovrebbe funzionare subito—basta sostituire la tua licenza e i percorsi delle immagini.

Pronto per il passo successivo? Prova a elaborare un'intera cartella di PDF scansionati, sperimenta con diverse opzioni `setLanguage`, o combina l'output OCR con un modello di machine‑learning per il post‑processing. I guadagni di prestazioni grazie all'accelerazione GPU rendono fattibili progetti su larga scala.

Buon coding, e sentiti libero di lasciare un commento se incontri problemi!

## Domande frequenti

**D: Posso usarlo in un'applicazione commerciale?**  
R: Sì—basta installare una licenza valida di Aspose OCR. La versione di prova è solo per valutazione.

**D: La versione GPU funziona sui server Linux?**  
R: Assolutamente; purché il driver NVIDIA e il toolkit CUDA siano installati, la libreria funziona in ambienti Linux headless.

**D: Qual è la dimensione massima dell'immagine supportata?**  
R: Aspose OCR può elaborare immagini fino a **5000 × 5000 px** senza caricare l'intero file in memoria.

**D: Come posso aggiornare all'ultima versione di Aspose OCR?**  
R: Sostituisci il vecchio JAR con quello nuovo e aggiorna il numero di versione della dipendenza Maven/Gradle.

**D: È possibile ottenere le coordinate del riquadro di delimitazione per ogni parola?**  
R: Sì—`OcrResult` fornisce informazioni di layout, incluse le bounding box a livello di parola, quando abiliti l'opzione `setIncludeLayout(true)`.

---

**Ultimo aggiornamento:** 2026-10-30  
**Testato con:** Aspose OCR for Java 24.11  
**Autore:** Aspose

## Tutorial correlati

- [Riconoscere testo da immagine Java OCR con accelerazione GPU](/ocr/java/advanced-ocr-techniques/recognize-text-from-image-java-ocr-with-gpu-acceleration/)
- [Come abilitare GPU per OCR in Java Estrarre testo da immagine](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)
- [Estrarre testo da immagine con Aspose OCR Java Guida rapida](/ocr/java/ocr-basics/extract-text-from-image-with-aspose-ocr-java-quick-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}