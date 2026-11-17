---
category: general
date: 2026-11-17
description: Java’da bir görüntü üzerinde OCR nasıl yapılır ve basit bir kod örneğiyle
  resimlerden metin nasıl çıkarılır öğrenin. Görüntü okuma Java ipuçlarını içerir.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text image
- read image java
- convert image to text
- image to text java
language: tr
lastmod: 2026-11-17
og_description: Java’da bir görüntüde OCR nasıl yapılır ve metin hızlıca çıkarılır.
  Görüntüyü Java ile okuma ve görüntüyü metne dönüştürme konusunda, çalıştırmaya hazır
  bir örnekle bu kılavuzu izleyin.
og_image_alt: Screenshot showing Java code that performs OCR on an image
og_title: Java'da bir görüntüde OCR nasıl yapılır – adım adım rehber
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: Learn how to perform OCR on an image in Java and extract text from
    pictures using a simple code example. Includes read image Java tips.
  headline: How to perform OCR on an image in Java – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Java
- Image processing
- Text extraction
title: Java'da bir görüntüde OCR nasıl yapılır – adım adım rehber
url: /tr/java/ocr-basics/how-to-perform-ocr-on-an-image-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java’da bir görüntüde OCR nasıl yapılır – adım adım rehber

Bir resimde **OCR nasıl yapılır** ihtiyacınız varsa, bu öğretici Java’da tam, çalıştırılabilir bir çözüm gösterir. Bir görüntü dosyasını nasıl okuyacağınızı, bir OCR motorunu nasıl yapılandıracağınızı ve motorun tanıdığı metni nasıl çıkaracağınızı göreceksiniz.

Taranmış belgeler, fişler veya ekran görüntüleriyle çalışmak genellikle görsel içeriği aranabilir metne dönüştürmeyi gerektirir. Bu kılavuz, görüntüyü yüklemekten çıkarılan metni yazdırmaya kadar her adımı size anlatır ve ayrıca desteklenmeyen dosya formatları ve boş sonuçlar gibi yaygın tuzakları da kapsar.

## Önkoşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

* Java Development Kit (JDK) 8 veya daha yeni bir sürüm.
* OCR kütüphanesini çekmek için bir yapı aracı (Maven veya Gradle).
* İşlemek istediğiniz bir görüntü dosyası (JPEG, PNG, BMP).

Kod, **`com.asprise.ocr` paketindeki OCR kütüphanesini** kullanır çünkü yalnızca tek bir JAR gerektirir ve tüm büyük platformlarda çalışır. İçe aktarma satırlarını ve motor‑başlatma kodunu değiştirerek başka bir sağlayıcı (Tesseract, Google Vision vb.) ile değiştirebilirsiniz.

## Adım 1: OCR bağımlılığını ekleyin

Maven kullanıyorsanız, `pom.xml` dosyanıza aşağıdaki bağımlılığı ekleyin:

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.2.0</version>
</dependency>
```

Gradle için, `build.gradle` dosyanıza şu satırı ekleyin:

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.2.0'
```

Bu satırlar, **read image Java** kodunun derlenebilmesini ve OCR motorunun çalışma zamanında erişilebilir olmasını sağlar.

## Adım 2: Görüntüyü Java ile okuyun

Bir görüntü dosyasını okumak, herhangi bir **extract text image** iş akışının ilk somut adımıdır. Java’nın yerleşik `ImageIO` sınıfı çoğu yaygın formatı destekler.

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Loads an image from the supplied path.
 *
 * @param path absolute or relative path to the image file
 * @return a BufferedImage instance, or null if the file cannot be read
 */
private static BufferedImage loadImage(String path) {
    try {
        return ImageIO.read(new File(path));
    } catch (Exception e) {
        System.err.println("Failed to read image: " + e.getMessage());
        return null;
    }
}
```

**Neden önemli:** `ImageIO.read` desteklenmeyen formatlar veya bozuk dosyalar için `null` döner. Yukarıdaki yöntem sorunu kaydeder ve `null` döner, böylece bir sonraki adım sorunsuz bir şekilde yanıt verebilir.

## Adım 3: OCR motorunu oluşturun ve yapılandırın

OCR motorunun hangi dili tanıyacağını bilmesi gerekir. Dil ayarı, özellikle İngilizce dışı belgelerde doğruluğu büyük ölçüde artırır.

```java
import com.asprise.ocr.Ocr;

/**
 * Instantiates an OCR engine configured for English.
 *
 * @return a ready‑to‑use Ocr object
 */
private static Ocr createEngine() {
    Ocr ocrEngine = new Ocr();
    // The first argument is the language; "eng" is the ISO code for English.
    ocrEngine.startEngine("eng", Ocr.SPEED_FAST);
    return ocrEngine;
}
```

**Neden önemli:** Motoru başlatmak nispeten ağır bir işlemdir, bu yüzden uygulamanız toplu işlem yapıyorsa motoru bir kez oluşturup birden çok görüntüde yeniden kullanmalısınız.

## Adım 4: OCR’u çalıştırın ve görüntüyü metne dönüştürün

Görüntü yüklendi ve motor hazır olduğuna göre tanıma adımını çalıştırabilirsiniz. Bu, **how to perform OCR**’un çekirdeğidir.

```java
/**
 * Runs OCR on a BufferedImage and returns the recognized text.
 *
 * @param ocrEngine an initialized Ocr instance
 * @param image     the image to process
 * @return the extracted text, or an empty string if nothing is recognized
 */
private static String extractText(Ocr ocrEngine, BufferedImage image) {
    if (image == null) {
        return "";
    }
    // The third parameter (0) tells the engine to return plain text.
    String result = ocrEngine.recognize(image, 0);
    return result != null ? result.trim() : "";
}
```

**Köşe‑durum yönetimi:** Görüntü `null` ise, yöntem bir `NullPointerException` fırlatmak yerine boş bir dize döner. Bu, kullanıcı‑tarafından sağlanan dosyalarla çalışırken çevre kodun daha dayanıklı olmasını sağlar.

## Adım 5: Çıkarılan metni gösterin

Son olarak, sonucu konsola yazdırın veya başka bir bileşene (ör. bir veritabanı veya UI widget’ı) yönlendirin.

```java
/**
 * Demonstrates the full OCR workflow.
 *
 * @param args command‑line arguments (first argument = path to image)
 */
public static void main(String[] args) {
    if (args.length == 0) {
        System.err.println("Usage: java OcrDemo <path-to-image>");
        return;
    }

    String imagePath = args[0];
    BufferedImage image = loadImage(imagePath);
    Ocr ocrEngine = createEngine();

    String text = extractText(ocrEngine, image);
    System.out.println("=== Recognized Text ===");
    System.out.println(text.isEmpty() ? "(no text detected)" : text);

    // Clean up the OCR engine to free native resources.
    ocrEngine.stopEngine();
}
```

Programı `java OcrDemo sample.jpg` ile çalıştırdığınızda, konsol tanınan karakterleri gösterir. Bu, **convert image to text** döngüsünü tamamlar.

### Beklenen çıktı

```
=== Recognized Text ===
The quick brown fox jumps over the lazy dog.
```

Görüntü okunabilir karakter içermiyorsa, program `(no text detected)` yazar.

## Yaygın varyasyonlar ve nasıl uyarlanır

| Varyasyon | Ne değişir | Ne zaman kullanılır |
|-----------|------------|---------------------|
| **Farklı dil** | `"eng"` yerine İspanyolca için `"spa"`, Fransızca için `"fra"` vb. değiştirin | İngilizce dışındaki dillerde yazılmış belgeler |
| **Toplu işleme** | Dosya yolu listesi üzerinde döngü kurun, aynı `Ocr` örneğini yeniden kullanın | Büyük miktarda taranmış sayfa |
| **Daha yüksek doğruluk** | Sayısal taramalar için `Ocr.SPEED_SLOW` kullanın veya `ocrEngine.setConfig("tessedit_char_whitelist", "0123456789")` etkinleştirin | OCR kalitesinin kritik olduğu durumlar (ör. fatura numaraları) |
| **Tesseract alternatifi** | İçe aktarmayı `net.sourceforge.tess4j.Tesseract` olarak değiştirin ve başlatma kodunu uyarlayın | Zaten Tesseract’a bağımlı projeler |

## Profesyonel ipuçları

* **Büyük görüntüleri yeniden boyutlandırın** motorun önüne göndermeden önce; OCR hızı piksel sayısıyla orantılıdır.
* **Görüntüyü ön‑işleyin** (gri ton, kontrast artırma) OpenCV gibi kütüphanelerle, kaynak gürültülü ise.
* **OCR motorunu önbelleğe alın** kısa sürede çok kez çağırıyorsanız—motoru başlatıp durdurmak ek yük getirir.
* **Sonucu doğrulayın** belirli bir format bekliyorsanız (tarih, telefon numarası gibi) düzenli ifadelerle.

## Sonuç

Artık Java’da bir görüntüde **OCR nasıl yapılır** konusunda, dosyayı okumaktan çıkarılan metni göstermeye kadar her şeyi biliyorsunuz. Öğreticide **read image Java**, **extract text image**, **convert image to text** ve **image to text java** teknikleri ele alındı ve gerçek dünya senaryoları için pratik ipuçları verildi.  

Bundan sonra şunları yapabilirsiniz:

* Yüklemeleri alan bir web hizmetine OCR adımını entegre edin.
* Çıktıyı tam‑metin arama için bir arama indeksine bağlayın, taranmış belgeler üzerinde arama yapın.
* Çok‑dilli destek veya özel karakter setleri gibi gelişmiş OCR seçeneklerini keşfedin.

İyi kodlamalar, ve resimleri aranabilir metne dönüştürmenin tadını çıkarın!


## Sonra Ne Öğrenmelisiniz?


Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakın konuları kapsayan kaynaklardır. Her biri, ek API özelliklerini ustalaşmanız ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [How to Use OCR in Java – Extract Text from Image with Spell Correction](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/)
- [Convert Image to Text in Java Using Aspose OCR – Full Guide](/ocr/english/java/ocr-operations/convert-image-to-text-in-java-using-aspose-ocr-full-guide/)
- [How to Enable GPU for OCR in Java – Extract Text from Image](/ocr/english/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}