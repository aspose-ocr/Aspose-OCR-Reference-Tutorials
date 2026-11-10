---
category: general
date: 2026-01-07
description: Aspose OCR'i Java'da kullanarak bir görüntüden aranabilir PDF oluşturun.
  Görüntüyü PDF'ye dönüştürmeyi, görüntüden metni tanımayı ve JPG'den PDF üretmeyi
  öğrenin.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- recognize text from image
- how to use ocr
- generate pdf from jpg
language: tr
og_description: Aspose OCR ile Java’da bir görüntüden aranabilir PDF oluşturun. Görüntüyü
  PDF’ye dönüştürmek, görüntüden metni tanımak ve JPG’den PDF üretmek için adım adım
  kılavuz.
og_title: Görüntüden Aranabilir PDF Oluşturma – Java OCR Rehberi
tags:
- OCR
- Java
- PDF
- Aspose
title: Görüntüden OCR ile Aranabilir PDF Oluşturma – Java Öğreticisi
url: /tr/java/ocr-operations/create-searchable-pdf-from-image-with-ocr-java-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüden Aranabilir PDF Oluşturma – Java Öğreticisi

Hiç taranmış bir fotoğraftan **aranabilir PDF** oluşturmanız gerekti, ancak nereden başlayacağınızı bilemediniz mi? Tek başınıza değilsiniz—bir JPEG'i gerçekten içinde arama yapabileceğiniz bir PDF'e dönüştürmeye çalışan birçok geliştirici bu engelle karşılaşıyor.  

Bu rehberde, **görüntüyü PDF'e dönüştürme**, **görüntüden metin tanıma** ve sonunda **JPG'den PDF oluşturma** işlemlerini Aspose OCR for Java kullanarak gösteren tam, çalıştırılabilir bir örnek üzerinden adım adım ilerleyeceğiz. Belirsiz referanslar yok, sadece bugün kopyalayıp çalıştırabileceğiniz kodlar.

## Gereksinimler

İlerlemeye başlamadan önce makinenizde aşağıdakilerin olduğundan emin olun:

* **Java 17** veya daha yeni bir sürüm (API, herhangi bir güncel JDK ile çalışır).  
* **Aspose.OCR for Java** kütüphanesi – en son JAR dosyasını Maven Central ya da Aspose web sitesinden alabilirsiniz.  
* Örnek bir görüntü, örneğin `sample.jpg`, referans alabileceğiniz bir klasöre yerleştirilmiş.  
* Bir IDE ya da basit bir metin editörü ve bir terminal—size uyan her şey.

Hepsi bu. Ağır çerçeveler, ekstra yerel bağımlılıklar yok. Hadi başlayalım.

## Adım 1 – Aranabilir PDF Oluşturma: OCR Motorunu Başlatma

İlk olarak bir `OcrEngine` örneği oluşturup kaynak görüntüyü ona yönlendiriyoruz. Bu nesne Aspose OCR'un kalbidir; bitmap'i yüklemekten tanınan metni ortaya çıkarmaya kadar her şeyi yönetir.

```java
import com.aspose.ocr.*;

public class HelloOcrTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the image you want to turn into a searchable PDF
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

> **Neden önemli:** Motoru doğru şekilde başlatmak, kütüphanenin beslediğiniz görüntü formatını okuyabilmesini sağlar. Yol hatalıysa `FileNotFoundException` alırsınız ve bütün işlem durur.

## Adım 2 – Performansı Artırma: GPU, Çok‑çekirdekli CPU ve Yazım Düzeltme

OCR, özellikle büyük belgelerde CPU‑ağırlıklıdır. Aspose, süreci daha hızlı ve daha doğru hâle getirmek için birkaç ayar sunar.

```java
        // 2️⃣ Turn on performance helpers – GPU, multi‑core CPU, and spell correction
        ocrEngine.getEngineOptions()
                 .setUseGpu(true)                 // uses GPU if one is available
                 .setUseMultiCore(true)           // spreads work across CPU cores
                 .setEnableSpellCorrection(true); // cleans up common OCR mistakes
```

> **İpucu:** GPU'suz bir sunucuda çalışıyorsanız `setUseGpu(false)` kullanmak zararlı olmaz—sadece çok‑çekirdekli CPU işleme geri döner.

## Adım 3 – Görüntü Kalitesini İyileştirme: Eğikliği Düzeltme ve Lekeleri Giderme (Opsiyonel ama Tavsiye Edilir)

Taramalar nadiren mükemmeldir. Küçük bir eğim ya da lekeler tanıma sürecini bozabilir. `ImageProcessingOptions` sınıfı, motorun okumaya başlamadan önce resmi temizlemenizi sağlar.

```java
        // 3️⃣ Pre‑process the image – straighten it and remove noise
        ocrEngine.getImageProcessingOptions()
                 .setDeskew(true)   // automatically rotates tilted text
                 .setDespeckle(true); // reduces background speckles
```

> **Köşe durumu:** Kaynak görüntünüz zaten temizse bu adımı atlayabilirsiniz. Zararı yoktur, sadece birkaç milisaniye ek yük getirir.

## Adım 4 – Görüntüden Metni Tanıma ve PDF Oluşturma

Şimdi sihir gerçekleşir. `recognize()` metodunu çağırıyoruz ve motor bir `OcrResult` döndürür. Buradan çıktıyı çeşitli formatlarda kaydedebiliriz—aranabilir belgeler için en yaygın format PDF’dir.

```java
        // 4️⃣ Perform OCR and get the result object
        OcrResult ocrResult = ocrEngine.recognize();

        // 5️⃣ Save the result as a searchable PDF (you could also choose TXT, DOCX, etc.)
        ocrResult.save("YOUR_DIRECTORY/sample-output.pdf", OcrOutputFormat.PDF);
    }
}
```

> **Gördükleriniz:** `sample-output.pdf` orijinal görüntüyü arka plan katmanı olarak içerirken, tanınan metin üstte görünmez bir katman olarak yer alır. Adobe Reader’da açıp metni seçmeyi deneyin—şaşıracaksınız.

## Adım 5 – Oluşturulan Aranabilir PDF’i Doğrulama

Dosya yazıldıktan sonra PDF’in gerçekten aranabilir olduğundan emin olmak iyi bir uygulamadır.

```java
import java.awt.Desktop;
import java.io.File;

public class VerifyPdf {
    public static void main(String[] args) throws Exception {
        File pdf = new File("YOUR_DIRECTORY/sample-output.pdf");
        if (pdf.exists() && Desktop.isDesktopSupported()) {
            Desktop.getDesktop().open(pdf); // opens the PDF in the default viewer
        } else {
            System.out.println("PDF not found or cannot be opened on this platform.");
        }
    }
}
```

PDF’i açın, **Ctrl F** tuşlayın, görüntüde kesinlikle bulunan bir kelimeyi yazın—arama bulursa **aranabilir pdf oluşturma** işlemini başarıyla tamamlamışsınız demektir!

## Gerçek Dünya Senaryolarında OCR Kullanımı (Bonus)

* **Toplu işleme:** Kodu, bir klasördeki JPG’ler üzerinde dönen bir döngüye sarın. Bellek kullanımını düşük tutmak için tek bir `OcrEngine` örneğini yeniden kullanmayı unutmayın.  
* **Dil desteği:** Aspose OCR 60’tan fazla dili destekler. Sadece `ocrEngine.getEngineOptions().setLanguage(Language.English);` (veya başka bir enum değeri) çağırın.  
* **Hata yönetimi:** Bozuk dosyaları nazikçe ele almak için `OcrException` yakalayın.  

Bu ince ayarlar, çözümünüzü üretim hatları için yeterince sağlam kılar.

## Tam Java Örneği – JPG’den Aranabilir PDF Oluşturma

Aşağıda, olduğu gibi derleyip çalıştırabileceğiniz tam, bağımsız program yer alıyor. `YOUR_DIRECTORY` kısmını makinenizdeki gerçek yol ile değiştirin.

```java
import com.aspose.ocr.*;

public class CreateSearchablePdf {
    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Load the source image
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));

        // -------------------------------------------------
        // 2️⃣ Performance helpers
        // -------------------------------------------------
        ocrEngine.getEngineOptions()
                 .setUseGpu(true)
                 .setUseMultiCore(true)
                 .setEnableSpellCorrection(true);

        // -------------------------------------------------
        // 3️⃣ Image pre‑processing (optional but helpful)
        // -------------------------------------------------
        ocrEngine.getImageProcessingOptions()
                 .setDeskew(true)
                 .setDespeckle(true);

        // -------------------------------------------------
        // 4️⃣ Run OCR and save as searchable PDF
        // -------------------------------------------------
        OcrResult result = ocrEngine.recognize();
        result.save("YOUR_DIRECTORY/sample-output.pdf", OcrOutputFormat.PDF);

        System.out.println("✅ Searchable PDF created at YOUR_DIRECTORY/sample-output.pdf");
    }
}
```

**Beklenen çıktı:**  

```
✅ Searchable PDF created at YOUR_DIRECTORY/sample-output.pdf
```

Oluşturulan PDF’i açın ve `sample.jpg` içinde yer alan herhangi bir kelimeyi arayabildiğinizi doğrulayın. Metin katmanını görmüyorsanız, görüntü yolunu ve OCR motorunun gizli bir istisna fırlatmadığını kontrol edin.

## Sonuç

Bir JPEG’den Aspose OCR for Java kullanarak **aranabilir PDF** oluşturmayı gösterdik. Görüntüyü yüklemek, performans ayarlarını ince ayarlamak, resmi temizlemek ve sonunda metni tanıyarak aranabilir bir PDF kaydetmek—her adımın *neden* ve *nasıl* olduğu açıklanmıştır.  

Artık kendi uygulamalarınızda **görüntüyü PDF'e dönüştürme**, **görüntüden metin tanıma** ve **JPG'den PDF oluşturma** yapabilirsiniz. Sonraki adım olarak, bir klasördeki tüm taramaları işleyebilir, farklı dillerle deneyebilir ya da çıktı PDF’ine şifre koruması ekleyebilirsiniz. Hayal gücünüz sınırsız.

Kenar durumları, lisanslama veya performans ayarlarıyla ilgili sorularınız mı var? Aşağıya yorum bırakın, iyi kodlamalar! 

![Diagram illustrating OCR pipeline – create searchable pdf](/images/ocr-pipeline.png "Create searchable PDF diagram")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}