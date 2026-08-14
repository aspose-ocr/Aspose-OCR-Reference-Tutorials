---
category: general
date: 2026-07-05
description: Aspose OCR kullanarak Java ile görüntüyü metne dönüştürün. Tarama, TIFF
  dosyaları ve akışlardan metni hızlı ve güvenilir bir şekilde nasıl çıkaracağınızı
  öğrenin.
draft: false
keywords:
- convert image to text
- extract text from scan
- extract text from tif
- recognize text from stream
- how to ocr stream
language: tr
og_description: Aspose OCR ile Java’da görüntüyü metne dönüştürün. Bu kılavuz, tarama,
  TIFF dosyaları ve akışlardan metin çıkarmayı, kurulumdan çıktıya kadar her adımı
  kapsayacak şekilde gösterir.
og_title: Java’da Görüntüyü Metne Dönüştür – Aspose OCR Tam Kılavuzu
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Convert image to text with Java using Aspose OCR. Learn how to extract
    text from scan, TIFF files, and streams quickly and reliably.
  headline: Convert Image to Text in Java Using Aspose OCR – Full Guide
  type: TechArticle
tags:
- Java
- OCR
- Aspose
title: Aspose OCR Kullanarak Java'da Görüntüyü Metne Dönüştürme – Tam Kılavuz
url: /tr/java/ocr-operations/convert-image-to-text-in-java-using-aspose-ocr-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da Aspose OCR Kullanarak Görüntüyü Metne Dönüştürme – Tam Kılavuz

Hiç **görüntüyü metne dönüştürme** işlemini düşük seviyeli görüntü işleme hileleriyle uğraşmadan nasıl yapabileceğinizi merak ettiniz mi? Yalnız değilsiniz. Birçok geliştirici, özellikle kaynak bir dosya yolu yerine bir akıştan geldiğinde, tarama dosyalarından veya büyük TIFF belgelerinden metin çıkarmak zorunda kaldığında bir duvara çarpar.

Bu öğreticide, **tarama** görüntülerinden metin çıkaran, **tif** dosyalarından metin çıkarma işlemini yöneten ve Aspose OCR Java kütüphanesini kullanarak **akıştan OCR** nasıl yapılacağını tam olarak gösteren pratik, uçtan uca bir çözümü adım adım inceleyeceğiz. Sonunda, tanınan metni doğrudan konsola yazdıran yeniden kullanılabilir bir kod parçacığına sahip olacaksınız.

## Gereksinimler

- **Java Development Kit (JDK) 8 veya daha yeni** – kod, herhangi bir yeni JDK üzerinde çalışır.
- **Maven veya Gradle** (favori yapı aracınız) Aspose OCR bağımlılığını çekmek için.
- Bir görüntü dosyası – tercihen test etmek istediğiniz çok sayfalı **TIFF** (`large_image.tif`).
- Biraz sabır (şaka yapıyorum – adımlar oldukça hızlı).

Eğer bunlardan biri size yabancı geliyorsa endişelenmeyin. İlk adımda Maven kurulumunu ele alacağız ve geri kalan tamamen Java.

## Adım 1: Aspose OCR'ı Projenize Ekleyin

İlk engel, OCR motorunu sınıf yolunuza (classpath) eklemektir. Aspose, kütüphanelerini Maven Central'da yayınlar, bu yüzden tek bir bağımlılık ekleyebilirsiniz.

```xml
<!-- pom.xml -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.9</version> <!-- Use the latest stable version -->
    </dependency>
</dependencies>
```

> **Pro ipucu:** Gradle kullanıyorsanız eşdeğeri  
> `implementation 'com.aspose:aspose-ocr:23.9'`.  
> Bu küçük ek, `OcrEngine`, `RecognitionResult` ve motorun arka planda yaptığı tüm ağır işleri kullanmanıza olanak tanır.

## Adım 2: OCR Motorunu Başlatın

Kütüphane hazır olduğuna göre, `OcrEngine` bir örneği oluşturabiliriz. Motoru, **akıştan gelen metni tanıyan** bir beyin olarak düşünün.

```java
import com.aspose.ocr.OcrEngine;

// ...

// Step 2: Initialize the OCR engine – this is where the magic starts.
OcrEngine engine = new OcrEngine();
```

Motoru neden sadece bir kez örnekliyoruz? Aynı `OcrEngine` nesnesini birden fazla görüntüde yeniden kullanmak, özellikle bir grup taranmış sayfa işlenirken, ek yükü azaltır ve performansı artırır.

## Adım 3: Görüntünüzü Akış Olarak Açın

Çoğu gerçek dünya senaryosu, görüntüleri bir ağ konumundan, veritabanından veya yüklenmiş bir dosyadan okumayı içerir – bunların hepsi akış olarak ortaya çıkar. İşte **akıştan metni tanımanın** dosya sistemine doğrudan dokunmadan nasıl yapılacağı.

```java
import java.io.FileInputStream;
import java.io.InputStream;

// ...

// Step 3: Load the image (a TIFF in this case) as an InputStream.
try (InputStream imageStream = new FileInputStream("YOUR_DIRECTORY/large_image.tif")) {
    // The try‑with‑resources block ensures the stream closes automatically.
```

Kaynağınız bir `ByteArrayInputStream` veya bir servlet isteğinden gelen `InputStream` ise, sadece `FileInputStream` yapıcısını değiştirin – kodun geri kalanı aynı kalır.

## Adım 4: OCR'ı Gerçekleştirin ve Metni Çıkarın

Akış elinizde olduğunda, `engine.recognizeImage` metodunu çağırıyoruz. Bu metod, çıkarılan dizeyi tutan bir `RecognitionResult` nesnesi döndürür.

```java
import com.aspose.ocr.RecognitionResult;

// ...

    // Step 4: Recognize text from the image stream
    RecognitionResult ocrResult = engine.recognizeImage(imageStream);

    // Step 5: Print the extracted text to the console
    System.out.println("=== OCR Output ===");
    System.out.println(ocrResult.getText());
}
```

`recognizeImage` çağrısının tüm ağır işleri nasıl yaptığını fark edin: TIFF'i çözer, OCR motorunu çalıştırır ve düz metni döndürür. Bu, **görüntüyü metne dönüştürme** işlevinin çekirdeğidir.

## Adım 5: Çok Sayfalı TIFF'leri İşleme (İsteğe Bağlı)

TIFF'iniz birden fazla sayfa içeriyorsa, Aspose OCR otomatik olarak her sayfanın metnini birleştirir. Ancak, okunabilirlik için sayfaları ayırmak isteyebilirsiniz. İşte hızlı bir ayarlama:

```java
String fullText = ocrResult.getText();
String[] pages = fullText.split("\\f"); // Form feed character denotes page break

for (int i = 0; i < pages.length; i++) {
    System.out.println("--- Page " + (i + 1) + " ---");
    System.out.println(pages[i].trim());
}
```

Bu kod parçacığı, **tarama** belgelerinden sayfa sayfa metin çıkarır ve çıktıyı ince ayarlarla kontrol etmenizi sağlar.

## Tam Çalışan Örnek

Her şeyi bir araya getirerek, IDE'nize kopyalayabileceğiniz tam, çalıştırılabilir bir sınıf burada.

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.RecognitionResult;
import java.io.FileInputStream;
import java.io.InputStream;

public class StreamOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // Step 2: Open the image file as a stream
        try (InputStream imageStream = new FileInputStream("YOUR_DIRECTORY/large_image.tif")) {

            // Step 3: Recognize text from the image stream
            RecognitionResult ocrResult = engine.recognizeImage(imageStream);

            // Step 4: Print the extracted text
            System.out.println("=== OCR Output ===");
            System.out.println(ocrResult.getText());

            // Optional: Separate pages if it's a multi‑page TIFF
            String[] pages = ocrResult.getText().split("\\f");
            for (int i = 0; i < pages.length; i++) {
                System.out.println("--- Page " + (i + 1) + " ---");
                System.out.println(pages[i].trim());
            }
        }
    }
}
```

**Beklenen çıktı** (kısaltılmış olarak):

```
=== OCR Output ===
This is the first line of the scanned document.
Another line follows...
--- Page 1 ---
This is the first line of the scanned document.
...
```

Görüntü bulanıksa veya dil İngilizce değilse, `engine.setLanguage` ayarını değiştirebilir veya ön işleme seçeneklerini ayarlayabilirsiniz – ancak temel akış aynı kalır.

## Yaygın Tuzaklar ve Nasıl Kaçınılır

| Belirti | Muhtemel Neden | Çözüm |
|---------|----------------|-------|
| `ocrResult.getText()` üzerinde NullPointerException | Motor başlatılmadı veya görüntü akışı erken kapatıldı | `OcrEngine`'in akışı açmadan **önce** oluşturulduğundan emin olun ve `recognizeImage` döndürülene kadar akışı açık tutun. |
| Bozuk karakterler | Görüntü DPI'sı çok düşük (300'ün altında) | Daha yüksek çözünürlüklü bir kaynak kullanın veya Aspose'un görüntü iyileştirmesini etkinleştirin (`engine.getImagePreprocessingOptions().setDpi(300)`). |
| Çok sayfalı TIFF için çıktı yok | Sonuç doğru şekilde bölünmedi | Sayfaları ayırmak için yukarıda gösterildiği gibi `\\f` (form feed) kullanın. |
| Büyük dosyalarda `OutOfMemoryError` | Tüm dosyanın belleğe yüklenmesi | TIFF'i döngü içinde `engine.recognizeImage(pageStream)` kullanarak sayfa sayfa işleyin. |

## Bonus: Sonucu Bir Metin Dosyasına Dönüştürme

Eğer **görüntüyü metne dönüştürme** ve daha sonra kullanmak üzere saklama ihtiyacınız varsa, sadece birkaç satır ekleyin:

```java
import java.nio.file.Files;
import java.nio.file.Paths;

// ...

String outputPath = "output.txt";
Files.write(Paths.get(outputPath), ocrResult.getText().getBytes());
System.out.println("Text saved to " + outputPath);
```

Artık OCR çıktısının kalıcı bir kopyasına sahipsiniz, bu da sonraki işleme veya indekslemeye mükemmeldir.

## Sonuç

Aspose OCR kullanarak Java'da **görüntüyü metne dönüştürme** yöntemini yeni öğrendiniz; **tarama** dosyalarından **tif** görüntülerine kadar her şeyi kapsadınız ve **akıştan metni tanıma** tekniklerinde ustalaştınız. Tam örnek, bugün çalıştırmanız gereken adımları gösteriyor ve isteğe bağlı kod parçacıkları çok sayfalı belgeleri nasıl işleyeceğinizi veya sonuçları diske nasıl kaydedeceğinizi gösteriyor.

Sırada ne var? OCR motorunu PDF'lerle beslemeyi deneyin, dil ayarlarıyla oynayın veya çıktıyı bir arama indeksine entegre edin. Aynı desen, web yüklemelerinden, bulut depolamadan veya hatta bir mesaj kuyruğundan gelen **akıştan OCR** verileri için de çalışır.

Sorularınız mı var ya da işbirliği yapmayan zor bir görüntünüz mü var? Aşağıya bir yorum bırakın, iyi kodlamalar!

![Görüntü dosyasından → InputStream → OcrEngine → Metin çıktısına akış diyagramı – görüntüyü metne dönüştürme](https://example.com/convert-image-to-text-diagram.png "görüntüyü metne dönüştürme akış diyagramı")

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Java için Aspose.OCR ile tiff'ten metin çıkarma nasıl yapılır](/ocr/english/java/ocr-operations/recognize-tiff/)
- [Aspose.OCR BufferedImage kullanarak Java'da Görüntüyü Metne Dönüştürme](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Aspose.OCR Kullanarak Dil ile Görüntü Metnini OCR Yapma](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}