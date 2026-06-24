---
category: general
date: 2026-06-16
description: Aspose OCR'i Java'da kullanarak metin görüntüsünü hızlı bir şekilde tanıyın.
  GPU cihazını nasıl ayarlayacağınızı, JPG'den metin çıkartmayı ve GPU hızlandırmasıyla
  metin resmini okumayı öğrenin.
draft: false
keywords:
- recognize text image
- set gpu device
- extract text jpg
- how to recognize text
- read text picture
language: tr
og_description: Java'da Aspose OCR ile metin görüntüsünü tanıyın. Bu kılavuz, GPU
  cihazını nasıl ayarlayacağınızı, metin JPG'sini nasıl çıkaracağınızı ve metin resmini
  verimli bir şekilde nasıl okuyacağınızı gösterir.
og_title: Java'da Aspose OCR + GPU ile metin görüntüsü tanıma
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: recognize text image quickly with Aspose OCR in Java. Learn how to
    set gpu device, extract text jpg, and read text picture using GPU acceleration.
  headline: recognize text image in Java using Aspose OCR + GPU
  type: TechArticle
tags:
- OCR
- Java
- Aspose
- GPU
title: Java'da Aspose OCR + GPU ile metin görüntüsünü tanıma
url: /tr/java/advanced-ocr-techniques/recognize-text-image-in-java-using-aspose-ocr-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da Aspose OCR + GPU ile metin görüntüsü tanıma

CPU'nuzu durma noktasına getirmeden bir Java uygulamasında metin görüntüsü tanıma nasıl yapılır hiç merak ettiniz mi? Tek başınıza değilsiniz—geliştiriciler sürekli daha hızlı ve daha güvenilir OCR boru hatları peşinde. Bu öğreticide, JPG bir resimden anında metin çıkaran tam bir GPU‑hızlandırmalı çözümü adım adım inceleyeceğiz.

İlk olarak Aspose OCR'ı kuracağız, ardından GPU hızlandırmayı etkinleştireceğiz ve son olarak metin resim dosyalarını nasıl okuyacağınızı, sonuçları nasıl yazdıracağınızı ve ara sıra oluşabilecek hataları nasıl yöneteceğinizi göstereceğiz. Sonuna geldiğinizde **metin görüntüsü tanıma** konusunda, ister taranmış bir fatura ister sıradan bir ekran görüntüsü olsun, her türlü resimde metin tanıma yapabileceksiniz.

## Gereksinimler

- **Java 17** (veya herhangi bir güncel JDK) – kod tüm modern çalışma zamanlarında çalışır.  
- **Aspose.OCR for Java** – Maven Central üzerinden temin edilebilir.  
- CUDA desteği olan bir **GPU** (isteğe bağlı ancak hız için şiddetle tavsiye edilir).  
- İşlemek istediğiniz örnek JPEG resmi (ör. `sample.jpg`).  

Başka üçüncü‑taraf kütüphane gerekmez; geriye kalan her şey Aspose OCR ile paketlenmiştir.

## Adım 1: Aspose OCR'ı Projeye Ekleyin

Maven kullanıyorsanız aşağıdaki bağımlılığı `pom.xml` dosyanıza ekleyin. Gradle kullanıcıları eşdeğer `implementation` satırını kopyalayabilir.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check for the latest version -->
</dependency>
```

> **İpucu:** Ücretsiz deneme sürümü küçük bir filigran ekler. Üretim ortamı için Aspose portalından bir lisans alın ve herhangi bir OCR işleminden önce `License license = new License(); license.setLicense("Aspose.OCR.lic");` kodunu çalıştırın.

## Adım 2: İşlemek İstediğiniz Görüntüyü Yükleyin

**Metin görüntüsü tanıma** yapmak istediğinizde ilk adım resmi OCR motoruna beslemektir. Aspose, bir dosya yolu, bir `InputStream` veya hatta bir bayt dizisinden okuyabilen kullanışlı bir `ImageStream` sarmalayıcısı sunar.

```java
import com.aspose.ocr.*;

public class GpuOcrExample {
    public static void main(String[] args) throws Exception {
        // Load the image – replace the path with your own picture
        OcrEngine engine = new OcrEngine();
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

Kodun mümkün olduğunca sade tutulduğuna dikkat edin; `setImage` çağrısı JPEG, PNG ve BMP dahil Aspose tarafından desteklenen herhangi bir raster formatını kabul eder.

## Adım 3: GPU Hızlandırmayı Etkinleştirin (set gpu device)

Şimdi bu rehberi farklı kılan bölüme geliyoruz: OCR motorunun CPU yerine grafik kartında çalışması için **set gpu device** ayarlayacağız. Bu, özellikle yüksek çözünürlüklü görüntülerde işleme süresini saniyelerce kısaltabilir.

```java
        // Enable GPU acceleration – this is where the magic happens
        engine.getRecognitionSettings().setUseGpu(true);

        // Optional: pick a specific GPU if you have more than one
        // engine.getRecognitionSettings().setGpuDeviceId(0);
```

Birden fazla GPU'nuz varsa, `setGpuDeviceId` satırının yorumunu kaldırın ve `0` yerine tercih ettiğiniz cihazın indeksini yazın. Aspose, uyumlu bir GPU bulunamazsa otomatik olarak CPU'ya geçer, bu yüzden çökme konusunda endişelenmenize gerek yok.

## Adım 4: OCR İşlemini Gerçekleştirin – nasıl metin tanınır

Görüntü yüklendi ve GPU aktif olduğuna göre, artık resim üzerindeki **nasıl metin tanınır** sorusunu cevaplayabiliriz. `recognize()` metodu tüm boru hattını çalıştırır—ön‑işleme, segmentasyon, karakter sınıflandırması ve son‑işleme.

```java
        // Execute the OCR process
        OcrResult result = engine.recognize();
```

Dönen `OcrResult` nesnesi ham metin dizesini, güven skorlarını ve gerekirse daha sonra düzen bilgisi almak için sınırlama kutularını içerir.

## Adım 5: Tanınan Metni Çıktılayın – extract text jpg / read text picture

Basitçe sonucu konsola yazdırarak **extract text jpg** ve **read text picture** işlemini gerçekleştirelim. Gerçek bir uygulamada muhtemelen bu veriyi bir veritabanına veya dosyaya yazarsınız.

```java
        // Show the recognized text in the console
        System.out.println("Recognized text:");
        System.out.println(result.getText());
    }
}
```

Programı çalıştırdığınızda aşağıdakine benzer bir çıktı görmelisiniz:

```
Recognized text:
Invoice #12345
Date: 2026-06-15
Total: $1,250.00
```

Görüntü gürültülü ise Aspose'un ön‑işleme ayarlarını (kontrast, ikilileştirme vb.) ayarlayabilirsiniz—ancak varsayılan ayarlar çoğu temiz JPG dosyası için yeterlidir.

## Tam Çalışan Örnek

Her şeyi bir araya getirdiğimizde, işte tamamen çalıştırılabilir sınıf:

```java
import com.aspose.ocr.*;

public class GpuOcrExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the image to be processed
        OcrEngine engine = new OcrEngine();
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));

        // Step 2: Enable GPU acceleration for faster recognition
        engine.getRecognitionSettings().setUseGpu(true);
        // Optional: specify a GPU device index if multiple GPUs are present
        // engine.getRecognitionSettings().setGpuDeviceId(0);

        // Step 3: Perform OCR on the loaded image
        OcrResult result = engine.recognize();

        // Step 4: Output the recognized text
        System.out.println("Recognized text:");
        System.out.println(result.getText());
    }
}
```

> **Beklenen çıktı:** Konsol, `sample.jpg` içinde görünen tam metni yazdırır. Resim bir makbuz fotoğrafı ise, her satırı ayrı bir dize olarak, satır sonlarını koruyarak göreceksiniz.

## Kenar Durumları ve Yaygın Tuzaklar

| Durum | Dikkat Edilmesi Gereken | Önerilen Çözüm |
|-----------|-------------------|---------------|
| **Birden fazla GPU** | Varsayılan GPU en güçlü olmayabilir. | `setGpuDeviceId` ile yüksek performanslı kartı hedefleyin. |
| **Büyük görüntülerde bellek yetersizliği** | Çok yüksek çözünürlüklü JPG'ler GPU belleğini tüketebilir. | Görüntüyü önce küçültün (`engine.getPreprocessingSettings().setResizeFactor(0.5)`). |
| **Düşük güven** | Resim bulanıksa bazı karakterler hatalı okunabilir. | Bağlam‑duyarlı düzeltmeler için `engine.getRecognitionSettings().setUseLanguageModel(true)` etkinleştirin. |
| **Desteklenmeyen görüntü formatı** | Aspose OCR birçok formatı destekler, ancak RAW sensör verisini desteklemez. | Dosyayı JPEG veya PNG'ye dönüştürüp motorun içine besleyin. |

Bu senaryoları ele alarak **metin görüntüsü tanıma** iş akışınızın farklı ortamlar içinde sağlam kalmasını sağlayabilirsiniz.

## Daha Hızlı ve Temiz OCR İçin Profesyonel İpuçları

- **Toplu işleme:** Birden çok resim için aynı `OcrEngine` örneğini yeniden kullanın; GPU bağlamı canlı kalır ve başlatma maliyeti azalır.  
- **İş parçacığı güvenliği:** Her iş parçacığı kendi `OcrEngine` nesnesine sahip olmalı; sınıf iş parçacığı‑güvenli değildir.  
- **Lisansı erken yükleyin:** Değerlendirme filigranını önlemek için uygulama başlangıcında Aspose lisansınızı yükleyin.  
- **Günlükleme:** Belirli bir resmin neden başarısız olduğunu debug etmek için `engine.getLogSettings().setEnableLogging(true)`'ı etkinleştirin.

## Sonuç

Aspose OCR ve GPU hızlandırma kullanarak Java'da **metin görüntüsü tanıma** nasıl yapılır gösterdik. Kütüphaneyi ekleme, JPEG yükleme, **set gpu device** ayarı, OCR motorunu çalıştırma ve sonunda **extract text jpg** ya da **read text picture** işlemlerini izleyerek bu süreci kendi projelerinizde uygulayabilirsiniz.

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ilgili konuları kapsamaktadır. Her kaynak, ek API özelliklerini öğrenmenize ve projelerinizde alternatif uygulama yaklaşımları keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım adım açıklamalar içerir.

- [Aspose OCR ile metin görüntüsü tanıma – Tam Java OCR Öğreticisi](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Aspose.OCR Detect Areas Modu ile Java'da Görüntüden Metin Çıkarma](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Aspose.OCR BufferedImage Kullanarak Java'da Görüntüyü Metne Dönüştürme](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}