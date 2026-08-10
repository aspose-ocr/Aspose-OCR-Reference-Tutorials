---
category: general
date: 2026-05-06
description: Aspose OCR'yi kullanarak görüntüden metin tanıma, otomatik dil algılamayı
  etkinleştirme ve Java'da OCR hızını artırma.
draft: false
keywords:
- how to use aspose
- recognize text from image
- improve ocr speed
- load image for ocr
- enable automatic language detection
language: tr
og_description: Aspose OCR'yi kullanarak görüntüden metni hızlı bir şekilde tanıma,
  otomatik dil algılamayı etkinleştirme ve Java'da OCR hızını artırma.
og_title: Karışık Dil Görüntüleri için Aspose OCR Nasıl Kullanılır
tags:
- Aspose
- OCR
- Java
- Image Processing
title: Aspose OCR'yi Karışık Dil Görüntülerinde Nasıl Kullanılır
url: /tr/java/advanced-ocr-techniques/how-to-use-aspose-ocr-for-mixed-language-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR'yi Karışık Dil Görsellerinde Nasıl Kullanılır

Bir resimde aynı anda birden fazla dil bulunduğunda **how to use Aspose**'yi merak ettiniz mi? Tek başınıza değilsiniz—geliştiriciler, bir görsel İngilizce, Rusça, Hintçe veya başka bir betik karıştırdığında sık sık bir engelle karşılaşıyor. İyi haber, Aspose OCR bunu sorunsuz bir şekilde yönetiyor ve dil kümesini daraltarak **recognize text from image** işlemini daha hızlı yapabilirsiniz.

Bu öğreticide, **loads image for OCR** yapan, **automatic language detection**'ı açan ve **improve OCR speed** için basit bir ipucu gösteren, tam ve çalıştırılabilir bir Java örneği üzerinden adım adım ilerleyeceğiz. Sonunda, çıkarılan metni konsola yazdıran bağımsız bir programınız olacak ve her ayarın neden önemli olduğunu anlayacaksınız.

> **Prerequisites** – Java 17+ yüklü, bağımlılık yönetimi için Maven veya Gradle ve bir Aspose OCR lisansı (ücretsiz deneme değerlendirme için çalışır). Başka bir kütüphane gerekmez.

---

## Step 1 – Add Aspose OCR to Your Project

Aspose'yi **use Aspose**'den önce, kütüphaneyi sınıf yolunuza eklemeniz gerekir. Maven ile şöyle görünür:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check for the latest version -->
</dependency>
```

Gradle tercih ediyorsanız:

```groovy
implementation 'com.aspose:aspose-ocr:23.12'
```

> **Pro tip:** En son kararlı sürümü kullanın; yeni sürümler genellikle **improve OCR speed**'i doğrudan etkileyen performans iyileştirmeleri içerir.

---

## Step 2 – Create the OCR Engine Instance  

Her Aspose OCR iş akışının kalbi `OcrEngine`'dir. Örneğini oluşturmak basittir, ancak motorun dahili önbellekler tuttuğunu belirtmek gerekir. Birçok görüntüde tek bir örneği yeniden kullanmak aslında **improve OCR speed** sağlar çünkü kütüphane tekrarlanan yerel başlatmayı önler.

```java
import com.aspose.ocr.*;

public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialise the OCR engine – one instance per application is ideal
        OcrEngine ocrEngine = new OcrEngine();
```

---

## Step 3 – **Load Image for OCR**  

Aspose birçok görüntü formatını (PNG, JPEG, TIFF, BMP) kabul eder. Burada İngilizce, Rusça ve Hintçe metin içeren bir PNG'yi yüklemeyi gösteriyoruz. `ImageStream.fromFile` yardımcı işlevi dosya‑G/Ç ayrıntılarını soyutlar ve görüntünün motor içine doğru şekilde akıtıldığından emin olur.

```java
        // Step 3: Load the picture that holds mixed languages
        // Replace the path with the actual location of your image file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/mixed-lang.png"));
```

> **What if the image is in memory?** Bunun yerine `ImageStream.fromByteArray(byte[])` kullanın—görüntüleri bayt akışı olarak alan web hizmetleri için mükemmeldir.

---

## Step 4 – Enable Automatic Language Detection  

Varsayılan olarak Aspose OCR tek bir dil varsayar, bu da çok dilli görsellerde bozuk çıktıya yol açabilir. Otomatik algılamayı açmak, motorun tanımadan önce her metin bloğunun betiğini tespit etmesini sağlar.

```java
        // Step 4: Turn on auto‑detect – this is the key to handling mixed‑language images
        ocrEngine.getSettings().setAutoDetectLanguage(true);
```

---

## Step 5 – **Improve OCR Speed** by Restricting the Language Pool  

Tam otomatik algılama, Aspose'un desteklediği tüm dilleri (70'ten fazla) tarar. Olası dilleri önceden biliyorsanız, motoru bir ipucu ile yönlendirebilirsiniz. Daha küçük bir dizi sağlamak arama alanını azaltır ve bu nedenle **improves OCR speed**.

> **Why does this help?** Motor, ihtiyacı olmayan dil modellerini atlar, CPU döngüleri ve bellek tasarrufu sağlar. Daha sonra daha fazla dil eklemek isterseniz, sadece diziyi güncelleyin—kod yeniden yazmaya gerek yok.

```java
        // Step 5 (optional but recommended): Limit detection to known languages
        // "en" = English, "ru" = Russian, "hi" = Hindi
        ocrEngine.getSettings().setPossibleLanguages(new String[] { "en", "ru", "hi" });
```

---

## Step 6 – Perform the Recognition and **Recognize Text from Image**

Şimdi asıl iş burada gerçekleşir. `recognize()` bir `OcrResult` nesnesi döndürür; bu nesne düz metni, güven skorlarını ve gerekirse daha sonra kullanabileceğiniz yerleşim bilgilerini içerir.

```java
        // Step 6: Run the OCR process
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 7: Output the recognized text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

### Expected Console Output

```
=== Extracted Text ===
Hello world!
Привет мир!
नमस्ते दुनिया!
```

Görsel ek gürültü veya eğik metin içeriyorsa, bu satırlar için daha düşük güven skorları görebilirsiniz. Bu durumda, Aspose'a göndermeden önce görüntüyü ön‑işleme (eğikliği düzeltme, ikilileştirme) yapmayı düşünün.

---

## Common Questions & Edge Cases

### What if the image is huge (e.g., >10 MP)?

Büyük görseller daha fazla bellek tüketir ve işleme süresini yavaşlatabilir. **improve OCR speed**'i hızlı bir şekilde artırmanın yolu, okunabilirliği koruyarak görüntüyü küçültmektir:

```java
// Example using java.awt for simple resizing (optional)
BufferedImage original = ImageIO.read(new File("large.png"));
int targetWidth = 2000; // adjust based on your needs
BufferedImage resized = new BufferedImage(targetWidth,
        (original.getHeight() * targetWidth) / original.getWidth(),
        BufferedImage.TYPE_INT_RGB);
Graphics2D g = resized.createGraphics();
g.drawImage(original, 0, 0, targetWidth, resized.getHeight(), null);
g.dispose();
ocrEngine.setImage(ImageStream.fromImage(resized));
```

### How do I handle right‑to‑left scripts like Arabic?

Sağ‑dan‑sol betikleri (ör. Arapça) nasıl ele alırım? Aspose OCR otomatik olarak betik yönünü dikkate alır, ancak son‑işleme için `RightToLeft` bayrağını ayarlamak isteyebilirsiniz:

```java
ocrEngine.getSettings().setRightToLeft(true);
```

### Can I extract text from PDFs instead of images?

Görseller yerine PDF'lerden metin çıkarabilir miyim? Evet—her PDF sayfasını bir görüntüye dönüştürün (Aspose PDF veya herhangi bir rasterleştirici kullanarak) ve sonucu aynı OCR işlem hattına besleyin. Aynı **recognize text from image** mantığı geçerlidir.

---

## Full Working Example (Copy‑Paste Ready)

```java
import com.aspose.ocr.*;
import java.io.File;

/**
 * Demonstrates how to use Aspose OCR to recognize text from an image
 * that contains multiple languages, with automatic language detection
 * and a speed‑optimising language whitelist.
 */
public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine – reuse this instance for many images
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image that holds mixed languages (replace with your path)
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/mixed-lang.png"));

        // Enable automatic detection of language per text block
        ocrEngine.getSettings().setAutoDetectLanguage(true);

        // OPTIONAL: Restrict detection to English, Russian, and Hindi to boost speed
        ocrEngine.getSettings().setPossibleLanguages(new String[] { "en", "ru", "hi" });

        // Run OCR and capture the result
        OcrResult ocrResult = ocrEngine.recognize();

        // Print the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Dosyayı `MixedLanguageDemo.java` olarak kaydedin, `javac` ile derleyin ve `java MixedLanguageDemo` ile çalıştırın. Her şey doğru ayarlandıysa, çok dilli metnin konsola yazdırıldığını göreceksiniz.

---

## Conclusion

Artık **how to use Aspose**'yi, birkaç dil içeren **recognize text from image** dosyalarından metin tanımak, **enable automatic language detection**'ı etkinleştirmek ve dil havuzunu sınırlayarak **improve OCR speed** için pratik bir ipucu olarak nasıl kullanacağınızı biliyorsunuz. Yukarıdaki tam kod kopyala‑yapıştır için hazır ve açıklamalar, **load image for OCR**'yi bir akıştan, bayt dizisinden ya da bir webcam anlık görüntüsünden almanız gerektiğinde çözümü uyarlamanız için size güven verir.

Sonraki adımlar? Şunları deneyin:

* Düşük kaliteli taramalar için görüntü ön‑işleme (gürültü azaltma, ikilileştirme) eklemek.  
* `OcrResult`'ı JSON olarak dışa aktarmak, sonraki hizmetler için.  
* Motoru bir Spring Boot REST uç noktasına entegre ederek istemcilerin görüntü yükleyip anında çıkarılan metni almasını sağlamak.

Kodlamaktan keyif alın, ve OCR işlem hatlarınız hızlı, doğru ve çok dilli olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}