---
category: general
date: 2026-05-31
description: Aspose OCR Java kullanarak görüntülerden metni hızlı bir şekilde tanıyın.
  PNG dosyalarından metin çıkarmayı ve en iyi sonuçlar için OCR dilini ayarlamayı
  öğrenin.
draft: false
keywords:
- recognize text from images
- extract text from png
- set OCR language
- Aspose OCR Java
- parallel OCR processing
language: tr
og_description: Aspose OCR Java ile görüntülerden metni verimli bir şekilde tanıyın.
  Bu öğreticide, png dosyalarından metin nasıl çıkarılır ve toplu işleme için OCR
  dili nasıl ayarlanır gösterilmektedir.
og_title: görüntülerden metin tanıma – Aspose OCR Java Paralel Toplu İşlem
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: recognize text from images quickly using Aspose OCR Java. Learn how
    to extract text from png files and set OCR language for optimal results.
  headline: recognize text from images with Aspose OCR – Java Parallel Batch Guide
  type: TechArticle
- description: recognize text from images quickly using Aspose OCR Java. Learn how
    to extract text from png files and set OCR language for optimal results.
  name: recognize text from images with Aspose OCR – Java Parallel Batch Guide
  steps:
  - name: How It Works
    text: '- **Thread Count** – The processor creates a thread pool of the size you
      specify. On a quad‑core laptop, `4` is a sweet spot; increase it for servers
      with more cores. - **Language Setting** – By calling `setLanguage(OcrLanguage.FRENCH)`,
      we tell the OCR engine to bias its dictionary toward French ch'
  - name: 1️⃣ Missing or Corrupt Images
    text: If an image path is invalid, `OcrBatchProcessor` throws an `IOException`.
      Wrap the call in a try‑catch block, log the problematic file, and continue with
      the rest of the batch.
  - name: 2️⃣ Mixed Languages in One Batch
    text: 'When you have documents in multiple languages, you can either:'
  - name: 3️⃣ Memory Constraints
    text: Processing very large images (e.g., >10 MB) can inflate heap usage. Pre‑scale
      the images or increase the JVM’s `-Xmx` flag if you encounter `OutOfMemoryError`.
  - name: 4️⃣ Customizing OCR Settings
    text: 'Beyond language, you can tweak recognition speed vs. accuracy:'
  - name: LicenseUtil.java
    text: '```java import com.aspose.ocr.*;'
  - name: ImageProvider.java
    text: '```java import java.util.*;'
  - name: ParallelBatchDemo.java
    text: '```java import com.aspose.ocr.*; import java.util.*;'
  type: HowTo
tags:
- Java
- OCR
- Aspose
- Image Processing
title: Aspose OCR ile Görsellerden Metin Tanıma – Java Paralel Toplu Rehberi
url: /tr/java/advanced-ocr-techniques/recognize-text-from-images-with-aspose-ocr-java-parallel-bat/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntülerden Metin Tanıma – Aspose OCR Java Paralel Toplu İşlem Öğreticisi

Hiç **görüntülerden metin tanıma** işleminin UI'nızı dondurmadığı bir şekilde nasıl yapılacağını merak ettiniz mi? Belki elinizde tarama, ekran görüntüsü ya da PNG ve JPEG dosyalarının karışımından oluşan bir klasör var ve metni acilen elde etmeniz gerekiyor. İyi haber? Aspose OCR for Java ile kahvenizi yudumlarken **png'den metin çıkarma** (ve diğer formatlar) yapan çok‑iş parçacıklı bir toplu işlem başlatabilirsiniz.

Bu rehberde, **OCR dili ayarlama**, dört paralel çalışan başlatma ve sonuçları yazdırma adımlarını gösteren tam, çalıştırılabilir bir örnek üzerinden ilerleyeceğiz. Sonunda, ekstra süslemeler olmadan, ihtiyacınız olan kodu içeren sağlam bir şablonu herhangi bir Java projesine ekleyebileceksiniz.

## Öğrenecekleriniz

- Aspose OCR lisansını nasıl uygulayacağınızı ve değerlendirme sınırlamalarıyla karşılaşmayacağınızı öğrenin.  
- **görüntülerden metin tanıma** işlemini paralel olarak nasıl yapacağınızı, çok çekirdekli makinelerde verimliliği artırarak keşfedin.  
- Daha iyi doğruluk için **OCR dili ayarlama** (demoda Fransızca) neden ve nasıl yapılır, öğrenin.  
- **png'den metin çıkarma** için pratik bir yol; aynı mantık JPG, TIFF, BMP vb. dosyalar için de geçerlidir.  

**Önkoşullar** – Java 8 veya daha yeni bir sürüm, Aspose OCR kütüphanesini çekmek için Maven ya da Gradle ve geçerli bir Aspose OCR lisans dosyası (`Aspose.OCR.Java.lic`) gerekir. Özel bir IDE hilesi gerekmez; Java derleyebilen herhangi bir editör yeterlidir.

---

## Adım 1: Aspose OCR Bağımlılığını Ekleyin

İlk olarak, Aspose OCR JAR dosyasının sınıf yolunuzda olduğundan emin olun. Maven kullanıyorsanız şunu ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

Gradle için:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

> **Pro ipucu:** Aspose sürüm notlarını takip edin; genellikle dil paketleri ya da performans iyileştirmeleri eklenir ve bu da toplu işlem sürelerini saniyelerce kısaltabilir.

## Adım 2: Aspose OCR Lisansını Uygulayın

Lisans olmadan kütüphane demo modunda çalışır ve çıktıya filigran ekler. Lisans dosyanızı bir kez, tercihen uygulama başlangıcında yükleyin.

```java
import com.aspose.ocr.*;

public class LicenseUtil {
    /** Loads the Aspose OCR license from the given path. */
    public static void applyLicense(String licensePath) throws Exception {
        License license = new License();
        license.setLicense(licensePath);
        System.out.println("Aspose OCR license applied successfully.");
    }
}
```

`LicenseUtil.applyLicense("Aspose.OCR.Java.lic")` çağrısı, sonraki her **görüntülerden metin tanıma** çağrısının kısıtlama olmadan çalışmasını sağlar.

## Adım 3: Görüntü Listesini Hazırlayın

Toplu işlemciye herhangi bir dosya yolu koleksiyonunu besleyebilirsiniz. Aşağıda **png'den metin çıkarma** örneğini JPEG ve TIFF dosyalarıyla birlikte gösteriyoruz—yolları kendi dizininizle değiştirmeniz yeterli.

```java
import java.util.*;

public class ImageProvider {
    /** Returns a list of absolute image paths to be processed. */
    public static List<String> getImagePaths() {
        return Arrays.asList(
            "YOUR_DIRECTORY/doc1.png",   // PNG – our primary example
            "YOUR_DIRECTORY/doc2.jpg",
            "YOUR_DIRECTORY/doc3.tif"
        );
    }
}
```

> **Neden Liste?** `OcrBatchProcessor`, işi otomatik olarak iş parçacıkları arasında bölüştürebilmek için bir `List<String>` bekler.

## Adım 4: Paralel Toplu İşlemciyi Yapılandırın ve Çalıştırın

İşte öğreticinin kalbi: bir `OcrBatchProcessor` oluşturmak, kaç iş parçacığı kullanılacağını belirtmek ve **OCR dili ayarlama**yı Fransızca olarak ayarlamak (gerektiğinde `OcrLanguage.ENGLISH` ya da desteklenen başka bir dil ile değiştirin).

```java
import com.aspose.ocr.*;

public class ParallelBatchDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply the license
        LicenseUtil.applyLicense("Aspose.OCR.Java.lic");

        // 2️⃣ Gather image files
        List<String> imagePaths = ImageProvider.getImagePaths();

        // 3️⃣ Create and configure the batch processor
        OcrBatchProcessor batchProcessor = new OcrBatchProcessor();
        batchProcessor.setThreadCount(4);                 // 4 parallel workers
        batchProcessor.setLanguage(OcrLanguage.FRENCH);   // set OCR language

        // 4️⃣ Run OCR on the entire batch – this is where we **recognize text from images**
        List<OcrResult> ocrResults = batchProcessor.recognize(imagePaths);

        // 5️⃣ Output the recognized text for each file
        for (int i = 0; i < ocrResults.size(); i++) {
            System.out.println("File: " + imagePaths.get(i));
            System.out.println(ocrResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

### Nasıl Çalışır

- **İş Parçacığı Sayısı** – İşlemci, belirttiğiniz boyutta bir iş parçacığı havuzu oluşturur. Dört çekirdekli bir dizüstü bilgisayarda `4` ideal bir değerdir; daha fazla çekirdeği olan sunucularda artırabilirsiniz.  
- **Dil Ayarı** – `setLanguage(OcrLanguage.FRENCH)` çağrısı, OCR motoruna sözlüğünü Fransızca karakterlere göre ağırlıklandırmasını söyler; bu, İngilizce dışı belgelerde doğruluğu büyük ölçüde artırır.  
- **Toplu Tanıma** – `recognize` metodu, sağlanan listeyi iç döngüyle işler, işi dağıtır ve orijinal sıralamayı koruyan bir `List<OcrResult>` döndürür. Kendi iş parçacığı yönetiminizi yazmadan **görüntülerden metin tanıma** yapmanın en basit yoludur.

## Adım 5: Çıktıyı Doğrulayın

Programı çalıştırdığınızda aşağıdakine benzer bir şey görmelisiniz:

```
File: YOUR_DIRECTORY/doc1.png
Bonjour le monde! Ceci est un test d'OCR.
---
File: YOUR_DIRECTORY/doc2.jpg
Hello world! This is an OCR test.
---
File: YOUR_DIRECTORY/doc3.tif
¡Hola mundo! Prueba de OCR.
---
```

Eğer Fransızca dosya (`doc1.png`) Fransızca metin içeriyorsa, **OCR dili ayarlama** adımı aksanlı karakterlerin doğru yakalanmasına yardımcı olacaktır. PNG dosyaları için bu, aynı toplu işlem içinde diğer formatları da ele alarak **png'den metin çıkarma** için temiz bir yol gösterir.

---

## Yaygın Kenar Durumlarını Ele Alma

### 1️⃣ Eksik veya Bozuk Görüntüler

Bir görüntü yolu geçersizse, `OcrBatchProcessor` bir `IOException` fırlatır. Çağrıyı try‑catch bloğuna alın, sorunlu dosyayı kaydedin ve toplu işlemin geri kalanına devam edin.

```java
try {
    List<OcrResult> results = batchProcessor.recognize(imagePaths);
} catch (IOException ex) {
    System.err.println("Failed to process: " + ex.getMessage());
}
```

### 2️⃣ Tek Bir Toplu İşlemde Karışık Diller

Birden fazla dilde belgeye sahipseniz şu iki yaklaşımdan birini seçebilirsiniz:

- Her biri kendi `setLanguage` ayarına sahip ayrı toplu işlemler çalıştırın.  
- Veya dili ayarlamadan bırakın (`OcrLanguage.AUTO_DETECT`) ve Aspose’un tahmin etmesine izin verin; ancak doğruluk düşebilir.

### 3️⃣ Bellek Kısıtlamaları

Çok büyük görüntüler (ör. >10 MB) heap kullanımını artırabilir. Görüntüleri önceden ölçeklendirin veya `OutOfMemoryError` alırsanız JVM’nin `-Xmx` bayrağını yükseltin.

```bash
java -Xmx2g -cp yourapp.jar ParallelBatchDemo
```

### 4️⃣ OCR Ayarlarını Özelleştirme

Dil dışındaki ayarlar arasında tanıma hızı ile doğruluk dengesini ayarlayabilirsiniz:

```java
batchProcessor.setRecognitionMode(OcrRecognitionMode.ACCURATE); // default is BALANCED
```

`ACCURATE` seçeneği daha yavaştır ancak gürültülü taramalar için daha iyi sonuç verir.

---

## Tam Çalışan Örnek (Tüm Dosyalar)

Aşağıda ihtiyacınız olan tam kaynak dosyaları bulabilirsiniz. Bunları bir Maven projesine kopyalayın, lisans yolunu ve görüntü dizinini ayarlayın, ardından `mvn exec:java -Dexec.mainClass=ParallelBatchDemo` komutunu çalıştırın.

### LicenseUtil.java
```java
import com.aspose.ocr.*;

public class LicenseUtil {
    public static void applyLicense(String licensePath) throws Exception {
        License license = new License();
        license.setLicense(licensePath);
        System.out.println("Aspose OCR license applied successfully.");
    }
}
```

### ImageProvider.java
```java
import java.util.*;

public class ImageProvider {
    public static List<String> getImagePaths() {
        return Arrays.asList(
            "YOUR_DIRECTORY/doc1.png",
            "YOUR_DIRECTORY/doc2.jpg",
            "YOUR_DIRECTORY/doc3.tif"
        );
    }
}
```

### ParallelBatchDemo.java
```java
import com.aspose.ocr.*;
import java.util.*;

public class ParallelBatchDemo {
    public static void main(String[] args) throws Exception {
        // Apply license
        LicenseUtil.applyLicense("Aspose.OCR.Java.lic");

        // Gather images
        List<String> imagePaths = ImageProvider.getImagePaths();

        // Configure batch processor
        OcrBatchProcessor batchProcessor = new OcrBatchProcessor();
        batchProcessor.setThreadCount(4);                 // Parallelism
        batchProcessor.setLanguage(OcrLanguage.FRENCH);   // set OCR language

        // Recognize text from images
        List<OcrResult> ocrResults = batchProcessor.recognize(imagePaths);

        // Output results
        for (int i = 0; i < ocrResults.size(); i++) {
            System.out.println("File: " + imagePaths.get(i));
            System.out.println(ocrResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

Çalıştırdığınızda, her dosyanın çıkarılan metninin konsola yazdırıldığını göreceksiniz—arama yapılabilir arşivler, veri girişi otomasyonu ya da erişilebilirlik araçları oluştururken tam da ihtiyacınız olan şey.

---

## Sonuç

Aspose OCR for Java kullanarak **görüntülerden metin tanıma** için tam, üretim‑hazır bir desen inceledik. Toplu işlemciyi yapılandırarak **png'den metin çıkarma** (ve diğer formatlar) işlemini paralel yapabilir ve **OCR dili ayarlama** sayesinde çok‑dilli iş yüklerinde mümkün olan en yüksek doğruluğu elde edebilirsiniz.

Sonraki adımlar? Dili `OcrLanguage.SPANISH` olarak değiştirin ya da daha zor taramalar için `OcrRecognitionMode.ACCURATE` ile deney yapın. Sonuçları bir veritabanına entegre edebilir, bir arama indeksine besleyebilir ya da bir çeviri API'sine yönlendirebilirsiniz.

PDF'lerde OCR ya da bulutta depolanan görüntüler gibi zor senaryolarınız mı var? Bunlar, bugün inşa ettiğimiz şeyin doğal uzantılarıdır. İçeri girin, ayarları değiştirin ve OCR motorunun ağır işi halletmesine izin verin.

Kodlamaktan keyif alın, metin çıkarımınız hızlı ve kusursuz olsun!

## Bir Sonraki Öğrenmeniz Gerekenler

- [Metin Görüntülerini Çıkarma – Aspose.OCR for Java ile OCR Temelleri](/ocr/english/java/ocr-basics/)
- [Aspose.OCR Kullanarak Dil Seçimiyle Görüntü Metni OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Aspose OCR ile Metin Görüntüsü Tanıma – Tam Java OCR Öğreticisi](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}