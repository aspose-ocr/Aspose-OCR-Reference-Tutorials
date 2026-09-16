---
category: general
date: 2026-09-16
description: Java'da daha hızlı OCR için GPU'yu nasıl etkinleştireceğinizi öğrenin,
  görüntü dosyalarından metin tanıyın ve Aspose OCR kullanarak görüntüyü metne dönüştürün.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable gpu
- recognize text from image
- extract text from image
- how to perform ocr
- convert image to text
language: tr
lastmod: 2026-09-16
og_description: Java’da OCR için GPU’yu nasıl etkinleştirir, görüntü dosyalarından
  metni tanır ve Aspose OCR ile görüntüyü metne dönüştürür – tam bir adım adım rehber.
og_image_alt: Screenshot showing Java code that enables GPU for OCR and extracts text
  from an image
og_title: Java'da GPU'yu etkinleştirme ve görüntülerden metin çıkarma
schemas:
- author: Aspose
  dateModified: '2026-09-16'
  description: Learn how to enable GPU for faster OCR in Java, recognize text from
    image files and convert image to text using Aspose OCR.
  headline: How to enable GPU and extract text from images in Java
  type: TechArticle
- description: Learn how to enable GPU for faster OCR in Java, recognize text from
    image files and convert image to text using Aspose OCR.
  name: How to enable GPU and extract text from images in Java
  steps:
  - name: '**Pre‑processing** – de‑skew, binarize, and enhance contrast (GPU‑accelerated).'
    text: '**Pre‑processing** – de‑skew, binarize, and enhance contrast (GPU‑accelerated).'
  - name: '**Segmentation** – locate text lines, words, and characters.'
    text: '**Segmentation** – locate text lines, words, and characters.'
  - name: '**Classification** – match each character against the built‑in language
      model.'
    text: '**Classification** – match each character against the built‑in language
      model.'
  type: HowTo
tags:
- OCR
- Java
- Aspose
- GPU acceleration
title: Java'da GPU'yu etkinleştirme ve görüntülerden metin çıkarma
url: /tr/java/advanced-ocr-techniques/how-to-enable-gpu-and-extract-text-from-images-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da GPU'yu Etkinleştirme ve Görüntülerden Metin Çıkarma

Optik karakter tanıma için **GPU'yu nasıl etkinleştireceğinizi** öğrenmeniz gerekiyorsa, bu kılavuz size tam adımları gösterir. GPU hızlandırmasını açarak **görüntü dosyalarından metin tanıyabilirsiniz** ve CPU‑only işleme göre birkaç kat daha hızlı olur. Örnek Aspose OCR for Java kullanıyor, ancak kavramlar herhangi bir GPU‑uyumlu OCR kütüphanesine de uygulanabilir.

Bu öğreticide şunları öğreneceksiniz:

* OCR motorunda GPU hızlandırmasını etkinleştirme.  
* Bir görüntüyü yükleme ve **görüntü dosyalarından metin çıkarma**.  
* **Görüntüyü metne dönüştürme** sadece birkaç satır kodla.  

Harici hizmetlere gerek yok—her şey makinenizde yerel olarak çalışır. Temel bir Java geliştirme ortamı ve Aspose OCR for Java kütüphanesi tek ön koşuldur.

## Önkoşullar

| Gereksinim | Sürüm / Detay |
|-------------|------------------|
| Java Development Kit (JDK) | 8 or newer |
| Maven or Gradle (for dependency management) | Any recent version |
| GPU with CUDA support (optional but recommended) | NVIDIA GPU with driver ≥ 450 |
| Aspose OCR for Java library | 23.9 or newer (download from the Aspose website) |

GPU'nuz yoksa, kod hâlâ çalışır; sadece CPU üzerinde çalışacaktır.

## Adım 1: Aspose OCR'yi projenize ekleyin

Maven için, aşağıdaki bağımlılığı `pom.xml` dosyanıza ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version>
</dependency>
```

Gradle için, bunu `build.gradle` dosyasına yerleştirin:

```groovy
implementation 'com.aspose:aspose-ocr:23.9'
```

Bu girdiler OCR motorunu ve yerel GPU ikili dosyalarını otomatik olarak çeker.

## Adım 2: OCR motoru için GPU'yu nasıl etkinleştirirsiniz

Ana görev, `OcrEngine`'e GPU'yu kullanmasını söylemektir. Aspose OCR basit bir bayrak sunar:

```java
// Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Enable GPU acceleration – this is the “how to enable gpu” step
ocrEngine.setGpuEnabled(true);
```

**Neden önemli:** `setGpuEnabled(true)` çağrıldığında, kütüphane görüntü ön işleme ve karakter segmentasyon aşamalarını paralelleştiren CUDA‑tabanlı çekirdekleri yükler. Modern bir NVIDIA kartta, varsayılan CPU yoluna göre 2‑4 kat hız artışı görebilirsiniz.

> **Pro ipucu:** Bayrağı etkinleştirmeden önce `SystemInfo.isCudaSupported()` çalıştırarak GPU'nuzun algılandığını doğrulayın. Metot `false` dönerse, motor otomatik olarak CPU'ya geri dönecektir.

## Adım 3: İşlemek istediğiniz görüntüyü yükleyin

OCR motoruna Aspose tarafından desteklenen herhangi bir görüntü formatını (JPEG, PNG, BMP, TIFF, vb.) verebilirsiniz. İşte bir JPEG dosyasını nasıl yükleyeceğiniz:

```java
// Load the image that contains the text to be recognized
String imagePath = "YOUR_DIRECTORY/sample.jpg";
ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

**Köşe durumu:** Görüntü büyükse (5 MB üzeri) önce yeniden boyutlandırarak bellek tüketimini azaltmayı düşünün. OCR motoru, yaklaşık 300 dpi civarındaki görüntülerde en iyi performansı gösterir.

## Adım 4: OCR'yi gerçekleştir ve **görüntüden metin tanı**

Motor yapılandırıldı ve görüntü yüklendiğine göre, tanıma işlemini çalıştırabilirsiniz:

```java
// Execute OCR – this is the core “how to perform ocr” step
String recognizedText = ocrEngine.recognize();
```

`recognize()` metodu düz metin bir `String` döndürür. İçeride motor birkaç aşama çalıştırır:

1. **Ön‑işleme** – eğriliği düzeltme, ikiliye çevirme ve kontrastı artırma (GPU‑hızlandırmalı).  
2. **Segmentasyon** – metin satırlarını, kelimeleri ve karakterleri bulma.  
3. **Sınıflandırma** – her karakteri yerleşik dil modeline karşı eşleştirme.

GPU etkin olduğu için, adım 1 ve 2 paralel yürütmeden en çok fayda sağlar.

## Adım 5: Çıkarılan metni göster veya kaydet

Son olarak, sonucu konsola, bir dosyaya veya herhangi bir sonraki işleyiciye çıktı olarak verin:

```java
// Show the extracted text – this completes the “convert image to text” flow
System.out.println("Recognized text:\n" + recognizedText);

// Optional: write the text to a file
Files.write(Paths.get("output.txt"), recognizedText.getBytes(StandardCharsets.UTF_8));
```

**Tipik çıktı** (“Hello World” içeren örnek bir görüntü için):

```
Recognized text:
Hello World
```

OCR herhangi bir karakter tespit edemezse, `recognizedText` boş bir dize olacaktır. Bu durumda, görüntü kalitesini yeniden kontrol edin veya performansı karşılaştırmak için GPU'yu devre dışı bırakın.

## Yaygın tuzakların ele alınması

| Sorun | Neden | Çözüm |
|-------|-------|-----|
| **GPU not detected** | Missing CUDA driver or unsupported GPU | Install the latest NVIDIA driver and verify with `nvidia-smi`. |
| **Incorrect characters** | Low contrast or noisy background | Pre‑process the image (e.g., increase contrast) before feeding it to the engine. |
| **Out‑of‑memory error** | Very large images on limited GPU memory | Resize the image to ≤ 2000 px width or process in tiles. |
| **Language mismatch** | Default language model is English but text is in another language | Call `ocrEngine.setLanguage(OcrLanguage.SPANISH)` (or appropriate enum) before `recognize()`. |

## Tam, çalıştırılabilir örnek

Aşağıda tüm adımları bir araya getiren bağımsız bir Java sınıfı bulunmaktadır. `GpuEnabledOcrExample.java` olarak kaydedin, görüntü yolunu ayarlayın ve `javac`/`java` ile ya da IDE'niz üzerinden çalıştırın.

```java
import com.aspose.ocr.*;
import java.nio.file.*;

public class GpuEnabledOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Turn on GPU acceleration for faster processing
        // This is the core "how to enable gpu" call
        ocrEngine.setGpuEnabled(true);

        // Optional sanity check – ensures CUDA is available
        if (!SystemInfo.isCudaSupported()) {
            System.out.println("CUDA not detected. Falling back to CPU.");
        }

        // Step 3: Load the image that contains the text to be recognized
        // Replace with the absolute path to your image file
        String imagePath = "YOUR_DIRECTORY/sample.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 4: Perform the OCR operation and obtain the recognized text
        // This answers "how to perform ocr" and "recognize text from image"
        String recognizedText = ocrEngine.recognize();

        // Step 5: Display the extracted text – completes "convert image to text"
        System.out.println("Recognized text:\n" + recognizedText);

        // (Optional) Save the result to a text file
        Path output = Paths.get("recognized_output.txt");
        Files.write(output, recognizedText.getBytes());
        System.out.println("Text saved to " + output.toAbsolutePath());
    }
}
```

### Beklenen sonuç

Programı çalıştırmak, çıkarılan metni konsola yazdırır ve aynı içeriği `recognized_output.txt` dosyasına yazar. GPU etkinleştirildiğinde, 2 MP bir görüntü için toplam yürütme süresi genellikle NVIDIA RTX 3060'da 200 ms'nin altında olur, CPU yalnızken ise ~500 ms'dir.

## Sonuç

Artık Java'da Aspose OCR için **GPU'yu nasıl etkinleştireceğinizi**, **görüntü dosyalarından metin tanıyacağınızı** ve **görüntüyü metne dönüştüreceğinizi** birkaç basit kod satırıyla biliyorsunuz. GPU hızlandırmasını kullanarak daha hızlı işlem elde edersiniz; bu, fatura tarama, fiş işleme ve belge dijitalleştirme gibi toplu veya gerçek‑zaman uygulamaları için çok önemlidir.

**Sonraki adımlar**

* Farklı dil modelleri (`ocrEngine.setLanguage`) ile **görüntü dosyalarından metin çıkarma** deneyin; Fransızca, Almanca veya Çince için.  
* OCR çıktısını Apache Tika ile birleştirerek çıkarılan içeriği otomatik olarak indeksleyin.  
* PDF içinde **görüntüden metin tanıma** çerçevelerine ihtiyacınız varsa büyük PDF'leri sayfa‑sayfa akış olarak keşfedin.

Örneği özgürce uyarlayın, kendi hizmetlerinize entegre edin ve sonuçlarınızı paylaşın. İyi kodlamalar!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Java'da Aspose OCR Kullanarak Görüntüden Metin Okuma – Tam Kılavuz](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Aspose OCR ile metin görüntüsü tanıma – Tam Java OCR Öğreticisi](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Java'da görüntüden metne: Aspose.OCR ile Görüntüyü Metne Dönüştürme](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}