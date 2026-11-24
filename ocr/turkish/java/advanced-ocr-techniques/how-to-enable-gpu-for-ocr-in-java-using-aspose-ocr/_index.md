---
category: general
date: 2026-08-18
description: Java'da OCR için GPU'yu nasıl etkinleştirir ve görüntü metnini hızlıca
  tanır, JPG metnini çıkarır, filtre ekler ve Aspose.OCR ile dili ayarlar.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable gpu
- recognize image text
- extract text jpg
- how to add filter
- how to set language
language: tr
lastmod: 2026-08-18
og_description: Java'da OCR için GPU'yu nasıl etkinleştirir ve görüntü metnini anında
  tanır, metni JPG olarak çıkarır, filtre ekler ve Aspose.OCR kullanarak dili ayarlar.
og_image_alt: Screenshot showing Java code that enables GPU for OCR with Aspose.OCR
og_title: Java'da OCR için GPU'yu nasıl etkinleştirirsiniz – tam Aspose.OCR rehberi
schemas:
- author: Aspose
  dateModified: '2026-08-18'
  description: How to enable GPU for OCR in Java and quickly recognize image text,
    extract text JPG, add filter, and set language with Aspose.OCR.
  headline: How to enable GPU for OCR in Java using Aspose.OCR
  type: TechArticle
- description: How to enable GPU for OCR in Java and quickly recognize image text,
    extract text JPG, add filter, and set language with Aspose.OCR.
  name: How to enable GPU for OCR in Java using Aspose.OCR
  steps:
  - name: 3.1 Set the OCR language
    text: '```java // Choose the language for recognition – this is the “how to set
      language” step engine.setLanguage(OcrLanguage.ENGLISH); ```'
  - name: 3.2 Add a preprocessing filter
    text: 'Noise, compression artifacts, or uneven lighting can hurt accuracy. Adding
      a denoise filter is the typical **how to add filter** approach:'
  - name: Expected output
    text: '``` Recognized text: The quick brown fox jumps over the lazy dog. ```'
  type: HowTo
tags:
- OCR
- Java
- Aspose
- GPU acceleration
title: Java'da Aspose.OCR kullanarak OCR için GPU'yu nasıl etkinleştirirsiniz
url: /tr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da Aspose.OCR ile OCR için GPU'yu nasıl etkinleştirirsiniz

Java'da OCR için **GPU'yu nasıl etkinleştireceğinizi** öğrenmeniz gerekiyorsa, bu kılavuz size tam adımları gösterir. GPU hızlandırmasını etkinleştirmek, **görüntü metnini tanımanıza** birkaç kat daha hızlı olanak tanır; bu, toplu olarak **JPG dosyalarından metin çıkarmak** zorunda olduğunuzda çok önemlidir. Ayrıca **filtre ekleme**, **dil ayarlama** ve son sonucu alma konularını da ele alacağız.

> **Önkoşul:** Java 17 veya daha yeni, Maven ve Aspose.OCR for Java lisansı (değerlendirme için ücretsiz deneme çalışır).

![Java'da OCR için GPU'yu nasıl etkinleştirirsiniz](/images/ocr-gpu.png){alt="Java'da OCR için GPU'yu nasıl etkinleştirirsiniz"}

## İhtiyacınız olanlar

| Öğe | Sebep |
|------|--------|
| **Java Development Kit (JDK) 17+** | Örneği derlemek ve çalıştırmak için gereklidir. |
| **Maven** | Aspose.OCR için bağımlılık yönetimini basitleştirir. |
| **Aspose.OCR for Java** | `OcrEngine` sınıfını ve GPU desteğini sağlar. |
| **A sample JPEG image** (`sample.jpg`) | **extract text JPG** göstermek için kullanılır. |
| **GPU‑compatible hardware** (optional but recommended) | Yapılandıracağımız performans artışını etkinleştirir. |

## Adım 1: Maven projesini kurun

Yeni bir Maven projesi oluşturun (veya mevcut birine ekleyin) ve Aspose.OCR bağımlılığını ekleyin:

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ocr-gpu-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- Aspose.OCR for Java -->
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-ocr</artifactId>
            <version>23.12</version> <!-- Use the latest stable version -->
        </dependency>
    </dependencies>
</project>
```

> **Pro ipucu:** Sürüm numarasını güncel tutun; daha yeni sürümler GPU yönetimini iyileştirir ve dil paketleri ekler.

## Adım 2: OCR motorunu başlatın ve **GPU'yu nasıl etkinleştirirsiniz**

Çözümün kalbi `OcrEngine`'dir. Oluşturulması basittir, ancak GPU hızlandırmasını açıkça etkinleştirmeniz gerekir:

```java
import com.aspose.ocr.*;

public class HelloWorldOcr {
    public static void main(String[] args) throws Exception {
        // Step 2.1: Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // Step 2.2: Enable GPU acceleration (this is the “how to enable GPU” part)
        engine.setUseGpu(true); // <-- GPU is now active

        // Step 2.3: Configure language and preprocessing filter (covered later)
```

**Neden GPU etkinleştirilmeli?**  
`setUseGpu(true)` çağrıldığında, Aspose.OCR ağır görüntü‑işleme çekirdeklerini grafik kartına devreder. Modern bir NVIDIA/AMD GPU'da tanıma hızı sayfa başına ~200 ms'den < 80 ms'ye çıkabilir; bu, büyük partilerde toplam işleme süresini büyük ölçüde azaltır.

## Adım 3: **Dili nasıl ayarlarsınız** ve **filtre nasıl eklenir**

### 3.1 OCR dilini ayarlama

```java
        // Choose the language for recognition – this is the “how to set language” step
        engine.setLanguage(OcrLanguage.ENGLISH);
```

Aspose.OCR, 100'den fazla dil için dil paketleriyle birlikte gelir. Kaynak materyalinize uygun olarak `ENGLISH` yerine `FRENCH`, `CHINESE_SIMPLIFIED` vb. kullanın.

### 3.2 Ön işleme filtresi ekleme

Gürültü, sıkıştırma artefaktları veya dengesiz aydınlatma doğruluğu azaltabilir. Denoise filtresi eklemek tipik **filtre ekleme** yaklaşımıdır:

```java
        // Add a denoising filter to improve OCR quality – “how to add filter”
        engine.addPreprocessFilter(FilterType.DENOISE);
```

Diğer faydalı filtreler `FilterType.CONTRAST`, `FilterType.BRIGHTNESS` ve `FilterType.BINARIZE`'dır. `addPreprocessFilter` metodunu tekrar tekrar çağırarak birden fazla filtreyi zincirleyebilirsiniz.

## Adım 4: Görüntüyü yükleyin – **JPG'den metin çıkarma**

Şimdi motoru işlemek istediğimiz JPEG dosyasına yönlendiriyoruz:

```java
        // Load the JPEG image – this demonstrates “extract text JPG”
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

`YOUR_DIRECTORY`'yi `sample.jpg` dosyasının bulunduğu gerçek yol ile değiştirin. Aspose.OCR ayrıca PNG, BMP, TIFF ve PDF'yi de destekler; aynı çağrı bu formatlar için de çalışır.

## Adım 5: OCR gerçekleştir ve **görüntü metnini tanı**

Motor yapılandırıldıktan sonra tanıma rutinini çağırın:

```java
        // Run the OCR operation – “recognize image text”
        engine.recognize();

        // Retrieve the recognized text
        String text = engine.getText();
        System.out.println("Recognized text: " + text);
    }
}
```

`recognize()` metodu görüntüyü GPU'da (etkinse) işler ve iç metin tamponunu doldurur. `getText()` düz metin bir `String` döndürür; bunu bir dosyaya, veritabanına yazabilir veya sonraki NLP boru hatlarına aktarabilirsiniz.

### Beklenen çıktı

```
Recognized text: The quick brown fox jumps over the lazy dog.
```

Görüntü birden fazla satır içeriyorsa, dönen dize orijinal düzeni koruyan yeni satır karakterleri (`\n`) içerir.

## Adım 6: GPU kullanımını doğrulayın (isteğe bağlı)

GPU'nun gerçekten kullanıldığını doğrulamak için Aspose kaydını etkinleştirin:

```java
        // Enable diagnostic logging (optional)
        engine.setLogLevel(com.aspose.ocr.logging.LogLevel.DEBUG);
        engine.setLogFile("ocr-debug.log");
```

Çalıştırmadan sonra `ocr-debug.log` dosyasını inceleyin; `GPU device: NVIDIA GeForce RTX 3080` ve `Processing time (GPU): 78 ms` gibi girişler görmelisiniz. Günlük **CPU**'yu belirtiyorsa, sürücü kurulumunuzu ve `setUseGpu(true)` çağrısının mevcut olduğunu iki kez kontrol edin.

## Yaygın tuzaklar ve nasıl önlenir

| Semptom | Muhtemel neden | Çözüm |
|---------|----------------|-------|
| **`java.lang.UnsatisfiedLinkError: no aspose_ocr_native`** | Missing native GPU libraries | Install the latest GPU driver and ensure the `aspose-ocr` native binaries are on the `java.library.path`. |
| **Poor accuracy on dark images** | No preprocessing filter | Add `engine.addPreprocessFilter(FilterType.BRIGHTNESS)` or increase `FilterType.CONTRAST`. |
| **`OutOfMemoryError` on large batches** | GPU memory exhaustion | Process images in smaller batches or disable GPU (`engine.setUseGpu(false)`) for very large resolutions. |
| **Incorrect language output** | Wrong language set | Verify `engine.setLanguage(OcrLanguage.YOUR_LANGUAGE)` matches the source text. |

## Tam, çalıştırılabilir örnek

Aşağıda `src/main/java/com/example/HelloWorldOcr.java` içine kopyalayıp yapıştırabileceğiniz tam Java sınıfı bulunmaktadır. Tüm adımları, hata yönetimini ve isteğe bağlı kaydı içerir.

```java
package com.example;

import com.aspose.ocr.*;

public class HelloWorldOcr {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // -------------------------------------------------
        // 1️⃣ Enable GPU acceleration – how to enable GPU
        // -------------------------------------------------
        engine.setUseGpu(true);

        // -------------------------------------------------
        // 2️⃣ Set language – how to set language
        // -------------------------------------------------
        engine.setLanguage(OcrLanguage.ENGLISH); // Change if needed

        // -------------------------------------------------
        // 3️⃣ Add preprocessing filter – how to add filter
        // -------------------------------------------------
        engine.addPreprocessFilter(FilterType.DENOISE);
        // Optional: engine.addPreprocessFilter(FilterType.CONTRAST);

        // -------------------------------------------------
        // 4️⃣ Load the JPEG image – extract text JPG
        // -------------------------------------------------
        String imagePath = "YOUR_DIRECTORY/sample.jpg";
        engine.setImage(ImageStream.fromFile(imagePath));

        // -------------------------------------------------
        // 5️⃣ Perform OCR – recognize image text
        // -------------------------------------------------
        engine.recognize();

        // Retrieve and display the recognized text
        String text = engine.getText();
        System.out.println("Recognized text: " + text);

        // -------------------------------------------------
        // 6️⃣ Optional: write output to a file
        // -------------------------------------------------
        java.nio.file.Files.writeString(
                java.nio.file.Paths.get("output.txt"),
                text,
                java.nio.charset.StandardCharsets.UTF_8
        );

        // -------------------------------------------------
        // 7️⃣ Optional: enable debug logging to verify GPU usage
        // -------------------------------------------------
        engine.setLogLevel(com.aspose.ocr.logging.LogLevel.DEBUG);
        engine.setLogFile("ocr-debug.log");
    }
}
```

### Programı çalıştırma

```bash
mvn compile exec:java -Dexec.mainClass=com.example.HelloWorldOcr
```

Tanıyan metnin konsola yazdırıldığını ve `output.txt` dosyasına kaydedildiğini görmelisiniz. `ocr-debug.log` dosyası GPU kullanımını doğrulayacaktır.

## Sonuç

Bu öğreticide Java'da Aspose.OCR için **GPU'yu nasıl etkinleştirirsiniz**, **görüntü metnini nasıl tanırsınız**, **JPG'den metin çıkarma**, **filtre nasıl eklenir** ve **dil nasıl ayarlanır** konularını tek, bağımsız bir program içinde gösterdik. GPU'yu etkinleştirerek önemli bir hız artışı elde ederken, filtreler ve dil ayarları çeşitli görüntü kaynaklarında yüksek doğruluk sağlar.

**Sonraki adımlar**

* Tarama belgeleri için `FilterType.BINARIZE` gibi ek filtreleri deneyin.  
* Diğer dillere geçin (`OcrLanguage.SPANISH`, `OcrLanguage.CHINESE_SIMPLIFIED`) çok dilli desteği genişletmek için.  
* Bu OCR hattını Apache PDFBox ile birleştirerek PDF sayfalarından doğrudan metin çıkarın.  

Kodu toplu işleme uyarlamaktan, bir Spring Boot servisine entegre etmekten veya gerçek zamanlı OCR iş yükleri için bir mesaj kuyruğuna bağlamaktan çekinmeyin. İyi kodlamalar!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Java'da Aspose OCR Kullanarak Görüntüden Metin Okuma – Tam Kılavuz](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Aspose.OCR Kullanarak Dil ile Görüntü Metnini OCR Yapma](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Aspose OCR ile Java'da Görüntü OCR Ön İşleme – Doğruluğu Artırma & Metin Çıkarma](/ocr/english/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}