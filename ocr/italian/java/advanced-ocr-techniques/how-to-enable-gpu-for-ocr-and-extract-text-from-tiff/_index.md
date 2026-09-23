---
category: general
date: 2026-02-14
description: Come abilitare la GPU in Aspose OCR Java per estrarre rapidamente il
  testo da un'immagine. Scopri come convertire TIFF in testo, impostare l'ID del dispositivo
  GPU e leggere il testo dai file TIFF.
draft: false
keywords:
- how to enable gpu
- extract text from image
- convert tiff to text
- set gpu device id
- read text from tiff
language: it
og_description: Come abilitare la GPU in Aspose OCR Java per estrarre rapidamente
  il testo da un'immagine. Segui questa guida per convertire TIFF in testo, impostare
  l'ID del dispositivo GPU e leggere il testo dal TIFF.
og_title: Come abilitare la GPU per l'OCR – Estrarre testo da TIFF
tags:
- OCR
- Java
- GPU acceleration
title: Come abilitare la GPU per l'OCR ed estrarre il testo da TIFF
url: /it/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-and-extract-text-from-tiff/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come abilitare la GPU per OCR e estrarre testo da TIFF

Ti sei mai chiesto **come abilitare la GPU** quando esegui OCR su file TIFF di grandi dimensioni? Non sei l'unico: gli sviluppatori cercano costantemente quel boost di velocità extra, soprattutto quando l'immagine di origine è un TIFF multi‑megabyte. La buona notizia? Con Aspose OCR per Java puoi attivare un interruttore, puntare alla GPU corretta e vedere il motore correre attraverso l'immagine.

In questo tutorial percorreremo l'intero flusso di lavoro: caricare un TIFF, attivare l'accelerazione GPU, opzionalmente scegliere un dispositivo GPU specifico, eseguire l'OCR e infine **estrarre il testo dall'immagine**. Alla fine sarai in grado di **convertire TIFF in testo** in poche righe di codice e vedrai anche come **leggere il testo da file TIFF** su qualsiasi piattaforma supportata.

## Cosa ti serve

- Java 17 o superiore (il codice funziona anche con Java 8+)
- Aspose OCR per Java 23.10 (o l'ultima versione al momento della scrittura)
- Una GPU compatibile CUDA con i driver più recenti installati
- Un TIFF multi‑pagina di esempio (lo chiameremo `sample_large.tif`)

Nessun trucco Maven? Nessun problema—basta inserire il JAR nel classpath e sei pronto a partire.

![Come abilitare GPU tutorial](gpu-ocr.png)

*Testo alternativo immagine: Come abilitare la GPU per OCR in Java*

## Passo 1: Caricare un'immagine TIFF per OCR

Prima di tutto: ti serve un'istanza di `OcrEngine` e un'immagine di origine. Aspose OCR può leggere praticamente qualsiasi formato raster, ma il TIFF è comune per i documenti scansionati.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the TIFF file – this is where we "read text from TIFF"
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample_large.tif"));
```

> **Perché è importante:** La chiamata `setImage` avvolge il file in uno `ImageStream`, consentendo al motore di gestire TIFF multi‑pagina senza doverli dividere manualmente. Se il file non viene trovato, otterrai un chiaro `FileNotFoundException`—controlla quindi il percorso.

## Passo 2: Abilitare l'accelerazione GPU

Ora avviene la magia. Attivare la GPU è solo una bandiera booleana, ma può ridurre di secondi—o addirittura minuti—i tempi di elaborazione.

```java
        // Enable GPU acceleration (requires a supported driver)
        ocrEngine.getEngineOptions().setUseGpu(true);
```

> **Consiglio professionale:** Se la tua macchina ha più GPU, di solito la predefinita è la prima (dispositivo 0). Puoi lasciare che Aspose scelga automaticamente il miglior dispositivo, ma specificarlo può evitare sorprese su workstation con più GPU.

## Passo 3: Impostare l'ID del dispositivo GPU (opzionale)

A volte sai esattamente quale GPU vuoi usare—magari la seconda scheda è dedicata ai carichi di lavoro AI. È qui che `setGpuDeviceId` brilla.

```java
        // Optional: select the GPU device (0 = first device, 1 = second, etc.)
        ocrEngine.getEngineOptions().setGpuDeviceId(0);
```

> **Caso limite:** Se passi un ID non valido, il motore lancia `IllegalArgumentException`. Un rapido `System.out.println(ocrEngine.getEngineOptions().getAvailableGpuDevices())` può elencare gli ID disponibili.

## Passo 4: Elaborare l'immagine e **estrarre testo dall'immagine**

Con il motore configurato, è il momento di eseguire l'OCR. L'oggetto risultato ti fornisce la stringa grezza, più i punteggi di confidenza se ti servono.

```java
        // Perform OCR – this is where we "convert TIFF to text"
        OcrResult ocrResult = ocrEngine.process();

        // Output the recognized text
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

### Output previsto

Se il TIFF contiene la frase “Hello, World!” dovresti vedere qualcosa di simile:

```
Recognized text:
Hello, World!
```

Il motore gestisce interruzioni di riga, punteggiatura e persino una rilevazione di layout di base. Per un controllo più granulare (ad esempio, estrarre testo per pagina), esplora `ocrResult.getPages()`.

## Passo 5: Verificare l'output e gestire i problemi comuni

### Perché la GPU potrebbe non essere utilizzata?

- **Incompatibilità driver:** Il driver GPU deve essere almeno la versione consigliata da Aspose (controlla le note di rilascio).
- **Memoria insufficiente:** Immagini molto grandi possono superare la VRAM della GPU. In tal caso, il motore ricade elegantemente sulla CPU—cerca un avviso nella console.
- **Hardware non supportato:** Le schede grafiche integrate spesso non hanno la capacità di calcolo richiesta.

### Come tornare alla CPU programmaticamente

```java
if (!ocrEngine.getEngineOptions().isGpuAvailable()) {
    System.out.println("GPU not available – switching to CPU.");
    ocrEngine.getEngineOptions().setUseGpu(false);
}
```

### Leggere il testo da TIFF in un ciclo

Se hai una cartella piena di TIFF, puoi iterare:

```java
File folder = new File("YOUR_DIRECTORY");
for (File file : folder.listFiles((dir, name) -> name.toLowerCase().endsWith(".tif"))) {
    ocrEngine.setImage(ImageStream.fromFile(file.getAbsolutePath()));
    OcrResult result = ocrEngine.process();
    System.out.println("File: " + file.getName());
    System.out.println(result.getText());
}
```

Questo snippet mostra come **leggere il testo da file TIFF** in blocco, mantenendo comunque i vantaggi dell'accelerazione GPU.

## Domande frequenti (FAQ)

**D: Funziona su Linux?**  
R: Assolutamente—Aspose OCR è cross‑platform. Basta assicurarsi che il toolkit CUDA e i driver siano installati.

**D: E se non ho una GPU?**  
R: Imposta `setUseGpu(false)` o semplicemente ometti la chiamata. Il motore usa la CPU per impostazione predefinita.

**D: Posso estrarre testo da altri formati?**  
R: Sì, lo stesso metodo `setImage` accetta JPEG, PNG, BMP e persino flussi PDF.

**D: Quanto è accurato l'OCR su TIFF a bassa risoluzione?**  
R: L'accuratezza cala sotto i 300 dpi. Considera di pre‑elaborare l'immagine (binarizzazione, deskew) prima di passarla al motore.

## Conclusione

Ora sai **come abilitare la GPU** per Aspose OCR Java, come **impostare l'ID del dispositivo GPU** e—soprattutto—come **estrarre testo dall'immagine**, in particolare **convertire TIFF in testo** e **leggere testo da TIFF** in modo efficiente. Attivando una singola bandiera e, opzionalmente, scegliendo un dispositivo, sblocchi guadagni di prestazioni enormi senza riscrivere alcuna logica OCR.

Pronto per il passo successivo? Prova a sperimentare con:

- **Elaborazione batch** di centinaia di TIFF in thread paralleli.
- **Pacchetti linguistici personalizzati** per migliorare il riconoscimento su documenti specializzati.
- **Post‑processing** della stringa estratta con regex per pulire la formattazione.

Sentiti libero di lasciare un commento se incontri difficoltà, e buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}