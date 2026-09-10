---
date: 2026-02-12
description: Aspose.OCR for Java kullanarak dil seçimiyle görüntü metnini OCR nasıl
  yapılır öğrenin. Bu adım adım rehber, Java’da metin çıkarma, OCR eğim düzeltmesi
  ve daha fazlasını kapsar.
linktitle: How to OCR Image Text with Language Using Aspose.OCR
second_title: Aspose.OCR Java API
title: Aspose.OCR Kullanarak Dil ile Görüntü Metnini OCR'lamak
url: /tr/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

/products-backtop-button >}}

Now produce final content with translations.

Be careful with preserving markdown formatting.

Let's craft translation.

Title: "# Aspose.OCR Kullanarak Dil Seçimiyle Görüntü Metnini OCR Yapma"

Introduction: translate.

I'll write.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.OCR Kullanarak Dil Seçimiyle Görüntü Metnini OCR Yapma

## Introduction

Görüntü dosyalarından metin çıkarmak, taranmış belgeleri dijitalleştiriyor, fişleri işliyor veya aranabilir arşivler oluşturuyorsanız yaygın bir gereksinimdir. Bu öğreticide, **görüntü metnini OCR yapmanın** belirli bir dil ayarıyla nasıl yapılacağını gösteren eksiksiz, uygulamalı bir örnek üzerinden ilerleyeceğiz; böylece güvenilir OCR’ı Java uygulamalarınıza bugün entegre edebilirsiniz. Ayrıca OCR eğikliği düzeltme ve bölge‑bazlı tanıma ile en iyi doğruluğu nasıl elde edeceğinizi de göreceksiniz.

## Quick Answers
- **What library handles OCR in Java?** Aspose.OCR for Java  
- **Which setting selects the language?** `settings.setLanguage(Language.Eng)` (or any supported language)  
- **Do I need a license for development?** A free evaluation license works for testing; a commercial license is required for production.  
- **Can I limit OCR to a region of the image?** Yes, use `RecognitionSettings.setRecognitionAreas()` with rectangles.  
- **What is the typical runtime?** A few seconds per page on a standard laptop, depending on image size and language complexity.

## How to OCR Image Text with Language Selection
Bu bölümde, metnin dilini bildiğiniz bir görüntüyü **nasıl OCR yapacağınızı** temel soruya yanıt veriyoruz. Doğru dili seçmek, OCR motorunun dil‑özel sözlükler ve karakter modelleri uygulayabilmesi sayesinde tanıma doğruluğunu büyük ölçüde artırır.

### Why this matters
- **Higher accuracy** – language‑specific models reduce mis‑recognitions.  
- **Performance boost** – the engine skips unnecessary language checks.  
- **Better handling of diacritics** – French, Spanish, German, etc., are recognized correctly when the matching `Language` enum is used.

## What is “extract text from image”?
Extracting text from image (OCR) converts the visual representation of characters into machine‑readable strings. This enables search, analytics, and data extraction workflows that would otherwise require manual transcription.

## Why use Aspose.OCR with language selection?
- **Multilingual support** – Choose the exact language(s) present in your image to boost accuracy.  
- **Fine‑tuned control** – Adjust skew, define recognition areas, and set auto‑skew behavior.  
- **Pure Java API** – No native dependencies, easy to integrate into any Java project.  
- **Rich result data** – Get plain text, JSON, bounding rectangles, and warnings in one call.

## Prerequisites

Before you start, make sure you have:

- **Java Development Kit (JDK)** installed (JDK 8 or later).  
- **Aspose.OCR for Java** library – download it from the official site [here](https://reference.aspose.com/ocr/java/).  
- An image file that contains the text you want to extract, e.g., `p3.png`.

## Import Packages

Java kaynak dosyanızda, gerekli Aspose.OCR sınıflarını ve standart Java yardımcı sınıflarını ekleyin:

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

## Step‑by‑Step Guide

### Step 1: Set up Your Document Directory

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

### Step 2: Define the Image Path

```java
// The image path
String file = dataDir + "p3.png";
```

### Step 3: Create Aspose.OCR API Instance

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

### Step 4: Set Recognition Options (Language Selection)

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

Burada:

1. Manuel bir eğiklik değeri sağladığımız için otomatik‑eğikliği devre dışı bırakıyoruz.  
2. OCR’ı yalnızca metin içeren kısmıyla sınırlamak için dikdörtgen bir bölge (`RecognitionAreas`) tanımlıyoruz.  
3. **Dili** İngilizce olarak ayarlıyoruz (`Language.Eng`). Kaynak görüntünüze göre bunu `Language.Fra`, `Language.Spa` vb. olarak değiştirin.

### Step 5: Perform OCR and Retrieve Results

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

`RecognizePage` çağrısı, görüntüyü ve tanımladığınız ayarları kullanarak OCR motorunu çalıştırır. Sonuç bir `RecognitionResult` nesnesinde saklanır.

### Step 6: Print and Utilize Results

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

Konsol çıktısı şunları gösterir:

- Tam çıkarılan metin (`recognitionText`).  
- Her tanımlı dikdörtgen için metin (`recognitionAreasText`).  
- Sınırlayıcı dikdörtgen koordinatları.  
- Kolay downstream işleme için JSON temsili.  
- Algılanan eğiklik açısı ve olası uyarılar.

Artık `result.recognitionText` değerini iş mantığınıza besleyebilirsiniz—saklayın, indeksleyin veya başka bir servise gönderin.

## Common Issues and Solutions

| Issue | Cause | Fix |
|-------|-------|-----|
| **Garbage characters** | Wrong language selected | Set the correct `Language` enum (e.g., `Language.Fra` for French). |
| **No text returned** | Recognition area does not cover the text | Adjust the `Rectangle` coordinates or remove `RecognitionAreas` to process the whole image. |
| **Slow performance** | Very large image or high resolution | Downscale the image before OCR or increase memory allocation for the JVM. |
| **Warnings about unsupported format** | Image format not recognized | Convert the image to PNG, JPEG, or TIFF before processing. |

## FAQ

**Q: Can I recognize multiple languages in a single OCR call?**  
A: Yes. Use `settings.setLanguage(Language.Eng | Language.Fra)` to enable multilingual recognition.

**Q: Which image formats does Aspose.OCR support?**  
A: PNG, JPEG, BMP, TIFF, GIF, and several others. Just provide the correct file path.

**Q: Is there a size limit for the image?**  
A: There’s no hard limit, but very large images increase memory usage and processing time. Consider resizing large files.

**Q: How do I obtain a production license?**  
A: Purchase a license from the Aspose website and apply it via the `License` class as shown in the Aspose documentation.

**Q: Can I extract text from a PDF page directly?**  
A: Not directly with Aspose.OCR. Convert the PDF page to an image first (e.g., using Aspose.PDF) and then run OCR.

## Conclusion

Aspose.OCR for Java kullanarak **görüntüden metin çıkarma** işlemini, uygun dili seçerek ve tanıma bölgesini sınırlayarak nasıl gerçekleştireceğinizi gördünüz. Bu yaklaşım, belge yönetim sistemlerinden veri yakalama boru hatlarına kadar herhangi bir Java‑tabanlı iş akışına gömülebilen doğru, yüksek‑performanslı bir OCR sunar. İleriye doğru adım atmaya hazır mısınız? Dil enumunu değiştirin, farklı tanıma bölgeleriyle deney yapın ve sonuçları kendi uygulama mantığınıza entegre edin.

---

**Last Updated:** 2026-02-12  
**Tested With:** Aspose.OCR 24.11 for Java  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}