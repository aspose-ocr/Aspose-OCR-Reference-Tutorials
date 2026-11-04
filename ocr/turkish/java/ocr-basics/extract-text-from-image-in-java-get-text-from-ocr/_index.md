---
category: general
date: 2026-05-25
description: Java’da OCR kullanarak görüntüden metin çıkarın. OCR için görüntünün
  nasıl yükleneceğini, fotoğraftan metnin nasıl tanınacağını ve basit bir kod örneğiyle
  OCR’dan metnin nasıl alınacağını öğrenin.
draft: false
keywords:
- extract text from image
- get text from ocr
- recognize text from photo
- java image to text
- load image for ocr
language: tr
og_description: Java’da görüntüden metin çıkarma, adım adım kılavuzla. OCR için görüntüyü
  yüklemeyi, fotoğraftan metni tanımayı ve OCR’den verimli bir şekilde metin almayı
  öğrenin.
og_title: Java'da Görüntüden Metin Çıkar – OCR'den Metin Al
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  headline: Extract Text from Image in Java – Get Text from OCR
  type: TechArticle
- description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  name: Extract Text from Image in Java – Get Text from OCR
  steps:
  - name: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
    text: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
  - name: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
    text: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
  - name: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
    text: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
  - name: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
    text: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
  - name: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
    text: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Java’da Görüntüden Metin Çıkar – OCR’dan Metin Al
url: /tr/java/ocr-basics/extract-text-from-image-in-java-get-text-from-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüden Metin Çıkarma Java’da – OCR’dan Metin Al

Hiç **görüntüden metin çıkarma** ihtiyacı duydunuz ama hangi Java kütüphanesini seçeceğinize karar veremediniz mi? Yalnız değilsiniz. İster makbuzları dijitalleştiriyor, ürün fotoğraflarından seri numaralarını alıyor, ister sadece eğlenceli bir yan proje ile oynuyor olun, bir resmi düzenlenebilir metne dönüştürmek yaygın bir engel.

Bu öğreticide, **load image for OCR** nasıl yapılır, motor nasıl yapılandırılır ve sonunda **recognize text from photo** nasıl yapılır gösteren, tamamen çalıştırılabilir bir örnek üzerinden adım adım ilerleyeceğiz. **get text from OCR** sadece birkaç satır kodla elde edilecek. Belirsiz referanslar yok—gereken her şey burada.

## What You’ll Learn

* Java’da hafif bir OCR motoru nasıl kurulur.  
* **load image for OCR** ve farklı dosya yollarının nasıl ele alınacağına dair tam adımlar.  
* Dil yapılandırmasının, İngilizce olmayan **extract text from image** işlemlerinde neden önemli olduğu.  
* Sonucu güvenli bir şekilde nasıl çıktıya alacağınız ve motor hiçbir şey döndürdüğünde ne yapmanız gerektiği.  
* En yaygın tuzaklardan kaçınmak için birkaç profesyonel ipucu.

Bu rehberin sonunda, Ukraynaca karakterler içeren bir JPEG (veya PNG) dosyasını okuyup tanınan dizeyi konsola yazdıran bağımsız bir programınız olacak. Dili ya da görüntüyü istediğiniz gibi değiştirebilirsiniz—her şey modüler.

---

![Java OCR motoru kullanarak görüntüden metin çıkarma akış diyagramı](/images/extract-text-from-image-java.png)

*Alt text: Java OCR motoru kullanarak görüntüden metin çıkarma akış diyagramı.*

## Prerequisites

* **Java Development Kit (JDK) 11+** – kod modern modül sistemini kullanıyor, ancak eski sürümler küçük ayarlamalarla çalışabilir.  
* **Maven or Gradle** – OCR kütüphanesini çekmek için (biz **Asprise OCR**’yi hafif ve ücretsiz bir geliştirme seçeneği olarak kullanacağız).  
* Programınızın okuyabileceği bir örnek görüntü dosyası (ör. `ukrainian_sign.jpg`).  
* Java’nın `main` metodu ve istisna yönetimi hakkında temel bilgi.

Bunlara sahipseniz hazırsınız. Değilseniz Oracle ya da AdoptOpenJDK’den JDK’yı indirin ve basit bir Maven projesi kurun—çok karmaşık bir şey değil.

---

## Step 1: Add the OCR Dependency

İlk olarak, build aracınıza OCR motorunu çekmesini söyleyin. Maven için `pom.xml` içine şunu ekleyin:

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.0.2</version>
</dependency>
```

Gradle tercih ediyorsanız eşdeğeri:

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.0.2'
```

Bu koordinatlar, `OcrEngine`, `OcrLanguage` ve kullanacağımız yardımcı sınıfları içeren kompakt bir JAR getirir. Temel Latin ve Kiril alfabeleri için ekstra yerel ikili dosyalar gerekmez.

---

## Step 2: Create a Java Class to **Extract Text from Image**

Şimdi gerçek programı yazacağız. Aşağıdakileri `src/main/java/com/example/ocr/ExtractTextDemo.java` içine kaydedin.

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;

/**
 * Demonstrates how to extract text from image using Asprise OCR.
 * The example loads a JPEG, sets the language to Ukrainian,
 * runs recognition, and prints the result.
 */
public class ExtractTextDemo {

    public static void main(String[] args) {
        // ---- 1️⃣  Initialize the OCR engine ---------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---- 2️⃣  Configure the engine to recognize Ukrainian text -----------
        // This is crucial if your image contains non‑Latin characters.
        ocrEngine.getEngineOptions().setLanguage(OcrLanguage.UKRAINIAN);

        // ---- 3️⃣  Load the image that contains Ukrainian characters ----------
        // Replace the path with the location of your own picture.
        String imagePath = "YOUR_DIRECTORY/ukrainian_sign.jpg";
        try {
            ocrEngine.getImage().loadFromFile(imagePath);
        } catch (Exception e) {
            System.err.println("Failed to load image: " + e.getMessage());
            return;
        }

        // ---- 4️⃣  Perform OCR recognition and obtain the extracted text -------
        String recognizedText;
        try {
            recognizedText = ocrEngine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Recognition error: " + e.getMessage());
            return;
        }

        // ---- 5️⃣  Output the recognized text to the console -------------------
        System.out.println("=== OCR Result ===");
        System.out.println(recognizedText);
    }
}
```

### Why This Structure Works

* **Separate numbered blocks** akışı kolay takip edilebilir kılar, özellikle **load image for OCR** ya da **recognize text from photo** nerede yapılacağını ararken.  
* Görüntü yükleme ve tanıma etrafındaki `try/catch`, dosya yolu yanlış olduğunda ya da OCR motoru dil verisini bulamadığında programın sorunsuz kapanmasını sağlar.  
* Dilin erken ayarlanması (adım 2) İngilizce dışı betikler için doğruluğu büyük ölçüde artırır. Daha sonra başka diller için **java image to text** ihtiyacınız olursa sadece `OcrLanguage.UKRAINIAN` yerine `OcrLanguage.ENGLISH`, `FRENCH` vb. değiştirin.

---

## Step 3: Build and Run the Program

Proje kökünden şu komutu çalıştırın:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.example.ocr.ExtractTextDemo"
```

Ya da Gradle kullanıyorsanız:

```bash
./gradlew run --args="com.example.ocr.ExtractTextDemo"
```

`ukrainian_sign.jpg` dosyası *«Ласкаво просимо»* (Ukraynaca “Hoş geldiniz”) metnini içeriyorsa, aşağıdakine benzer bir çıktı görmelisiniz:

```
=== OCR Result ===
Ласкаво просимо
```

Bu çıktı, **extract text from image** ve **get text from OCR** işlemlerini tek bir çalıştırmada başarıyla yaptığınızı doğrular.

---

## Step 4: Tweak the Workflow – From **Java Image to Text** in Real Projects

Demo minimal olsa da gerçek dünyada genellikle biraz daha fazlasına ihtiyaç duyulur:

| Senaryo | Ne Ayarlanmalı | Sebep |
|----------|----------------|--------|
| **Batch processing** | `List<Path>` üzerinde döngü kurup her sonucu bir veritabanına kaydedin. | Yüzlerce fotoğrafınız olduğunda manuel işi azaltır. |
| **Different image formats** | `ImageIO.read(new File(path))` ile ön‑işleme yapın, ardından `BufferedImage`ı `ocrEngine.getImage().loadFromBufferedImage(bufImg)` ile motorun içine gönderin. | PNG, BMP veya dönüşüm sonrası PDF gibi formatları destekler. |
| **Performance tuning** | `ocrEngine.getEngineOptions().setSpeed(OcrEngine.Speed.FAST)` çağrısı, biraz daha düşük doğruluk kabul edebiliyorsanız kullanın. | Düşük‑performans donanımında tanıma hızını artırır. |
| **Post‑processing** | Boşlukları kırpın, yaygın OCR hatalarını (`0` → `O`, `1` → `I`) değiştirin. | Sonraki veri kalitesini iyileştirir. |

Bu varyasyonlar, **recognize text from photo** temel fikrini korurken üretim ortamları için esneklik sağlar.

---

## Common Pitfalls & Pro Tips

1. **Yanlış dil ayarı** – Adım 2’yi atlayınca motor varsayılan olarak İngilizceyi seçer ve Kiril karakterleri anlamsız hâle gelir. Dil kodunu her zaman kontrol edin.  
2. **Görüntü kalitesi önemlidir** – Düşük çözünürlük ya da bulanık fotoğraflar doğruluğu düşürür. Gerekirse kontrast artırma ya da ikilileştirme ile ön‑işleme yapın.  
3. **Dosya yolu tuhaflıkları** – Windows’da ters eğik çizgiler kaçırılmalı (`C:\\images\\file.jpg`). `java.nio.file`’ten `Path.of(...)` kullanmak bu sorunu ortadan kaldırır.  
4. **Bellek sızıntıları** – `OcrEngine` yerel kaynak tutar. Özellikle uzun‑çalışan servislerde işiniz bittiğinde `ocrEngine.dispose()` çağırın.  
5. **Thread safety** – Motor varsayılan olarak çok iş parçacıklı değildir. Her iş parçacığı için ayrı bir örnek oluşturun ya da erişimi senkronize edin.

---

## Full Working Example (All‑In‑One)

Aşağıda, herhangi bir IDE’ye kopyalayıp yapıştırabileceğiniz tek dosya var. `dispose()` çağrısı ve kodu biraz daha temiz hâle getiren küçük bir yardımcı metod içeriyor.

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;
import java.nio.file.Path;

/**
 * Complete, runnable demo that extracts text from an image using Java OCR.
 */
public class FullDemo {

    public static void main(String[] args) {
        // Path to the image – change this to your own file.
        Path imgPath = Path.of("YOUR_DIRECTORY/ukrainian_sign.jpg");

        // Run the OCR workflow and capture the output.
        String result = extractTextFromImage(imgPath, OcrLanguage.UKRAINIAN);
        if (result != null) {
            System.out.println("=== OCR Result ===");
            System.out.println(result);
        }
    }

    /**
     * Core method that encapsulates the 5‑step OCR process.
     *
     * @param imagePath Path to the image file.
     * @param language  Desired OCR language.
     * @return Recognized text, or {@code null} if something went wrong.
     */
    private static String extractTextFromImage(Path imagePath, OcrLanguage language) {
        OcrEngine engine = new OcrEngine();
        try {
            // 1️⃣ Set language
            engine.getEngineOptions().setLanguage(language);

            // 2️⃣ Load image
            engine.getImage().loadFromFile(imagePath.toString());

            // 3️⃣ Recognize and return text
            return engine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Error during OCR: " + e.getMessage());
            return null;
        } finally {
            // 4️⃣ Release native resources
            engine.dispose();
        }
    }
}
```

Bu programı çalıştırdığınızda daha önce gösterilen aynı konsol çıktısını alacaksınız. `OcrLanguage.UKRAINIAN` yerine `OcrLanguage.ENGLISH` ya da desteklenen başka bir dili koyarak motorun nasıl uyum sağladığını görebilirsiniz.

---

## Conclusion

Java kullanarak **extract text from image** işlemi için ihtiyacınız olan her şeyi adım adım inceledik: OCR bağımlılığını eklemekten **load image for OCR** aşamasına kadar.

## Related Tutorials

- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}