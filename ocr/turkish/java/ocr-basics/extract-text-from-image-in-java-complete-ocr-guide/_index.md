---
category: general
date: 2026-07-21
description: Java OCR kullanarak görüntüden metin çıkarın. PNG'yi metne dönüştürmeyi,
  PNG'den metin okumayı, OCR için görüntüyü yüklemeyi ve sadece birkaç adımda görüntüde
  OCR yapmayı öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert png to text
- read text from png
- load image for ocr
- perform ocr on image
language: tr
lastmod: 2026-07-21
og_description: Java ile görüntüden metin çıkarın. Bu rehber, PNG'yi metne dönüştürmeyi,
  PNG'den metin okumayı, OCR için görüntüyü yüklemeyi ve görüntü üzerinde verimli
  bir şekilde OCR yapmayı gösterir.
og_image_alt: Screenshot of Java code extracting text from an image using OCR
og_title: Java'da Görüntüden Metin Çıkarma – Adım Adım OCR Öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  headline: Extract Text from Image in Java – Complete OCR Guide
  type: TechArticle
- description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  name: Extract Text from Image in Java – Complete OCR Guide
  steps:
  - name: Low‑Quality Images
    text: 'If the PNG is blurry or has low contrast, OCR accuracy drops. A quick fix
      is to pre‑process the image:'
  - name: Multi‑Language Support
    text: Tess4J can handle many languages. Just download the appropriate `.traineddata`
      file and point `tesseract.setLanguage("spa")` for Spanish, for example.
  - name: Large PDFs or Multi‑Page Images
    text: If you need to **extract text from image** files inside a PDF, split each
      page into PNGs first (using PDFBox) and then feed each PNG to the same OCR routine.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Java'da Görüntüden Metin Çıkarma – Tam OCR Rehberi
url: /tr/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java’da Görüntüden Metin Çıkarma – Tam OCR Rehberi

Görüntüden **metin çıkarmak** gerektiğinde ama hangi Java kütüphanesini seçeceğinizi bilemediğiniz oldu mu? Yalnız değilsiniz. Makbuzları dijitalleştiriyor, PDF'leri tarıyor ya da aranabilir bir arşiv oluşturuyorsanız, bir PNG'den metin çekmek birçok geliştirici için günlük bir sorun.

Bu öğreticide, **PNG'yi metne dönüştürmenizi**, **PNG'den metin okumanızı**, **OCR için görüntüyü yüklemenizi** ve **görüntü üzerinde OCR gerçekleştirmenizi** sağlayan uygulamalı bir çözümü adım adım inceleyeceğiz—temiz birkaç Java kod satırıyla. Sonunda, herhangi bir projeye ekleyebileceğiniz çalıştırılabilir bir programınız olacak.

## Oluşturacağınız Şey

Küçük bir Java konsol uygulaması oluşturacağız ki:

1. Diskten bir PNG dosyası yükler.  
2. Görüntüyü bir OCR motoruna gönderir (Tess4J, Tesseract için bir Java sarmalayıcı).  
3. Tanımlanan metni konsola yazdırır.

Harici hizmetler yok, sihir yok—sadece saf Java ve açık kaynaklı bir OCR motoru.

## Önkoşullar

- **Java 17** veya üzeri (kod eski sürümlerle de derlenir, ancak Java 17 en yeni dil özelliklerini sunar).  
- Bağımlılık yönetimi için **Maven** veya **Gradle**.  
- `sample.png` adlı örnek bir PNG, referans verebileceğiniz bir klasöre yerleştirilmiş (ör. `src/main/resources`).  
- Java’nın `main` metodu ve istisna yönetimi hakkında temel bilgi.

Eğer bunlardan biri size yabancı geliyorsa endişelenmeyin—her adım hızlı bir özet içerir.

## Adım 1: Projeyi Kurun ve OCR Kütüphanesini Ekleyin

İlk olarak, yeni bir Maven projesi oluşturun (ya da tercih ederseniz Gradle). Tess4J bağımlılığını ekleyin; bu, sizin için Tesseract ikili dosyalarını getirir.

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
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

> **Pro tip:** Gradle kullanıyorsanız, eşdeğer satır `implementation 'net.sourceforge.tess4j:tess4j:5.5.1'` şeklindedir.

Bu kütüphaneyi eklemek, **görüntü üzerinde OCR gerçekleştirme** işlemlerinin ağır işini yapan `Tesseract` sınıfını sağlar.

## Adım 2: OCR için Görüntüyü Yükleyin

Şimdi **OCR için görüntüyü yüklememiz** gerekiyor. Tess4J, `java.awt.image.BufferedImage` ile çalışır, bu yüzden PNG'yi `ImageIO` kullanarak okuyacağız.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

public class OcrDemo {

    /**
     * Loads a PNG file from the given path and returns a BufferedImage.
     *
     * @param path absolute or relative path to the PNG file
     * @return BufferedImage containing the image data
     * @throws IOException if the file cannot be read
     */
    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image to be recognized
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }
```

Yukarıdaki yöntem, **OCR için görüntüyü yükleme** mantığını temiz bir şekilde izole eder ve kodun geri kalanının test edilmesini kolaylaştırır. Yoruma dikkat edin – orijinal kodu yansıtırken açıklık için genişletilmiştir.

## Adım 3: Görüntü Üzerinde OCR Gerçekleştirin

Görüntü bellekte olduğunda artık **görüntü üzerinde OCR gerçekleştirebiliriz**. `Tesseract` örneği bizim motorumuz; Tess4J ile gelen varsayılan İngilizce dil verisini kullanacak şekilde yapılandıracağız.

```java
    /**
     * Runs OCR on the supplied BufferedImage and returns the extracted text.
     *
     * @param image the image to analyze
     * @return plain text recognized from the image
     * @throws TesseractException if the OCR process fails
     */
    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();

        // Optional: set the datapath if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");

        // Step 4: Run OCR and capture the recognized text
        return tesseract.doOCR(image);
    }
```

Burada, `Tesseract` nesnesinin oluşturulmasının maliyetinin düşük olması ve kodun kompakt kalmasını istediğimiz için orijinal “Adım 1” ve “Adım 4” tek bir yöntemde birleştirildi. Yorum hâlâ izlenebilirlik için orijinal adımlara referans veriyor.

## Adım 4: Hepsini Birleştirin – Main Metodu

Son olarak, her şeyi `main` içinde birleştiriyoruz. İşte **PNG'den metin okuyacağınız** ve sonucun konsola yazdırıldığını göreceğiniz yer.

```java
    public static void main(String[] args) {
        // Adjust the path to point at your PNG file
        String imagePath = "src/main/resources/sample.png";

        try {
            // Load the PNG image
            BufferedImage image = loadImage(imagePath);

            // Extract text from the image
            String recognizedText = extractText(image);

            // Step 5: Display the extracted text
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR error: " + e.getMessage());
        }
    }
}
```

`mvn compile exec:java -Dexec.mainClass="com.example.ocrdemo.OcrDemo"` (veya Gradle eşdeğeri) komutunu çalıştırdığınızda aşağıdakine benzer bir çıktı görmelisiniz:

```
=== OCR Result ===
Hello, world!
This is a sample PNG file.
```

Bu çıktı, tek bir düzenli programda **görüntüden metin çıkardığınızı**, **PNG'yi metne dönüştürdüğünüzü** ve **PNG'den metin okuduğunuzu** başarıyla kanıtlar.

## Yaygın Kenar Durumlarını Ele Alma

### Düşük Kaliteli Görüntüler

PNG bulanık ya da düşük kontrastlı ise OCR doğruluğu düşer. Hızlı bir çözüm, görüntüyü ön işleme tabi tutmaktır:

```java
// Example: Convert to grayscale and apply a binary threshold
BufferedImage gray = new BufferedImage(
        image.getWidth(), image.getHeight(),
        BufferedImage.TYPE_BYTE_GRAY);
Graphics2D g = gray.createGraphics();
g.drawImage(image, 0, 0, null);
g.dispose();

// Simple binary threshold
for (int y = 0; y < gray.getHeight(); y++) {
    for (int x = 0; x < gray.getWidth(); x++) {
        int rgb = gray.getRGB(x, y) & 0xFF;
        int binary = rgb < 128 ? 0x000000 : 0xFFFFFF;
        gray.setRGB(x, y, binary);
    }
}
String text = extractText(gray);
```

### Çok Dilli Destek

Tess4J birçok dili destekleyebilir. Örneğin İspanyolca için uygun `.traineddata` dosyasını indirip `tesseract.setLanguage("spa")` şeklinde ayarlamanız yeterlidir.

### Büyük PDF'ler veya Çok Sayfalı Görüntüler

Eğer bir PDF içindeki **görüntü dosyalarından metin çıkarmanız** gerekiyorsa, önce her sayfayı PNG'lere bölün (PDFBox kullanarak) ve ardından her PNG'yi aynı OCR rutinine besleyin.

## Tam Çalışan Örnek (Tüm Kod Tek Bir Yerde)

Aşağıda eksiksiz, çalıştırmaya hazır Java sınıfı yer alıyor. `src/main/java/com/example/ocrdemo/OcrDemo.java` içine kopyalayıp yapıştırın, hazırsınız.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Demonstrates how to extract text from image (PNG) using Java and Tess4J.
 */
public class OcrDemo {

    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image for OCR
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }

    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();
        // Uncomment and set if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");
        // Step 4: Perform OCR on image
        return tesseract.doOCR(image);
    }

    public static void main(String[] args) {
        // Path to the PNG you want to convert to text
        String imagePath = "src/main/resources/sample.png";

        try {
            BufferedImage image = loadImage(imagePath);
            String recognizedText = extractText(image);
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("Error during OCR: " + e.getMessage());
        }
    }
}
```

Sınıfı çalıştırmak OCR sonucunu yazdırır ve **görüntü üzerinde OCR gerçekleştirdiğinizi** ve PNG'nizi düzenlenebilir metne dönüştürdüğünüzü doğrular.

## Özet ve Sonraki Adımlar

Hafif bir Java ortamı kullanarak **görüntüden metin çıkarmaya** başladık. Artık **OCR için görüntüyü yükleme**, **görüntü üzerinde OCR gerçekleştirme** ve **PNG'den metin okuma** konularını biliyorsunuz—herhangi bir belge‑dijitalleştirme hattı için temel yapı taşları.

Daha ileri gitmek mi istiyorsunuz? Şu fikirleri deneyin:

- **Toplu işleme:** PNG'lerin bulunduğu bir diziyi döngüye alıp her sonucu bir `.txt` dosyasına yazın.  
- **Veritabanı entegrasyonu:** Çıkarılan dizeleri, aranabilir arşivler için meta verilerle birlikte depolayın.  
- **NLP ile birleştirme:** OCR çıktısını hızlı içgörüler için bir duygu‑analizi modeline besleyin.  

Bu uzantıların her biri, ele aldığımız aynı temel kavramlar üzerine inşa edildiği için denemeye hazırsınız.

---

*Kodlamanın keyfini çıkarın! Eğer bir sorunla karşılaşırsanız*

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren eksiksiz çalışan kod örnekleri sunar.

- [Aspose.OCR Detect Areas Mode ile Java’da Görüntüden Metin Çıkarma](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [image to text java: Aspose.OCR ile Görüntüyü Metne Dönüştürme](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Aspose.OCR Kullanarak Dil ile Görüntü Metnini OCR Yapma](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}