---
category: general
date: 2026-03-07
description: Java OCR ile görüntüden metin çıkarın. OCR için görüntüyü nasıl yükleyeceğinizi,
  dili nasıl yapılandıracağınızı öğrenin ve dakikalar içinde tam bir Java OCR öğreticisini
  çalıştırın.
draft: false
keywords:
- extract text from image
- load image for ocr
- use OCR in java
- java ocr tutorial
language: tr
og_description: Java OCR kullanarak görüntüden metin çıkarın. Bu öğretici, OCR için
  bir görüntünün nasıl yükleneceğini, dilin nasıl yapılandırılacağını ve adım adım
  bir Java OCR öğreticisinin nasıl çalıştırılacağını gösterir.
og_title: Java'da Görüntüden Metin Çıkarma – Tam OCR Rehberi
tags:
- OCR
- Java
- Image Processing
title: Java'da Görüntüden Metin Çıkarma – Java OCR Öğreticisi
url: /tr/java/ocr-basics/extract-text-from-image-in-java-java-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüden Metin Çıkarma Java’da – Tam OCR Rehberi

Java’da **görüntüden metin çıkarma** ihtiyacı hiç duydunuz mu ama nereden başlayacağınızı bilemediniz mi? Tek başınıza değilsiniz—geliştiriciler taranmış işaretler, makbuzlar veya el yazısı notları aranabilir dizelere dönüştürürken sürekli bu duvara çarpıyor.  

İyi haber? Birkaç dakikada Kannada, İngilizce veya desteklenen herhangi bir dili okuyabilen çalışan bir OCR hattına sahip olabilirsiniz. Bu öğreticide **OCR için görüntü yükleme**, motoru yapılandırma ve **Java OCR öğreticisi**ni adım adım kopyalayıp bugün çalıştırabileceğiniz şekilde ele alacağız.

## Bu Kılavuzda Neler Kapsanıyor

Araçları listeleyerek başlayacağız, ardından **adım adım** uygulamaya geçeceğiz. Sonunda şunları yapabilecek duruma geleceksiniz:

* Bir Java `ImageInputStream`ine görüntü dosyası yükleme.
* Belirli bir dili (örneğimizde Kannada) tanıyacak şekilde OCR motorunu yapılandırma.
* Tanıma sürecini çalıştırma ve çıkarılan metni yazdırma.
* Doğruluğu artırmak için ayarları ince ayar yapma ve yaygın tuzakları ele alma.

Harici bir dokümantasyona gerek yok—gereken her şey burada.  

**Önkoşullar**: Java 17 veya daha yeni bir sürüm, Maven ya da Gradle gibi bir yapı aracı ve bir `OcrEngine` sınıfı sunan bir OCR kütüphanesi (örneğin, hayali *SimpleOCR* SDK). Maven kullanıyorsanız, aşağıda gösterilen bağımlılığı ekleyin.

---

## 1. Adım – Projenizi Kurun ve OCR Kütüphanesini Ekleyin

Kod yazmaya başlamadan önce projenizin OCR sınıflarını görebildiğinden emin olun. Maven ile bu snippet’i `pom.xml` dosyanıza ekleyin:

```xml
<!-- Maven dependency for SimpleOCR (replace with your actual OCR SDK) -->
<dependency>
    <groupId>com.example</groupId>
    <artifactId>simple-ocr</artifactId>
    <version>1.4.2</version>
</dependency>
```

Gradle tercih ediyorsanız eşdeğeri:

```gradle
implementation 'com.example:simple-ocr:1.4.2'
```

> **Pro ipucu:** Kütüphane sürümünü güncel tutun; yeni sürümler genellikle doğruluğu artıran dil‑model iyileştirmeleri içerir.

Bağımlılık çözüldükten sonra IDE’nizi yenileyin ve kod yazmaya hazırsınız.

## 2. Adım – Gerekli Sınıfları İçe Aktarın

Aşağıda örnek için ihtiyacınız olan tam import listesi yer alıyor. Bilinçli olarak minimal tutulmuştur, böylece her sınıfın ne işe yaradığını net görebilirsiniz.

```java
import com.example.ocr.OcrEngine;      // Main OCR engine
import com.example.ocr.OcrResult;      // Holds recognition result
import com.example.io.ImageInputStream; // Wrapper for image files
import java.nio.file.Paths;             // Convenient path handling
import java.io.IOException;             // For proper exception handling
```

> **Bu import’lar neden?** `OcrEngine` ve `OcrResult` OCR sürecinin kalbidir, `ImageInputStream` ise dosya okuma ayrıntılarını soyutlar. `java.nio.file.Paths` kullanmak kodun işletim sistemi bağımsız olmasını sağlar.

## 3. Adım – OCR İçin Görüntüyü Yükleyin

Şimdi çoğu kişinin takıldığı kısma geliyoruz: motorun doğru görüntü formatını alması. OCR SDK’sı bir `ImageInputStream` bekler; bunu disk üzerindeki herhangi bir dosyadan elde edebilirsiniz.

```java
// Step 3: Load the image that contains the text you want to extract
String imagePath = "YOUR_DIRECTORY/kannada_sign.jpg";
ImageInputStream imageStream = new ImageInputStream(Paths.get(imagePath));
```

> **Köşe durumu:** Görüntü bozuk ya da desteklenmeyen bir formatta (ör. GIF) ise yapıcı `IOException` fırlatır. Çağrıyı bir try‑catch bloğuna alın ya da dosyayı önceden doğrulayın.

## 4. Adım – Motoru Belirli Bir Dili Tanıyacak Şekilde Yapılandırın

Çoğu OCR motoru çok dilli desteğe sahiptir. Doğruluğu artırmak için motora tam olarak hangi dili araması gerektiğini söylemelisiniz. Biz örnek olarak Kannada için `"kn"` dil kodunu kullanıyoruz.

```java
// Step 4: Create and configure the OCR engine for Kannada
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getConfig().setLanguage("kn"); // 'kn' = Kannada
```

> **Dil ayarlaması neden?** Karakter setini sınırlamak, özellikle benzer gliflerin çok olduğu yazı sistemlerinde yanlış pozitifleri azaltır.

Dilleri değiştirmek isterseniz sadece kod dizesini değiştirin—başka bir değişiklik yapmanıza gerek yok.

## 5. Adım – OCR Sürecini Çalıştırın ve Metni Çıkarın

Görüntü yüklendi ve motor yapılandırıldı, gerçek tanıma tek bir metod çağrısıdır. Sonuç nesnesi size düz metni ve isteğe bağlı olarak güven skorlarını verir.

```java
// Step 5: Run OCR and retrieve the recognized text
OcrResult ocrResult = ocrEngine.recognize(imageStream);
String extractedText = ocrResult.getText();
```

> **Sık sorulan soru:** *OCR boş bir string döndürürse ne olur?*  
> Genellikle bu, görüntü kalitesinin çok düşük (bulanık, düşük kontrast) olması ya da dilin doğru ayarlanmamış olmasından kaynaklanır. Görüntüyü ön işleme (kontrast artırma, ikilileştirme) yapın ya da dil kodunu tekrar kontrol edin.

## 6. Adım – Sonucu Görüntüleyin

Son olarak çıktıyı konsola yazdırın. Gerçek bir uygulamada bunu bir veritabanına kaydedebilir veya bir arama indeksine besleyebilirsiniz.

```java
// Step 6: Output the recognized Kannada text
System.out.println("Extracted text:");
System.out.println(extractedText);
```

### Beklenen Çıktı

Kaynak görüntü “ಕರ್ನಾಟಕ” (Karnataka) ifadesini içeriyorsa, konsol şu şekilde görünmelidir:

```
Extracted text:
ಕರ್ನಾಟಕ
```

İşte bu kadar—herhangi bir dil veya görüntü kaynağına uyarlayabileceğiniz tam bir **Java’da OCR kullanma** iş akışı.

---

## Tam Çalışan Örnek

Aşağıda derlenmeye hazır tüm program yer alıyor. `YOUR_DIRECTORY` kısmını görüntü dosyanızın gerçek yolu ile değiştirin.

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrResult;
import com.example.io.ImageInputStream;
import java.nio.file.Paths;
import java.io.IOException;

public class KannadaOcrExample {
    public static void main(String[] args) {
        try {
            // Create OCR engine instance
            OcrEngine ocrEngine = new OcrEngine();

            // Configure for Kannada (language code "kn")
            ocrEngine.getConfig().setLanguage("kn");

            // Load the image you want to extract text from
            String imagePath = "YOUR_DIRECTORY/kannada_sign.jpg";
            ImageInputStream imageStream = new ImageInputStream(Paths.get(imagePath));

            // Run the OCR process
            OcrResult ocrResult = ocrEngine.recognize(imageStream);

            // Print the extracted text
            System.out.println("Extracted text:");
            System.out.println(ocrResult.getText());
        } catch (IOException e) {
            System.err.println("Failed to load image or run OCR: " + e.getMessage());
        } catch (Exception e) {
            System.err.println("Unexpected error during OCR: " + e.getMessage());
        }
    }
}
```

> **İpucu:** Üretim kodunda, birden çok görüntü için tek bir `OcrEngine` örneğini yeniden kullanmayı düşünün; sürekli yeniden oluşturmak maliyetli olabilir.

---

## Sık Sorulan Sorular & Köşe Durumları

### Gürültülü fotoğraflarda doğruluğu nasıl artırırım?
- **Ön‑işleme** yapın: görüntüyü gri tonlamaya çevirin, medyan filtre uygulayın veya kontrastı artırın.
- **Yeniden boyutlandırın**; en az 300 DPI olmalı; çoğu OCR motoru bu çözünürlüğü bekler.
- **Beyaz liste** oluşturun; beklenen çıktıyı (ör. sadece rakamlar) biliyorsanız karakter setini sınırlayın.

### Bu yaklaşımı PDF’ler için kullanabilir miyim?
Evet. Her sayfayı bir görüntü olarak çıkarın (PDFBox veya iText kullanarak), ardından bu görüntüleri aynı pipeline’a besleyin. Kod aynı kalır; sadece görüntü kaynağı değişir.

### Tek bir görüntüde birden fazla dili tanımam gerekirse?
Çoğu SDK, `"en,kn"` gibi virgülle ayrılmış bir liste almanıza izin verir. Motor sağlanan scriptlerden herhangi birini eşleştirmeye çalışır.

### Güven skorlarını almanın bir yolu var mı?
`OcrResult` genellikle her satır için 0 ile 1 arasında bir değer döndüren `getConfidence()` metoduna sahiptir. Düşük güvenilir sonuçları filtrelemek için bunu kullanabilirsiniz.

---

## Sonraki Adımlar

Java kullanarak **görüntüden metin çıkarma** yapabildiğinize göre şu konuları keşfedebilirsiniz:

* **Toplu işleme** – bir klasördeki tüm görüntüler üzerinde döngü kurup sonuçları CSV’ye yazın.
* **Apache Tika ile entegrasyon** – OCR’u belge ayrıştırmasıyla birleştirerek birleşik bir arama indeksi oluşturun.
* **Sunucu‑tarafı API** – OCR mantığını bir REST uç noktasına (Spring Boot bunu çok kolay yapar) açın.
* **Alternatif kütüphaneler** – açık kaynak bir çözüm gerekiyorsa `tess4j` üzerinden Tesseract’ı deneyin.

Bu konular, bu **java ocr tutorial**’da ele alınan temel kavramlar üzerine inşa edildiği için kodu deneyimleyip genişletmekten çekinmeyin.

---

## Sonuç

Java’da **görüntüden metin çıkarma** yapan tam bir örnek üzerinden geçtik; **OCR için görüntü yükleme**, dil ayarlarını yapılandırma ve **Java’da OCR kullanma** adımlarını adım adım gösterdik. Parçacık bağımsız, hataları zarifçe ele alıyor ve minimal çabayla herhangi bir Java projesine eklenebiliyor.  

Deneyin, dil kodunu ayarlayın ve kısa sürede taranmış belgeleri arama yapılabilir verilere dönüştürün. İyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}