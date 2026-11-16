---
category: general
date: 2026-07-05
description: Java OCR seçili alan tekniğiyle tabloyu nasıl OCR yapılır. Hazır‑çalıştır
  örneğiyle tablo veri görüntüsünü çıkarmayı ve metin bölgesini tanımayı öğrenin.
draft: false
keywords:
- how to ocr table
- ocr selected area
- extract table data image
- recognize text region
language: tr
og_description: 'Java''da tablo OCR nasıl yapılır: seçilen alanı OCR''lamak, tablo
  veri görüntüsünü çıkarmak ve metin bölgesini tanımak için tam kaynak kodlu pratik
  bir öğretici.'
og_title: Java'da tablo OCR nasıl yapılır – Tam Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: how to ocr table using Java OCR selected area technique. Learn to extract
    table data image and recognize text region with a ready‑to‑run example.
  headline: how to ocr table in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: how to ocr table using Java OCR selected area technique. Learn to extract
    table data image and recognize text region with a ready‑to‑run example.
  name: how to ocr table in Java – Complete Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '- Java 17 or newer (the code compiles on JDK 11+ as well). - An OCR library
      that provides `OcrEngine`, `Region`, and `RecognitionResult` classes (e.g.,
      Aspose.OCR for Java, Tesseract‑Java wrapper, or any vendor‑specific SDK). -
      A sample image (`rotated_table.png`) placed in a known directory. - Basi'
  - name: 1. Different Image Formats
    text: Most OCR SDKs accept PNG, JPEG, BMP, and TIFF. If you receive a PDF, convert
      the first page to an image first (e.g., using Apache PDFBox). This extra step
      ensures the **ocr selected area** logic works on a raster image.
  - name: 2. Varying Rotation Angles
    text: The automatic deskew works best for rotations up to ±15°. For extreme angles,
      pre‑rotate the image using a library like `java.awt.Graphics2D` before feeding
      it to the OCR engine.
  - name: 3. Large Images and Memory Footprint
    text: If the source image is huge (several megabytes), consider scaling it down
      while preserving DPI. Most SDKs expose a `setResolution(int dpi)` method; 300
      dpi is a good compromise between speed and accuracy.
  - name: 4. Capturing Structured Data
    text: Some OCR engines can return a table model (rows × columns) instead of plain
      text. Look for methods like `recognitionResult.getTable()` or `recognitionResult.getCsv()`.
      When available, you can directly feed the result into a database or spreadsheet.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
- Table Extraction
title: Java'da tablo OCR nasıl yapılır – Tam Adım Adım Rehber
url: /tr/java/advanced-ocr-techniques/how-to-ocr-table-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da tablo OCR nasıl yapılır – Tam Adım‑Adım Kılavuz

Hiç bir taranmış belgeden tüm sayfayı belleğe almadan **how to ocr table** yapmayı merak ettiniz mi? Tek başınıza değilsiniz. Gerçek dünyadaki birçok projede—fatura işleme veya eski PDF'lerden veri taşıma gibi—yalnızca tablo bölgesi önemlidir, geri kalan ise sadece gürültüdür.  

Bu öğreticide, belirli bir dikdörtgene odaklanarak **how to ocr table** gösteren kompakt, çalıştırılabilir bir örnek üzerinden ilerleyeceğiz; motorun içeriği otomatik olarak eğriltmeyi düzeltebilmesine izin vererek. Sonunda sadece birkaç Java satırıyla **ocr selected area**, **extract table data image** ve **recognize text region** yapabilecek olacaksınız.

## Öğrenecekleriniz

- Java'da bir OCR motoru örneği kurun.
- Döndürülmüş tabloyu izole eden bir **Region** tanımlayın.
- OCR motorunun eğriltmeyi düzeltirken **recognize text region** yapmasına izin verin.
- Çıkarılan tablo metnini konsola yazdırın.
- Farklı görüntü formatları, dönüş açıları ve performans ayarlarıyla başa çıkma ipuçları

### Önkoşullar

- Java 17 veya daha yeni (kod JDK 11+ üzerinde de derlenir).
- `OcrEngine`, `Region` ve `RecognitionResult` sınıflarını sağlayan bir OCR kütüphanesi (ör. Aspose.OCR for Java, Tesseract‑Java wrapper veya herhangi bir satıcı‑özel SDK).
- Bilinen bir dizine yerleştirilmiş örnek bir görüntü (`rotated_table.png`).
- Bağımlılık yönetimi için Maven/Gradle konusunda temel bilgi.

> **Pro tip:** Maven kullanıyorsanız, OCR kütüphanesi bağımlılığını `pom.xml` dosyanıza ekleyin. Gradle için ise `build.gradle` içine koyun. Kesin koordinatlar satıcıya göre değişir, ancak genellikle `com.aspose:aspose-ocr:23.10` şeklindedir.

## Adım 1: OCR Motorunu Başlatma – **how to ocr table**'ın Çekirdeği

Bir motor örneği oluşturmak, **ocr selected area** yapmak istediğinizde ilk yaptığınız şeydir. Motoru, daha sonra tanımladığınız dikdörtgen içindeki pikselleri yorumlayacak beyin olarak düşünün.

```java
// Step 1: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

> **Neden önemli:** Bir motor olmadan, dil, algılama modu veya eğriltme düzeltme seçenekleri için bağlam yoktur. Çoğu SDK, herhangi bir tanıma metodunu çağırmadan önce bu ayarları (ör. `ocrEngine.setLanguage(Language.English)`) değiştirmenize izin verir.

## Adım 2: Döndürülmüş Tabloyu Barındıran Bölgeyi Tanımlama

Bir **Region** nesnesi, işlemek istediğiniz alanın `(x, y, width, height)` koordinatlarını tanımlar. Bizim örneğimizde tablo `(120, 350)` konumunda ve `800 × 500` piksel ölçüsündedir. Bu sayıları kendi belgenize göre ayarlayın.

```java
// Step 2: Define the region (x, y, width, height) that contains the rotated table
Region tableRegion = new Region(120, 350, 800, 500);
```

> **Neden önemli:** OCR'ı bir **selected area** ile sınırlayarak işleme süresini büyük ölçüde azaltır ve doğruluğu artırırsınız. Motor, bu dikdörtgen içindeki içeriği otomatik olarak da eğriltmeyi düzeltir; bu, tablo döndürülmüş olduğunda çok önemlidir.

## Adım 3: Bölgedeki Metni Tanıma – **recognize text region** Eylemde

Şimdi motorunize görüntü yolunu ve önceden tanımlanmış `Region`'ı veriyoruz. `recognizeRegion` yöntemi iki şey yapar: görüntüyü dikdörtgene kırpar ve ardından OCR çalıştırır, gerekli dönüşüm düzeltmesini uygular.

```java
// Step 3: Recognize text only within the specified region; the engine will deskew it automatically
RecognitionResult recognitionResult = ocrEngine.recognizeRegion(
        "YOUR_DIRECTORY/rotated_table.png",   // path to your image
        tableRegion);                         // the region we defined above
```

> **Neden önemli:** Bu tek çağrı, aksi takdirde manuel kırpma, eğriltme düzeltme ve ardından OCR içeren çok adımlı bir işlem hattını yerine geçirir. Bu, **how to ocr table**'ı verimli bir şekilde yapmanın kalbidir.

## Adım 4: Çıkarılan Tablo Metnini Çıktılamak – **extract table data image** Sonucunu Doğrulama

Son olarak OCR çıktısını yazdırıyoruz. `RecognitionResult` nesnesi genellikle ham metni, güven skorlarını ve isteğe bağlı olarak yapılandırılmış bir temsili (ör. CSV dizesi) içerir.

```java
// Step 4: Output the extracted text
System.out.println("Table text:");
System.out.println(recognitionResult.getText());
```

> **Beklenen çıktı (örnek):**  

```
Table text:
Item   Qty   Price
Apple   10   $1.20
Banana   5   $0.80
Total        $16.00
```

Eğer tablo hâlâ hizalanmamışsa, `Region` boyutlarını ayarlayabilir veya motor ayarlarıyla daha yüksek çözünürlük işleme etkinleştirebilirsiniz.

## Yaygın Kenar Durumlarını Ele Alma

### 1. Farklı Görüntü Formatları

Çoğu OCR SDK'sı PNG, JPEG, BMP ve TIFF formatlarını kabul eder. PDF alırsanız, ilk sayfayı önce bir görüntüye dönüştürün (ör. Apache PDFBox kullanarak). Bu ekstra adım, **ocr selected area** mantığının bir raster görüntüde çalışmasını sağlar.

### 2. Değişen Dönüş Açıları

Otomatik eğriltme düzeltme, ±15°'ye kadar olan dönüşler için en iyisidir. Aşırı açılar için, OCR motoruna vermeden önce `java.awt.Graphics2D` gibi bir kütüphane kullanarak görüntüyü önceden döndürün.

```java
BufferedImage src = ImageIO.read(new File("rotated_table.png"));
AffineTransform tx = new AffineTransform();
tx.rotate(Math.toRadians(30), src.getWidth() / 2, src.getHeight() / 2);
AffineTransformOp op = new AffineTransformOp(tx, AffineTransformOp.TYPE_BILINEAR);
BufferedImage rotated = op.filter(src, null);
ImageIO.write(rotated, "png", new File("pre_rotated.png"));
```

Ardından `recognizeRegion`'ı `pre_rotated.png`'ye yönlendirin.

### 3. Büyük Görüntüler ve Bellek Ayak İzi

Eğer kaynak görüntü çok büyükse (birkaç megabayt), DPI'yi koruyarak ölçeklendirmeyi düşünün. Çoğu SDK, `setResolution(int dpi)` metodunu sunar; 300 dpi hız ve doğruluk arasında iyi bir denge sağlar.

### 4. Yapılandırılmış Veri Yakalama

Bazı OCR motorları, düz metin yerine tablo modeli (satır × sütun) döndürebilir. `recognitionResult.getTable()` veya `recognitionResult.getCsv()` gibi metodlara bakın. Kullanılabilir olduğunda, sonucu doğrudan bir veritabanına veya elektronik tabloya aktarabilirsiniz.

## Tam Çalışan Örnek

Aşağıda, tüm parçaları bir araya getiren eksiksiz, çalıştırmaya hazır Java programı yer almaktadır. `YOUR_DIRECTORY` ifadesini görüntünüzün gerçek yolu ile değiştirin.

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.Region;

public class TableOcrDemo {
    public static void main(String[] args) {
        // Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Optional: set language and other settings
        // ocrEngine.setLanguage(Language.English);
        // ocrEngine.setResolution(300);

        // Define the region that contains the rotated table
        Region tableRegion = new Region(120, 350, 800, 500);

        // Perform OCR on the selected area – the engine deskews automatically
        RecognitionResult recognitionResult = ocrEngine.recognizeRegion(
                "YOUR_DIRECTORY/rotated_table.png",
                tableRegion);

        // Print the extracted table text
        System.out.println("Table text:");
        System.out.println(recognitionResult.getText());
    }
}
```

**Programı çalıştırmak** (`javac TableOcrDemo.java && java TableOcrDemo`) tablo içeriğini konsola yazdırmalı ve döndürülmüş bir kaynaktan başarıyla **extract table data image** yaptığınızı doğrulamalıdır.

## Pro İpuçları & Dikkat Edilmesi Gerekenler

- **Batch processing:** Birden fazla görüntünüz varsa yukarıdaki mantığı bir döngüye alın. Aynı `OcrEngine` örneğini yeniden kullanmak başlatma yükünü azaltır.
- **Confidence filtering:** Bazı motorlar `recognitionResult.getConfidence()` metodunu sunar. Güven %80'in altında olan satırları atın ve manuel inceleme için işaretleyin.
- **Performance tuning:** Büyük partiler için çoklu iş parçacığını (`ExecutorService`) etkinleştirin ancak çoğu OCR motorunun CPU‑ağır olduğunu ve doğrusal ölçeklenemeyebileceğini unutmayın.
- **Legal note:** Tarama belgelerini işlerken her zaman telif hakkına saygı gösterin; veriyi çıkarmak için gerekli haklara sahip olduğunuzdan emin olun.

## Sonuç

Şimdi, Java OCR motoru kullanarak **ocr selected area**, **extract table data image** ve **recognize text region** nasıl yapılır gösteren öz fakat **how to ocr table** bir rehberi tamamladık. Motor oluşturma, bölge tanımlama, bölge‑tabanlı tanıma ve çıktı adımları, herhangi bir tablo çıkarma senaryosuna uyarlayabileceğiniz tekrarlanabilir bir desen oluşturur.

Bir sonraki meydan okumaya hazır mısınız? OCR sonucunu CSV'ye dışa aktarmayı, bir makine‑öğrenme modeline beslemeyi veya bir görüntü URL'si alıp yapılandırılmış JSON dönen bir mikro hizmet oluşturmayı deneyin. Java'da **how to ocr table**'ı ustalaştığınızda sınır yoktur.

İyi kodlamalar, ve sorularınızı ya da başarı hikayelerinizi aşağıdaki yorumlarda paylaşmaktan çekinmeyin! 

![how to ocr table example](ocr-table-diagram.png "how to ocr table example")


## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım‑adım açıklamalı eksiksiz çalışan kod örnekleri içerir.

- [Aspose.OCR'da OCR Metin Tanıması İçin Sayfa Dikdörtgenlerini Tanıma](/ocr/english/java/advanced-ocr-techniques/prepare-rectangles-for-ocr/)
- [Aspose.OCR Detect Areas Modu ile Java'da Görüntüden Metin Çıkarma](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Aspose OCR ile Metin Görüntüsü Tanıma – Tam Java OCR Öğreticisi](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}