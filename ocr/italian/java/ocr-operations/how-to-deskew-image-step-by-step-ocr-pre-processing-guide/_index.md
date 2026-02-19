---
category: general
date: 2026-02-19
description: Impara a raddrizzare l'immagine e rimuovere il rumore per l'OCR. Questo
  tutorial mostra come riconoscere il testo nell'immagine, correggere la rotazione
  dell'immagine e pre‑elaborare l'immagine per l'OCR con Aspose OCR.
draft: false
keywords:
- how to deskew image
- recognize text image
- how to remove noise
- correct image rotation
- preprocess image ocr
language: it
og_description: Come raddrizzare l'immagine e rimuovere il rumore per riconoscere
  rapidamente il testo nell'immagine. Segui questa guida per correggere la rotazione
  dell'immagine e pre‑elaborare l'OCR dell'immagine con Aspose.
og_title: Come raddrizzare l'immagine – Tutorial completo di pre‑elaborazione OCR
tags:
- OCR
- Java
- Image Processing
title: Come raddrizzare l'immagine — Guida passo passo alla pre‑elaborazione OCR
url: /it/java/ocr-operations/how-to-deskew-image-step-by-step-ocr-pre-processing-guide/
---

of markdown, we can translate the title string. Keep the URL unchanged.

Also headings and list items need translation.

We must keep code block placeholders unchanged.

Also there are bold text like **how to deskew image** etc. Should translate but keep the bold markup.

Also there are inline code like `OcrEngine` etc - keep as is.

Also there are bullet points with file paths etc.

We need to be careful with "step-by-step in order". We'll translate each section.

Let's produce the final content.

Start with the three opening shortcodes lines unchanged.

Then heading "# How to Deskew Image — Complete OCR Pre‑Processing Tutorial" translate to Italian: "# Come correggere l'inclinazione di un'immagine — Tutorial completo di pre‑elaborazione OCR". Keep the dash and spacing.

Then paragraph.

We'll translate.

Let's write.

Be careful to preserve markdown formatting.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come correggere l'inclinazione di un'immagine — Tutorial completo di pre‑elaborazione OCR

Ti sei mai chiesto **come correggere l'inclinazione di un'immagine** prima di passarla a un motore OCR? Forse hai scansionato un lotto di ricevute e le pagine sembrano leggermente inclinate, oppure la scansione è piena di punti casuali. È un problema comune: immagini inclinate e rumorose ostacolano il riconoscimento del testo.  

La buona notizia? Puoi raddrizzare (correggere la rotazione dell'immagine) e denoisare (come rimuovere il rumore) in poche righe di Java usando Aspose.OCR. In questa guida percorreremo l’intero flusso: dal caricamento di un PNG ruotato e rumoroso, all’applicazione di deskew + denoise mediano, fino al **riconoscimento del testo nell'immagine** e alla stampa del risultato. Alla fine avrai uno snippet riutilizzabile da inserire in qualsiasi progetto Java.

## Cosa ti serve

- **Java 17** o versioni successive (il codice compila anche con versioni più vecchie, ma 17 è l’ideale).  
- **Aspose.OCR per Java** – puoi scaricare l’ultimo JAR da Maven Central (`com.aspose:aspose-ocr`).  
- Un file immagine sia ruotato sia rumoroso (ad es. `noisy-rotated.png`).  
- Un IDE modesto (IntelliJ, Eclipse o anche VS Code).  

Non servono strumenti di build sofisticati; un semplice `javac` + `java` funziona benissimo.

---

## Passo 1 – Creare l'istanza del motore OCR  

La prima cosa da fare è istanziare un `OcrEngine`. Pensalo come il cervello che più tardi leggerà i caratteri per te.

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // Initialize the OCR engine – this object holds all settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **Consiglio:** Mantieni il motore come singleton se elabori molte immagini; riutilizza buffer interni e velocizza il processo.

## Passo 2 – Abilitare Deskew e Denoise mediano (Come rimuovere il rumore)

Ora diciamo al motore di **correggere la rotazione dell'immagine** e di **come rimuovere il rumore**. Entrambi i filtri sono opzionali, ma insieme migliorano drasticamente l’accuratezza.

```java
        // Turn on preprocessing filters
        ocrEngine.getPreprocessing().setDeskew(true);          // fixes rotation
        ocrEngine.getPreprocessing().setMedianDenoise(true);   // smooths out speckles
```

Perché il denoise mediano? Preserva i bordi (le linee che definiscono i caratteri) mentre elimina i pixel isolati—esattamente ciò che serve per un OCR pulito.

## Passo 3 – Caricare l'immagine da elaborare  

Qui puntiamo il motore al file che necessita di pulizia. `ImageStream.fromFile` legge il PNG in memoria.

```java
        // Load the noisy‑rotated image
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/noisy-rotated.png"));
```

Se la tua immagine si trova su un server remoto, basta fornire un `InputStream`—Aspose lo gestisce senza problemi.

## Passo 4 – Eseguire l'OCR e catturare il testo riconosciuto  

Con la pre‑elaborazione attiva, il motore ora legge l’immagine corretta. La chiamata `recognize()` restituisce un `RecognitionResult` che contiene la stringa estratta.

```java
        // Perform OCR – the engine automatically applies deskew & denoise first
        String recognizedText = ocrEngine.recognize().getText();

        // Show the output
        System.out.println("=== Recognized Text ===");
        System.out.println(recognizedText);
    }
}
```

Dovresti vedere testo pulito e leggibile nella console, anche se l’immagine originale era inclinata e granulosa.

## Passo 5 – Verificare il risultato (Cosa aspettarsi)

Quando tutto funziona, la console stampa qualcosa del genere:

```
=== Recognized Text ===
Invoice #12345
Date: 2026‑02‑15
Total: $1,234.56
```

Se l'output contiene ancora caratteri illeggibili, ricontrolla:

- La risoluzione dell'immagine (≥ 300 dpi è l’ideale).  
- Che il percorso del file sia corretto.  
- Se filtri aggiuntivi (ad es. `setContrastStretch`) potrebbero aiutare.

---

## Opzionale: Conferma visiva con un’immagine di esempio  

Di seguito trovi un piccolo anteprima di una ricevuta ruotata e rumorosa. Nota l’inclinazione—il nostro codice la raddrizzerà per te.

![come correggere l'inclinazione di un'immagine – prima e dopo l'elaborazione](deskew-demo.png "come correggere l'inclinazione di un'immagine")

*Testo alternativo: come correggere l'inclinazione di un'immagine – prima e dopo l'elaborazione.*

---

## Domande frequenti

### Funziona con PDF o solo PNG/JPEG?  
Aspose.OCR può leggere PDF direttamente; basta sostituire `ImageStream.fromFile` con `ImageStream.fromPdf`. Gli stessi flag di pre‑elaborazione si applicano, così otterrai comunque **come correggere l'inclinazione di un'immagine** e **come rimuovere il rumore**.

### E se devo mantenere l'orientamento originale per passaggi successivi?  
Puoi clonare l'immagine prima della pre‑elaborazione:

```java
Image original = ocrEngine.getImage().clone();
ocrEngine.getPreprocessing().apply(); // modifies the internal copy
// Use original later if needed
```

### Posso cambiare manualmente l'angolo di deskew?  
Sì—`setDeskewAngle(double degrees)` ti permette di sovrascrivere l'algoritmo di auto‑rilevamento. Utile quando l'auto‑rilevamento fallisce su rotazioni estreme.

### In che cosa il denoise mediano differisce dal blur gaussiano?  
I filtri mediani sostituiscono ogni pixel con la mediana dei suoi vicini, preservando i bordi. Il blur gaussiano sfuma tutto, potenzialmente smussando i tratti dei caratteri—perciò il filtro mediano è la scelta più sicura per l'OCR.

---

## Conclusioni  

In questo tutorial abbiamo trattato **come correggere l'inclinazione di un'immagine**, dimostrato **come rimuovere il rumore**, e mostrato come **riconoscere il testo nell'immagine** usando la pre‑elaborazione integrata di Aspose OCR. Abilitando `setDeskew(true)` e `setMedianDenoise(true)`, correggi automaticamente la rotazione dell’immagine e rimuovi i punti, trasformando una scansione confusa in una stringa di testo pulita.  

Sentiti libero di sperimentare: prova diverse strategie di denoise, elabora PDF, o concatenare più immagini in un ciclo. Lo stesso schema—motore → pre‑elaborazione → riconoscimento—vale per ogni scenario, fornendo una solida base per qualsiasi pipeline OCR.

**Passi successivi** da esplorare:

- **Elaborazione batch** – itera su una cartella di immagini e scrivi ogni risultato in un file `.txt`.  
- **Pacchetti linguistici** – carica un dizionario specifico per migliorare l'accuratezza su testi non‑inglesi.  
- **Filtri avanzati** – come `setContrastStretch` o `setBinarization` per scansioni a basso contrasto.  

Hai altre domande? Lascia un commento, e buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}