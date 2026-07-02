---
category: general
date: 2026-06-28
description: Impara un esempio Aspose OCR Java per estrarre testo da progetti Java
  di immagini e impostare il limite di memoria GPU per risultati più rapidi.
draft: false
keywords:
- aspose ocr java example
- extract text from image java
- set gpu memory limit
- gpu accelerated OCR Java
- Aspose OCR licensing
language: it
og_description: Esempio Aspose OCR Java che mostra come estrarre testo da un'immagine
  con codice Java impostando il limite di memoria GPU per prestazioni ottimali.
og_title: Esempio OCR Java di Aspose – Estrarre Testo Rapidamente con Accelerazione
  GPU
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Learn an Aspose OCR Java example to extract text from image Java projects
    and set GPU memory limit for faster results.
  headline: Aspose OCR Java Example – Extract Text from Image with GPU
  type: TechArticle
tags:
- Aspose OCR
- Java
- GPU
title: Esempio Aspose OCR Java – Estrai testo da immagine con GPU
url: /it/java/advanced-ocr-techniques/aspose-ocr-java-example-extract-text-from-image-with-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esempio Aspose OCR Java – Estrarre Testo da Immagine con GPU

Ti sei mai chiesto come **estrarre testo da immagine Java** applicazioni senza sovraccaricare la CPU? Non sei l'unico. In molti scenari reali—pensa alla scansione di ricevute, alla verifica di ID o all'archiviazione di documenti in blocco—il collo di bottiglia è il motore OCR stesso.  

Buone notizie: questo **esempio Aspose OCR Java** ti guida passo passo attraverso un programma completo, pronto‑all'uso, che sfrutta l'accelerazione GPU e mostra anche come **impostare il limite di memoria GPU** affinché il tuo server rimanga sereno. Alla fine di questa guida avrai una classe Java funzionante che legge un file immagine, esegue l'OCR sulla GPU e stampa il testo riconosciuto nella console. Niente riferimenti vaghi, solo codice concreto e spiegazioni chiare.

Copriamo tutto, dalla licenza alla messa a punto della GPU, quindi che tu sia uno sviluppatore Java esperto o che stia appena iniziando con la computer‑vision, troverai valore qui. L'unico prerequisito è un ambiente di sviluppo Java (JDK 8 o superiore) e l'accesso a una GPU compatibile con CUDA o OpenCL.

---

## Prerequisiti

- **Java Development Kit (JDK) 8+** – puoi scaricarlo da Oracle o adottare OpenJDK.  
- **Aspose.OCR for Java** library – ottieni il JAR dal sito Aspose o da Maven Central.  
- **Un file di licenza Aspose OCR valido** (`Aspose.OCR.Java.lic`). La versione di prova gratuita funziona per i test, ma la licenza rimuove i watermark di valutazione.  
- **GPU con supporto CUDA o OpenCL** – la demo rileva automaticamente la modalità migliore, ma è necessario installare i driver.  
- **Un'immagine per il test** – un PNG o JPEG chiaro di una ricevuta, di un cartello o di qualsiasi testo stampato.  

Se qualcuno di questi ti è sconosciuto, non preoccuparti. I passaggi seguenti ti indicheranno i link di download esatti e mostreranno dove posizionare i file.

## Passo 1: Esempio Aspose OCR Java – Configurare il Progetto

Per prima cosa, crea un nuovo progetto Maven (o una semplice cartella se preferisci usare `javac`). Aggiungi la dipendenza Aspose OCR al tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Use the latest version -->
</dependency>
```

> **Consiglio:** Maven scaricherà tutte le dipendenze transitive, incluse le librerie di supporto GPU, così non dovrai cercare JAR aggiuntivi.

Posiziona il tuo file `Aspose.OCR.Java.lic` nella radice del progetto (o in qualsiasi cartella a cui farai riferimento più tardi). L'**esempio aspose ocr java** che stiamo creando si aspetta che il percorso della licenza sia `"Aspose.OCR.Java.lic"`.

## Passo 2: Applicare la Licenza Aspose OCR

Il passaggio della licenza è cruciale—senza di essa, il motore OCR funziona in modalità di valutazione e aggiunge un watermark all'output. Ecco il codice minimo di cui hai bisogno:

```java
import com.aspose.ocr.*;

public class LicenseUtil {
    public static void applyLicense() throws Exception {
        License license = new License();
        // Adjust the path if your license file lives elsewhere
        license.setLicense("Aspose.OCR.Java.lic");
        System.out.println("Aspose OCR license applied successfully.");
    }
}
```

Eseguire questo una volta all'inizio della tua applicazione garantisce che **tutte le successive chiamate OCR** siano completamente licenziate.

## Passo 3: Configurare l'Accelerazione GPU – Impostare il Limite di Memoria GPU

Ora arriva la parte divertente: dire ad Aspose di usare la GPU e opzionalmente **impostare il limite di memoria GPU**. La libreria include `GpuEngineOptions`, che ti permette di attivare la modalità GPU, scegliere un dispositivo e limitare l'uso della memoria. Limitare la memoria è utile su server condivisi dove non vuoi che il tuo lavoro OCR consumi tutta la GPU.

```java
import com.aspose.ocr.gpu.*;

public class GpuConfig {
    public static GpuEngineOptions createOptions() {
        GpuEngineOptions gpuOptions = new GpuEngineOptions();
        gpuOptions.setEnableGpu(true);          // turn on GPU acceleration
        gpuOptions.setDeviceId(0);              // use the first GPU device
        gpuOptions.setMemoryLimitMb(2048);      // **set GPU memory limit** to 2 GB
        System.out.println("GPU options configured (memory limit = 2048 MB).");
        return gpuOptions;
    }
}
```

> **Perché impostare un limite di memoria?** Se i tuoi compiti OCR coinvolgono immagini molto grandi o esegui molti lavori concorrenti, la GPU può esaurire rapidamente la VRAM, causando crash. Limitando l'allocazione, mantieni il processo entro limiti sicuri e permetti ad altri carichi di lavoro di coesistere pacificamente.

## Passo 4: Estrarre Testo da Immagine Java – Caricamento dell'Immagine

Con licenza e impostazioni GPU sistemate, possiamo finalmente **estrarre testo da immagine Java**. Il frammento seguente crea un `OcrEngine` usando le opzioni GPU, carica un file immagine ed esegue il riconoscimento.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply the license
        LicenseUtil.applyLicense();

        // 2️⃣ Set up GPU options (including memory limit)
        GpuEngineOptions gpuOptions = GpuConfig.createOptions();

        // 3️⃣ Create the OCR engine with GPU acceleration
        OcrEngine ocrEngine = new OcrEngine(gpuOptions);

        // 4️⃣ Load the image you want to process
        OcrInput ocrInput = new OcrInput();
        // Replace the placeholder with your actual image path
        ocrInput.add("YOUR_DIRECTORY/receipt.png");

        // 5️⃣ Perform OCR recognition
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // 6️⃣ Output the recognized text
        System.out.println("Recognized Text (GPU):");
        System.out.println(ocrResult.getText());
    }
}
```

**Punti chiave** in questo **esempio aspose ocr java**:

- `OcrInput.add()` può accettare più immagini; il motore le elaborerà sequenzialmente.  
- `ocrResult.getText()` restituisce una stringa di testo semplice, preservando le interruzioni di riga ma non le informazioni di layout.  
- L'intera pipeline gira sulla GPU, che può essere **5‑10× più veloce** rispetto all'elaborazione solo CPU per immagini ad alta risoluzione.

## Passo 5: Eseguire la Demo e Verificare l'Output

Compila ed esegui il programma:

```bash
mvn compile exec:java -Dexec.mainClass=GpuOcrDemo
```

Se tutto è configurato correttamente, dovresti vedere qualcosa di simile:

```
Aspose OCR license applied successfully.
GPU options configured (memory limit = 2048 MB).
Recognized Text (GPU):
Item   Qty   Price
Apple   2    $1.20
Banana  5    $0.75
Total          $5.85
```

Il testo esatto dipende dalla tua immagine, ma la cosa importante è che la console stampi **il testo riconosciuto** senza il watermark “Evaluation version”. Se incontri un errore `CUDA driver not found`, verifica che i driver della GPU siano aggiornati e che il toolkit CUDA sia nel percorso di sistema.

## Problemi Comuni & Come Evitarli

| Sintomo | Causa Probabile | Soluzione |
|---------|-----------------|-----------|
| `OutOfMemoryError: CUDA out of memory` | Memoria GPU superata | Riduci `setMemoryLimitMb` (es., 1024) o elabora blocchi di immagine più piccoli. |
| `LicenseException` | File di licenza mancante o percorso errato | Assicurati che `Aspose.OCR.Java.lic` sia raggiungibile e che il percorso corrisponda. |
| Nessun testo restituito | Immagine troppo sfocata o spazio colore errato | Pre‑elabora l'immagine (aumenta il contrasto, converti in scala di grigi) prima di passarla all'OCR. |
| GPU non utilizzata | `setEnableGpu(false)` o driver mancante | Verifica `gpuOptions.setEnableGpu(true)` e reinstalla i driver GPU. |

## Estendere l'Esempio

Ora che hai un solido **esempio aspose ocr java**, potresti voler:

- **Elaborare in batch una cartella** – iterare sui file e memorizzare i risultati in un database.  
- **Rilevare la lingua** – usa `ocrEngine.setLanguage(OcrLanguage.English)` o aggiungi più lingue.  
- **Applicare post‑processing** – pulire la stringa grezza con regex o inviarla a un correttore ortografico.  

Tutte queste estensioni riutilizzano lo stesso codice di licenza e configurazione GPU, quindi devi aggiungere solo la logica di business.

## Considerazioni Finali

Hai appena visto un **esempio aspose ocr java** completo che **estrae testo da immagine Java** applicazioni impostando **il limite di memoria GPU** per prestazioni robuste. Le idee fondamentali—licenziare in anticipo, configurare la GPU, caricare l'immagine, leggere il testo—sono riutilizzabili in innumerevoli progetti, dagli scanner di ricevute ai sistemi di inserimento automatico di moduli.

Da qui, sentiti libero di sperimentare con diversi valori di `GpuEngineOptions`, provare immagini più grandi o integrare il passaggio OCR in un microservizio Spring Boot. Il cielo è il limite, e grazie all'accelerazione GPU, il limite è molto più alto di prima.

Hai domande o hai bisogno di aiuto per regolare le impostazioni di memoria per il tuo hardware specifico? Lascia un commento qui sotto, e buona programmazione!

![Diagramma esempio Aspose OCR Java che mostra il flusso da input immagine → OCR accelerato GPU → output testo](https://example.com/images/aspose-ocr-java-example-diagram.png "diagramma esempio aspose ocr java")

## Cosa Dovresti Imparare Dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come impostare la licenza e verificare la licenza Aspose.OCR in Java](/ocr/english/java/ocr-basics/set-license/)
- [Estrarre testo da immagine Java con modalità Rileva Aree di Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Convertire immagine in testo in Java usando Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}