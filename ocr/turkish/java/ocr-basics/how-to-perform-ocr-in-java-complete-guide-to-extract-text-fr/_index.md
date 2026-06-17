---
category: general
date: 2026-06-06
description: Java’da OCR nasıl yapılır – görüntüden hızlıca metin çıkarma, görüntüyü
  metne dönüştürme ve basit bir kod örneğiyle jpg’den metin okuma.
draft: false
keywords:
- how to perform OCR
- ocr in java
- extract text from image
- convert image to text
- read text from jpg
language: tr
og_description: Java'da OCR nasıl yapılır – görüntüden metin çıkarma, görüntüyü metne
  dönüştürme ve jpg'den metin okuma konularını hazır‑çalıştırılabilir bir örnekle
  öğrenin.
og_title: Java'da OCR Nasıl Yapılır – Adım Adım Rehber
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: how to perform OCR in Java – quickly extract text from image, convert
    image to text, and read text from jpg using a simple code example.
  headline: How to Perform OCR in Java – Complete Guide to Extract Text from Images
  type: TechArticle
- description: how to perform OCR in Java – quickly extract text from image, convert
    image to text, and read text from jpg using a simple code example.
  name: How to Perform OCR in Java – Complete Guide to Extract Text from Images
  steps:
  - name: What You’ll Learn
    text: '- Install an OCR library (yes, **ocr in java** is easier than you think).
      - Create and configure an OCR engine instance. - Load a JPG (or any image) and
      set the language. - Process the image and **extract text from image** files.
      - Print the recognized string to the console.'
  - name: Expected Output
    text: 'If `input.jpg` contains the Mongolian phrase “Сайн байна уу?” the console
      will show:'
  - name: 'Pro Tip: Batch Processing'
    text: 'If you need to **extract text from image** files in bulk, wrap the core
      logic in a loop:'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Java'da OCR Nasıl Yapılır – Görsellerden Metin Çıkarma İçin Tam Rehber
url: /tr/java/ocr-basics/how-to-perform-ocr-in-java-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da OCR Nasıl Yapılır – Görsellerden Metin Çıkarma Tam Kılavuzu

Telefonunuzla çektiğiniz bir fotoğrafta **how to perform OCR** yapmayı hiç merak ettiniz mi? Tek başınıza değilsiniz. İster bir fiş tarama uygulaması geliştiriyor olun, ister taranmış bir PDF'den metin çıkarmanız gerekiyor olsun, Java'da **how to perform OCR** bir beceridir ve hızlıca karşılığını alır. Bu öğreticide, **extracts text from image** dosyalarından metin çıkarmayı, **converts image to text** işlemini ve hatta sadece birkaç satır kodla **read text from jpg** nasıl yapılır gösteren pratik bir örnek üzerinden ilerleyeceğiz.

> *Pro tip:* Aynı yaklaşım PNG, BMP veya OCR motorunun desteklediği herhangi bir format için çalışır—sadece dosya adını değiştirin.

## Java'da OCR Nasıl Yapılır – Genel Bakış

Optik Karakter Tanıma (OCR), harf resimlerini gerçek, aranabilir metne dönüştüren teknolojidir. Java ekosisteminde Tesseract, Asprise ve ticari SDK'lar gibi çeşitli kütüphaneler bulunur; hepsi benzer bir iş akışı sunar: bir görüntü yükleyin, motorun hangi dili bekleyeceğini belirtin, tanıma işlemini çalıştırın ve sonucu alın. Aşağıda örneği net tutmak için genel bir `OcrEngine` sınıfı kullanacağız, ancak aynı deseni izleyen herhangi bir somut uygulama ile değiştirebilirsiniz.

### Öğrenecekleriniz

- Bir OCR kütüphanesi kurun (evet, **ocr in java** düşündüğünüzden daha kolay).
- Bir OCR motoru örneği oluşturun ve yapılandırın.
- Bir JPG (veya herhangi bir görüntü) yükleyin ve dili ayarlayın.
- Görüntüyü işleyin ve **extract text from image** dosyalarından metin çıkarın.
- Tanınan dizeyi konsola yazdırın.

Sonunda, herhangi bir projeye ekleyebileceğiniz ve anında çalıştırabileceğiniz bağımsız bir Java programına sahip olacaksınız.

![how to perform OCR example](ocr-example.png "how to perform OCR in Java illustration")

## Adım 1 – Bir OCR Kütüphanesi Kurun ve İçe Aktarın (ocr in java)

Java kodu yazmadan önce, işi gerçekten yapan bir kütüphaneye ihtiyacınız var. Maven kullanıyorsanız, aşağıdaki gibi bir bağımlılık ekleyin (`com.example.ocr` kısmını seçtiğiniz SDK'nın gerçek grup kimliğiyle değiştirin):

```xml
<dependency>
    <groupId>com.example</groupId>
    <artifactId>ocr-sdk</artifactId>
    <version>1.4.2</version>
</dependency>
```

Gradle tercih ediyorsanız:

```gradle
implementation 'com.example:ocr-sdk:1.4.2'
```

JAR sınıf yolunda yer aldığında, ihtiyacınız olan sınıfları içe aktarın:

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrInputImage;
import com.example.ocr.OcrResult;
```

> **Neden önemli:** Doğru sınıfları içe aktarmak “cannot find symbol” hatalarını önler ve IDE'nizi mutlu eder—**convert image to text** yapmaya çalışırken eksik bir import kadar sinir bozucu bir şey yoktur.

## Adım 2 – OCR Motoru Örneğini Oluşturun (how to perform OCR)

Kütüphane hazır olduğuna göre, motoru başlatın. Motoru, piksellere bakıp harfleri tahmin edecek beyin olarak düşünün.

```java
// Step 2: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

Motoru oluşturmak genellikle ucuzdur; çoğu SDK iç tamponları tembel bir şekilde tahsis eder, bu yüzden bir toplu işlem yapıyorsanız aynı örneği birçok görüntüde güvenle yeniden kullanabilirsiniz.

## Adım 3 – Görüntüyü Yükleyin ve Dili Ayarlayın (extract text from image)

Sonraki adım, motora okuyacak bir şey vermektir. Burada bir JPEG'i disktan yüklüyor ve OCR motoruna metnin Moğolca (ISO 639‑2 kodu “mon”) olduğunu söylüyoruz. Yol ya da dil kodunu kullanım durumunuza göre değiştirebilirsiniz.

```java
// Step 3: Load the image you want to recognize
ocrEngine.setImage(new OcrInputImage("YOUR_DIRECTORY/input.jpg"));

// Step 3b: Specify the language (e.g., English = "eng", Mongolian = "mon")
ocrEngine.getSettings().setLanguage("mon");
```

> **Not:** Bir dil ayarlamazsanız, motor varsayılan olarak İngilizceyi kullanır; metin aslında Kiril alfabesi ya da başka bir yazı sistemi ise doğruluk büyük ölçüde düşebilir. Mümkün olduğunda doğru dili her zaman belirtin.

## Adım 4 – Görüntüyü İşleyin ve Sonucu Alın (convert image to text)

Görüntü ve dil ayarları yapıldıktan sonra, motorun sihrini çalıştırın. `process()` çağrısı OCR algoritmasını çalıştırır ve tanınan dizeyi ve güven skorlarını içeren bir `OcrResult` nesnesi döndürür.

```java
// Step 4: Process the image and obtain the recognition result
OcrResult ocrResult = ocrEngine.process();
```

Arka planda motor, ön işleme—eğrilik düzeltme, ikilileştirme, gürültü azaltma—yapabilir, böylece bu adımları kendiniz yazmak zorunda kalmazsınız. Bu yüzden çoğu modern OCR kütüphanesi **convert image to text** görevleri için kullanımı keyifli kılar.

## Adım 5 – Çıkarılan Metni Çıktılayın (read text from jpg)

Son olarak, sonuçtan düz metni alın ve bununla bir şeyler yapın. Bu demo için sadece konsola yazdırıyoruz, ancak bir dosyaya yazabilir, bir arama indeksine besleyebilir ya da başka bir servise gönderebilirsiniz.

```java
// Step 5: Output the extracted text
System.out.println(ocrResult.getText());
```

Bu satır, **read text from jpg** (veya desteklenen herhangi bir format) işlemini başarıyla gerçekleştirdiğinizi kanıtlar. Çıktı bozuk görünüyorsa, dil kodunu ve görüntü kalitesini tekrar kontrol edin.

## Tam Çalışan Örnek (Tüm Adımlar Birleştirildi)

Aşağıda, tüm parçaları bir araya getiren eksiksiz, çalıştırmaya hazır bir Java sınıfı bulunuyor. `OcrDemo.java` adlı bir dosyaya kopyalayın, görüntü yolunu ve dili ayarlayın, ardından `javac OcrDemo.java && java OcrDemo` komutunu çalıştırın.

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrInputImage;
import com.example.ocr.OcrResult;

/**
 * Demonstrates how to perform OCR in Java using a generic OCR SDK.
 * This example loads a JPG, sets the language to Mongolian, and prints
 * the recognized text to the console.
 *
 * Replace the import package with the actual library you are using.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Validate command‑line arguments
        if (args.length < 2) {
            System.err.println("Usage: java OcrDemo <image-path> <language-code>");
            System.exit(1);
        }

        String imagePath = args[0];   // e.g., "input.jpg"
        String language = args[1];    // e.g., "mon" for Mongolian

        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image
        ocrEngine.setImage(new OcrInputImage(imagePath));

        // Step 3: Set the language (ISO‑639‑2)
        ocrEngine.getSettings().setLanguage(language);

        // Step 4: Run the recognition
        OcrResult result = ocrEngine.process();

        // Step 5: Print the extracted text
        System.out.println("=== Recognized Text ===");
        System.out.println(result.getText());
    }
}
```

### Beklenen Çıktı

Eğer `input.jpg` Moğolca “Сайн байна уу?” ifadesini içeriyorsa, konsol şu çıktıyı gösterir:

```
=== Recognized Text ===
Сайн байна уу?
```

Eğer görüntü bulanıksa veya dil kodu yanlışsa, bozuk karakterler veya boş bir dize göreceksiniz—sonraki bölümde ele alacağımız yaygın tuzaklar.

## Yaygın Tuzaklar ve Çözümleri

| Belirti | Muhtemel Neden | Çözüm |
|---------|----------------|-------|
| Bozuk Kiril karakterleri | Yanlış dil kodu (varsayılan olarak İngilizce) | `ocrEngine.getSettings().setLanguage("mon")` ya da uygun kodu ayarlayın. |
| Hiç çıktı yok | Görüntü yolu hatalı veya dosya okunamıyor | Yolu doğrulayın, dosyanın var olduğundan ve işlemin okuma izinlerine sahip olduğundan emin olun. |
| Düşük doğruluk (<%70) | Görüntü düşük kontrastlı veya döndürülmüş | Görüntüyü ön işleyin: kontrastı artırın, eğriliği düzeltin veya motorun önüne göndermeden önce gri tonlamaya dönüştürün. |
| Büyük PDF'lerde `OutOfMemoryError` | Birçok yüksek çözünürlüklü sayfayı aynı anda yüklemek | Sayfaları tek tek işleyin veya OCR'den önce görüntüleri küçültün. |

### Pro Tip: Toplu İşleme

Eğer toplu olarak **extract text from image** dosyalarından metin çıkarmanız gerekiyorsa, temel mantığı bir döngü içinde sarın:

```java
for (File img : new File("batchFolder").listFiles()) {
    ocrEngine.setImage(new OcrInputImage(img.getAbsolutePath()));
    OcrResult r = ocrEngine.process();
    System.out.println(r.getText());
}
```

Bu snippet, tek bir JPG'den bir klasör içindeki tüm taramalara ölçeklendirmenin ne kadar kolay olduğunu gösterir.

## Daha İleri – Sonraki Keşifler

- **Language Packs:** Çoğu OCR SDK'sı ek dil veri dosyaları indirmenize izin verir. Yeni bir paket eklemek, İngilizce ve Moğolcadan daha fazla dil için **convert image to text** yapmanızı sağlar.
- **PDF OCR:** Bu kodu Apache PDFBox ile birleştirerek

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalar içeren eksiksiz çalışan kod örnekleri sunar.

- [Metin Görsellerini Çıkar – Aspose.OCR for Java ile OCR Temelleri](/ocr/english/java/ocr-basics/)
- [Java'da Aspose.OCR BufferedImage Kullanarak Görüntüyü Metne Dönüştür](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Aspose.OCR Kullanarak Dil ile Görüntü Metnini OCR Yapma](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}