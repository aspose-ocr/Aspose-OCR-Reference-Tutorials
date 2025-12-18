---
date: 2025-12-10
description: Aspose.OCR for Java kullanarak görüntüden metin tanımayı ve görüntüden
  paragrafları çıkarmayı öğrenin. Kod örnekleriyle adım adım rehber.
linktitle: Recognize Text from Image and Retrieve Text Area Rectangles
second_title: Aspose.OCR Java API
title: Görüntüden Metni Tanı ve Metin Alanı Dikdörtgenlerini Al
url: /tr/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüden Metin Tanıma ve Metin Alanı Dikdörtgenlerini Alma

## Giriş

Java uygulamanızda **görüntüden metin tanıma** yapmanız gerekiyorsa, Aspose.OCR for Java bu işlemi hızlı ve doğru bir şekilde gerçekleştirmenizi sağlar. Bu öğreticide, bir görüntüden paragrafları çıkarmak, her metin alanı için sınırlayıcı dikdörtgenleri elde etmek ve bu koordinatları konsola yazdırmak için gereken adımları adım adım göstereceğiz. Sonunda bu yaklaşımın neden işe yaradığını, kütüphaneyi nasıl entegre edeceğinizi ve kendi kullanım senaryolarınız için nerelerde genişletebileceğinizi anlayacaksınız.

## Hızlı Yanıtlar
- **“görüntüden metin tanıma” ne anlama geliyor?** Bir resimdeki görsel karakterlerin düzenlenebilir dize verisine dönüştürülmesi demektir.  
- **Java’da bunu hangi kütüphane sağlıyor?** Aspose.OCR for Java.  
- **Geliştirme için lisansa ihtiyacım var mı?** Test için geçici bir lisans mevcuttur; üretim için tam lisans gereklidir.  
- **Tek tek kelimeler yerine paragrafları çıkarabilir miyim?** Evet – paragraf‑düzeyindeki dikdörtgenleri almak için `AreasType.PARAGRAPHS` kullanın.  
- **Kod Java 11+ ile uyumlu mu?** Kesinlikle, API Java 11 ve üzeri sürümlerle çalışır.

## Aspose.OCR’da “görüntüden metin tanıma” nedir?
Aspose.OCR’un `RecognizePage` yöntemi bitmap’i analiz eder, OCR algoritmalarını uygular ve tanınan dizeyi döndürür. Metin alanları istediğinizde, kütüphane aynı zamanda her metin bloğu için tam `Rectangle` koordinatlarını hesaplar; böylece daha sonra belirli bölümleri vurgulamak veya işlemek kolaylaşır.

## Neden Aspose.OCR for Java?
- **Yüksek doğruluk** – birden çok dili ve karmaşık yazı tiplerini destekler.  
- **Kolay entegrasyon** – tek bir JAR tam OCR yeteneklerini ekler.  
- **Esnek çıktı** – ham metin, biçimlendirilmiş HTML veya kesin metin‑alan dikdörtgenlerini alabilirsiniz.  
- **İş parçacığı‑güvenli** – yüksek verimli sunucu ortamları için uygundur.

## Önkoşullar

- **Java Development Kit** (JDK 11 veya daha yeni) makinenizde kurulu olmalı.  
- **Aspose.OCR for Java** kütüphanesi – resmi siteden [buradan](https://releases.aspose.com/ocr/java/) indirebilirsiniz.  
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

### Adım 2: Belge Dizini ve Görüntü Yolunu Tanımlayın
Örnek görüntünüzün bulunduğu yeri belirtin:

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### Adım 3: Aspose.OCR Örneğini Oluşturun
OCR motorunu başlatın:

```java
// Create Aspose.OCR instance
AsposeOCR api = new AsposeOCR();
```

### Adım 4: Görüntüdeki Metni Tanıyın
`RecognizePage` metodunu çağırarak resmi düz metne dönüştürün. Bu adım, temel **görüntüden metin tanıma** yeteneğini gösterir:

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### Adım 5: Metin Alanlarıyla Dikdörtgenleri Alın
Şimdi her paragraf (veya diğer alan tipleri) için sınırlayıcı dikdörtgenleri alın. Bu, **görüntüden paragrafları çıkarma** ve koordinatlarını elde etme aşamasıdır:

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

## Yaygın Sorunlar ve Sorun Giderme

| Belirti | Muhtemel Neden | Çözüm |
|---------|----------------|-------|
| `IOException` on `RecognizePage` | Yanlış dosya yolu veya eksik okuma izni | `imagePath` geçerli bir PNG/JPG dosyasına işaret ediyor ve uygulamanın dosya sistemine erişimi olduğundan emin olun. |
| Boş sonuç dizesi | Düşük kalite görüntü veya desteklenmeyen dil | Görüntüyü ön‑işleme tabi tutun (kontrastı artırın, ikilileştirin) veya `api.setLanguage("eng")` ile doğru dili belirtin. |
| Dikdörtgen döndürülmüyor | Yanlış `AreasType` kullanımı (ör. paragraflar beklerken `WORDS` seçilmiş) | İhtiyaca göre `AreasType.PARAGRAPHS` veya `AreasType.LINES` kullanın. |

## Sık Sorulan Sorular

**S: Aspose.OCR Java 11 ile uyumlu mu?**  
C: Evet, Aspose.OCR Java 11 ve sonraki sürümlerle çalışır.

**S: Aspose.OCR’ı kişisel ve ticari projelerde kullanabilir miyim?**  
C: Evet, her türlü projede kullanabilirsiniz. Lisans detayları için [burayı](https://purchase.aspose.com/buy) ziyaret edin.

**S: Değerlendirme için geçici bir lisans nasıl alabilirim?**  
C: Geçici lisansı [buradan](https://purchase.aspose.com/temporary-license/) temin edebilirsiniz.

**S: Topluluk desteği veya resmi yardım nereden bulunur?**  
C: Destek ve tartışmalar için [Aspose.OCR forumunu](https://forum.aspose.com/c/ocr/16) ziyaret edin.

**S: Aspose.OCR çoklu iş parçacığını destekliyor mu?**  
C: Evet, kütüphane iş parçacığı‑güvenlidir ve daha iyi performans için eşzamanlı ortamlarda kullanılabilir.

## Sonuç

Bu öğreticide, Aspose.OCR for Java kullanarak **görüntüden metin tanıma** dosyalarını nasıl gerçekleştireceğinizi, paragrafları nasıl çıkaracağınızı ve her metin bloğunu çevreleyen tam dikdörtgenleri nasıl alacağınızı öğrendiniz. Bu yetenekler, aranabilir PDF’ler oluşturmanıza, UI kaplamalarında metni vurgulamanıza veya yapılandırılmış veriyi sonraki süreçlere aktarmanıza olanak tanır. API’yı daha fazla keşfederek dil ayarlarını özelleştirebilir, farklı görüntü formatlarını işleyebilir veya bulut depolama ile entegre edebilirsiniz.

---

**Son Güncelleme:** 2025-12-10  
**Test Edilen Sürüm:** Aspose.OCR 23.10 for Java  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}