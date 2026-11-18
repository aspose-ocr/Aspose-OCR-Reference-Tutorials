---
category: general
date: 2026-08-12
description: Java OCR motoru kullanarak görüntüden metni tanıyın. Görüntüden metin
  nasıl çıkarılır, OCR doğruluğu nasıl artırılır ve PNG dosyalarında OCR için görüntü
  nasıl ön işlenir öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize text from image
- how to extract text from image
- how to improve OCR accuracy
- how to preprocess image for OCR
- perform OCR on PNG
language: tr
lastmod: 2026-08-12
og_description: Java ile görüntüden metin tanıma. Bu öğreticide görüntüden metin çıkarma,
  OCR doğruluğunu artırma ve çoklu iş parçacığı ile GPU kullanarak PNG üzerinde OCR
  gerçekleştirme gösterilmektedir.
og_image_alt: Diagram showing Java OCR engine recognizing text from image
og_title: Java'da görüntüden metin tanıma – adım adım OCR öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: recognize text from image using Java OCR engine. Learn how to extract
    text from image, improve OCR accuracy, and preprocess image for OCR on PNG files.
  headline: recognize text from image in Java – complete OCR guide
  type: TechArticle
- description: recognize text from image using Java OCR engine. Learn how to extract
    text from image, improve OCR accuracy, and preprocess image for OCR on PNG files.
  name: recognize text from image in Java – complete OCR guide
  steps:
  - name: Explanation of each step
    text: '| Step | Why it matters | How it helps you **recognize text from image**
      | |------|----------------|-----------------------------------------------|
      | 1️⃣ Create the OCR engine | Instantiates the core component that drives all
      subsequent operations. | Provides the entry point for all OCR actions. | '
  - name: Expected output
    text: 'If `sample-image.png` contains the sentence “Hello, world! 123”, the console
      will display something similar to:'
  - name: 1. Binarization with Otsu’s method
    text: '```java import java.awt.image.BufferedImage; import com.example.image.Binarizer;
      // hypothetical helper class'
  - name: 2. Scaling to 300 dpi
    text: '```java import com.example.image.Resizer;'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Java’da görüntüden metin tanıma – tam OCR rehberi
url: /tr/java/advanced-ocr-techniques/recognize-text-from-image-in-java-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüden metin tanıma Java’da – tam OCR rehberi

Java uygulamasında **görüntüden metin tanıma** ihtiyacınız varsa, bu öğretici tam olarak nasıl yapılacağını gösterir. Rehberin sonunda görüntü dosyalarından metin çıkarabilecek, OCR doğruluğunu artırabilecek ve çok çekirdekli ve GPU desteğiyle PNG varlıkları üzerinde OCR çalıştırabileceksiniz.

Birçok geliştirici, özel bir sinir ağı yazmadan **görüntüden metin nasıl çıkarılır** diye merak eder. Çözüm, kanıtlanmış bir OCR motoru kullanmak, onu hız ve doğruluk için yapılandırmak ve doğru ön işleme adımlarını uygulamaktır. Aşağıdaki bölümler her gereksinimi adım adım anlatır, böylece kodu doğrudan projenize kopyalayabilirsiniz.

## Öğrenecekleriniz

* Java’da bir OCR motoru kurun.
* Çok iş parçacıklı çalışmayı ve isteğe bağlı GPU hızlandırmasını etkinleştirin.
* İngilizce ve İspanyolca için dil paketleri ekleyin.
* Tanıma kalitesini artırmak için görüntü ön işleme filtreleri uygulayın.
* Daha temiz çıktı için yerleşik yazım düzelticiyi açın.
* PNG dosyalarında OCR gerçekleştirin ve tanınan metni yazdırın.

Harici hizmetlere gerek yok—her şey yerel olarak çalışır, bu da çevrim dışı veya gizlilik‑duyarlı uygulamalar için idealdir.

## Önkoşullar

* Java 17 veya daha yeni (kod modern `var` sözdizimini kullanıyor ancak geriye dönük olarak da kullanılabilir).
* `OcrEngine`, `Language` ve `EngineOptions` sınıflarını sağlayan bir OCR kütüphanesi (ör. **GroupDocs.Parser**, **Aspose.OCR** veya uyumlu herhangi bir SDK).
* Bağımlılık yönetimi için Maven veya Gradle.
* `sample-image.png` adlı örnek bir PNG görüntüsü `YOUR_DIRECTORY` içinde yer almalı.

> **Pro ipucu:** Binlerce görüntü işleyecekseniz, GPU tamponu için yeterli RAM ayırın ve yalnızca ham OCR çıktısına ihtiyacınız olduğunda yazım düzelticiyi devre dışı bırakın.

## Java OCR motoru ile görüntüden metin tanıma

Aşağıda, orijinal kod parçacığında gösterilen sekiz adımı izleyen tam, çalıştırılabilir bir Java programı bulunmaktadır. İçe aktarmaları, bir `main` metodunu ve her satırın amacını açıklayan satır içi yorumları içerir.

```java
// File: OcrDemo.java
import com.example.ocr.OcrEngine;            // Replace with your OCR library's package
import com.example.ocr.Language;
import com.example.ocr.EngineOptions;
import com.example.ocr.ImagePreprocessingOptions;

public class OcrDemo {

    public static void main(String[] args) {
        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable multi‑core processing for faster throughput
        ocrEngine.getEngineOptions().setUseMultiThreading(true);

        // Step 3: (Optional) Turn on GPU acceleration if a compatible GPU is present
        ocrEngine.getEngineOptions().setUseGpu(true);

        // Step 4: Add the languages you want to recognize (English and Spanish)
        ocrEngine.getLanguage().add(Language.English);
        ocrEngine.getLanguage().add(Language.Spanish);

        // Step 5: Apply common image‑preprocessing filters to improve OCR accuracy
        ImagePreprocessingOptions imgOpts = ocrEngine.getImagePreprocessingOptions();
        imgOpts.setRotate(true);   // Auto‑rotate based on EXIF orientation
        imgOpts.setDeskew(true);   // Straighten skewed text lines
        imgOpts.setDenoise(true);  // Reduce background noise

        // Step 6: Enable the built‑in spell corrector for cleaner output
        ocrEngine.getEngineOptions().setUseSpellCorrector(true);

        // Step 7: Perform OCR on the target PNG image
        // This demonstrates how to perform OCR on PNG files efficiently.
        String imagePath = "YOUR_DIRECTORY/sample-image.png";
        String ocrResult = ocrEngine.recognizeImage(imagePath);

        // Step 8: Output the recognized text
        System.out.println("=== OCR Result ===");
        System.out.println(ocrResult);
    }
}
```

### Her adımın açıklaması

| Adım | Neden Önemli | **görüntüden metin tanıma** nasıl yardımcı olur |
|------|----------------|-----------------------------------------------|
| 1️⃣ OCR motorunu oluştur | Sonraki tüm işlemleri yönlendiren çekirdek bileşeni örnekler. | Tüm OCR eylemleri için giriş noktasını sağlar. |
| 2️⃣ Çok çekirdekli işlemeyi etkinleştir | Modern CPU'lar birden çok çekirdeğe sahiptir; bunları kullanmak toplam işlem süresini azaltır. | PNG dosyalarında **paralel olarak OCR gerçekleştirirken** toplu işleri hızlandırır. |
| 3️⃣ GPU hızlandırmasını aç (isteğe bağlı) | GPU'lar paralel piksel işlemlerinde, özellikle büyük görüntülerde mükemmeldir. | Desteklenen donanımlarda tanıma süresini %70'e kadar azaltabilir. |
| 4️⃣ Dil paketleri ekle | OCR doğruluğu dil modellerine bağlıdır; yalnızca gereken dilleri belirtmek yanlış pozitifleri azaltır. | Çok dilli senaryolarda **görüntüden metin nasıl çıkarılır** sorusunu yanıtlayarak karakterleri doğru tanıma şansını artırır. |
| 5️⃣ Görüntü ön işleme | Döndürme, eğikliği düzeltme ve gürültü giderme yaygın tarama sorunlarını düzeltir. | Motorun daha temiz bir bitmap almasını sağlayarak **OCR doğruluğunu nasıl artırılır** sorusuna doğrudan yanıt verir. |
| 6️⃣ Yazım düzeltici | Yaygın OCR yazım hatalarını düzelten bir son‑işlem adımı. | Manuel temizlik yapmadan daha okunabilir çıktı sağlar. |
| 7️⃣ PNG üzerinde OCR gerçekleştir | `recognizeImage` yöntemi dosyayı okur, ön işleme uygular ve tanıma hattını çalıştırır. | **PNG üzerinde OCR gerçekleştir** ve format‑özel özellikleri (ör. kayıpsız sıkıştırma) ele alır. |
| 8️⃣ Sonucu yazdır | Başarıyı doğrulamak için anında geri bildirim verir. | Metnin doğru şekilde **görüntüden tanındığını** onaylamanızı sağlar. |

### Beklenen çıktı

`sample-image.png` dosyası “Hello, world! 123” cümlesini içeriyorsa, konsol aşağıdakine benzer bir şey gösterecektir:

```
=== OCR Result ===
Hello, world! 123
```

Tam çıktı, görüntü kalitesi ve dil ayarlarına bağlı olarak biraz değişebilir, ancak yazım düzeltici genellikle “Helli” → “Hello” gibi küçük tanıma hatalarını düzeltir.

## OCR için görüntü ön işleme – derinlemesine inceleme

Yukarıdaki kod motorun yerleşik ön işleme özelliğini kullansa da, görüntüyü OCR motoruna vermeden önce özel filtreler de uygulayabilirsiniz. Aşağıda iki yaygın teknik yer almaktadır:

### 1. Otsu yöntemiyle ikileştirme

```java
import java.awt.image.BufferedImage;
import com.example.image.Binarizer; // hypothetical helper class

BufferedImage original = ImageIO.read(new File(imagePath));
BufferedImage binary = Binarizer.otsuThreshold(original);
ocrEngine.recognizeImage(binary);
```

İkileştirme, görüntüyü siyah‑beyaz'a dönüştürür; bu genellikle düşük kontrastlı taramalarda **OCR doğruluğunu nasıl artırılır** sorusuna çözüm olur.

### 2. 300 dpi’ye ölçekleme

```java
import com.example.image.Resizer;

BufferedImage scaled = Resizer.scaleToDPI(original, 300);
ocrEngine.recognizeImage(scaled);
```

Çoğu OCR motoru, optimal karakter tanıma için en az 300 dpi bekler. Ölçekleme, motorun çok küçük glifleri yanlış okumasını önler.

> **Not:** Hem özel ön işleme hem de motorun yerleşik seçeneklerini etkinleştirirseniz, motor filtrelerini *sizininkinden sonra* uygular. Görüntü özelliklerinize en uygun sıralamayı seçin.

## Görüntüden metin çıkarma – kenar durumlarıyla başa çıkma

| Durum | Önerilen ayar |
|-----------|-------------------|
| **Çok gürültülü arka plan** | `setDenoise(true)` yoğunluğunu artırın veya OCR'den önce bir medyan filtresi çalıştırın. |
| **Eğim > 15°** | `setDeskew(true)` kullanın *ve* `imgOpts.setRotateAngle(θ)` ile manuel bir dönüş açısı sağlayın. |
| **Karışık diller (ör. İngilizce + İspanyolca)** | Adım 4'te gösterildiği gibi her iki dil paketini ekleyin; motor bağlamı otomatik olarak değiştirir. |
| **PNG'ye dönüştürülmüş büyük PDF'ler** | Her sayfayı ayrı bir PNG olarak işleyin ve sonuçları birleştirin; çok iş parçacıklı (Adım 2) toplam süreyi düşük tutar. |
| **GPU mevcut değil** | `setUseGpu(true)` tutun ancak bir try‑catch içinde sarın; motor çökmeden CPU'ya geri dönecektir. |

## PNG üzerinde OCR gerçekleştirme – toplu işleme örneği

Bir dizindeki **PNG dosyalarında OCR gerçekleştirmek** gerektiğinde, aynı motor örneğiyle basit bir döngü iyi çalışır:

```java
Path dir = Paths.get("YOUR_DIRECTORY");
try (Stream<Path> files = Files.list(dir)) {
    files.filter(p -> p.toString().endsWith(".png"))
         .forEach(p -> {
             String text = ocrEngine.recognizeImage(p.toString());
             System.out.println("File: " + p.getFileName());
             System.out.println(text);
             System.out.println("---");
         });
}
```

Motor zaten çok çekirdekli ve GPU için yapılandırıldığı için, bu döngü ek kod olmadan paralel olarak onlarca görüntüyü işleyebilir.

## Tam çalışan örnek

Her şeyi bir araya getirerek, IDE'ye kopyalayıp yapıştırabileceğiniz, uygun Maven bağımlılığını ekleyebileceğiniz ve hemen çalıştırabileceğiniz bağımsız bir sınıf:



## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Aspose.OCR Kullanarak Dil ile Görüntü Metnini OCR Yapma](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Aspose.OCR Detect Areas Modu ile Java’da Görüntüden Metin Çıkarma](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [image to text java: Aspose.OCR ile Görüntüyü Metne Dönüştürme](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}