---
category: general
date: 2026-10-11
description: Java’da bir PNG görüntü üzerinde OCR nasıl yapılır, görüntüden metin
  nasıl çıkarılır ve basit bir OcrEngine örneğiyle görüntüyü metne nasıl dönüştürülür
  öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- recognize text from PNG
- load image java
- convert image to text
language: tr
lastmod: 2026-10-11
og_description: Java’da PNG görüntü üzerinde OCR nasıl yapılır, görüntüden metin nasıl
  çıkarılır ve kısa, doğrudan çalıştırılabilir bir örnekle görüntü metne nasıl dönüştürülür.
og_image_alt: Diagram showing how to perform OCR on a PNG image using Java
og_title: Java'da PNG Görüntüsü Üzerinde OCR Nasıl Yapılır – Tam Rehber
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  headline: How to perform OCR on a PNG image in Java
  type: TechArticle
- description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  name: How to perform OCR on a PNG image in Java
  steps:
  - name: 4.1 Handling low‑resolution PNGs
    text: 'Tesseract performs best on images with at least 300 DPI. If your source
      PNG is smaller, upscale it before OCR:'
  - name: 4.2 Extracting non‑English text
    text: 'To **extract text from image** that contains other languages, download
      the appropriate `.traineddata` files and set the language code:'
  - name: 4.3 Batch processing multiple PNGs
    text: 'If you need to **recognize text from PNG** files in a folder, iterate over
      the directory:'
  - name: 4.4 Dealing with OCR errors
    text: 'Typical OCR mistakes include misreading `0` (zero) as `O` or `1` as `l`.
      Post‑processing with regular expressions can clean the result:'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
- Text Extraction
title: Java'da PNG görüntüsü üzerinde OCR nasıl yapılır
url: /tr/java/ocr-basics/how-to-perform-ocr-on-a-png-image-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da PNG Görüntüsü Üzerinde OCR Nasıl Yapılır

Bir görüntü dosyası üzerinde **perform OCR** yapmanız gerekiyorsa, Java'da **how to perform OCR** öğrenmek birçok otomasyon görevi için çok önemlidir. Makbuzları dijitalleştiriyor, taranmış belgeleri indeksliyor ya da aranabilir bir fotoğraf arşivi oluşturuyor olun, **extract text from image** dosyalarından metin çıkarma yeteneği sayısız manuel saati tasarruf ettirir.

Bu öğretici, bir PNG dosyasını yükleyen, bir OCR motoru çalıştıran ve **recognize text from PNG** dosyalarından metin tanıyan eksiksiz, çalıştırılabilir bir çözüm gösterir. Ayrıca **convert image to text** nasıl yapılır ve düşük çözünürlüklü giriş ya da ASCII olmayan karakterler gibi yaygın tuzakların nasıl ele alınacağını göreceksiniz.

## Neler Başaracaksınız

Bu rehberin sonunda şunları yapabilecek durumdasınız:

* **load image java** kodu, diskteki bir PNG dosyasını okur,
* hafif bir OCR motoru başlatır,
* **extract text from image** ve sonucu konsola yazdırır,
* çözümü diğer görüntü formatları veya toplu işleme için uyarlayın.

Harici hizmetlere gerek yok—yalnızca tek bir açık kaynak OCR kütüphanesi (Tess4J) ve Java SE çalışma zamanı.

## Önkoşullar

* Java 17 veya daha yeni (kod JDK 17 ile derlenir).
* Bağımlılık yönetimi için Maven veya Gradle.
* Seçtiğiniz komut satırı ve IDE hakkında temel bilgi.
* `tess4j` kütüphanesi (Tesseract için bir Java sarmalayıcı). Aşağıdaki Maven bağımlılığını ekleyin:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

Gradle kullanıyorsanız, eşdeğeri şudur:

```gradle
implementation 'net.sourceforge.tess4j:tess4j:5.4.0'
```

Ayrıca Tesseract veri dosyalarına (`.traineddata`) ihtiyacınız var. Resmi depodan İngilizce veri paketini indirin ve proje kökünde `tessdata` adlı bir klasöre yerleştirin.

## Adım 1: Görüntüyü Java'da Yükleyin

Standart `ImageIO` sınıfı ile PNG yüklemek basittir. Aşağıdaki kod, **load image java** güvenli ve istisna‑bilinçli bir şekilde gösterir:

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Reads a PNG file from the given path and returns a BufferedImage.
 *
 * @param path absolute or relative path to the PNG file
 * @return BufferedImage representation of the file
 * @throws Exception if the file cannot be read or is not a PNG
 */
private static BufferedImage loadPng(String path) throws Exception {
    File imgFile = new File(path);
    if (!imgFile.exists()) {
        throw new IllegalArgumentException("File not found: " + path);
    }
    BufferedImage img = ImageIO.read(imgFile);
    if (img == null) {
        throw new IllegalArgumentException("Unsupported image format or corrupt file: " + path);
    }
    return img;
}
```

**Neden önemli:** `ImageIO.read` görüntü formatını otomatik olarak algılar, ancak PNG bozuk olduğunda sessiz hatalardan kaçınmak için `null` kontrolü yaparız. Bu desen, OCR için **load image java** yaparken en iyi uygulamalardan biridir.

## Adım 2: OCR Motorunu Başlatın

Tess4J, yerel Tesseract ikili dosyasını sarar ve basit bir Java API'si sunar. Aşağıdaki metod bir `Tesseract` örneği oluşturur, onu `tessdata` klasörüne yönlendirir ve dili İngilizce olarak yapılandırır:

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;

/**
 * Configures and returns a ready‑to‑use Tesseract instance.
 *
 * @return configured ITesseract object
 */
private static ITesseract createOcrEngine() {
    ITesseract tesseract = new Tesseract();
    // Path to the folder that contains .traineddata files
    tesseract.setDatapath("tessdata");
    // Language code – "eng" for English; you can add more languages later
    tesseract.setLanguage("eng");
    // Optional: increase OCR accuracy for PNGs with low DPI
    tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
    return tesseract;
}
```

**Neden bunu yapıyoruz:** Motoru bir kez başlatıp birden çok görüntüde yeniden kullanmak başlangıç yükünü azaltır. `setOcrEngineMode` çağrısı varsayılan modu seçer, bu çoğu PNG için iyi çalışır. Gürültülü taramalarla karşılaşırsanız, diğer modları deneyebilirsiniz (örn., `OEM_LSTM_ONLY`).

## Adım 3: OCR Yapın ve **recognize text from PNG**

Şimdi görüntü yükleyiciyi ve OCR motorunu birleştiriyoruz. Aşağıdaki metod bir `BufferedImage` üzerinde OCR çalıştırır ve çıkarılan dizeyi döndürür:

```java
/**
 * Runs OCR on the supplied image and returns the recognized text.
 *
 * @param image BufferedImage containing the PNG to process
 * @param tesseract configured OCR engine
 * @return plain‑text result of OCR
 * @throws Exception if OCR fails
 */
private static String extractText(BufferedImage image, ITesseract tesseract) throws Exception {
    // Tess4J can directly accept a BufferedImage
    return tesseract.doOCR(image);
}
```

**Tam çalıştırılabilir örnek**

```java
import java.awt.image.BufferedImage;
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.TesseractException;

public class OcrDemo {

    public static void main(String[] args) {
        try {
            // 1️⃣ Load the PNG file
            BufferedImage image = loadPng("sample.png");

            // 2️⃣ Create and configure the OCR engine
            ITesseract ocrEngine = createOcrEngine();

            // 3️⃣ Recognize text from PNG
            String recognizedText = extractText(image, ocrEngine);

            // 4️⃣ Display the result – this is the **convert image to text** step
            System.out.println("=== OCR RESULT ===");
            System.out.println(recognizedText);
        } catch (Exception e) {
            System.err.println("Error during OCR processing:");
            e.printStackTrace();
        }
    }

    // ----- Helper methods from previous steps -----
    // loadPng, createOcrEngine, extractText (copy-pasted here for completeness)
    // ... (methods omitted for brevity; see the sections above) ...
}
```

**Beklenen çıktı**

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑09‑30
Total: $1,234.56
Thank you for your business!
```

Konsol, motorun `sample.png` dosyasından çıkardığı tam karakterleri gösterecek. PNG yalnızca tek bir kelime içeriyorsa, çıktı bu kelime ve ardından bir yeni satır olacaktır.

## Adım 4: Yaygın varyasyonlar ve kenar durumları

### 4.1 Düşük‑çözünürlüklü PNG'leri İşleme

Tesseract en az 300 DPI'ye sahip görüntülerde en iyi performansı gösterir. Kaynak PNG'niz daha küçükse, OCR'dan önce ölçeklendirin:

```java
import java.awt.Graphics2D;
import java.awt.Image;
import java.awt.RenderingHints;

private static BufferedImage upscale(BufferedImage src, int scaleFactor) {
    int width = src.getWidth() * scaleFactor;
    int height = src.getHeight() * scaleFactor;
    Image tmp = src.getScaledInstance(width, height, Image.SCALE_SMOOTH);
    BufferedImage resized = new BufferedImage(width, height, BufferedImage.TYPE_INT_ARGB);
    Graphics2D g2d = resized.createGraphics();
    g2d.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                         RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g2d.drawImage(tmp, 0, 0, null);
    g2d.dispose();
    return resized;
}
```

`extractText`'i çağırmadan önce `upscale(image, 2)` uygulayarak doğruluğu artırın.

### 4.2 İngilizce olmayan metin çıkarma

Diğer dilleri içeren bir görüntüden **extract text from image** yapmak için uygun `.traineddata` dosyalarını indirin ve dil kodunu ayarlayın:

```java
tesseract.setLanguage("eng+deu"); // English + German
```

### 4.3 Birden çok PNG'yi toplu işleme

Bir klasördeki **recognize text from PNG** dosyalarını işlemek istiyorsanız, dizini döngüyle gezinin:

```java
File folder = new File("pngs/");
for (File file : folder.listFiles((d, name) -> name.toLowerCase().endsWith(".png"))) {
    BufferedImage img = loadPng(file.getPath());
    String text = extractText(img, ocrEngine);
    System.out.println("File: " + file.getName());
    System.out.println(text);
}
```

### 4.4 OCR hatalarıyla başa çıkma

Tipik OCR hataları, `0` (sıfır) karakterini `O` ya da `1` karakterini `l` olarak okuma gibi hataları içerir. Düzenli ifadelerle son işlem yaparak sonucu temizleyebilirsiniz:

```java
String cleaned = recognizedText.replaceAll("[\\r\\n]+", " ").trim();
```

## Java'da Güvenilir OCR İçin Profesyonel İpuçları

| Tip | Neden |
|-----|--------|
| **Use a lossless PNG** | JPEG'deki sıkıştırma artefaktları motoru şaşırtabilir. |
| **Trim white borders** | Gereksiz beyaz boşluk işlem süresini artırır ve yanlış pozitiflere yol açabilir. |
| **Set `tesseract.setPageSegMode(ITesseract.PSM_AUTO)`** only when layout is unknown; otherwise choose a specific mode (e.g., `PSM_SINGLE_BLOCK`). | Düzen bilinmediğinde sadece `tesseract.setPageSegMode(ITesseract.PSM_AUTO)` ayarlayın; aksi takdirde belirli bir mod seçin (örn., `PSM_SINGLE_BLOCK`). |
| **Cache the `ITesseract` instance** |  |

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalar içeren eksiksiz çalışan kod örnekleri sunar.

- [How to Read Text from an Image in Java Using Aspose OCR – Complete Guide](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [How to Use OCR in Java – Recognize Text from Image Quickly](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/)
- [Batch Image OCR in Java – Extract Text from PNG Files Fast](/ocr/english/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}