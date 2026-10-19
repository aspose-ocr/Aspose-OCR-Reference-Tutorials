---
category: general
date: 2026-09-23
description: Scopri come eseguire l'OCR su immagini in Java usando Aspose OCR, estrarre
  il testo dall'immagine e abilitare la correzione ortografica con un dizionario personalizzato.
draft: false
keywords:
- how to perform ocr
- how to extract text from image
- java ocr maven dependency
- java image to text conversion
- aspose ocr java
lastmod: 2026-09-23
og_description: Come eseguire l'OCR su immagini in Java con Aspose OCR. Questa guida
  mostra come caricare un'immagine, estrarre il testo dall'immagine e aggiungere la
  correzione ortografica per risultati accurati.
og_image_alt: 'Aspose OCR Java tutorial: extracting text from images with spell correction'
og_title: Come eseguire l'OCR su immagini con Aspose OCR in Java
schemas:
- author: Aspose
  dateModified: '2026-09-23'
  description: Learn how to perform OCR on images in Java using Aspose OCR, extract
    text from image, and enable spell correction with a custom dictionary.
  headline: How to perform OCR on images with Aspose OCR in Java
  type: TechArticle
- description: Learn how to perform OCR on images in Java using Aspose OCR, extract
    text from image, and enable spell correction with a custom dictionary.
  name: How to perform OCR on images with Aspose OCR in Java
  steps:
  - name: set up the project and import dependencies
    text: Add the Aspose OCR Maven dependency to your `pom.xml`. This single line
      pulls in the core OCR engine and all required transitive libraries. > **Pro
      tip:** Verify the version number on Maven Central; newer releases add language
      packs and performance improvements.
  - name: load the image for OCR
    text: '`OcrEngine` works with any `InputStream`. Use `ImageStream` to wrap a file
      path, byte array, or URL. **Definition anchor:** `ImageStream` is Aspose OCR’s
      lightweight wrapper that reads image data from various sources without converting
      it to a `BufferedImage` first.'
  - name: enable spell‑correction (optional but powerful)
    text: Turn on the built‑in spell‑correction flag to automatically fix common OCR
      mis‑recognitions such as “l” vs “1”. Spell‑correction can improve accuracy by
      up to **80 %** on low‑contrast scans, turning “Inv0ice” into “Invoice” without
      extra code.
  - name: provide a custom dictionary (tailor the engine)
    text: Supply a plain‑text dictionary for industry‑specific terminology—medical
      codes, legal terms, product SKUs, etc. **Definition anchor:** `CustomDictionary`
      loads a UTF‑8 word list that the OCR engine consults during post‑processing
      to prefer your domain vocabulary.
  - name: run the OCR process
    text: Invoke `process()` to get an `OcrResult` containing the recognized text,
      confidence scores, and optional layout data. If an error occurs, `ocrResult.getErrorMessage()`
      returns a detailed description you can log or display.
  - name: output the recognized (and corrected) text
    text: 'Print the extracted string to the console or write it to a file. For quick
      testing, a simple `System.out.println` is sufficient. Running the program should
      produce clean, searchable text similar to: If you notice stray characters, revisit
      your custom dictionary and consider pre‑processing the image '
  type: HowTo
- questions:
  - answer: No. The library runs entirely offline; all recognition happens locally
      on your JVM.
    question: Does Aspose OCR require an internet connection?
  - answer: Aspose OCR supports Java 8 through Java 21, including both standard and
      OpenJDK distributions.
    question: Which Java versions are supported?
  - answer: Yes. The engine streams data and can handle images up to 500 MB, limited
      only by available heap memory.
    question: Can I process images larger than 10 MB?
  - answer: Purchase a commercial license from the Aspose store and set the license
      file with `License license = new License(); license.setLicense("Aspose.OCR.lic");`.
    question: How do I license Aspose OCR for production?
  - answer: Aspose OCR includes a handwriting mode that can be enabled via `ocrEngine.getEngineOptions().setHandwriting(true);`,
      improving accuracy on cursive scripts.
    question: Is there built‑in support for handwritten text?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
- image to text
- OCR Maven dependency
title: Come eseguire l'OCR su immagini con Aspose OCR in Java
url: /it/java/advanced-ocr-techniques/perform-ocr-on-image-with-aspose-ocr-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esegui OCR su immagine – tutorial Java completo

Se stai cercando un modo affidabile per **eseguire OCR** su file immagine usando Java, sei nel posto giusto. Con Aspose OCR per Java puoi estrarre testo da risorse immagine in poche righe di codice, aumentare la precisione con un dizionario personalizzato e abilitare la correzione ortografica per pulire scansioni rumorose. Questo tutorial ti guida passo dopo passo—dalla lettura dell’immagine per l’OCR alla stampa del testo corretto—così potrai integrare la conversione immagine‑testo nelle tue applicazioni oggi.

## Risposte rapide
- **Qual è la classe principale per avviare l'OCR?** `OcrEngine` è la classe core di Aspose OCR che esegue il riconoscimento ottico dei caratteri.
- **Quale artefatto Maven aggiunge il supporto OCR?** Aggiungi `com.aspose:aspose-ocr` al tuo `pom.xml`.
- **È necessaria una licenza per lo sviluppo?** Una licenza temporanea gratuita funziona per i test; è richiesta una licenza commerciale per la produzione.
- **Posso migliorare la precisione su scansioni di bassa qualità?** Sì—abilita la correzione ortografica e fornisci un dizionario personalizzato.
- **Il supporto multi‑pagina è integrato?** Elabora ogni immagine di pagina in un ciclo; il motore è thread‑safe per esecuzioni concorrenti.

## Che cos’è eseguire OCR?
La frase **eseguire OCR** si riferisce al processo di conversione del testo stampato o scritto a mano in un’immagine in caratteri digitali modificabili e ricercabili mediante la tecnologia di riconoscimento ottico dei caratteri. Aspose OCR implementa questo processo con un motore a singolo passaggio che supporta oltre 20 formati raster e più di 50 lingue.

## Perché usare Aspose OCR per Java?
Aspose OCR supporta **oltre 20 formati immagine** (inclusi PNG, JPEG, TIFF, BMP e GIF) e può elaborare **batch di centinaia di pagine** senza caricare l’intero documento in memoria, offrendo fino a **300 pagine al minuto** su un tipico server a 4 core. Le sue funzionalità integrate di correzione ortografica e dizionario personalizzato riducono i tassi di errore OCR tipici dal 12 % a meno del 2 % su fatture rumorose.

## Prerequisiti
- **Java Development Kit (JDK) 8+** – runtime Java standard.
- **Libreria Aspose OCR per Java** – ottieni l’ultimo JAR da Maven Central o dal portale di download Aspose.
- Un file immagine (ad es. `invoice.png`) che desideri elaborare.
- (Opzionale) `custom_dict.txt` – file di testo UTF‑8 contenente parole specifiche del dominio, una per riga.

Questo è tutto ciò di cui hai bisogno—nessun servizio esterno o framework ingombrante.

## Come eseguire OCR su immagine in Java?
Carica la tua immagine, abilita la correzione ortografica, opzionalmente fornisci un dizionario personalizzato, avvia il motore e leggi il risultato. Questo approccio funziona sia per file a pagina singola sia per elaborazioni batch, e il motore gestisce automaticamente la decodifica dell’immagine, il rilevamento della lingua e il punteggio di confidenza, fornendoti un output testuale affidabile pronto per ulteriori elaborazioni. Le sezioni seguenti scompongono ogni passaggio con spiegazioni chiare e il codice esatto da copiare.

### Passo 1: configura il progetto e importa le dipendenze

Aggiungi la dipendenza Maven di Aspose OCR al tuo `pom.xml`. Questa singola riga importa il motore OCR core e tutte le librerie transitive richieste.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

> **Suggerimento:** Verifica il numero di versione su Maven Central; le versioni più recenti aggiungono pacchetti lingua e miglioramenti di performance.

### Passo 2: carica l’immagine per l’OCR

`OcrEngine` funziona con qualsiasi `InputStream`. Usa `ImageStream` per avvolgere un percorso file, un array di byte o un URL.

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 2: Load the image you wish to process
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));
```

**Ancora di definizione:** `ImageStream` è il wrapper leggero di Aspose OCR che legge i dati immagine da varie sorgenti senza convertirli prima in un `BufferedImage`.

### Passo 3: abilita la correzione ortografica (opzionale ma potente)

Attiva il flag di correzione ortografica integrato per correggere automaticamente le comuni errate interpretazioni OCR come “l” vs “1”.

```java
        // Step 3: Turn on spell‑checking to improve result quality
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);
```

La correzione ortografica può migliorare la precisione fino all’**80 %** su scansioni a basso contrasto, trasformando “Inv0ice” in “Invoice” senza codice aggiuntivo.

### Passo 4: fornisci un dizionario personalizzato (adatta il motore)

Fornisci un dizionario di testo semplice per terminologia specifica del settore—codici medici, termini legali, SKU di prodotto, ecc.

```java
        // Step 4: Load a custom dictionary to boost recognition of domain terms
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));
```

**Ancora di definizione:** `CustomDictionary` carica un elenco di parole UTF‑8 che il motore OCR consulta durante il post‑processing per privilegiare il tuo vocabolario di dominio.

### Passo 5: esegui il processo OCR

Invoca `process()` per ottenere un `OcrResult` contenente il testo riconosciuto, i punteggi di confidenza e, opzionalmente, i dati di layout.

```java
        // Step 5: Execute OCR and capture the result
        OcrResult ocrResult = ocrEngine.process();
```

Se si verifica un errore, `ocrResult.getErrorMessage()` restituisce una descrizione dettagliata che puoi registrare o visualizzare.

### Passo 6: output del testo riconosciuto (e corretto)

Stampa la stringa estratta sulla console o scrivila su un file. Per test rapidi, un semplice `System.out.println` è sufficiente.

```java
        // Step 6: Print the corrected text to the console
        System.out.println(ocrResult.getText());
    }
}
```

L’esecuzione del programma dovrebbe produrre testo pulito e ricercabile simile a:

```
Invoice Number: 12345
Date: 2023‑07‑15
Total Amount: $1,250.00
```

Se noti caratteri estranei, rivedi il tuo dizionario personalizzato e considera un pre‑processing dell’immagine (aumenta il contrasto, riduci il rumore o converti in scala di grigi).

## Come estrarre testo da immagine usando un dizionario personalizzato?
Carica il dizionario prima dell’elaborazione, quindi chiama `ocrEngine.setCustomDictionary(customDict)`. Il motore darà priorità alle parole dell’elenco, riducendo drasticamente i falsi positivi per vocabolari specializzati. Fornendo termini specifici del dominio, aiuti il post‑processor OCR a risolvere caratteri ambigui, come distinguere la lettera “O” dal numero “0”, migliorando la precisione complessiva su documenti tecnici.

## Come aggiungere correttamente la dipendenza Maven per OCR Java?
Aggiungi il seguente snippet al tuo `pom.xml` nella sezione `<dependencies>`. Questa dipendenza importa la libreria core di Aspose OCR insieme a tutti i componenti transitori necessari, garantendo che il motore OCR possa essere istanziato senza configurazioni aggiuntive. Assicurati di eseguire `mvn clean install` dopo aver aggiornato il file affinché Maven risolva l’ultima versione dal repository centrale.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

## Domande comuni & casi limite

### E se l’immagine è in un formato diverso (PDF, TIFF, ecc.)?
Aspose OCR gestisce direttamente i formati raster. Per i PDF, estrai prima ogni pagina come immagine—Aspose PDF per Java fornisce `PdfExtractor` per farlo in modo efficiente. Una volta ottenuto un `BufferedImage` o uno stream di byte, la stessa chiamata `setImage` funziona. Questo approccio ti consente di elaborare documenti multi‑pagina senza convertire l’intero PDF in memoria, mantenendo il flusso di lavoro veloce e scalabile.

### Come gestire documenti multi‑pagina?
Itera su ogni immagine di pagina, istanzia un nuovo `OcrEngine` (o resetta quello esistente) e concatena i valori restituiti da `OcrResult.getText()`. Questo mantiene i contesti di correzione ortografica indipendenti per pagina. Elaborando le pagine in sequenza o in thread paralleli, puoi mantenere un alto throughput garantendo che ogni pagina benefici delle stesse impostazioni di dizionario e correzione ortografica.

### È possibile limitare la lingua o il set di caratteri?
Sì. Chiama `ocrEngine.getEngineOptions().setLanguage(Language.English)` (o qualsiasi lingua supportata) per restringere l’ambito di riconoscimento, accelerando l’elaborazione fino al **30 %**. Limitare la lingua riduce il set di caratteri che il motore deve considerare, diminuendo l’ambiguità e migliorando sia la velocità sia la precisione, soprattutto per documenti contenenti solo caratteri latini.

### Cosa dice delle prestazioni su grandi batch?
Il motore è thread‑safe per operazioni di sola lettura. Crea un pool di thread e assegna a ciascuna immagine la propria istanza di `OcrEngine`. Su una macchina a 4 core, è possibile raggiungere **≈250 pagine/minuto** con esecuzione parallela. Assicurati di allocare sufficiente heap memory e monitora l’uso della CPU per evitare colli di bottiglia quando elabori migliaia di immagini ad alta risoluzione.

## Suggerimenti per una migliore precisione

- **Pre‑processa l’immagine**: aumenta il contrasto, applica un filtro mediano o converti in scala di grigi prima dell’OCR.
- **Usa scansioni a 300 dpi o superiori**; risoluzioni più basse aumentano drasticamente i tassi di errore.
- **Mantieni il dizionario personalizzato focalizzato**: parole non correlate in eccesso possono confondere il correttore ortografico.
- **Post‑processa con regex**: valida date, numeri o ID dopo l’estrazione per catturare eventuali anomalie residue.

## Prossimi passi

Ora che sai **come eseguire OCR** su immagini e **come estrarre testo da file immagine**, potresti esplorare:

- Salvataggio dell’output OCR come PDF ricercabile con livello di testo nascosto.
- Memorizzazione dei dati di fattura estratti direttamente in un database relazionale.
- Applicazione di modelli di machine‑learning per pulire ulteriormente note scritte a mano.
- Esposizione del flusso di lavoro OCR come servizio web RESTful per immagini caricate dagli utenti.

Ognuna di queste estensioni si basa sui passaggi fondamentali descritti sopra, quindi la transizione sarà fluida.

---

**Ultimo aggiornamento:** 2026-09-23  
**Testato con:** Aspose OCR 24.12 per Java  
**Autore:** Aspose  



## Domande frequenti

**D: Aspose OCR richiede una connessione internet?**  
R: No. La libreria funziona interamente offline; tutto il riconoscimento avviene localmente sulla tua JVM.

**D: Quali versioni di Java sono supportate?**  
R: Aspose OCR supporta Java 8 fino a Java 21, incluse le distribuzioni standard e OpenJDK.

**D: Posso elaborare immagini più grandi di 10 MB?**  
R: Sì. Il motore trasmette i dati in streaming e può gestire immagini fino a 500 MB, limitato solo dalla memoria heap disponibile.

**D: Come licenziare Aspose OCR per la produzione?**  
R: Acquista una licenza commerciale dallo store Aspose e imposta il file di licenza con `License license = new License(); license.setLicense("Aspose.OCR.lic");`.

**D: È disponibile il supporto integrato per il testo scritto a mano?**  
R: Aspose OCR include una modalità handwriting che può essere attivata tramite `ocrEngine.getEngineOptions().setHandwriting(true);`, migliorando la precisione su script corsivi.

---

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you wish to process
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));

        // Step 3: Enable spell‑checking for the OCR result
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);

        // Step 4: Provide a custom dictionary (one word per line)
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));

        // Step 5: Run the OCR process
        OcrResult ocrResult = ocrEngine.process();

        // Step 6: Output the recognized (and corrected) text
        System.out.println(ocrResult.getText());
    }
}
```

## Tutorial correlati

- [Perform Ocr On Image With Aspose Ocr Java Step By Step Guide](/ocr/java/advanced-ocr-techniques/perform-ocr-on-image-with-aspose-ocr-java-step-by-step-guide/)
- [Preprocess Image Ocr In Java Boost Accuracy Extract Text](/ocr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)
- [How To Enable Gpu For Ocr In Java Recognize Text From Image](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-recognize-text-from-image/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}