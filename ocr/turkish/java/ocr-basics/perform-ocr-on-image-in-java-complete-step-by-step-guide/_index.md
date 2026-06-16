---
category: general
date: 2026-06-16
description: Java’da görüntü dosyalarında OCR nasıl yapılır öğrenin. Bu öğreticide
  PNG’den metin tanıma, görüntüden metin çıkarma, görüntüyü metne dönüştürme ve OCR
  için görüntü yükleme konuları ele alınmaktadır.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- extract text from image
- convert image to text
- load image for OCR
language: tr
og_description: Java kullanarak görüntüde OCR gerçekleştirin. Bu rehber, PNG'den metin
  tanıma, görüntüden metin çıkarma ve çalıştırmaya hazır bir örnekle görüntüyü metne
  dönüştürme yöntemlerini gösterir.
og_title: Java'da Görüntü Üzerinde OCR Yapma – Tam Programlama Öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  headline: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  name: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'If `hello.png` contains the phrase “Hello, OCR world!”, the console will
      display something like:'
  - name: 5.1 Dealing with Low‑Resolution Images
    text: 'If the source PNG is blurry, OCR accuracy drops. A quick fix is to upscale
      the image before feeding it to the engine:'
  - name: 5.2 Multi‑Language Documents
    text: 'If you anticipate French or German text, simply add the language codes
      to `setLanguage`:'
  - name: 5.3 Skipping Empty Pages
    text: 'Sometimes a scanned PDF page renders as a blank PNG. Detecting an empty
      image saves processing time:'
  type: HowTo
tags:
- Java
- OCR
- Image Processing
title: Java'da Görüntüde OCR Yapmak – Tam Adım Adım Kılavuz
url: /tr/java/ocr-basics/perform-ocr-on-image-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java’da Görüntü Üzerinde OCR Yapma – Tam Adım‑Adım Kılavuz

Hiç **perform OCR on image** dosyalarıyla çalışmanız gerekti ama hangi Java kütüphanesini seçeceğinizden emin değildiniz mi? Yalnız değilsiniz. İster bir fiş tarayıcısı, bir belge arşivleyici geliştirin, ister sadece resimleri aranabilir metne dönüştürmekle ilgili meraklı olun, Java ile **perform OCR on image** öğrenmek kullanışlı bir beceridir.

Bu öğreticide **perform OCR on image** dosyalarıyla ilgili her şeyi adım adım inceleyeceğiz: görüntüyü yükleme, motoru yapılandırma, metni tanıma ve sonunda sonucu yazdırma. Sonunda **recognize text from PNG** dosyalarını, **extract text from image** kaynaklarını ve **convert image to text** işlemlerini sadece birkaç satır kodla yapabilecek duruma geleceksiniz.

## Önkoşullar

- Java 17 veya daha yeni (kod, herhangi bir güncel JDK ile derlenir)
- Maven kurulu (veya tercih ettiğiniz yapı aracı)
- Java sözdizimi hakkında temel bilgi
- Test etmek istediğiniz bir PNG dosyası (biz ona `hello.png` diyeceğiz)

> **Pro tip:** Eğer elinizde bir PNG yoksa, herhangi bir metnin ekran görüntüsünü alıp `hello.png` olarak `resources` adlı bir klasöre kaydedin.

## Ne İnşa Edeceğiz

`OcrDemo` adlı küçük bir konsol uygulaması ki:

1. **Loads image for OCR** – diskteki bir PNG dosyasını okur.
2. **Performs OCR on image** – Tesseract motorunu Tess4J aracılığıyla kullanır.
3. **Extracts text from image** – tanınan içeriği bir `String` olarak döndürür.
4. Sonucu konsola yazdırır.

Hadi başlayalım.

## Adım 1: Projeyi Kurun ve Tess4J’yi Ekleyin

İlk olarak yeni bir Maven projesi oluşturun (isteğe bağlı olarak Gradle da kullanabilirsiniz). Popüler Tesseract OCR motorunu saran Tess4J bağımlılığını ekleyin.

```xml
<!-- pom.xml -->
<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>ocr-demo</artifactId>
  <version>1.0.0</version>
  <properties>
    <maven.compiler.source>17</maven.compiler.source>
    <maven.compiler.target>17</maven.compiler.target>
  </properties>

  <dependencies>
    <!-- Tess4J – Java wrapper for Tesseract OCR -->
    <dependency>
      <groupId>net.sourceforge.tess4j</groupId>
      <artifactId>tess4j</artifactId>
      <version>5.5.1</version>
    </dependency>
  </dependencies>
</project>
```

> **Why Tess4J?** Aktif olarak bakımda, platformlar arası çalışıyor ve **perform OCR on image** görevleri için temiz bir Java API’si sunuyor.

## Adım 2: Görüntü‑Yükleme Mantığını Hazırlayın

Şimdi **load image for OCR** yapan bir yardımcı metod yazacağız. Metod, Java’nın `ImageIO` sınıfını kullanarak bir PNG’yi `BufferedImage` içine okur.

```java
package com.example.ocr;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Utility class responsible for loading images from the file system.
 */
public final class ImageLoader {

    private ImageLoader() { /* utility class */ }

    /**
     * Loads a PNG (or any supported format) from the given path.
     *
     * @param path absolute or relative path to the image file
     * @return BufferedImage instance ready for OCR processing
     * @throws IOException if the file cannot be read
     */
    public static BufferedImage load(String path) throws IOException {
        File imgFile = new File(path);
        if (!imgFile.exists()) {
            throw new IOException("Image file not found: " + path);
        }
        return ImageIO.read(imgFile);
    }
}
```

Metodun adı, **load image for OCR** amacını açıkça yansıtıyor, bu da kodun kendini belgeleyen bir yapıya sahip olmasını sağlıyor.

## Adım 3: OCR Motorunu **Perform OCR on Image** İçin Yapılandırın

Görüntü elimizde olduğunda bir `Tesseract` örneği oluşturur, otomatik dil algılamayı etkinleştirir ve `doOCR` metodunu çağırırız. Bu, **perform OCR on image** verileriyle nasıl çalıştığımızın özüdür.

```java
package com.example.ocr;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

/**
 * Wrapper around Tess4J that abstracts the OCR workflow.
 */
public final class OcrEngine {

    private final ITesseract tesseract;

    public OcrEngine() {
        tesseract = new Tesseract();

        // Use the bundled tessdata folder (you can also point to a custom one)
        tesseract.setDatapath("tessdata");

        // Enable automatic language detection – improves accuracy across multilingual images
        tesseract.setLanguage("eng"); // fallback language
        tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
        tesseract.setPageSegMode(ITesseract.PSM_AUTO);
    }

    /**
     * Performs OCR on the supplied BufferedImage and returns the recognized text.
     *
     * @param image image to be processed
     * @return the text extracted from the image
     * @throws TesseractException if OCR fails
     */
    public String recognize(BufferedImage image) throws TesseractException {
        return tesseract.doOCR(image);
    }
}
```

> **Why enable auto‑detect?** Motorun görüntü için en uygun dil modelini seçmesini sağlar; bu, İngilizce ve diğer dillerin karıştığı kaynaklardan **convert image to text** yaparken özellikle faydalıdır.

## Adım 4: Hepsini Birleştirin – Ana Uygulama

İşte **recognize text from PNG**, **extract text from image** yapan ve sonunda sonucu ekrana yazdıran giriş noktası. Bu, tam ve çalıştırılabilir örnektir.

```java
package com.example.ocr;

import net.sourceforge.tess4j.TesseractException;
import java.awt.image.BufferedImage;
import java.io.IOException;

/**
 * Demo application that shows how to perform OCR on image files.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Path to the PNG you want to process
        String imagePath = "resources/hello.png";

        try {
            // Step 1: Load image for OCR
            BufferedImage image = ImageLoader.load(imagePath);

            // Step 2: Create OCR engine instance
            OcrEngine engine = new OcrEngine();

            // Step 3: Perform OCR on image and retrieve the text
            String recognizedText = engine.recognize(image);

            // Step 4: Output the recognized text to the console
            System.out.println("=== Recognized Text ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR processing error: " + e.getMessage());
        }
    }
}
```

### Beklenen Çıktı

`hello.png` içinde “Hello, OCR world!” ifadesi varsa, konsol şu şekilde bir çıktı verir:

```
=== Recognized Text ===
Hello, OCR world!
```

Tam çıktı, görüntü kalitesine bağlı olarak biraz değişebilir, ancak PNG’ye koyduğunuz metni görmelisiniz.

## Adım 5: Yaygın Kenar Durumlarını Ele Alma

### 5.1 Düşük‑Çözünürlüklü Görüntülerle Başa Çıkma

Kaynak PNG bulanıksa, OCR doğruluğu düşer. Hızlı bir çözüm, motoru beslemeden önce görüntüyü büyütmektir:

```java
import java.awt.Graphics2D;
import java.awt.RenderingHints;

public static BufferedImage upscale(BufferedImage original, int factor) {
    int width = original.getWidth() * factor;
    int height = original.getHeight() * factor;
    BufferedImage scaled = new BufferedImage(width, height, original.getType());
    Graphics2D g = scaled.createGraphics();
    g.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                       RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g.drawImage(original, 0, 0, width, height, null);
    g.dispose();
    return scaled;
}
```

`engine.recognize(image)` çağrısından önce `upscale(image, 2)` metodunu kullanarak sonuçları iyileştirin.

### 5.2 Çok‑Dilli Belgeler

Fransızca veya Almanca metin bekliyorsanız, `setLanguage` metoduna dil kodlarını eklemeniz yeterlidir:

```java
tesseract.setLanguage("eng+fra+deu");
```

Motor, birleşik dil modellerini kullanarak **extract text from image** işlemine çalışacaktır.

### 5.3 Boş Sayfaları Atlamak

Bazen taranmış bir PDF sayfası boş bir PNG olarak ortaya çıkar. Boş bir görüntüyü tespit etmek işlem süresinden tasarruf sağlar:

```java
if (image.getWidth() == 0 || image.getHeight() == 0) {
    System.out.println("Empty image – skipping OCR.");
    return;
}
```

## Adım 6: Uygulamayı Paketleme ve Çalıştırma

1. **Compile:** `mvn clean compile`
2. **Run:** `mvn exec:java -Dexec.mainClass="com.example.ocr.OcrDemo"`

` t`essdata` klasörünün (dil dosyalarını içeren) derlenmiş JAR’ın yanına yerleştirildiğinden emin olun veya mutlak yolunu `OcrEngine` içinde belirtin.

## Sonuç

Artık Java kullanarak **perform OCR on image** dosyaları için sağlam, üretim‑hazır bir deseniniz var. **loading image for OCR**’dan **recognize text from PNG**’e kadar, **extract text from image**, **convert image to text** işlemlerini ve düşük‑çözünürlüklü taramalar ya da çok‑dilli içerik gibi zorlu senaryoları nasıl yöneteceğimizi kapsadık.

Sonraki adımda şunları keşfedebilirsiniz:

- **Batch processing** – PNG klasörünü döngüye alıp her sonucu bir `.txt` dosyasına yazın.
- **PDF generation** – Çıkarılan metni tekrar aranabilir PDF’lere gömün.
- **Cloud OCR services** – Yerel Tesseract performansını Google Vision veya Azure Cognitive Services gibi API’lerle karşılaştırın.

Denemeler yapmaktan, parametreleri ayarlamaktan ve bulgularınızı paylaşmaktan çekinmeyin. Mutlu kodlamalar, ve görüntüleriniz her zaman temiz, aranabilir metne dönüşsün!

![OCR iş akışını gösteren diyagram – perform OCR on image](https://example.com/ocr-workflow.png "perform OCR on image örneği")


## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve birbirine yakın konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanıza ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım adım açıklamalar içerir.

- [Aspose OCR ile Görüntü Metni Tanıma – Tam Java OCR Kılavuzu](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Java’da Aspose.OCR BufferedImage Kullanarak Görüntüyü Metne Dönüştürme](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Aspose.OCR Detect Areas Modu ile Java’da Görüntüden Metin Çıkarma](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}