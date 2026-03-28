---
category: general
date: 2026-03-28
description: Scopri come riconoscere il testo nelle immagini in Java usando Aspose
  OCR, estrarre file PNG di testo e utilizzare l'accelerazione GPU per una rapida
  OCR di immagini di grandi dimensioni.
draft: false
keywords:
- recognize image text
- extract text png
- use gpu acceleration
- ocr large image
- java ocr example
language: it
og_description: Scopri come riconoscere il testo nelle immagini in Java, estrarre
  il testo da file PNG e utilizzare l'accelerazione GPU per l'OCR di immagini di grandi
  dimensioni.
og_title: Riconosci il testo dell'immagine con Java OCR – Esempio accelerato GPU
tags:
- OCR
- Java
- GPU
title: Riconoscere il testo delle immagini con Java OCR – Esempio accelerato da GPU
url: /it/java/advanced-ocr-techniques/recognize-image-text-with-java-ocr-gpu-accelerated-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# riconoscere il testo delle immagini con Java OCR – Esempio accelerato GPU

Hai mai dovuto **riconoscere il testo di un'immagine** da un enorme PNG ma la versione CPU era troppo lenta? Non sei il solo. In molte pipeline reali—ad esempio la scansione di fatture o l'archiviazione di documenti storici—le dimensioni dell'immagine possono crescere notevolmente, e il motore OCR predefinito semplicemente non riesce a tenere il passo.  

Buone notizie: Aspose OCR per Java ti permette di **usare l'accelerazione GPU** per velocizzare il processo, e il codice è sorprendentemente compatto. In questo tutorial vedrai un esempio completo e funzionante di OCR in Java che **estrae testo da file PNG**, sfrutta una GPU abilitata CUDA e gestisce un **OCR large image** con poche righe di codice. Alla fine saprai esattamente come integrare tutto nel tuo progetto Java e perché ogni impostazione è importante.

## Cosa imparerai

- Come configurare Aspose OCR in un progetto Maven o Gradle.  
- Il processo passo‑per‑passo per **riconoscere il testo delle immagini** sulla GPU.  
- Perché configurare il numero di stream GPU può migliorare il throughput.  
- Come verificare l'output e risolvere i problemi più comuni.  

> **Prerequisiti** – Java 17 (o successiva), una GPU compatibile CUDA con driver aggiornato, e una licenza valida di Aspose OCR per Java (la versione di prova gratuita è sufficiente per la valutazione). Non sono richieste altre librerie esterne.

---

## Step 1: Add Aspose OCR Dependency

First, bring the Aspose OCR library into your build. If you use **Maven**, add the following snippet to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check Maven Central for the latest version -->
</dependency>
```

For **Gradle**, place this in `build.gradle`:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Pro tip:** The latest version (as of March 2026) includes performance improvements for GPU workloads, so always pull the newest release.

---

## Step 2: Initialize the OCR Engine and Enable GPU

Creating an OCR engine is straightforward. The crucial part is turning on the GPU flag—otherwise the engine falls back to CPU mode.

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU acceleration (requires a CUDA‑enabled GPU and driver)
        ocrEngine.getRecognitionSettings().setUseGpu(true);

        // 3️⃣ (Optional) Set the number of GPU streams for parallel processing
        //    More streams can improve throughput on multi‑core GPUs.
        ocrEngine.getRecognitionSettings().setGpuStreams(2);
```

### Why Enable GPU?

When you enable `setUseGpu(true)`, Aspose offloads the heavy convolutional neural network computations to the graphics card. This can shave seconds off the processing time of a **ocr large image**, especially when the image exceeds 4000 × 4000 px. If your environment lacks a compatible GPU, the call simply becomes a no‑op and the engine continues on the CPU—no crash, just slower performance.

---

## Step 3: Recognize a PNG Image and Extract Its Text

Now point the engine at the file you want to process. The example uses `sample-large.png`, but you can replace it with any PNG or JPEG.

```java
        // 4️⃣ Perform OCR on the input image
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/sample-large.png");

        // 5️⃣ Print the recognized text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

When you run the program, you should see something like:

```
=== Recognized Text ===
Invoice #12345
Date: 2026‑03‑27
Total: $1,234.56
...
```

That output confirms the **recognize image text** operation succeeded and that you successfully **extract text png** content.

---

## Step 4: Verify GPU Utilization (Optional but Helpful)

If you’re curious whether the GPU is really being used, open your system’s GPU monitoring tool (e.g., `nvidia-smi` on Linux). While the Java process runs, you should see a modest spike in memory usage and compute utilization.

```bash
$ nvidia-smi
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   PID   Type   Process name                  GPU Memory               |
|  0    12345 C++    java                           1024MiB                  |
+-----------------------------------------------------------------------------+
```

If you don’t see any activity, double‑check that:

1. The CUDA driver matches the GPU model.  
2. The `setUseGpu(true)` call isn’t being overridden later in the code.  
3. Your license file (if you have one) isn’t restricting GPU usage.

---

## Step 5: Handling Common Edge Cases

### Large Images Exceeding GPU Memory

When an image is massive (e.g., 8000 × 8000 px), the GPU may run out of memory. A quick workaround is to downscale the image before feeding it to Aspose:

```java
import java.awt.image.BufferedImage;
import javax.imageio.ImageIO;
import java.io.File;

BufferedImage original = ImageIO.read(new File("sample-large.png"));
int maxDim = 4000; // target max dimension
int width = original.getWidth();
int height = original.getHeight();

float scale = Math.min((float)maxDim / width, (float)maxDim / height);
int newWidth = Math.round(width * scale);
int newHeight = Math.round(height * scale);

BufferedImage resized = new BufferedImage(newWidth, newHeight, original.getType());
// Simple scaling (for demo purposes)
resized.getGraphics().drawImage(original, 0, 0, newWidth, newHeight, null);
ImageIO.write(resized, "png", new File("sample-resized.png"));
```

Then pass `"sample-resized.png"` to `recognizeImage`. This keeps the OCR accurate while staying within GPU limits.

### Multi‑Page PDFs

Aspose OCR can also handle PDFs page‑by‑page. Loop over each page, convert it to an image, and feed it to the engine. The same **use gpu acceleration** flag applies, giving you a fast PDF‑to‑text pipeline.

---

## Full Working Example (Copy‑Paste Ready)

Below is the complete Java class, ready to compile and run. Replace `YOUR_DIRECTORY` with the path to your PNG file.

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable GPU acceleration (requires a CUDA‑enabled GPU and driver)
        ocrEngine.getRecognitionSettings().setUseGpu(true);

        // Step 3: (Optional) Set the number of GPU streams for parallel processing
        // Using 2 streams works well on most modern GPUs.
        ocrEngine.getRecognitionSettings().setGpuStreams(2);

        // Step 4: Perform OCR on the input image
        // This will **recognize image text** from a PNG file.
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/sample-large.png");

        // Step 5: Print the recognized text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**Expected output** – a plain‑text representation of everything the engine could read from the image. If the image contains a table, you’ll get the cell contents concatenated with line breaks; Aspose does not preserve layout, but you can post‑process the string if needed.

---

## Frequently Asked Questions

| Question | Answer |
|----------|--------|
| **Do I need a paid license?** | The trial works for up to 200 pages and disables watermark for OCR. For production, a license removes limits and unlocks the full GPU stack. |
| **What if my GPU is older (e.g., GTX 750)?** | Older GPUs may still work but with reduced speed; ensure you have at least Compute Capability 3.0. |
| **Can I process JPG or BMP files?** | Absolutely—`recognizeImage` accepts any format supported by Java ImageIO. |
| **Is there a way to batch‑process many images?** | Wrap the OCR call in a loop, and consider increasing `setGpuStreams` to match the number of concurrent streams you want. |
| **What if I need to preserve layout?** | Use Aspose OCR’s `LayoutOptions` to get bounding boxes; this is beyond the scope of this quick guide but documented in the API. |

---

## Conclusion

You now have a concise, end‑to‑end **java ocr example** that **recognize image text**, **extract text png**, and **use GPU acceleration** to speed up processing of an **ocr large image**. By tweaking the GPU stream count and, if necessary, downscaling oversized images, you can tailor the solution to virtually any hardware configuration.

Ready for the next step? Try feeding a folder of scanned receipts into the same pipeline, or experiment with Aspose’s `TextRegion` API to keep the original layout intact. And if you hit any snags, the Aspose forums and Javadoc are excellent resources—just remember the basics we covered here.

Happy coding, and may your OCR be lightning‑fast!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}