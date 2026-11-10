---
category: general
date: 2026-06-22
description: 'OCR için görüntüyü eğriltmeyi düzeltme: Görüntü ön işleme OCR adımlarını
  öğrenin, tuz ve biber gürültüsünü kaldırın ve doğruluğu artırın.'
draft: false
keywords:
- how to deskew image
- image preprocessing ocr
- remove salt pepper
- preprocess images OCR
language: tr
og_description: OCR için görüntüyü eğriltmeyi düzeltme, tuz ve karabiber gürültüsünü
  kaldırma ve görüntü ön işleme OCR tekniklerini tam bir Java örneğinde uygulama.
og_title: Görüntüyü Nasıl Düzeltiriz – Görüntü Ön İşleme OCR Kılavuzu
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: 'How to deskew image for OCR: learn image preprocessing OCR steps,
    remove salt pepper noise, and boost accuracy.'
  headline: How to Deskew Image – Image Preprocessing OCR Guide
  type: TechArticle
tags:
- OCR
- image-processing
- Java
title: Görüntüyü Nasıl Düzeltiriz – Görüntü Ön İşleme OCR Kılavuzu
url: /tr/java/ocr-operations/how-to-deskew-image-image-preprocessing-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Deskew Image – Image Preprocessing OCR Guide

Hiç **görüntüyü eğik düzeltme (deskew)** nasıl yapılır diye merak ettiniz mi, böylece OCR motorunuz metni gerçekten okuyabilir? Tek başınıza değilsiniz. Eğik bir tarama, kusursuz bir belgeyi karışık bir karmaşaya dönüştürebilir ve çoğu geliştirici bu sorunu en az bir kez yaşamıştır.

Bu öğreticide, sadece dönüşümü düzeltmekle kalmayıp **salt pepper** bozulmalarını da **kaldıran** ve kontrastı artıran tam bir **image preprocessing OCR** hattını adım adım inceleyeceğiz—temelde OCR‑stilinde **preprocess images OCR** yapmanız için ihtiyacınız olan her şey. Sonunda çalıştırmaya hazır bir Java kod parçacığı ve her adımın neden önemli olduğuna dair net bir zihinsel model elde edeceksiniz.

## How to Deskew Image – Building the Preprocessing Pipeline

Her OCR‑dostu iş akışının kalbi, bir dizi filtreyi bir araya getiren bir **preprocess options** nesnesidir. Bunu bir taşıma bandı gibi düşünün: her filtre bir işi yapar, ardından görüntüyü bir sonraki filtreye aktarır. Aşağıda, `DeskewFilter`, `DenoiseFilter` ve `ContrastBoostFilter` içeren varsayımsal bir OCR kütüphanesini kullanan minimal ama eksiksiz bir örnek yer alıyor.

```java
import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.DeskewFilter;
import com.example.ocr.filters.DenoiseFilter;
import com.example.ocr.filters.ContrastBoostFilter;

/**
 * Demonstrates how to deskew image and apply common OCR preprocessing steps.
 */
public class OcrPreprocessDemo {

    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine (replace with your actual implementation)
        Engine engine = new Engine();

        // 2️⃣ Build the preprocessing pipeline
        ImagePreprocessOptions preprocessOptions = new ImagePreprocessOptions();

        // 2a️⃣ Deskew – correct rotation up to ±15°
        preprocessOptions.addFilter(new DeskewFilter(15));

        // 2b️⃣ Denoise – remove salt‑and‑pepper noise
        preprocessOptions.addFilter(new DenoiseFilter());

        // 2c️⃣ Contrast boost – make low‑contrast scans more readable
        preprocessOptions.addFilter(new ContrastBoostFilter(1.5f));

        // 3️⃣ Attach the pipeline to the engine
        engine.setPreprocessOptions(preprocessOptions);

        // 4️⃣ Run OCR on a sample image
        String result = engine.recognizeText("sample-scanned-page.png");

        // 5️⃣ Output the recognized text
        System.out.println("=== OCR RESULT ===");
        System.out.println(result);
    }
}
```

### Why this works

* **DeskewFilter** görüntünün baskın metin satırlarını analiz eder, açıyı tahmin eder ve bitmap’i yatay konuma geri döndürür. Çoğu kütüphane düzeltmeyi ±15° ile sınırlar; çünkü daha büyük açılar genellikle manuel müdahale gerektiren kötü taranmış bir sayfayı gösterir.
* **DenoiseFilter** klasik *salt‑and‑pepper* desenine hedef alır—TV’deki statik gibi görünen izole siyah veya beyaz pikseller. Bunları kaldırmak, OCR motorunun gürültüyü karakterle karıştırmasını önler.
* **ContrastBoostFilter** histogramı genişleterek soluk çizgileri öne çıkarır. `1.5f` çarpanı güvenli bir varsayılandır; taramalarınız özellikle soluk ise bunu artırabilirsiniz.

> **Pro tip:** Belgelerinizin eğiminin 10°’yi geçmediğini biliyorsanız, `DeskewFilter`’a bu daha küçük sınırı verin—algoritma daha hızlı çalışır ve aşırı düzeltme olasılığı azalır.

## Image Preprocessing OCR: Adding Filters in the Right Order

Sıra önemlidir. **Deskew** işleminden önce **denoise** yaparsanız, gürültü açı tespitini bozabilir ve hatalı bir sonuç elde edebilirsiniz. Öte yandan, kontrast artırmayı **deskew** işleminden sonra uygulamak, dönüşümün yeni bozulmalara yol açmasını engeller.

Aşağıdaki kontrol listesi, herhangi bir projeye kopyalayıp yapıştırabileceğiniz bir özet sunar:

| Step | Filter | Reason |
|------|--------|--------|
| 1 | `DeskewFilter` | Metin taban çizgisini hizalar |
| 2 | `DenoiseFilter` | İzole piksel gürültüsünü kaldırır |
| 3 | `ContrastBoostFilter` | OCR için okunabilirliği artırır |

Ek adımlar eklemeniz gerekirse—örneğin **binarizasyon** filtresi binary OCR için—bu filtreyi **kontrast artırmadan sonra** yerleştirin; çünkü temiz, yüksek kontrastlı bir görüntü daha doğru bir şekilde ikiliye dönüştürülür.

## Remove Salt Pepper Noise with DenoiseFilter

Salt‑and‑pepper gürültüsü, özellikle ucuz telefon kameralarından gelen düşük kaliteli taramalarda yaygındır. Kütüphanemizdeki `DenoiseFilter`, bir medyan‑filtre çekirdeği uygular; her pikseli çevresindeki komşularının medyanı ile değiştirir. Sonuç? Bu lekeler karakterleri bulanıklaştırmadan kaybolur.

```java
// Example: customizing the median kernel size (default is 3x3)
preprocessOptions.addFilter(new DenoiseFilter(5)); // 5x5 kernel for heavy noise
```

*Kernel boyutunu ne zaman artırmalı?* Kaynak görüntüleriniz büyük lekelerle doluysa, daha büyük bir çekirdek bu lekeleri temizler; fakat çok büyük bir çekirdek, ince fontlardaki ince çizgileri silmeye başlayabilir.

## Preprocess Images OCR – Applying the Pipeline

Filtre zincirini oluşturduktan sonra, motorunuza eklemek tek satır kod (`engine.setPreprocessOptions`) ile yapılır. Bundan sonra, `recognizeText` çağrısı otomatik olarak bu hattı izler. Her bir filtreyi manuel olarak çağırmanıza gerek kalmaz—kodunuz düzenli kalır ve gelecekteki değişiklikler (yeni bir filtre ekleme, parametre ayarlama) merkezi bir noktada yapılır.

Aşağıda, başlangıçta 12° eğik ve belirgin pepper gürültüsü olan bir örnek tarama ile başarılı bir çalışmanın çıktısı gösterilmiştir:

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

Metnin temiz, doğru yönlendirilmiş ve “I n v o i c e” ya da “$‑‑‑” gibi hatalı karakterlerden arındırılmış olduğunu fark edeceksiniz.

## Edge Cases & Common Pitfalls

| Situation | What to watch for | Suggested fix |
|-----------|-------------------|---------------|
| Rotation > 15° | DeskewFilter may give up | Pre‑rotate manually or use a higher‑range filter |
| Extremely low resolution ( < 100 dpi ) | Contrast boost can’t recover details | Resample the image first (e.g., `ResampleFilter`) |
| Mixed noise (Gaussian + salt‑pepper) | DenoiseFilter alone isn’t enough | Chain a `GaussianBlurFilter` before `DenoiseFilter` |
| Color scans with colored text | Grayscale conversion needed | Insert `GrayscaleFilter` before contrast boost |

Bu senaryoları önceden tahmin ederek ileride saatler süren hata ayıklamaktan kurtulursunuz.

## Full Working Example (All‑in‑One)

Aşağıda, `com.example.ocr` bağımlılığını içeren herhangi bir Maven ya da Gradle projesine ekleyebileceğiniz, **görüntüyü eğik düzeltme (deskew)**, **salt pepper** gürültüsünü kaldırma ve **preprocess images OCR**‑stilinde ön işleme yapmayı gösteren bütünleşik bir Java sınıfı yer alıyor.

```java
package com.myapp.demo;

import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.*;

public class CompleteOcrPipeline {

    public static void main(String[] args) {
        // -------------------------------------------------
        // 1️⃣ Initialise OCR engine (replace with your own)
        // -------------------------------------------------
        Engine engine = new Engine();

        // -------------------------------------------------
        // 2️⃣ Configure preprocessing pipeline
        // -------------------------------------------------
        ImagePreprocessOptions options = new ImagePreprocessOptions();

        // Deskew up to ±15° – the core of "how to deskew image"
        options.addFilter(new DeskewFilter(15));

        // Remove salt‑and‑pepper artifacts
        options.addFilter(new DenoiseFilter());

        // Boost contrast by 1.5× to aid OCR recognition
        options.addFilter(new ContrastBoostFilter(1.5f));

        // (Optional) Convert to grayscale – often improves OCR accuracy
        options.addFilter(new GrayscaleFilter());

        // Attach the pipeline
        engine.setPreprocessOptions(options);

        // -------------------------------------------------
        // 3️⃣ Perform OCR on a test file
        // -------------------------------------------------
        String imagePath = "src/main/resources/scanned-document.png";
        String text = engine.recognizeText(imagePath);

        // -------------------------------------------------
        // 4️⃣ Show the result
        // -------------------------------------------------
        System.out.println("=== OCR RESULT ===");
        System.out.println(text);
    }
}
```

**Beklenen çıktı** (örnek `scanned-document.png` net bir fatura içeriyorsa):

```
=== OCR RESULT ===
Invoice #98765
Date: 2024‑02‑28
Amount Due: $2,340.75
Please remit payment within 30 days.
```

Görüntüyü zaten tamamen hizalanmış bir dosyayla değiştirirseniz, hattın hâlâ çalıştığını—hiçbir şeyin kırılmadığını ve OCR doğruluğunun yüksek kaldığını göreceksiniz.

## Conclusion

Artık **görüntüyü eğik düzeltme (deskew)** nasıl yapılır ve her ön işleme adımının—**image preprocessing OCR**, **remove salt pepper** ve **preprocess images OCR**—temiz, aranabilir metin elde etmekteki kritik rolünü iyi biliyorsunuz. Yukarıdaki örnek eksiksiz bir çözümdür,

## What Should You Learn Next?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakın konuları ele alır. Her kaynak, adım adım açıklamalar ve tam çalışan kod örnekleri içerir; böylece ek API özelliklerini öğrenebilir ve projelerinizde alternatif uygulama yaklaşımlarını keşfedebilirsiniz.

- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Calculate Skew Angle for OCR Image Preprocessing](/ocr/english/net/skew-angle-calculation/calculate-skew-angle/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}