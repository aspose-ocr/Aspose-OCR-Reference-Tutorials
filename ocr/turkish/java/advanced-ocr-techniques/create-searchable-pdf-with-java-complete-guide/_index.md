---
category: general
date: 2026-03-18
description: Aspose OCR kullanarak taranmış dosyalardan aranabilir PDF oluşturun.
  Taranmış PDF'yi nasıl dönüştüreceğinizi, PDF çözünürlüğünü nasıl ayarlayacağınızı
  öğrenin ve PDF'yi aranabilir hâle getirmeyi ustalaşın.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- how to convert pdf
- convert pdf to searchable
- set pdf resolution
language: tr
og_description: Aspose OCR kullanarak taranmış dosyalardan aranabilir PDF oluşturun.
  Bu öğreticide taranmış PDF'yi nasıl dönüştüreceğiniz, PDF çözünürlüğünü nasıl ayarlayacağınız
  ve aranabilir bir sonuç elde edeceğiniz gösterilmektedir.
og_title: Java ile Aranabilir PDF Oluşturma – Tam Kılavuz
tags:
- Java
- OCR
- PDF
- Aspose
title: Java ile Aranabilir PDF Oluşturma – Tam Kılavuz
url: /tr/java/advanced-ocr-techniques/create-searchable-pdf-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java ile Aranabilir PDF Oluşturma – Tam Kılavuz

Hiç **aranabilir PDF** oluşturmanız gerektiğinde, taranmış belgeler yığınıyla ne yapacağınızı bilemediniz mi? Tek başınıza değilsiniz—birçok geliştirici, yalnızca görüntü içeren PDF’leri metin‑aranabilir dosyalara dönüştürmeye çalışırken bu engelle karşılaşıyor. İyi haber? Birkaç satır Java kodu ve Aspose OCR kütüphanesiyle, **taranmış PDF**’yi saniyeler içinde aranabilir bir PDF’ye **dönüştürebilirsiniz**.  

Bu öğreticide, kütüphaneyi kurmaktan çözünürlüğü yapılandırmaya, dönüşümü gerçekleştirmeye kadar bilmeniz gereken her şeyi adım adım ele alacağız. Sonunda, kullanıcılarınızın terim arayabileceği, kopyalayabileceği ve indeksleyebileceği **aranabilir PDF** dosyaları oluşturabileceksiniz. Süslü bir giriş yok, sadece uygulanabilir, çalıştırılabilir bir örnek.

## Gereksinimler

Başlamadan önce şunların kurulu olduğundan emin olun:

- Java 17 veya daha yeni bir sürüm (kod modern `var` sözdizimini kullanıyor, ancak gerekirse daha eski bir sürüme geçebilirsiniz)
- Aspose OCR bağımlılığını çekmek için Maven ya da Gradle
- Tarama yapılmış bir PDF dosyası (herhangi bir çok sayfalı belge yeterli)
- Tercih ettiğiniz bir IDE veya metin editörü—IntelliJ IDEA harika çalışır, Eclipse de uygundur

Bu ön koşullar hazır olduğunda akış sorunsuz ilerleyecek—yolda kesinti yaşamayacaksınız.

## Adım 1: Aspose OCR’ı Projeye Ekleyin

İlk olarak OCR motorunu sınıf yoluna eklememiz gerekiyor. Maven kullanıyorsanız, aşağıdakileri `pom.xml` dosyanıza ekleyin:

```xml
<!-- Aspose OCR for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- latest as of 2026 -->
</dependency>
```

Gradle tercih edenler şunu ekleyebilir:

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

> **Pro ipucu:** En son sürüm için resmi Aspose Maven deposunu kontrol edin; yeni sürümler yüksek çözünürlüklü PDF’ler için performans iyileştirmeleri içerebilir.

## Adım 2: OCR Motorunu Başlatın

Kütüphane artık erişilebilir olduğuna göre, bir `OcrEngine` örneği oluşturuyoruz. Bu nesneyi, rasterleştirilmiş sayfaları okuyup pikselleri metne dönüştüren beyin olarak düşünebilirsiniz.

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.PdfRecognitionOptions;

/**
 * Demonstrates how to create a searchable PDF from a scanned source.
 */
public class PdfToSearchableDemo {

    public static void main(String[] args) throws Exception {
        // Step 2: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

Neden açık bir motor örneği oluşturuyoruz? Çünkü Aspose, OCR mantığını dosya‑işleme mantığından ayırarak dil paketleri ve tanıma modları gibi konularda ince ayar yapmanıza olanak tanıyor.

## Adım 3: PDF Çözünürlüğünü Yapılandırın – **set pdf resolution**

Çözünürlük, kütüphanenin her PDF sayfasını OCR motoruna vermeden önce rasterleştirdiği DPI (inç başına nokta) değeridir. Daha yüksek DPI, daha iyi metin doğruluğu sağlar ancak daha fazla bellek ve CPU süresi tüketir.

```java
        // Step 3: Configure PDF recognition options
        PdfRecognitionOptions pdfOptions = new PdfRecognitionOptions();
        pdfOptions.setPageRange(1, 5);      // optional: process pages 1‑5 only
        pdfOptions.setResolution(300);     // 300 DPI is a sweet spot for most scans
```

Eğer çok düşük kaliteli taramalarla çalışıyorsanız çözünürlüğü 400 DPI’ye çıkarın; büyük belgelerde hız öncelikli ise 200 DPI yeterli olabilir. `setPageRange` çağrısı isteğe bağlıdır—tüm dosyayı işlemek için bu satırı atlayabilirsiniz.

## Adım 4: Taranmış PDF’yi Aranabilir PDF’ye Dönüştürün – **convert scanned pdf**

İşte asıl kısım. `convertPdfToSearchablePdf` metodu üç argüman alır: kaynak yolu, hedef yolu ve az önce ayarladığımız seçenekler.

```java
        // Step 4: Convert the scanned PDF into a searchable PDF
        ocrEngine.convertPdfToSearchablePdf(
                "YOUR_DIRECTORY/scanned.pdf",      // input scanned PDF
                "YOUR_DIRECTORY/searchable.pdf",   // output searchable PDF
                pdfOptions);
```

Bu satır çalıştığında Aspose, her sayfayı rasterleştirir, OCR uygular ve orijinal görüntünün üzerine görünmez bir metin katmanı ekler. Ortaya çıkan dosya görsel olarak kaynakla aynı görünür, ancak artık içinde herhangi bir kelimeyi arayabilirsiniz.

## Adım 5: Sonucu Doğrulayın

Basit bir `System.out.println` çıktısı, dosyanın nereye kaydedildiğini gösterir. Program bittiğinde çıktıyı herhangi bir PDF okuyucusunda açın ve yerleşik aramayı (Ctrl + F) deneyin. Orijinal PDF sadece bir resim olsa bile eşleşmeler görmelisiniz.

```java
        // Step 5: Notify the user
        System.out.println("Searchable PDF created at YOUR_DIRECTORY/searchable.pdf");
    }
}
```

**Beklenen konsol çıktısı**

```
Searchable PDF created at YOUR_DIRECTORY/searchable.pdf
```

Ve taranan sayfalarda bulunan bir kelimeyi yazdığınızda görüntüleyici onu vurgular—bu da **aranabilir pdf oluşturduğunuzun** kanıtıdır.

## Adım 6: İsteğe Bağlı – Yalnızca Belirli Sayfaları Dönüştürmek

Bazen sadece bir alt küme (ör. 200 sayfalık bir sözleşmenin ilk on sayfası) aranabilir yapmak isteyebilirsiniz. Tek yapmanız gereken `setPageRange` çağrısını şu şekilde ayarlamak:

```java
pdfOptions.setPageRange(1, 10); // process only pages 1‑10
```

Diğer her şey aynı kalır. Bu küçük ayar, büyük arşivlerde saatler süren işlem süresinden tasarruf sağlayabilir.

## Adım 7: PDF’leri Aranabilir Formata Dönüştürme İçin En İyi Uygulamalar

- **Toplu işleme:** Eğer onlarca dosyanız varsa dönüşüm kodunu bir döngü içinde çalıştırın. Aynı `OcrEngine` örneğini yeniden kullanarak ek yükten kaçının.
- **Bellek yönetimi:** Çok büyük PDF’lerde JVM yığın boyutunu (`-Xmx2g` veya daha fazla) artırarak `OutOfMemoryError` hatasından korunabilirsiniz.
- **Dil desteği:** Varsayılan olarak Aspose OCR İngilizceyi algılar. Belgeleriniz İspanyolca, Fransızca vb. bir dildeyse, uygun dil paketini şu şekilde yükleyin: `ocrEngine.getLanguage().add(Language.Spanish);`.
- **Son‑işlem:** Dönüştürmeden sonra PDF’i sıkıştırmak isteyebilirsiniz (`PdfSaveOptions.setCompressionLevel`)—gizli metin katmanını kaybetmeden dosya boyutunu küçültür.

## Görsel Genel Bakış

Aşağıda taranmış bir PDF’den aranabilir bir PDF’ye akışı gösteren basit bir diyagram yer alıyor. Alt metin, ana anahtar kelimeyi içeriyor ve arama motorları ile AI modellerinin görsel bağlamı anlamasına yardımcı oluyor.

![Aranabilir PDF oluşturma örneği](https://example.com/images/create-searchable-pdf.png "aranabilir pdf iş akışı")

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.PdfRecognitionOptions;

/**
 * Complete, runnable example that demonstrates how to create a searchable PDF
 * from a scanned PDF using Aspose OCR for Java.
 */
public class PdfToSearchableDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Configure PDF recognition options
        PdfRecognitionOptions pdfOptions = new PdfRecognitionOptions();
        pdfOptions.setPageRange(1, 5);      // optional: limit to pages 1‑5
        pdfOptions.setResolution(300);     // set PDF resolution (DPI)

        // Convert the scanned PDF into a searchable PDF
        ocrEngine.convertPdfToSearchablePdf(
                "YOUR_DIRECTORY/scanned.pdf",
                "YOUR_DIRECTORY/searchable.pdf",
                pdfOptions);

        // Notify the user
        System.out.println("Searchable PDF created at YOUR_DIRECTORY/searchable.pdf");
    }
}
```

Sınıfı çalıştırın, yolları gerçek dosyalarınıza yönlendirin ve sihrin gerçekleşmesini izleyin. Temel bir dönüşüm için ek bir yapılandırma gerekmez.

## Sonuç

Artık Java ve Aspose OCR kullanarak taranmış kaynaklardan **aranabilir PDF** dosyaları **nasıl oluşturulacağını** tam olarak biliyorsunuz. Kütüphaneyi kurmak, motoru başlatmak, çözünürlüğü ayarlamak ve `convertPdfToSearchablePdf` metodunu çağırmak adımları basit ve kod, herhangi bir projeye kolayca eklenebilir.  

Eğer **taranmış pdf** dosyalarını toplu olarak **dönüştürmek** istiyorsanız, yukarıdaki toplu‑işleme ipuçlarını inceleyin ya da **convert pdf to searchable** seçenekleri arasında OCR dil paketleri ve sıkıştırma ayarlarıyla daha derine dalın. Bir sonraki adımda **pdf nasıl dönüştürülür** konusunu (DOCX, HTML vb.) keşfedebilir ya da çok‑dilli belgeler için OCR deneyebilirsiniz.

İyi kodlamalar, ve PDF’leriniz her zaman aranabilir olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}