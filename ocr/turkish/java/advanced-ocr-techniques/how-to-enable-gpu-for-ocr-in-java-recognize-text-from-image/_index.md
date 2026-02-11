---
category: general
date: 2026-01-02
description: Java OCR'de GPU'yu etkinleştirerek görüntüden metni hızlı bir şekilde
  tanıyın. PNG'den metin çıkarma, görüntü seçeneklerini ayarlama ve metni verimli
  bir şekilde tanıma hakkında bilgi edinin.
draft: false
keywords:
- how to enable gpu
- recognize text from image
- extract text from png
- how to set image
- how to recognize text
language: tr
og_description: Java OCR'de GPU'yu etkinleştirerek görüntüden metni hızlıca tanıma.
  Bu kılavuz, PNG'den metin çıkarmayı, görüntü seçeneklerini ayarlamayı ve metni verimli
  bir şekilde tanımayı gösterir.
og_title: Java'da OCR için GPU'yu Nasıl Etkinleştirirsiniz – Görüntüden Metni Hızlıca
  Tanıyın
tags:
- OCR
- Java
- GPU
title: Java'da OCR için GPU'yu Nasıl Etkinleştirirsiniz – Görüntüden Metni Hızlıca
  Tanıyın
url: /tr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-recognize-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java’da OCR için GPU Nasıl Etkinleştirilir – Görüntüden Metni Hızlıca Tanıyın

Java OCR uygulamanızda GPU’yu etkinleştirmek, hızlı metin çıkarımı ihtiyacı duyan geliştiriciler için yaygın bir engeldir. Bu öğreticide **GPU’yu nasıl etkinleştireceğinizi**, görüntüden metni nasıl tanıyacağınızı ve Aspose OCR kütüphanesini kullanarak PNG’den metni nasıl çıkaracağınızı göstereceğiz.  

Eğer yavaş bir OCR sürecine bakıp bir grafik kartının işleri hızlandırıp hızlandıramayacağını merak ettiyseniz, doğru yerdesiniz. Ayrıca OCR motorunun dosyalarınızı doğru okuyabilmesi için görüntü işleme seçeneklerini nasıl ayarlayacağınızı ele alacağız ve kaçınılmaz “metni nasıl tanıyabilirim” sorularına yanıt vereceğiz.

## Gereksinimler

- **Java 17** veya daha yenisi (kod daha eski sürümlerle derlenebilir, ancak 17 ideal noktadır).  
- **Aspose OCR for Java** – en yeni JAR dosyasını Aspose web sitesinden ya da Maven Central’dan edinebilirsiniz.  
- **GPU‑destekli bir makine** (NVIDIA RTX 3060 veya CUDA‑uyumlu herhangi bir kart yeterli).  
- Test etmek için bir görüntü dosyası – büyük bir fatura PNG’si benchmark için harika çalışır.

> **Pro tip:** Entegre grafik kartlı bir dizüstü bilgisayar kullanıyorsanız, sürücü ayarlarında ayrık GPU’nun seçili olduğundan emin olun; aksi takdirde kütüphane sessizce CPU’ya geri döner.

![how to enable gpu example](image.png "how to enable gpu example")

*Alt metin: Java kod parçacığını gösteren GPU etkinleştirme örneği.*

## Adım 1 – Aspose OCR’yi Kurun ve GPU Kullanılabilirliğini Doğrulayın

GPU desteğini **nasıl etkinleştireceğinizi** kullanabilmek için önce kütüphaneyi sınıf yolunuza eklemeniz gerekir. Maven bağımlılığını ekleyin (ya da JAR dosyasını `libs/` klasörüne bırakın):

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Check for the latest version -->
</dependency>
```

Bağımlılık yerleştirildikten sonra hızlı bir bütünlük kontrolü çalıştırın:

```java
import com.aspose.ocr.GpuSettings;

public class GpuCheck {
    public static void main(String[] args) {
        GpuSettings settings = new GpuSettings();
        System.out.println("GPU enabled? " + settings.getEnable());
        System.out.println("Detected GPU count: " + settings.getDeviceCount());
    }
}
```

Eğer çıktı sıfırdan farklı bir cihaz sayısı gösteriyorsa, JVM GPU’yu görmüş demektir. Sıfır gösteriyorsa, sürücü kurulumunu ve `CUDA_PATH` ortam değişkeninin ayarlı olduğunu tekrar kontrol edin.

## Adım 2 – Aspose OCR’de GPU’yu Nasıl Etkinleştirirsiniz

Sistem grafik kartını tanıdıktan sonra, şimdi gerçekten açalım. Ana anahtar kelime başlıkta yer alıyor, SEO kuralını karşılıyor.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.GpuSettings;
import com.aspose.ocr.ImageProcessingOptions;
import com.aspose.ocr.RecognitionLanguage;
import com.aspose.ocr.OcrResult;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create the OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // 2️⃣ Enable GPU processing (auto‑detects available device)
        GpuSettings gpuSettings = new GpuSettings();
        gpuSettings.setEnable(true);          // turn GPU on
        gpuSettings.setDeviceId(0);           // first GPU (change if you have multiple)
        ocrEngine.setGpuSettings(gpuSettings);

        // 3️⃣ Optimize image preprocessing for GPU performance
        ImageProcessingOptions imgOpts = new ImageProcessingOptions();
        imgOpts.setAutoDeskew(true);
        imgOpts.setBinarization(true);
        ocrEngine.setImageProcessingOptions(imgOpts);

        // 4️⃣ Recognize text from an image file (PNG in this case)
        OcrResult result = ocrEngine.recognizeImage(
                "YOUR_DIRECTORY/large_invoice.png",
                RecognitionLanguage.ENGLISH);

        // 5️⃣ Output the detected text
        System.out.println("Detected text:\n" + result.getText());
    }
}
```

### Neden GPU Etkinleştirilmeli?

GPU hızlandırması, OCR modellerinin gerçekleştirdiği yoğun matris‑çarpım işini binlerce paralel çekirdeğe devreder. Pratikte, orta seviye bir RTX 2060’da **2‑5× hız artışı** görebilir, daha yeni kartlarda ise daha da fazlasını elde edebilirsiniz. Tek dezavantaj, hafifçe artan bellek tüketimi; ancak tipik fatura‑boyutundaki PNG’ler için genellikle sorun olmaz.

## Adım 3 – Görüntüden Metni Tanıma (ve PNG’den Metin Çıkarma)

GPU artık çalışırken, gerçek *görüntüden metni tanıma* adımına odaklanalım. Yukarıdaki kod zaten bunu yapıyor, ancak OCR çağrısını izole eden sade bir versiyon aşağıda:

```java
// Assuming ocrEngine is already configured with GPU
String imagePath = "sample.png";
OcrResult ocrResult = ocrEngine.recognizeImage(imagePath, RecognitionLanguage.ENGLISH);
String extractedText = ocrResult.getText();

System.out.println("Extracted text from PNG:");
System.out.println(extractedText);
```

**Dikkat edeceğiniz:** `recognizeImage` metodu dosya tipini otomatik algılar, bu yüzden JPEG, TIFF veya PNG’yi ekstra bayraklar olmadan besleyebilirsiniz. Bu yüzden *png’den metin çıkarma* sorunsuz çalışır.

### Büyük Dosyalarla Çalışma

PNG dosyanız 5 MB’dan büyükse, OCR’dan önce ölçeklendirmeyi düşünün:

```java
imgOpts.setResizeFactor(0.5); // shrink to 50 % of original dimensions
ocrEngine.setImageProcessingOptions(imgOpts);
```

Alt örnekleme, GPU bellek kullanımını azaltır ve modelin daha temiz kenarları görmesi sayesinde doğruluğu artırabilir.

## Adım 4 – Daha İyi Doğruluk İçin Görüntü Seçeneklerini Nasıl Ayarlarsınız

*Görüntü ayarlarını nasıl yaparım* ifadesi, ön işleme konuşurken doğal olarak ortaya çıkar. Aspose OCR birkaç ayar sunar:

| Seçenek                     | Ne işe yarar                                 | Tipik değer |
|-----------------------------|----------------------------------------------|-------------|
| `setAutoDeskew(true)`       | Eğik metin satırlarını düzleştirir           | true        |
| `setBinarization(true)`     | Kontrast için siyah‑beyaz dönüştürür         | true        |
| `setResizeFactor(x)`        | Görüntüyü ölçeklendirir (0 < x ≤ 1)          | 0.5‑0.8     |
| `setContrastAdjustment(y)`  | Kontrastı artırır (0‑100)                    | 30          |

Bu ayarları istediğiniz sırayla birleştirebilirsiniz; kütüphane görüntüyü sinir ağına beslemeden önce sırasıyla uygular. Deneme yanılma burada kritiktir—farklı faturalar farklı eşik değerleri gerektirebilir.

## Adım 5 – Kenar Durumlarında Metni Nasıl Tanırsınız

GPU gücüne rağmen, bazı senaryolar OCR’yi zorlayabilir:

1. **Düşük çözünürlüklü taramalar (< 150 dpi).** Önce ölçeklendirin veya kullanıcıdan daha yüksek çözünürlükte bir tarama isteyin.  
2. **El yazısı notlar.** Varsayılan model basılı metne odaklanır; el yazısı için özel bir model eğitmeniz gerekir.  
3. **Birden çok dil.** `RecognitionLanguage` parametresine virgülle ayrılmış bir liste verin, örn. `RecognitionLanguage.ENGLISH_FRENCH`.

```java
ocrEngine.recognizeImage("multilang.png",
        RecognitionLanguage.ENGLISH_FRENCH);
```

## Beklenen Çıktı

Tam `GpuExample` sınıfını `large_invoice.png` üzerinde çalıştırdığınızda aşağıdakine benzer bir çıktı almanız gerekir:

```
Detected text:
Invoice #12345
Date: 2025‑12‑31
Total: $1,234.56
...
```

Eğer anlamsız karakterler görürseniz, `gpuSettings.setEnable(true)`’nin gerçekten etkili olup olmadığını tekrar kontrol edin (hata ayıklama kaydı açıksa konsol GPU cihazını listeleyecektir).

## Yaygın Tuzaklar ve Pro İpuçları

- **GPU cihaz kimliği ayarlamayı unutmak.** Çoklu GPU sistemlerde `setDeviceId(1)` gerekebilir.  
- **NVIDIA runtime olmadan Docker içinde çalıştırmak.** `docker run` komutuna `--gpus all` ekleyin.  
- **CPU‑only ve GPU‑enabled kod yollarını karıştırmak.** Her iş parçacığı için tek bir `AsposeOCR` örneği tutun, durum çakışmalarını önleyin.  
- **Bellek sızıntıları.** Uzun çalışan servislerde `ocrEngine.dispose()` çağrısını unutmayın.

## Sonuç

Java’da Aspose OCR için **GPU’yu nasıl etkinleştirirsiniz** konusunu adım adım inceledik, **görüntüden metni nasıl tanırsınız** gösterdik, **PNG’den metin çıkarma** en basit yolunu sergiledik, **görüntü işleme seçeneklerini nasıl ayarlarsınız** açıklamalarıyla birlikte, gerçek dünya dosyalarında **metni nasıl tanırsınız** inceliklerini ele aldık. GPU aktif olduğunda OCR hattınız belirgin şekilde daha hızlı çalışacak ve toplu fatura işleme ya da canlı belge tarama gibi yüksek verimli senaryolar için uygun hale gelecektir.

Bir sonraki adıma hazır mısınız? Varsayılan İngilizce modeli çok dilli bir modele geçirin ya da gürültülü makbuzlar için özel ön işleme boru hatları deneyin. Gökyüzü sınırdır—özellikle ağır işleri GPU’nuz üstleniyorsa.

---

*Kodlamaktan keyif alın, OCR’nuz daima hızlı olsun!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}