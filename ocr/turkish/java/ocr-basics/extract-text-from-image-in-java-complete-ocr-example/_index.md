---
category: general
date: 2026-01-12
description: Aspose OCR'i Java'da kullanarak görüntüden metin çıkarın. Java OCR örneğiyle
  bir fatura görüntüsünden metin nasıl çıkarılır öğrenin ve çıktıyı OCR metni olarak
  alın.
draft: false
keywords:
- extract text from image
- how to extract text
- java ocr example
- process invoice image
- output ocr text
language: tr
og_description: Aspose OCR kullanarak Java’da görüntüden metin çıkarma. Bu kılavuz,
  bir fatura görüntüsünden metnin nasıl çıkarılacağını gösterir, bir Java OCR örneği
  içerir ve OCR metnini çıktılar.
og_title: Java'da Görüntüden Metin Çıkarma – Tam OCR Örneği
tags:
- OCR
- Java
- Aspose
title: Java’da Görüntüden Metin Çıkarma – Tam OCR Örneği
url: /tr/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüden Metin Çıkarma Java’da – Tam OCR Örneği

Saçınızı yolmadan **görüntüden metin çıkarma** dosyalarını nasıl yapacağınızı hiç merak ettiniz mi? Belki taranmış faturalar yığınına sahipsiniz ve numaraları hızlıca ihtiyacınız var. Benim deneyimime göre, en kolay yol, özel bir OCR kütüphanesinin ağır işi yapmasına izin vermektir. Bu öğretici, Aspose OCR for Java kullanarak tipik bir fatura görüntüsünden *metin nasıl çıkarılır* gösterir ve hatta **java ocr example** örneğiyle OCR metnini alttaki sisteminize aktarabileceğiniz bir çıktı verir.

Projeyi kurmaktan, başlık ve toplam tutara odaklanan ilgi bölgesi (ROI) tanımlamaya, son olarak çıkarılan metni yazdırmaya kadar bilmeniz gereken her şeyi adım adım anlatacağız. Sonunda **process invoice image** dosyalarını otomatik olarak işleyebilecek ve temiz, aranabilir metin elde edebileceksiniz.

> **Ne elde edeceksiniz:** çalıştırmaya hazır bir Java programı, her adımın net açıklamaları ve gerçek dünyadaki faturalarla başa çıkmak için pratik ipuçları.

## Önkoşullar

- Java Development Kit (JDK) 8 veya daha yeni bir sürüm yüklü.
- Bağımlılık yönetimi için Maven veya Gradle (Maven örneği gösterilmiştir).
- Aspose OCR for Java lisansı (ücretsiz deneme testi için çalışır).
- Bilinen bir dizine yerleştirilmiş bir fatura görüntüsü (`invoice.png`).

Eğer bunlardan biri size yabancı geliyorsa endişelenmeyin—çoğu sadece bir indirme uzaklığında ve kod topluluk sürümüyle de derlenebilecektir.

## Adım 1: Maven Projenizi Kurun

İlk olarak, yeni bir Maven projesi oluşturun (veya mevcut birine ekleyin). `pom.xml` dosyanıza Aspose OCR bağımlılığını ekleyin:

```xml
<!-- pom.xml -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.9</version> <!-- Use the latest version available -->
    </dependency>
</dependencies>
```

> **Pro ipucu:** Sürüm numarasını güncel tutun; yeni sürümler genellikle faturalarda bulunan zor fontlar için doğruluğu artırır.

Dosyayı kaydettikten sonra, kütüphaneyi yerel depoya çekmek için `mvn clean install` komutunu çalıştırın.

## Adım 2: Fatura Görüntüsünü Yükleyin

Kütüphane hazır olduğuna göre, küçük bir Java sınıfı yazalım. İlk yaptığımız `OcrEngine` örneği oluşturup okumak istediğiniz görüntüyü ona işaretlemek.

```java
import com.aspose.ocr.*;

public class RoiExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage("YOUR_DIRECTORY/invoice.png"); // <-- replace with your path
```

Neden motoru **görüntüyü** yüklemeden önce oluşturuyoruz? Motor, dil, DPI ve ROI gibi yapılandırmaları tutar. Görüntüyü erken ayarlamak, bu ayarların işlenecek tam dosyaya uygulanmasını sağlar.

## Adım 3: İlgi Bölgelerini (ROI) Tanımlayın

Faturalar genellikle çok fazla gürültü içerir—tablolar, logolar ve ince yazılar. OCR'ı sadece başlık ve toplam tutara daraltarak hız ve doğruluğu büyük ölçüde artırırsınız. Aspose, bu bölgeleri dikdörtgenlerle tanımlamanıza izin verir.

```java
        // Step 3: Define the regions of interest (header and total amount)
        OcrRegion region = OcrRegion.builder()
                .addRectangle(0, 0, 800, 150)      // header area
                .addRectangle(0, 1200, 800, 200)   // total amount area
                .build();

        // Apply ROI to the engine
        engine.setRegion(region);
```

Koordinatlar piksel cinsindendir (`x`, `y`, `width`, `height`). Faturalarınız boyut olarak değişiyorsa, bu değerleri dinamik olarak hesaplayabilirsiniz—belki önce görüntü boyutlarını kontrol ederek. Bu, toplu olarak çalışan bir **process invoice image** çözümüne ihtiyacınız varsa güzel bir genişletmedir.

## Adım 4: Belirtilen Bölgelerde OCR Çalıştırın

ROI ayarlandıktan sonra, OCR motoru en önemli bölgelere odaklanabilir. `recognize()` metodu, çıkarılan metni içeren bir `OcrResult` döndürür.

```java
        // Step 4: Run OCR on the specified regions
        OcrResult result = engine.recognize();
```

Arka planda, Aspose birkaç ön işleme adımı gerçekleştirir: ikilileştirme, gürültü kaldırma ve karakter segmentasyonu. Bunları manuel olarak çağırmanıza gerek yok—`recognize()`'ın işini yapmasına izin verin.

## Adım 5: Çıkarılan Metni Çıktılayın

Son olarak, metni konsola yazdırıyoruz. Gerçek bir uygulamada bunu bir veritabanına kaydedebilir, alt sistem analiz hattına besleyebilir veya hatta aranabilir bir PDF oluşturabilirsiniz.

```java
        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(result.getText());
    }
}
```

Programı çalıştırdığınızda aşağıdakine benzer bir çıktı görmelisiniz:

```
ROI text:
Acme Corp.
Invoice #12345
Date: 2025-12-31
Total Amount: $1,250.00
```

Çıktı bozuk görünüyorsa, dikdörtgen koordinatlarını tekrar kontrol edin veya görüntü çözünürlüğünü artırın. OCR motorları net, yüksek DPI taramaları sever.

## Tam Çalışan Örnek

Aşağıda, `src/main/java/RoiExample.java` dosyasına kopyalayıp yapıştırabileceğiniz eksiksiz, bağımsız Java dosyası bulunmaktadır. Harici kod parçacığı gerekmez—gereken her şey burada.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.region.*;

public class RoiExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage("YOUR_DIRECTORY/invoice.png");

        // Step 2: Define the regions of interest (header and total amount)
        OcrRegion region = OcrRegion.builder()
                .addRectangle(0, 0, 800, 150)      // header area
                .addRectangle(0, 1200, 800, 200)   // total amount area
                .build();

        // Step 3: Apply the ROI configuration to the engine
        engine.setRegion(region);

        // Step 4: Run OCR on the specified regions
        OcrResult result = engine.recognize();

        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(result.getText());
    }
}
```

> **Not:** `YOUR_DIRECTORY` ifadesini fatura görüntünüzün mutlak yolu ile değiştirin. Göreli bir yol kullanıyorsanız, çalışma dizininin `java` komutunu çalıştırdığınız konumla eşleştiğinden emin olun.

## Yaygın Sorular ve Kenar Durumları

### Fatura boyutu değişirse ne olur?

ROI'yi dinamik olarak hesaplayabilirsiniz:

```java
int imgWidth = engine.getImage().getWidth();
int imgHeight = engine.getImage().getHeight();

int headerHeight = imgHeight / 10;
int totalHeight = imgHeight / 8;

OcrRegion region = OcrRegion.builder()
        .addRectangle(0, 0, imgWidth, headerHeight)
        .addRectangle(0, imgHeight - totalHeight, imgWidth, totalHeight)
        .build();
```

### Birden fazla dili nasıl yönetirim?

Aspose OCR dil paketlerini destekler. `recognize()`'ı çağırmadan önce dili ayarlamanız yeterlidir:

```java
engine.setLanguage(OcrLanguage.Spanish); // or OcrLanguage.English, etc.
```

### OCR boş string döndürürse ne olur?

Tipik suçlular şunlardır:

- Düşük görüntü çözünürlüğü (< 300 DPI). Yükseltin veya daha yüksek kalite taramaları isteyin.
- Çok karanlık veya çok açık arka planlar. OCR'dan önce basit bir kontrast artırma filtresi uygulayın.
- Metni tamamen kaçıran hatalı ROI koordinatları.

## Üretim‑Hazır OCR İçin İpuçları

1. **Batch Processing:** Mantığı, fatura dosyalarının bulunduğu bir dizinde dönen bir döngüye sarın. Her sonucu denetlenebilirlik için kaydedin.
2. **Error Handling:** `OcrException` yakalayarak bozuk görüntüleri tüm işi durdurmadan nazikçe atlayın.
3. **Performance:** Birden fazla görüntüde tek bir `OcrEngine` örneğini yeniden kullanın; dosya başına yeni bir motor oluşturmak gereksiz yük getirir.
4. **Validation:** Çıkarma sonrası, toplam tutar üzerinde bir regex kontrolü (`\$\d{1,3}(,\d{3})*(\.\d{2})?`) çalıştırarak sayının gerçekçi göründüğünden emin olun.

Bu önerileri uygulamak, basit bir **java ocr example**'ı, gece boyunca **process invoice image** dosyalarını işlemek zorunda olan herhangi bir işletme için sağlam, ölçeklenebilir bir çözüme dönüştürür.

## Sonuç

Aspose OCR kullanarak Java’da **görüntüden metin çıkarma** dosyalarını, pratik bir fatura‑işleme senaryosuna odaklanarak nasıl yapacağınızı yeni gördük. İlgi bölgesi tanımlayarak, OCR motorunu çalıştırıp **output OCR text**'i yazdırarak, otomatik veri yakalama hatları oluşturmak için sağlam bir temele sahipsiniz.

Sonraki adımlar? ROI'yi satır‑satır tablo içerecek şekilde genişletmeyi deneyin, farklı dil ayarlarıyla deney yapın veya çıkarılan string'leri aranabilir belgeler için bir PDF‑oluşturma kütüphanesine besleyin. OCR'ı modern Java araçlarıyla birleştirdiğinizde sınır yoktur.

**how to extract text**'i diğer belge türlerinden çıkarmak hakkında daha fazla sorunuz varsa ya da alışılmadık düzenler için ROI'yi ayarlamakta yardıma ihtiyacınız varsa, aşağıya bir yorum bırakın—mutlu kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}