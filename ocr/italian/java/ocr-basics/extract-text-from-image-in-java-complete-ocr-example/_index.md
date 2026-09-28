---
category: general
date: 2026-01-12
description: Estrai il testo da un'immagine usando Aspose OCR in Java. Scopri come
  estrarre il testo da un'immagine di una fattura con un esempio di OCR in Java e
  ottieni il testo OCR risultante.
draft: false
keywords:
- extract text from image
- how to extract text
- java ocr example
- process invoice image
- output ocr text
language: it
og_description: Estrai testo da un'immagine usando Aspose OCR in Java. Questa guida
  mostra come estrarre testo da un'immagine di fattura, include un esempio di OCR
  in Java e restituisce il testo OCR.
og_title: Estrai testo da immagine in Java – Esempio completo di OCR
tags:
- OCR
- Java
- Aspose
title: Estrai testo da un'immagine in Java – Esempio completo di OCR
url: /it/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrai testo da immagine in Java – Esempio OCR completo

Ti sei mai chiesto come **estrarre testo da immagine** senza impazzire? Forse hai una pila di fatture scannerizzate e hai bisogno dei numeri rapidamente. Nella mia esperienza, il modo più semplice è lasciare che una libreria OCR dedicata faccia il lavoro pesante. Questo tutorial mostra *come estrarre testo* da una tipica immagine di fattura usando Aspose OCR per Java, e dimostra anche un **java ocr example** che restituisce il testo OCR che puoi inviare al tuo sistema a valle.

Passeremo in rassegna tutto ciò che devi sapere: dalla configurazione del progetto, alla definizione della regione di interesse (ROI) che si concentra sull'intestazione e sull'importo totale, fino alla stampa del testo estratto. Alla fine, sarai in grado di **process invoice image** file automaticamente e recuperare testo pulito e ricercabile.

> **Cosa otterrai:** un programma Java pronto‑all'uso, spiegazioni chiare di ogni passaggio e consigli pratici per gestire fatture reali.

---

## Prerequisiti

- Java Development Kit (JDK) 8 o versioni successive installato.
- Maven o Gradle per la gestione delle dipendenze (mostrato esempio Maven).
- Una licenza Aspose OCR per Java (la versione di prova gratuita funziona per i test).
- Un'immagine di fattura (`invoice.png`) posizionata in una directory nota.

Se qualcuno di questi ti è sconosciuto, non preoccuparti: la maggior parte è a un click di download, e il codice si compila comunque con l'edizione community.

---

## Passo 1: Configura il tuo progetto Maven

Per prima cosa, crea un nuovo progetto Maven (o aggiungine uno esistente). Nel tuo `pom.xml`, aggiungi la dipendenza Aspose OCR:

```xml
<!-- pom.xml -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.9</version> <!-- Use the latest version available -->
    </dependency>
</dependencies>
```

> **Pro tip:** Mantieni il numero di versione aggiornato; le versioni più recenti spesso migliorano l'accuratezza per i caratteri difficili presenti nelle fatture.

Dopo aver salvato il file, esegui `mvn clean install` per scaricare la libreria nel tuo repository locale.

---

## Passo 2: Carica l'immagine della fattura

Ora che la libreria è pronta, scriviamo una piccola classe Java. La prima cosa che facciamo è creare un'istanza `OcrEngine` e puntarla all'immagine che vuoi leggere.

```java
import com.aspose.ocr.*;

public class RoiExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage("YOUR_DIRECTORY/invoice.png"); // <-- replace with your path
```

Perché creiamo il motore **prima** di caricare l'immagine? Il motore contiene configurazioni come lingua, DPI e ROI. Impostare l'immagine in anticipo garantisce che tali impostazioni si applichino al file esatto che stai per elaborare.

---

## Passo 3: Definisci le regioni di interesse (ROI)

Le fatture spesso contengono molto rumore—tabelle, loghi e stampe piccole. Limitando l'OCR solo all'intestazione e all'importo totale, aumenti notevolmente sia la velocità che l'accuratezza. Aspose ti permette di descrivere queste zone con rettangoli.

```java
        // Step 3: Define the regions of interest (header and total amount)
        OcrRegion region = OcrRegion.builder()
                .addRectangle(0, 0, 800, 150)      // header area
                .addRectangle(0, 1200, 800, 200)   // total amount area
                .build();

        // Apply ROI to the engine
        engine.setRegion(region);
```

Le coordinate sono in pixel (`x`, `y`, `width`, `height`). Se le tue fatture variano in dimensione, puoi calcolare questi valori in modo dinamico—magari controllando prima le dimensioni dell'immagine. È una buona estensione se ti serve una soluzione **process invoice image** che funzioni su lotti.

---

## Passo 4: Esegui l'OCR sulle regioni specificate

Con la ROI impostata, il motore OCR può concentrare la sua attenzione dove conta di più. Il metodo `recognize()` restituisce un `OcrResult` contenente il testo estratto.

```java
        // Step 4: Run OCR on the specified regions
        OcrResult result = engine.recognize();
```

Dietro le quinte, Aspose esegue diversi passaggi di pre‑elaborazione: binarizzazione, rimozione del rumore e segmentazione dei caratteri. Non devi chiamarli manualmente—basta lasciare che `recognize()` faccia il suo lavoro.

---

## Passo 5: Output del testo estratto

Infine, stampiamo il testo sulla console. In un'applicazione reale potresti salvarlo in un database, inviarlo a una pipeline di analisi a valle, o persino generare un PDF ricercabile.

```java
        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(result.getText());
    }
}
```

Quando esegui il programma, dovresti vedere qualcosa del genere:

```
ROI text:
Acme Corp.
Invoice #12345
Date: 2025-12-31
Total Amount: $1,250.00
```

Se l'output appare confuso, ricontrolla le coordinate del rettangolo o aumenta la risoluzione dell'immagine. I motori OCR amano scansioni nitide ad alta DPI.

---

## Esempio completo funzionante

Di seguito trovi il file Java completo e autonomo che puoi copiare‑incollare in `src/main/java/RoiExample.java`. Non servono snippet esterni—tutto ciò di cui hai bisogno è qui.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.region.*;

public class RoiExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage("YOUR_DIRECTORY/invoice.png");

        // Step 2: Define the regions of interest (header and total amount)
        OcrRegion region = OcrRegion.builder()
                .addRectangle(0, 0, 800, 150)      // header area
                .addRectangle(0, 1200, 800, 200)   // total amount area
                .build();

        // Step 3: Apply the ROI configuration to the engine
        engine.setRegion(region);

        // Step 4: Run OCR on the specified regions
        OcrResult result = engine.recognize();

        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(result.getText());
    }
}
```

> **Nota:** Sostituisci `YOUR_DIRECTORY` con il percorso assoluto della tua immagine di fattura. Se usi un percorso relativo, assicurati che la directory di lavoro corrisponda a dove esegui il comando `java`.

---

## Domande comuni e casi limite

### Cosa succede se la dimensione della fattura cambia?

Puoi calcolare la ROI in modo dinamico:

```java
int imgWidth = engine.getImage().getWidth();
int imgHeight = engine.getImage().getHeight();

int headerHeight = imgHeight / 10;
int totalHeight = imgHeight / 8;

OcrRegion region = OcrRegion.builder()
        .addRectangle(0, 0, imgWidth, headerHeight)
        .addRectangle(0, imgHeight - totalHeight, imgWidth, totalHeight)
        .build();
```

### Come gestire più lingue?

Aspose OCR supporta pacchetti linguistici. Basta impostare la lingua prima di chiamare `recognize()`:

```java
engine.setLanguage(OcrLanguage.Spanish); // or OcrLanguage.English, etc.
```

### Cosa fare se l'OCR restituisce stringhe vuote?

Tipici colpevoli sono:

- Bassa risoluzione dell'immagine (< 300 DPI). Ingrandisci o richiedi scansioni di qualità superiore.
- Sfondi eccessivamente scuri o chiari. Applica un semplice filtro di miglioramento del contrasto prima dell'OCR.
- Coordinate ROI errate che non includono il testo.

---

## Consigli per un OCR pronto per la produzione

1. **Batch Processing:** Avvolgi la logica in un ciclo che itera su una directory di file di fattura. Registra ogni risultato per l'auditabilità.
2. **Error Handling:** Cattura `OcrException` per saltare elegantemente le immagini corrotte senza interrompere l'intero lavoro.
3. **Performance:** Riutilizza una singola istanza `OcrEngine` per più immagini; creare un nuovo motore per ogni file aggiunge overhead inutile.
4. **Validation:** Dopo l'estrazione, esegui un controllo regex sull'importo totale (`\$\d{1,3}(,\d{3})*(\.\d{2})?`) per assicurarti che il numero sia realistico.

Implementare questi suggerimenti trasforma un semplice **java ocr example** in una soluzione robusta e scalabile per qualsiasi azienda che deve **process invoice image** file ogni notte.

---

## Conclusione

Abbiamo appena coperto come **estrarre testo da immagine** file in Java usando Aspose OCR, concentrandoci su uno scenario pratico di elaborazione delle fatture. Definendo una regione di interesse, eseguendo il motore OCR e stampando il **output OCR text**, ora hai una solida base per costruire pipeline di acquisizione dati automatizzate.

Prossimi passi? Prova ad ampliare la ROI per includere le tabelle delle righe, sperimenta con impostazioni linguistiche diverse, o invia le stringhe estratte a una libreria di generazione PDF per documenti ricercabili. Il cielo è il limite quando combini OCR con gli strumenti Java moderni.

Hai altre domande su **come estrarre testo** da altri tipi di documento, o hai bisogno di aiuto per regolare la ROI per layout insoliti? Lascia un commento qui sotto—buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}