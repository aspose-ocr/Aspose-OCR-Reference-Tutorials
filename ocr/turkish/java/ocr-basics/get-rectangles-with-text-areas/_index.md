---
date: 2026-02-09
description: Aspose OCR Java kütüphanesini kullanarak görüntüyü metne dönüştürmeyi
  ve metin alanı dikdörtgenlerini çıkarmayı öğrenin. Kod örnekleriyle adım adım rehber.
linktitle: Recognize Text from Image and Retrieve Text Area Rectangles
second_title: Aspose.OCR Java API
title: Görüntüyü Metne Dönüştür – Görüntüden Metni Tanı ve Metin Alanı Dikdörtgenlerini
  Al
url: /tr/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüyü Metne Dönüştür – Görüntüden Metni Tanıma ve Metin Alanı Dikdörtgenlerini Alma

## Giriş

Bir Java uygulamasında **görüntüyü metne dönüştürme** ve **görselden metni tanıma** dosyalarına ihtiyaç duyuyorsanız, Aspose.OCR for Java bu işlemi hızlı ve doğru bir şekilde yapmanızı sağlar. Bu öğreticide, bir görüntüden paragrafları nasıl çıkaracağınızı, her metin alanı için sınırlayıcı dikdörtgenleri nasıl elde edeceğinizi ve bu koordinatları konsola nasıl yazdıracağınızı adım adım göstereceğiz. Sonunda bu yaklaşımın neden çalıştığını, kütüphaneyi nasıl entegre edeceğinizi ve kendi senaryolarınız için nerelerde genişletebileceğinizi anlayacaksınız.

## Hızlı Yanıtlar
- **“görselden metni tanıma” ne anlama geliyor?** Bir resimdeki görsel karakterlerin düzenlenebilir dize verisine dönüştürülmesi anlamına gelir.  
- **Java’da bunu hangi kütüphane sağlıyor?** Aspose.OCR for Java.  
- **Geliştirme için lisansa ihtiyacım var mı?** Test için geçici bir lisans mevcuttur; üretim için tam lisans gereklidir.  
- **Tek tek kelimeler yerine paragrafları çıkarabilir miyim?** Evet – `AreasType.PARAGRAPHS` kullanarak paragraf‑düzeyinde dikdörtgenler alabilirsiniz.  
- **Kod Java 11+ ile uyumlu mu?** Kesinlikle, API Java 11 ve sonraki sürümlerle çalışır.

## Aspose.OCR'de “görüntüyü metne dönüştür” ne anlama geliyor?
Aspose.OCR’nin `RecognizePage` metodu bitmap'i analiz eder, OCR algoritmalarını uygular ve tanınan dizeyi döndürür. Metin alanları talep edildiğinde, kütüphane ayrıca her metin bloğu için tam `Rectangle` koordinatlarını hesaplar; böylece daha sonra belirli bölümleri vurgulamak veya işlemek kolaylaşır.

## Neden bu **java ocr kütüphanesini** kullanmalısınız?
- **Yüksek doğruluk** – birden çok dili ve karmaşık yazı tiplerini destekler.  
- **Kolay entegrasyon** – tek bir JAR tam OCR yeteneklerini ekler.  
- **Esnek çıktı** – ham metin, biçimlendirilmiş HTML veya kesin metin‑alanı dikdörtgenlerini alabilirsiniz.  
- **Thread‑safe** – yüksek verimli sunucu ortamları için uygundur.

## Önkoşullar

- **Java Development Kit** (JDK 11 veya daha yeni) makinenizde kurulu olmalı.  
- **Aspose.OCR for Java** kütüphanesi – resmi siteden [buradan](https://releases.aspose.com/ocr/java/) indirin.  
- JAR bağımlılığını yönetmek için bir IDE veya yapı aracı (Maven/Gradle).

## Paketleri İçe Aktarma

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

## Adım Adım Kılavuz

### Adım 1: Projenizi Kurun
Yeni bir Java projesi oluşturun (veya mevcut bir projeye ekleyin) ve Aspose.OCR JAR dosyasını sınıf yoluna (classpath) yerleştirin. Maven kullanıyorsanız, indirme paketinde açıklanan bağımlılığı ekleyin.

### Adım 2: Belge Dizini ve Görüntü Yolunu Tanımlayın
Örnek görüntünüzün nerede bulunduğunu belirtin:

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### Adım 3: Aspose.OCR Örneği Oluşturun
OCR motorunu başlatın:

```java
// Create AsposeOCR instance
AsposeOCR api = new AsposeOCR();
```

### Adım 4: Görüntüdeki Metni Tanıyın
`RecognizePage` metodunu çağırarak resmi düz metne dönüştürün. Bu adım, temel **recognize text image java** yeteneğini gösterir:

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
Şimdi her paragraf (veya diğer alan tipleri) için sınırlayıcı dikdörtgenleri alın. Bu adımda **extract paragraphs from image** işlemini yapar ve koordinatlarını elde edersiniz:

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

## Yaygın Sorunlar ve Çözümleme

| Belirti | Muhtemel Neden | Çözüm |
|---------|----------------|-------|
| `IOException` on `RecognizePage` | Yanlış dosya yolu veya eksik okuma izni | `imagePath`'in mevcut bir PNG/JPG dosyasına işaret ettiğini ve uygulamanın dosya sistemine erişimi olduğunu doğrulayın. |
| Boş sonuç dizesi | Düşük kalite görüntü veya desteklenmeyen dil | Görüntüyü ön‑işleme (kontrast artırma, ikilileştirme) yapın veya `api.setLanguage("eng")` ile doğru dili belirtin. |
| Dikdörtgen döndürülmedi | Yanlış `AreasType` kullanımı (ör. paragraflar beklerken `WORDS`) | İhtiyaca göre `AreasType.PARAGRAPHS` veya `AreasType.LINES`'a geçiş yapın. |

## Sıkça Sorulan Sorular

**S: Aspose.OCR Java 11 ile uyumlu mu?**  
C: Evet, Aspose.OCR Java 11 ve sonraki sürümlerle çalışır.

**S: Aspose.OCR'ı kişisel ve ticari projelerde kullanabilir miyim?**  
C: Evet, her türlü projede kullanabilirsiniz. Lisans detayları için [burayı](https://purchase.aspose.com/buy) ziyaret edin.

**S: Değerlendirme için geçici bir lisans nasıl alınır?**  
C: Geçici lisansı [buradan](https://purchase.aspose.com/temporary-license/) alabilirsiniz.

**S: Topluluk desteği veya resmi yardım nereden bulunur?**  
C: Destek ve tartışmalar için [Aspose.OCR forumunu](https://forum.aspose.com/c/ocr/16) ziyaret edin.

**S: Aspose.OCR çoklu iş parçacığını (multithreading) destekliyor mu?**  
C: Evet, kütüphane thread‑safe'dir ve daha iyi performans için eşzamanlı ortamlarda kullanılabilir.

## Sonuç

Bu **aspose ocr java tutorial** içinde Aspose.OCR for Java kullanarak **görüntüyü metne dönüştürme**, paragrafları çıkarma ve her metin bloğunu çevreleyen kesin dikdörtgenleri elde etme konularını öğrendiniz. Bu yetenekler, aranabilir PDF'ler oluşturmanıza, UI katmanlarında metni vurgulamanıza veya yapılandırılmış veriyi sonraki süreçlere aktarmanıza olanak tanır. API'yi daha fazla keşfederek dil ayarlarını özelleştirebilir, farklı görüntü formatlarını işleyebilir veya bulut depolama ile bütünleştirebilirsiniz.

---

**Last Updated:** 2026-02-09  
**Tested With:** Aspose.OCR 23.10 for Java  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}