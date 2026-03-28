---
category: general
date: 2026-03-28
description: Aspose OCR kullanarak Java’da görüntüde OCR çalıştırın, görüntüyü metne
  dönüştürün ve PNG’den Tayca metni hızlı ve güvenilir bir şekilde çıkarın.
draft: false
keywords:
- run OCR on image
- convert image to text
- extract text from PNG
- extract Thai text
- recognize Thai text
language: tr
og_description: Java ve Aspose OCR kullanarak görüntüde OCR çalıştırın. Görüntüyü
  metne nasıl dönüştüreceğinizi, PNG’den Tayca metni nasıl çıkaracağınızı ve yaygın
  hatalarla nasıl başa çıkacağınızı öğrenin.
og_title: Java ile Görselde OCR Çalıştır – Tayca Metni Hızlıca Çıkar
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Java ile Görüntüde OCR Çalıştır – PNG'den Tay Metnini Çıkar
url: /tr/java/ocr-operations/run-ocr-on-image-with-java-extract-thai-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java ile Görüntü Üzerinde OCR Çalıştırma – Tam Özellikli Öğretici

Java kodundan doğrudan **run OCR on image** dosyalarını çalıştırmayı hiç merak ettiniz mi? Belki Tayland fişleri, taranmış belgeler ya da ekran görüntülerinden oluşan bir koleksiyonunuz var ve metni elle yazmak istemiyorsunuz. Bu, özellikle kaynak bir PNG dosyası ve dil Latin dışı olduğunda sık karşılaşılan bir sorundur.  

Bu rehberde, Aspose OCR kütüphanesini kullanarak **run OCR on image** nasıl yapılır, resmi düz metne dönüştürür ve Tay karakterlerini güvenilir bir şekilde nasıl çıkarırsınız, adım adım göstereceğiz. Sonunda **convert image to text**, **extract text from PNG** ve hatta sadece birkaç satır kodla **recognize Thai text** yapabileceksiniz.

## Bu Öğreticide Neler Ele Alınıyor

* Maven/Gradle projesine Aspose OCR bağımlılığının eklenmesi.  
* `OcrEngine`'in başlatılması ve Tay dili için yapılandırılması.  
* PNG dosyası üzerinde OCR çalıştırılması ve olası hataların ele alınması.  
* Sonucun konsola yazdırılması ve çıktının doğrulanması.  

Aspose ile daha önce çalışmış olmanız gerekmez—sadece temel bir Java IDE'si ve işlemek istediğiniz bir görüntü dosyası yeterlidir.

## Ön Koşullar

* Java 8 veya daha yeni bir sürüm (kütüphane Java 11+ ile de çalışır).  
* Bir yapı aracı – Maven ya da Gradle (Maven örneğini göstereceğiz).  
* Aspose OCR lisansı (ücretsiz deneme sürümü test için yeterlidir, ancak lisans değerlendirme sınırlamalarını kaldırır).  
* Tayca metin içeren bir PNG, örneğin proje kaynak klasörünüzde `input.png` olarak bulunmalı.

---

## Adım 1: Aspose OCR'ı Projeye Ekleyin

### Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest version -->
</dependency>
```

### Gradle (Kotlin DSL)

```kotlin
implementation("com.aspose:aspose-ocr:23.9")
```

> **Pro ipucu:** Kütüphane sürümünü resmi Aspose sürüm notlarıyla senkronize tutun; yeni sürümler dil paketleri ve performans iyileştirmeleri ekler.

Bağımlılık çözüldükten sonra IDE gerekli sınıfları otomatik olarak içe aktaracaktır.

## Adım 2: OCR Motorunu Başlatın

Motor, sürecin kalbidir – piksel desenlerini analiz eden “beyin” gibi düşünün. Ayrıca sadece Tay karakterleriyle ilgilendiğimizi motor’a söyleyeceğiz.

```java
import com.aspose.ocr.*;

public class ThaiOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Tell the engine to look for Thai language patterns
        ocrEngine.getRecognitionSettings().setLanguage("th");
```

Neden dili açıkça ayarlıyoruz? `"th"` belirtmek karakter kümesini daraltır, tanıma hızını artırır ve benzer görünümlü gliflerin hatalı okunmasını azaltır.

## Adım 3: PNG Dosyası Üzerinde OCR Çalıştırın

Şimdi motoru çözmek istediğimiz görüntüyle besliyoruz. `recognizeImage` metodu, çıkarılan dizeyi ve güven skorlarını tutan bir `OcrResult` nesnesi döndürür.

```java
        // Step 3: Perform OCR on the target image
        String imagePath = "src/main/resources/input.png";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);
```

Dosya bulunamazsa Aspose bir `FileNotFoundException` fırlatır. Üretim kodu için çağrıyı bir `try‑catch` bloğuna almak iyi bir fikirdir, ancak bu öğreticide doğrudan ilerleyeceğiz.

## Adım 4: Tanınan Metni Çıktılayın

Son olarak sonucu ekrana yazdırıyoruz. `getText()` metodu, bir Java `String`i döndürür; bu dizeyi saklayabilir, ağ üzerinden gönderebilir ya da bir dosyaya yazabilirsiniz.

```java
        // Step 4: Display the extracted Thai text
        System.out.println("=== Recognized Thai Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Programı çalıştırdığınızda aşağıdaki gibi bir çıktı görmelisiniz:

```
=== Recognized Thai Text ===
สวัสดีครับ นี่คือข้อความจากรูปภาพ
```

Çıktı bozuk görünüyorsa, kaynak PNG'nin yüksek çözünürlüklü (en az 300 dpi) olduğundan ve dil kodunun `"th"` hedef dilinizle eşleştiğinden emin olun.

### Tam Kod Listesi

Aşağıda tamamen çalıştırılabilir Java dosyası yer alıyor. IDE'nize kopyalayıp yapıştırın, gerekirse görüntü yolunu değiştirin ve **Run** tuşuna basın.

```java
import com.aspose.ocr.*;

public class ThaiOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Select Thai language for recognition
        ocrEngine.getRecognitionSettings().setLanguage("th");

        // Run OCR on the PNG image
        String imagePath = "src/main/resources/input.png";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);

        // Output the recognized text
        System.out.println("=== Recognized Thai Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

![run OCR on image example](image.png "run OCR on image example – Java code extracting Thai text from PNG")

## Adım 5: Yaygın Varyasyonlar ve Kenar Durumları

### Diğer Formatlarda Görüntüyü Metne Dönüştürme

JPEG ya da BMP için **convert image to text** yapmanız gerekiyorsa, sadece `imagePath` içindeki dosya uzantısını değiştirin. Aspose OCR PNG, JPEG, BMP, TIFF ve hatta PDF sayfalarını destekler.

### PNG'den Çoklu Dillerde Metin Çıkarma

Motoru aynı anda birden fazla dili algılaması için yapılandırabilirsiniz:

```java
ocrEngine.getRecognitionSettings().setLanguage("th,en");
```

Sonuç, Tayca ve İngilizce karakterlerin bir karışımını içerecek; bu, çift dilli fişler için kullanışlıdır.

### Düşük Kaliteli Görüntülerle Baş Etme

Bulanık taramalar için ön işleme etkinleştirmeyi düşünün:

```java
ocrEngine.getRecognitionSettings().setPreprocessMode(PreprocessMode.Auto);
```

Bu, yerleşik gürültü azaltma ve kontrast artırma algoritmalarını tetikler, **extract text from PNG** adımını iyileştirir.

### Lisans Aktivasyonu

Lisans olmadan Aspose, 100 sayfadan sonra çıktıya bir filigran satırı ekler. Lisansınızı erken etkinleştirin:

```java
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

`.lic` dosyasını JAR dosyanızın yanına koyun ya da mutlak bir yol ile referans verin.

## Sık Sorulan Sorular

**S: Bu Linux'ta çalışır mı?**  
C: Kesinlikle. Aspose OCR saf Java olduğundan, JVM uyumlu herhangi bir işletim sistemi yeterlidir.

**S: PNG içinde el yazısı Tayca varsa ne olur?**  
C: El yazısı tanıma sınırlıdır; özel bir sinir ağı modeli gerekebilir. Aspose OCR basılı metinlerde çok iyidir.

**S: Bir klasördeki görüntüleri toplu olarak işleyebilir miyim?**  
C: `recognizeImage` çağrısını `Files.list(Paths.get("folder"))` döngüsü içinde sarın. Performans için aynı `OcrEngine` örneğini yeniden kullanın.

## Sonuç

Java’da **run OCR on image** dosyaları üzerinde tam bir uçtan uca örnek üzerinden ilerledik; özellikle bir PNG’den **extract Thai text** elde ettik. `OcrEngine`'i başlatıp dili ayarlayarak, `recognizeImage`'ı çağırıp sonucu yazdırarak, üçüncü taraf hizmetlere ihtiyaç duymadan **convert image to text** yapmanın güvenilir bir yolunu elde ettiniz.

Bundan sonra şunları yapabilirsiniz:

* **extract text from PNG** dosyalarını toplu olarak veri madenciliği projeleri için işlemek.  
* OCR çıktısını bir çeviri API'si ile birleştirerek İngilizce karşılıklarını elde etmek.  
* Dil kodunu değiştirerek Aspose tarafından desteklenen diğer dilleri keşfetmek; örneğin Çince ya da Arapça.

Kendi görüntülerinizle deneyin—ön işleme ayarlarını ayarlayın, farklı dosya formatlarıyla oynayın ve çözümün gerçek dünyadaki iş akışınızda ne kadar dayanıklı olduğunu görün.

İyi kodlamalar, OCR boru hatlarınız daima doğru sonuçlar versin!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}