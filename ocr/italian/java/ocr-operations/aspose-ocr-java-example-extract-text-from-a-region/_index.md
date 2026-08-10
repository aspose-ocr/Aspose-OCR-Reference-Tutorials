---
category: general
date: 2026-05-03
description: L'esempio Aspose OCR Java mostra come caricare un'immagine per l'OCR
  ed estrarre il testo da una regione in poche righe di codice.
draft: false
keywords:
- aspose ocr java example
- load image for OCR
- extract text from region
language: it
og_description: L'esempio Aspose OCR Java dimostra il caricamento di un'immagine per
  OCR e l'estrazione del testo da una regione specifica, perfetto per l'elaborazione
  delle fatture.
og_title: Esempio OCR Java di Aspose – Estrazione del testo da una regione
tags:
- Aspose OCR
- Java
- Image Processing
title: 'Esempio Aspose OCR Java: Estrarre il testo da una regione'
url: /it/java/ocr-operations/aspose-ocr-java-example-extract-text-from-a-region/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esempio Aspose OCR Java: Estrarre Testo da una Regione

Cerchi un **esempio Aspose OCR Java** che ti permetta di estrarre solo la parte di cui hai bisogno da un'immagine? In questa guida vedremo **come caricare un'immagine per l'OCR** e **come estrarre il testo da una regione**, perfetto per numeri di fattura, campi di modulo o qualsiasi dato nascosto all'interno di un'immagine più grande.

Ti starai chiedendo perché limitare l'OCR a un rettangolo invece di scansionare l'intera pagina. La risposta breve: velocità e precisione. Quando il motore analizza solo una porzione definita, ignora il rumore irrilevante, è più veloce e spesso produce risultati più puliti. Alla fine di questo tutorial avrai un programma Java autonomo che fa esattamente questo, insieme a una serie di consigli per evitare le insidie più comuni che ostacolano i principianti.

## Cosa Ti Serve

Prima di iniziare, assicurati di avere:

- **Java Development Kit (JDK) 11** o versioni successive installate.  
- Libreria **Aspose.OCR for Java** (puoi scaricare l'ultimo JAR dal repository Maven Central o dal portale di download Aspose).  
- Un file immagine che contenga il testo da leggere – per la demo useremo `invoice.png`, che contiene un numero di fattura vicino all'angolo in alto a destra.  
- Un IDE preferito o un semplice editor di testo più un terminale; qualsiasi strumento di build (Maven, Gradle o plain `javac`) andrà bene.

Tutto qui. Nessun motore OCR aggiuntivo, nessun binario nativo, solo Java puro e Aspose.

![Screenshot dell'esempio Aspose OCR Java](/images/aspose-ocr-java-example.png "Esempio Aspose OCR Java che mostra l'estrazione della regione")

## Esempio Aspose OCR Java – Inizializzare il Motore OCR

La prima cosa di cui ha bisogno qualsiasi flusso di lavoro OCR è un'istanza del motore. Aspose fornisce una classe leggera `OcrEngine` che gestisce tutto, dal caricamento dell'immagine alla selezione della lingua.

```java
import com.aspose.ocr.*;

public class RegionOcrExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

**Perché è importante:** Creare il motore in anticipo ti fornisce un oggetto pulito da configurare. Puoi riutilizzare lo stesso `OcrEngine` per più immagini se stai elaborando un batch, risparmiando memoria e tempo di inizializzazione.

## Caricare l'Immagine per l'OCR

Ora indichiamo al motore quale immagine scansionare. Aspose fornisce l'helper `ImageStream.fromFile`, che astrae il boilerplate a basso livello di `FileInputStream`.

```java
        // Step 2: Load the image that contains the invoice
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));
```

**Suggerimento:** Sostituisci `YOUR_DIRECTORY` con un percorso assoluto o relativo che punti alla cartella dove hai salvato `invoice.png`. Se il file non viene trovato, Aspose lancia un `IOException`, quindi potresti voler avvolgere questo codice in un blocco try‑catch per il codice di produzione.

## Definire ed Estrarre il Testo da una Regione

Ora arriva la parte centrale: il rettangolo che indica al motore dove guardare. Il costruttore `java.awt.Rectangle` accetta `(x, y, width, height)` – tutti misurati in pixel.

```java
        // Step 3: Define the region where the invoice number is located (x, y, width, height)
        java.awt.Rectangle invoiceRegion = new java.awt.Rectangle(120, 250, 300, 80);
        ocrEngine.setRegion(invoiceRegion);   // restrict recognition to this area
```

**Come funziona:** Chiamando `setRegion`, limiti la scansione OCR a una striscia larga 300 pixel che inizia a 120 pixel dal bordo sinistro e a 250 pixel dall'alto. Regola questi numeri in base al tuo layout; un modo rapido per trovarli è aprire l'immagine in un editor grafico che mostri le coordinate dei pixel.

## Abilitare la Lingua ed Eseguire il Riconoscimento

Aspose OCR supporta decine di lingue, ma per un numero di fattura ci serve solo l'inglese. Abilitare la lingua corretta riduce drasticamente i falsi positivi.

```java
        // Step 4: Enable English language for recognition
        ocrEngine.getLanguage().setEnglish(true);

        // Step 5: Perform recognition and output the extracted text
        if (ocrEngine.recognize()) {
            System.out.println("Extracted region text: " + ocrEngine.getText());
        } else {
            System.err.println("OCR recognition failed.");
        }
    }
}
```

**Perché abilitare solo l'inglese?** Il motore OCR proverà a far corrispondere i caratteri di tutti i set linguistici abilitati, il che può confonderlo quando il testo è semplicemente alfanumerico. Limitare l'ambito linguistico migliora sia la velocità sia la precisione.

### Output Atteso

Quando tutto è configurato correttamente, vedrai qualcosa di simile:

```
Extracted region text: INV-12345
```

Se il rettangolo è spostato di qualche pixel, l'output potrebbe risultare confuso o vuoto. È un controllo di sanità semplice: esegui il programma, guarda la console e verifica che il testo corrisponda a quello visibile nell'immagine.

## Eseguire il Codice e Verificare l'Output

Supponendo che tu stia usando Maven, aggiungi la dipendenza Aspose OCR al tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Use the latest version available -->
</dependency>
```

Compila ed esegui:

```bash
mvn compile exec:java -Dexec.mainClass=RegionOcrExample
```

Oppure, se preferisci usare plain `javac`:

```bash
javac -cp "aspose-ocr-23.10.jar" RegionOcrExample.java
java -cp ".:aspose-ocr-23.10.jar" RegionOcrExample
```

Dovresti vedere la riga **Extracted region text** stampata sulla console. Se ottieni “OCR recognition failed”, ricontrolla il percorso del file e assicurati che la regione contenga effettivamente caratteri leggibili.

## Casi Limite & Varianti Comuni

| Situazione | Cosa Cambiare |
|-----------|----------------|
| **Più lingue** (es. Inglese + Spagnolo) | Chiama `ocrEngine.getLanguage().setSpanish(true);` insieme all'inglese. |
| **Regione fuori dai limiti dell'immagine** | Aspose taglierà silenziosamente il rettangolo, ma perderai dati. Usa `ImageInfo` (`ocrEngine.getImage().getWidth()`) per verificare le dimensioni prima di impostare la regione. |
| **Fatture dinamiche** (layout diversi) | Considera di eseguire una pre‑scansione leggera sull'intera immagine per individuare parole chiave come “Invoice #” e poi calcolare programmaticamente il rettangolo. |
| **Immagini ad alta DPI** | Incrementa `ocrEngine.getImage().setResolution(300);` per una maggiore precisione su documenti scansionati. |
| **Ottimizzazione delle prestazioni** | Disabilita le lingue non necessarie, mantieni la regione il più piccola possibile e riutilizza una singola istanza di `OcrEngine` per molti file. |

## Pro Tips Dal Campo

- **Pro tip:** Se ti servono solo cifre (comune per i numeri di fattura), abilita la modalità numerica con `ocrEngine.getLanguage().setDigits(true);`. Questo elimina il rumore alfabetico.  
- **Attenzione a:** PNG trasparenti. Aspose a volte interpreta male il canale alfa; convertire l'immagine in un JPEG con sfondo solido può risolvere output bianchi anomali.  
- **Ricorda:** Il rettangolo utilizza il sistema di coordinate native dell'immagine, non quello di eventuali scaling UI che potresti vedere sullo schermo. Testa sempre con il file esatto che utilizzerai in produzione.

## E Dopo?

Ora che hai un solido **esempio Aspose OCR Java** per l'estrazione basata su regione, puoi estenderlo in diverse direzioni utili:

- **Elaborazione batch:** Scorri una cartella di fatture, riutilizzando lo stesso `OcrEngine` per migliorare il throughput.  
- **Validazione dati:** Invia il testo estratto a una regex come `INV-\\d{5}` per assicurarti di aver catturato un numero di fattura valido.  
- **Integrazione con PDF:** Usa Aspose.PDF per sovrapporre il testo estratto al documento originale a fini di tracciamento.  
- **Distribuzione cloud:** Avvolgi il codice in un servizio REST leggero (Spring Boot) così altri sistemi possono chiamarlo on demand.  

Ognuno di questi passaggi utilizza gli stessi concetti di base—**caricare l'immagine per l'OCR**, **estrarre il testo da una regione** e gestire i risultati—quindi la transizione sarà indolore.

---

*Buona programmazione! Se incontri difficoltà, lascia un commento qui sotto o visita i forum Aspose dove la community condivide aggiustamenti pratici per layout complessi.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}