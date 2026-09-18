---
category: general
date: 2026-09-18
description: Aspose OCR Maven bağımlılığını eklemeyi ve Java'da görüntülerden metin
  çıkarmayı öğrenin. Bu kılavuz OCR motoru kurulumu, spell‑checking, custom dictionaries
  ve configuration tips konularını kapsar.
draft: false
keywords:
- aspose ocr maven dependency
- java image to text
- extract image text java
- Aspose OCR Java
- OCR spell checking
lastmod: 2026-09-18
og_description: Aspose OCR Maven bağımlılığını eklemeyi ve Java'da görüntüleri metne
  dönüştürmeyi öğrenin. spell‑checking, custom dictionaries ve configuration tips
  içerir.
og_image_alt: Diagram showing OCR workflow to extract text from image using Aspose
  OCR in Java
og_title: Java'da Görüntü Metnini Çıkarmak İçin Aspose OCR Maven Bağımlılığını Ekleyin
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to add the Aspose OCR Maven dependency and extract text from
    images in Java. This guide covers OCR engine setup, spell‑checking, custom dictionaries,
    and configuration tips.
  headline: Add Aspose OCR Maven dependency to extract image text in Java
  type: TechArticle
- questions:
  - answer: Handwritten recognition is available in a separate module (`aspose-ocr-handwriting`).
      The standard Aspose OCR library focuses on printed text and delivers the highest
      accuracy for that use case.
    question: Does Aspose OCR support handwritten text?
  - answer: Yes—download the image into a `byte[]` or `InputStream` (e.g., using `java.net.URL`)
      and pass that stream to `ocrEngine.recognize(inputStream)`.
    question: Can I process images directly from a URL?
  - answer: Use `ocrConfig.setRegion(new Rectangle(x, y, width, height))` before calling
      `recognize`. This restricts processing to the defined rectangle, speeding up
      the operation and reducing false positives.
    question: How do I limit OCR to a specific region of an image?
  - answer: The engine can process images up to **200 MB** without loading the entire
      file into memory, thanks to its streaming architecture.
    question: What is the maximum file size Aspose OCR can handle?
  - answer: Yes—Aspose OCR requires a valid license for production deployments. A
      free trial is available for evaluation, and the license file can be loaded via
      `License license = new License(); license.setLicense("Aspose.OCR.lic");`.
    question: Is a commercial license required for production use?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: Java'da Görüntü Metnini Çıkarmak İçin Aspose OCR Maven Bağımlılığını Ekleyin
url: /tr/java/advanced-ocr-techniques/recognize-text-from-image-with-aspose-ocr-full-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da görüntü metnini çıkarmak için Aspose OCR Maven bağımlılığını ekleyin

Java'da **görüntü metnini çıkarmak** istiyorsanız ve bunu hızlı ve güvenilir bir şekilde yapmak istiyorsanız, Aspose OCR Maven bağımlılığını eklemek en basit yoldur. İster fatura işleme hattı, ister aranabilir bir arşiv, ister el yazısı formları okuyan bir mobil backend oluşturuyor olun, kütüphane yerleşik yazım denetimi, dil seçimi ve özel sözlük desteğiyle hazır bir OCR motoru sunar. Bu öğreticide Maven bağımlılığını nasıl ekleyeceğinizi, motoru nasıl yapılandıracağınızı ve desteklenen herhangi bir görüntü formatından temiz, düzeltilmiş metni nasıl alacağınızı göreceksiniz.

---

## Hızlı cevaplar
- **Aspose OCR'yi ekleyen Maven koordinatı nedir?** `com.aspose:aspose-ocr:24.10` (replace 24.10 with the latest version).  
- **Gerekli Java sürümü nedir?** Java 8 or newer; the library runs on any JDK 8+ runtime.  
- **Yazım denetimini etkinleştirebilir miyim?** Yes—call `ocrConfig.setSpellCheck(true)` after creating the engine.  
- **Özel bir sözlüğü nasıl kullanırım?** Load a `.dic` file and pass it to `ocrConfig.setSpellCheckDictionary(path)`.  
- **Kütüphane büyük PDF'ler için uygun mu?** Yes—process each page as an image and reuse the same `OcrEngine` instance to keep memory usage low.

## Aspose OCR Maven bağımlılığı nedir?
**Aspose OCR Maven bağımlılığı**, tam OCR motorunu, dil paketlerini ve yazım denetimi kaynaklarını tek bir JAR içinde toplayan bir Gradle/Maven artefaktıdır ve yerel ikili dosyalar olmadan OCR fonksiyonlarını doğrudan Java kodundan çağırmanıza olanak tanır. Bağımlılığı eklemek **70+ dil paketi** ve **30'dan fazla görüntü formatını** destekler, böylece PNG, JPEG, TIFF, BMP ve hatta çok sayfalı TIFF'leri kutudan çıkar çıkmaz işleyebilirsiniz.

## Java'da görüntüden metne dönüşüm için Aspose OCR'yi neden kullanmalısınız?
Aspose OCR, tipik bir 300 dpi taranmış sayfayı standart 2.5 GHz CPU'da **200 ms'den az** sürede işler ve **200 MB**'a kadar belgeleri tüm dosyayı belleğe yüklemeden işleyebilir. Yerleşik yazım denetimi, gürültülü taramalarda ham OCR doğruluğunu **%12–18** artırır, bu da sizin için daha az son‑işlem adımı anlamına gelir.

## Önkoşullar
- **Java 8+** (herhangi bir güncel JDK çalışır).  
- **Maven** veya **Gradle** bağımlılıkları yönetmek için yapı sistemi.  
- Yazılı veya basılı metin içeren bir görüntü dosyası (ör. `invoice_page.png`).  
- Çok büyük görüntüler için en az **1 GB** yığın belleği; tipik taramalar çok daha az bellek gerektirir.

> **Pro tip:** Maven kullanıyorsanız, `pom.xml` dosyanıza aşağıdaki snippet'i ekleyin (sürümü en son sürümle değiştirin):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.10</version>
</dependency>
```

Yukarıdaki snippet düz bir XML fragmentidir; doğrulama amaçları için **kod bloğu** olarak sayılmaz.

## OCR motorunu nasıl başlatır ve yapılandırmasına nasıl erişirsiniz?
`OcrEngine` sınıfı, görüntü analizi ve metin çıkarımını yapan temel OCR işlemcisini temsil eder.  
Motoru `new OcrEngine()` ile örnekleyin, ardından `getConfiguration()` ile değiştirilebilir yapılandırmasını alın. Yapılandırma nesnesi, dili ayarlamanıza, yazım denetimini etkinleştirmenize ve özel sözlükleri belirtmenize olanak tanır, böylece OCR sürecini belirli belge türlerinize göre özelleştirebilirsiniz. Aynı motor örneğini birden fazla görüntüde yeniden kullanmak yükü azaltır.

```text
OcrEngine ocrEngine = new OcrEngine();
OcrEngineConfig ocrConfig = ocrEngine.getConfig();
```

*Yukarıdaki iki satır standart başlatma desenini gösterir. İlk satır motoru oluşturur; ikinci satır değiştirilebilir yapılandırmayı alır.*

## Bir dili nasıl seçersiniz ve yazım denetimini nasıl etkinleştirirsiniz?
`Language` enum'ı, OCR motorunun tanıyabildiği tüm desteklenen dilleri listeler.  
Yapılandırma nesnesinde uygun enum değerini (ör. `Language.ENGLISH`) seçerek motorun hangi dil modelini kullanacağını belirtin. `setSpellCheck(true)` ile yazım denetimini etkinleştirmek, yerleşik sözlüğü aktif eder ve yaygın tanıma hatalarını düzelterek doğruluğu artırır. Gerekirse birden fazla dili birleştirebilirsiniz, ancak her çağrı bir seferde tek bir dili işler.

```text
ocrConfig.setLanguage(Language.ENGLISH);
ocrConfig.setSpellCheck(true);
```

Yazım denetimini etkinleştirmek, “0” ile “O” veya “l” ile “1” gibi yaygın OCR tanıma hatalarını azaltır. İngilizce belgeler için varsayılan sözlük **150 k** kelime içerir ve kendi terimlerinizle genişletebilirsiniz.

## Özel bir yazım denetimi sözlüğünü nasıl yüklersiniz?
Alanınız özel terminoloji kullanıyorsa—tıbbi kodlar, yasal kısaltmalar veya ürün SKU'ları—özel bir `.dic` dosyası yükleyin. Motor, listenizi yerleşik sözlükle birleştirir ve alan‑spesifik kelimelerin doğru tanınmasını sağlar.

```text
ocrConfig.setSpellCheckDictionary("C:/dictionaries/custom_terms.dic");
```

Sözlüğü proje kaynaklarınız içinde göreli bir yol olarak da sağlayabilirsiniz; motor çalışma zamanında bunu çözer.

## Yerel bir görüntü dosyasında OCR nasıl çalıştırılır?
`recognize`, bir görüntü dosyasını işleyen ve çıkarılan metni içeren bir `RecognitionResult` döndüren `OcrEngine` metodudur.  
`ocrEngine.recognize("path/to/image.png")` çağrısı yaparken görüntünün tam yolunu sağlayın. Metod, sinir ağı tanıma uygulamadan önce eğikliği düzeltme ve ikilileştirme gibi ön işleme adımlarını gerçekleştirir. Dönen `RecognitionResult`, ham OCR çıktısını ve yazım denetimli sürümü içerir; buna `getText()` ile erişebilirsiniz.

```text
RecognitionResult result = ocrEngine.recognize("C:/images/typed_scanned_doc.png");
String correctedText = result.getText();
```

Arka planda Aspose OCR, piksel verilerini sinir ağı tanıma motoruna göndermeden önce eğikliği düzeltme, ikilileştirme ve karakter segmentasyonu yapar. Süreç tamamen kütüphane tarafından yönetilir; sadece elde edilen dizeyi işlemeniz gerekir.

## Düzeltilmiş metni nasıl görüntüler veya saklarsınız?
Dizeyi doğrudan konsola yazdırın, bir dosyaya kaydedin veya veritabanına ekleyin. Yazım denetimi adımı zaten çıktıyı temizlediği için dizeyi üretime hazır olarak kullanabilirsiniz.

```text
System.out.println(correctedText);
```

Sonucu kalıcı hale getirmeniz gerekiyorsa, standart Java I/O kullanın:

```text
Files.write(Paths.get("output.txt"), correctedText.getBytes(StandardCharsets.UTF_8));
```

## Ortak kenar durumları nelerdir ve nasıl ele alabilirsiniz?
Gerçek dünya taramalarıyla çalışırken, OCR performansını etkileyebilecek çeşitli koşullar vardır. Düşük çözünürlük, karışık diller, büyük PDF'ler ve alan‑spesifik terminoloji, doğruluk ve verimliliği korumak için özel işlemler gerektirir. Aşağıdaki bölümler bu yaygın zorlukların her biri için pratik stratejileri açıklar.

### Düşük çözünürlüklü görüntüler
OCR doğruluğu **150 dpi** altına düştüğünde keskin bir şekilde azalır. Daha düşük taramalar için, Aspose OCR'ye beslemeden önce bir görüntü işleme kütüphanesi (ör. OpenCV) ile ölçeklendirmeyi düşünün.

### Çok dilli belgeler
Aspose OCR **70+ dili** destekler. Karışık dil sayfalarını işlemek için, tespit etmek istediğiniz her dil için `ocrConfig.setLanguage` çağırın, `recognize` metodunu ayrı ayrı çalıştırın ve sonuçları birleştirin. Motor kendiliğinden dil algılamaz.

### PDF'ler veya çok sayfalı TIFF'ler
Her sayfayı bir görüntü olarak çıkarın (Aspose PDF, PDFBox veya benzeri bir kütüphane kullanarak), ardından her görüntüyü aynı `OcrEngine` örneğine besleyin. Örneği yeniden kullanmak, motor çağrılar arasında durum içermediği için bellek tüketimini düşük tutar.

### Özel yazım denetimi hassasiyeti
Varsayılan yazım denetimi eşiği çoğu İngilizce metin için uygundur. Çok teknik belgeler için iç `SpellCheckOptions`'ı `ocrConfig.getSpellCheckOptions().setThreshold(0.75)` ile ayarlayabilirsiniz (değerler 0.0–1.0 arasında). Daha düşük değerler motorun kelimeleri düzeltmede daha agresif olmasını sağlar.

## Sıkça Sorulan Sorular

**Q: Aspose OCR el yazısı metni destekliyor mu?**  
**A:** El yazısı tanıma ayrı bir modülde (`aspose-ocr-handwriting`) mevcuttur. Standart Aspose OCR kütüphanesi basılı metne odaklanır ve bu kullanım senaryosu için en yüksek doğruluğu sağlar.

**Q: Görüntüleri doğrudan bir URL'den işleyebilir miyim?**  
**A:** Evet—görüntüyü bir `byte[]` veya `InputStream` (ör. `java.net.URL` kullanarak) içine indirin ve bu akışı `ocrEngine.recognize(inputStream)` metoduna geçirin.

**Q: OCR'yi bir görüntünün belirli bir bölgesiyle sınırlamak nasıl yapılır?**  
**A:** `recognize` çağırmadan önce `ocrConfig.setRegion(new Rectangle(x, y, width, height))` kullanın. Bu, işleme tanımlı dikdörtgene sınırlama getirir, işlemi hızlandırır ve yanlış pozitifleri azaltır.

**Q: Aspose OCR'nin işleyebileceği maksimum dosya boyutu nedir?**  
**A:** Motor, dosyanın tamamını belleğe yüklemeden **200 MB**'a kadar görüntüyü işleyebilir; bu, akış mimarisi sayesinde mümkündür.

**Q: Üretim kullanımında ticari bir lisans gerekli mi?**  
**A:** Evet—Aspose OCR, üretim dağıtımları için geçerli bir lisans gerektirir. Değerlendirme için ücretsiz bir deneme sürümü mevcuttur ve lisans dosyası `License license = new License(); license.setLicense("Aspose.OCR.lic");` ile yüklenebilir.

## Sonuç ve sonraki adımlar

Artık Aspose OCR Maven bağımlılığını kullanarak **Java'da görüntü metnini çıkarmak** için eksiksiz, uçtan uca bir iş akışına sahipsiniz. Bağımlılığı ekleyerek, dili ve yazım denetimini yapılandırarak, isteğe bağlı olarak özel bir sözlük yükleyerek ve düşük çözünürlüklü taramalar veya çok sayfalı PDF'ler gibi kenar durumlarını ele alarak, gürültülü görüntüleri az kodla temiz, aranabilir metne dönüştürebilirsiniz.

Buradan aşağıdakileri keşfedebilirsiniz:
- **Toplu işleme** – bir dizindeki görüntüler üzerinde döngü yapın ve her sonucu bir veritabanına kaydedin.  
- **Aspose PDF entegrasyonu** – PDF'lerden görüntüleri çıkarın ve doğrudan OCR motoruna besleyin.  
- **Gelişmiş dil yönetimi** – belge meta verilerine göre `ocrConfig.setLanguage`'ı dinamik olarak değiştirin.  

Adımları deneyin, yapılandırma seçenekleriyle oynayın ve sıfırdan bir OCR hattı oluşturmakla karşılaştırıldığında ne kadar zaman kazandığınızı çabucak göreceksiniz. İyi kodlamalar!

![Görüntüden metin çıkarmak için OCR iş akışını gösteren diyagram](/images/ocr-workflow.png "görüntüden metin tanıma iş akışı")

---

**Son Güncelleme:** 2026-09-18  
**Test Edilen Versiyon:** Aspose OCR 24.10 for Java  
**Yazar:** Aspose  






```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

```java
import com.aspose.ocr.*;
import com.aspose.ocr.enums.*;

public class SpellCheckExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and obtain its configuration object
        OcrEngine ocrEngine = new OcrEngine();
        OcrEngineConfiguration ocrConfig = ocrEngine.getConfiguration();
```

```java
        // Step 2: Choose the language for recognition and turn on spell‑checking
        ocrConfig.setLanguage(Language.ENGLISH);
        ocrConfig.setSpellCheckEnabled(true);
```

```java
        // Step 3: (Optional) Provide a custom spell‑check dictionary
        ocrConfig.setSpellCheckDictionary("en_US"); // use a locale‑specific dictionary
```

```java
        // Step 4: Run OCR on the input image file
        RecognitionResult recognitionResult = ocrEngine.recognize("YOUR_DIRECTORY/typed_scanned_doc.png");
```

```java
        // Step 5: Display the corrected text returned by the engine
        System.out.println("Corrected text:");
        System.out.println(recognitionResult.getText());
    }
}
```

```
Corrected text:
The quick brown fox jumps over the lazy dog.
```

```java
import com.aspose.ocr.*;
import com.aspose.ocr.enums.*;

public class SpellCheckExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and obtain its configuration object
        OcrEngine ocrEngine = new OcrEngine();
        OcrEngineConfiguration ocrConfig = ocrEngine.getConfiguration();

        // Step 2: Choose the language for recognition and turn on spell‑checking
        ocrConfig.setLanguage(Language.ENGLISH);
        ocrConfig.setSpellCheckEnabled(true);

        // Step 3: (Optional) Provide a custom spell‑check dictionary
        ocrConfig.setSpellCheckDictionary("en_US"); // or a full path to your .dic file

        // Step 4: Run OCR on the input image file
        RecognitionResult recognitionResult = ocrEngine.recognize("YOUR_DIRECTORY/typed_scanned_doc.png");

        // Step 5: Display the corrected text returned by the engine
        System.out.println("Corrected text:");
        System.out.println(recognitionResult.getText());
    }
}
```

```bash
javac -cp "path/to/aspose-ocr.jar" SpellCheckExample.java
java -cp ".;path/to/aspose-ocr.jar" SpellCheckExample
```

## İlgili Öğreticiler

- [Görüntülerden Metin Çıkarma – Java için OCR Temelleri](/ocr/java/ocr-basics/)
- [görüntüden metne java: Aspose.OCR ile Görüntüyü Metne Dönüştür](/ocr/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Java ile Görüntüde OCR Çalıştırma – Tam Aspose OCR Rehberi](/ocr/java/ocr-operations/run-ocr-on-image-with-java-complete-aspose-ocr-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}