---
category: general
date: 2026-02-17
description: Java'da Aspose OCR ile OCR için görüntüyü ön işleme. Görüntü kontrastını
  artırmayı, kontrast seviyesini ayarlamayı ve görüntüden metni sadece birkaç dakikada
  tanımayı öğrenin.
draft: false
keywords:
- preprocess image for ocr
- boost image contrast
- recognize text from image
- extract text using OCR
- set contrast level
language: tr
og_description: Aspose OCR Java kullanarak OCR için görüntüyü ön işleme. Bu kılavuz,
  görüntü kontrastını artırmayı, kontrast seviyesini ayarlamayı ve görüntüden metni
  hızlı bir şekilde tanımayı gösterir.
og_title: OCR için Görüntüyü Ön İşleme – Kontrastı Artırma ve Metin Çıkarma İçin Java
  Eğitimi
tags:
- Java
- OCR
- Image Processing
title: OCR için Görüntüyü Ön İşleme – Kontrastı Artırmak ve Metin Çıkarmak için Tam
  Java Rehberi
url: /tr/java/advanced-ocr-techniques/preprocess-image-for-ocr-complete-java-guide-to-boost-contra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR için Görüntü Ön İşleme – Tam Java Rehberi

Hiç **OCR için görüntü ön işleme** yapmanız gerekti ama hangi ayarların gerçekten fark yarattığından emin olamadınız mı? Yalnız değilsiniz. Çoğu geliştirici bir görüntüyü OCR motoruna atar ve sihrin gerçekleşmesini bekler, sadece bozuk bir çıktı alır. Bu öğreticide, **görüntü kontrastını artıran**, **kontrast seviyesini ayarlayan** ve sonunda Aspose OCR for Java kullanarak **görüntüden metin tanıyan** pratik, uçtan uca bir örnek üzerinden ilerleyeceğiz.

Tamamladığınızda, gürültülü taramalarda bile **OCR kullanarak metin çıkaran** yeniden kullanılabilir bir kod parçacığına sahip olacaksınız. Gizli hileler yok, sadece net adımlar ve her birinin ardındaki mantık var.

## Gereksinimler

- Java 17 veya daha yeni bir sürüm (kod, herhangi bir güncel JDK ile derlenebilir)
- Aspose OCR for Java kütüphanesi (resmi Aspose sitesinden indirin)
- Geçerli bir Aspose OCR lisans dosyası (`Aspose.OCR.lic`)
- Okumak istediğiniz giriş görüntüsü (`input.jpg`)
- Sevdiğiniz bir IDE veya basit bir komut satırı ortamı

Eğer bunlara sahipseniz, harika—hadi hemen başlayalım.

## Adım 1: Aspose OCR Lisansını Yükleyin (Temel Kurulum)

OCR motoru bir şey yapmadan önce lisanslı olduğunuzu bilmesi gerekir. Aksi takdirde deneme su işaretiyle karşılaşırsınız.

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {

        // Load the Aspose OCR license – this disables the evaluation limits
        License ocrLicense = new License();
        ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

**Neden önemli:** Uygun bir lisans olmadan motor değerlendirme modunda çalışır, bu da sonuçları kısaltabilir veya su işareti ekleyebilir. Lisansı erken ayarlamak, sonraki tüm ön işleme seçeneklerinin tam özellikli modda uygulanmasını da sağlar.

## Adım 2: OCR Motorunu Başlatın

Bir `OcrEngine` örneği oluşturmak, tanıma ve ön işleme boru hatlarına erişmenizi sağlar.

```java
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

**İpucu:** Birden çok görüntüyü toplu olarak işlemek istiyorsanız motoru tek bir örnek (singleton) olarak tutun; iç kaynakları önbelleğe alır ve sonraki çağrıları hızlandırır.

## Adım 3: Ön İşlemeyi Yapılandırın – Döndürme Düzeltme, Gürültü Giderme ve Kontrast Artırma

İşte **OCR için görüntü ön işleme** kısmı. Ayarlayacağımız üç düğme şunlar:

1. **Deskew** – hafif döndürmeleri düzeltir.
2. **Denoise** – karakter bölütlemesini karıştıran lekeleri temizler.
3. **Contrast enhancement** – koyu metnin arka plan üzerinde öne çıkmasını sağlar.

```java
        // Access preprocessing settings
        PreprocessingSettings preprocessing = ocrEngine.getPreprocessing();

        // Enable automatic deskew (helps with scanned pages that are a few degrees off)
        preprocessing.setDeskew(true);
        preprocessing.setDeskewAngleTolerance(0.1); // tolerance in degrees

        // Turn on denoising – median works well for salt‑and‑pepper noise
        preprocessing.setDenoise(true);
        preprocessing.setDenoiseMode(DenoiseMode.MEDIAN); // alternatives: GAUSSIAN

        // Boost contrast – this is the “boost image contrast” step
        preprocessing.setContrastEnhance(true);
        preprocessing.setContrastLevel(1.3f); // 1.0 = no change, >1.0 = stronger contrast
```

### Neden Kontrast Seviyesi Ayarlanmalı?

Kontrast seviyesini artırmak, görüntünün histogramını genişletir; koyu pikseller daha koyu, parlak pikseller daha parlak olur. Pratikte, `1.3f` **kontrast seviyesi** çoğu basılı belge için en iyi dengeyi verir, `1.5f` üzerindeki bir değer ise ince çizgileri aşırı aydınlatabilir. Denemekten çekinmeyin; bu ayar değiştirmesi ucuzdur ve **görüntüden metin tanıma** başarısını büyük ölçüde artırabilir.

## Adım 4: Giriş Görüntüsünü Hazırlayın

`OcrInput` sınıfı dosya işlemlerini soyutlar. Toplu işleme ihtiyacınız varsa birden çok görüntü ekleyebilirsiniz.

```java
        // Prepare the image for OCR – you can add more files to the same OcrInput
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.jpg");
```

**Köşe durumu:** Görüntünüz standart dışı bir formatta (ör. çok sayfalı TIFF) ise her sayfayı ayrı ayrı yükleyebilir veya önce PNG/JPEG’e dönüştürebilirsiniz.

## Adım 5: Tanıma İşlemini Gerçekleştirin

Şimdi motor, az önce yapılandırdığımız ön işleme boru hattını çalıştırır, ardından temizlenmiş görüntüyü temel OCR algoritmasına verir.

```java
        // Run OCR – this returns a result object containing the extracted text
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Arka planda ne oluyor?** Aspose OCR önce döndürme düzeltme dönüşümünü uygular, ardından gürültü giderme filtresini çalıştırır ve son olarak kontrastı ayarlar; ardından görüntüyü sinir ağı tabanlı tanıma motoruna gönderir. Sıra kasıtlıdır; değiştirilmesi alt‑optimum sonuçlara yol açabilir.

## Adım 6: Tanınan Metni Çıktılayın

Son olarak, çıkarılan dizeyi konsola yazdırıyoruz. Gerçek bir uygulamada bunu bir dosyaya yazabilir veya bir ağa gönderebilirsiniz.

```java
        // Print the recognized text to the console
        System.out.println(ocrResult.getText());
    }
}
```

### Beklenen Çıktı

`input.jpg` içinde “Hello World!” ifadesi varsa, konsol şu şekilde görüntülenmelidir:

```
Hello World!
```

Çıktı bozuk görünüyorsa, özellikle **kontrast seviyesi** ve **gürültü giderme modu** gibi ön işleme değerlerini yeniden kontrol edin ve farklı bir görüntü formatı deneyin.

## Bonus: Ön‑İşlenmiş Görüntüyü Görselleştirme (İsteğe Bağlı)

Bazen motorun döndürme düzeltme, gürültü giderme ve kontrast artırma sonrası ne gördüğünü görmek istersiniz. Aspose OCR ara bitmap’i dışa aktarmanıza izin verir:

```java
        // Export the pre‑processed image for debugging
        BufferedImage processed = preprocessing.getProcessedImage();
        ImageIO.write(processed, "png", new File("processed.png"));
```

`processed.png` dosyasını orijinaliyle yan yana açın; daha düz bir ufuk ve daha net metin fark edeceksiniz. Bu adım, belirli bir taramanın neden başarısız olduğunu araştırırken çok işe yarar.

![OCR için görüntü ön işleme örneği](/images/ocr-preprocess-example.png "OCR için görüntü ön işleme – kontrast artırmadan önce ve sonra")

*Yukarıdaki görsel, kontrast artırma ve gürültü giderme sayesinde bulanık bir taramanın temiz, OCR‑hazır bir resme dönüşümünü göstermektedir.*

## Yaygın Tuzaklar ve Kaçınma Yöntemleri

| Tuzak | Neden Oluşur | Çözüm |
|------|--------------|------|
| **Aşırı kontrast** (`setContrastLevel` çok yüksek) | Açık arka plan beyazlaşır, soluk karakterler silinir | Çoğu basılı metin için seviyeyi 1.1‑1.4 arasında tutun |
| **Düşük döndürme toleransı** | Küçük döndürmeler düzeltilmez | `setDeskewAngleTolerance` değerini 0.2 ya da 0.3’e yükseltin |
| **Binary görüntülerde GAUSSIAN gürültü giderme** | Kenarları bulanıklaştırır, karakterleri birleştirir | Siyah‑beyaz taramalarda `DenoiseMode.MEDIAN` kullanın |
| **Lisans eksikliği** | Motor deneme moduna geçer, çıktıyı kısaltır | `Aspose.OCR.lic` dosyasının yolunu ve okunabilirliğini doğrulayın |

## Sonraki Adımlar: Temel Ön‑İşlemenin Ötesine Geçmek

Artık **OCR için görüntü ön işleme** ve **OCR kullanarak metin çıkarma** yapabildiğinize göre, aşağıdaki genişletmeleri düşünebilirsiniz:

- **Dil paketleri** – İngilizce dışı metinlerde doğruluğu artırmak için belirli dil sözlüklerini yükleyin.
- **İlgi bölgesi (ROI) kırpma** – sayfanın yalnızca bir kısmına ihtiyacınız varsa o bölgeye odaklanın.
- **Toplu işleme** – bir dizindeki tüm görüntüler üzerinde döngü kurun, aynı `OcrEngine` örneğini yeniden kullanarak hızı artırın.
- **PDF entegrasyonu** – Aspose OCR’u Aspose PDF ile birleştirerek taranmış PDF’leri tek bir boru hattında aranabilir PDF’lere dönüştürün.

Bu konular doğal olarak ikincil anahtar kelimelerimizi içerir: hâlâ **görüntü kontrastını artıracak**, **kontrast seviyesini ayarlayacak** ve **görüntüden metin tanıyacak** şekilde çalışacaksınız.

## Sonuç

Aspose OCR for Java kullanarak **OCR için görüntü ön işleme** konusundaki tüm adımları ele aldık: lisansı yükleme, döndürme düzeltme, gürültü giderme ve kontrast artırma yapılandırması, görüntüyü besleme ve sonunda **görüntüden metin tanıma**. Yukarıdaki tam, çalıştırılabilir örnekle artık **OCR kullanarak metin çıkarabilir** ve uygun şekilde hazırlanmış herhangi bir resimde bunu uygulayabilirsiniz.

Kodu çalıştırın, **kontrast seviyesini** ayarlayın ve doğruluğun nasıl yükseldiğini izleyin. Hazır olduğunuzda, dil‑spesifik modelleri veya toplu boru hatlarını keşfederek bu tek‑görüntü demosunu üretim‑düzeyinde bir çözüme dönüştürün.

*İyi kodlamalar, ve taramalarınız her zaman net olsun!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}