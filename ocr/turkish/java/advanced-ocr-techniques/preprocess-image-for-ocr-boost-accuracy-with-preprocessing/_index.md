---
category: general
date: 2026-05-31
description: Aspose OCR Java kullanarak ön işleme ile OCR doğruluğunu büyük ölçüde
  artırmak için görüntüyü ön işleyin. Tam bir adım‑adım kılavuzu izleyin.
draft: false
keywords:
- preprocess image for OCR
- improve OCR accuracy with preprocessing
language: tr
og_description: OCR için görüntüyü ön işleme tabi tutun ve Aspose OCR kullanarak Java’da
  ön işleme ile OCR doğruluğunu nasıl artıracağınızı öğrenin.
og_title: OCR için Görüntüyü Ön İşleme – Ön İşleme ile Doğruluğu Artırın
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Preprocess image for OCR to dramatically improve OCR accuracy with
    preprocessing using Aspose OCR Java. Follow a complete step‑by‑step guide.
  headline: Preprocess Image for OCR – Boost Accuracy with Preprocessing
  type: TechArticle
- description: Preprocess image for OCR to dramatically improve OCR accuracy with
    preprocessing using Aspose OCR Java. Follow a complete step‑by‑step guide.
  name: Preprocess Image for OCR – Boost Accuracy with Preprocessing
  steps:
  - name: Loads the original PNG.
    text: Loads the original PNG.
  - name: Feeds it through `AutoDeskew`, `DenoiseMedian`, and `ContrastStretch`.
    text: Feeds it through `AutoDeskew`, `DenoiseMedian`, and `ContrastStretch`.
  - name: Runs the recognizer on the cleaned bitmap.
    text: Runs the recognizer on the cleaned bitmap.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: OCR için Görüntüyü Ön İşleme – Ön İşleme ile Doğruluğu Artırın
url: /tr/java/advanced-ocr-techniques/preprocess-image-for-ocr-boost-accuracy-with-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR için Görüntüyü Ön İşleme – Ön İşleme ile Doğruluğu Artırın

Hiç merak ettiniz mi, OCR sonuçlarınız kaynağındaki resim iyi görünmesine rağmen karışık bir karmaşa gibi neden görünüyor? Çoğu durumda suçlu görüntünün içinde gizlidir—eğrilik, gürültü, düşük kontrast—akıllı tanıyıcıları bile zorlayan şeyler. **Preprocess image for OCR** ve kalite içinde dramatik bir artış göreceksiniz.  

Bu öğreticide sadece **preprocess image for OCR** nasıl yapılacağını göstermekle kalmayacağız, aynı zamanda Aspose OCR for Java ile küçük ama güçlü bir pipeline oluşturarak **how to improve OCR accuracy with preprocessing** nasıl yapılacağını da açıklayacağız. Sonunda, gürültülü, eğik bir PNG'yi temiz, okunabilir metne dönüştüren çalıştırmaya hazır bir programınız olacak.

## Öğrenecekleriniz

- OCR motorları için ön işlemenin neden önemli olduğu  
- Bir Java projesinde Aspose OCR'ı nasıl kuracağınız  
- Deskew, denoise ve contrast filtrelerini kullanarak **preprocesses image for OCR** yapan adım adım kod  
- Kendi veri setlerinizde **improve OCR accuracy with preprocessing** için pipeline'ı ayarlama ipuçları  

Süs yok, sadece eksiksiz, çalıştırılabilir bir örnek ve her satırın ardındaki mantık.

## Önkoşullar

| Requirement | Reason |
|-------------|--------|
| Java 8 or newer | Aspose OCR Java kütüphanesi Java 8+ hedefler |
| Maven or Gradle (optional) | Aspose OCR bağımlılığını eklemeyi basitleştirir |
| Aspose OCR for Java license file (`Aspose.OCR.Java.lic`) | Tam işlevselliği açmak için gereklidir |
| A sample image (e.g., `noisy_skewed.png`) | OCR için *preprocess image for OCR* yapacağınız resim |

Eğer bunlardan herhangi biri eksikse, şimdi durun ve temin edin—lisans olmadan kodu çalıştırmak sadece bir istisna fırlatır.

## Adım 1: Aspose OCR Lisansınızı Uygulayın

İlk iş olarak. OCR motoru geçerli bir lisans olmadan faydalı bir şey yapmaz. Bu adım **preprocesses image for OCR** dolaylı olarak tam görüntü filtresi setini açarak gerçekleştirir.

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {
        // Apply your Aspose OCR license
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");
```

> **Pro ipucu:** Lisans dosyasını sürüm kontrolünden uzak tutun. Üretimde ortam değişkenleri veya güvenli bir kasayı kullanın.

## Adım 2: OCR Motorunu Başlatın ve Kaynak Görüntüyü Yükleyin

Şimdi motoru oluşturuyor, beklediğimiz dili belirtiyor ve *preprocess image for OCR* yapmak istediğimiz dosyayı işaretliyoruz.

```java
        // Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Set the language – English works for most demos
        ocrEngine.setLanguage(OcrLanguage.ENGLISH);

        // Load the source image (the one that needs preprocessing)
        ocrEngine.setImage(new OcrImage("YOUR_DIRECTORY/noisy_skewed.png"));
```

Neden dili ayarlıyoruz? Çünkü motor dil‑spesifik sezgileri uygulayabilir ve bu zaten **improve OCR accuracy with preprocessing** yapmadan önce filtrelere dokunmadan fayda sağlar.

## Adım 3: Ön İşleme Pipeline'ı Oluşturun

Bu, öğreticinin kalbidir. Burada üç filtreyi zincirleyerek **preprocess image for OCR** yapıyoruz:

| Filter | Ne yapar | Doğruluk için neden önemlidir |
|--------|----------|-------------------------------|
| `AutoDeskew` | Dönüşü algılar ve düzeltir | Eğik metin satırları karakter segmentasyonunu karıştırır |
| `DenoiseMedian(3)` | Median filtre gürültü azaltma (kernel = 3) | Serseri karakter gibi görünen lekeleri kaldırır |
| `ContrastStretch` | Histogramı genişleterek kontrastı artırır | Karanlık arka planlar okunabilir hâle gelir, açık metin öne çıkar |

```java
        // Access the preprocessor
        OcrPreprocessor preprocessor = ocrEngine.getPreprocessor();

        // 1️⃣ Correct image skew
        preprocessor.addFilter(new AutoDeskew());

        // 2️⃣ Reduce noise with a median filter (kernel size = 3)
        preprocessor.addFilter(new DenoiseMedian(3));

        // 3️⃣ Enhance contrast for sharper edges
        preprocessor.addFilter(new ContrastStretch());
```

Görünüşe göre sıfırdan bir görüntü‑işleme kodu yazmamıza gerek yok—Aspose hazır filtreler sunar. Bu, uygulamayı özlü tutarken **improve OCR accuracy with preprocessing** dramatik bir şekilde artırır.

## Adım 4: Ön‑işlenmiş Görüntüde OCR Çalıştırın

Pipeline kurulduğunda, motor tanımadan önce filtreleri otomatik olarak uygular. Tek yapmanız gereken tek bir çağrı:

```java
        // Perform OCR on the pre‑processed image
        String extractedText = ocrEngine.recognize();
```

Motorun perde arkasında yaptığı işler:

1. Orijinal PNG'yi yükler.  
2. `AutoDeskew`, `DenoiseMedian` ve `ContrastStretch` üzerinden geçirir.  
3. Temizlenmiş bitmap üzerinde tanıyıcıyı çalıştırır.  

Bu, **preprocess image for OCR** sihiridir—ağır iş yükü soyutlanmıştır.

## Adım 5: Tanınan Metni Çıktı Olarak Verin

Son olarak, sonucu konsola yazdırın ya da bir dosyaya kaydedin. Demo amaçlı basit bir `System.out.println` iş görür.

```java
        // Show the extracted text
        System.out.println(extractedText);
    }
}
```

Her şey yolunda giderse, karışık bir karmaşa yerine temiz, okunabilir cümleler görmelisiniz. Tam çıktı kaynak görüntüye bağlıdır, ancak ham dosyada OCR çalıştırmaya kıyasla belirgin bir iyileşme fark edeceksiniz.

### Beklenen Çıktı (örnek)

```
The quick brown fox jumps over the lazy dog.
This is a sample text line for OCR testing.
```

Hâlâ garip karakterler alıyorsanız, filtre sırasını iki kez kontrol edin—bazen `ContrastStretch` *before* `DenoiseMedian` uygulamak, çok bozulmuş taramalarda daha iyi sonuç verir.

## Pipeline'ı Görselleştirme (Opsiyonel)

Aşağıda, görüntünün her filtre üzerinden nasıl aktığını gösteren bir şema bulunuyor. Bu, süreci ekip arkadaşlarınıza açıklamanıza ya da dokümantasyona eklemenize yardımcı olabilir.

![preprocess image for OCR diyagramı](pipeline.png "AutoDeskew → DenoiseMedian → ContrastStretch aşamalarını gösteren diyagram")

*Alt metin:* *preprocess image for OCR diyagramı, tanıma öncesinde uygulanan üç filtreyi gösterir.*

## Yaygın Tuzaklar ve Çözümleri

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| Metin hâlâ ön işlemden sonra bulanık | Kontrast filtresi yeterince güçlü değil | Stretch faktörünü artırın veya `HistogramEqualization` deneyin |
| OCR `NullPointerException` hatası veriyor | Lisans dosyası yolu yanlış | Yolu doğrulayın ve dosyanın okunabilir olduğundan emin olun |
| Eğrilik hâlâ var | Görüntü dönüşü > 15° (AutoDeskew sınırı) | Pipeline'dan önce `AffineTransform` kullanarak manuel olarak ön‑döndürün |
| Çok fazla yanlış pozitif | Gürültü seviyesi yüksek, kernel boyutu çok düşük | Median kernel'ini yükseltin (ör. `new DenoiseMedian(5)`) |

Bu sorunları önceden tahmin ederek, en zorlu taramalarda bile **improve OCR accuracy with preprocessing** yapabilirsiniz.

## Pipeline'ı Genişletmek

Daha fazla kontrol mü istiyorsunuz? Aspose OCR, özel filtreler eklemenize ya da mevcut olanları yeniden sıraya koymanıza izin verir. İşte birkaç fikir:

- **Binarizasyon**: `preprocessor.addFilter(new BinarizeOtsu());` – saf siyah‑beyaz zorlar, basılı belgeler için faydalıdır.  
- **Yeniden Boyutlandırma**: `preprocessor.addFilter(new Scale(2.0));` – düşük çözünürlüklü görüntüleri büyütür, genellikle doğruluğu artırır.  
- **Keskinleştirme**: `preprocessor.addFilter(new Sharpen());` – küçük fontlar için kenarları vurgular.  

Unutmayın, her ek filtre işleme süresini artırır, bu yüzden hedef donanımınızda benchmark yapın.

## Tam Kaynak Kodu (Kopyala‑Yapıştır Hazır)

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Apply your Aspose OCR license
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // Step 2: Create the OCR engine and configure language & source image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setLanguage(OcrLanguage.ENGLISH);
        ocrEngine.setImage(new OcrImage("YOUR_DIRECTORY/noisy_skewed.png"));

        // Step 3: Build a preprocessing pipeline to improve OCR accuracy with preprocessing
        OcrPreprocessor preprocessor = ocrEngine.getPreprocessor();
        preprocessor.addFilter(new AutoDeskew());               // Correct image skew
        preprocessor.addFilter(new DenoiseMedian(3));           // Reduce noise (kernel size = 3)
        preprocessor.addFilter(new ContrastStretch());         // Enhance contrast

        // Step 4: Perform OCR on the pre‑processed image
        String extractedText = ocrEngine.recognize();

        // Step 5: Output the recognized text
        System.out.println(extractedText);
    }
}
```

Bunu `PreprocessDemo.java` olarak kaydedin, Aspose OCR JAR dosyasını sınıf yolunuza ekleyin (ya da Maven'de deklar edin) ve çalıştırın:



## Sonra Ne Öğrenmelisiniz?

- [Aspose.OCR Kullanarak Dil ile Görüntü Metnini OCR Yapma](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Aspose.OCR Detect Areas Modu ile Java'da Görüntüden Metin Çıkarma](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Aspose.OCR Kullanarak Java'da Eğrilik Açısını Hesaplama](/ocr/english/java/ocr-basics/calculate-skew-angle/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}