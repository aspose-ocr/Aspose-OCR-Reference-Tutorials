---
category: general
date: 2026-04-26
description: Impara a riconoscere il testo da un'immagine usando Aspose OCR con accelerazione
  GPU in Java. Include impostare il limite di memoria GPU e caricare l'immagine per
  i passaggi OCR.
draft: false
keywords:
- recognize text from image
- set gpu memory limit
- load image for ocr
- Aspose OCR Java
- GPU acceleration OCR
language: it
og_description: Scopri come riconoscere rapidamente il testo da un'immagine usando
  l'OCR Aspose accelerato da GPU in Java. Guida passo passo con impostazione del limite
  di memoria GPU e caricamento dell'immagine per l'OCR.
og_title: Riconosci il testo da un'immagine con GPU Aspose OCR (Java)
tags:
- OCR
- Java
- GPU
- Aspose
title: Riconoscere il testo da un'immagine con GPU Aspose OCR (Java)
url: /it/java/advanced-ocr-techniques/recognize-text-from-image-with-gpu-aspose-ocr-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Riconoscere testo da immagine con GPU Aspose OCR (Java)

Hai mai avuto bisogno di **recognize text from image** rapidamente su un backend Java? Con l'accelerazione GPU di Aspose OCR puoi risparmiare secondi su ogni scansione—niente più attese mentre la CPU elabora megabyte di pixel. In questo tutorial vedremo come attivare la GPU, opzionalmente **set GPU memory limit**, e infine **load image for OCR** così otterrai una stringa di testo pulita in poche righe di codice.

Copriamo tutto ciò di cui hai bisogno per eseguire la demo su una scheda abilitata CUDA, spieghiamo perché ogni impostazione è importante e ti mostriamo un esempio completo, pronto‑da‑eseguire. Alla fine sarai in grado di inserire OCR accelerato da GPU in qualsiasi servizio Java, sia esso una pipeline di ingestione documenti o un backend mobile in tempo reale.

## Cosa ti serve

- **Java 17** o versioni più recenti (l'Aspose OCR JAR è destinato a JVM moderne)  
- Una **CUDA‑compatible GPU** con almeno 2 GB di VRAM (la demo limita l'uso a 1024 MB)  
- Libreria **Aspose.OCR for Java** (scarica dal sito Aspose o ottieni da Maven)  
- Un file immagine da elaborare – preferibilmente una scansione o foto ad alta risoluzione  

Nessun servizio esterno, nessuna chiave cloud, solo un'installazione locale. Se non hai ancora una GPU, puoi comunque eseguire il codice; la chiamata `setUseGpu(true)` tornerà automaticamente alla CPU.

## Passo 1: Aggiungi Aspose OCR al tuo progetto e recognize text from image

Per prima cosa, assicurati che il JAR di Aspose OCR sia nel tuo classpath. Se usi Maven, aggiungi:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check for the latest version -->
</dependency>
```

Una volta che la libreria è disponibile, crea un'istanza di `OcrEngine`. Questo oggetto è il punto di ingresso per le operazioni di **recognize text from image**.

```java
// Step 1: Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

Perché istanziamo prima `OcrEngine`? Contiene tutte le impostazioni di riconoscimento (flag GPU, pacchetti lingua, ecc.) e isola ogni scansione, così puoi riutilizzare in sicurezza lo stesso engine per più immagini senza perdite di memoria.

## Passo 2: Abilita l'accelerazione GPU e opzionalmente **set GPU memory limit**

L'accelerazione GPU è il segreto che rende fattibile l'OCR su larga scala. Aspose ti permette di attivarla con una singola chiamata:

```java
// Step 2: Turn on GPU acceleration (requires a CUDA‑enabled GPU)
ocrEngine.getRecognitionSettings().setUseGpu(true);
```

Se la tua GPU è condivisa con altri carichi di lavoro, potresti voler limitare quanta VRAM può prendere l'engine. È qui che entra in gioco **set GPU memory limit**:

```java
// Optional: Limit the amount of GPU memory the engine may use (in MB)
ocrEngine.getRecognitionSettings().setGpuMemoryLimit(1024);
```

Impostare un limite di memoria previene crash per out‑of‑memory quando si elaborano molte immagini ad alta risoluzione in parallelo. Il valore è in megabyte, quindi `1024` significa “usa al massimo 1 GB di VRAM”.

> **Consiglio professionale:** Su una scheda da 4 GB, un limite di 2 GB è solitamente un punto ottimale; puoi sperimentare valori più alti se noti che la GPU resta inattiva.

## Passo 3: **Load image for OCR** – indica al motore il tuo file

Ora che il motore è pronto, dobbiamo dirgli quale immagine scansionare. Aspose accetta un percorso file, un `java.io.File`, o anche un `java.awt.image.BufferedImage`. Per semplicità useremo un percorso:

```java
// Step 3: Load the high‑resolution image to be processed
ocrEngine.setImage("YOUR_DIRECTORY/high_res_photo.jpg");
```

Sostituisci `YOUR_DIRECTORY/high_res_photo.jpg` con la posizione reale della tua immagine di test. Se l'immagine è nella cartella resources, puoi usare `getClass().getResource("/images/sample.png").getPath()` al suo posto.

Perché il caricamento è importante? Il motore esegue una fase di pre‑processing (deskew, binarizzazione) fortemente dipendente dalla GPU. Fornire un file pulito e ad alta risoluzione permette alla GPU di lavorare in modo efficiente e migliora la precisione del **recognize text from image**.

## Passo 4: Esegui il riconoscimento e recupera la stringa estratta

Con la GPU attivata e l'immagine caricata, la chiamata finale è semplice:

```java
// Step 4: Run the recognition and retrieve the extracted text
String extractedText = ocrEngine.recognize().getText();
```

Il metodo `recognize()` blocca l'esecuzione finché la GPU non termina, poi `getText()` restituisce una semplice `String`. Internamente Aspose utilizza un modello di deep‑learning che gira sui core CUDA, quindi la latenza è tipicamente una frazione di quella necessaria per un OCR solo CPU.

## Passo 5: Stampa il risultato

Stampiamo l'output OCR sulla console così puoi verificare che abbia funzionato:

```java
// Step 5: Output the GPU‑accelerated OCR result
System.out.println("GPU‑accelerated result:\n" + extractedText);
```

Se tutto è collegato correttamente vedrai il testo trascritto apparire istantaneamente. Su una modesta RTX 2060, un'immagine 3000 × 2000 px viene elaborata in meno di un secondo.

![riconoscere testo da immagine usando GPU Aspose OCR](/images/gpu-ocr-demo.png "Demo OCR accelerato da GPU")

*Testo alternativo dell'immagine:* **recognize text from image** – screenshot dell'output della console dopo GPU OCR.

## Output previsto

Eseguendo il programma completo su una ricevuta di esempio si ottiene qualcosa di simile:

```
GPU‑accelerated result:
Item      Qty   Price
Apple      2    $1.20
Banana     5    $0.75
Total          $3.75
```

Il tuo testo reale differirà in base all'immagine di origine, ma il formato sopra dimostra che l'engine estrae correttamente interruzioni di riga e numeri.

## Problemi comuni & consigli pratici

| Problema | Perché accade | Come risolverlo |
|-------|----------------|---------------|
| **GPU not detected** | Driver CUDA mancante o versione JAR incompatibile | Installa l'ultimo driver NVIDIA, verifica che `nvidia-smi` funzioni, e usa Aspose OCR 23.12 o più recente |
| **Out‑of‑memory error** | Immagine troppo grande per la VRAM limitata | Aumenta `setGpuMemoryLimit` o ridimensiona l'immagine prima del caricamento |
| **Garbage characters** | Immagine sfocata o a basso contrasto | Pre‑processa con `ocrEngine.getPreprocessingSettings().setBinarization(true)` |
| **Slow performance on first run** | Overhead di inizializzazione del contesto GPU | Riscalda l'engine processando una piccola immagine fittizia prima del carico reale |

Ricorda, **set gpu memory limit** è opzionale ma

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}