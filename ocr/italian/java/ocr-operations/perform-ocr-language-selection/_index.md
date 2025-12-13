---
date: 2025-12-13
description: Scopri come estrarre il testo da un'immagine usando Aspose.OCR per Java
  con selezione della lingua. Questo tutorial passo‑passo di Aspose OCR per Java mostra
  una configurazione OCR precisa.
linktitle: How to Extract Text from Image with Language Selection Using Aspose.OCR
second_title: Aspose.OCR Java API
title: Come estrarre testo da un'immagine con selezione della lingua usando Aspose.OCR
url: /it/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come Estrarre Testo da Immagine con Selezione della Lingua Utilizzando Aspose.OCR

## Introduzione

Estrarre testo da file immagine è una necessità comune, sia che tu stia digitalizzando documenti scannerizzati, elaborando ricevute o creando archivi ricercabili. Aspose.OCR per Java rende questo compito semplice e ti offre un controllo dettagliato sulla selezione della lingua, la correzione dello skew e le aree di riconoscimento. In questo tutorial percorreremo un esempio completo e pratico che mostra **come estrarre testo da un'immagine** con un'impostazione linguistica specifica, così potrai integrare un OCR affidabile nelle tue applicazioni Java oggi stesso.

## Risposte Rapide
- **Quale libreria gestisce l'OCR in Java?** Aspose.OCR per Java  
- **Quale impostazione seleziona la lingua?** `settings.setLanguage(Language.Eng)` (o qualsiasi lingua supportata)  
- **È necessaria una licenza per lo sviluppo?** Una licenza di valutazione gratuita funziona per i test; è richiesta una licenza commerciale per la produzione.  
- **Posso limitare l'OCR a una regione dell'immagine?** Sì, usa `RecognitionSettings.setRecognitionAreas()` con rettangoli.  
- **Qual è il tempo di esecuzione tipico?** Alcuni secondi per pagina su un laptop standard, a seconda delle dimensioni dell'immagine e della complessità della lingua.

## Cos'è “estrarre testo da immagine”?
Estrarre testo da immagine (OCR) converte la rappresentazione visiva dei caratteri in stringhe leggibili dalla macchina. Questo consente ricerche, analisi e flussi di lavoro di estrazione dati che altrimenti richiederebbero una trascrizione manuale.

## Perché usare Aspose.OCR con selezione della lingua?
- **Supporto multilingue** – Scegli la lingua o le lingue presenti nella tua immagine per aumentare la precisione.  
- **Controllo fine‑tuned** – Regola lo skew, definisci le aree di riconoscimento e imposta il comportamento di auto‑skew.  
- **API Java pura** – Nessuna dipendenza nativa, facile da integrare in qualsiasi progetto Java.  
- **Dati di risultato ricchi** – Ottieni testo semplice, JSON, rettangoli di delimitazione e avvisi in una sola chiamata.

## Prerequisiti

Prima di iniziare, assicurati di avere:

- **Java Development Kit (JDK)** installato (JDK 8 o successivo).  
- **Libreria Aspose.OCR per Java** – scaricala dal sito ufficiale [qui](https://reference.aspose.com/ocr/java/).  
- Un file immagine che contenga il testo da estrarre, ad esempio `p3.png`.

## Importare i Pacchetti

Nel tuo file sorgente Java, includi le classi Aspose.OCR necessarie e le utility Java standard:

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

## Guida Passo‑Passo

### Passo 1: Configura la Directory del Documento

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

Sostituisci `"Your Document Directory"` con il percorso assoluto dove risiede `p3.png`.

### Passo 2: Definisci il Percorso dell'Immagine

```java
// The image path
String file = dataDir + "p3.png";
```

Assicurati che la variabile `file` punti all'immagine esatta che intendi elaborare.

### Passo 3: Crea l'Istanza dell'API Aspose.OCR

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

L'oggetto `AsposeOCR` ti dà accesso a tutte le operazioni OCR.

### Passo 4: Imposta le Opzioni di Riconoscimento (Selezione della Lingua)

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

1. Disabilitiamo l'auto‑skew perché forniamo un valore di skew manuale.  
2. Definiamo una regione rettangolare (`RecognitionAreas`) per limitare l'OCR alla parte dell'immagine che contiene effettivamente testo.  
3. Impostiamo la **lingua** su Inglese (`Language.Eng`). Cambiala in `Language.Fra`, `Language.Spa`, ecc., a seconda dell'immagine di origine.

### Passo 5: Esegui l'OCR e Recupera i Risultati

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

La chiamata `RecognizePage` avvia il motore OCR usando l'immagine e le impostazioni definite. Il risultato è memorizzato in un oggetto `RecognitionResult`.

### Passo 6: Stampa e Utilizza i Risultati

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
- Le coordinate dei rettangoli di delimitazione.  
- Una rappresentazione JSON per una facile elaborazione successiva.  
- L'angolo di skew rilevato e eventuali avvisi.

Ora puoi alimentare `result.recognitionText` nella tua logica di business—memorizzarlo, indicizzarlo o passarlo a un altro servizio.

## Problemi Comuni e Soluzioni

| Problema | Causa | Soluzione |
|----------|-------|-----------|
| **Caratteri spazzatura** | Lingua errata selezionata | Imposta l'enumerazione `Language` corretta (es. `Language.Fra` per il francese). |
| **Nessun testo restituito** | L'area di riconoscimento non copre il testo | Regola le coordinate del `Rectangle` o rimuovi `RecognitionAreas` per elaborare l'intera immagine. |
| **Prestazioni lente** | Immagine molto grande o ad alta risoluzione | Ridimensiona l'immagine prima dell'OCR o aumenta l'allocazione di memoria per la JVM. |
| **Avvisi su formato non supportato** | Formato immagine non riconosciuto | Converti l'immagine in PNG, JPEG o TIFF prima dell'elaborazione. |

## Domande Frequenti

**D: Posso riconoscere più lingue in una singola chiamata OCR?**  
R: Sì. Usa `settings.setLanguage(Language.Eng | Language.Fra)` per abilitare il riconoscimento multilingue.

**D: Quali formati immagine supporta Aspose.OCR?**  
R: PNG, JPEG, BMP, TIFF, GIF e diversi altri. Basta fornire il percorso corretto del file.

**D: Esiste un limite di dimensione per l'immagine?**  
R: Non c'è un limite rigido, ma immagini molto grandi aumentano l'uso di memoria e il tempo di elaborazione. Considera di ridimensionare i file di grandi dimensioni.

**D: Come ottengo una licenza di produzione?**  
R: Acquista una licenza dal sito Aspose e applicala tramite la classe `License` come mostrato nella documentazione di Aspose.

**D: Posso estrarre testo direttamente da una pagina PDF?**  
R: Non direttamente con Aspose.OCR. Converti prima la pagina PDF in immagine (ad esempio usando Aspose.PDF) e poi esegui l'OCR.

## Conclusione

Ora hai visto come **estrarre testo da immagine** usando Aspose.OCR per Java, selezionando la lingua appropriata e limitando il riconoscimento a regioni specifiche. Questo approccio offre un OCR accurato e ad alte prestazioni che può essere integrato in qualsiasi flusso di lavoro basato su Java—da sistemi di gestione documentale a pipeline di acquisizione dati.

---

**Ultimo aggiornamento:** 2025-12-13  
**Testato con:** Aspose.OCR 24.11 per Java  
**Autore:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}