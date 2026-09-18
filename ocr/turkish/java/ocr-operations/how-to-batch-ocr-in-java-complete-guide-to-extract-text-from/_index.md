---
category: general
date: 2026-02-09
description: Aspose OCR ile Java’da toplu OCR nasıl yapılır öğrenin. Görüntülerden
  metin çıkarın, PNG, JPG ve TIFF dosyalarından tek bir çağrıda metin tanıyın.
draft: false
keywords:
- how to batch ocr
- extract text from images
- recognize text from png
- recognize text from jpg
- recognize text from tiff
language: tr
og_description: Java'da toplu OCR nasıl yapılır öğrenin. Bu öğreticide, Aspose OCR
  kullanarak PNG, JPG ve TIFF görüntülerinden metin çıkarmayı net kod örnekleriyle
  gösteriyoruz.
og_title: Java'da Toplu OCR Nasıl Yapılır – Görsellerden Metni Verimli Şekilde Çıkarın
tags:
- OCR
- Java
- Aspose
title: Java'da Toplu OCR Nasıl Yapılır – Görsellerden Metin Çıkarma İçin Tam Kılavuz
url: /tr/java/ocr-operations/how-to-batch-ocr-in-java-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da Toplu OCR Nasıl Yapılır – Görsellerden Metin Çıkarma İçin Tam Kılavuz

Her dosya için bir döngü yazmadan bir avuç resmi **toplu OCR** yapmanın nasıl olduğunu hiç merak ettiniz mi? Tek başınıza değilsiniz. Gerçek dünyadaki birçok projede bir klasör dolusu tarama alırsınız—PNG makbuzlar, JPG ekran görüntüleri veya hatta çok sayfalı TIFF'ler—ve metne hızlıca ihtiyacınız olur.  

İyi haber şu ki Aspose OCR tam da bunu yapmanıza izin veriyor: PNG, JPG ve TIFF dosyalarından metni aynı anda tanıyan tek bir metod çağrısı. Bu öğreticide projeyi kurmaktan sonuçları yazdırmaya kadar tüm süreci adım adım anlatacağız, böylece bugün görsellerden metin çıkarmaya başlayabilirsiniz.

## Bu Öğreticide Neler Ele Alınacak

* **Toplu OCR nasıl yapılır** Aspose'un `OcrBatchProcessor`ı kullanarak.
* Farklı formatlardaki (PNG, JPG, TIFF) **görüntülerden metin çıkarma** yolları.
* Uygulamanızın yanıt verebilirliğini korumak için paralellik kontrol ipuçları.
* Kopyala‑yapıştır yapıp hemen çalıştırabileceğiniz eksiksiz, çalıştırılabilir bir Java programı.

Aspose ile ilgili önceden bir deneyime ihtiyacınız yok—sadece temel bir Java kurulumu ve tercih ettiğiniz bir IDE yeterli. Sonunda, PNG, JPG ve TIFF dosyalarından toplu olarak metin tanıma konusunda sağlam bir temele sahip olacaksınız.

---

![Birden fazla görüntü dosyasını toplu OCR yapmayı gösteren diyagram](/images/batch-ocr-diagram.png "toplu ocr nasıl yapılır")

*Görsel alt metni: birden fazla görüntü dosyasının birlikte işlendiğini gösteren toplu ocr diyagramı.*

## Önkoşullar

| Gereksinim | Neden önemli |
|-------------|----------------|
| Java 17 veya daha yeni | Aspose OCR modern JVM'leri hedefler. |
| Maven veya Gradle | Aspose OCR kütüphanesini eklemeyi basitleştirir. |
| Temel Java bilgisi | Kod akışını anlamak için gereklidir. |
| Örnek görüntü seti (`.png`, `.jpg`, `.tif`) | Çıkarma işlemini canlı görmek için. |

Eğer bunlara zaten sahipseniz, harika—hadi başlayalım.

## Adım 1: Projenize Aspose OCR'ı Ekleyin

İhtiyacınız olan ilk şey Aspose OCR JAR dosyasıdır. Maven ile bunu `pom.xml` dosyanıza ekleyin:

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

Bağımlılığı eklemek, **png'den metin tanıma**, **jpg'den metin tanıma** ve **tiff'den metin tanıma** için gereken her şeyi getirir. Ek native kütüphanelere ihtiyaç yok.

## Adım 2: İşlemek İstediğiniz Görüntü Dosyalarını Tanımlayın

Şimdi OCR motoruna hangi dosyaları işleyeceğini söyleyeceğiz. İşte **toplu OCR nasıl yapılır**ın gerçekten parladığı yer—sadece bir yol listesi verin ve kütüphane ağır işi yapsın.

```java
import java.util.Arrays;
import java.util.List;

// Step 2: List your image files (PNG, JPG, TIFF)
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/img1.png",   // PNG file – recognize text from png
        "YOUR_DIRECTORY/img2.jpg",   // JPG file – recognize text from jpg
        "YOUR_DIRECTORY/img3.tif");  // TIFF file – recognize text from tiff
```

> **Pro ipucu:** Dosya yollarınızı mutlak tutun veya farklı işletim sistemlerinde sürpriz yaşamamak için `Paths.get(...)` kullanın.

## Adım 3: Toplu İşlemciyi Oluşturun ve Paralelliği Ayarlayın

Aspose OCR, paralel olarak birden fazla tanıma çalıştırabilen `OcrBatchProcessor` ile birlikte gelir. İş parçacığı sayısını kontrol etmek, onlarca görüntü olduğunda uygulamanızın CPU'yu aşırı kullanmasını önler.

```java
import com.aspose.ocr.OcrBatchProcessor;

// Step 3: Initialise the batch processor
OcrBatchProcessor ocrProcessor = new OcrBatchProcessor();

// Limit to 4 concurrent threads – a sweet spot for most desktops
ocrProcessor.setMaxParallelism(4);
```

Neden paralelliği sınırlamalısınız? Orta seviye bir dizüstü bilgisayarda çok fazla iş parçacığı çalıştırırsanız, hızlanma yerine yavaşlama görebilirsiniz. `setMaxParallelism` ayarı, hız ve istikrarı dengelemenizi sağlar.

## Adım 4: Toplu OCR Çağrısını Çalıştırın

İşte **toplu OCR nasıl yapılır**ın özü: her görüntü için bir `RecognitionResult` nesnesi döndüren tek bir `recognize` çağrısı.

```java
import com.aspose.ocr.RecognitionResult;
import java.util.List;

// Step 4: Execute batch OCR
List<RecognitionResult> recognitionResults = ocrProcessor.recognize(imageFiles);
```

Metod, tüm görüntüler işlenene kadar bloklanır, ardından metni size verir. Eğer bloklamayan bir davranışa ihtiyacınız varsa, bunu bir `CompletableFuture` içinde sarabilirsiniz, ancak çoğu betik için senkron çağrı kodu düzenli tutar.

## Adım 5: Çıkarılan Metni Yazdırın

Son olarak, sonuçlar üzerinde döngü kurarak tanınan dizeleri gösterin. Bu, çeşitli formatlardaki **görüntülerden metin çıkarma** işlemini başarıyla gerçekleştirdiğimizi gösterir.

```java
// Step 5: Output the recognized text for each file
for (int i = 0; i < recognitionResults.size(); i++) {
    System.out.println("File: " + imageFiles.get(i));
    System.out.println(recognitionResults.get(i).getText());
    System.out.println("---");
}
```

### Beklenen Çıktı

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

OCR motoru bir dosyayı okuyamazsa, `getText()` metodu boş bir string döndürür, bu yüzden uyarı kaydetmek için basit bir kontrol ekleyebilirsiniz.

## Tam Çalışan Örnek

Her şeyi bir araya getirerek, eksiksiz, çalıştırmaya hazır Java sınıfını burada bulabilirsiniz. `BatchOcrTutorial.java` adlı bir dosyaya kopyalayın, görüntü yollarını ayarlayın ve `javac && java` komutlarıyla çalıştırın.

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

Çalıştırın, ve konsolda her PNG, JPG ve TIFF dosyası için çıkarılan metni göreceksiniz—zihninizde **toplu OCR nasıl yapılır** sorusu olduğunda tam da ihtiyacınız olan şey.

## Yaygın Sorular ve Kenar Durumları

### Üçten fazla görüntüm olsaydı ne olur?

`imageFiles` listesine daha fazla giriş ekleyin. Toplu işlemci, `setMaxParallelism` ile yapılandırdığınız iş parçacıkları arasında işi otomatik olarak bölüştürür.

### Görüntülerim bir alt klasörde—her birini manuel olarak listelemem gerekir mi?

Belirli bir uzantıya sahip tüm dosyaları programatik olarak toplayabilirsiniz:

```java
try (Stream<Path> paths = Files.walk(Paths.get("YOUR_DIRECTORY"))) {
    List<String> imageFiles = paths
        .filter(Files::isRegularFile)
        .filter(p -> p.toString().matches(".*\\.(png|jpg|tif|tiff)$"))
        .map(Path::toString)
        .collect(Collectors.toList());
}
```

Bu, kodu esnek tutar ve hâlâ **toplu OCR nasıl yapılır** ilkesine saygı gösterir.

### Düşük güvenilirlik sonuçlarını nasıl ele alırım?

`RecognitionResult` bir `getConfidence()` metodu sağlar. Bir eşik değerinin altındaki sonuçları filtreleyebilir ve daha yüksek DPI ayarlarıyla yeniden deneyebilirsiniz:

```java
ocrProcessor.setResolution(300); // increase DPI for better accuracy
```

### Aspose OCR diğer dilleri destekliyor mu?

Evet—`recognize` çağrısından önce `ocrProcessor.setLanguage(OcrLanguage.Spanish)` (veya desteklenen herhangi bir enum) çağırmanız yeterlidir. Bu, İngilizcenin ötesinde kullanışlılığı genişletir ve **görüntülerden metin çıkarma** işlemini gerçekten çok dilli hâle getirir.

## Performans İpuçları

* **Batch size matters** – Daha büyük batch'ler overhead'i azaltır, ancak çok büyük listeler daha fazla bellek tüketebilir. 50–200 görüntüyle batch test edin.
* **Parallelism** – 4 çekirdekli bir CPU'da `setMaxParallelism(4)` genellikle en iyi verimi verir. Sunucunuzun iş yüküne göre ayarlayın.
* **Image preprocessing** – OCR'den önce görüntüleri gri tonlamaya dönüştürmek veya kontrastı artırmak, özellikle gürültülü taramalarda doğruluğu artırabilir.

## Sonuç

Artık Aspose OCR kullanarak Java'da **toplu OCR nasıl yapılır**ı, çeşitli formatlardaki **görüntülerden metin çıkarma** yöntemlerini ve paralelliği kontrol etmenin neden önemli olduğunu biliyorsunuz. Eksiksiz kod örneği, PNG, JPG ve TIFF dosyalarından tek bir verimli çağrıyla metin tanıma işlemini gösteriyor.

Bir sonraki adım için hazırsınız? OCR çıktısını bir arama indeksine, bir veritabanına ya da hatta bir AI özetleyiciye beslemeyi deneyin. PDF girişiyle (Aspose OCR bunu destekler) deney yapabilir ya da OpenCV gibi görüntü‑ön işleme kütüphaneleriyle birleştirerek doğruluğu daha da artırabilirsiniz.

Kodlamaktan keyif alın ve unutmayın—toplu OCR bir baş ağrısı olmak zorunda değil. Doğru araçlar ve net bir desenle, bir anda yığınla resmi aranabilir metne dönüştürebilirsiniz.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}