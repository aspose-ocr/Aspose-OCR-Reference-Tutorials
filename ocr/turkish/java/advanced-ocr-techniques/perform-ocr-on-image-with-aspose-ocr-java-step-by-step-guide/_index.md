---
category: general
date: 2026-09-23
description: Aspose OCR kullanarak Java'da görüntülerde OCR nasıl yapılır, görüntüden
  metin nasıl çıkarılır ve custom dictionary ile yazım düzeltmesi nasıl etkinleştirilir
  öğrenin.
draft: false
keywords:
- how to perform ocr
- how to extract text from image
- java ocr maven dependency
- java image to text conversion
- aspose ocr java
lastmod: 2026-09-23
og_description: Java'da Aspose OCR ile görüntülerde OCR nasıl yapılır. Bu kılavuz,
  bir görüntünün yüklenmesini, görüntüden metin çıkarılmasını ve doğru sonuçlar için
  spell correction eklenmesini gösterir.
og_image_alt: 'Aspose OCR Java tutorial: extracting text from images with spell correction'
og_title: Java'da Aspose OCR ile görüntülerde OCR nasıl yapılır
schemas:
- author: Aspose
  dateModified: '2026-09-23'
  description: Learn how to perform OCR on images in Java using Aspose OCR, extract
    text from image, and enable spell correction with a custom dictionary.
  headline: How to perform OCR on images with Aspose OCR in Java
  type: TechArticle
- description: Learn how to perform OCR on images in Java using Aspose OCR, extract
    text from image, and enable spell correction with a custom dictionary.
  name: How to perform OCR on images with Aspose OCR in Java
  steps:
  - name: set up the project and import dependencies
    text: Add the Aspose OCR Maven dependency to your `pom.xml`. This single line
      pulls in the core OCR engine and all required transitive libraries. > **Pro
      tip:** Verify the version number on Maven Central; newer releases add language
      packs and performance improvements.
  - name: load the image for OCR
    text: '`OcrEngine` works with any `InputStream`. Use `ImageStream` to wrap a file
      path, byte array, or URL. **Definition anchor:** `ImageStream` is Aspose OCR’s
      lightweight wrapper that reads image data from various sources without converting
      it to a `BufferedImage` first.'
  - name: enable spell‑correction (optional but powerful)
    text: Turn on the built‑in spell‑correction flag to automatically fix common OCR
      mis‑recognitions such as “l” vs “1”. Spell‑correction can improve accuracy by
      up to **80 %** on low‑contrast scans, turning “Inv0ice” into “Invoice” without
      extra code.
  - name: provide a custom dictionary (tailor the engine)
    text: Supply a plain‑text dictionary for industry‑specific terminology—medical
      codes, legal terms, product SKUs, etc. **Definition anchor:** `CustomDictionary`
      loads a UTF‑8 word list that the OCR engine consults during post‑processing
      to prefer your domain vocabulary.
  - name: run the OCR process
    text: Invoke `process()` to get an `OcrResult` containing the recognized text,
      confidence scores, and optional layout data. If an error occurs, `ocrResult.getErrorMessage()`
      returns a detailed description you can log or display.
  - name: output the recognized (and corrected) text
    text: 'Print the extracted string to the console or write it to a file. For quick
      testing, a simple `System.out.println` is sufficient. Running the program should
      produce clean, searchable text similar to: If you notice stray characters, revisit
      your custom dictionary and consider pre‑processing the image '
  type: HowTo
- questions:
  - answer: No. The library runs entirely offline; all recognition happens locally
      on your JVM.
    question: Does Aspose OCR require an internet connection?
  - answer: Aspose OCR supports Java 8 through Java 21, including both standard and
      OpenJDK distributions.
    question: Which Java versions are supported?
  - answer: Yes. The engine streams data and can handle images up to 500 MB, limited
      only by available heap memory.
    question: Can I process images larger than 10 MB?
  - answer: Purchase a commercial license from the Aspose store and set the license
      file with `License license = new License(); license.setLicense("Aspose.OCR.lic");`.
    question: How do I license Aspose OCR for production?
  - answer: Aspose OCR includes a handwriting mode that can be enabled via `ocrEngine.getEngineOptions().setHandwriting(true);`,
      improving accuracy on cursive scripts.
    question: Is there built‑in support for handwritten text?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
- image to text
- OCR Maven dependency
title: Java'da Aspose OCR ile görüntülerde OCR nasıl yapılır
url: /tr/java/advanced-ocr-techniques/perform-ocr-on-image-with-aspose-ocr-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüde OCR Yapma – Tam Java Öğreticisi

Java kullanarak görüntü dosyalarında **how to perform OCR** yapmak için güvenilir bir yol arıyorsanız, doğru yere geldiniz. Aspose OCR for Java ile sadece birkaç satır kodla görüntü varlıklarından metin çıkarabilir, özel bir sözlükle doğruluğu artırabilir ve gürültülü taramaları temizlemek için yazım‑düzeltmeyi etkinleştirebilirsiniz. Bu öğretici, OCR için görüntüyü yüklemekten düzeltilmiş metni yazdırmaya kadar her adımı size gösterir; böylece uygulamalarınıza görüntü‑metin dönüşümünü bugün entegre edebilirsiniz.

## Hızlı Yanıtlar
- **OCR başlatmak için ana sınıf nedir?** `OcrEngine` Aspose OCR’nin optik karakter tanıma yapan çekirdek sınıfıdır.
- **Hangi Maven artefaktı OCR desteği ekler?** `com.aspose:aspose-ocr` öğesini `pom.xml` dosyanıza ekleyin.
- **Geliştirme için lisansa ihtiyacım var mı?** Test için ücretsiz geçici bir lisans yeterlidir; üretim için ticari lisans gereklidir.
- **Düşük kaliteli taramalarda doğruluğu artırabilir miyim?** Evet—spell‑correction'ı etkinleştirin ve özel bir sözlük sağlayın.
- **Çok sayfalı destek yerleşik mi?** Her sayfa görüntüsünü bir döngüde işleyin; motor eşzamanlı yürütme için thread‑safe'dir.

## 'how to perform OCR' nedir?
**how to perform OCR** ifadesi, bir görüntüdeki basılı veya el yazısı metni, optik karakter tanıma teknolojisi kullanarak düzenlenebilir, aranabilir dijital karakterlere dönüştürme sürecini ifade eder. Aspose OCR, 20'den fazla raster formatı ve 50+ dili destekleyen tek‑geçiş motoru ile bu süreci uygular.

## Neden Aspose OCR for Java Kullanmalı?
Aspose OCR **20+ görüntü formatını** (PNG, JPEG, TIFF, BMP ve GIF dahil) destekler ve tüm belgeyi belleğe yüklemeden **çok yüz‑sayfalı toplu işleme** yapabilir; tipik bir 4‑çekirdek sunucuda **dakikada 300 sayfa** işleyebilir. Yerleşik yazım‑düzeltme ve özel sözlük özellikleri, gürültülü faturalar üzerindeki tipik OCR hata oranını %12'den %2'nin altına düşürür.

## Önkoşullar
- **Java Development Kit (JDK) 8+** – standart Java çalışma zamanı.
- **Aspose OCR for Java** kütüphanesi – en son JAR'ı Maven Central'dan veya Aspose indirme portalından edinin.
- İşlemek istediğiniz bir görüntü dosyası (ör. `invoice.png`).
- (Opsiyonel) `custom_dict.txt` – alan‑spesifik kelimeleri satır satır içeren UTF‑8 metin dosyası.

Bunlar yeterli; harici hizmetler veya ağır çerçeveler gerekmez.

## Java'da Görüntüde OCR Nasıl Yapılır?
Görüntünüzü yükleyin, yazım‑düzeltmeyi etkinleştirin, isteğe bağlı olarak özel bir sözlük sağlayın, motoru çalıştırın ve sonucu okuyun. Bu yaklaşım tek‑sayfalı dosyalar ve toplu işleme için de çalışır; motor görüntü kod çözümlemesini, dil algılamayı ve güven puanı hesaplamayı otomatik olarak yönetir, güvenilir bir metin çıktısı sağlar. Aşağıdaki bölümler her adımı net açıklamalar ve kopyalamanız gereken tam kod ile açıklar.

### Adım 1: Projeyi kurun ve bağımlılıkları içe aktarın

Aspose OCR Maven bağımlılığını `pom.xml` dosyanıza ekleyin. Bu tek satır çekirdek OCR motorunu ve tüm gerekli geçişli kütüphaneleri getirir.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

> **Pro tip:** Maven Central'daki sürüm numarasını kontrol edin; yeni sürümler dil paketleri ve performans iyileştirmeleri ekler.

### Adım 2: OCR için görüntüyü yükleyin

`OcrEngine` herhangi bir `InputStream` ile çalışır. Dosya yolu, bayt dizisi veya URL'yi sarmak için `ImageStream` kullanın.

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 2: Load the image you wish to process
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));
```

**Definition anchor:** `ImageStream` Aspose OCR’nin hafif sarmalayıcısıdır; görüntü verisini çeşitli kaynaklardan okur ve önce bir `BufferedImage`'a dönüştürmez.

### Adım 3: Spell‑correction'ı etkinleştirin (opsiyonel ama güçlü)

Yaygın OCR hatalarını otomatik olarak düzeltmek için yerleşik spell‑correction bayrağını açın; örneğin “l” ile “1” arasındaki karışıklıkları giderir.

```java
        // Step 3: Turn on spell‑checking to improve result quality
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);
```

Spell‑correction, düşük kontrastlı taramalarda doğruluğu **%80**'e kadar artırabilir, “Inv0ice” kelimesini ekstra kod olmadan “Invoice” hâline getirir.

### Adım 4: Özel bir sözlük sağlayın (motoru özelleştirin)

Sektöre özgü terminoloji (medikal kodlar, yasal terimler, ürün SKU'ları vb.) için düz metin sözlüğü ekleyin.

```java
        // Step 4: Load a custom dictionary to boost recognition of domain terms
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));
```

**Definition anchor:** `CustomDictionary` OCR motorunun post‑processing aşamasında tercih edeceği kelimeleri içeren UTF‑8 kelime listesini yükler.

### Adım 5: OCR sürecini çalıştırın

`process()` metodunu çağırarak tanınan metin, güven puanları ve isteğe bağlı yerleşim verilerini içeren bir `OcrResult` elde edin.

```java
        // Step 5: Execute OCR and capture the result
        OcrResult ocrResult = ocrEngine.process();
```

Bir hata oluşursa, `ocrResult.getErrorMessage()` ayrıntılı açıklamayı döndürür; bunu kaydedebilir veya ekranda gösterebilirsiniz.

### Adım 6: Tanınan (ve düzeltilen) metni çıktı olarak verin

Çıkarılan dizeyi konsola yazdırın veya bir dosyaya kaydedin. Hızlı test için basit bir `System.out.println` yeterlidir.

```java
        // Step 6: Print the corrected text to the console
        System.out.println(ocrResult.getText());
    }
}
```

Programı çalıştırdığınızda aşağıdaki gibi temiz, aranabilir bir metin elde etmelisiniz:

```
Invoice Number: 12345
Date: 2023‑07‑15
Total Amount: $1,250.00
```

Gereksiz karakterler görürseniz, özel sözlüğünüzü gözden geçirin ve görüntüyü ön‑işleme (kontrast artırma, gürültü azaltma veya gri tonlamaya çevirme) yapmayı düşünün.

## Özel bir sözlük kullanarak görüntüden metin nasıl çıkarılır?
Sözlüğü işlemden önce yükleyin, ardından `ocrEngine.setCustomDictionary(customDict)` çağrısını yapın. Motor, listedeki kelimelere öncelik verir; bu sayede teknik belgelerde “O” harfi ile “0” rakamı arasındaki karışıklıklar gibi hatalar büyük ölçüde azalır.

## Java OCR Maven bağımlılığı doğru şekilde nasıl eklenir?
`pom.xml` dosyanızın `<dependencies>` bölümü içine aşağıdaki snippet'i ekleyin. Bu bağımlılık, çekirdek Aspose OCR kütüphanesini ve gereken tüm geçişli bileşenleri getirir; böylece OCR motorunu ek konfigürasyon olmadan başlatabilirsiniz. Dosyayı güncelledikten sonra `mvn clean install` komutunu çalıştırarak Maven'in en yeni sürümü indirdiğinden emin olun.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

## Yaygın sorular ve uç durumlar

### Görüntü farklı bir formatta (PDF, TIFF, vb.) ise ne olur?
Aspose OCR raster formatlarını doğrudan işler. PDF'ler için önce her sayfayı görüntüye dönüştürün—Aspose PDF for Java `PdfExtractor` ile bunu verimli bir şekilde yapabilirsiniz. Bir `BufferedImage` ya da bayt akışı elde ettiğinizde aynı `setImage` çağrısı çalışır. Bu yöntem, tüm PDF'i belleğe yüklemeden çok sayfalı belgeleri hızlı ve ölçeklenebilir şekilde işlemeyi sağlar.

### Çok sayfalı belgeler nasıl işlenir?
Her sayfa görüntüsü için bir döngüde yeni bir `OcrEngine` (veya mevcut olanı sıfırla) oluşturun ve `OcrResult.getText()` değerlerini birleştirin. Bu yaklaşım, sayfa başına bağımsız yazım‑denetimi bağlamı sağlar. Sayfaları sıralı ya da paralel iş parçacıklarında işleyerek yüksek verim elde ederken aynı sözlük ve yazım‑düzeltme ayarlarından faydalanabilirsiniz.

### Dil veya karakter kümesini sınırlayabilir miyim?
Evet. `ocrEngine.getEngineOptions().setLanguage(Language.English)` (veya desteklenen başka bir dil) çağrısı ile tanıma kapsamını daraltabilirsiniz; bu, işleme süresini **%30**'a kadar hızlandırır. Dil sınırlaması, motorun dikkate alması gereken karakter setini azaltır, belirsizliği düşürür ve özellikle yalnızca Latin karakterli belgelerde hız ve doğruluğu artırır.

### Büyük toplu işlemlerde performans nasıl?
Motor, yalnızca okuma işlemleri için thread‑safe'dir. Bir iş parçacığı havuzu oluşturup her görüntüyü kendi `OcrEngine` örneğine atayın. 4‑çekirdek bir makinede paralel yürütme ile **≈250 sayfa/dakika** elde edilebilir. Yüksek çözünürlüklü binlerce görüntü işlerken yeterli heap belleği ayırdığınızdan ve CPU kullanımını izlediğinizden emin olun.

## Daha İyi Doğruluk İçin İpuçları

- **Görüntüyü ön‑işleme:** OCR'dan önce kontrastı artırın, bir medyan filtresi uygulayın veya gri tonlamaya çevirin.
- **300 dpi veya daha yüksek taramalar kullanın;** düşük çözünürlükler hata oranını dramatik şekilde artırır.
- **Özel sözlüğü odaklı tutun:** Alakasız kelimeler yazım‑denetleyiciyi şaşırtabilir.
- **Regex ile post‑processing:** Tarih, sayı veya kimlik numaralarını çıkarımdan sonra doğrulayarak kalan anormallikleri yakalayın.

## Sonraki Adımlar

Artık **how to perform OCR** ve **how to extract text from image** konularını öğrendiğinize göre şunları keşfedebilirsiniz:

- OCR çıktısını gizli bir metin katmanı içeren aranabilir bir PDF olarak kaydetmek.
- Çıkarılan fatura verilerini doğrudan ilişkisel bir veritabanına depolamak.
- El yazısı notları daha da temizlemek için makine‑öğrenimi modelleri uygulamak.
- Kullanıcı‑yüklediği fotoğraflar için OCR iş akışını bir RESTful web servisi olarak sunmak.

Bu uzantıların her biri, yukarıda kapsanan temel adımlara dayanır; geçişin sorunsuz olacağını göreceksiniz.

---

**Son Güncelleme:** 2026-09-23  
**Test Edilen:** Aspose OCR 24.12 for Java  
**Yazar:** Aspose  



## Sık Sorulan Sorular

**Q: Aspose OCR internet bağlantısı gerektiriyor mu?**  
A: Hayır. Kütüphane tamamen çevrim dışı çalışır; tüm tanıma işlemleri JVM'nizde yerel olarak gerçekleşir.

**Q: Hangi Java sürümleri destekleniyor?**  
A: Aspose OCR, Java 8'den Java 21'e kadar, hem standart hem de OpenJDK dağıtımlarını destekler.

**Q: 10 MB'den büyük görüntüleri işleyebilir miyim?**  
A: Evet. Motor veri akışı yapar ve 500 MB'ye kadar (sadece mevcut heap belleği sınırlaması) görüntüyü işleyebilir.

**Q: Aspose OCR'yi üretim ortamında nasıl lisanslarım?**  
A: Aspose mağazasından ticari bir lisans satın alın ve lisans dosyasını `License license = new License(); license.setLicense("Aspose.OCR.lic");` kodu ile ayarlayın.

**Q: El yazısı metin için yerleşik destek var mı?**  
A: Aspose OCR, `ocrEngine.getEngineOptions().setHandwriting(true);` ile etkinleştirilebilen bir el‑yazısı moduna sahiptir; bu, el yazısı betimlemelerde doğruluğu artırır.

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you wish to process
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));

        // Step 3: Enable spell‑checking for the OCR result
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);

        // Step 4: Provide a custom dictionary (one word per line)
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));

        // Step 5: Run the OCR process
        OcrResult ocrResult = ocrEngine.process();

        // Step 6: Output the recognized (and corrected) text
        System.out.println(ocrResult.getText());
    }
}
```

## İlgili Öğreticiler

- [Görüntüde OCR Yapma – Aspose OCR Java Adım Adım Kılavuzu](/ocr/java/advanced-ocr-techniques/perform-ocr-on-image-with-aspose-ocr-java-step-by-step-guide/)
- [Java'da Görüntü OCR Ön‑İşleme – Doğruluğu Artırma ve Metin Çıkarma](/ocr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)
- [Java'da OCR için GPU Nasıl Etkinleştirilir – Görüntüden Metin Tanıma](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-recognize-text-from-image/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}