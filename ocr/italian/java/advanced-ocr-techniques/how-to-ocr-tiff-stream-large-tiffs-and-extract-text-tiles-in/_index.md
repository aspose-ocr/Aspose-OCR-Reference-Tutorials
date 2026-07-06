---
category: general
date: 2026-04-29
description: Impara come eseguire l'OCR di file TIFF usando la modalità streaming
  di Aspose OCR. Questa guida ti mostra come estrarre le tessere di testo da immagini
  TIFF a piastrelle in modo efficiente.
draft: false
keywords:
- how to ocr tiff
- extract text tiles
language: it
og_description: Come eseguire OCR su TIFF usando lo streaming di Aspose OCR. Codice
  passo‑passo per estrarre le tessere di testo da grandi immagini TIFF.
og_title: come fare OCR su TIFF – Guida completa allo streaming
tags:
- OCR
- Java
- Aspose
- TIFF
title: come fare OCR su TIFF – Stream di grandi TIFF ed estrazione di piastrelle di
  testo in Java
url: /it/java/advanced-ocr-techniques/how-to-ocr-tiff-stream-large-tiffs-and-extract-text-tiles-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# come fare OCR su TIFF – Stream di grandi TIFF e estrarre riquadri di testo in Java

Ti sei mai chiesto **come fare OCR su TIFF** file troppo grandi per essere caricati interamente in memoria? Non sei l'unico. Molti sviluppatori si trovano in difficoltà quando le loro immagini TIFF sono suddivise in decine di riquadri, e la consueta chiamata `ocrEngine.recognize()` semplicemente si blocca.  

La buona notizia? La modalità streaming di Aspose OCR ti permette di fornire ogni riquadro come un flusso separato, così puoi **estrarre riquadri di testo** senza far esplodere l'heap. In questo tutorial percorreremo un esempio Java completo, pronto‑da‑eseguire, spiegheremo perché ogni riga è importante e indicheremo le insidie da evitare.

> **Cosa otterrai:** un programma eseguibile che unisce i TIFF a tasselli al volo, stampa il testo combinato e ti mostra come adattare il codice ad altre lingue o formati immagine.

---

## Prerequisiti

- **Java 17** o versioni successive (il codice utilizza try‑with‑resources, quindi JDK 8+ funziona, ma JDK 17 è l'LTS attuale).
- **Aspose.OCR for Java** library (v23.10 o successiva). Aggiungila tramite Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

- Una cartella contenente i singoli riquadri TIFF (ad es., `tile_0.tif`, `tile_1.tif`, …).  
- Opzionale: un IDE come IntelliJ IDEA o VS Code – ma un semplice editor di testo va bene.

---

## Passo 1 – Preparare i Percorsi dei Riquadri (Perché è Importante)

Prima che il motore OCR possa fare qualcosa, deve sapere dove si trovano i singoli pezzi dell'immagine. Codificare i percorsi in modo statico va bene per una dimostrazione, ma in produzione probabilmente scannerizzerai una directory o leggerai un file manifesto.

```java
// Define the absolute or relative paths to each TIFF tile
String[] tilePaths = {
    "YOUR_DIRECTORY/tile_0.tif",
    "YOUR_DIRECTORY/tile_1.tif",
    "YOUR_DIRECTORY/tile_2.tif"
};
```

> **Consiglio professionale:** mantieni i riquadri in ordine lessicografico (0, 1, 2…) perché il motore concatenarà il testo riconosciuto nella stessa sequenza con cui fornisci i flussi.

---

## Passo 2 – Abilitare la Modalità Streaming sul Motore OCR (Parola Chiave Principale)

Ora creiamo l'istanza `OcrEngine` e attiviamo lo streaming. Questo è il fulcro di **come fare OCR su TIFF** senza caricare l'intera immagine in RAM.

```java
// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Activate streaming – essential for large or tiled TIFFs
ocrEngine.getProcessingSettings().setEnableStreaming(true);

// Set the language to English; change as needed (e.g., "fr", "de")
ocrEngine.getLanguageSettings().setLanguage("en");
```

**Perché lo streaming?**  
Quando viene chiamato `setEnableStreaming(true)`, il motore tratta ogni `ImageStream` in ingresso come una continuazione del precedente. Costruisce una tela virtuale interna, unisce i riquadri virtualmente e avvia l'OCR una sola volta alla fine. Questo evita l'“OutOfMemoryError” che si verificherebbe se si provasse a caricare un TIFF multi‑gigabyte tutto in una volta.

---

## Passo 3 – Aggiungere Ogni Riquadro come Stream di Input (Parola Chiave Secondaria)

Ecco il ciclo che fornisce ogni riquadro al motore. Il blocco `try‑with‑resources` garantisce che il handle del file venga chiuso prontamente, il che è cruciale quando si gestiscono decine di file.

```java
for (String tilePath : tilePaths) {
    try (InputStream stream = new FileInputStream(tilePath)) {
        // Wrap the raw InputStream in Aspose's ImageStream wrapper
        ocrEngine.appendImage(ImageStream.fromStream(stream));
    } catch (IOException e) {
        // If a single tile fails, we log and continue – you might want to abort instead
        System.err.println("Failed to load tile: " + tilePath);
        e.printStackTrace();
    }
}
```

Nota che la frase **estrarre riquadri di testo** è inserita naturalmente: ogni iterazione *estrae* il testo da un riquadro e lo aggiunge al risultato in crescita.

---

## Passo 4 – Eseguire il Riconoscimento e Stampare il Testo Combinato (Parola Chiave Principale)

Dopo che tutti i riquadri sono stati accodati, una singola chiamata esegue l'OCR sull'immagine virtuale. Il risultato contiene il testo completo, proprio come se avessi un unico TIFF enorme.

```java
// Perform OCR on the combined virtual image
OcrResult ocrResult = ocrEngine.recognize();

// Print the extracted text to the console
System.out.println("=== OCR Output ===");
System.out.println(ocrResult.getText());
```

**Output previsto** (supponendo che i riquadri contengano la frase “Hello World” suddivisa tra di loro):

```
=== OCR Output ===
Hello World
```

Se i tuoi riquadri contengono più righe, appariranno nello stesso ordine in cui li hai forniti. Puoi anche scrivere `ocrResult.getText()` su un file per l'elaborazione successiva.

---

## Passo 5 – Esempio Completo e Eseguibile (Tutti i Passi in Un Solo Luogo)

Di seguito trovi il programma completo che puoi copiare‑incollare in `StreamingExample.java`. Include tutti gli import, i commenti e la gestione degli errori.

```java
import com.aspose.ocr.*;
import java.io.*;

public class StreamingExample {
    public static void main(String[] args) throws Exception {
        // ------------------------------------------------------------
        // Step 1: List the TIFF tile files
        // ------------------------------------------------------------
        String[] tilePaths = {
            "YOUR_DIRECTORY/tile_0.tif",
            "YOUR_DIRECTORY/tile_1.tif",
            "YOUR_DIRECTORY/tile_2.tif"
        };

        // ------------------------------------------------------------
        // Step 2: Set up the OCR engine in streaming mode
        // ------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getProcessingSettings().setEnableStreaming(true);
        ocrEngine.getLanguageSettings().setLanguage("en");

        // ------------------------------------------------------------
        // Step 3: Feed each tile as a separate stream
        // ------------------------------------------------------------
        for (String tilePath : tilePaths) {
            try (InputStream stream = new FileInputStream(tilePath)) {
                ocrEngine.appendImage(ImageStream.fromStream(stream));
            } catch (IOException e) {
                System.err.println("Unable to read tile: " + tilePath);
                e.printStackTrace();
                // Optionally: return; // abort on missing tile
            }
        }

        // ------------------------------------------------------------
        // Step 4: Recognize the combined image and display the text
        // ------------------------------------------------------------
        OcrResult ocrResult = ocrEngine.recognize();
        System.out.println("=== OCR Output ===");
        System.out.println(ocrResult.getText());
    }
}
```

Salva, compila e avvia:

```bash
javac -cp "path/to/aspose-ocr.jar" StreamingExample.java
java -cp ".:path/to/aspose-ocr.jar" StreamingExample
```

Dovresti vedere il testo OCR concatenato stampato sulla console.

---

## Suggerimenti Avanzati & Problemi Comuni (Perché Questo Funziona)

| Problema | Perché Accade | Come Risolvere / Ottimizzare |
|----------|----------------|------------------------------|
| **Errori di Out‑of‑memory** | Caricare un TIFF a dimensione intera in un `BufferedImage` consuma l'intero heap. | Usa la modalità streaming (`setEnableStreaming(true)`) – il motore non materializza mai l'intera immagine. |
| **Mancata corrispondenza dell'ordine dei riquadri** | I file vengono ordinati alfabeticamente anziché numericamente (es., `tile_10.tif` prima di `tile_2.tif`). | Aggiungi zeri di riempimento ai numeri (`tile_00.tif`, `tile_01.tif`) o ordina programmaticamente usando `Comparator`. |
| **Lingua errata** | L'OCR usa l'inglese di default; il testo non inglese diventa illeggibile. | Chiama `ocrEngine.getLanguageSettings().setLanguage("fr")` (o qualsiasi codice ISO supportato). |
| **Errori parziali** | Un riquadro corrotto interrompe l'intero processo. | Cattura `IOException` per ogni riquadro, registra il log e decidi se continuare o abortire. |
| **Collo di bottiglia delle prestazioni** | L'I/O del disco domina quando si leggono molti file piccoli. | Raggruppa i riquadri in un ZIP e stream da memoria, o usa un SSD veloce. |

---

## Quando Usare lo Streaming vs. OCR su Immagine Singola

- **Streaming** è ideale per:
  - TIFF multi‑pagina o scansioni gigapixel.
  - Situazioni in cui la memoria è limitata (es., container Docker, dispositivi mobili).
  - Pipeline che ricevono già blocchi di immagine (es., flussi di telecamera).

- **OCR su immagine singola** funziona bene per:
  - File PNG/JPEG piccoli (< 5 MB).
  - Scansioni occasionali dove la semplicità supera le prestazioni.

---

## Conclusione

Ora hai una solida comprensione di **come fare OCR su TIFF** usando le capacità di streaming di Aspose OCR, e sai come **estrarre riquadri di testo** in modo efficiente. La soluzione completa — inizializzare il motore, abilitare lo streaming, aggiungere ogni riquadro e infine riconoscere la tela virtuale — copre il “cosa”, il “perché” e il “come” di cui hai bisogno per un codice pronto per la produzione.

Prossimi passi? Prova a sostituire `"en"` con un'altra lingua, o sperimenta con formati immagine diversi (`.png`, `.jpg`). Potresti anche inviare il risultato OCR direttamente in un indice di ricerca o in un generatore di PDF. Il modello rimane lo stesso: stream, stitch, recognize.

Hai domande su come scalare a centinaia di riquadri, o hai bisogno di aiuto con la gestione degli errori? Lascia un commento qui sotto, e buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}