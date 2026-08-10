---
category: general
date: 2026-05-06
description: Come utilizzare l'OCR per estrarre il testo da un'immagine in Java. Impara
  la conversione da immagine a testo con OCR, correggi gli errori OCR e carica l'immagine
  per l'OCR con Aspose OCR.
draft: false
keywords:
- how to use ocr
- extract text from image
- ocr image to text
- correct ocr errors
- load image for ocr
language: it
og_description: Come utilizzare l'OCR in Java per estrarre il testo da un'immagine,
  correggere gli errori OCR e caricare l'immagine per l'OCR usando Aspose OCR.
og_title: Come usare OCR in Java – Guida completa
tags:
- OCR
- Java
- Aspose
title: Come usare OCR in Java – Estrarre testo da un'immagine con correzione ortografica
url: /it/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come usare OCR in Java – Estrarre testo da immagine con correzione ortografica

Ti sei mai chiesto **come usare OCR** per trasformare una foto sfuocata di una ricevuta in testo pulito e ricercabile? Non sei solo. In molti progetti—app di monitoraggio delle spese, pipeline di digitalizzazione delle fatture o anche un semplice script per prendere appunti—ottenere testo affidabile da un'immagine è il primo ostacolo.  

Questo tutorial ti mostra esattamente come usare OCR in Java, coprendo tutto, dal caricamento dell'immagine per OCR alla correzione degli errori OCR in modo che il risultato sembri digitato da un umano. Alla fine, sarai in grado di **extract text from image**, eseguire la conversione **OCR image to text** e correggere automaticamente gli errori di riconoscimento più comuni.

## Cosa Costruirai

Creeremo un piccolo programma console Java che:

1. Carica un PNG (o qualsiasi formato supportato) nel motore Aspose OCR.  
2. Abilita la funzione di correzione ortografica integrata per **correct OCR errors**.  
3. Esegue il processo di riconoscimento e stampa il testo pulito.  

Nessun servizio esterno, nessun framework ingombrante—solo un singolo JAR e poche righe di codice.

### Prerequisiti

- Java Development Kit (JDK) 8 o superiore.  
- Maven (o qualsiasi strumento di build) per scaricare la libreria Aspose OCR.  
- Un file immagine (ad esempio `receipt.png`) che desideri analizzare.  

Se ti manca il JAR Aspose OCR, aggiungi questa dipendenza al tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

> **Suggerimento:** La versione di valutazione gratuita funziona per i test, ma una licenza rimuove la filigrana di valutazione.

## Passo 1 – Inizializzare il motore OCR (Parola chiave principale in azione)

La prima cosa da fare è creare un'istanza di `OcrEngine`. Pensala come il cervello che leggerà i pixel e li trasformerà in caratteri.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Initialise the OCR engine – this is where we start using OCR
        OcrEngine ocrEngine = new OcrEngine();
```

*Perché è importante:* Inizializzare il motore configura le risorse interne (modelli linguistici, dizionari, ecc.). Saltare questo passo causerebbe un `NullPointerException` più tardi quando si tenta di caricare un'immagine.

## Passo 2 – Caricare l'immagine per OCR

Ora carichiamo effettivamente **load image for OCR**. Aspose fornisce un comodo helper `ImageStream.fromFile`, ma puoi anche fornire un `byte[]` se preferisci.

```java
        // Load the image you want to analyse – replace the path with your own file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));
```

*Errore comune:* Il percorso del file deve essere assoluto o relativo alla directory di lavoro. Se l'immagine non viene trovata, il motore lancia un `IOException`. Verifica attentamente il percorso, specialmente quando si esegue da un IDE rispetto a un JAR confezionato.

## Passo 3 – Abilitare la correzione ortografica per **Correct OCR Errors**

L'OCR pronto all'uso può essere rumoroso—pensa a “l0ve” invece di “love” o “0” per “O”. Abilitare la correzione ortografica indica al motore di eseguire un passaggio di post‑elaborazione che corregge gli errori tipici.

```java
        // Turn on the spell‑correction feature – this helps to correct OCR errors
        ocrEngine.getSettings().setEnableSpellCorrection(true);
```

*Perché potresti volerlo:* Senza correzione ortografica, potresti dover pulire manualmente l'output, il che vanifica lo scopo dell'automazione. Il dizionario integrato funziona bene per l'inglese e diverse altre lingue.

## Passo 4 – Eseguire il riconoscimento (**OCR Image to Text**)

Con l'immagine caricata e la correzione ortografica abilitata, possiamo finalmente chiedere al motore di riconoscere il testo.

```java
        // Run the OCR process – this converts the image to text
        OcrResult ocrResult = ocrEngine.recognize();
```

*Caso limite:* Se l'immagine ha basso contrasto o è fortemente inclinata, il risultato potrebbe ancora contenere spazzatura. Considera un pre‑processamento (ad es., binarizzazione, correzione dell'inclinazione) prima di passarla al motore.

## Passo 5 – Stampare il testo pulito

L'ultimo passo è semplicemente stampare il risultato. In un'applicazione reale potresti scriverlo in un database o in un file, ma per questa demo `System.out` è sufficiente.

```java
        // Display the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

### Output previsto

Assumendo che `receipt.png` contenga un elenco chiaro di articoli, potresti vedere qualcosa del genere:

```
Corrected text:
Item           Qty   Price
Apple          2     $1.20
Banana         5     $0.75
Total               $5.55
```

Nota come “Qty” e “Price” siano scritti correttamente anche se la scansione originale aveva un “Qy” errato.

## Esempio completo funzionante

Di seguito trovi il programma completo che puoi copiare‑incollare in un file chiamato `SpellCorrectDemo.java`. Assicurati che il JAR Aspose OCR sia nel tuo classpath.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // Replace "YOUR_DIRECTORY/receipt.png" with the actual path
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));

        // Step 3: Enable spell correction to improve accuracy
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Step 4: Perform OCR recognition (OCR image to text)
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

Eseguilo con:

```bash
javac -cp "aspose-ocr-23.9.jar" SpellCorrectDemo.java
java -cp ".:aspose-ocr-23.9.jar" SpellCorrectDemo
```

Dovresti ora vedere il testo pulito stampato sulla console.

## Bonus: Regolare le impostazioni per una migliore precisione

Mentre la configurazione predefinita funziona per la maggior parte dei documenti stampati, potresti dover regolare alcuni parametri per scenari specializzati:

| Impostazione | Cosa fa | Quando modificare |
|--------------|----------|-------------------|
| `setLanguage(OcrLanguage.English)` | Forza il dizionario inglese (riduce i falsi positivi) | Se la tua immagine contiene solo testo in inglese. |
| `setResolution(300)` | Indica al motore i DPI dell'immagine sorgente | Per scansioni ad alta risoluzione. |
| `setEnableAutoSkewCorrection(true)` | Ruota automaticamente pagine leggermente inclinate | Quando le immagini sono catturate con uno smartphone. |

```java
ocrEngine.getSettings().setLanguage(OcrLanguage.English);
ocrEngine.getSettings().setResolution(300);
ocrEngine.getSettings().setEnableAutoSkewCorrection(true);
```

## Domande frequenti

**Q: Funziona con i PDF?**  
A: Sì. Converti ogni pagina PDF in un'immagine (ad esempio, usando Aspose PDF) e passa l'immagine al motore OCR.

**Q: E se la mia immagine è in formato BMP?**  
A: `ImageStream.fromFile` supporta PNG, JPEG, BMP, TIFF e GIF nativamente. Basta cambiare l'estensione del file.

**Q: Posso disabilitare la correzione ortografica?**  
A: Assolutamente—imposta `setEnableSpellCorrection(false)` se ti serve l'output OCR grezzo per l'elaborazione successiva.

## Conclusione

Ora sai **come usare OCR** in Java per **estrarre testo da immagine**, correggere automaticamente **OCR errors**, e caricare correttamente **image for OCR** usando Aspose OCR. Il flusso a cinque passaggi—inizializzare, caricare, abilitare la correzione ortografica, riconoscere e stampare—copre la maggior parte dei compiti OCR quotidiani.  

Da qui, considera di concatenare questa logica con una scrittura su database, un endpoint REST o un processore batch per gestire decine di ricevute contemporaneamente. Sperimenta con la tabella delle impostazioni aggiuntive sopra per estrarre l'ultima goccia di precisione.

Buon coding, e che i tuoi risultati OCR siano sempre più puliti delle tue ricevute macchiate di caffè! 

![diagramma di come usare OCR che mostra immagine → OCR engine → flusso di testo corretto]

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}