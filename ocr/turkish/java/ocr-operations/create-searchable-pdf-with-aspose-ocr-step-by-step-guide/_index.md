---
category: general
date: 2026-01-02
description: Aspose OCR kullanarak taranmış görüntü PDF'sinden aranabilir PDF oluşturun.
  OCR dilini ayarlamayı, bir metin katmanı PDF'si eklemeyi ve yüksek sıkıştırmalı
  PDF seçeneklerini uygulamayı öğrenin.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- high compression pdf
- embed text layer pdf
- set OCR language
language: tr
og_description: Aranabilir PDF'yi hızlıca oluşturun. Bu kılavuz, taranmış görüntü
  PDF'sini nasıl dönüştüreceğinizi, bir metin katmanı ekleyeceğinizi, OCR dilini ayarlayacağınızı
  ve yüksek sıkıştırmalı PDF'yi etkinleştireceğinizi gösterir.
og_title: Aspose OCR ile Aranabilir PDF Oluşturma – Tam Kılavuz
tags:
- Aspose OCR
- Java PDF
- Document Automation
title: Aspose OCR ile Aranabilir PDF Oluşturma – Adım Adım Kılavuz
url: /tr/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Searchable PDF Oluşturma – Tam Programlama Öğreticisi

Hiç **create searchable PDF** dosyaları oluşturmanız gerekti, ancak nereden başlayacağınızı bilmiyor muydunuz? Yalnız değilsiniz. Birçok belge‑ağır iş akışında, yalnızca görüntü içeren bir PDF, arama ve indeksleme için bir çıkmazdır.  

İyi haber şu ki, Aspose OCR ile sadece birkaç Java satırıyla **convert scanned image PDF**'yi tamamen aranabilir bir belgeye dönüştürebilirsiniz. Bu öğretici, her adımı size gösterir—OCR motorunu başlatma, yüksek sıkıştırmalı PDF ayarlarını yapılandırma, gizli bir metin katmanı gömme ve hatta doğru OCR dilini seçme.

Bu rehberin sonunda, aranabilir bir PDF üreten çalıştırılabilir bir programınız olacak; bu dosyayı herhangi bir arama motoruna ya da belge yönetim sistemine sorunsuz bir şekilde ekleyebilirsiniz.

---

## Searchable PDF Oluşturma – Genel Bakış

Koda dalmadan önce, “create searchable PDF” ifadesinin gerçekte ne anlama geldiğini açıklığa kavuşturalım. Searchable PDF iki paralel katman içerir:

1. **Visual layer** – orijinal taranmış görüntü (veya render edilmiş sayfa).  
2. **Text layer** – görünmez ancak OCR tarafından çıkarılan makine‑okunabilir karakterler.

Böyle bir PDF'yi Adobe Reader'da açıp metni seçtiğinizde, aslında resimle değil, gizli metin katmanıyla etkileşimde bulunursunuz. Bu çift‑katman yaklaşımı, **embed text layer PDF** işlevselliğini mümkün kılar.

## Aspose OCR Kullanarak Convert Scanned Image PDF Dönüştürme

İhtiyacınız olan ilk şey, PDF'ye dönüştürmek istediğiniz bir taranmış görüntüdür (PNG, JPEG, TIFF). Aspose OCR bu görüntüyü okuyabilir, OCR çalıştırabilir ve sonucu bir PDF yazarına aktarabilir.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialize the OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Step 2: Configure PDF save options to embed a searchable text layer
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // enable searchable PDF
        pdfSaveOptions.setCompressionLevel(9);        // optional: high compression

        // Step 3: Perform OCR on the scanned image and save the result as a searchable PDF
        ocrEngine.recognizeImageAndSave(
                "YOUR_DIRECTORY/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,                // set OCR language
                "YOUR_DIRECTORY/output.pdf",                // output PDF file
                pdfSaveOptions);                            // options defined above

        // Step 4: Indicate that the PDF has been created
        System.out.println("Searchable PDF created.");
    }
}
```

**Neden bu çalışıyor:**  
- `setCreateSearchablePdf(true)` Aspose'a gizli metin katmanını oluşturmasını söyler, **embed text layer pdf** gereksinimini karşılar.  
- `setCompressionLevel(9)` dosyayı **high compression pdf** aralığına iter, OCR doğruluğundan ödün vermeden son boyutu küçültür.  
- `RecognitionLanguage.ENGLISH` argümanı, **set OCR language** nasıl yapılacağını gösterir; kaynak materyalinize bağlı olarak bunu Fransızca, Almanca vb. ile değiştirebilirsiniz.

## Yüksek Sıkıştırmalı PDF Ayarları

Büyük taranmış PDF'ler hızla yüzlerce megabayta çıkabilir. Aspose, PDF seviyesinde çalışan basit bir sıkıştırma API'si sunar. `setCompressionLevel` yöntemi 0 (sıkıştırma yok) ile 9 (maksimum sıkıştırma) arasında değer alır.  

```java
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
pdfSaveOptions.setCompressionLevel(9); // 9 = strongest compression
```

- **Use lossless image formats** (PNG) metin‑ağır taramalar için; JPEG fotoğraflar için daha iyidir.  
- **Enable font subsetting** özel yazı tipleri gömüyorsanız—Aspose, searchable PDF oluşturduğunuzda bunu otomatik olarak yapar.  
- **Test the output size** her değişiklikten sonra; bazen seviye‑8 sıkıştırma, seviye‑9'a kıyasla %10'luk bir boyut azaltması sağlar ve kalite kaybı ihmal edilebilir.

## Aranabilirlik İçin Text Layer PDF'yi Gömme

`setCreateSearchablePdf(true)` çağrısını atlayarsanız, ortaya çıkan dosya iyi görünecek ancak içeriğini arayamayacaksınız. Gizli metin katmanı, tanınan her karakteri sayfadaki konumuna eşleyerek oluşturulur.  

```java
pdfSaveOptions.setCreateSearchablePdf(true);
```

- **Mixed‑language documents** – her dil için OCR'ı iki kez çalıştırmanız ve ardından metin katmanlarını birleştirmeniz gerekebilir.  
- **Complex layouts** (tablolar, çok‑sütunlu) – Aspose işini iyi yapar, ancak çıktıyı gizli metni gösteren bir PDF görüntüleyiciyle (ör. Adobe Acrobat’ın “Edit PDF” modu) iki kez kontrol edin.

## Doğru Tanıma İçin OCR Dilini Ayarlama

OCR motorunun doğruluğu, ona beklediği dili söylemenize bağlıdır. Aspose, yerleşik dillerin bir setiyle gelir ve ayrıca özel dil paketleri ekleyebilirsiniz.

```java
ocrEngine.recognizeImageAndSave(
        "input.png",
        RecognitionLanguage.ENGLISH, // change to RecognitionLanguage.FRENCH, etc.
        "output.pdf",
        pdfSaveOptions);
```

- Belgeler **Latin dışı yazı sistemleri** (Kiril, Arapça) içeriyorsa – uygun `RecognitionLanguage`'a geçin.  
- Karışık dil sayfaları – `recognizeImageAndSave` metodunu iki kez, her seferinde farklı bir dil ile çağırabilir ve ardından PDF'leri birleştirebilirsiniz.

## Tam Örneği Çalıştırma

Aşağıda tam, çalıştırmaya hazır program yer alıyor. Yer tutucu yolları gerçek dosya konumlarıyla değiştirin, Aspose OCR JAR dosyasının sınıf yolunuzda olduğundan emin olun ve çalıştırın.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Initialize OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Configure PDF save options
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // embed text layer PDF
        pdfSaveOptions.setCompressionLevel(9);        // high compression PDF

        // Perform OCR and save searchable PDF
        ocrEngine.recognizeImageAndSave(
                "C:/scans/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,          // set OCR language
                "C:/output/searchable.pdf",           // output PDF
                pdfSaveOptions);                      // options defined above

        System.out.println("Searchable PDF created.");
    }
}
```

**Expected output:** Programı çalıştırdığınızda, konsol şu çıktıyı verir:

```
Searchable PDF created.
```

`searchable.pdf` dosyasını herhangi bir PDF görüntüleyicide açın, metin seçmeyi deneyin ve gizli katmanın çalıştığını göreceksiniz. Taranmış bir görüntüden **create searchable pdf** işlemini başarıyla gerçekleştirdiniz.

![searchable pdf örneği oluşturma](image-placeholder.png "searchable pdf örneği oluşturma")

*Yukarıdaki ekran görüntüsü (yer tutucu) genellikle taranmış bir sayfa üzerinde seçilebilir metin gösteren bir PDF görüntüleyiciyi gösterir.*

## Sonuç

Aspose OCR kullanarak **create searchable PDF** dosyaları oluşturmak için bilmeniz gereken her şeyi ele aldık:

- OCR motorunu başlatın.  
- PNG/JPEG'i `recognizeImageAndSave` metoduna vererek **Convert scanned image PDF** yapın.  
- `setCreateSearchablePdf(true)` kullanarak **embed text layer PDF** oluşturun.  
- `setCompressionLevel(9)` uygulayarak hafif kalan bir **high compression PDF** elde edin.  
- En yüksek doğruluk için doğru `RecognitionLanguage` seçerek **set OCR language** ayarlayın.

Buradan, toplu işleme, farklı dillere ya da birden fazla taranmış sayfayı tek bir searchable PDF'ye birleştirmeye deneyebilirsiniz. Aynı desen, İspanyolca veya Japonca gibi diğer diller için de çalışır—sadece `RecognitionLanguage` enum'ını değiştirin.

Herhangi bir sorunla karşılaşırsanız yorum bırakmaktan çekinmeyin ve mutlu kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}