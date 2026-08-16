---
category: general
date: 2026-04-26
description: Gürültüyü kaldırarak, görüntüleri düzleştirerek ve resmi metne dönüştürerek
  OCR doğruluğunu nasıl artıracağınızı öğrenin. Aspose OCR ile adım adım keşfedin.
draft: false
keywords:
- how to improve ocr
- how to remove noise
- how to extract text
- how to deskew image
- convert image to text
language: tr
og_description: Java'da OCR doğruluğunu artırma—gürültüyü kaldırma, görüntüleri eğrilik
  düzeltme ve Aspose OCR kullanarak görüntüyü metne dönüştürme.
og_title: Java'da Gelişmiş Ön İşleme ile OCR'yi Nasıl İyileştirirsiniz
tags:
- OCR
- Java
- Image Processing
title: Java'da Gelişmiş Ön İşleme ile OCR'ı Nasıl İyileştiririz
url: /tr/java/advanced-ocr-techniques/how-to-improve-ocr-with-advanced-preprocessing-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da Gelişmiş Ön İşleme ile OCR'ı Nasıl İyileştirirsiniz

Tarama dosyalarınız karışık göründüğünde **OCR sonuçlarını nasıl iyileştirebileceğinizi** hiç merak ettiniz mi? Belki belge döndürülmüş, grenli artefaktlarla dolu ya da okunamayacak kadar düşük kontrastlıdır. İyi haber şu ki, birkaç ön işleme adımı titrek bir görüntüyü temiz, makine‑okunur bir metne dönüştürebilir—büyüye gerek yok.

Bu öğreticide **gürültüyü nasıl kaldıracağınızı**, **görüntüyü nasıl düzleştireceğinizi** ve sonunda **metni nasıl çıkaracağınızı** (veya *görüntüyü metne dönüştürmeyi*) Aspose OCR for Java kullanarak adım adım göstereceğiz. Sonunda, gözle görülür şekilde daha iyi OCR doğruluğu sağlayan hazır bir programınız olacak.

## Gerekenler

- **Java Development Kit (JDK) 11+** – herhangi bir güncel sürüm yeterlidir.  
- **Aspose.OCR for Java** kütüphanesi (deneme sürümü test için çalışır).  
- Döndürülmüş, gürültülü veya düşük kontrastlı bir örnek görüntü (ör. `skewed_noisy.jpg`).  
- Bir IDE ya da basit bir metin düzenleyici; kodu sade tutacağız.

> **Pro tip:** Maven kullanıyorsanız, Aspose OCR bağımlılığını `pom.xml` dosyanıza ekleyin. Gradle tercih ediyorsanız aynı koordinatlar geçerlidir.

## Adım 1: Aspose OCR Motorunu Kurun – *OCR'ı Nasıl İyileştirirsiniz* Temelleri

İlk olarak bir `OcrEngine` örneği oluşturun. Bu nesne, her OCR işleminin giriş noktasıdır.

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

*Neden önemli:* Motor, Aspose'un görüntüyü nasıl yorumlayacağını belirleyen tüm ayarları tutar. Onsuz, **OCR'ı nasıl iyileştirirsiniz** sorusuna yanıt veren ön işleme hilelerini etkinleştiremezsiniz.

## Adım 2: Gelişmiş Görüntü Ön İşlemeyi Etkinleştirin – *OCR'ı Nasıl İyileştirirsiniz*'in Çekirdeği

Şimdi, **OCR'ı nasıl iyileştirirsiniz** sorusuna doğrudan yanıt veren dört ön işleme anahtarını açıyoruz: düzleştirme, gürültü giderme, kontrast genişletme ve ikilileştirme.

```java
        // Step 2: Turn on preprocessing features
        ImagePreprocessingSettings preprocessing = ocrEngine.getPreprocessingSettings();
        preprocessing.setDeskew(true);           // how to deskew image
        preprocessing.setDenoise(true);         // how to remove noise
        preprocessing.setContrastStretch(true); // boost contrast automatically
        preprocessing.setBinarize(true);        // Otsu binarization for clean black‑white
```

*Açıklama:*  
- **Deskew** görüntüyü otomatik olarak 0°'ye döndürür, böylece karakterler yatay olarak hizalanır.  
- **Denoise** lekeleri yumuşatan bir filtre uygular—*gürültüyü nasıl kaldıracağınız* sorusunun tam yanıtı.  
- **Contrast stretch** ton aralığını genişleterek soluk harflerin öne çıkmasını sağlar.  
- **Binarize** her pikseli siyah ya da beyaz yapar; klasik bir OCR ön koşuludur.

## Adım 3: Sorunlu Görüntüyü Yükleyin – *Metni Nasıl Çıkarırsınız* İçin Hazırlık

```java
        // Step 3: Point the engine at your source image
        ocrEngine.setImage("YOUR_DIRECTORY/skewed_noisy.jpg");
```

`YOUR_DIRECTORY` kısmını makinenizdeki gerçek yol ile değiştirin. Görüntü JPEG, PNG, BMP veya TIFF formatında olabilir—Aspose OCR hepsini destekler.

## Adım 4: OCR'ı Çalıştırın ve *Görüntüyü Metne Dönüştürün*

```java
        // Step 4: Perform OCR and capture the result
        String recognizedText = ocrEngine.recognize().getText();
```

Bu noktada motor, ön işleme hattını uyguladıktan sonra karakter tanıma yapar. `recognize()` çağrısı bir `OcrResult` nesnesi döndürür; `getText()` ise düz metin dizesini çıkarır—*Java'da görüntüyü metne nasıl dönüştürürsünüz* tam olarak budur.

## Adım 5: Temizlenmiş Sonucu Görüntüleyin – *Metni Nasıl Çıkarırsınız* Doğrulaması

```java
        // Step 5: Show the OCR output
        System.out.println("Result after advanced preprocessing:\n" + recognizedText);
    }
}
```

Programı çalıştırdığınızda aşağıdakine benzer bir çıktı görmelisiniz:

```
Result after advanced preprocessing:
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

Orijinal görüntü bulanık ve döndürülmüş bir tarama ise, çıktının artık okunaklı ve doğru sırada olduğunu fark edeceksiniz. Bu, **OCR'ı nasıl iyileştirirsiniz** kontrol listesini uygulamanın somut fayfasıdır.

---

## Gürültüyü Nasıl Kaldırırsınız – Daha Derin Bir Bakış

Gürültü, özellikle düşük çözünürlüklü taramalarda rastgele lekeler ya da gren olarak ortaya çıkar. `setDenoise(true)` bayrağı, her pikseli komşularının medyan değeriyle değiştiren bir medyan filtresi etkinleştirir. Pratikte, izole koyu lekeleri yumuşatırken kenarları korur.

**Ne zaman ayarlama yapmalı:** Kaynak görüntüleriniz zaten temizse, işleme süresini hızlandırmak için gürültü giderme özelliğini kapatabilirsiniz. Aksine, çok grenli fotoğraflar için Aspose'un gürültü giderimini özel bir OpenCV ön filtresiyle birleştirerek ekstra güç elde edebilirsiniz.

## Görüntüyü Nasıl Düzleştirirsiniz – Gerçeğe Geri Döndürme

Deskew algoritması, metin taban çizgisini analiz eder ve optimal döndürme açısını hesaplar. En az bir satır metin net bir şekilde görünürse en iyi çalışır. Görüntü sadece grafik içeriyorsa, Aspose'a vermeden önce elle döndürmeyi düşünün.

**Köşe durumu:** Bazı diller (ör. Arapça) sağ‑dan‑sol yönlendirmeye sahiptir. Deskew hâlâ çalışır, ancak yanlış döndürmeleri önlemek için dil ipucunu ayarlamanız (`ocrEngine.setLanguage(OcrLanguage.Arabic)`) gerekebilir.

## Metni Nasıl Çıkarırsınız – Düz Metinlerin Ötesinde

Ham metinden daha fazlasına ihtiyacınız varsa—ör. sınırlama kutuları, güven skorları veya kelime‑düzeyi konumlandırma—daha zengin `OcrResult` API'sını kullanın:

```java
OcrResult result = ocrEngine.recognize();
for (OcrWord word : result.getWords()) {
    System.out.printf("Word: %s, Confidence: %.2f%%, Box: %s%n",
        word.getText(), word.getConfidence() * 100, word.getRectangle());
}
```

Bu snippet, **metni nasıl çıkarırsınız** sorusuna yanıt olarak meta verileri de gösterir; aranabilir PDF'ler oluşturmak ya da belgeleri açıklamak için faydalıdır.

## Java'da Görüntüyü Metne Dönüştürmek – Hepsini Bir Araya Getirmek

Aşağıdaki tam, çalıştırılabilir örnek, tartıştığımız her şeyi birleştirir:

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {
        // Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Enable preprocessing (how to improve OCR)
        ImagePreprocessingSettings preprocessing = ocrEngine.getPreprocessingSettings();
        preprocessing.setDeskew(true);           // how to deskew image
        preprocessing.setDenoise(true);         // how to remove noise
        preprocessing.setContrastStretch(true);
        preprocessing.setBinarize(true);

        // Load the image you want to convert image to text from
        ocrEngine.setImage("YOUR_DIRECTORY/skewed_noisy.jpg");

        // Perform OCR
        String recognizedText = ocrEngine.recognize().getText();

        // Output the result
        System.out.println("Result after advanced preprocessing:\n" + recognizedText);
    }
}
```

Bunu `PreprocessDemo.java` olarak kaydedin, `javac` ile derleyin ve `java` ile çalıştırın. Konsola temizlenmiş metin yazdırılacaktır.

---

## Yaygın Tuzaklar ve Çözümleri

| Belirti | Muhtemel Neden | Çözüm |
|---------|----------------|------|
| Boş çıktı | Görüntü yolu yanlış veya desteklenmeyen format | Yolu kontrol edin, mutlak yol kullanın, dosyanın JPEG/PNG/TIFF olduğundan emin olun |
| Bozuk karakterler | Ön işleme kapalı veya dil ayarlanmamış | `setDeskew`, `setDenoise` etkinleştirin ve `ocrEngine.setLanguage(OcrLanguage.English)` ayarlayın |
| Büyük toplularda yavaş performans | Her görüntüde dört ön işleme adımı çalışıyor | Gerekmiyorsa `setContrastStretch` veya `setBinarize` kapatın, ya da görüntüleri paralel iş parçacıklarında işleyin |

---

## Sonraki Adımlar – OCR Boru Hattınızı Genişletmek

Artık **OCR'ı nasıl iyileştirirsiniz** bildiğinize göre şu ek fikirleri değerlendirebilirsiniz:

- **Toplu işleme:** Bir klasördeki tüm görüntüler üzerinde aynı ayarları döngüyle uygulayın.  
- **Son‑işleme:** Yaygın OCR hatalarını (ör. “0” vs “O”) temizlemek için düzenli ifadeler kullanın.  
- **PDF entegrasyonu:** Aspose OCR'ı Aspose PDF ile birleştirerek çıkarılan metni doğrudan aranabilir PDF'lere gömün.  
- **Dil desteği:** `ocrEngine.setLanguage(OcrLanguage.Spanish)` (veya desteklenen başka bir dil) ile çok‑dilli belgeleri işleyin.

---

## Sonuç

Java'da **OCR'ı nasıl iyileştirirsiniz** sorusunun tam yanıtını, deskew, denoise, contrast stretch ve binarization'ı Aspose `OcrEngine` içinde etkinleştirerek verdik. Artık **gürültüyü nasıl kaldırırsınız**, **görüntüyü nasıl düzleştirirsiniz**, **metni nasıl çıkarırsınız** ve hatta **görüntüyü metne nasıl dönüştürürsünüz** sorularının cevaplarını tek, öz bir programda biliyorsunuz. Ayarlarla oynayın, kendi taramalarınızda test edin ve tanıma doğruluğunda belirgin bir artış göreceksiniz.

OCR ipuçlarıyla ilgili daha fazla sorunuz varsa ya da bunu daha büyük bir uygulamaya entegre etmeniz gerekiyorsa, aşağıya yorum bırakın. Mutlu kodlamalar!  

![OCR ön işleme nasıl iyileştirilir](/images/ocr-preprocess-example.png "ocr nasıl iyileştirilir")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}