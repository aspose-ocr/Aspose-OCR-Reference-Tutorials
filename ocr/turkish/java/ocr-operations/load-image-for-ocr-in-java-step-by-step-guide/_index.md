---
category: general
date: 2026-03-07
description: Java'da OCR için resmi hızlıca yükleyin. OCR motorunu nasıl ayarlayacağınızı,
  ROI'yi nasıl tanımlayacağınızı ve metni nasıl çıkaracağınızı öğrenin – tam kod örneği
  ve OCR ayarlama ipuçları içerir.
draft: false
keywords:
- load image for OCR
- how to set OCR
- OCR region of interest
- Java OCR example
- image processing Java
language: tr
og_description: Java'da OCR için görüntü yükleyin ve OCR motorunu nasıl ayarlayacağınızı
  öğrenin. Bu rehber, ROI işleme, döndürme ve tam kod konularında size yol gösterir.
og_title: Java'da OCR için Görüntü Yükleme – Tam Programlama Rehberi
tags:
- OCR
- Java
- Image Processing
title: Java’da OCR için Görüntü Yükleme – Adım Adım Rehber
url: /tr/java/ocr-operations/load-image-for-ocr-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java’da OCR için Görüntü Yükleme – Tam Programlama Rehberi

Hiç **load image for OCR** yapmanız gerektiğinde hangi çağrıları yapacağınızdan emin olmadınız mı? Yalnız değilsiniz—çoğu geliştirici, ilk görüntü geldiğinde ve OCR motoru kafası karıştığında bu duvara çarpar. İyi haber şu ki, doğru adımları bildiğinizde çözüm oldukça basittir.

Bu öğreticide **how to set OCR** parametrelerini gösterecek, ilgi bölgesi (ROI) tanımlayacak ve sonunda o resim diliminden metni çekeceğiz. Sonunda OCR için bir görüntü yükleyen, gerekirse otomatik döndüren ve çıkarılan metni yazdıran çalıştırılabilir bir Java programınız olacak—hiçbir gizemli el hareketi olmadan.

## İhtiyacınız Olanlar

- Java 17 veya daha yeni (kod, kısalık için `var` anahtar kelimesini kullanıyor, ancak gerekirse daha eski bir sürüme geçebilirsiniz).  
- `OcrEngine`, `OcrResult` ve `ImageInputStream` sınıflarını sağlayan bir OCR SDK – **Tesseract‑Java**, **ABBYY** gibi kütüphaneleri veya özel bir çözümü düşünebilirsiniz.  
- Okumak istediğiniz metni içeren bir örnek görüntü (`multi_page_form.png`).  
- Basit bir IDE (IntelliJ IDEA, Eclipse, VS Code) – herhangi biri yeterli.

Temel mantık için ekstra Maven veya Gradle sihirbazlığı gerekmez; sadece OCR JAR dosyasını sınıf yolunuza ekleyin, yeter.

## Adım 1: OCR Motorunu Kurun – How to Set OCR Doğru Şekilde

**load image for OCR** yapmadan önce, ne araması gerektiğini bilen bir motor örneğine ihtiyacınız var. Çoğu SDK, bir yapılandırma nesnesi sunar; burada motoru ROI içindeki metni otomatik döndürmesi için ayarlarsınız.

```java
import com.example.ocr.OcrEngine;   // Replace with your actual package
import com.example.ocr.OcrConfig;

public class OcrSetup {
    public static OcrEngine createEngine() {
        OcrEngine engine = new OcrEngine();

        // Enable automatic rotation handling within the region of interest
        engine.getConfig().setAutoRotateWithinRegion(true);

        // You can also tweak language, confidence thresholds, etc.
        // engine.getConfig().setLanguage("eng");
        // engine.getConfig().setMinConfidence(0.75);

        return engine;
    }
}
```

**Neden önemli:** `setAutoRotateWithinRegion` özelliğini açmak, size çok fazla son‑işlemden tasarruf sağlar. Kullanıcının sayfayı birkaç derece eğdiği taranmış bir formu hayal edin—bu bayrak olmadan OCR anlamsız karakterler okur. Bunu etkinleştirmek *how to set OCR* seçenekleri, kutudan çıkar çıkmaz sağlamlık sağlar.

## Adım 2: OCR için Görüntü Yükleme – Motoru Besleme

Motor hazır olduğunda, gerçekte **load image for OCR** yaparız. `ImageInputStream` sınıfı dosya işlemlerini soyutlar ve OCR SDK'nın bir akışı doğrudan tüketmesine izin verir.

```java
import com.example.ocr.ImageInputStream;
import java.nio.file.Paths;

public class ImageLoader {
    public static ImageInputStream load(String path) throws Exception {
        // Validate the file exists and is readable
        if (!java.nio.file.Files.isReadable(Paths.get(path))) {
            throw new IllegalArgumentException("Cannot read image at: " + path);
        }

        // Create the stream – most SDKs accept a simple file path, but a stream is more flexible
        return new ImageInputStream(path);
    }
}
```

**İpucu:** Çok sayfalı PDF'lerle çalışıyorsanız, birçok OCR kütüphanesi akış yapıcısına bir sayfa indeksi geçirmenize izin verir. Böylece ek dönüşüm adımları olmadan sayfalar arasında döngü yapabilirsiniz.

## Adım 3: İlgi Bölgesi (ROI) Tanımlama

Tüm resmi taramak, özellikle büyük formlar için gereksiz olabilir. Odak noktasını bir dikdörtgene daraltarak işleme süresini hızlandırır ve doğruluğu artırırsınız.

```java
import java.awt.Rectangle;

public class RoiHelper {
    public static Rectangle defineRoi() {
        // x, y, width, height – adjust these numbers to match your form layout
        int x = 120;
        int y = 350;
        int width = 800;
        int height = 200;

        return new Rectangle(x, y, width, height);
    }
}
```

**Köşe durumu:** ROI görüntü sınırlarının dışına çıkarsa, çoğu motor bir istisna fırlatır. Hızlı bir tutarlılık kontrolü (ör. `x + width` ile `image.getWidth()` karşılaştırması) çöküşleri önleyebilir.

## Adım 4: ROI Üzerinde OCR Çalıştırma

Motor, görüntü ve ROI hazır olduğunda, **load image for OCR** zamanı geldi ve metni gerçekten tanımalısınız.

```java
import com.example.ocr.OcrResult;

public class OcrRunner {
    public static OcrResult run(OcrEngine engine,
                                ImageInputStream image,
                                Rectangle roi) throws Exception {
        // The recognize method returns both text and confidence data
        return engine.recognize(image, roi);
    }
}
```

Her kelime için güven puanına ihtiyacınız varsa, `OcrResult` genellikle her girişin `getConfidence()` metoduna sahip olduğu bir `getWords()` koleksiyonu sunar. Düşük güvenli kelimeleri filtrelemek, sonraki doğrulama için kullanışlı olabilir.

## Adım 5: Metni Çıkarın ve Çıktıyı Doğrulayın

Son olarak, çıkarılan dizeyi yazdırıyoruz. Gerçek bir uygulamada muhtemelen bir veritabanına yazarsınız veya bir ayrıştırıcıya beslersiniz, ancak bir konsol çıktısı gösterim için yeterlidir.

```java
public class RoiOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create and configure the OCR engine
        OcrEngine ocrEngine = OcrSetup.createEngine();

        // Step 2: Load the image you want to process
        ImageInputStream imageStream = ImageLoader.load("YOUR_DIRECTORY/multi_page_form.png");

        // Step 3: Define where to look – the ROI
        Rectangle regionOfInterest = RoiHelper.defineRoi();

        // Step 4: Run OCR limited to that region
        OcrResult ocrResult = OcrRunner.run(ocrEngine, imageStream, regionOfInterest);

        // Step 5: Show the result
        System.out.println("ROI text:");
        System.out.println(ocrResult.getText());
    }
}
```

### Beklenen Çıktı

ROI içinde “Invoice #12345” ifadesi olduğunu varsayarsak, şöyle bir şey göreceksiniz:

```
ROI text:
Invoice #12345
Date: 2026-03-07
Total: $1,250.00
```

OCR motoru herhangi bir metin bulamazsa, `ocrResult.getText()` boş bir dize döndürür – ROI koordinatlarını veya görüntü kalitesini tekrar kontrol etmek için iyi bir işarettir.

## Yaygın Tuzakların Ele Alınması

| Problem | Neden Olur | Hızlı Çözüm |
|---------|------------|-------------|
| **Boş çıktı** | ROI görüntü sınırlarının dışında veya görüntü düşük kontrastlı gri tonlamalı. | Koordinatları bir görüntü düzenleyiciyle doğrulayın; OCR'den önce kontrastı artırın veya ikilileştirin. |
| **Bozuk karakterler** | Döndürme işlenmemiş veya yanlış dil paketi. | `setAutoRotateWithinRegion(true)` etkin olduğundan emin olun; doğru dil modelini yükleyin (`engine.getConfig().setLanguage("eng")`). |
| **Performans gecikmesi** | Tüm görüntüyü ROI yerine işlemek. | Her zaman tarama alanını sınırlamak için bir `Rectangle` geçirin; büyük görüntüleri önce küçültmeyi düşünün. |
| **Bellek dışı hatalar** | Çok büyük görüntüler ham bayt olarak yükleniyor. | Streaming API'lerini (`ImageInputStream`) kullanın ve destekleniyorsa döşeme işleme isteyin. |

**Pro ipucu:** Çok sayfalı formlarla çalışırken, OCR çağrısını sayfa indeksini artıran bir döngü içinde sarın. Çoğu SDK, aynı `OcrEngine` örneğini yeniden kullanmanıza izin verir, bu da başlatma yükünü azaltır.

## Daha İleri – Daha Fazla Şeye İhtiyacınız Olursa?

- **Toplu işleme:** Dosya yolu listesi toplayın, üzerinde döngü yapın ve her OCR sonucunu bir CSV dosyasına kaydedin.  
- **Dinamik ROI:** Form alanlarını otomatik olarak tespit etmek için OpenCV kullanın, ardından bu koordinatları OCR adımına besleyin.  
- **Son‑işleme:** ROI'dan çıkarılan tarihleri, fatura numaralarını veya para birimi değerlerini temizlemek için regex kalıpları uygulayın.  

Bu uzantıların tümü, az önce ele aldığımız temel modele dayanır: **load image for OCR**, **how to set OCR** yapılandırması, bir bölge tanımlama, motoru çalıştırma ve sonucu işleme.

![Form üzerindeki ROI'nin vurgulandığını gösteren ekran görüntüsü – load image for OCR örneği](roi-screenshot.png "load image for OCR örneği")

*Görsel alt metni: load image for OCR – örnek bir formda vurgulanan ilgi bölgesi.*

## Sonuç

Artık Java’da **load image for OCR** nasıl yapılır, **how to set OCR** seçenekleri doğru şekilde nasıl ayarlanır ve belirli bir bölgeden metin nasıl çıkarılır gösteren eksiksiz, çalıştırılabilir bir örneğiniz var. Adımlar modülerdir, böylece farklı bir OCR kütüphanesiyle değiştirebilir veya ROI'yi yeniden ayarlayabilirsiniz, tüm kodu yeniden yazmanıza gerek kalmaz.

Sırada, farklı görüntü formatları (TIFF, BMP) ile denemeler yapın veya gürültülü taramalarda doğruluğu artırmak için OpenCV ile bir ön‑işleme adımı ekleyin. Birden çok sayfayı nasıl ele alacağınızı merak ediyorsanız, `RoiOcrExample` içindeki döngüyü sayfa indeksleri üzerinde yinelemek için genişletin.

Kodlamaktan keyif alın, ve OCR sonuçlarınız her zaman kristal gibi net olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}