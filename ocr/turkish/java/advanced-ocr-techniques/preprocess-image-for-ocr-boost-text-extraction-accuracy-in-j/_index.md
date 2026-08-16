---
category: general
date: 2026-03-28
description: OCR için resmi ön işleyin ve Aspose OCR ile görüntüden metni tanıyın.
  Fotoğraftan metin çıkarma, OCR doğruluğunu artırma ve ön işleme adım adım nasıl
  yapılır öğrenin.
draft: false
keywords:
- preprocess image for OCR
- recognize text from image
- extract text from photo
- improve OCR accuracy preprocessing
- Aspose OCR Java
- image preprocessing pipeline
language: tr
og_description: Görüntüyü OCR için ön işleme tabi tutun ve Aspose OCR Java ile fotoğraftan
  metin çıkarın. OCR doğruluğunu artırmak için sadece birkaç adımda bu öğreticiyi
  izleyin.
og_title: OCR için Görüntüyü Ön İşleme – Tam Java Rehberi
tags:
- OCR
- Java
- Image Processing
title: OCR için Görüntüyü Ön İşleme – Java’da Metin Çıkarma Doğruluğunu Artırın
url: /tr/java/advanced-ocr-techniques/preprocess-image-for-ocr-boost-text-extraction-accuracy-in-j/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüyü OCR için Ön İşleme – Tam Bir Java Rehberi

Görüntüyü OCR için **preprocess image for OCR** yapmayı hiç denediniz mi ve hâlâ bozuk çıktı mı aldınız? Yalnız değilsiniz. Birçok gerçek‑dünya projesinde, ham bir tarama ya da akıllı telefon fotoğrafı eğim, gürültü veya düşük kontrast içerir ve bu da en akıllı tanıma motorunu bile şaşırtır. İyi haber? Kısa bir ön işleme hattı—de‑skew, denoise, binarize—**improve OCR accuracy preprocessing** büyük ölçüde artırabilir.

Bu öğreticide, Aspose OCR for Java kullanarak **recognize text from image** işlemini tam olarak gösteren bir uygulamalı örnek üzerinden ilerleyeceğiz. Sonunda **extract text from photo** dosyalarından çok daha az hata ile metin çıkarabilecek ve her bir ön işleme adımının neden önemli olduğunu anlayacaksınız.

> **Ne kazanacaksınız**  
> * Eğimli bir fotoğrafı yükleyen, üç klasik filtre uygulayan ve temiz metin yazdıran tamamen çalıştırılabilir bir Java programı.  
> * de‑skew, denoise ve binarize işlemlerinin “neden”ine dair içgörü.  
> * Köşe durumlarıyla başa çıkmak için ipuçları—büyük dosyalar, farklı görüntü formatları ve özel filtre sıralaması.

## Ön Koşullar

- Java 8 veya daha yeni bir sürüm kurulu (kod JDK 11 ile de derlenir).  
- Aspose OCR kütüphanesini çekmek için Maven veya Gradle.  
- `angled-photo.jpg` gibi hafif döndürülmüş ve biraz görsel gürültü içeren bir örnek görüntü.  
- Java’nın `main` metoduna temel aşinalık—derin OCR uzmanlığı gerektirmez.

Eğer bunlardan herhangi birine sahip değilseniz, Oracle veya OpenJDK'dan en son JDK'yı edinin ve `pom.xml` dosyanıza aşağıdaki Maven bağımlılığını ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check Maven Central for the newest version -->
</dependency>
```

Şimdi, koda dalalım.

## Adım 1 – OCR Motoru Örneğini Oluşturma

İhtiyacınız olan ilk şey bir `OcrEngine` nesnesidir. Bunu, daha sonra işlenmiş görüntüyü okuyacak beyin olarak düşünün.

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // Initialize the OCR engine – this object holds all settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **Why this matters:** Motor, tanıma ayarlarını, dil paketlerini ve—bizim için en önemlisi—ön işleme seçeneklerini kapsar. Onsuz, görüntü‑işleme kütüphanelerini manuel olarak zincirlemeniz gerekir, bu da temiz bir hattın amacını bozar.

## Adım 2 – Ön İşleme Hattı Oluşturma (de‑skew → denoise → binarize)

Aspose OCR, ihtiyacınız olan tam sırada filtreleri istifleyebileceğiniz yerleşik bir `PreprocessingOptions` sınıfı ile birlikte gelir. Burada üç filtre ekliyoruz:

1. **DE_SKEW** – döndürülmüş metni düzeltir.  
2. **DENOISE** – karakter olarak algılanabilecek grenli pikselleri yumuşatır.  
3. **BINARIZE** – görüntüyü saf siyah‑beyaz hâle getirir, OCR motorunun işini kolaylaştırır.

```java
        // Step 2: Assemble the preprocessing pipeline
        PreprocessingOptions preprocessingOptions = new PreprocessingOptions();
        preprocessingOptions.addFilter(PreprocessFilter.DE_SKEW);   // correct rotation
        preprocessingOptions.addFilter(PreprocessFilter.DENOISE);  // remove grain
        preprocessingOptions.addFilter(PreprocessFilter.BINARIZE); // high‑contrast B&W

        // Attach the pipeline to the OCR engine
        ocrEngine.getRecognitionSettings().setPreprocessingOptions(preprocessingOptions);
```

> **Pro tip:** Filtrelerin sırası çok önemlidir. Eğer binarize *önce* denoise yaparsanız, gürültü tanıyıcıyı şaşırtan keskin siyah lekeler haline gelebilir. Önce de‑skew yapmak, metin tabanının yatay olmasını sağlar, bu da hem denoise hem de binarize sonuçlarını iyileştirir.

## Adım 3 – Görüntüyü Motora Besleme

Şimdi motoru okumak istediğimiz dosyaya yönlendiriyoruz. Yol, projenizin köküne göre mutlak ya da göreli olabilir.

```java
        // Step 3: Run OCR on the target image
        String imagePath = "YOUR_DIRECTORY/angled-photo.jpg";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);
```

> **Görüntü çok büyük olursa ne olur?** Aspose OCR, en uzun kenarı 2000 px'den büyük olan görüntüleri otomatik olarak küçültür, ancak bellek endişesi varsa bunu `ocrEngine.getRecognitionSettings().setMaxImageDimension(1500)` ile geçersiz kılabilirsiniz.

## Adım 4 – Tanınan Metni Çıktı Olarak Verme

Son olarak, çıkarılan dizeyi konsola yazdırıyoruz. Gerçek bir uygulamada bunu bir veritabanına, bir dosyaya yazabilir ya da sonraki bir NLP hattına besleyebilirsiniz.

```java
        // Step 4: Print the result
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

### Beklenen Çıktı

`angled-photo.jpg` dosyası *“The quick brown fox jumps over the lazy dog.”* cümlesini içeriyorsa, aşağıdakine benzer bir şey görmelisiniz:

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
```

Çıktının ne kadar temiz olduğuna dikkat edin—gereksiz semboller yok, kırık satırlar yok. İşte **preprocess image for OCR**'un gücü.

## Adım 5 – Doğrulama ve Ayarlama (İsteğe Bağlı)

Sağlam bir hatla bile, köşe durumlarıyla karşılaşabilirsiniz:

| Durum | Önerilen ayar |
|-----------|-----------------|
| **Çok düşük kontrast** (ör. solmuş taranmış belgeler) | Binarizasyondan önce ekstra bir `ContrastAdjustment` filtresi ekleyin. |
| **Renkli arka plan** (ör. renkli damgalar içeren fişler) | `BackgroundRemoval` filtresi ekleyin veya önce manuel olarak gri tonlamaya dönüştürün. |
| **Çok sayfalı PDF'ler** | Her sayfa görüntüsü üzerinden döngü yapın ve aynı `preprocessingOptions` nesnesini yeniden kullanın. |

`preprocessingOptions.addFilter(PreprocessFilter.CONTRAST)` gibi bir çağrı yaparak veya Aspose OCR API belgelerinde listelenen diğer filtreleri kullanarak deneyebilirsiniz.

## Tam, Çalıştırılabilir Örnek

Aşağıda, `PreprocessExample.java` adlı bir dosyaya kopyalayıp yapıştırmaya hazır tam program bulunmaktadır. Derlemeden önce Maven bağımlılığının çözüldüğünden emin olun.

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure preprocessing: de‑skew → denoise → binarize
        PreprocessingOptions preprocessingOptions = new PreprocessingOptions();
        preprocessingOptions.addFilter(PreprocessFilter.DE_SKEW);
        preprocessingOptions.addFilter(PreprocessFilter.DENOISE);
        preprocessingOptions.addFilter(PreprocessFilter.BINARIZE);
        ocrEngine.getRecognitionSettings().setPreprocessingOptions(preprocessingOptions);

        // 3️⃣ Perform OCR on the chosen image
        String imagePath = "YOUR_DIRECTORY/angled-photo.jpg";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);

        // 4️⃣ Output the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Derleyin ve çalıştırın:

```bash
mvn compile exec:java -Dexec.mainClass=PreprocessExample
```

Konsola temiz metnin yazdırıldığını görmelisiniz; bu, **preprocess image for OCR** ve **recognize text from image** işlemlerini başarıyla tamamladığınızı doğrular.

## Sık Sorulan Sorular & Cevaplar

**S1: Bu PNG veya TIFF dosyalarıyla çalışır mı?**  
Evet—Aspose OCR JPEG, PNG, BMP, TIFF ve birkaç başka formatı destekler. Aynı ön işleme hattı uygulanır; kütüphane formatı otomatik olarak algılar.

**S2: Telefonla çekilen bir fotoğraftan metin çıkarmam gerekirse ne yapmalıyım?**  
Telefon fotoğrafları genellikle dengesiz aydınlatmadan etkilenir. Binarizasyondan önce bir `LIGHTING_CORRECTION` filtresi eklemek yardımcı olabilir. Kod değişikliği tek bir satırdır:

```java
preprocessingOptions.addFilter(PreprocessFilter.LIGHTING_CORRECTION);
```

**S3: OCR dilini değiştirebilir miyim?**  
Kesinlikle. Motoru oluşturduktan sonra dili şu şekilde ayarlayın:

```java
ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.SPANISH);
```

**S4: Bu, OCR doğruluğunu nasıl artırır?**  
Her filtre belirli bir görsel gürültü tipini azaltır. De‑skew metin satırlarını hizalar, denoise rastgele lekeleri temizler ve binarize yüksek kontrastlı bir görüntü oluşturur. Birlikte, tanıma algoritmasına daha temiz bir sinyal sağlar; bu da karakter‑seviyesinde daha yüksek doğruluk anlamına gelir—genellikle gürültülü girişlerde %15‑30 artış sağlar.

## Sonraki Adımlar & İlgili Konular

- **Batch processing:** Çekirdek mantığı bir döngü içinde sararak fotoğraf klasörlerinin tamamını işleyin.  
- **Custom filter order:** Belgeler zaten yüksek kontrastlıysa `BINARIZE`'ı `DENOISE`'dan önce denemek faydalı olabilir.  
- **Performance tuning:** `ocrEngine.getRecognitionSettings().setThreadCount(4)` kullanarak çok çekirdekli makinelerde paralelleştirme yapın.  
- **Alternative libraries:** Açık kaynak senaryoları için Aspose OCR'ı Tesseract‑Java ile karşılaştırın.  
- **Post‑processing:** Ham çıktıyı daha da temizlemek için yazım denetimi veya regex temizliği uygulayın.

**preprocess image for OCR** iş akışını ustalaştırarak, fotoğraf kaynaklarından metin çıkarma işleminin tahmin edilebilir, tekrarlanabilir bir görev haline geldiğini göreceksiniz; artık şans oyununa dönüşmez.

---

*OCR hattınızı güçlendirmeye hazır mısınız? Kodu alın, filtreleri ayarlayın ve doğruluğun yükselişini izleyin. Bir sorunla karşılaşırsanız, aşağıya yorum bırakın—iyi kodlamalar!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}