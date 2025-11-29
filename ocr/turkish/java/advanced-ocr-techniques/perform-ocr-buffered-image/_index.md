---
date: 2025-11-29
description: Görüntülerden metin çıkarmayı Java OCR kütüphanesiyle öğrenin. Bu rehber,
  Aspose OCR'ı nasıl kuracağınızı, birden çok dili nasıl yöneteceğinizi ve çeşitli
  OCR görüntü formatlarıyla nasıl çalışacağınızı gösterir.
language: tr
linktitle: Performing OCR on BufferedImage in Aspose.OCR for Java
second_title: Aspose.OCR Java API
title: Java OCR Kütüphanesi (Aspose.OCR) Kullanarak BufferedImage Üzerinde OCR Yapma
url: /java/advanced-ocr-techniques/perform-ocr-buffered-image/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# BufferedImage Üzerinde OCR Yapma – Java OCR Kütüphanesi (Aspose.OCR)

## Giriş

Java’da **görüntülerden metin çıkarmak** istiyorsanız güvenilir bir *java ocr library* şarttır. Bu öğreticide, Aspose.OCR – güçlü bir Java OCR kütüphanesi – kullanarak bir `BufferedImage` üzerinden doğrudan metin tanıma işlemini nasıl yapacağınızı göstereceğiz. Kütüphaneyi kurma, bir görüntüyü yükleme ve tanınan dizeyi alma adımlarını sadece birkaç satır kodla göreceksiniz.

## Hızlı Yanıtlar
- **En iyi java ocr library hangisidir?** Aspose.OCR for Java yüksek doğruluk ve geniş dil desteği sunar.  
- **Aspose OCR nasıl kurulur?** JAR dosyasını Aspose web sitesinden indirip projenizin classpath’ine ekleyin.  
- **Birden fazla dili tanıyabilir miyim?** Evet—Aspose.OCR kutudan çıktığı gibi birden çok dili destekler.  
- **Hangi görüntü formatları destekleniyor?** Kütüphane PNG, JPEG, BMP ve TIFF gibi yaygın OCR görüntü formatlarıyla çalışır.  
- **Metin çıkarmak için tipik kod nasıl olur?** Görüntüyü bir `BufferedImage` içine yükleyin, bir `AsposeOCR` örneği oluşturun ve `RecognizePage` metodunu çağırın.

## Java OCR Kütüphanesi Nedir?
Bir *java ocr library*, raster görüntüleri analiz edip görsel metni makine‑okunur dizgelere dönüştürebilen Java sınıflarının bir setidir. Aspose.OCR for Java, yüksek hassasiyetli tanıma, dil algılama ve çok çeşitli görüntü formatı desteği sunan bir kütüphanedir.

## Neden Aspose.OCR for Java?
- **Yüksek doğruluk** hem basılı hem el yazısı belgelerde.  
- **OCR multiple languages** desteği; İngilizce, Fransızca, Almanca, Çince ve daha birçok dil.  
- `BufferedImage` ile doğrudan çalışan basit API, ara dosya dönüşümlerine gerek kalmaz.  
- **ocr image formats** desteği: PNG, JPEG, BMP, TIFF ve GIF.

## Ön Koşullar

Başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:

1. **Java Development Kit (JDK)** – herhangi bir güncel sürüm (8 veya üzeri). İndirmek için [Oracle](https://www.oracle.com/java/technologies/javase-downloads.html) sitesine göz atın.  
2. **Aspose.OCR for Java library** – en son JAR dosyasını Aspose indirme sayfasından alın ([install aspose ocr](https://releases.aspose.com/ocr/java/)).  
3. **Örnek görüntülerin bulunduğu bir klasör** – kod içinde `dataDir` değişkenini bu klasöre işaret edecek şekilde güncelleyin.

## Paketleri İçe Aktarma

Başlamak için gerekli sınıfları içe aktarın. Bu blok değişmeden kalır; sadece Aspose OCR API’si ve Java I/O yardımcılarını kapsam içine alır.

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;
```

## BufferedImage Üzerinde OCR Nasıl Yapılır

Adım adım ilerleyeceğiz. Her adım kısa bir açıklama ve ardından (orijinal koddan değişmeyen) kod parçacığını içerir.

### Adım 1: Belge Dizini ve Görüntü Yolu Ayarlama  
Görüntülerinizin nerede olduğunu tanımlayın ve işlemek istediğiniz dosyayı gösterin.

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

> **İpucu:** Geliştirme sırasında `FileNotFoundException` almamak için mutlak yol kullanın, üretim ortamına geçerken göreli yola dönün.

### Adım 2: AsposeOCR Örneği Oluşturma  
OCR motorunu başlatın. Bu nesne tüm tanıma metodlarına erişim sağlar.

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

### Adım 3: BufferedImage’dan Sayfa Tanıma  
Görüntüyü bir `BufferedImage` içine yükleyin, OCR motorunu çalıştırın ve sonucu ekrana yazdırın.

```java
// Recognize page from BufferedImage
try {
    BufferedImage loaded = ImageIO.read(new File(imagePath));
    String result = api.RecognizePage(loaded);
    System.out.println("Result BufferedImage: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

**Ne oluyor?**  
1. `ImageIO.read` dosyayı belleğe `BufferedImage` olarak okur.  
2. `api.RecognizePage` gerçek OCR işlemini gerçekleştirir.  
3. Tanınan metin bir `String` olarak döner ve konsola yazdırılır.

İhtiyacınız olan her görüntü için bu üç adımı tekrarlayın—sadece `imagePath` değerini değiştirin.

## Yaygın Sorunlar & Çözümler

| Sorun | Sebep | Çözüm |
|-------|--------|-----|
| `NullPointerException` on `loaded` | Görüntü dosyası bulunamadı veya desteklenmeyen format | Yolun doğruluğunu kontrol edin ve dosyanın desteklenen **ocr image format** (PNG, JPEG, BMP, TIFF) olduğundan emin olun. |
| Bozuk çıktı | Dil ayarlanmamış veya desteklenmeyen karakterler | AsposeOCR otomatik dil algılar, ancak `api.setLanguage("eng")` gibi ISO kodlarıyla dili açıkça belirtebilirsiniz. |
| Büyük görüntülerde yavaş performans | Yüksek çözünürlük çok fazla bellek tüketir | Tanımadan önce `BufferedImage.getScaledInstance` ile görüntüyü küçültün. |

## Sık Sorulan Sorular (Orijinal)

### Q1: Aspose.OCR birden fazla dili destekliyor mu?

A1: Evet, Aspose.OCR geniş bir dil yelpazesini destekler ve çeşitli metin tanıma ihtiyaçları için uygundur.

### Q2: Aspose.OCR farklı görüntü formatlarıyla uyumlu mu?

A2: Kesinlikle! Aspose.OCR çeşitli formatlardaki görüntüleri işleyebilir, OCR projelerinizde esneklik sağlar.

### Q3: Aspose.OCR ne sıklıkla güncelleniyor?

A3: Aspose, özellikleri geliştirmek ve sorunları gidermek için düzenli olarak güncellemeler yayınlar. En yeni bilgiler için [belgelendirme](https://reference.aspose.com/ocr/java/) sayfasına bakın.

### Q4: Aspose.OCR’ı satın almadan deneyebilir miyim?

A4: Evet, ücretsiz deneme sürümünü [burada](https://releases.aspose.com/) bulabilirsiniz.

### Q5: Aspose.OCR için topluluk desteği nereden alınır?

A5: Topluluk desteği ve tartışmalar için [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) adresini ziyaret edin.

## Ek SSS (Yeni)

**S: Aspose OCR’ı bir Maven projesine nasıl eklerim?**  
C: Aspose OCR bağımlılığını, Aspose indirme sayfasında verilen koordinatlarla `pom.xml` dosyanıza ekleyin.

**S: Bu kütüphaneyi taranmış bir PDF’den metin çıkarmak için kullanabilir miyim?**  
C: Evet—her PDF sayfasını bir görüntüye (ör. Aspose.PDF ile) dönüştürün ve aynı `BufferedImage` OCR iş akışını uygulayın.

**S: Renkli görüntülerde OCR desteği var mı?**  
C: Kesinlikle. Aspose OCR renkli, gri tonlamalı ve ikili görüntülerle çalışır; ancak yüksek kontrastlı siyah‑beyaz görüntüler genellikle en iyi doğruluğu verir.

**S: Tek bir çalıştırmada işleyebileceğim sayfa sayısında bir limit var mı?**  
C: Katı bir limit yok, ancak bellek tüketimi görüntü boyutuyla artar. `OutOfMemoryError` almamak için büyük partileri bölerek işleyin.

**S: El yazısı metin için doğruluğu nasıl artırabilirim?**  
C: El yazısı modunu (varsa) etkinleştirin veya kontrastı artırıp gürültüyü azaltarak görüntüyü ön‑işlemden geçirin.

---

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Son Güncelleme:** 2025-11-29  
**Test Edilen Sürüm:** Aspose.OCR 24.11 for Java  
**Yazar:** Aspose