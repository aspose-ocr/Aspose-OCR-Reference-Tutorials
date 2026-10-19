---
category: general
date: 2026-03-07
description: Esegui OCR su un'immagine usando Java. Scopri come riconoscere il testo
  da PNG, estrarre il testo da una ricevuta e caricare l'immagine per l'OCR con un
  esempio completo di OCR in Java.
draft: false
keywords:
- run OCR on image
- recognize text from png
- extract text from receipt
- java OCR example
- load image for OCR
language: it
og_description: Esegui OCR su un'immagine con Java. Questa guida mostra come riconoscere
  il testo da un PNG, estrarre il testo da una ricevuta e caricare l'immagine per
  l'OCR usando un esempio completo di OCR in Java.
og_title: Esegui OCR su immagine con Java – Estrazione del testo con GPU
tags:
- OCR
- Java
- GPU
- Image Processing
title: Esegui OCR su immagine con Java – Estrazione del testo accelerata da GPU
url: /it/java/advanced-ocr-techniques/run-ocr-on-image-with-java-gpu-powered-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esegui OCR su Immagine con Java – Estrazione di Testo Accelerata da GPU

Ti è mai capitato di dover **eseguire OCR su immagine** ma di non sapere da dove partire in Java? Non sei solo: molti sviluppatori incontrano lo stesso ostacolo quando provano per la prima volta a estrarre testo da una ricevuta scansionata o da uno screenshot PNG.  

In questo tutorial ti guideremo attraverso un **esempio completo di OCR in Java** che non solo **riconosce testo da file PNG**, ma mostra anche come **estrarre testo da immagini di ricevute**, sfruttando l’accelerazione GPU per la velocità. Alla fine avrai un programma pronto all’uso che carica un’immagine per l’OCR, la elabora e stampa il risultato in testo semplice.

## Cosa Imparerai

- Come **caricare immagine per OCR** usando un semplice `ImageInputStream`.
- Abilitare il supporto GPU affinché il motore funzioni più velocemente sull’hardware moderno.
- I passaggi esatti per **riconoscere testo da PNG** e estrarre stringhe utili da una ricevuta.
- Insidie comuni (ad es. ID dispositivo GPU errato) e consigli di best‑practice.
- Uno snippet di codice completo e eseguibile che puoi copiare‑incollare nel tuo IDE.

**Prerequisiti**

- Java 17 o superiore (il codice usa la parola chiave `var` per brevità, ma puoi sostituirla con tipi espliciti se sei su Java 8).
- Una libreria OCR che fornisce le classi `OcrEngine`, `ImageInputStream` e `OcrResult` (ad esempio il fittizio *FastOCR* SDK; sostituiscila con quella reale che stai usando).
- Una macchina con GPU abilitata se desideri il boost di prestazioni (opzionale ma consigliato).

---

## Step 1: Run OCR on Image – Enable GPU Acceleration

The first thing to do is create the OCR engine and tell it to use the GPU. This step is crucial because without GPU support the engine falls back to the CPU, which can be noticeably slower for high‑resolution receipts.

```java
// Step 1: Create the OCR engine and enable GPU acceleration
OcrEngine ocrEngine = new OcrEngine();

// Turn on GPU usage – this makes the recognition much faster
ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage

// Optional: select which GPU device to use (0 = first GPU)
ocrEngine.getConfig().setGpuDeviceId(0);
```

**Why this matters:**  
GPU acceleration offloads the heavy matrix calculations that OCR engines perform. If you have multiple GPUs, you can pick the one with the most memory by changing the `setGpuDeviceId` value. Forgetting to enable the GPU is a common source of “why is my OCR so slow?” complaints.

> **Pro tip:** If your machine doesn’t have a compatible GPU, the `setUseGpu(true)` call will simply be ignored—no crash, just slower processing.

---

## Step 2: Load Image for OCR

Now that the engine is ready, we need to feed it an image. The example below shows how to load a PNG receipt stored on disk. You can replace the path with any image format supported by your OCR library.

```java
// Step 2: Load the image you want to recognize
ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
```

**Edge case:**  
If the file doesn’t exist or the path is wrong, `ImageInputStream` will throw an `IOException`. Wrap the call in a try‑catch block and log a helpful message:

```java
try {
    ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
} catch (IOException e) {
    System.err.println("Failed to load image: " + e.getMessage());
    return;
}
```

---

## Step 3: Recognize Text from PNG

With the image loaded, the OCR engine can now do its magic. This step actually **recognizes text from PNG** (or any other supported format) and returns an `OcrResult` object.

```java
// Step 3: Run the OCR process on the image
OcrResult ocrResult = ocrEngine.recognize(imageStream);
```

**What’s happening under the hood?**  
The engine performs preprocessing (deskew, binarization), runs a neural network to detect characters, and then assembles them into lines of text. Because we enabled the GPU earlier, those neural‑network calculations happen on the graphics card, shaving seconds off the total runtime.

---

## Step 4: Extract Text from Receipt

After recognition, you’ll typically want just the raw text. The `OcrResult` class usually provides a `getText()` method that returns a single `String`. You can then post‑process it (e.g., regex to pull out totals, dates, etc.).

```java
// Step 4: Print the recognized plain‑text result
System.out.println("Recognized text:");
System.out.println(ocrResult.getText());
```

**Typical receipt output:**  

```
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

You can now feed this string into your own parser to pull out the total amount, line items, or tax information.

---

## Step 5: Full Java OCR Example – Ready to Run

Putting everything together, here’s the **complete Java OCR example** that you can drop into a `Main.java` file. Make sure you have the OCR library on your classpath.

```java
import com.fastocr.OcrEngine;
import com.fastocr.ImageInputStream;
import com.fastocr.OcrResult;

public class Main {
    public static void main(String[] args) {
        // 1️⃣ Create OCR engine and enable GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage
        ocrEngine.getConfig().setGpuDeviceId(0);        // optional: select GPU #0

        // 2️⃣ Load the image you want to recognize
        ImageInputStream imageStream;
        try {
            imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
        } catch (Exception e) {
            System.err.println("Error loading image: " + e.getMessage());
            return;
        }

        // 3️⃣ Run OCR on the image
        OcrResult ocrResult = ocrEngine.recognize(imageStream);

        // 4️⃣ Output the plain‑text result
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

**Expected console output** (assuming the sample receipt above):

```
Recognized text:
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

If the output looks garbled, double‑check that the image is clear (high DPI) and that the OCR language pack matches your receipt’s language.

---

## Common Questions & Gotchas

| Question | Answer |
|----------|--------|
| *What if my GPU isn’t detected?* | The engine will fall back to CPU automatically. Verify drivers and that the `setGpuDeviceId` matches an existing device (`nvidia-smi` on Linux can help). |
| *Can I process JPEG or TIFF files?* | Yes—just change the file extension in `ImageInputStream`. The OCR library usually auto‑detects the format. |
| *Is there a way to batch‑process many receipts?* | Wrap the recognition code in a loop and reuse the same `OcrEngine` instance; re‑initializing per image wastes GPU memory. |
| *How do I improve accuracy on low‑contrast receipts?* | Pre‑process the image (increase contrast, convert to grayscale) before feeding it to the OCR engine. Some libraries expose a `preprocess` API. |

---

## Conclusion

You now know **how to run OCR on image** files in Java, from loading the picture to extracting clean text from a receipt. The walkthrough covered **recognize text from PNG**, **extract text from receipt**, and showed a **java OCR example** that you can adapt to any project.  

Next steps? Try swapping the GPU flag off to see the performance difference, experiment with different image resolutions, or integrate a regex‑based parser to pull totals automatically. If you’re curious about more advanced topics, look into **OCR post‑processing**, **language model correction**, or **batch processing pipelines**.

Happy coding, and may your receipts always be readable!  

![esempio di esecuzione OCR su immagine](/images/run-ocr-on-image.png "run OCR on image – Java example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}