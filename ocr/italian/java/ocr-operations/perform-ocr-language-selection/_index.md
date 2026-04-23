---
date: 2026-02-12
description: Scopri come eseguire l'OCR del testo delle immagini con selezione della
  lingua usando Aspose.OCR per Java. Questa guida passo passo copre l'estrazione del
  testo in Java, la correzione dell'inclinazione OCR e molto altro.
linktitle: How to OCR Image Text with Language Using Aspose.OCR
second_title: Aspose.OCR Java API
title: Come fare OCR del testo di un'immagine con lingua usando Aspose.OCR
url: /it/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come eseguire OCR del testo di un'immagine con lingua usando Aspose.OCR

## Introduzione

Estrarre testo da file immagine è una necessità comune, sia che tu stia digitalizzando documenti scansionati, elaborando ricevute o creando archivi ricercabili. In questo tutorial ti guideremo attraverso un esempio completo e pratico che mostra **come eseguire OCR del testo di un'immagine** con un'impostazione di lingua specifica, così potrai integrare un OCR affidabile nelle tue applicazioni Java oggi. Vedrai anche come gestire la correzione di inclinazione (skew) dell'OCR e il riconoscimento basato su regioni per una precisione ottimale.

## Risposte rapide
- **Quale libreria gestisce l'OCR in Java?** Aspose.OCR for Java  
- **Quale impostazione seleziona la lingua?** `settings.setLanguage(Language.Eng)` (o qualsiasi lingua supportata)  
- **È necessaria una licenza per lo sviluppo?** Una licenza di valutazione gratuita funziona per i test; è richiesta una licenza commerciale per la produzione.  
- **Posso limitare l'OCR a una regione dell'immagine?** Sì, usa `RecognitionSettings.setRecognitionAreas()` con rettangoli.  
- **Qual è il tempo di esecuzione tipico?** Alcuni secondi per pagina su un laptop standard, a seconda della dimensione dell'immagine e della complessità della lingua.

## Come eseguire OCR del testo di un'immagine con selezione della lingua
In questa sezione rispondiamo alla domanda fondamentale **come eseguire OCR** su un'immagine quando conosci la lingua del testo. Selezionare la lingua corretta migliora notevolmente la precisione del riconoscimento perché il motore OCR può applicare dizionari e modelli di caratteri specifici per la lingua.

### Perché è importante
- **Maggiore precisione** – i modelli specifici per lingua riducono gli errori di riconoscimento.  
- **Miglioramento delle prestazioni** – il motore salta i controlli di lingua non necessari.  
- **Gestione migliore dei segni diacritici** – francese, spagnolo, tedesco, ecc., vengono riconosciuti correttamente quando si utilizza l'enumerazione `Language` corrispondente.

## Cos'è “estrarre testo da un'immagine”?
Estrarre testo da un'immagine (OCR) converte la rappresentazione visiva dei caratteri in stringhe leggibili dalla macchina. Questo consente ricerche, analisi e flussi di lavoro di estrazione dati che altrimenti richiederebbero una trascrizione manuale.

## Perché usare Aspose.OCR con selezione della lingua?
- **Supporto multilingue** – Scegli la lingua/e esatta/e presente/i nella tua immagine per aumentare la precisione.  
- **Controllo fine‑tuned** – Regola l'inclinazione, definisci le aree di riconoscimento e imposta il comportamento di auto‑skew.  
- **Pure Java API** – Nessuna dipendenza nativa, facile da integrare in qualsiasi progetto Java.  
- **Dati di risultato ricchi** – Ottieni testo semplice, JSON, rettangoli di delimitazione e avvisi in una sola chiamata.

## Prerequisiti

Prima di iniziare, assicurati di avere:

- **Java Development Kit (JDK)** installato (JDK 8 o successivo).  
- **Libreria Aspose.OCR for Java** – scaricala dal sito ufficiale [qui](https://reference.aspose.com/ocr/java/).  
- Un file immagine che contiene il testo da estrarre, ad esempio `p3.png`.

## Importare i pacchetti

Nel tuo file sorgente Java, includi le classi Aspose.OCR necessarie e le utility standard di Java:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Guida passo‑passo

### Passo 1: Configura la tua directory dei documenti

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

Sostituisci `"Your Document Directory"` con il percorso assoluto dove si trova `p3.png`.

### Passo 2: Definisci il percorso dell'immagine

```java
// The image path
String file = dataDir + "p3.png";
```

Assicurati che la variabile `file` punti all'immagine esatta che intendi elaborare.

### Passo 3: Crea l'istanza dell'API Aspose.OCR

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

L'oggetto `AsposeOCR` ti dà accesso a tutte le operazioni OCR.

### Passo 4: Imposta le opzioni di riconoscimento (selezione della lingua)

```java
// Set recognition options
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

Qui:

1. Disabilitiamo l'auto‑skew perché forniamo un valore di inclinazione manuale.  
2. Definiamo una regione rettangolare (`RecognitionAreas`) per limitare l'OCR alla parte dell'immagine che contiene effettivamente testo.  
3. Impostiamo la **lingua** su English (`Language.Eng`). Cambia questo in `Language.Fra`, `Language.Spa`, ecc., a seconda della tua immagine di origine.

### Passo 5: Esegui l'OCR e recupera i risultati

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

La chiamata `RecognizePage` esegue il motore OCR usando l'immagine e le impostazioni che hai definito. Il risultato è memorizzato in un oggetto `RecognitionResult`.

### Passo 6: Stampa e utilizza i risultati

```java
// Print result
System.out.println("Result: \n" + result.recognitionText + "\n\n");
for (String n : result.recognitionAreasText) {
    System.out.println(n);
}
for (Rectangle n : result.recognitionAreasRectangles) {
    System.out.println(n.height + ":" + n.width + ":" + n.x + ":" + n.y);
}
System.out.println("\nJSON:" + result.GetJson());
System.out.println("Angle:" + result.skew);
for (String n : result.warnings) {
    System.out.println(n);
}

System.out.println("OCROperationWithLanguageSelection: execution complete");
```

L'output della console mostra:

- Il testo estratto completo (`recognitionText`).  
- Il testo per ciascun rettangolo definito (`recognitionAreasText`).  
- Le coordinate del rettangolo di delimitazione.  
- Una rappresentazione JSON per una facile elaborazione a valle.  
- L'angolo di inclinazione rilevato e eventuali avvisi.

Ora puoi inserire `result.recognitionText` nella tua logica di business — archiviarlo, indicizzarlo o passarlo a un altro servizio.

## Problemi comuni e soluzioni

| Problema | Causa | Soluzione |
|----------|-------|-----------|
| **Caratteri spazzatura** | Lingua errata selezionata | Imposta l'enumerazione `Language` corretta (ad es., `Language.Fra` per il francese). |
| **Nessun testo restituito** | L'area di riconoscimento non copre il testo | Regola le coordinate del `Rectangle` o rimuovi `RecognitionAreas` per elaborare l'intera immagine. |
| **Prestazioni lente** | Immagine molto grande o ad alta risoluzione | Ridimensiona l'immagine prima dell'OCR o aumenta l'allocazione di memoria per la JVM. |
| **Avvisi su formato non supportato** | Formato immagine non riconosciuto | Converti l'immagine in PNG, JPEG o TIFF prima dell'elaborazione. |

## FAQ

**D: Posso riconoscere più lingue in una singola chiamata OCR?**  
R: Sì. Usa `settings.setLanguage(Language.Eng | Language.Fra)` per abilitare il riconoscimento multilingue.

**D: Quali formati immagine supporta Aspose.OCR?**  
R: PNG, JPEG, BMP, TIFF, GIF e diversi altri. Basta fornire il percorso file corretto.

**D: Esiste un limite di dimensione per l'immagine?**  
R: Non c'è un limite rigido, ma immagini molto grandi aumentano l'uso di memoria e il tempo di elaborazione. Considera di ridimensionare i file di grandi dimensioni.

**D: Come ottengo una licenza di produzione?**  
R: Acquista una licenza dal sito web di Aspose e applicala tramite la classe `License` come mostrato nella documentazione di Aspose.

**D: Posso estrarre testo da una pagina PDF direttamente?**  
R: Non direttamente con Aspose.OCR. Converti prima la pagina PDF in un'immagine (ad es., usando Aspose.PDF) e poi esegui l'OCR.

## Conclusione

Hai ora visto come **estrarre testo da un'immagine** usando Aspose.OCR per Java selezionando la lingua appropriata e limitando il riconoscimento a regioni specifiche. Questo approccio fornisce un OCR accurato e ad alte prestazioni che può essere integrato in qualsiasi flusso di lavoro basato su Java — dai sistemi di gestione documentale alle pipeline di acquisizione dati. Pronto a procedere? Prova a cambiare l'enumerazione della lingua, sperimenta con diverse aree di riconoscimento e integra i risultati nella logica della tua applicazione.

---

**Ultimo aggiornamento:** 2026-02-12  
**Testato con:** Aspose.OCR 24.11 for Java  
**Autore:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}