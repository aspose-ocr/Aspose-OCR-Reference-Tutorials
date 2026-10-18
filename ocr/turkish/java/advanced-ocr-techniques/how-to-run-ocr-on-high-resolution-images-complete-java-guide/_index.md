---
category: general
date: 2026-03-07
description: Bir TIFF dosyasında OCR'yi hızlıca çalıştırmayı, yüksek çözünürlüklü
  görüntüyü yüklemeyi, paralel OCR işleme etkinleştirmeyi ve Java'da OCR metnini çıkarmayı
  öğrenin.
draft: false
keywords:
- how to run OCR
- load high resolution image
- parallel OCR processing
- how to extract OCR text
- recognize text from tiff
language: tr
og_description: OCR çalıştırma, yüksek çözünürlüklü görüntü yükleme, paralel OCR işleme
  etkinleştirme ve TIFF dosyalarından OCR metni çıkarma konusunda adım adım rehber.
og_title: Yüksek Çözünürlüklü Görüntülerde OCR Nasıl Çalıştırılır – Java Öğreticisi
tags:
- OCR
- Java
- Image Processing
title: Yüksek Çözünürlüklü Görüntülerde OCR Nasıl Çalıştırılır – Tam Java Rehberi
url: /tr/java/advanced-ocr-techniques/how-to-run-ocr-on-high-resolution-images-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Yüksek Çözünürlüklü Görüntülerde OCR Çalıştırma – Tam Java Rehberi

Hiç **OCR nasıl çalıştırılır** diye büyük bir taranmış belgeyi uygulamanız yavaşlamadan nasıl işleyebileceğinizi merak ettiniz mi? Yalnız değilsiniz. Gerçek dünyadaki birçok projede giriş, hızlı işlenmesi gereken çok megabaytlık bir TIFF dosyasıdır ve geleneksel tek iş parçacıklı yaklaşım yeterli olmaz.  

Bu öğreticide yüksek çözünürlüklü bir görüntüyü yüklemeyi, paralel OCR işlemeyi etkinleştirmeyi ve sonunda OCR metnini çıkarmayı—temiz, üretim‑hazır Java kodu ile adım adım göstereceğiz. Sonuna kadar bir TIFF dosyasından **OCR metni nasıl çıkarılır** ve her ayarın neden önemli olduğunu tam olarak öğreneceksiniz.

## Öğrenecekleriniz

- OCR için **yüksek çözünürlüklü görüntü** dosyalarını yükleme adımları.
- OCR motorunu tüm kullanılabilir CPU çekirdeklerinde **paralel OCR işleme** için nasıl yapılandırılır.
- TIFF dosyalarından **metin tanıma** ve düz metin sonucunu alma en iyi yolu.
- İpuçları, tuzaklar ve kenar‑durum yönetimi sayesinde çözümünüz üretimde sağlam kalır.

**Önkoşullar:** Java 11+ (veya herhangi bir güncel JDK), `OcrEngine` sağlayan bir OCR kütüphanesi (ör. Tesseract‑Java veya ticari bir SDK) ve taramak istediğiniz bir TIFF dosyası. Başka bir dış araç gerekmez.

![yüksek çözünürlüklü TIFF görüntüsünde OCR nasıl çalıştırılır](ocr-highres.png)

*Görsel alt metni: yüksek çözünürlüklü TIFF görüntüsünde OCR nasıl çalıştırılır*

---

## Adım 1: Projeyi Kurun ve Bağımlılıkları İçe Aktarın

Koda girmeden önce OCR kütüphanesinin sınıf yolunuzda olduğundan emin olun. Maven kullanıyorsanız, aşağıdakine benzer bir şey ekleyin:

```xml
<dependency>
    <groupId>com.example</groupId>
    <artifactId>ocr-sdk</artifactId>
    <version>2.4.1</version>
</dependency>
```

> **Pro ipucu:** SDK’nın en son kararlı sürümünü kullanın; yeni sürümler genellikle çok‑iş parçacıklı performansı artırır ve daha iyi TIFF desteği ekler.

Şimdi demo kodumuzu barındıracak basit bir Java sınıfı oluşturun:

```java
package com.example.ocrdemo;

import com.example.ocr.OcrEngine;
import com.example.ocr.OcrResult;
import com.example.io.ImageInputStream;
import java.io.IOException;
```

Bu, temel akış için ihtiyacınız olan tüm içe aktarmalardır.

## Adım 2: OCR için Yüksek Çözünürlüklü Görüntü Yükleyin

Bir **yüksek çözünürlüklü görüntüyü** doğru şekilde yüklemek, herhangi bir OCR hattının temelidir. Düşük kaliteli bir küçük resim verirseniz, motor karakterleri tanıması için gereken detayları asla görmez.

```java
// Step 2: Load a high‑resolution TIFF image
String imagePath = "YOUR_DIRECTORY/high_res_scan.tif";
ImageInputStream imageStream = new ImageInputStream(imagePath);
```

> **Neden önemli:** `ImageInputStream` dosyayı bayt‑bayt okur, orijinal DPI’yı korur. Bazı kütüphaneler otomatik olarak küçültür; ham akışı kullanarak her noktayı tutarız, bu da daha sonra **TIFF’den metin tanıma** sırasında doğruluğu büyük ölçüde artırır.

## Adım 3: Paralel OCR İşlemeyi Etkinleştirin

Tek‑iş parçacıklı OCR, özellikle çok çekirdekli bir sunucuda darboğaz olabilir. Kullandığımız SDK, çok‑iş parçacığını tek bir bayrakla açıp kapamanıza izin verir:

```java
// Step 3: Enable parallel OCR processing
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getConfig().setUseMultiThreading(true);
ocrEngine.getConfig().setThreadCount(Runtime.getRuntime().availableProcessors());
```

> **Arka planda ne oluyor?** Motor görüntüyü parçalara (tile) ayırır, her parçayı bir işçi iş parçacığına atar ve ardından sonuçları birleştirir. İş parçacığı sayısını `availableProcessors()` ile eşleştirerek, JVM’nin donanımınız için en uygun noktayı belirlemesine izin veririz.

### Kenar‑Durum: Çok Fazla İş Parçacığı

Bu kodu CPU’yu sınırlayan bir konteyner içinde çalıştırıyorsanız, `availableProcessors()` gerçekte sahip olduğunuzdan daha yüksek bir sayı döndürebilir. Bu durumda, daha düşük bir iş parçacığı sayısını manuel olarak ayarlayın:

```java
ocrEngine.getConfig().setThreadCount(4); // safe default for 4‑core containers
```

## Adım 4: OCR Tanımasını Çalıştırın

Motor yapılandırıldı ve görüntü hazır olduğuna göre, gerçek tanıma tek satırlık bir kodla yapılır:

```java
// Step 4: Perform OCR on the high‑resolution image
OcrResult ocrResult = ocrEngine.recognize(imageStream);
```

`recognize` metodu, ham metni ve isteğe bağlı meta verileri (güven skorları, sınırlayıcı kutular vb.) içeren bir `OcrResult` nesnesi döndürür.

## Adım 5: OCR Metnini Çıkarın ve Çıktıyı Doğrulayın

Son olarak, `OcrResult` içinden **OCR metni nasıl çıkarılır** bilmemiz gerekir. SDK basit bir getter sağlar:

```java
// Step 5: Extract and display the recognized text
String extractedText = ocrResult.getText();
System.out.println("=== OCR Output ===");
System.out.println(extractedText);
```

### Beklenen Çıktı

TIFF, “Hello, World!” yazan bir taranmış sayfa içeriyorsa, şu çıktıyı görmelisiniz:

```
=== OCR Output ===
Hello, World!
```

Çıktı bozuk görünüyorsa, gerçekten **yüksek çözünürlüklü bir görüntü yüklediğinizi** ve OCR dil paketlerinin belgenin diliyle eşleştiğini iki kez kontrol edin.

## Tam Çalışan Örnek

Her şeyi bir araya getirerek, IDE’nize kopyalayıp hemen çalıştırabileceğiniz bağımsız bir program burada:

```java
package com.example.ocrdemo;

import com.example.ocr.OcrEngine;
import com.example.ocr.OcrResult;
import com.example.io.ImageInputStream;
import java.io.IOException;

/**
 * Demonstrates how to run OCR on a high‑resolution TIFF using parallel processing.
 */
public class ParallelOcrDemo {

    public static void main(String[] args) {
        try {
            // 1️⃣ Create the OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // 2️⃣ Enable multi‑core processing
            ocrEngine.getConfig().setUseMultiThreading(true);
            ocrEngine.getConfig().setThreadCount(Runtime.getRuntime().availableProcessors());

            // 3️⃣ Load the high‑resolution image
            String imagePath = "YOUR_DIRECTORY/high_res_scan.tif";
            ImageInputStream imageStream = new ImageInputStream(imagePath);

            // 4️⃣ Run OCR
            OcrResult result = ocrEngine.recognize(imageStream);

            // 5️⃣ Extract and print the text
            String text = result.getText();
            System.out.println("=== OCR Output ===");
            System.out.println(text);
        } catch (IOException e) {
            System.err.println("Failed to read the image file: " + e.getMessage());
        } catch (Exception e) {
            System.err.println("OCR processing error: " + e.getMessage());
        }
    }
}
```

Programı çalıştırın, ve çıkarılan karakterlerin konsola yazdırıldığını göreceksiniz. Bu, **OCR nasıl çalıştırılır** sorusunun uçtan uca cevabıdır; yüksek çözünürlüklü bir görüntü yüklemekten temiz metni almak kadar.

## Yaygın Sorular & Tuzaklar

| Soru | Cevap |
|----------|--------|
| **TIFF dosyam çok sayfalı olursa ne olur?** | `ImageInputStream` sayfalar arasında iterasyon yapabilir; sadece `for (int i = 0; i < imageStream.getPageCount(); i++)` döngüsüyle her sayfa için `recognize` çağırın. |
| **Bellek kullanımını sınırlayabilir miyim?** | Evet—`ocrEngine.getConfig().setMaxMemoryMb(512)` (veya başka uygun bir limit) ayarlayın. Motor gerektiğinde parçaları diske döker. |
| **Paralel işleme Windows’ta çalışır mı?** | Kesinlikle. SDK, iş parçacığı havuzunu soyutlar, bu yüzden aynı kod Linux, macOS veya Windows’ta değişiklik yapmadan çalışır. |
| **OCR dilini nasıl değiştiririm?** | `recognize`'den önce `ocrEngine.getConfig().setLanguage("eng+spa")` çağırın. Bu, birden fazla dil içeren **TIFF dosyalarından metin tanıma** gerektiğinde faydalıdır. |
| **Çıktım gereksiz satır sonları içeriyor—neden?** | OCR motoru metni tam olarak görüntüde göründüğü gibi döndürür. Sütun korumasına ihtiyacınız varsa `String.replaceAll("\\r?\\n+", "\n")` ile sonrası işleyin veya düzen‑bilgili bir ayrıştırıcı kullanın. |

## Sonuç

Yüksek çözünürlüklü bir TIFF üzerinde **OCR nasıl çalıştırılır** konusunu, **yüksek çözünürlüklü bir görüntü yüklemek**ten **paralel OCR işleme**yi etkinleştirmeye ve sonunda **OCR metni nasıl çıkarılır** konusuna kadar ele aldık. Yukarıdaki adımları izleyerek, kod tabanınızı düzenli ve sürdürülebilir tutarken daha hızlı ve güvenilir sonuçlar elde edeceksiniz.

Bir sonraki meydan okumaya hazır mısınız? Şunları deneyin:

- **Toplu işleme** tek bir çalıştırmada onlarca TIFF (bir dizin üzerinde döngü, aynı `OcrEngine` örneğini yeniden kullanın).
- **Akış OCR** görüntü verisini disk yazmadan bir ağ kaynağından besleyin.
- **İnce ayar** motorun güven eşiğini düşük kalite tanıma sonuçlarını filtreleyecek şekilde ayarlayın.

Eğer **TIFF dosyalarından metin tanıma** hakkında sorularınız varsa veya kendi performans ipuçlarınızı paylaşmak istiyorsanız, aşağıya bir yorum bırakın. Kodlamanız keyifli olsun ve OCR’nuz her zaman doğru olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}