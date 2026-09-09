---
category: general
date: 2026-01-07
description: Aspose OCR Java kullanarak bir görüntüden OCR metni alın. Metin görüntüsünü
  nasıl çıkaracağınızı, görüntüyü OCR’ye nasıl yükleyeceğinizi öğrenin ve birkaç dakika
  içinde bir Java OCR örneği çalıştırın.
draft: false
keywords:
- get OCR text
- extract text image
- java OCR example
- aspose OCR Java
- load image OCR
language: tr
og_description: Aspose OCR Java ile görüntülerden OCR metni alın. Bu kılavuz, bir
  Java OCR örneğini, görüntüden metnin nasıl çıkarılacağını ve görüntü OCR'sinin nasıl
  verimli bir şekilde yapılacağını gösterir.
og_title: Java’da OCR Metni Al – Tam Aspose OCR Öğreticisi
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Java’da OCR Metnini Al – Tam Aspose OCR Örneği
url: /tr/java/ocr-basics/get-ocr-text-in-java-complete-aspose-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java’da OCR Metni Al – Tam Aspose OCR Örneği

Tarayıcıdan bir belgeyi **OCR metni olarak almak** istediğinizde hangi kütüphaneyi seçeceğinizi bilemediğiniz oldu mu? Tek başınıza değilsiniz. Gerçek dünyadaki birçok projede—fatura otomasyonu, fiş işleme veya çok dilli form dijitalleştirme gibi—görüntülerden metin çıkarmak otomasyonun ilk adımıdır.  

Bu öğreticide, Aspose OCR for Java kütüphanesini kullanan bir **java OCR örneği** üzerinden adım adım ilerleyeceğiz. Sonunda **görüntü OCR yükleme**, motoru çalıştırma ve sadece birkaç satır kodla **metin görüntüsü** verisini çıkarma konularını öğreneceksiniz. Gereksiz ayrıntı yok, doğrudan projenize kopyalayıp yapıştırabileceğiniz pratik bir çözüm.

## Öğrenecekleriniz

- Aspose OCR for Java’ı (Maven koordinatları dahil) nasıl kurulur.  
- **Görüntü OCR yükleme** ve bir dil belirtmenin tam adımları.  
- **OCR metnini** düz bir string olarak alıp konsola nasıl yazdırılır.  
- Çok dilli görüntüler ve otomatik dil algılaması için ipuçları.  

*Önkoşullar*: Java 8 ve üzeri, Maven uyumlu bir IDE (IntelliJ IDEA, Eclipse veya VS Code) ve geçerli bir Aspose OCR for Java lisansı (değerlendirme için ücretsiz deneme sürümü yeterli).

---

![Flowchart showing how to get OCR text from an image using Aspose OCR Java](https://example.com/ocr-flowchart.png "Get OCR text flow diagram")

## Adım 1 – Aspose OCR Bağımlılığını Ekleyin (Görüntü OCR Yükleme)

Öncelikle Maven’a Aspose OCR kütüphanesini indirmesini söyleyin. `pom.xml` dosyanızı açın ve `<dependencies>` içinde aşağıdaki `<dependency>` bloğunu ekleyin:

```xml
<!-- Aspose OCR for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest version available -->
</dependency>
```

> **Pro ipucu**: Gradle kullanıyorsanız eşdeğeri `implementation 'com.aspose:aspose-ocr:23.9'` şeklindedir. Bağımlılığı eklemek, projenize **görüntü OCR yükleme** yeteneklerini kazandırmanın en ucuz yoludur.

## Adım 2 – OCR Motorunu Oluşturun ve Görüntünüzü Yükleyin

Şimdi bir `OcrEngine` örneği oluşturan, bir görüntü dosyasına işaret eden ve motorun tanıyacağı dili belirten küçük bir Java sınıfı yazacağız. Dil, ISO‑639‑2 kodu ile tanımlanır (ör. Tamil için `"tam"`).

```java
package com.example.ocr;

import com.aspose.ocr.*;

public class LanguageExample {

    public static void main(String[] args) throws Exception {
        // 2️⃣ Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // 2️⃣ Load the image you want to process – this is the "load image OCR" step
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multilingual.png"));

        // 2️⃣ Choose the language (ISO‑639‑2). Change "tam" to any supported code.
        engine.getEngineOptions().setLanguage("tam");
        // If you prefer automatic detection, uncomment the next line:
        // engine.getEngineOptions().setAutoDetectLanguage(true);
```

### Neden dili açıkça ayarlamalısınız?

Dili belirtmek yanlış pozitifleri azaltır ve tanıma hızını artırır. Çok dilli PDF’lerde dil kodları dizisi üzerinde döngü kurabilir ya da rahatlık için otomatik algılamayı etkinleştirebilirsiniz.

## Adım 3 – OCR İşlemini Çalıştırın ve **OCR Metnini Alın**

Motor yapılandırıldıktan sonra bir sonraki satır tanıma işlemini gerçekleştirir. Sonuç nesnesi çıkarılan string’i ve ek meta verileri içerir.

```java
        // 3️⃣ Perform OCR – this is where we finally **get OCR text**
        OcrResult result = engine.recognize();

        // 3️⃣ Output the recognized text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

`LanguageExample` sınıfını çalıştırdığınızda aşağıdaki gibi bir çıktı görmelisiniz:

```
=== Extracted Text ===
தமிழ் உரை இங்கு வருகிறது...
```

`setAutoDetectLanguage(true)` kullandıysanız, motor sizin için dili tahmin etmeye çalışır; bu, bilinmeyen belgelerle çalışırken oldukça kullanışlıdır.

## Adım 4 – Yaygın Kenar Durumlarını Ele Alma (Metin Görüntüsü Varyasyonlarını Çıkarma)

### Düşük Çözünürlüklü Görüntülerle Baş Etme

OCR doğruluğu 300 dpi’nin altına düştüğünde keskin bir şekilde azalır. Kaynak görüntünüz düşük çözünürlüklüyse, önce yükseltmeyi düşünün:

```java
engine.getEngineOptions().setResolution(300); // forces 300 DPI
```

### Arka Plan Gürültüsünü Kaldırma

Bazen taranmış formlarda motoru şaşırtan lekeler bulunur. Ön işleme etkinleştirilebilir:

```java
engine.getEngineOptions().setPreprocessMode(EngineOptions.PreprocessMode.Auto);
```

### Belirli Bölgelerden Metin Çıkarma

Sadece belirli bir dikdörtgenden (ör. bir tablo hücresi) metin gerekiyorsa, `recognize()` çağırmadan önce bir `Rectangle` ayarlayın:

```java
engine.setRegion(new Rectangle(50, 100, 400, 200));
```

Bu ayarlamalar, **java OCR örneğinizi** üretim ortamları için yeterince sağlam hâle getirir.

## Adım 5 – Çıktıyı Doğrulama (Ne Beklemelisiniz?)

Başarılı bir çalıştırma, görüntünün düz metin versiyonunu konsola yazdırır. Çok dilli görüntülerde karışık yazı tipleri görebilirsiniz:

```
Hello World
こんにちは世界
مرحبا بالعالم
```

Çıktı boş ya da bozuk ise şu kontrolleri yapın:

1. `setImage` içindeki dosya yolu (doğru mu?).  
2. Dil kodu, görüntüdeki yazı tipine uygun mu?  
3. Görüntü kalitesi (kontrast, DPI) yeterli mi?

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda tüm dosya yer alıyor, derlenip çalıştırılmaya hazır. `YOUR_DIRECTORY/multilingual.png` kısmını test görüntünüzün gerçek yolu ile değiştirin.

```java
package com.example.ocr;

import com.aspose.ocr.*;

public class LanguageExample {
    public static void main(String[] args) throws Exception {
        // Initialize OCR engine
        OcrEngine engine = new OcrEngine();

        // Load the image – this is the core "load image OCR" step
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multilingual.png"));

        // Set language (ISO‑639‑2). For Tamil use "tam". Change as needed.
        engine.getEngineOptions().setLanguage("tam");
        // Uncomment for auto‑detect:
        // engine.getEngineOptions().setAutoDetectLanguage(true);

        // Optional: improve accuracy on low‑res images
        // engine.getEngineOptions().setResolution(300);
        // engine.getEngineOptions().setPreprocessMode(EngineOptions.PreprocessMode.Auto);

        // Perform OCR and retrieve text
        OcrResult result = engine.recognize();

        // Print the extracted text – this is how we **get OCR text**
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

Derleyin ve çalıştırın:

```bash
mvn compile exec:java -Dexec.mainClass="com.example.ocr.LanguageExample"
```

Şimdi çıkarılan içeriğin konsolda göründüğünü göreceksiniz.

---

## Sonuç

Aspose OCR for Java kullanarak bir görüntüden **OCR metni almanın** nasıl yapılacağını gösterdik. Bu **java OCR örneğini** izleyerek **metin görüntüsü** verisini çıkarabilir, **görüntü OCR yükleme** yapabilir ve çok dilli ya da gürültülü girdiler için motoru ayarlayabilirsiniz.  

Bundan sonra şunları yapabilirsiniz:

- OCR adımını daha büyük bir iş akışına entegre etmek (ör. metni bir veritabanına kaydetmek).  
- Çok dilli taramaları tek bir dile dönüştürmek için bir çeviri API’si ile birleştirmek.  
- PDF dönüşümü veya barkod algılama gibi diğer Aspose OCR özelliklerini denemek.

Deneyin, birkaç şey kırın ve ayarları mükemmel sonuç alana kadar iyileştirin. İyi kodlamalar, OCR’unuz her zaman kristal berraklığında olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}