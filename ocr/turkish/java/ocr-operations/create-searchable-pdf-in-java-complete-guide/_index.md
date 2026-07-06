---
category: general
date: 2026-07-05
description: Aspose OCR kullanarak Java’da aranabilir PDF oluşturun. PDF’deki görüntüleri
  nasıl sıkıştıracağınızı, taranmış görüntüyü PDF’ye nasıl dönüştüreceğinizi ve daha
  küçük dosyalar için PDF’de font gömülmesini nasıl devre dışı bırakacağınızı öğrenin.
draft: false
keywords:
- create searchable pdf
- compress images in pdf
- convert scanned image to pdf
- disable font embedding pdf
language: tr
og_description: Aspose OCR ile Java’da aranabilir PDF oluşturun. Bu öğreticide PDF’deki
  görüntüleri sıkıştırma, taranmış görüntüyü PDF’ye dönüştürme ve PDF’de yazı tipi
  gömülmesini devre dışı bırakma gösterilmektedir.
og_title: Java’da Aranabilir PDF Oluşturma – Adım Adım Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create searchable PDF in Java using Aspose OCR. Learn how to compress
    images in PDF, convert scanned image to PDF, and disable font embedding PDF for
    smaller files.
  headline: Create Searchable PDF in Java – Complete Guide
  type: TechArticle
tags:
- Java
- OCR
- PDF
title: Java’da Aranabilir PDF Oluşturma – Tam Kılavuz
url: /tr/java/ocr-operations/create-searchable-pdf-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java’da Aranabilir PDF Oluşturma – Tam Kılavuz

Hiç taranmış bir belgeden **create searchable PDF** oluşturmanız gerekti, ancak “bunu nasıl yaparım” kısmında takıldıysanız? Yalnız değilsiniz. Birçok projede, bir TIFF veya JPEG’i gerçekten arayabileceğiniz bir PDF’ye dönüştürmek *olmazsa olmaz* bir özelliktir, özellikle **compress images in PDF** yaparak dosya boyutlarını yönetilebilir tutmak istediğinizde.  

Bu öğreticide, Aspose OCR for Java kullanarak uygulamalı bir örnek üzerinden ilerleyeceğiz. Sonunda **convert scanned image to PDF** nasıl yapılır, **compress images in PDF** ayarını nasıl ayarlarsınız ve hatta **disable font embedding PDF** ile birkaç ekstra kilobaytı nasıl azaltırsınız tam olarak bileceksiniz. Gereksiz şey yok—sadece bugün kod tabanınıza ekleyebileceğiniz eksiksiz, çalıştırılabilir bir çözüm.

## Öğrenecekleriniz

- Java projesinde Aspose OCR motorunu kurun.  
- Bir TIFF üzerinde (veya herhangi bir raster görüntü) OCR gerçekleştirin.  
- `PdfSaveOptions` yapılandırarak **compress images in PDF** ve **disable font embedding PDF**.  
- Sonucu **searchable PDF** olarak kaydedin; böylece anında indeksleyebilir veya arayabilirsiniz.  

**Önkoşullar**  
- Java 8 veya daha yeni bir sürüm yüklü.  
- Bağımlılık yönetimi için Maven veya Gradle (Maven örneğini göstereceğiz).  
- İşlenecek bir taranmış görüntü dosyası (TIFF, PNG veya JPEG).  

Eğer bunlara sahipseniz, başlayalım.

![Aranabilir PDF oluşturma iş akışı – Java OCR'dan PDF dönüşümü](/images/create-searchable-pdf-workflow.png "Aspose OCR ile aranabilir PDF oluşturma adımlarını gösteren diyagram")

## Adım 1: Aspose OCR Bağımlılığını Ekleyin

İlk olarak, Aspose OCR kütüphanesini projenize ekleyin. Maven kullanıyorsanız, bunu `pom.xml` dosyanıza ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Gradle tercih ediyorsanız, eşdeğeri şudur:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Pro tip:** Aspose sürüm notlarını takip edin; yeni sürümler genellikle OCR doğruluğu için performans artışı sağlar.

## Adım 2: OCR Motorunu Başlatın

`OcrEngine` nesnesini örnekleyerek bir OCR motoru oluşturmak çok basittir. Bu nesne, görüntü yüklemeden metin çıkarımına kadar her şeyi yönetecek.

```java
import com.aspose.ocr.OcrEngine;

// ...

// Step 2: Create an OCR engine instance
OcrEngine engine = new OcrEngine();
```

Neden ayrı bir motora ihtiyacımız var? Aspose, ağır işleri (görüntü ön işleme, dil modelleri) uygulamanızın geri kalanından ayırır, böylece aynı `engine` nesnesini birden fazla dosyada yeniden başlatmadan yeniden kullanabilirsiniz.

## Adım 3: Taranmış Görüntüde OCR Gerçekleştirin

Şimdi motoru taranmış bir dosyayla besliyoruz. `recognizeImage` yöntemi, çıkarılan metin ve düzen bilgilerini tutan bir `RecognitionResult` döndürür.

```java
import com.aspose.ocr.RecognitionResult;

// ...

// Step 3: Perform OCR on the source image
String sourcePath = "YOUR_DIRECTORY/document_scan.tif"; // could be .png or .jpg too
RecognitionResult result = engine.recognizeImage(sourcePath);
```

> **Görüntü TIFF değilse ne olur?**  
> Aspose OCR, yaygın raster formatlarını otomatik olarak algılar, bu yüzden kodu değiştirmeden JPEG, PNG veya BMP'ye yönlendirebilirsiniz.

## Adım 4: PDF Kaydetme Seçeneklerini Yapılandırın (Görüntüleri Sıkıştır ve Yazı Tipi Gömmeyi Devre Dışı Bırak)

İşte ikincil anahtar kelimelerin parladığı yer. Aspose'a **compress images in PDF** ve **disable font embedding PDF** yapmasını söyleyeceğiz. Her iki ayar da nihai dosya boyutunu azaltır—birçok belge gönderdiğinizde kullanışlıdır.

```java
import com.aspose.ocr.pdf.PdfSaveOptions;

// ...

// Step 4: Set up PDF save options
PdfSaveOptions pdfOpts = new PdfSaveOptions();

// Reduce PDF size by compressing images
pdfOpts.setCompressImages(true);
pdfOpts.setImageQuality(80); // 0‑100, 80 is a good balance

// Prevent fonts from being embedded – saves a few KB per page
pdfOpts.setEmbedFonts(false);
```

**Neden görüntüleri sıkıştırıyoruz?**  
Taranmış sayfalar genellikle yüksek çözünürlüktedir; kaliteyi %80'e düşürmek, 10 sayfalık bir PDF'i 12 MB'den 3 MB'nin altına, görsel kayıp olmadan küçültebilir.

**Neden yazı tipi gömmeyi devre dışı bırakıyoruz?**  
OCR motoru standart sistem yazı tiplerini (Arial veya Times New Roman gibi) kullanıyorsa, bunları gömmek gereksizdir. Devre dışı bırakmak dosya boyutunu daha da azaltır, özellikle büyük toplularda.

## Adım 5: OCR Sonucunu Aranabilir PDF Olarak Kaydedin

Son adım her şeyi birleştirir: ham görüntü, çıkarılan metin katmanı ve az önce ayarladığımız PDF seçenekleri.

```java
// Step 5: Save the OCR result as a searchable PDF
String outputPath = "YOUR_DIRECTORY/document.pdf";
engine.saveAsSearchablePdf(outputPath, pdfOpts);

System.out.println("Searchable PDF created at: " + outputPath);
```

`document.pdf` dosyasını Adobe Reader veya herhangi bir modern görüntüleyicide açtığınızda, orijinal taranmış görüntüyü **artı** görünmez bir metin katmanı olarak göreceksiniz. Arama kutusuna bir kelime yazmak eşleşmeleri vurgular—tam da “create searchable pdf”in vaat ettiği gibi.

### Beklenen Çıktı

Geçerli bir TIFF ile programı çalıştırdığınızda aşağıdakine benzer bir çıktı alırsınız:

```
Searchable PDF created at: YOUR_DIRECTORY/document.pdf
```

PDF'i açın, `Ctrl+F` tuşlarına basın, taranmış sayfada bulunan bir kelimeyi yazın ve doğru konuma atladığını izleyin. Bu, başarılı bir **create searchable pdf** iş akışının işaretidir.

## Yaygın Tuzaklar ve Nasıl Kaçınılır

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Boş PDF** | `PdfSaveOptions` `saveAsSearchablePdf`'e geçirilmedi. | `PdfSaveOptions` kabul eden aşırı yüklemeyi (overload) çağırdığınızdan emin olun. |
| **Bozuk karakterler** | OCR dili ayarlanmamış (varsayılan İngilizce). | `recognizeImage`'den önce `engine.getLanguage().setLanguage(OcrLanguage.FRENCH);` kullanın. |
| **Aşırı büyük dosya boyutu** | `setCompressImages(false)` veya `setEmbedFonts(true)`. | Yukarıda gösterildiği gibi her iki bayrağı da açık tutun. |
| **Görüntü bozulması** | `setImageQuality` çok düşük ayarlandı (<50). | İyi bir denge için 70‑90 arasında tutun. |

## Örneği Genişletmek

Artık **convert scanned image to PDF** yapabildiğinize ve boyutu kontrol edebildiğinize göre, şunları yapmak isteyebilirsiniz:

- **Batch process** bir klasördeki taramaları basit bir `for(File f : folder.listFiles())` döngüsüyle işleyin.  
- Aspose PDF (`PdfDocument.addWatermarkText`) kullanarak **watermarks** ekleyin.  
- OCR metnini indeksleme sistemleri için **plain .txt** dosyasına (`result.getText().writeToFile("doc.txt")`) dışa aktarın.  

Bu uzantıların tümü aynı `OcrEngine` örneğini yeniden kullanır, bellek kullanımını düşük tutar.

## Tam, Çalıştırmaya Hazır Kod

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.pdf.PdfSaveOptions;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Step 2: Perform OCR on the source image
        String source = "YOUR_DIRECTORY/document_scan.tif";
        RecognitionResult result = engine.recognizeImage(source);

        // Step 3: Configure PDF save options (compress images & disable fonts)
        PdfSaveOptions pdfOpts = new PdfSaveOptions();
        pdfOpts.setCompressImages(true);      // Reduce PDF size by compressing images
        pdfOpts.setImageQuality(80);          // Image quality (0‑100)
        pdfOpts.setEmbedFonts(false);         // Do not embed fonts to keep file size small

        // Step 4: Save the OCR result as a searchable PDF
        String output = "YOUR_DIRECTORY/document.pdf";
        engine.saveAsSearchablePdf(output, pdfOpts);

        // Step 5: Inform the user that the PDF has been created
        System.out.println("Searchable PDF created at: " + output);
    }
}
```

Bunu IDE'nize kopyalayıp yapıştırın, `YOUR_DIRECTORY`'yi gerçek bir yol ile değiştirin ve çalıştırın. Her şey doğru ayarlandıysa, **searchable PDF** elde edeceksiniz; aynı zamanda görüntü sıkıştırması ve devre dışı bırakılmış yazı tipi gömme sayesinde hafif olacaktır.

## Sonuç

Aspose OCR kullanarak Java’da **create searchable pdf** dosyaları oluşturmak için bilmeniz gereken her şeyi yeni kapsadık. Motoru başlatmaktan OCR yapmaya, **compress images in pdf** ve **disable font embedding pdf** ayarlarını ince ayarlamaya, sonunda aranabilir bir belge kaydetmeye kadar—her adım nedenini açıklayarak anlatıldı.  

Bir sonraki meydan okumaya hazır mısınız? OCR dil paketleri eklemeyi, tüm klasörleri toplu işlemeyi veya PDF'leri ek açıklamalarla katmanlamayı deneyin. Şimdi öğrendiğiniz temeller bu uzantıları çok kolay hale getirecek.  

Sorularınız mı var ya da kendi ipuçlarınızı paylaşmak mı istiyorsunuz? Aşağıya yorum bırakın, iyi kodlamalar!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [PDF Metnini Tanıma – Aspose.OCR for Java ile OCR İşlemleri](/ocr/english/java/ocr-operations/)
- [Aspose.OCR for Java'da PDF Belgelerini OCR ile Tanıma](/ocr/english/java/ocr-operations/recognize-pdf/)
- [.NET'te Aspose.OCR ile PDF OCR Nasıl Yapılır](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}