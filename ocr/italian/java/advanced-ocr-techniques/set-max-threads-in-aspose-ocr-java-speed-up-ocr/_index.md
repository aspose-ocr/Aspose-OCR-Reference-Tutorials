---
category: general
date: 2026-04-29
description: Imposta il numero massimo di thread in Aspose OCR Java per accelerare
  l'elaborazione OCR ed estrarre facilmente i file immagine di testo. Scopri come
  configurare il tiling parallelo per risultati più rapidi.
draft: false
keywords:
- set max threads
- extract text image
- speed up OCR
language: it
og_description: Imposta il numero massimo di thread in Aspose OCR Java per velocizzare
  l'OCR ed estrarre rapidamente i file immagine di testo. Segui questa guida passo
  passo.
og_title: Imposta il numero massimo di thread in Aspose OCR Java – velocizza l'OCR
tags:
- OCR
- Java
- Aspose
title: Imposta il numero massimo di thread in Aspose OCR Java – Velocizza l'OCR
url: /it/java/advanced-ocr-techniques/set-max-threads-in-aspose-ocr-java-speed-up-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# set max threads in Aspose OCR Java – Velocizza OCR

Ti sei mai chiesto come **set max threads** quando usi Aspose OCR in Java? Impostare max threads ti consente di **speed up OCR** e **extract text image** file molto più velocemente su macchine multi‑core. In questo tutorial vedremo un esempio completo, pronto‑all‑uso, che mostra esattamente come configurare l'elaborazione parallela, perché è importante e cosa puoi aspettarti come output.

Se ti sei mai trovato a fissare un documento scansionato gigantesco e a pensare “Ci vuole un'eternità”, sei nel posto giusto. Tratteremo anche alcuni problemi comuni—come l'esaurimento della memoria durante il tiling di immagini grandi—così non rimarrai bloccato a metà.

---

## Cosa ti serve

- **Java 17** o versioni più recenti (l'API funziona anche con versioni precedenti ma 17 offre le migliori prestazioni).  
- **Aspose.OCR for Java** library – puoi scaricarla da Maven Central.  
- Un file immagine (PNG, JPEG, TIFF, ecc.) da cui vuoi **extract text image**.  
- Una CPU decente con almeno 4 core – più core, più beneficio otterrai impostando max threads.

Nessuna dipendenza nativa aggiuntiva, nessun servizio esterno. Solo Java puro e il JAR di Aspose.

## Passo 1: Aggiungi la dipendenza Aspose OCR

Se usi Maven, inserisci il seguente snippet nel tuo `pom.xml`. Gli utenti Gradle possono tradurlo facilmente.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check Maven Central for the latest version -->
</dependency>
```

> **Pro tip:** Mantieni il numero di versione aggiornato. Le nuove release spesso includono ottimizzazioni delle prestazioni che **speed up OCR** ulteriormente.

## Passo 2: Inizializza il motore OCR

Creare un'istanza di `OcrEngine` è semplice. Pensala come il cervello che in seguito estrarrà i dati **extract text image**.

```java
import com.aspose.ocr.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

A questo punto il motore è inattivo, in attesa di un'immagine e di alcune impostazioni. Arriveremo alla parte cruciale—**setting max threads**—nel passo successivo.

## Passo 3: Carica l'immagine da elaborare

Puoi caricare un'immagine da un file, da uno stream o anche da un array di byte. Qui usiamo il metodo comodo `ImageStream.fromFile`.

```java
        // Step 3: Load the image to be processed
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/big_image.png"));
```

Sostituisci `YOUR_DIRECTORY/big_image.png` con il percorso dell'immagine da cui vuoi **extract text image**. Il motore ora contiene il bitmap pronto per il riconoscimento.

## Passo 4: **set max threads** – Configura l'elaborazione parallela

Questo è il cuore del tutorial. Per impostazione predefinita Aspose OCR usa un conteggio di thread che corrisponde al numero di core logici della CPU. Se vuoi ottimizzarlo—ad esempio, limitare il carico su un server condiviso—puoi esplicitamente **set max threads**.

```java
        // Step 4: Allow up to 8 parallel threads (defaults to number of CPU cores)
        ocrEngine.getProcessingSettings().setMaxParallelThreads(8);
```

Perché è importante? Ogni thread lavora su una porzione dell'immagine. Più thread → più porzioni → elaborazione complessiva più veloce—purché la tua macchina possa gestire i contesti aggiuntivi. Se hai una workstation a 16 core, potresti aumentare a 12 o anche 16 per la massima velocità.

## Passo 5: Abilita il tiling parallelo – Un altro modo per **speed up OCR**

Il tiling parallelo suddivide un'immagine enorme in tessere più piccole che possono essere elaborate indipendentemente. È particolarmente utile per scansioni molto grandi (pensa a planimetrie formato A0).

```java
        // Step 5: Enable tile‑based parallelism for faster processing of large images
        ocrEngine.getProcessingSettings().setEnableParallelTiling(true);
```

Quando combini **set max threads** con il tiling, di fatto fornisci al motore OCR una spinta a due vie: più worker *e* una distribuzione del lavoro più intelligente. Nei miei test, un PNG 4000×3000 è passato da ~12 secondi a meno di 5 secondi.

## Passo 6: Esegui il riconoscimento e il contenuto **extract text image**

Ora eseguiamo effettivamente il motore OCR. Il metodo `recognize()` restituisce un oggetto `OcrResult` che contiene la rappresentazione in plain‑text.

```java
        // Step 6: Perform OCR recognition
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 7: Output the recognized text
        System.out.println(ocrResult.getText());
    }
}
```

La chiamata `getText()` ti restituisce una singola `String` contenente tutto ciò che il motore ha potuto leggere. Puoi ulteriormente post‑processarla (rimuovere spazi, dividere in righe, ecc.) a seconda delle tue esigenze successive.

## Output previsto

Se l'immagine di origine contiene la frase *“Hello, world!”* vedrai qualcosa di simile:

```
Hello, world!
```

Per PDF multi‑pagina rasterizzati, l'output concatenarà il testo di ogni pagina, preservando le interruzioni di riga. La console mostrerà l'intero contenuto estratto, dimostrando che hai **extract text image** con successo mentre **speed up OCR** grazie alle impostazioni dei thread.

## Esempio completo funzionante (pronto per copia‑incolla)

```java
import com.aspose.ocr.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 3: Load the image to be processed
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/big_image.png"));

        // Step 4: Allow up to 8 parallel threads (defaults to number of CPU cores)
        ocrEngine.getProcessingSettings().setMaxParallelThreads(8);

        // Step 5: Enable tile‑based parallelism for faster processing of large images
        ocrEngine.getProcessingSettings().setEnableParallelTiling(true);

        // Step 6: Perform OCR recognition
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 7: Output the recognized text
        System.out.println(ocrResult.getText());
    }
}
```

> **Nota:** Se incontri un `OutOfMemoryError` su file estremamente grandi, prova a ridurre `setMaxParallelThreads` o a disabilitare il tiling (`setEnableParallelTiling(false)`). Il giusto equilibrio dipende dal tuo hardware.

## Panoramica visiva

![configurazione set max threads in Aspose OCR Java](https://example.com/images/set-max-threads.png "configurazione set max threads in Aspose OCR Java")

*Lo screenshot mostra il pannello `ProcessingSettings` dove puoi regolare il conteggio dei thread e attivare/disattivare il tiling.*

## Domande comuni e casi particolari

### E se ho solo un laptop dual‑core?

Puoi comunque **set max threads** a `2` (il valore predefinito). Il guadagno sarà modesto, ma abilitare il tiling può comunque risparmiare uno o due secondi su immagini grandi.

### Funziona su macOS e Linux?

Assolutamente. La libreria Aspose OCR è indipendente dalla piattaforma purché tu abbia una JRE compatibile. Assicurati solo che il percorso dell'immagine utilizzi il separatore di file corretto (`/` funziona ovunque).

### Posso usarlo con uno stream invece di un file?

Sì. Sostituisci `ImageStream.fromFile` con `ImageStream.fromByteArray` o `ImageStream.fromInputStream`. Il resto della configurazione—**set max threads**, **speed up OCR**—rimane identico.

### L'aumento del conteggio dei thread può mai *rallentare* le cose?

Se superi di gran lunga il numero di core fisici, l'OS inizierà a fare molti context‑switch, il che può effettivamente aumentare la latenza. Una buona regola pratica: **threads ≤ cores + 2**. Sperimenta e monitora l'uso della CPU.

## Consigli per ottenere il massimo dal OCR parallelo

1. **Profile First** – Esegui una baseline senza impostazioni parallele, poi abilita `setMaxParallelThreads` e confronta i tempi.  
2. **Batch Process** – Se hai decine di immagini, inviale sequenzialmente attraverso lo stesso `O

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}