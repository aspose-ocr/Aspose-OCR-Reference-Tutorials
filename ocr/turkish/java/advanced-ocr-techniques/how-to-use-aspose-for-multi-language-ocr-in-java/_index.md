---
category: general
date: 2026-10-24
description: Aspose OCR'i Java'da kullanarak görüntüden metin çıkarmayı öğrenin; İngilizce,
  Ukraynaca ve Arapça dilleri desteklenir. OCR için görüntüyü yükleme ve OCR'ı çalıştırma
  adım adım rehberi.
draft: false
keywords:
- extract text from image
- load image for ocr
- run ocr on image
- Aspose OCR Java
- multi language OCR
lastmod: 2026-10-24
og_description: Aspose OCR'i Java'da kullanarak görüntüden metin çıkarmayı öğrenin;
  İngilizce, Ukraynaca ve Arapça dilleri desteklenir. OCR için görüntüyü yükleme ve
  OCR'ı çalıştırma adımları.
og_image_alt: 'Developer guide: extract text from image using Aspose OCR in Java'
og_title: Java'da Aspose OCR ile görüntüden metin çıkarma
schemas:
- author: Aspose
  dateModified: '2026-10-24'
  description: Learn how to extract text from image using Aspose OCR in Java, supporting
    English, Ukrainian and Arabic. Step‑by‑step guide to load image for OCR and run
    OCR on image.
  headline: How to extract text from image with Aspose OCR in Java
  type: TechArticle
- questions:
  - answer: No, a single Aspose OCR license covers all bundled language packs.
    question: Do I need a separate license for each language pack?
  - answer: The only practical limit is memory; Aspose processes each image sequentially,
      so you can add hundreds of files without issue.
    question: Is there a limit on the number of images I can add to `OcrInput`?
  - answer: The engine analyses each text block independently, so it can switch languages
      mid‑line and still produce accurate results.
    question: How does auto‑detection handle mixed scripts on the same line?
  - answer: Yes, `OcrResult` provides a `getConfidence()` method for granular quality
      metrics.
    question: Can I get confidence scores for each recognized word?
  - answer: Aspose OCR works with Java 8 through Java 21, including LTS releases.
    question: What Java versions are supported?
  type: FAQPage
tags:
- Aspose
- OCR
- Java
- extract text from image
- multi language OCR
title: Java'da Aspose OCR ile görüntüden metin çıkarma
url: /tr/java/advanced-ocr-techniques/how-to-use-aspose-for-multi-language-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da Aspose OCR ile görselden metin çıkarma

Eğer İngilizce, Ukraynaca ve Arapça karakterlerin karışımını içeren **görselden metin çıkarma** dosyalarına ihtiyacınız varsa, Aspose OCR bunu basit hale getirir. Bu öğreticide, **OCR için görsel yükleme**, *çok‑dilli OCR* etkinleştirme ve sonunda **görselde OCR çalıştırma** yoluyla temiz, okunabilir metin elde etmeyi gösteren tam, çalıştırmaya hazır bir örnek göreceksiniz. Adımlar sade bir dille açıklanmıştır, böylece *ne* yapmanız gerektiğini ve *neden* önemli olduğunu anlarsınız.

## Hızlı cevaplar
- **Kodun ilk satırı nedir?** `OcrEngine engine = new OcrEngine();`
- **Yerleşik olarak hangi diller desteklenir?** İngilizce (`en`), Ukraynaca (`uk`), Arapça (`ar`) ve 27 ek dil.
- **Test için lisansa ihtiyacım var mı?** Hayır, ücretsiz deneme çalışır, ancak lisans filigranı kaldırır.
- **Birden fazla görseli aynı anda işleyebilir miyim?** Evet, `recognize` çağırmadan önce birkaç dosya eklemek için `OcrInput` kullanın.
- **Hangi Java sürümü gereklidir?** Java 8 veya daha yenisi.

## Aspose OCR ile Java'da görselden metin çıkarma nasıl yapılır?

Görselinizi `OcrInput` ile yükleyin, gerekli diller için `OcrEngine`'i yapılandırın ve `engine.recognize(input)` metodunu çağırın. Motor, dil bloklarını otomatik olarak algılar, doğru OCR modelini uygular ve tanınan metni içeren bir `OcrResult` döndürür. Bu tek adımlı akış, 10 000 × 10 000 piksele kadar herhangi bir görsel boyutu için çalışır ve 30'dan fazla dil paketini destekler.

## Öğrenecekleriniz

- Aspose OCR kütüphanesini bir Java projesine (Maven veya Gradle) ekleyin.  
- OCR motorunu doğru şekilde başlatın.  
- Motoru *çok‑dilli OCR* için yapılandırın ve otomatik algılamayı etkinleştirin.  
- Karışık betik içeren bir görsel yükleyin.  
- Tanıma işlemini yürütün ve **görselden metin çıkarın**.  
- Desteklenmeyen diller veya eksik dosyalar gibi yaygın tuzakları yönetin.

Sonunda, herhangi bir projeye ekleyebileceğiniz ve görselleri anında işlemeye başlayabileceğiniz bağımsız bir Java sınıfına sahip olacaksınız.

## Önkoşullar

| Gereksinim | Neden önemli |
|------------|--------------|
| Java 8 veya yenisi | Aspose OCR, Java 8+ hedefler. |
| Maven veya Gradle (herhangi bir yapı aracı) | Aspose OCR JAR dosyasını otomatik olarak çeker. |
| Karışık‑dilli metin içeren bir görsel dosyası (ör. `mixed_script.jpg`) | Bu, **OCR için görsel yükleyeceğimiz** şeydir. |
| Geçerli bir Aspose OCR lisansı (isteğe bağlı) | Lisans olmadan su işareti eklenmiş bir çıktı alırsınız, ancak kod aynı şekilde çalışır. |

Hepsini anladınız mı? Harika—başlayalım.

## Adım 1: Projeye Aspose OCR ekleyin

### Maven

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- latest as of Feb 2026 -->
</dependency>
```

### Gradle

```groovy
// build.gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

> **İpucu:** Aspose OCR, 30'dan fazla dil paketini destekler ve tüm dosyayı belleğe yüklemeden 10 000 × 10 000 piksele kadar görselleri işleyebilir, böylece yüksek çözünürlüklü taramaları verimli bir şekilde yönetebilirsiniz.

Bağımlılığı eklemek, **Aspose nasıl kullanılır** konundaki ilk somut adımdır—kütüphane, daha sonra ihtiyaç duyacağımız `OcrEngine`, `OcrInput` ve `OcrResult` sınıflarını getirir.

## Adım 2: OCR motorunu başlatın

`OcrEngine` sınıfı, tanıma sürecini gerçekleştiren Aspose OCR'ın temel bileşenidir.  

```java
import com.aspose.ocr.*;

public class MultiLangOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2.1: Create the OCR engine – the core object that does all the heavy lifting.
        OcrEngine engine = new OcrEngine();

        // Step 2.2: (Optional) Apply your license to avoid watermarks.
        // engine.setLicense("Aspose.Total.lic");
```

**Neden önemli:**  
Motor başlatmayı atlayarsanız, daha sonra *görselde OCR çalıştırma* için bir şey kalmaz ve bir `NullPointerException` ile karşılaşırsınız.

## Adım 3: Çok‑dilli desteği ve otomatik algılamayı yapılandırın

`OcrEngine`, hangi dil modellerinin yükleneceğini belirtmek için `setRecognitionLanguages` metodunu ve metin bloğu başına otomatik dil algılamayı etkinleştiren `setAutoDetectLanguage` metodunu sağlar.  

```java
        // Step 3.1: Tell the engine which languages you expect.
        engine.setRecognitionLanguages(new String[] { "en", "uk", "ar" });

        // Step 3.2: Enable automatic language detection – crucial for mixed‑script images.
        engine.setAutoDetectLanguage(true);
```

**Açıklama:**  
- `"en"` = İngilizce, `"uk"` = Ukraynaca, `"ar"` = Arapça.  
- Otomatik algılama, Aspose'un görseli taramasını, her segmentin hangi dile ait olduğunu belirlemesini ve doğru OCR modelini uygulamasını sağlar. Onsuz üç ayrı tanıma çalıştırmanız gerekir—zor ve hata yapmaya meyillidir.

## Adım 4: OCR için görseli yükleyin

`OcrInput`, işleme için bir veya daha fazla görsel akışı tutan Aspose OCR konteyneridir.  

```java
        // Step 4.1: Prepare an OcrInput container.
        OcrInput input = new OcrInput();

        // Step 4.2: Add the image file. Replace the path with your actual location.
        input.add("YOUR_DIRECTORY/mixed_script.jpg");
```

> **Neden `OcrInput` kullanıyoruz:** Birden fazla sayfa veya görsel tutabilir, böylece daha sonra toplu modda **OCR için görsel yükleme** esnekliğini sağlar. Dosya bulunamazsa, Aspose bir `FileNotFoundException` fırlatır. Hızlı bir kontrol (`if (!new File(path).exists())`) hata ayıklama süresini tasarruf eder.

## Adım 5: Görselde OCR çalıştırın

`recognize` metodu resmi analiz eder, dil bloklarını algılar ve tanınan metni içeren bir `OcrResult` nesnesi üretir.  

```java
        // Step 5.1: Execute the recognition process.
        OcrResult result = engine.recognize(input);
```

## Adım 6: Görselden metin çıkarın ve görüntüleyin

`OcrResult`, satır sonları ve güven skorları dahil olmak üzere nihai metin çıktısını kapsar.  

```java
        // Step 6.1: Pull the plain text out of the result.
        String extractedText = result.getText();

        // Step 6.2: Print it to the console – you could also write it to a file.
        System.out.println("=== Extracted Text ===");
        System.out.println(extractedText);
    }
}
```

**Gördükleriniz:**  
`mixed_script.jpg` “Hello мир مرحبا” içeriyorsa, konsol çıktısı şu şekilde olacaktır:

```
=== Extracted Text ===
Hello мир مرحبا
```

Bu, **Aspose nasıl kullanılır** konusunda **görselden metin çıkarma** için çoklu dillerle tam çözümdür.

## Kenar durumları ve sık sorulan sorular

### Bir dil tanınmazsa ne olur?

Aspose, yalnızca OCR modelleriyle gelen dilleri destekler. Japonca eklemek için `setRecognitionLanguages` içinde `"ja"` ekleyin. Model mevcut değilse, motor varsayılan (İngilizce) modele geri döner ve bozuk karakterler alırsınız.

### Düşük çözünürlüklü görsellerde doğruluğu nasıl artırabilirsiniz?

`setResolution`, motorun girdi görseli için varsaydığı DPI değerini ayarlar, bu da düşük çözünürlüklü taramalara yardımcı olur.  
`setPreprocessOptions`, OCR öncesi otomatik döndürme gibi ön işleme eylemlerini seçer.

- Görseli ön‑işlemden geçirin (DPI artırın, ikilileştirme uygulayın).  
- Motorun beklenen DPI'yi bilmesi için `engine.setResolution(300)` kullanın.  
- Döndürülmüş taramalar için `engine.setPreprocessOptions(OcrEngine.PreprocessOptions.AutoRotate)` etkinleştirin.

### Bir klasördeki görselleri işleyebilir miyim?

Kesinlikle. `input.add()` çağrısını, bir dizindeki tüm dosyalar üzerinde dönen bir döngüye sarın. Aynı `engine.recognize(input)` çağrısı, her sayfa için birleştirilmiş metni döndürecektir.

## Tam çalışan örnek (kopyala‑yapıştır hazır)

```java
import com.aspose.ocr.*;

public class MultiLangOcrDemo {
    public static void main(String[] args) throws Exception {

        // Create the OCR engine
        OcrEngine engine = new OcrEngine();

        // Optional: apply your license to avoid watermarks
        // engine.setLicense("Aspose.Total.lic");

        // Configure languages (English, Ukrainian, Arabic) and enable auto‑detect
        engine.setRecognitionLanguages(new String[] { "en", "uk", "ar" });
        engine.setAutoDetectLanguage(true);

        // Load the image that contains mixed‑language text
        OcrInput input = new OcrInput();
        input.add("YOUR_DIRECTORY/mixed_script.jpg"); // <-- replace with your path

        // Run the recognition process
        OcrResult result = engine.recognize(input);

        // Print the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

Bunu `MultiLangOcrDemo.java` olarak kaydedin, `javac` ile derleyin ve `java MultiLangOcrDemo` ile çalıştırın. Her şey doğru ayarlandıysa, tanınan metnin konsola yazdırıldığını göreceksiniz.

## Sıkça Sorulan Sorular

**S: Her dil paketi için ayrı bir lisansa ihtiyacım var mı?**  
C: Hayır, tek bir Aspose OCR lisansı tüm paketlenmiş dil paketlerini kapsar.

**S: `OcrInput`'a ekleyebileceğim görsel sayısında bir sınırlama var mı?**  
C: Tek pratik sınırlama bellek; Aspose her görseli sırasıyla işler, bu yüzden sorunsuzca yüzlerce dosya ekleyebilirsiniz.

**S: Otomatik algılama aynı satırdaki karışık betikleri nasıl yönetir?**  
C: Motor, her metin bloğunu bağımsız olarak analiz eder, bu yüzden satır ortasında dilleri değiştirebilir ve hâlâ doğru sonuçlar üretebilir.

**S: Tanınan her kelime için güven skorları alabilir miyim?**  
C: Evet, `OcrResult` ayrıntılı kalite ölçütleri için bir `getConfidence()` metodu sunar.

**S: Hangi Java sürümleri destekleniyor?**  
C: Aspose OCR, Java 8'den Java 21'e kadar, LTS sürümleri dahil, çalışır.

## Sonuç

**Aspose nasıl kullanılır** konusunu baştan sona ele aldık: kütüphaneyi eklemekten, *çok‑dilli OCR* yapılandırmaya, **OCR için görsel yükleme**, **görselde OCR çalıştırma** ve sonunda **görselden metin çıkarma** adımlarına kadar. Yaklaşım ölçeklenebilir—daha fazla dil kodu ekleyin veya bir dosya listesi sağlayın, ve dakikalar içinde sağlam bir OCR hattına sahip olacaksınız.

Sırada ne var? Şu fikirleri deneyin:

- **Toplu işleme:** Bir dizin üzerinde döngü kurun ve her sonucu ayrı bir `.txt` dosyasına yazın.  
- **Son‑işleme:** Çıktıyı temizlemek için regex veya NLP kütüphanelerini kullanın (gereksiz satır sonlarını kaldırın, yaygın OCR hatalarını düzeltin).  
- **Entegrasyon:** OCR adımını bir Spring Boot REST uç noktası aracılığıyla sunun, böylece diğer hizmetler görselleri gönderip JSON‑kodlu metin alabilir.

Denemekten, hatalar yapmaktan ve ardından düzeltmekten çekinmeyin—bu, Aspose ile OCR konusunda gerçekten uzmanlaşmanın yoludur. Herhangi bir sorunla karşılaşırsanız, aşağıya yorum bırakın. Kodlamanın tadını çıkarın!  

---

![aspose OCR kullanımını gösteren ekran görüntüsü](/images/aspose-ocr-demo.png){alt="aspose OCR örneği Java kodunu gösteriyor"}

[aspose OCR kullanımını gösteren ekran görüntüsü](/images/aspose-ocr-demo.png)

**Son Güncelleme:** 2026-10-24  
**Test Edilen Versiyon:** Aspose OCR 24.11 for Java  
**Yazar:** Aspose

## İlgili Öğreticiler

- [Java'da OCR için Görsel Yükleme Adım Adım Kılavuzu](/ocr/java/ocr-operations/load-image-for-ocr-in-java-step-by-step-guide/)
- [Java OCR'da Otomatik Dil Algılama Adım Adım Kılavuzu](/ocr/java/advanced-ocr-techniques/automatic-language-detection-in-java-ocr-step-by-step-guide/)
- [Java'da OCR için GPU'yu Etkinleştirme ve Görselden Metin Çıkarma](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}