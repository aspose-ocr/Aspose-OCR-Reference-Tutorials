---
category: general
date: 2026-09-18
description: Aspose OCR kullanarak Java'da görüntülerden metin nasıl çıkarılacağını
  öğrenin. PNG, JPG ve TIFF dosyalarını tek bir çağrıda verimli bir şekilde toplu
  işleyin.
keywords:
- extract text from images
- convert images to text
- how to batch ocr
- extract text from png
- extract text from jpg
- extract text from tiff
lastmod: 2026-09-18
og_description: Java'da toplu OCR ile görüntülerden metin çıkarma konusunda uzmanlaşın.
  Aspose OCR'yi kullanarak PNG, JPG ve TIFF dosyalarını tek bir çağrıda dönüştürün.
og_image_alt: Diagram showing multiple image files processed together for batch OCR
og_title: Java'da görüntülerden metin çıkarma – toplu OCR rehberi
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to extract text from images in Java using Aspose OCR. Batch
    process PNG, JPG, and TIFF files efficiently in a single call.
  headline: How to extract text from images in Java by batch OCR
  type: TechArticle
- questions:
  - answer: Yes, Aspose OCR is pure Java and requires no UI components, so it works
      perfectly on headless environments.
    question: Can I run this on a headless server?
  - answer: A commercial license is needed for production deployments; a free trial
      is available for evaluation.
    question: Is a license required for production use?
  - answer: Any OS that can run Java 17+, including Windows, Linux, and macOS.
    question: Which operating systems are supported?
  - answer: Over 60 languages are supported out of the box, ranging from English and
      Spanish to Arabic and Chinese.
    question: How many languages can Aspose OCR recognise?
  - answer: Individual image files up to 200 MB are supported; larger files should
      be split before processing.
    question: What is the maximum file size Aspose OCR can handle?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: Java'da toplu OCR ile görüntülerden metin çıkarma
url: /tr/java/ocr-operations/how-to-batch-ocr-in-java-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntülerden Metin Çıkarma Java'da Toplu OCR ile

Eğer **görüntülerden metin çıkarmak** istiyor ve her dosya için döngü yazmadan hızlı bir çözüm arıyorsanız, toplu OCR cevaptır. Birçok gerçek dünya projesinde PNG makbuzlar, JPG ekran görüntüleri veya çok sayfalı TIFF'ler gibi tarama dosyalarıyla dolu bir klasör alırsınız ve bunları aranabilir metne dönüştürmeniz gerekir. Aspose OCR, PNG, JPG ve TIFF dosyalarını birlikte işleyen tek bir yöntem çağrısı ile bunu tam olarak yapmanızı sağlar, geliştirme süresini ve CPU döngülerini tasarruf ettirir.

## Hızlı Yanıtlar
- **Toplu OCR ne yapar?** Tek bir istekte birden fazla görüntü dosyasını işler ve her dosya için metin döndürür.
- **Hangi formatlar desteklenir?** PNG, JPG/JPEG ve çok sayfalı TIFF kutudan çıktığı gibi işlenir.
- **Ayrı bir yerel kütüphane gerekir mi?** Hayır, Aspose OCR JAR'ı ihtiyacınız olan her şeyi içerir.
- **Kaç iş parçacığının çalışacağını kontrol edebilir miyim?** Evet, toplu işlemci üzerinde `setMaxParallelism` kullanın.
- **Hangi Java sürümü gerekiyor?** Java 17 veya daha yenisi.

## Aspose OCR Nedir?
Aspose OCR, dış bağımlılıklar olmadan görüntü dosyalarındaki basılı ve el yazısı metni tanıyan bir Java kütüphanesidir. 60'tan fazla dili destekler ve toplu başına 100 görüntü işleyebilir, bu da büyük ölçekli belge dijitalleştirme için idealdir.

## Bu öğreticide neler ele alınacak
Görüntü yollarının bir listesini yükleyin, bir `OcrBatchProcessor` oluşturun, paralelliği ayarlayın, tek bir `recognize` çağrısı çalıştırın ve çıkarılan dizeleri yazdırın. Sonunda, PNG, JPG ve TIFF dosyalarından toplu olarak metin çıkaran, çalıştırmaya hazır bir Java programına sahip olacaksınız.

- **Toplu OCR nasıl yapılır** Aspose'in `OcrBatchProcessor`'ı kullanarak.
- Farklı formatlardaki (PNG, JPG, TIFF) **görüntülerden metin çıkarma** yolları.
- Uygulamanızın yanıt verebilirliğini korumak için paralelliği kontrol etme ipuçları.
- Kopyalayıp yapıştırıp hemen çalıştırabileceğiniz tam, çalıştırılabilir bir Java programı.

Aspose ile ilgili önceden bir deneyim gerekmiyor—sadece temel bir Java kurulumu ve tercih ettiğiniz bir IDE yeterli. Sonunda, PNG, JPG ve TIFF dosyalarından toplu olarak metin tanıma konusunda sağlam bir temele sahip olacaksınız.

---

![Birden fazla görüntü dosyasını toplu OCR ile işleme diyagramı](/images/batch-ocr-diagram.png "toplu ocr nasıl yapılır")

*Görsel alt metni: toplu ocr diyagramı, birden fazla görüntü dosyasının birlikte işlendiğini gösterir.*

## Önkoşullar

| Requirement | Why it matters |
|-------------|----------------|
| Java 17 or newer | Aspose OCR modern JVM'leri hedefler. |
| Maven or Gradle | Aspose OCR kütüphanesini eklemeyi basitleştirir. |
| Basic Java knowledge | Kod akışını anlamak için gereklidir. |
| A set of sample images (`.png`, `.jpg`, `.tif`) | Çıkarma işlemini canlı görmek için. |

Eğer bunlara sahipseniz, harika—hadi başlayalım.

## Adım 1: Aspose OCR'yi projenize ekleyin

İlk olarak ihtiyacınız olan Aspose OCR JAR'ıdır. Maven ile bunu `pom.xml` dosyanıza ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

Gradle tercih ediyorsanız, eşdeğeri şudur:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

Bağımlılığı eklemek, **png'den metin çıkarma**, **jpg'den metin çıkarma** ve **tiff'den metin çıkarma** için gereken her şeyi getirir. Ek yerel kütüphanelere ihtiyaç yoktur.

## Adım 2: İşlemek istediğiniz görüntü dosyalarını tanımlayın

Şimdi OCR motoruna hangi dosyaları işleyeceğini söyleyeceğiz. İşte **toplu OCR nasıl yapılır** gerçekten parladığı yer—sadece bir yol listesi geçin ve kütüphane ağır işi yapsın.

```java
import java.util.Arrays;
import java.util.List;

// Step 2: List your image files (PNG, JPG, TIFF)
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/img1.png",   // PNG file – recognize text from png
        "YOUR_DIRECTORY/img2.jpg",   // JPG file – recognize text from jpg
        "YOUR_DIRECTORY/img3.tif");  // TIFF file – recognize text from tiff
```

> **Pro ipucu:** Dosya yollarınızı mutlak tutun veya farklı işletim sistemlerinde sürprizlerden kaçınmak için `Paths.get(...)` kullanın.

## Adım 3: Toplu işlemciyi oluşturun ve paralelliği ayarlayın

Aspose OCR, paralel olarak birkaç tanıma çalıştırabilen `OcrBatchProcessor` ile birlikte gelir. İş parçacığı sayısını kontrol etmek, onlarca görüntünüz olduğunda uygulamanızın CPU'yu aşırı kullanmasını önler.

```java
import com.aspose.ocr.OcrBatchProcessor;

// Step 3: Initialise the batch processor
OcrBatchProcessor ocrProcessor = new OcrBatchProcessor();

// Limit to 4 concurrent threads – a sweet spot for most desktops
ocrProcessor.setMaxParallelism(4);
```

Neden paralelliği sınırlamalısınız? Mütevazı bir dizüstü bilgisayarda çok fazla iş parçacığı çalıştırırsanız, hızlanma yerine yavaşlama görebilirsiniz. `setMaxParallelism` ayarlamak, hız ve kararlılığı dengelemenizi sağlar.

## Adım 4: Toplu OCR çağrısını çalıştırın

İşte **toplu OCR nasıl yapılır**'ın özü: her görüntü için bir `RecognitionResult` nesnesi döndüren tek bir `recognize` çağrısı.  
`recognize` sağlanan görüntüleri işler ve çıkarılan metni içeren `RecognitionResult` nesnelerinin bir listesini döndürür.

```java
import com.aspose.ocr.RecognitionResult;
import java.util.List;

// Step 4: Execute batch OCR
List<RecognitionResult> recognitionResults = ocrProcessor.recognize(imageFiles);
```

Metod, tüm görüntüler işlenene kadar bloklanır, ardından size metni verir. Eğer bloklamayan bir davranışa ihtiyacınız varsa, bunu bir `CompletableFuture` içinde sarabilirsiniz, ancak çoğu betik için senkron çağrı kodu düzenli tutar.

## Adım 5: Çıkarılan metni yazdırın

Son olarak, sonuçlar üzerinde döngü kurun ve tanınan dizeleri gösterin. Bu, çeşitli formatlardaki **görüntülerden metin çıkarma** işlemini başarıyla gerçekleştirdiğimizi gösterir.  
`RecognitionResult`, çıkarılan metin ve güven puanı dahil olmak üzere tek bir görüntünün OCR çıktısını tutar.

```java
// Step 5: Output the recognized text for each file
for (int i = 0; i < recognitionResults.size(); i++) {
    System.out.println("File: " + imageFiles.get(i));
    System.out.println(recognitionResults.get(i).getText());
    System.out.println("---");
}
```

### Beklenen çıktı

```
File: YOUR_DIRECTORY/img1.png
The quick brown fox jumps over the lazy dog.
---
File: YOUR_DIRECTORY/img2.jpg
Invoice #12345
Total: $567.89
---
File: YOUR_DIRECTORY/img3.tif
Page 1 of 3
Report generated on 2026-02-09
---
```

OCR motoru bir dosyayı okuyamazsa, `getText()` metodu boş bir dize döndürür, bu yüzden uyarı kaydetmek için basit bir kontrol ekleyebilirsiniz.

## Tam Çalışan Örnek

Her şeyi bir araya getirerek, işte tam, çalıştırmaya hazır Java sınıfı. `BatchOcrTutorial.java` adlı bir dosyaya kopyalayın, görüntü yollarını ayarlayın ve `javac && java` komutlarını çalıştırın.

```java
import com.aspose.ocr.*;
import java.util.Arrays;
import java.util.List;

public class BatchOcrTutorial {
    public static void main(String[] args) throws Exception {

        // Step 1: Define the image files to be processed
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/img1.png",
                "YOUR_DIRECTORY/img2.jpg",
                "YOUR_DIRECTORY/img3.tif");

        // Step 2: Create the batch OCR processor and optionally limit parallelism
        OcrBatchProcessor ocrProcessor = new OcrBatchProcessor();
        ocrProcessor.setMaxParallelism(4); // limit to 4 concurrent threads

        // Step 3: Perform OCR on all images in a single batch call
        List<RecognitionResult> recognitionResults = ocrProcessor.recognize(imageFiles);

        // Step 4: Output the recognized text for each file
        for (int i = 0; i < recognitionResults.size(); i++) {
            System.out.println("File: " + imageFiles.get(i));
            System.out.println(recognitionResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

Çalıştırın, ve konsolda her PNG, JPG ve TIFF dosyası için çıkarılan metni göreceksiniz—aklınızda **toplu OCR nasıl yapılır** sorusu olduğunda tam olarak ihtiyacınız olan şey.

## Yaygın Sorular ve Kenar Durumları

### Üçten fazla görüntüm olursa ne olur?
Sadece `imageFiles` listesine daha fazla giriş ekleyin. Toplu işlemci, `setMaxParallelism` ile yapılandırdığınız iş parçacıkları arasında işi otomatik olarak bölüştürür.

### Görüntülerim bir alt klasörde—her birini manuel olarak listelemem gerekir mi?
`Files.list` bir dizindeki yolların tembel doldurulmuş bir akışını döndürür.

```java
try (Stream<Path> paths = Files.walk(Paths.get("YOUR_DIRECTORY"))) {
    List<String> imageFiles = paths
        .filter(Files::isRegularFile)
        .filter(p -> p.toString().matches(".*\\.(png|jpg|tif|tiff)$"))
        .map(Path::toString)
        .collect(Collectors.toList());
}
```

Bu, kodu esnek tutar ve hâlâ **toplu OCR nasıl yapılır**'ı saygı gösterir.

### Düşük güvenilirlik sonuçlarını nasıl ele alırım?
`getConfidence()` tanınan metnin ne kadar doğru olabileceğini gösteren sayısal bir güven değeri döndürür.

```java
ocrProcessor.setResolution(300); // increase DPI for better accuracy
```

### Aspose OCR diğer dilleri destekliyor mu?
Evet—`recognize` çağrısından önce `ocrProcessor.setLanguage(OcrLanguage.Spanish)` (veya desteklenen herhangi bir enum) çağırın. Bu, işlevi İngilizce'nin ötesine genişletir ve **görüntülerden metin çıkarma** işlemini gerçekten çok dilli yapar.

## Performans İpuçları

* **Toplu boyut önemlidir** – Daha büyük toplular ek yükü azaltır, ancak çok büyük listeler daha fazla bellek tüketebilir. 50–200 görüntü başına toplu ile test edin.
* **Paralellik** – 4 çekirdekli bir CPU'da, `setMaxParallelism(4)` genellikle en iyi verimi verir. Sunucunuzun iş yüküne göre ayarlayın.
* **Görüntü ön işleme** – OCR'den önce görüntüleri gri tonlamaya dönüştürmek veya kontrastı artırmak, özellikle gürültülü taramalarda doğruluğu artırabilir.

## Sonuç

Artık Aspose OCR kullanarak Java'da **toplu OCR nasıl yapılır**, çeşitli formatlardaki **görüntülerden metin nasıl çıkarılır** ve paralelliği kontrol etmenin neden önemli olduğunu biliyorsunuz. Tam kod örneği, PNG, JPG ve TIFF dosyalarından tek, verimli bir çağrıyla metin tanımayı gösteriyor.

Bir sonraki adım için hazır mısınız? OCR çıktısını bir arama indeksine, veritabanına veya bir AI özetleyiciye besleyin. PDF girişiyle (Aspose OCR bunu destekler) deney yapabilir veya OpenCV gibi görüntü ön işleme kütüphaneleriyle birleştirerek daha yüksek doğruluk elde edebilirsiniz.

Kodlamaktan keyif alın ve unutmayın—toplu OCR bir baş ağrısı olmak zorunda değil. Doğru araçlar ve net bir desenle, resim yığınlarını kısa sürede aranabilir metne dönüştüreceksiniz.

## Sıkça Sorulan Sorular

**S: Bunu başsız bir sunucuda çalıştırabilir miyim?**  
C: Evet, Aspose OCR saf Java'dır ve UI bileşenlerine ihtiyaç duymaz, bu yüzden başsız ortamlarda mükemmel çalışır.

**S: Üretim kullanımında lisans gerekli mi?**  
C: Üretim dağıtımları için ticari bir lisans gerekir; değerlendirme için ücretsiz deneme mevcuttur.

**S: Hangi işletim sistemleri destekleniyor?**  
C: Java 17+ çalıştırabilen herhangi bir OS, Windows, Linux ve macOS dahil.

**S: Aspose OCR kaç dili tanıyabilir?**  
C: Kutudan çıktığı gibi 60'tan fazla dil desteklenir, İngilizce ve İspanyolca'dan Arapça ve Çince'ye kadar.

**S: Aspose OCR'nin işleyebileceği maksimum dosya boyutu nedir?**  
C: Tek tek görüntü dosyaları 200 MB'a kadar desteklenir; daha büyük dosyalar işlenmeden önce bölünmelidir.

---

**Son Güncelleme:** 2026-09-18  
**Test Edilen Versiyon:** Aspose OCR 24.9 for Java  
**Yazar:** Aspose

## İlgili Öğreticiler

- [Görüntülerden Metin Çıkarma – Java için OCR Temelleri](/ocr/java/ocr-basics/)
- [Java'da Toplu OCR Nasıl Yapılır – Metin Çıkarma İçin Tam Kılavuz](/ocr/java/ocr-operations/how-to-batch-ocr-in-java-complete-guide-to-extract-text-from/)
- [Java'da Görüntü Ön İşleme OCR – Doğruluğu Artırma ve Metin Çıkarma](/ocr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}