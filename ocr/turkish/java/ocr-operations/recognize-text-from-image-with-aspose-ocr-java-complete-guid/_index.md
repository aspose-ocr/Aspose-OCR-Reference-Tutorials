---
category: general
date: 2026-03-18
description: Aspose OCR kullanarak Java’da görüntüden metin tanımayı öğrenin. Bu adım‑adım
  öğretici, OCR için görüntünün nasıl yükleneceğini ve yazım düzelticisinin nasıl
  kapatılacağını gösterir.
draft: false
keywords:
- recognize text from image
- load image for ocr
- aspose ocr java example
- extract text from image
- turn off spell corrector
language: tr
og_description: Aspose OCR kullanarak Java’da görüntüden metin tanıyın. Bu pratik
  öğreticide OCR için görüntüyü nasıl yükleyeceğinizi ve yazım düzelticiyi nasıl kapatacağınızı
  öğrenin.
og_title: Aspose OCR Java ile Görüntüden Metin Tanıma – Tam Kılavuz
tags:
- Aspose OCR
- Java
- Image Processing
title: Aspose OCR Java ile Görüntüden Metin Tanıma – Tam Kılavuz
url: /tr/java/ocr-operations/recognize-text-from-image-with-aspose-ocr-java-complete-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR Java ile Görüntüden Metin Tanıma – Tam Kılavuz

Hiç **görüntüden metin tanıma** ihtiyacı duydunuz ama hangi kütüphaneyi seçeceğinizi bilemediniz mi? Yalnız değilsiniz. Gerçek dünyadaki birçok projede—makbuz tarama, formları dijitalleştirme veya ekran görüntülerinden altyazı çekme gibi—bir bitmap’ten temiz, ham metin elde etmek günlük bir mücadele.  

Bu öğreticide, **Aspose OCR Java örneği** üzerinden **OCR için görüntü yükleme**, motoru çalıştırma ve gerektiğinde **imla düzelticiyi kapatma** adımlarını adım adım göstereceğiz. Sonunda, istenmeyen düzenlemeler olmadan görüntüden metin çıkaran çalıştırılabilir bir programınız olacak.

## Öğrenecekleriniz

- Java için **Aspose OCR** iş akışının net bir resmi.
- **Görüntüden metin tanıma** ve **görüntüden metin çıkarma** için gereken tam kod.
- Dahili imla düzelticiyi ne zaman devre dışı bırakmanız gerektiği ve bunu güvenli bir şekilde nasıl yapacağınız.
- Çıktının beklentilerinize uygun olup olmadığını doğrulamak için hızlı bir kontrol.

### Ön Koşullar (asgari gereksinimler)

- Makinenizde yüklü Java 8 veya daha yeni bir sürüm.
- Bağımlılık yönetimi için Maven ya da Gradle (Maven örneğini göstereceğiz).
- `Aspose.OCR` JAR dosyası (Aspose web sitesinden ücretsiz deneme sürümünü alabilirsiniz).
- Okumak istediğiniz metni içeren bir görüntü dosyası (PNG, JPG, BMP vb.). Demo için `mixed-lang.png` dosyasını kullanacağız.

> **Pro ipucu:** Çok sayıda görüntü işleyecekseniz, dosya tanıtıcı sızıntılarını önlemek için görüntüleri akış (stream) olarak yüklemeyi düşünün.

---

![Görüntüden metin tanıma adımlarını gösteren OCR işlem hattı diyagramı](ocr-pipeline.png)

*Alt metin: Aspose OCR kullanarak görüntüden metin tanıma adımlarını gösteren diyagram.*

## Adım 1 – Projeyi Kurun ve Aspose OCR Bağımlılığını Ekleyin

OCR metodlarını çağırmadan önce kütüphanenin sınıf yolunda (classpath) olması gerekir. Maven kullanıyorsanız, aşağıdakini `pom.xml` dosyanıza ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Gradle tercih ediyorsanız eşdeğeri şu şekildedir:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

Bağımlılık çözüldükten sonra ihtiyacımız olan iki sınıfı içe aktarabiliriz:

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.Image;
```

> **Neden önemli:** JAR’ı bir yapı aracıyla eklemek, doğru sürümün tüm ortamlar arasında kullanılmasını sağlar ve “class not found” hatalarını ortadan kaldırır.

## Adım 2 – OCR Motorunu Oluşturun ve İmla Düzelticiyi Kapatın

Aspose OCR, yazdığınız şeyi tahmin etmeye çalışan dahili bir imla düzelticiyle gelir. Bu, temiz belgeler için harika, ancak çok dilli tabelalar ya da kod parçacıkları taradığınızda istemediğiniz “düzeltmeler”le karşılaşırsınız. İşte devre dışı bırakma yöntemi:

```java
// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Disable the automatic spell correction
ocrEngine.getSpellCorrector().setEnabled(false);
```

**Arka planda ne oluyor?** `SpellCorrector` nesnesi, ham glifler çözüldükten sonra sözlük tabanlı bir geçiş uygular. `setEnabled(false)` çağırarak motorun bu geçişi atlamasını ve algıladığı karakter dizisini olduğu gibi korumasını sağlarız.

## Adım 3 – OCR İçin Görüntüyü Yükleyin

Şimdi gerçekten **OCR için görüntü yükleme** işlemini yapacağız. Aspose’un `Image.load` metodu bir dosya yolu, bir `InputStream` ya da bir bayt dizisi kabul eder. Basitlik açısından dosya yolunu kullanacağız:

```java
// Replace the path with the location of your image file
Image inputImage = Image.load("YOUR_DIRECTORY/mixed-lang.png");
```

> **Köşe durumu:** Görüntü 5 MB’dan büyükse önce ölçeklendirmeyi düşünün. Büyük görüntüler bellek tüketimini artırır ve tanıma motorunu yavaşlatabilir.

## Adım 4 – Metni Tanıyın ve Ham Çıktıyı Yakalayın

Motor hazır ve görüntü bellekteyken, gerçek tanıma tek satırda gerçekleşir:

```java
// Perform OCR and store the raw text
String rawText = ocrEngine.recognize(inputImage);
```

`recognize` metodu, **görüntüden metin çıkarma** işlemini motorun gördüğü şekilde—imla kontrolü ve son işleme olmadan—içeren bir `String` döndürür.

## Adım 5 – Sonucu Görüntüleyin (İmla Kontrolü Yok)

Son olarak, ham OCR çıktısını konsola yazdıralım ki doğrulayabilesiniz:

```java
System.out.println("Raw OCR (no spell‑check):\n" + rawText);
```

Programı çalıştırdığınızda aşağıdakine benzer bir şey görmelisiniz:

```
Raw OCR (no spell‑check):
Hello, 世界!
12345
```

Görüntü karışık diller veya özel semboller içeriyorsa, imla düzelticiyi kapattığımız için değişmeden görüneceklerdir.

## Tam, Çalıştırılabilir Örnek

Tüm parçaları bir araya getirdiğimizde, **tam Aspose OCR Java örneği** aşağıdadır; `SpellCorrectionDemo.java` dosyasına kopyalayıp yapıştırabilirsiniz:

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.Image;

public class SpellCorrectionDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Turn off the built‑in spell corrector
        ocrEngine.getSpellCorrector().setEnabled(false);

        // Step 3: Load the image you want to recognize
        Image inputImage = Image.load("YOUR_DIRECTORY/mixed-lang.png");

        // Step 4: Run OCR on the image and obtain the raw text
        String rawText = ocrEngine.recognize(inputImage);

        // Step 5: Display the OCR result without spell‑checking
        System.out.println("Raw OCR (no spell‑check):\n" + rawText);
    }
}
```

### Nasıl Çalıştırılır

1. Dosyayı `SpellCorrectionDemo.java` olarak kaydedin.
2. Derleyin: `javac -cp "path/to/aspose-ocr-23.9.jar" SpellCorrectionDemo.java`
3. Çalıştırın: `java -cp ".;path/to/aspose-ocr-23.9.jar" SpellCorrectionDemo`

`path/to` kısmını sisteminizdeki Aspose JAR dosyasının gerçek konumuyla değiştirin.

## Yaygın Sorular & Dikkat Edilmesi Gerekenler

### Görüntü farklı bir formatta (ör. PDF) ise ne olur?

Aspose OCR, PDF sayfalarını doğrudan okuyabilir, ancak önce PDF sayfasını bir görüntüye dönüştürmeniz ya da `OcrEngine.recognizePdf` aşırı yüklemesini (overload) kullanmanız gerekir. Bu ayrı bir öğreticidir, ancak aynı **görüntüden metin tanıma** prensibi geçerlidir.

### İmla düzelticiyi devre dışı bırakmak performansı etkiler mi?

Biraz. Sözlük geçişinin atlanması sayfa başına birkaç milisaniye tasarruf sağlar; binlerce dosya işlediğinizde bu birikerek fark yaratabilir. Ancak otomatik yazım hatası düzeltmelerini kaybedersiniz—bu yüzden veri kalitenize göre karar verin.

### Dil‑özgü sonuçlar alabilir miyim?

Evet. Motor otomatik olarak betiği (script) algılar, ancak `ocrEngine.setLanguage(OcrEngine.Language.English)` gibi bir çağrı yaparak dili zorlayabilirsiniz. Görüntünün yalnızca tek bir dil içerdiğini biliyorsanız doğruluğu artırmak için faydalıdır.

### Çok sayfalı TIFF’leri nasıl işlerim?

Her sayfayı ayrı bir `Image` nesnesi olarak ele alın: `Image.load("file.tif", pageIndex)`. Sayfalar üzerinde döngü kurun, her birini tanıyın ve sonuçları birleştirin.

## Gerçek Dünya Projeleri İçin Pro İpuçları

- **Toplu işleme:** OCR mantığını bir `InputStream` kabul eden bir metoda sarın. Böylece S3, Azure Blob veya başka bir depolama alanından dosya sistemine dokunmadan akış olarak görüntü alabilirsiniz.
- **Bellek yönetimi:** İşiniz bittiğinde `ocrEngine.dispose()` çağırarak yerel kaynakları serbest bırakın.
- **Loglama:** Ham çıktıyı denetim izleri için bir log dosyasına kaydedin—özellikle imla düzelticiyi kapattığınızda bu çok önemlidir.
- **Test:** Bilinen bir görüntüyü besleyen ve beklenen ham dizeyi doğrulayan bir birim testi yazın. Böylece gelecekteki kütüphane güncellemeleri davranışı sessizce değiştirmez.

## Sonuç

Aspose OCR for Java kullanarak **görüntüden metin tanıma**, **OCR için görüntü yükleme** ve **imla düzelticiyi kapatma** adımlarını gösterdik. Yukarıdaki kısa, bağımsız kod parçacığı herhangi bir Java projesine eklenmeye hazır ve açıklamalar her satırın “neden”ini ortaya koyuyor.

Sonraki adımda, **görüntüden toplu metin çıkarma**, dil ipuçlarıyla deneyler yapma veya çıktıyı bir arama indeksine entegre etme üzerine çalışabilirsiniz. Ne seçerseniz seçin, burada ele aldığımız temeller OCR hattınızı güvenilir ve bakımını kolay tutacaktır.

Deneyimlerinizi paylaşmak ister misiniz? Lütfen bir yorum bırakın ya da kendi **Aspose OCR Java örneğinizi** paylaşın. İyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}