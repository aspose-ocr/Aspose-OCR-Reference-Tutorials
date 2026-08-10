---
category: general
date: 2026-02-14
description: Aspose OCR'i Java’da kullanarak bir görüntüde OCR nasıl yapılır ve görüntüden
  metin nasıl çıkarılır öğrenin. OCR için görüntü yükleme, özel sözlük ve yazım düzeltme
  içerir.
draft: false
keywords:
- perform OCR on image
- extract text from image
- load image for OCR
- Aspose OCR Java
- spell correction OCR
language: tr
og_description: Java'da Aspose OCR ile görüntüde OCR gerçekleştirin. Bu kılavuz, OCR
  için görüntüyü nasıl yükleyeceğinizi, görüntüden metni nasıl çıkaracağınızı ve yazım
  düzeltmeyi nasıl etkinleştireceğinizi gösterir.
og_title: Görselde OCR Yap – Tam Java Öğreticisi
tags:
- OCR
- Java
- Aspose
title: Aspose OCR ile Görüntüde OCR Yapma – Java Adım Adım Kılavuzu
url: /tr/java/advanced-ocr-techniques/perform-ocr-on-image-with-aspose-ocr-java-step-by-step-guide/
---

phrase. The bold phrase is **perform OCR on image**. Probably keep unchanged. So translate rest.

Let's go paragraph by paragraph.

Will produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntü Üzerinde OCR Yapma – Tam Java Öğreticisi

Görüntü dosyalarında **perform OCR on image** yapmanız gerektiğinde nereden başlayacağınızı bilemediniz mi? Yalnız değilsiniz; birçok geliştirici ilk kez görüntü verisinden metin çıkarmaya çalıştığında aynı duvara çarpar. İyi haber şu ki, Aspose OCR for Java ile sadece birkaç satır kodla güvenilir sonuçlar elde edebilir ve özel bir sözlük ile imla denetimi ekleyerek doğruluğu artırabilirsiniz.

Bu rehberde, OCR için görüntüyü yüklemekten imla düzeltmeyi etkinleştirmeye ve temizlenmiş metni yazdırmaya kadar bilmeniz gereken her şeyi adım adım inceleyeceğiz. Sonunda, kendi Java projelerinizde **perform OCR on image** varlıklarını kullanabilecek ve **extract text from image** dosyalarını gürültülü taramalarda bile çalışacak şekilde çıkarabileceksiniz.

## Gereksinimler

İlerlemeye başlamadan önce aşağıdakilerin hazır olduğundan emin olun:

- **Java Development Kit (JDK) 8+** – kod standart Java API'lerini kullanıyor.
- **Aspose OCR for Java** kütüphanesi (en son JAR dosyasını Aspose web sitesinden veya Maven Central'dan alabilirsiniz).
- İşlemek istediğiniz bir görüntü dosyası (ör. `invoice.png`).
- (İsteğe bağlı) Her satırda bir kelime olacak şekilde alan‑spesifik kelimeler içeren `custom_dict.txt` adlı bir düz metin dosyası.

Hepsi bu kadar—ağır çerçeveler, harici hizmetler yok. Sadece saf Java ve Aspose OCR JAR'ı.

## Adım 1: Projeyi Oluşturun ve Bağımlılıkları Ekleyin

İlk olarak yeni bir Maven (veya Gradle) projesi oluşturun ve Aspose OCR bağımlılığını ekleyin. Maven kullanıyorsanız `pom.xml` dosyanız şu bölümü içermelidir:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check for the latest version -->
</dependency>
```

JAR dosyasını manuel olarak indirmeyi tercih ederseniz, `libs` klasörüne koyun ve sınıf yoluna ekleyin.

> **İpucu:** Yazım zamanı itibarıyla sürüm numarasını her zaman kontrol edin; yeni sürümler dil paketleri gibi ek özellikler getirebilir.

## Adım 2: OCR İçin Görüntüyü Yükleyin

Gerçek kod adımının ilk kısmı, OCR motorunu analiz etmesi gereken görüntüye yönlendirmektir. Aspose OCR, bir dosyadan, bayt dizisinden veya hatta bir URL'den okuyabilen bir `ImageStream` sarmalayıcısı kullanır.

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

Görüntüyü **load image for OCR** tek bir metod çağrısıyla yüklediğimize dikkat edin—karmaşık `BufferedImage` işlemlerine gerek yok. Görüntünüz kaynaklarda ise yolu `getClass().getResourceAsStream(...)` ile değiştirin.

## Adım 3: İmla Düzeltmeyi Etkinleştirin (İsteğe Bağlı ama Güçlü)

Aspose OCR, yaygın OCR hatalarını (ör. “l” ile “1” karışıklığı) otomatik olarak düzeltebilir. Bu özelliği açmak sadece bir bayrağı değiştirmenize bağlı:

```java
        // Step 3: Turn on spell‑checking to improve result quality
        ocrEngine.getEngineOptions().setSpellCorrectionEnabled(true);
```

Neden? Küçük bir font ve tarayıcının getirdiği lekelerle basılmış bir faturayı taradığınızı hayal edin. İmla düzeltme, “Inv0ice” gibi hataları ekstra bir çaba harcamadan “Invoice” hâline getirebilir.

## Adım 4: Özel Bir Sözlük Sağlayın (Motoru Özelleştirin)

Sektöre özgü terminolojiyle (tıbbi kodlar, hukuki jargon, ürün SKU'ları vb.) çalışıyorsanız, özel bir sözlük doğruluğu büyük ölçüde artırır. Sözlük, satır başına bir kelime içeren basit bir metin dosyasıdır.

```java
        // Step 4: Load a custom dictionary to boost recognition of domain terms
        ocrEngine.getEngineOptions().setCustomDictionary(
                Files.readAllLines(Paths.get("YOUR_DIRECTORY/custom_dict.txt")));
```

Dosyanın UTF‑8 kodlamasını kullandığından emin olun; aksi takdirde ASCII dışı karakterler bozulmuş görünebilir.

## Adım 5: OCR İşlemini Çalıştırın

Şimdi motorun sihrini izne veriyoruz. `process()` çağrısı, tanınan metin, güven skorları ve gerekirse daha sonra kullanabileceğiniz düzeni içeren bir `OcrResult` nesnesi döndürür.

```java
        // Step 5: Execute OCR and capture the result
        OcrResult ocrResult = ocrEngine.process();
```

Motorun bir istisna fırlatıp fırlatmadığını merak ederseniz, bu çağrıyı bir try‑catch bloğuna alın ve detaylar için `ocrResult.getErrorMessage()` metodunu inceleyin.

## Adım 6: Tanınan (ve Düzeltlenmiş) Metni Çıktılayın

Son adım, çıkarılan dizeyi ekrana yazdırmak ya da saklamaktır. Hızlı bir demo için sadece konsola bastıralım:

```java
        // Step 6: Print the corrected text to the console
        System.out.println(ocrResult.getText());
    }
}
```

Programı çalıştırdığınızda aşağıdakine benzer bir çıktı görmelisiniz:

```
Invoice Number: 12345
Date: 2023‑07‑15
Total Amount: $1,250.00
```

Eğer garip karakterler görürseniz, özel sözlüğünüzü tekrar kontrol edin ve görüntü kalitesini (ör. kontrastı artırarak) motorun önüne göndermeyi düşünün.

### Tam Çalışan Örnek

Hepsini bir araya getirerek, çalıştırmaya hazır sınıf aşağıdadır:

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

Bu dosyayı `SpellCorrectDemo.java` olarak kaydedin, yolları ayarlayın, `javac` ile derleyin ve `java SpellCorrectDemo` ile çalıştırın. Artık **perform OCR on image** dosyalarını kullanabilir ve çıkarılan metni ekranda görebilirsiniz.

## Yaygın Sorular & Kenar Durumları

### Görüntü farklı bir formatta (PDF, TIFF vb.) ise ne olur?

Aspose OCR, birçok raster formatını kutudan çıkar çıkmaz destekler. PDF'ler için önce her sayfayı görüntüye dönüştürmeniz gerekir—Aspose PDF for Java bunu rahatça yapar. `setImage` çağrısı, bir `BufferedImage` ya da bayt akışı elde ettiğinizde aynı şekilde çalışır.

### Çok sayfalı belgeler nasıl işlenir?

Her sayfa görüntüsü üzerinde döngü kurun, OCR adımlarını çalıştırın ve sonuçları birleştirin. Bağımsız imla denetimi bağlamları istiyorsanız, her sayfa için yeni bir `OcrEngine` oluşturmayı unutmayın.

### Dil ya da karakter seti sınırlanabilir mi?

Evet. `ocrEngine.getEngineOptions().setLanguage(Language.English);` (veya desteklenen başka bir dil) kullanarak yanlış pozitifleri azaltabilir ve işlem hızını artırabilirsiniz.

### Büyük toplu işlemlerde performans nasıl?

Aspose OCR, yalnızca okuma‑sadece işlemler için thread‑safe'dir. Bir thread havuzu oluşturup görüntüleri eşzamanlı işleyebilirsiniz—tek bir `OcrEngine` örneğini thread'ler arasında paylaşmamaya dikkat edin.

## Doğruluğu Artırmak İçin İpuçları

- **Görüntüyü ön‑işleyin**: kontrastı artırın, arka plan gürültüsünü temizleyin veya gri tonlamaya dönüştürün.
- **Yüksek çözünürlüklü tarama** kullanın (300 dpi veya üzeri). Düşük çözünürlükler genellikle bozuk karakterlere yol açar.
- **Özel sözlüğü sade tutun**: çok fazla alakasız kelime imla denetleyicisini şaşırtabilir.
- **Çıktıyı doğrulayın**: beklenen formatı (tarih, sayı vb.) biliyorsanız, anomalileri yakalamak için bir regex sonrası işlem ekleyin.

## Sonraki Adımlar

Artık **perform OCR on image** dosyalarını ve **extract text from image** işlemlerini Aspose OCR ile yapabildiğinize göre, aşağıdaki konuları keşfetmek isteyebilirsiniz:

- **OCR çıktısını aranabilir metin katmanına sahip bir PDF** olarak kaydetmek.
- **Veritabanına entegrasyon** yaparak çıkarılan fatura verilerini otomatik olarak saklamak.
- **Makine öğrenimi sonrası işleme** uygulayarak el yazısı notlarda bile daha yüksek doğruluk elde etmek.
- **Web servisinde `load image for OCR` bayrağını** kullanarak kullanıcı‑yüklemeli fotoğrafları işlemek.

Bu konular, burada ele aldığımız temel adımlara dayanır; geçişiniz sorunsuz olacaktır.

---

*Kodlamanız keyifli olsun! Herhangi bir sorunla karşılaşırsanız, yorum bırakmaktan çekinmeyin—gerçek dünyadan örneklerle öğrenmekten daha iyisi yoktur.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}