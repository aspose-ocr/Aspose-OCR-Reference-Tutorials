---
category: general
date: 2026-02-17
description: Aspose OCR GPU desteğiyle Java’da metin görüntüsünü hızlıca tanıyın.
  Görüntüden metin çıkarmayı öğrenin ve optimal performans için GPU cihaz kimliğini
  ayarlayın.
draft: false
keywords:
- recognize text image
- extract text from image
- set gpu device id
- Aspose OCR Java
- GPU acceleration OCR
language: tr
og_description: Aspose OCR GPU desteğiyle Java’da metin görüntüsünü hızlıca tanıyın.
  Bu kılavuz, görüntüden metin çıkarmayı ve GPU cihaz kimliğini ayarlamayı gösterir.
og_title: Aspose OCR GPU – Java ile metin görüntüsünü tanıma
tags:
- Java
- OCR
- Aspose
- GPU
title: Aspose OCR GPU – Java ile metin görüntüsünü tanıma
url: /tr/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR GPU – Java kullanarak metin görüntüsü tanıma

Ever needed to **recognize text image** in a Java application but the CPU was choking on large files? You're not the only one—many developers hit that wall when processing high‑resolution scans. The good news? Aspose OCR lets you **extract text from image** on the GPU, slashing processing time dramatically.  

In this tutorial we’ll walk through a complete, ready‑to‑run example that shows exactly how to set up the license, enable GPU acceleration, and **set gpu device id** when you have multiple graphics cards. By the end you’ll have a self‑contained program that prints the recognized text to the console—no extra steps required.

## Gereksinimler

- **Java 17** veya daha yeni (API, Java 8+ ile uyumludur, ancak en yeni LTS daha iyi performans sağlar).  
- **Aspose OCR for Java** kütüphanesi (JAR dosyasını Aspose web sitesinden indirin).  
- Geçerli bir **Aspose OCR lisans dosyası** (`Aspose.OCR.lic`). Ücretsiz deneme çalışır, ancak GPU özellikleri lisanslı bir sürümle açılır.  
- Açık, makine tarafından okunabilir metin içeren bir görüntü dosyası (`sample-image.png`).  
- GPU‑destekli bir ortam (NVIDIA CUDA‑uyumlu kart en iyisidir).  

If any of those sound unfamiliar, don’t worry—each bullet point will be explained as we go.

## Adım 1: Aspose OCR'ı Projenize Ekleyin

First, include the Aspose OCR JAR on your classpath. If you’re using Maven, add the following dependency to `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

For Gradle, it’s:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

If you prefer the manual route, drop the JAR into your `libs/` folder and add it to the IDE’s module path.

> **Pro tip:** Sürüm numarasını kütüphanenin sürüm notlarıyla senkronize tutun; daha yeni sürümler genellikle GPU işleme için performans iyileştirmeleri getirir.

## Adım 2: Aspose OCR Lisansını Yükleyin (GPU kullanımı için gerekli)

Without a license the `setEnableGpu(true)` call will silently fall back to CPU mode. Load the license right at the start of `main`:

```java
import com.aspose.ocr.License;

// ...

License ocrLicense = new License();
ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

Replace `YOUR_DIRECTORY` with the absolute or relative path where you stored the `.lic` file. If the path is wrong, Aspose will throw a `FileNotFoundException`, so double‑check the spelling.

## Adım 3: OCR motorunu oluşturun ve GPU hızlandırmayı etkinleştirin

Now we instantiate `OcrEngine` and tell it to use the GPU. The `setGpuDeviceId` method lets you pick a specific card when more than one is present.

```java
import com.aspose.ocr.OcrEngine;

// ...

OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getDevice().setEnableGpu(true);       // activate GPU support
ocrEngine.getDevice().setGpuDeviceId(0);        // optional: choose GPU index (0 = first card)
```

Why bother with the device ID? In a multi‑GPU server you might reserve one card for image preprocessing and another for OCR. Setting the ID ensures the right hardware does the heavy lifting.

## Adım 4: Giriş görüntüsünü hazırlayın

Aspose OCR works with a variety of formats (PNG, JPG, BMP, TIFF). Wrap your file in an `OcrInput` object:

```java
import com.aspose.ocr.OcrInput;

// ...

OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/sample-image.png"); // path to the image you want to process
```

If you need to process a stream (e.g., an uploaded file), use `ocrInput.add(InputStream)` instead.

## Adım 5: Tanıma sürecini çalıştırın ve sonucu alın

The `recognize` method returns an `OcrResult` which contains the plain text, confidence scores, and even layout information if you need it.

```java
import com.aspose.ocr.OcrResult;

// ...

OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("Recognized text:\n" + ocrResult.getText());
```

The console will display something like:

```
Recognized text:
Hello, world!
This is a sample image.
```

If the image is blurry or the language isn’t supported, the result may be empty. In that case, check the `ocrResult.getConfidence()` value (0‑100) to decide whether to retry with preprocessing.

## Tam, Çalıştırılabilir Örnek

Putting all the pieces together gives you a single Java class you can copy‑paste into your IDE:

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license – required for GPU usage
        License ocrLicense = new License();
        ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");

        // 2️⃣ Create OCR engine and turn on GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getDevice().setEnableGpu(true);      // enable GPU acceleration
        ocrEngine.getDevice().setGpuDeviceId(0);       // optional: select GPU index

        // 3️⃣ Load the image you want to process
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/sample-image.png");

        // 4️⃣ Perform recognition
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // 5️⃣ Output the recognized text
        System.out.println("Recognized text:\n" + ocrResult.getText());
    }
}
```

> **Expected output:** Konsol, `sample-image.png` içinde görülen tam metni yazdırır. GPU aktifse, tipik 300 dpi taramalar için işleme süresinin birkaç saniyeden (CPU) bir saniyenin altına düştüğünü fark edeceksiniz.

## Yaygın Sorular & Özel Durumlar

### Bu, ekransız (headless) bir sunucuda çalışır mı?

Yes. The GPU driver must be installed, but no display is required. Just ensure the `CUDA` toolkit (or equivalent for your GPU) is in the system `PATH`.

### Birden fazla GPU'm var ve GPU 1'i kullanmak istiyorum, ne yapmalıyım?

Change the device ID:

```java
ocrEngine.getDevice().setGpuDeviceId(1); // selects the second GPU (zero‑based index)
```

### Farklı bir dilde görüntüden metin nasıl çıkarılır?

Set the language before calling `recognize`:

```java
ocrEngine.setLanguage(OcrLanguage.FRENCH);
```

Aspose 30'dan fazla dili destekler; tam liste için API belgelerine bakın.

### Görüntü birden fazla sayfa içeriyorsa (ör. PDF görüntülere dönüştürülmüşse) ne olur?

Create a separate `OcrInput` entry for each page, or loop over the files:

```java
for (String path : imagePaths) {
    ocrInput.add(path);
}
```

The engine will concatenate the results in order.

### Düşük güvenilirlik sonuçları nasıl ele alınır?

Check the confidence score:

```java
if (ocrResult.getConfidence() < 70) {
    System.out.println("Low confidence – consider preprocessing the image.");
}
```

Typical preprocessing steps include binarization, noise reduction, or resizing to 300 dpi.

## Performans İpuçları

- **Batch processing:** Birçok görüntüyü tek bir `OcrInput` içine eklemek, GPU bağlamının tekrar tekrar başlatılmasından kaynaklanan ek yükü azaltır.  
- **Warm‑up:** JVM başlatıldıktan sonra bir deneme tanıması çalıştırın; ilk çağrı sürücü başlatma gecikmesi getirir.  
- **Memory management:** İşiniz bittiğinde büyük `OcrInput` nesnelerini (`ocrInput.clear()`) temizleyerek GPU belleğini serbest bırakın.  

## Sonuç

You now know how to **recognize text image** efficiently with Aspose OCR’s GPU engine in Java, how to **extract text from image** in any supported language, and how to **set gpu device id** when working with multiple graphics cards. The complete, runnable code above should work out‑of‑the‑box—just swap in your license and image paths.

Ready for the next step? Try processing a folder of scanned PDFs, experiment with different `setLanguage` options, or combine OCR with a machine‑learning model for post‑processing. The possibilities are endless, and the performance gains from GPU acceleration make even large‑scale projects feasible.

Happy coding, and feel free to drop a comment if you hit any snags!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}