---
category: general
date: 2026-02-14
description: Estrai il testo dall'immagine usando Aspose OCR in Java. Scopri come
  estrarre il testo dai campi del modulo con regioni di interesse per risultati precisi.
draft: false
keywords:
- extract text from image
- extract text from form
language: it
og_description: Estrai il testo da un'immagine usando Aspose OCR in Java. Questo tutorial
  mostra come estrarre il testo dai campi del modulo tramite regioni di interesse.
og_title: Estrai testo da immagine con Aspose OCR – Guida Java
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Estrai testo da immagine con Aspose OCR – Guida Java
url: /it/java/advanced-ocr-techniques/extract-text-from-image-with-aspose-ocr-java-guide/
---

da immagine". So bold will be **estrarre testo da immagine**.

Similarly later "extract text from form" etc.

Proceed.

Let's craft translation.

Also note "RTL formatting" not needed.

Let's produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrarre testo da immagine con Aspose OCR – Guida Java

Ti è mai capitato di **estrarre testo da immagine** ma di finire per analizzare l’intera foto, sprecando cicli CPU e ottenendo risultati rumorosi? Non sei l’unico. In molte applicazioni reali — pensiamo a scanner di fatture, lettori di passaporti o moduli di inserimento dati — ti interessano solo pochi campi, non l’intera tela.

La buona notizia è che Aspose OCR ti consente di **estrarre testo da immagine** *e* da aree specifiche del modulo definendo dei poligoni. In questo tutorial vedrai esattamente come **estrarre testo da campi di modulo** usando Java, perché l’approccio è importante e cosa regolare quando le cose non vanno come previsto.

Di seguito copriremo tutto, dalla configurazione della libreria alla gestione di casi limite complessi, così alla fine avrai uno snippet pronto all’uso che estrae solo i dati di cui hai bisogno.

## Cosa ti serve

- Java 17 (o qualsiasi JDK recente) – le versioni più nuove hanno un migliore supporto Unicode.  
- Aspose.OCR per Java 23.10 (o l’ultima versione disponibile al momento della lettura).  
- Un’immagine di esempio chiamata `form.png` contenente campi ben definiti.  
- Un IDE o un semplice editor di testo — IntelliJ IDEA, VS Code o anche Notepad vanno bene.

Non è necessario alcun wizard Maven/Gradle per la demo principale; basta aggiungere il JAR di Aspose OCR al classpath.

---

## Passo 1 – Inizializzare il motore OCR e caricare l’immagine

La prima cosa di cui il motore ha bisogno è una bitmap su cui lavorare. Lo punteremo a `form.png`, che si trova nella stessa cartella del file sorgente.

```java
import com.aspose.ocr.*;
import java.awt.Polygon;
import java.util.*;

public class MultiRoiDemo {
    public static void main(String[] args) throws Exception {

        // Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the source image – replace the path if your file lives elsewhere
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.png"));
```

*Perché è importante:*  
Creare un nuovo `OcrEngine` ti garantisce una base pulita, evitando che impostazioni residue influenzino l’esecuzione. Caricare l’immagine subito verifica anche che il file esista, così ottieni un’eccezione utile prima di perdere tempo nei passaggi successivi.

> **Consiglio professionale:** Se la tua immagine è molto grande (oltre 5 MB), considera di ridimensionarla prima. Aspose OCR è più veloce su immagini inferiori a 2000 px in entrambe le dimensioni.

---

## Passo 2 – Definire i poligoni per i campi da leggere

Una *Region of Interest* (ROI) è semplicemente un poligono che indica al motore dove guardare. Qui creiamo due rettangoli — uno per “First Name” e un altro per “Date of Birth”. Regola le coordinate in base al tuo modulo.

```java
        // Polygon for the first field (e.g., First Name)
        Polygon firstField = new Polygon(
                new int[]{50, 200, 200, 50},   // X‑coordinates
                new int[]{100, 100, 150, 150}, // Y‑coordinates
                4);

        // Polygon for the second field (e.g., Date of Birth)
        Polygon secondField = new Polygon(
                new int[]{300, 500, 500, 300},
                new int[]{200, 200, 250, 250},
                4);
```

*Perché usare i poligoni invece dei rettangoli?*  
I poligoni ti danno la flessibilità di gestire caselle inclinate o non rettangolari — comune quando si scansionano moduli stampati che non sono perfettamente allineati.

---

## Passo 3 – Dire ad Aspose OCR di concentrarsi solo su quelle regioni

Ora associamo i poligoni al motore. Il metodo `setRegionsOfInterest` accetta una lista, così puoi aggiungere tutti i campi che desideri.

```java
        // Limit OCR to the defined regions
        ocrEngine.getEngineOptions()
                 .setRegionsOfInterest(Arrays.asList(firstField, secondField));
```

*Cosa succede dietro le quinte?*  
Aspose OCR ritaglia ogni poligono in una bitmap separata, esegue l’algoritmo di riconoscimento e poi unisce i risultati. Questo riduce drasticamente i falsi positivi provenienti da grafiche circostanti.

---

## Passo 4 – Eseguire il processo OCR

Con tutto configurato, avviamo l’OCR. La chiamata `process()` restituisce un oggetto `OcrResult` che contiene il testo estratto e i punteggi di confidenza.

```java
        // Execute OCR on the selected ROIs
        OcrResult ocrResult = ocrEngine.process();
```

Se ti serve la confidenza per campo, puoi ispezionare `ocrResult.getRegions()` — ogni regione porta il proprio punteggio. Per la maggior parte dei moduli semplici, il testo complessivo è sufficiente.

---

## Passo 5 – Visualizzare (o memorizzare) il testo estratto

Infine, stampiamo il risultato sulla console. In un’applicazione reale potresti scriverlo su un database, su un file JSON o inviarlo tramite API.

```java
        // Output the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**Output previsto (esempio):**

```
=== Extracted Text ===
John Doe
12/04/1990
```

Le due righe corrispondono ai due poligoni definiti. Se vedi spazi bianchi extra, rimuovili con `String.trim()`.

---

## Come estrarre testo da modulo quando hai molti campi

Quando un modulo contiene decine di input, digitare manualmente le coordinate diventa tedioso. Ecco un pattern rapido da adottare:

1. **Crea un CSV** dove ogni riga contiene `fieldName, x1, y1, x2, y2, x3, y3, x4, y4`.  
2. **Carica il CSV** a runtime, itera su ogni riga, costruisci un `Polygon` e aggiungilo alla lista ROI.  

```java
List<Polygon> rois = new ArrayList<>();
try (BufferedReader br = new BufferedReader(new FileReader("fields.csv"))) {
    String line;
    while ((line = br.readLine()) != null) {
        String[] parts = line.split(",");
        int[] xs = { Integer.parseInt(parts[1]), Integer.parseInt(parts[3]),
                    Integer.parseInt(parts[5]), Integer.parseInt(parts[7]) };
        int[] ys = { Integer.parseInt(parts[2]), Integer.parseInt(parts[4]),
                    Integer.parseInt(parts[6]), Integer.parseInt(parts[8]) };
        rois.add(new Polygon(xs, ys, 4));
    }
}
ocrEngine.getEngineOptions().setRegionsOfInterest(rois);
```

*Perché farlo?*  
Automatizzare la generazione delle ROI ti permette di riutilizzare lo stesso codice Java su più layout di modulo, mantenendo il progetto DRY (Don’t Repeat Yourself).

---

## Casi limite e consigli a cui potresti non aver pensato

- **Scansioni ruotate:** Se l’intera immagine è ruotata, chiama `ocrEngine.getEngineOptions().setRotateAngle(degrees)`.  
- **Basso contrasto:** Imposta `ocrEngine.getEngineOptions().setContrast(1.5f)` per migliorare la leggibilità.  
- **Script non latini:** Cambia la lingua con `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.Spanish)` (o qualsiasi lingua supportata).  
- **Fallimenti OCR parziali:** Controlla sempre `ocrResult.getConfidence()`; se scende sotto l’80 %, considera di chiedere una verifica manuale all’utente.  

---

## Esempio completo funzionante (pronto per il copy‑paste)

Di seguito trovi il programma completo, pronto per essere compilato ed eseguito. Sostituisci `YOUR_DIRECTORY` con la cartella che contiene `form.png`.

```java
import com.aspose.ocr.*;
import java.awt.Polygon;
import java.util.*;

public class MultiRoiDemo {
    public static void main(String[] args) throws Exception {

        // Step 1 – Initialize engine and load image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.png"));

        // Step 2 – Define polygons for each form field
        Polygon firstField = new Polygon(
                new int[]{50, 200, 200, 50},
                new int[]{100, 100, 150, 150},
                4);
        Polygon secondField = new Polygon(
                new int[]{300, 500, 500, 300},
                new int[]{200, 200, 250, 250},
                4);

        // Step 3 – Limit OCR to those regions
        ocrEngine.getEngineOptions()
                 .setRegionsOfInterest(Arrays.asList(firstField, secondField));

        // Step 4 – Run OCR
        OcrResult ocrResult = ocrEngine.process();

        // Step 5 – Show the result
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Compila con:

```bash
javac -cp "aspose-ocr-23.10.jar" MultiRoiDemo.java
java -cp ".:aspose-ocr-23.10.jar" MultiRoiDemo
```

Dovresti vedere le due righe di testo appartenenti alle ROI definite.

---

## Domande frequenti

**D: Funziona con i PDF?**  
R: Non direttamente. Converti ogni pagina PDF in immagine prima (ad esempio con Aspose PDF) e poi passa l’immagine al motore OCR.

**D: E se il mio modulo ha caselle di controllo?**  
R: L’OCR non può leggere stati booleani, ma puoi trattare l’area della casella come ROI e analizzare la densità dei pixel per inferire un segno di spunta.

**D: Posso estrarre testo da un modulo multipagina in un’unica operazione?**  
R: Itera su ciascuna immagine di pagina, riutilizza la stessa lista ROI e concatena i risultati.

---

## Conclusione

Abbiamo percorso una soluzione completa, end‑to‑end, per **estrarre testo da immagine** usando Aspose OCR, e mostrato come la stessa tecnica ti permetta di **estrarre testo da campi di modulo** con precisione chirurgica. Definendo i poligoni, limitando il focus del motore e gestendo le insidie più comuni, ottieni dati rapidi e puliti senza l’onere di elaborare l’intera immagine.

Pronto per il passo successivo? Prova a trasformare questo output OCR in un payload JSON, o a inviarlo a un modello di machine‑learning per la validazione. Il cielo è il limite, e ora tu

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}