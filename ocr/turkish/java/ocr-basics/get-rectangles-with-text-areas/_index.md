---
date: 2026-06-19
description: Java'da image'ı text'e dönüştürmeyi, image'dan paragrafları çıkarmayı
  ve Aspose OCR Java library kullanarak text area rectangles'ı almayı öğrenin.
keywords:
- image to text java
- convert scanned image text
- extract paragraphs from image
- aspose ocr java tutorial
linktitle: Image to Text Java – Image'dan Text'i Tanı ve Text Area Rectangles'ı Al
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to convert image to text in Java, extract paragraphs from
    image, and retrieve text area rectangles using Aspose OCR Java library.
  headline: Image to Text Java – Convert Image to Text and Retrieve Text Area Rectangles
  type: TechArticle
- description: Learn how to convert image to text in Java, extract paragraphs from
    image, and retrieve text area rectangles using Aspose OCR Java library.
  name: Image to Text Java – Convert Image to Text and Retrieve Text Area Rectangles
  steps:
  - name: Set Up Your Project
    text: Create a new Java project (or add to an existing one) and place the Aspose.OCR
      JAR on the classpath. If you use Maven, add the dependency as described in the
      download package.
  - name: Define Document Directory and Image Path
    text: 'Specify where your sample image resides:'
  - name: Create AsposeOCR Instance
    text: '`AsposeOCR` is the main class that provides OCR functionality. Instantiate
      the OCR engine:'
  - name: Recognize Text in the Image
    text: Load your image and call `RecognizePage` to convert the picture into plain
      text. This single method call performs image preprocessing, character segmentation,
      and language‑specific recognition in one step.
  - name: Get Rectangles with Text Areas
    text: Retrieve the bounding rectangles for each paragraph (or other area types).
      This step returns a collection of `Rectangle` objects that precisely enclose
      the detected text blocks, enabling you to highlight or further process individual
      sections. CODE_BLOCK_PLACEHOLDER_5_END
  type: HowTo
- questions:
  - answer: Yes, Aspose.OCR works with Java 11 and later versions.
    question: Is Aspose.OCR compatible with Java 11?
  - answer: Yes, you can use it in any type of project. For licensing details, visit
      [here](https://purchase.aspose.com/buy).
    question: Can I use Aspose.OCR for both personal and commercial projects?
  - answer: You can obtain a temporary license [here](https://purchase.aspose.com/temporary-license/).
    question: How do I obtain a temporary license for evaluation?
  - answer: For support and discussions, visit the [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16).
    question: Where can I find community support or official assistance?
  - answer: Yes, the library is thread‑safe and can be used in concurrent environments
      for better performance.
    question: Does Aspose.OCR support multithreading?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Image to Text Java – Image'ı Text'e Dönüştür ve Text Area Rectangles'ı Al
url: /tr/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüden Metin Java – Görüntüyü Metne Dönüştür ve Metin Alanı Dikdörtgenlerini Al

## Giriş

Bir Java uygulamasında **görüntüyü metne dönüştürmek** istiyorsanız, Aspose.OCR for Java hızlı ve doğru bir çözüm sunar. Bu öğreticide, bir görüntüden paragrafları çıkarmak, her metin alanı için sınırlayıcı dikdörtgenleri elde etmek ve bu koordinatları konsola yazdırmak için gereken adımları adım adım göstereceğiz. Sonunda bu yaklaşımın neden çalıştığını, kütüphaneyi nasıl entegre edeceğinizi ve kendi kullanım senaryolarınız için nerede genişletebileceğinizi anlayacaksınız.

## Hızlı Yanıtlar
`AreasType` bir metin segmentasyonu seviyesini (kelimeler, satırlar, paragraflar) belirten bir enumdur.

- **“Görüntüden metni tanıma” ne anlama geliyor?** Bir resimdeki görsel karakterleri düzenlenebilir dize verisine dönüştürmek anlamına gelir.  
- **Java’da bunu hangi kütüphane yönetiyor?** Aspose.OCR for Java.  
- **Geliştirme için lisansa ihtiyacım var mı?** Test için geçici bir lisans mevcuttur; üretim için tam lisans gereklidir.  
- **Tek kelimeler yerine paragraflar çıkarabilir miyim?** Evet – paragraf‑seviyesindeki dikdörtgenleri almak için `AreasType.PARAGRAPHS` kullanın.  
- **Kod Java 11+ ile uyumlu mu?** Kesinlikle, API Java 11 ve sonraki sürümlerle çalışır.

## Aspose.OCR'de “görüntüyü metne dönüştürmek” nedir?

`convert image to text`, bir bitmap'i analiz etmeyi, OCR algoritmalarını uygulamayı ve tanınan karakterleri bir dize olarak döndürmeyi ifade eder. Aspose.OCR’un `RecognizePage` yöntemi, bu dönüşümü gerçekleştirirken isteğe bağlı olarak her algılanan metin bloğu için kesin `Rectangle` koordinatlarını da sağlar.

## Neden bu **java ocr library**'yi kullanmalısınız?

Aspose.OCR **30+ dil** destekler ve **50 MB**'a kadar görüntüyü bütün dosyayı belleğe yüklemeden işleyebilir, tipik sunucu donanımında saniyenin altında yanıt süreleri sunar. Kütüphane çok iş parçacıklı kullanım için güvenlidir, yalnızca tek bir JAR gerektirir ve ham metin, HTML ve kesin metin‑alanı dikdörtgenleri dahil esnek çıktı formatları sunar—yüksek hacimli kurumsal senaryolar için idealdir.

## Önkoşullar

- **Java Development Kit** (JDK 11 veya daha yeni) makinenizde kurulu olmalı.  
- **Aspose.OCR for Java** kütüphanesi – resmi siteden [buradan](https://releases.aspose.com/ocr/java/) indirin.  
- JAR bağımlılığını yönetmek için bir IDE veya yapı aracı (Maven/Gradle).

## Paketleri İçe Aktar

Java projenizde gerekli sınıfları içe aktarın:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AreasType;
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Adım‑Adım Kılavuz

### Adım 1: Projenizi Kurun
Yeni bir Java projesi oluşturun (veya mevcut bir projeye ekleyin) ve Aspose.OCR JAR dosyasını sınıf yoluna yerleştirin. Maven kullanıyorsanız, indirme paketinde açıklanan bağımlılığı ekleyin.

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### Adım 2: Belge Dizini ve Görüntü Yolunu Tanımlayın
Örnek görüntünüzün bulunduğu yeri belirtin:

```java
// Create AsposeOCR instance
AsposeOCR api = new AsposeOCR();
```

### Adım 3: AsposeOCR Örneği Oluşturun
`AsposeOCR` OCR işlevselliği sağlayan ana sınıftır.

OCR motorunu örnekleyin:

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### Adım 4: Görüntüdeki Metni Tanıyın
Görüntünüzü yükleyin ve resmi düz metne dönüştürmek için `RecognizePage` metodunu çağırın. Bu tek metod çağrısı, görüntü ön işleme, karakter segmentasyonu ve dil‑spesifik tanıma işlemlerini bir adımda gerçekleştirir.

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

### Adım 5: Metin Alanlarıyla Dikdörtgenleri Alın
Her paragraf (veya diğer alan tipleri) için sınırlayıcı dikdörtgenleri alın. Bu adım, algılanan metin bloklarını tam olarak çevreleyen `Rectangle` nesnelerinin bir koleksiyonunu döndürür; böylece bireysel bölümleri vurgulayabilir veya daha ileri işlem yapabilirsiniz.

CODE_BLOCK_PLACEHOLDER_5_END

## Yaygın Sorunlar ve Sorun Giderme

| Belirti | Muhtemel Neden | Çözüm |
|---------|----------------|-------|
| `IOException` on `RecognizePage` | Yanlış dosya yolu veya eksik okuma izni | `imagePath`'in mevcut bir PNG/JPG'ye işaret ettiğini ve uygulamanın dosya sistemi erişimine sahip olduğunu doğrulayın. |
| Empty result string | Düşük kalite görüntü veya desteklenmeyen dil | Görüntüyü ön işleyin (kontrastı artırın, ikilileştirin) veya doğru dili `api.setLanguage("eng")` ile belirtin. |
| No rectangles returned | Yanlış `AreasType` kullanımı (ör. paragraflar beklenirken `WORDS`) | Gerektiği gibi `AreasType.PARAGRAPHS` veya `AreasType.LINES`'a geçiş yapın. |

## Sıkça Sorulan Sorular

**S: Aspose.OCR Java 11 ile uyumlu mu?**  
C: Evet, Aspose.OCR Java 11 ve sonraki sürümlerle çalışır.

**S: Aspose.OCR'ı kişisel ve ticari projelerde kullanabilir miyim?**  
C: Evet, her türlü projede kullanabilirsiniz. Lisans detayları için [burayı](https://purchase.aspose.com/buy) ziyaret edin.

**S: Değerlendirme için geçici bir lisans nasıl alınır?**  
C: Geçici bir lisansı [buradan](https://purchase.aspose.com/temporary-license/) alabilirsiniz.

**S: Topluluk desteği veya resmi yardım nereden bulunur?**  
C: Destek ve tartışmalar için [Aspose.OCR forumunu](https://forum.aspose.com/c/ocr/16) ziyaret edin.

**S: Aspose.OCR çok iş parçacıklı çalışmayı destekliyor mu?**  
C: Evet, kütüphane çok iş parçacıklı ortamlar için güvenlidir ve daha iyi performans sağlamak amacıyla eşzamanlı olarak kullanılabilir.

## Sonuç

Bu **aspose ocr java tutorial**'da Aspose.OCR for Java kullanarak **görüntüyü metne dönüştürmeyi**, paragrafları çıkarmayı ve her metin bloğunu çevreleyen kesin dikdörtgenleri elde etmeyi öğrendiniz. Bu yetenekler, aranabilir PDF'ler oluşturmanıza, UI katmanlarında metni vurgulamanıza veya yapılandırılmış veriyi sonraki süreçlere aktarmanıza olanak tanır. API'yi daha fazla keşfederek dil ayarlarını özelleştirebilir, farklı görüntü formatlarını işleyebilir veya bulut depolama ile entegre edebilirsiniz.

---

**Last Updated:** 2026-06-19  
**Tested With:** Aspose.OCR 23.10 for Java  
**Author:** Aspose  

{{< blocks/products/products-backtop-button >}}

## İlgili Eğitimler

- [Metin Görüntülerini Çıkar – Aspose.OCR for Java ile OCR Temelleri](/ocr/java/ocr-basics/)
- [Aspose.OCR Detect Areas Mode ile Java’da Görüntüden Metin Çıkarma](/ocr/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Aspose.OCR BufferedImage Kullanarak Java’da Görüntüyü Metne Dönüştür](/ocr/java/advanced-ocr-techniques/perform-ocr-buffered-image/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}