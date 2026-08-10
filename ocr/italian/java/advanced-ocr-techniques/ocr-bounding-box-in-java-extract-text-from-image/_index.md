---
category: general
date: 2026-06-16
description: Il tutorial OCR bounding box in Java mostra come estrarre testo da un'immagine,
  leggere il testo da un'immagine e ottenere il punteggio di confidenza OCR per file
  JPG.
draft: false
keywords:
- ocr bounding box
- extract text from image
- ocr confidence score
- recognize text from jpg
- read text from image
language: it
og_description: Il bounding box OCR in Java ti consente di riconoscere il testo da
  file JPG, estrarre il testo dall’immagine e visualizzare i punteggi di confidenza
  OCR—tutto in un semplice esempio di codice.
og_title: Rettangolo di delimitazione OCR in Java – Estrai testo dall'immagine
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: OCR bounding box tutorial in Java shows how to extract text from image,
    read text from image, and get OCR confidence score for JPG files.
  headline: OCR Bounding Box in Java – Extract Text from Image
  type: TechArticle
tags:
- OCR
- Java
- image-processing
- text-recognition
title: Rettangolo di delimitazione OCR in Java – Estrai testo dall'immagine
url: /it/java/advanced-ocr-techniques/ocr-bounding-box-in-java-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Bounding Box in Java – Estrarre Testo da Immagine

Ti sei mai chiesto come ottenere il **ocr bounding box** per ogni frammento di testo in un'immagine Java? In questo tutorial ti mostreremo come **estrarre testo da immagine** file, **leggere testo da immagine**, e persino vedere il **ocr confidence score** mentre **rilevi testo da file jpg**. La risposta breve? Alcune righe di codice usando una libreria OCR moderna, più una breve spiegazione del perché ogni chiamata è importante.

Di seguito troverai un esempio completo, pronto‑all'uso, una suddivisione passo‑passo e una serie di consigli pratici che puoi copiare direttamente nel tuo progetto. Alla fine, sarai in grado di produrre qualcosa di simile a:

```
Text: "Hello World"  Confidence: 0.97  Box: (x=12, y=45, width=210, height=30)
```

## Cosa Ti Serve

- **Java 11** o versioni successive (la sintassi qui sotto usa la keyword `var` per brevità, ma puoi rimuoverla per JDK più vecchi).  
- Una libreria OCR che offre un'API Java – per questa guida useremo **[Tesseract4J](https://github.com/nguyenq/tess4j)**, un leggero wrapper attorno al popolare motore Tesseract.  
- Un'immagine JPEG (`.jpg`) che contiene testo stampato chiaro.  
- Il tuo IDE preferito (IntelliJ IDEA, Eclipse, VS Code…) – qualsiasi va bene.

Se ti manca la libreria, aggiungi semplicemente questa dipendenza Maven:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

Ora immergiamoci.

![OCR bounding box example](ocr-bounding-box.png "OCR bounding box example")

## OCR Bounding Box: Configurare il Motore

La prima cosa da fare è creare un'istanza del motore OCR. Pensala come accendere lo scanner che in seguito leggerà i pixel.

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

ITesseract ocrEngine = new Tesseract();          // Step 1 – create the OCR engine
ocrEngine.setDatapath("tessdata");               // point to the language data files
ocrEngine.setLanguage("eng");                    // we’ll work with English for now
```

**Perché è importante:**  
Senza impostare `datapath`, Tesseract non saprà dove si trovano i pacchetti di lingua e otterrai un criptico errore “Failed loading language”. La chiamata `setLanguage` è opzionale se ti serve solo il pacchetto predefinito inglese, ma essere espliciti rende il codice più chiaro per i lettori futuri.

## Carica l'Immagine da Processare

Successivamente, fornisci al motore il JPEG che desideri analizzare. La libreria accetta un `File` o un `BufferedImage`; useremo un `File` per semplicità.

```java
import java.io.File;

File imageFile = new File("YOUR_DIRECTORY/text_page.jpg");   // Step 2 – load the image
```

**Consiglio professionale:**  
Se la tua immagine si trova nelle risorse (ad esempio, dentro un JAR), usa `getResourceAsStream` e avvolgila con `ImageIO.read`. In questo modo il tutorial funziona sia localmente sia in un'app confezionata.

## Esegui il Riconoscimento OCR

Ora chiediamo effettivamente al motore di leggere l'immagine. Il risultato è una stringa di testo semplice, ma vogliamo anche il **ocr confidence score** e il **ocr bounding box** per ogni riga.

```java
try {
    // Step 3 – run OCR and get a result object with layout data
    var result = ocrEngine.doOCR(imageFile, null);
    // The simple doOCR call returns only text; to get boxes we need the
    // getWords method with a specific page iterator level.
    var words = ocrEngine.getWords(imageFile, ITesseract.PageIteratorLevel.RIL_WORD);
    
    // Step 4 – iterate over each detected word
    for (var word : words) {
        System.out.printf(
            "Text: \"%s\"  Confidence: %.2f  Box: %s%n",
            word.getText(),
            word.getConfidence(),
            word.getBoundingBox().toString()
        );
    }
} catch (TesseractException e) {
    System.err.println("OCR failed: " + e.getMessage());
}
```

**Perché usiamo `getWords` invece del semplice `doOCR`:**  
`doOCR` ti restituisce la stringa grezza ma scarta le informazioni spaziali. Chiamando `getWords` con `RIL_WORD` (o `RIL_TEXTLINE` se preferisci i riquadri a livello di riga), otteniamo una lista di oggetti `Word` che contengono il testo, la confidenza e il rettangolo di delimitazione. Questo è il cuore della funzionalità **ocr bounding box**.

## Comprendere l'Output

Eseguire lo snippet sopra su un JPEG pulito produce un output simile a:

```
Text: "Hello"  Confidence: 0.99  Box: java.awt.Rectangle[x=34,y=12,width=112,height=28]
Text: "World"  Confidence: 0.97  Box: java.awt.Rectangle[x=156,y=12,width=98,height=28]
```

- **Testo** – i caratteri riconosciuti.  
- **Confidenza** – un valore a virgola mobile tra 0 e 1; più alto indica che il motore è più sicuro.  
- **Box** – il rettangolo che racchiude la parola in coordinate pixel (x, y, larghezza, altezza).  

Ora puoi **leggere testo da immagine** e sapere esattamente dove si trova ogni frammento sulla tela—perfetto per evidenziare, ritagliare o inviare a pipeline NLP successive.

## Casi Limite & Problemi Comuni

| Situation | What to Watch For | Fix / Work‑around |
|-----------|-------------------|-------------------|
| L'immagine è sfocata o a basso contrasto | I punteggi di confidenza diminuiscono drasticamente (spesso sotto 0,6). | Pre‑processare con OpenCV: aumentare il contrasto, applicare la sogliatura. |
| Il JPEG contiene testo ruotato | I riquadri di delimitazione appaiono distorti o mancanti. | Usa `ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO_OSD)` per consentire a Tesseract di rilevare automaticamente l'orientamento. |
| Immagini grandi causano OutOfMemoryError | L'heap Java si riempie caricando immagini grandi. | Ridimensiona l'immagine prima dell'OCR (`ImageIO.read` → `BufferedImage.getScaledInstance`). |
| Hai bisogno di riquadri a livello di riga anziché a livello di parola | `RIL_WORD` restituisce riquadri per parola. | Passa a `ITesseract.PageIteratorLevel.RIL_TEXTLINE`. |
| Caratteri non‑inglesi appaiono come � | Dati di lingua non caricati. | Scarica il file `.traineddata` appropriato e punta `setDatapath` alla sua cartella. |

Affrontare questi problemi in anticipo ti farà risparmiare ore di debug in seguito.

## Esempio Completo Funzionante (Tutti i Passaggi in Un Solo File)

Di seguito trovi una classe Java autonoma che puoi copiare‑incollare in una cartella `src/main/java` ed eseguire con `mvn exec:java`. Raccoglie tutto ciò di cui abbiamo parlato.



## Cosa Dovresti Imparare Dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Estrarre Testo da Immagine Java con Aspose.OCR Modalità Rileva Aree](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Estrarre Immagini di Testo – Nozioni Base OCR con Aspose.OCR per Java](/ocr/english/java/ocr-basics/)
- [Come Eseguire OCR su Testo di Immagine con Lingua Usando Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}