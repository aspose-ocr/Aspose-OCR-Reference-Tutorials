---
category: general
date: 2026-01-07
description: OCR doğruluğunu artırmak ve metin görüntüsünü çıkarmak için görüntü OCR
  ön işleme – Aspose OCR ile geliştiriciler için adım adım rehber.
draft: false
keywords:
- preprocess image OCR
- extract text image
- improve OCR accuracy
- how to preprocess OCR
language: tr
og_description: OCR doğruluğunu artırmak ve metin görüntüsünü çıkarmak için görüntüyü
  ön işleme tabi tutun, Aspose OCR kullanın. Kodlu tam Java öğreticisi.
og_title: Java'da Görüntü OCR'sini Ön İşleme – Doğruluğu Artırın
tags:
- OCR
- Java
- Image Processing
title: Java'da Görüntü OCR'ını Ön İşleme – Doğruluğu Artırın ve Metni Çıkarın
url: /tr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java’da Görüntü OCR Ön İşleme – Tam Kılavuz

Hiç **preprocess image OCR** yaparken taramalarınızın lekeler ve eğik metinlerle dolu bir karmaşa gibi görünmesiyle mücadele ettiniz mi? Yalnız değilsiniz. Çoğu geliştirici, ham görüntü gürültülü, eğik ya da düşük kontrast olduğunda duvara çarpar ve OCR motoru beklenen cümleler yerine anlamsız karakterler üretir.  

İyi haber şu ki, birkaç ön işleme adımı OCR doğruluğunu **dramatically improve OCR accuracy** edebilir, sarsıntılı bir anlık görüntüyü temiz, makine‑okunur metne dönüştürebilir. Bu öğreticide, Aspose OCR for Java kullanarak **how to preprocess OCR** adımlarını tam olarak göstereceğiz ve **extract text image** içeriğini güvenilir bir şekilde nasıl çıkaracağınızı göreceksiniz.

Gereken her şeyi ele alacağız: gerekli kütüphaneler, adım‑adım kod, her seçeneğin neden önemli olduğu ve karşılaşabileceğiniz uç durumlar için ipuçları. Sonunda, gürültülü bir JPEG’i alıp temizleyen ve çıkarılan metni konsola yazdıran çalıştırmaya hazır bir programınız olacak.

---

## What You’ll Need

Başlamadan önce şunların olduğundan emin olun:

- Java Development Kit (JDK) 8 veya daha yeni bir sürüm yüklü.
- Bağımlılıkları yönetmek için Maven veya Gradle (Maven snippet’ını göstereceğiz).
- Aspose OCR for Java lisansı (ücretsiz deneme testi için yeterli).
- Örnek bir görüntü, ör. `skewed-noisy.jpg`, bilinen bir dizine yerleştirilmiş.

Hepsi bu—Aspose OCR, yerleşik ön işleme yetenekleriyle ekstra bir görüntü‑işleme kütüphanesine ihtiyaç duymadan geliyor.

---

## Step 1: Set Up Aspose OCR in Your Project

İlk olarak, `pom.xml` dosyanıza Aspose OCR bağımlılığını ekleyin. Bu, çekirdek motoru ve daha sonra kullanacağımız görüntü‑işleme yardımcılarını getirir.

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- use the latest version available -->
</dependency>
```

Gradle tercih ediyorsanız eşdeğeri şu şekildedir:

```groovy
implementation 'com.aspose:aspose-ocr:23.12'
```

> **Pro tip:** Bağımlılıklarınızı güncel tutun; yeni sürümler genellikle **improve OCR accuracy** sağlayan daha akıllı deskew algoritmaları içerir.

---

## Preprocess Image OCR – Step 2: Load the Image

Kütüphane kurulduğuna göre, bir `OcrEngine` örneği oluşturup temizlemek istediğiniz görüntüyü işaretleyebiliriz.

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // Step 2: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image you want to preprocess
        // Replace "YOUR_DIRECTORY" with the actual folder path
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/skewed-noisy.jpg"));
```

Neden önce motoru örnekliyoruz? Aspose OCR, ön işleme hattını doğrudan motorla ilişkilendirir, böylece daha sonra ayarladığınız seçenekler aynı görüntü akışını etkiler. Bu, **extract text image** işleminin ham dosya yerine temizlenmiş sürüm üzerinde çalışmasını sağlar.

---

## Improve OCR Accuracy – Step 3: Configure Preprocessing Options

Sihir `ImageProcessingOptions` içinde gerçekleşir. Her bayrak, OCR performansını olumsuz etkileyen yaygın bir kusuru hedef alır.

```java
        // Step 3: Configure image preprocessing options
        ImageProcessingOptions processingOptions = ocrEngine.getImageProcessingOptions();

        // Straighten rotated text – essential for skewed scans
        processingOptions.setDeskew(true);

        // Remove isolated pixels that look like speckles
        processingOptions.setDespeckle(true);

        // Boost contrast by 30% – helps low‑contrast prints
        processingOptions.setContrastBoost(1.3f);
```

- **Deskew**: Döndürme açısını algılar ve görüntüyü yataya geri döndürür. Olmazsa OCR motoru karakterleri yanlış yorumlayabilir.
- **Despeckle**: Noktalama işareti ya da rastgele harf olarak yanlış algılanabilecek rastgele gürültüyü temizler.
- **Contrast Boost**: Ön plan (metin) ile arka plan arasındaki farkı artırır; bu, **how to preprocess OCR** için soluk baskılarda kritik bir faktördür.

Kaynak materyalinize göre bu bayrakları istediğiniz gibi açıp kapatabilirsiniz. Örneğin, mükemmel taranmış bir belge `setDespeckle(true)` gerektirmeyebilir ve birkaç milisaniye tasarruf sağlar.

---

## Extract Text Image – Step 4: Run OCR on the Preprocessed Image

Görüntü temizlendikten sonra, Aspose OCR’dan metni tanımasını isteriz.

```java
        // Step 4: Run OCR on the preprocessed image
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the recognized text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

`recognize()` çağrısı, önceden yapılandırdığımız ön işleme hattını dahili olarak uygular, ardından karakter segmentasyonu ve tanıma işlemlerini gerçekleştirir. Sonuç, arama indeksleme, veri girişi otomasyonu gibi sonraki süreçlere besleyebileceğiniz düz metin bir dizedir.

---

## How to Preprocess OCR – Common Pitfalls & Edge Cases

### 1. Image Size Matters
Çok büyük görüntüler (ör. > 5 MP) bellek baskısına yol açabilir. `OutOfMemoryError` alırsanız, önce `processingOptions.setResizeFactor(0.5f)` ile görüntüyü yeniden boyutlandırın.

### 2. Color vs. Grayscale
Aspose OCR, gri tonlamalı görüntülerde en iyi performansı gösterir. Kaynağınız renkliyse, deskew’den önce `processingOptions.setConvertToGrayscale(true)` etkinleştirin.

### 3. Multi‑Page PDFs
PDF’lerle çalışırken, her sayfayı bir görüntü olarak çıkarıp aynı hattı bir döngü içinde çalıştırın. API, bu amaçla `PdfImageExtractor` sağlar.

### 4. Language Support
Metniniz İngilizce değilse, dili açıkça ayarlayın:

```java
ocrEngine.setLanguage(OcrLanguage.FRENCH);
```

Bu adımı atlamak, **improve OCR accuracy**’yi düşürebilir çünkü motor karakter setini tahmin etmeye çalışır.

---

## Full Working Example (Copy‑Paste Ready)

Aşağıda, derlenip çalıştırılmaya hazır tam program yer alıyor. Yer tutucu yolu gerçek görüntü konumunuzla değiştirin.

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image to be processed
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/skewed-noisy.jpg"));

        // Step 3: Configure image preprocessing options
        ImageProcessingOptions processingOptions = ocrEngine.getImageProcessingOptions();
        processingOptions.setDeskew(true);          // straighten rotated text
        processingOptions.setDespeckle(true);      // remove isolated pixels
        processingOptions.setContrastBoost(1.3f);   // boost contrast by 30%
        // Optional: processingOptions.setConvertToGrayscale(true);

        // Step 4: Run OCR on the preprocessed image
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the recognized text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**Beklenen çıktı** (kısaltılmış):

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
...
```

Eğer bozuk karakterler görürseniz, görüntü yolunun doğru olduğundan ve ön işleme bayraklarının görüntünün durumuna uygun olduğundan emin olun.

---

## Visual Summary

<img src="preprocess-ocr.png" alt="preprocess image OCR demonstration" style="max-width:100%;">

Şema, akışı gösterir: **Load → Deskew → Despeckle → Contrast Boost → Recognize → Extract Text**. Her blok, yukarıdaki kod parçacıklarına karşılık gelir.

---

## Conclusion

Aspose OCR kullanarak Java’da **preprocess image OCR** yapmanın pratik bir yolunu adım adım inceledik; proje kurulumundan **improve OCR accuracy** sağlayan ince ayar seçeneklerine kadar her şeyi kapsadık. Deskew, despeckle ve contrast‑boost uygulayarak gürültülü, eğik bir JPEG’i temiz, aranabilir metne dönüştürürsünüz—tam da **extract text image** verisini sonraki uygulamalara aktarmak istediğinizde ihtiyacınız olan şey.

Sırada ne var? `setBinarizationThreshold` gibi ikili görüntüler için diğer ön işleme özelliklerini deneyin ya da birden fazla görüntüyü tek bir toplu işte zincirleyin. Sonucu Apache Tika ile indeksleyebilir veya bir dil modeli ile duygu analizi yapabilirsiniz. **how to preprocess OCR** temellerini kavradıktan sonra sınır yoktur.

Belirli bir dosya türü ya da dil hakkında sorularınız mı var? Aşağıya yorum bırakın, iyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}