---
category: general
date: 2026-06-19
description: Java'da Aspose OCR kullanarak görüntüyü otomatik olarak düzleştirin.
  Eğimi düzeltmeyi, OCR ile metin çıkarmayı ve birkaç kolay adımda düzleştirme açısını
  öğrenin.
draft: false
keywords:
- auto deskew image
- extract text ocr
- how to correct skew
- how to get deskew
language: tr
og_description: Java'da Aspose OCR ile otomatik eğikliği düzeltin. Eğikliği nasıl
  düzelteceğinizi, OCR ile metin çıkarımını ve düzeltme açısını nasıl alacağınızı
  keşfedin—hepsi tek bir rehberde.
og_title: Java'da Otomatik Eğik Düzeltme Görüntüsü – Tam Aspose OCR Öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Auto deskew image using Aspose OCR in Java. Learn how to correct skew,
    extract text OCR and get deskew angle in a few easy steps.
  headline: Auto Deskew Image in Java – Complete Aspose OCR Guide
  type: TechArticle
tags:
- Aspose OCR
- Java
- Image Processing
title: Java'da Görüntüyü Otomatik Düzle – Tam Aspose OCR Kılavuzu
url: /tr/java/ocr-operations/auto-deskew-image-in-java-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da Otomatik Çarpıtma Düzeltme – Tam Aspose OCR Kılavuzu

OCR çalıştırmadan önce **auto deskew image** dosyalarını nasıl otomatik olarak düzeltileceğini hiç merak ettiniz mi? Belki kaydırılmış bir masada bir makbuz fotoğrafı çektiniz ya da taranmış bir form hafif bir eğimle geldi ve metin çıkarımı bozulmuş oldu. Bu, özellikle sonraki işlemler için güvenilir **extract text OCR** sonuçlarına ihtiyacınız olduğunda yaygın bir sorun.

Bu öğreticide, Aspose OCR for Java kullanarak **auto deskew image** dosyalarını nasıl otomatik olarak düzelteceğinizi adım adım gösterecek, **how to correct skew** yöntemini gösterecek ve motor tamamlandığında **how to get deskew** ayrıntılarını ortaya çıkaracağız. Sonunda, sadece resimleri otomatik olarak düzeltmekle kalmayıp aynı zamanda temiz metin çıkaran, çalıştırmaya hazır bir Java programına sahip olacaksınız. Gereksiz ayrıntı yok, sadece bugün kopyalayıp yapıştırabileceğiniz pratik kod ve açıklamalar.

## Öğrenecekleriniz

- Bir Java projesinde Aspose OCR'yi yükleyin ve lisanslayın.  
- Motorun otomatik çarpıtma düzeltme (deskew) özelliğini etkinleştirin.  
- Aşırı düzeltmeyi önlemek için bir güven eşiği (confidence threshold) ayarlayın.  
- Eğik bir görüntüde OCR çalıştırın ve uygulanan deskew açısını alın.  
- Güven temelli sonuçlarla tanınan metni çıkarın.  

**Önkoşullar** – Java 8+ SDK, bağımlılık yönetimi için Maven veya Gradle ve bir Aspose OCR lisans dosyası. Maven'a yeniyseniz endişelenmeyin; ihtiyacınız olan minimal `pom.xml` snippet'ini ele alacağız.

---

## ## Aspose OCR ile Otomatik Çarpıtma Düzeltme – Adım 1: Projeyi Kurun

İlk olarak, kütüphaneyi projenize ekleyelim. Aşağıdaki bağımlılığı `pom.xml` dosyanıza (veya eşdeğer Gradle girdisine) ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check for the latest version -->
</dependency>
```

> **Pro ipucu:** Versiyon numarasına dikkat edin; Aspose, deskew algoritmaları için performans iyileştirmeleri sık sık yayınlar.

Maven artefaktı çözdükten sonra `SkewDemo` adlı basit bir Java sınıfı oluşturun. Bu, **how to correct skew** ve **how to get deskew** bilgilerini göstereceğimiz bir oyun alanı olacak.

## ## Çarpıtma Düzeltmeyi Nasıl Yaparsınız – Adım 2: Lisans ve Motor Başlatma

Herhangi bir OCR metodunu çağırmadan önce lisansınızı yüklemelisiniz. Aksi takdirde, kütüphane değerlendirme modunda çalışır ve işleyebileceğiniz sayfa sayısını sınırlar.

```java
import com.aspose.ocr.*;

public class SkewDemo {
    public static void main(String[] args) throws Exception {
        // Load the Aspose OCR license (replace with your actual path)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

Lisans adımının en üstte izole edildiğine dikkat edin—bu, lisanslamanın bir kez yapılan bir kurulum olduğu ve her görüntü için tekrarlanmadığı en iyi uygulamaları yansıtır. Bunu unutursanız, motor bir lisanslama istisnası fırlatır; bu, yeni başlayanlar için yaygın bir engeldir.

## ## Deskew Bilgisini Nasıl Alırsınız – Adım 3: Otomatik‑Deskew'i Etkinleştirin ve Güveni Ayarlayın

Şimdi OCR motorunu örnekleyip ona **auto deskew image** işlemini otomatik olarak yapmasını söylüyoruz. `setAutoDeskew(true)` çağrısı, dönüş açısını algılayan ve bitmap'i yatay bir temel çizgiye geri döndüren dahili algoritmayı etkinleştirir.

```java
        // Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Enable automatic deskewing
        ocrEngine.setAutoDeskew(true);                     // auto deskew image
        // Define how confident the engine must be before applying the correction
        ocrEngine.setDeskewConfidenceThreshold(0.85);     // 85% confidence is a safe default
```

Güven eşiği neden? Garip bir açıdan çekilmiş bir reklam panosu fotoğrafını hayal edin; motor büyük bir dönüş tahmin edebilir ve metni bozabilir. `0.85` ayarlayarak “yalnızca %85'ten fazla emin olduğumuzda deskew uygula” diyoruz. Görüntü setiniz ne kadar gürültülü ise bu değeri artırıp azaltabilirsiniz.

## ## Metin Çıkarma OCR – Adım 4: Görüntüyü Tanıma

Motor hazır olduğunda, ona eğik bir resmin yolunu verin. `recognizeImage` metodu, hem deskew'i (etkinse) hem de OCR'yi tek bir geçişte gerçekleştirir.

```java
        // Recognize text from a skewed image
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/angled-photo.jpg");
```

Dosya bulunamazsa, Java bir `FileNotFoundException` fırlatır. Hızlı bir kontrol—yolun programı başlattığınız çalışma dizinine göre mutlak ya da göreli olduğundan emin olun.

## ## Otomatik Çarpıtma Düzeltme – Adım 5: Deskew Açısını ve Çıkarılan Metni Alın

Tanıma sonrasında, `OcrResult` nesnesi size iki değer verir: motorun uyguladığı açı ve düz metin çıktısı.

```java
        // Print the applied deskew angle
        System.out.println("Applied angle: " + ocrResult.getAppliedDeskewAngle());

        // Print the extracted text
        System.out.println("Extracted text:");
        System.out.println(ocrResult.getText());
    }
}
```

`getAppliedDeskewAngle()` metodu, dereceyi temsil eden bir `double` döndürür (saat yönünde dönüş için pozitif). Görüntü zaten düzse, `0.0` görürsünüz. Bu, **how to get deskew** bilgisinin özüdür; denetim izleri için kaydedilebilir veya sahne arkasında gerçekleşen düzeltmeyi kullanıcıya göstermek için bir UI'ye geri beslenebilir.

## ## Tam Çalışan Örnek – Tüm Adımlar Tek Dosyada

Aşağıda tam, çalıştırmaya hazır Java sınıfı yer alıyor. IDE'nize kopyalayın, lisans ve resim yollarını değiştirin ve *Run* tuşuna basın.

```java
import com.aspose.ocr.*;

public class SkewDemo {
    public static void main(String[] args) throws Exception {
        // -------------------- Step 1: License --------------------
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic"); // <-- update path

        // -------------------- Step 2: Engine --------------------
        OcrEngine ocrEngine = new OcrEngine();

        // -------------------- Step 3: Auto‑Deskew --------------------
        ocrEngine.setAutoDeskew(true);                     // auto deskew image
        ocrEngine.setDeskewConfidenceThreshold(0.85);     // high‑confidence only

        // -------------------- Step 4: Recognize --------------------
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/angled-photo.jpg"); // <-- update path

        // -------------------- Step 5: Results --------------------
        System.out.println("Applied angle: " + ocrResult.getAppliedDeskewAngle());
        System.out.println("Extracted text:");
        System.out.println(ocrResult.getText());
    }
}
```

**Beklenen çıktı** (örnek):

```
Applied angle: -2.7
Extracted text:
Invoice #12345
Date: 2024‑04‑01
Total: $89.99
Thank you for your business!
```

Açının küçük bir negatif sayı olduğunu fark edin—bu, orijinal fotoğrafın birkaç derece saat yönünün tersine eğildiği ve Aspose'un OCR'den önce bunu düzelttiği anlamına gelir.

## ## Yaygın Tuzaklar ve Kenar Durumları

| Sorun | Neden Oluşur | Çözüm |
|-------|----------------|-----|
| **Deskew uygulanmadı (açı = 0)** | Görüntü zaten düz veya güven eşiği altında. | `setDeskewConfidenceThreshold` değerini gürültülü taramalar için `0.6`'ya düşürün. |
| **Çıktıda bozuk karakterler** | Görüntü kalitesi çok düşük; gürültü hem deskew'i hem de OCR'yi etkiler. | Aspose'a göndermeden önce bir yumuşatma filtresiyle ön işleme yapın veya DPI'yi artırın. |
| **Lisans bulunamadı** | Yanlış yol veya eksik dosya. | Mutlak bir yol kullanın veya `.lic` dosyasını sınıf yoluna (classpath) yerleştirin ve `license.setLicense("Aspose.OCR.lic");` çağrısını yapın. |
| **Büyük toplu işlemlerde bellek yetersizliği** | Her çağrı tüm görüntüyü belleğe yükler. | Tek bir `OcrEngine` örneğini yeniden kullanın ve her görüntüden sonra `ocrEngine.clear()` çağırın. |

## ## İleriye Dönük – Sonraki Adımlar

- **Batch processing:** Görüntü dizini üzerinde döngü oluşturun, her `appliedDeskewAngle` değerini toplayın ve analiz için sonuçları bir CSV dosyasına kaydedin.  
- **Language selection:** Çok dilli belgelerde doğruluğu artırmak için `ocrEngine.setLanguage(OcrLanguage.English);` kullanın.  
- **Region‑based OCR:** Sadece belirli bir alanla (ör. barkod) ilgileniyorsanız `ocrEngine.recognizeRegion(rect);` çağırın.  

Bu uzantıların tümü, oluşturduğumuz **auto deskew image** temeli sayesinde fayda sağlar, çünkü doğru yönlendirilmiş bir bitmap yüksek kaliteli OCR için en önemli faktördür.

## ## Sonuç

Java'da Aspose OCR ile **auto deskew image** dosyalarını nasıl yapacağınızı, **how to correct skew** yöntemini, **how to get deskew** açılarını nasıl alacağınızı ve sonunda **extract text OCR** ile temiz metin çıkarımını gösterdik. Kısa, bağımsız program saniyeler içinde çalışır, ancak aksi takdirde ayrı bir görüntü işleme kütüphanesi gerektirecek karmaşık bir sorunu çözer.

Kendi fotoğraflarınızla deneyin, güven eşiğini ayarlayın ve konsolda deskew açısının göründüğünü izleyin. Rahat olduğunuzda toplu iş mantığını ekleyin veya çıktıyı bir belge yönetim hattına entegre edin. Gökyüzü sınırdır—sadece doğru yönlendirilmiş bir görüntünün güvenilir OCR'ın gizli sosu olduğunu unutmayın.

Herhangi bir sorunla karşılaşırsanız, aşağıya yorum bırakın veya en son API değişiklikleri için Aspose'un resmi Java belgelerine göz atın. Kodlamaktan keyif alın ve taramalarınız her zaman düz kalsın! 

![OCR çıkarımı öncesinde eğik bir görüntünün otomatik deskew işlemini gösteren diyagram – auto deskew image süreci](auto-deskew-diagram.png "auto deskew image iş akışı")


## Sonra Ne Öğrenmelisiniz?

- [Aspose.OCR kullanarak Java'da çarpıtma açısını nasıl hesaplarım](/ocr/english/java/ocr-basics/calculate-skew-angle/)
- [Aspose OCR ile metin görüntüsü tanıma – Tam Java OCR Öğreticisi](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Aspose.OCR Detect Areas Mode ile Java'da Görüntüden Metin Çıkarma](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}