---
category: general
date: 2026-04-26
description: Come migliorare l'accuratezza OCR rimuovendo il rumore, raddrizzando
  le immagini e convertendo l'immagine in testo. Impara passo passo con Aspose OCR.
draft: false
keywords:
- how to improve ocr
- how to remove noise
- how to extract text
- how to deskew image
- convert image to text
language: it
og_description: Come migliorare la precisione OCR in Java—rimuovere il rumore, correggere
  l'inclinazione delle immagini e convertire l'immagine in testo usando Aspose OCR.
og_title: Come migliorare l'OCR con la preelaborazione avanzata in Java
tags:
- OCR
- Java
- Image Processing
title: Come migliorare l'OCR con la preelaborazione avanzata in Java
url: /it/java/advanced-ocr-techniques/how-to-improve-ocr-with-advanced-preprocessing-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come migliorare l'OCR con la pre‑elaborazione avanzata in Java

Ti sei mai chiesto **come migliorare l'OCR** quando le tue scansioni sembrano un caos?  Forse il documento è ruotato, pieno di artefatti granulosi, o semplicemente ha un contrasto troppo basso per essere letto.  La buona notizia è che una serie di passaggi di pre‑elaborazione può trasformare un'immagine traballante in testo pulito e leggibile dalla macchina—niente magia.

In questo tutorial vedremo **come rimuovere il rumore**, **come raddrizzare l'immagine** e infine **come estrarre il testo** (o *convertire immagine in testo*) usando Aspose OCR per Java.  Alla fine avrai un programma pronto all'uso che offre una precisione OCR notevolmente migliore.

## Cosa ti serve

- **Java Development Kit (JDK) 11+** – qualsiasi versione recente funziona.
- **Aspose.OCR for Java** library (la versione di prova gratuita funziona per i test).
- Un'immagine di esempio che è inclinata, rumorosa o a basso contrasto (ad es., `skewed_noisy.jpg`).
- Un IDE o un semplice editor di testo; manterremo il codice puro e semplice.

> **Consiglio professionale:** Se usi Maven, aggiungi la dipendenza Aspose OCR al tuo `pom.xml`.  Se preferisci Gradle, le stesse coordinate si applicano.

## Passo 1: Configura il motore Aspose OCR – Fondamenti di *Come migliorare l'OCR*

Per prima cosa, crea un'istanza di `OcrEngine`.  Questo oggetto è il punto di ingresso per ogni operazione OCR.

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

*Perché è importante:* Il motore contiene tutte le impostazioni che determinano come Aspose interpreterà l'immagine.  Senza di esso, non puoi abilitare nessuno dei trucchi di pre‑elaborazione che effettivamente **come migliorare l'OCR**.

## Passo 2: Abilita la pre‑elaborazione avanzata delle immagini – Il nucleo di *Come migliorare l'OCR*

Ora attiviamo i quattro interruttori di pre‑elaborazione che rispondono direttamente alla domanda **come migliorare l'OCR**: raddrizzamento, riduzione del rumore, estensione del contrasto e binarizzazione.

```java
        // Step 2: Turn on preprocessing features
        ImagePreprocessingSettings preprocessing = ocrEngine.getPreprocessingSettings();
        preprocessing.setDeskew(true);           // how to deskew image
        preprocessing.setDenoise(true);         // how to remove noise
        preprocessing.setContrastStretch(true); // boost contrast automatically
        preprocessing.setBinarize(true);        // Otsu binarization for clean black‑white
```

*Spiegazione:*  
- **Deskew** ruota automaticamente l'immagine di nuovo a 0° in modo che i caratteri siano allineati orizzontalmente.  
- **Denoise** applica un filtro che smussa i granelli—esattamente ciò di cui hai bisogno quando chiedi *come rimuovere il rumore*.  
- **Contrast stretch** espande la gamma tonale, facendo risaltare le lettere deboli.  
- **Binarize** forza ogni pixel a nero o bianco, un prerequisito classico per l'OCR.

## Passo 3: Carica l'immagine problematica – Preparazione per *Come estrarre il testo*

```java
        // Step 3: Point the engine at your source image
        ocrEngine.setImage("YOUR_DIRECTORY/skewed_noisy.jpg");
```

Sostituisci `YOUR_DIRECTORY` con il percorso reale sulla tua macchina.  L'immagine può essere in formato JPEG, PNG, BMP o TIFF—Aspose OCR supporta tutti questi formati.

## Passo 4: Esegui l'OCR e *Converti immagine in testo*

```java
        // Step 4: Perform OCR and capture the result
        String recognizedText = ocrEngine.recognize().getText();
```

A questo punto il motore ha applicato la pipeline di pre‑elaborazione, quindi ha eseguito il riconoscimento dei caratteri.  La chiamata `recognize()` restituisce un oggetto `OcrResult`; chiamare `getText()` estrae la stringa di testo semplice—*esattamente come convertire immagine in testo* in Java.

## Passo 5: Visualizza il risultato pulito – Verifica *Come estrarre il testo*

```java
        // Step 5: Show the OCR output
        System.out.println("Result after advanced preprocessing:\n" + recognizedText);
    }
}
```

Quando esegui il programma, dovresti vedere qualcosa del genere:

```
Result after advanced preprocessing:
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

Se l'immagine originale era una scansione sfocata e ruotata, nota come l'output è ora leggibile e correttamente ordinato.  Questo è il beneficio tangibile del seguire la checklist **come migliorare l'OCR**.

---

## Come rimuovere il rumore – Un'analisi più approfondita

Il rumore appare spesso come granelli o macchie casuali, specialmente nelle scansioni a bassa risoluzione.  Il flag `setDenoise(true)` attiva un filtro mediano che sostituisce ogni pixel con il valore mediano dei suoi vicini.  In pratica, questo leviga le macchie scure isolate preservando i bordi.

**Quando regolare:** Se le tue immagini di origine sono già pulite, puoi disabilitare la riduzione del rumore per velocizzare l'elaborazione.  Al contrario, per foto molto granulose, potresti combinare la riduzione del rumore di Aspose con un pre‑filtro OpenCV personalizzato per maggiore potenza.

## Come raddrizzare l'immagine – Ruotare di nuovo alla realtà

L'algoritmo di deskew analizza la linea di base del testo e calcola l'angolo di rotazione ottimale.  Funziona al meglio quando almeno una riga di testo è chiaramente visibile.  Se l'immagine contiene solo grafica, considera di ruotarla manualmente prima di passarla ad Aspose.

**Caso limite:** Alcune lingue (ad es., l'arabo) hanno orientamento da destra a sinistra.  Deskew funziona comunque, ma potresti dover impostare il suggerimento di lingua (`ocrEngine.setLanguage(OcrLanguage.Arabic)`) per evitare rotazioni errate.

## Come estrarre il testo – Oltre le semplici stringhe

Se ti serve più del semplice testo grezzo—ad esempio riquadri di delimitazione, punteggi di confidenza o posizionamento a livello di parola—usa l'API più ricca `OcrResult`:

```java
OcrResult result = ocrEngine.recognize();
for (OcrWord word : result.getWords()) {
    System.out.printf("Word: %s, Confidence: %.2f%%, Box: %s%n",
        word.getText(), word.getConfidence() * 100, word.getRectangle());
}
```

Questo frammento mostra **come estrarre il testo** insieme ai metadati, utile per creare PDF ricercabili o annotare documenti.

## Convertire immagine in testo in Java – Mettere tutto insieme

L'esempio completo e eseguibile combina tutto ciò di cui abbiamo parlato:

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {
        // Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Enable preprocessing (how to improve OCR)
        ImagePreprocessingSettings preprocessing = ocrEngine.getPreprocessingSettings();
        preprocessing.setDeskew(true);           // how to deskew image
        preprocessing.setDenoise(true);         // how to remove noise
        preprocessing.setContrastStretch(true);
        preprocessing.setBinarize(true);

        // Load the image you want to convert image to text from
        ocrEngine.setImage("YOUR_DIRECTORY/skewed_noisy.jpg");

        // Perform OCR
        String recognizedText = ocrEngine.recognize().getText();

        // Output the result
        System.out.println("Result after advanced preprocessing:\n" + recognizedText);
    }
}
```

Salva questo come `PreprocessDemo.java`, compila con `javac` e esegui con `java`.  Vedrai il testo pulito stampato sulla console.

---

## Problemi comuni e come evitarli

| Sintomo | Probabile causa | Soluzione |
|---------|----------------|-----------|
| Output vuoto | Percorso immagine errato o formato non supportato | Verifica il percorso, usa il percorso assoluto, assicurati che il file sia JPEG/PNG/TIFF |
| Caratteri illeggibili | Pre‑elaborazione disabilitata o lingua non impostata | Abilita `setDeskew`, `setDenoise` e imposta `ocrEngine.setLanguage(OcrLanguage.English)` |
| Prestazioni lente su grandi batch | Tutti e quattro i passaggi di pre‑elaborazione su ogni immagine | Disabilita `setContrastStretch` o `setBinarize` se non necessari, oppure elabora le immagini in thread paralleli |

---

## Prossimi passi – Estendere il tuo pipeline OCR

Ora che sai **come migliorare l'OCR**, considera queste idee successive:

- **Elaborazione batch:** Scorri una cartella di immagini, applicando le stesse impostazioni a ogni file.
- **Post‑elaborazione:** Usa espressioni regolari per pulire gli errori OCR comuni (ad es., “0” vs “O”).
- **Integrazione con PDF:** Combina Aspose OCR con Aspose PDF per incorporare il testo estratto direttamente in PDF ricercabili.
- **Supporto linguistico:** Cambia `ocrEngine.setLanguage(OcrLanguage.Spanish)` (o qualsiasi lingua supportata) per gestire documenti multilingue.

## Conclusione

Abbiamo coperto la risposta completa a **come migliorare l'OCR** in Java abilitando deskew, denoise, contrast stretch e binarizzazione—tutto all'interno di `OcrEngine` di Aspose.  Ora sai **come rimuovere il rumore**, **come raddrizzare l'immagine**, **come estrarre il testo**, e persino **convertire immagine in testo** in un unico programma conciso.  Gioca con le impostazioni, prova con le tue scansioni e vedrai un notevole aumento della precisione di riconoscimento.

Hai altre domande sui trucchi OCR o hai bisogno di aiuto per integrare questo in un'applicazione più grande?  Lascia un commento qui sotto, e buona programmazione!

![Come migliorare la pre‑elaborazione OCR](/images/ocr-preprocess-example.png "come migliorare l'ocr")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}