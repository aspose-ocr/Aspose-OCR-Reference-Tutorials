---
category: general
date: 2026-08-22
description: Java OCR'de GPU'yu etkinleştirerek görüntüden metni hızlıca tanıma yöntemi.
  PNG'den metin çıkarmayı, görüntü seçeneklerini ayarlamayı ve Aspose OCR kullanarak
  metni verimli bir şekilde tanımayı öğrenin.
draft: false
keywords:
- how to enable gpu
- recognize text image java
- aspose ocr java tutorial
- extract text from png
- set image options
lastmod: 2026-08-22
og_description: Java OCR'de GPU'yu etkinleştirerek görüntüden metni hızlıca tanıma
  yöntemi. Bu rehber, PNG'den metin çıkarmayı, görüntü seçeneklerini ayarlamayı ve
  Aspose OCR kullanarak metni verimli bir şekilde tanımayı gösterir.
og_image_alt: Java OCR GPU example code snippet showing Aspose OCR usage
og_title: Java'da OCR için GPU'yu Nasıl Etkinleştirirsiniz – hızlı metin çıkarma
schemas:
- author: Aspose
  dateModified: '2026-08-22'
  description: How to enable GPU in Java OCR to recognize text from image quickly.
    Learn to extract text from PNG, set image options, and recognize text efficiently
    using Aspose OCR.
  headline: How to Enable GPU for OCR in Java – Recognize Text from Image Fast
  type: TechArticle
- description: How to enable GPU in Java OCR to recognize text from image quickly.
    Learn to extract text from PNG, set image options, and recognize text efficiently
    using Aspose OCR.
  name: How to Enable GPU for OCR in Java – Recognize Text from Image Fast
  steps:
  - name: '**Low‑resolution scans (< 150 dpi).** Upscale first or ask the user for
      a higher‑resolution scan.'
    text: '**Low‑resolution scans (< 150 dpi).** Upscale first or ask the user for
      a higher‑resolution scan.'
  - name: '**Handwritten notes.** The default model focuses on printed text; you’d
      need a custom trained model for cursive.'
    text: '**Handwritten notes.** The default model focuses on printed text; you’d
      need a custom trained model for cursive.'
  - name: '**Multiple languages.** Pass a comma‑separated list to `RecognitionLanguage`,
      e.g., `RecognitionLanguage.ENGLISH_FRENCH`.'
    text: '**Multiple languages.** Pass a comma‑separated list to `RecognitionLanguage`,
      e.g., `RecognitionLanguage.ENGLISH_FRENCH`.'
  type: HowTo
- questions:
  - answer: Yes, the Aspose OCR trial includes full GPU support; you just need to
      enable it in code.
    question: Does the free trial support GPU acceleration?
  - answer: Aspose OCR can rasterize PDF pages internally, but for best performance
      convert to high‑resolution PNG first.
    question: Can I process PDFs directly without converting to images?
  - answer: CUDA 11.2 or newer is recommended; older versions may work but are not
      officially tested.
    question: What CUDA version is required?
  - answer: Validate file size and type before processing, and run the OCR in a sandboxed
      thread to mitigate risks.
    question: Is it safe to run OCR on untrusted user uploads?
  - answer: Set `ocrEngine.setDebugMode(true)`; the console will list the selected
      GPU device and memory statistics.
    question: How do I enable logging to verify GPU usage?
  type: FAQPage
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

# Java'da OCR için GPU'yu Etkinleştirme – Görüntüden Metni Hızlıca Tanıma

Enabling GPU acceleration in a Java OCR application can cut processing time dramatically, especially when you need to extract text from large images or high‑volume batches. In this tutorial you’ll learn **how to enable GPU**, how to **recognize text from image** files, and the exact steps to **extract text from PNG** using the Aspose OCR library. We’ll also walk through image‑pre‑processing options that improve accuracy and answer common “how to recognize text” questions along the way.

## Hızlı Yanıtlar
- **En büyük hız artışı nedir?** CPU‑only OCR'a kıyasla orta seviye RTX 2060'da 5 kat daha hızlı.  
- **Özel bir lisansa ihtiyacım var mı?** Standart Aspose OCR lisansı GPU için çalışır; sadece GPU bayrağını etkinleştirin.  
- **Hangi Java sürümü gerekiyor?** En iyi performans için Java 17 veya daha yenisi önerilir.  
- **Bunu Docker içinde çalıştırabilir miyim?** Evet – sadece `--gpus all` bayrağını ekleyin ve konteyner içinde NVIDIA sürücülerini kurun.  
- **Kod diğer görüntü formatlarıyla uyumlu mu?** Aynı API JPEG, TIFF, BMP ve PNG için değişiklik yapmadan çalışır.

## Gerekenler

GPU destekli bir makineye, Aspose OCR for Java kütüphanesine ve Java 17 (veya daha yenisi) geliştirme ortamına ihtiyacınız var. Tipik bir kurulum NVIDIA RTX 3060 veya herhangi bir CUDA uyumlu kart, Maven Central'dan en son Aspose OCR JAR'ı ve performans ölçümü için örnek bir PNG fatura içerir.

**Doğrudan yanıt (40‑70 kelime):** Başlamak için Java 17 kurmalı, projenize Aspose OCR bağımlılığını eklemeli, JVM'in en az bir CUDA cihazını görebildiğini doğrulamalı ve bir test görüntüsü hazırlamalısınız. Bu ön koşullar sağlandığında OCR motorunda GPU'yu etkinleştirebilir ve görüntüleri GPU hızında işlemeye başlayabilirsiniz.

- **Java 17** (veya daha yenisi) – kod daha eski sürümlerle derlenebilir ancak 17 en iyi API desteğini sağlar.  
- **Aspose OCR for Java** – en son JAR'ı Aspose web sitesinden veya Maven Central'dan edinin.  
- **CUDA uyumlu bir GPU** – örn., NVIDIA RTX 3060, RTX 2070 veya uygun sürücülere sahip modern bir kart.  
- **Test görüntüsü** – büyük formatlı bir PNG fatura, performans ölçümü için iyidir.

> **Pro ipucu:** Hem entegre hem de ayrık grafiklere sahip dizüstü bilgisayarlarda, sürücü kontrol paneli üzerinden JVM'in ayrık GPU'yu kullanmasını zorlayın; aksi takdirde kütüphane sessizce CPU'ya geri döner.

![GPU'yu etkinleştirme örneği](image.png "GPU'yu etkinleştirme örneği")
[GPU'yu etkinleştirme örneği](image.png "GPU'yu etkinleştirme örneği")

*Alt metin: GPU'yu etkinleştirme örneği, Java kod parçacığını gösteriyor.*

## Adım 1 – Aspose OCR'yi Kurun ve GPU Kullanılabilirliğini Doğrulayın

GpuSettings, Aspose OCR motoru için GPU kullanımını kontrol eden bir sınıftır.

Maven bağımlılığını ekleyin (veya JAR'ı `libs/` klasörüne bırakın):

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Check for the latest version -->
</dependency>
```

Mevcut cihazları listelemek için sağlık kontrolü kod parçacığını çalıştırın:

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

Çıktı sıfır olmayan bir cihaz sayısı gösteriyorsa, JVM GPU'yu görüyor demektir. Sıfır rapor ediyorsa, sürücü kurulumunu ve `CUDA_PATH` ortam değişkeninin ayarlı olduğunu iki kez kontrol edin.

## Adım 2 – Aspose OCR'de GPU'yu Nasıl Etkinleştirirsiniz

**Doğrudan yanıt (40‑70 kelime):** GPU'yu etkinleştirmek için bir `GpuSettings` nesnesi oluşturun, `setEnable(true)` ayarlayın, isteğe bağlı olarak cihaz kimliğini belirtin ve bu ayar nesnesini `AsposeOCR` yapıcısına geçirin. Bundan sonra tüm sonraki OCR çağrıları seçilen GPU'da çalışacak ve performans bölümünde açıklanan hız artışlarını sağlayacaktır.

`GpuSettings` sınıfı, birden fazla GPU bulunduğunda GPU kullanımını açıp kapamanıza ve belirli bir cihaz seçmenize olanak tanır.

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

### Neden GPU'yu Etkinleştirirsiniz?

GPU hızlandırması, OCR modellerinin gerçekleştirdiği ağır matris çarpım işini binlerce paralel çekirdeğe devreder. Pratikte orta seviye bir RTX 2060'da **2‑5× hız artışı** görürsünüz ve daha yeni kartlarda daha da fazlasını elde edersiniz. Dezavantajı, hafifçe daha yüksek bellek ayak izi olmasıdır, ancak bu genellikle tipik fatura‑boyutlu PNG'ler için sorun oluşturmaz.

## Adım 3 – Java'da Metin Görüntüsü Tanıma – En İyi Uygulamalar

`recognizeImage` yöntemi verilen görüntü dosyasını işler ve çıkarılan metni döndürür.

**Doğrudan yanıt (40‑70 kelime):** GPU etkinleştirildikten sonra `ocrEngine.recognizeImage(filePath)` çağırın; yöntem dosya formatını otomatik olarak algılar, OCR modelini GPU'da çalıştırır ve çıkarılan metni döndürür. En iyi doğruluk için, çağrıdan önce görüntünün ikiliye dönüştürülmüş ve eğimi düzeltilmiş olduğundan emin olun.

Yukarıdaki kod zaten bunu yapıyor, ancak OCR çağrısını izole eden sadeleştirilmiş bir versiyon burada:

```java
// Assuming ocrEngine is already configured with GPU
String imagePath = "sample.png";
OcrResult ocrResult = ocrEngine.recognizeImage(imagePath, RecognitionLanguage.ENGLISH);
String extractedText = ocrResult.getText();

System.out.println("Extracted text from PNG:");
System.out.println(extractedText);
```

**Dikkat edeceğiniz:** `recognizeImage` yöntemi dosya tipini otomatik olarak algılar, bu yüzden JPEG, TIFF veya PNG'yi ek bayraklar olmadan besleyebilirsiniz. Bu yüzden **PNG'den metin çıkarma** kutudan çıktığı gibi çalışır.

### Büyük Dosyaları İşleme

PNG dosyanız 5 MB'den büyükse, OCR'den önce ölçeklendirmeyi düşünün:

```java
imgOpts.setResizeFactor(0.5); // shrink to 50 % of original dimensions
ocrEngine.setImageProcessingOptions(imgOpts);
```

Alt örnekleme GPU bellek kullanımını azaltır ve genellikle modelin daha temiz kenarları görmesi nedeniyle doğruluğu artırır.

## Adım 4 – Daha İyi Doğruluk İçin Görüntü Seçeneklerini Nasıl Ayarlarsınız

ImageOptions, OCR'den önce eğim düzeltme ve ikileştirme gibi ön işleme adımlarını ayarlamanıza olanak tanıyan bir yapılandırma nesnesidir.

**Doğrudan yanıt (40‑70 kelime):** Görüntüyü OCR motoruna göndermeden önce otomatik eğim düzeltme, ikileştirme ve isteğe bağlı yeniden boyutlandırmayı etkinleştirmek için `ImageOptions` nesnesini kullanın. Tipik değerler `setAutoDeskew(true)`, `setBinarization(true)` ve büyük taramalar için 0.5 ile 0.8 arasında bir yeniden boyutlandırma faktörüdür. Bu ayarlar kontrast ve hizalamayı iyileştirir, böylece sinir ağı karakterleri daha doğru tanır, özellikle gürültülü veya eğimli belgelerde.

**how to set image** ifadesi ön işleme hakkında konuşurken doğal olarak ortaya çıkar. Aspose OCR birkaç ayar sunar:

| Seçenek                    | Ne yapar                                   | Tipik değer |
|----------------------------|--------------------------------------------|-------------|
| `setAutoDeskew(true)`      | Eğik metin satırlarını düzeltir            | true        |
| `setBinarization(true)`    | Kontrast için siyah‑beyaz dönüştürür       | true        |
| `setResizeFactor(x)`       | Görüntüyü ölçeklendirir (0 < x ≤ 1)        | 0.5‑0.8     |
| `setContrastAdjustment(y)` | Kontrastı artırır (0‑100)                  | 30          |

Bu ayarları herhangi bir sırayla birleştirebilirsiniz; kütüphane görüntüyü sinir ağına beslemeden önce sıralı olarak uygular. Deneyim anahtardır—farklı faturalar farklı eşik değerleri gerektirebilir.

## Adım 5 – Kenar Durumlarda Metni Nasıl Tanırsınız

`GpuExample` sınıfı, Aspose OCR'yi GPU hızlandırmasıyla kullanan tam bir uçtan uca OCR iş akışını gösterir.

**Doğrudan yanıt (40‑70 kelime):** Düşük çözünürlüklü taramalar için önce görüntüyü yükseltin veya daha yüksek dpi kaynağı isteyin; el yazısı notlar için özel eğitilmiş bir modele geçin; çok dilli belgeler için `RecognitionLanguage`'a virgülle ayrılmış bir liste gönderin. Bu ayarlamalar, GPU hızlandırmalı motorun hâlâ güvenilir sonuçlar vermesini sağlar.

GPU gücüne rağmen, belirli senaryolar OCR'yi zorlayabilir:

1. **Düşük çözünürlüklü taramalar (< 150 dpi).** Önce yükseltin veya kullanıcıdan daha yüksek çözünürlüklü bir tarama isteyin.  
2. **El yazısı notlar.** Varsayılan model basılı metne odaklanır; el yazısı için özel eğitilmiş bir modele ihtiyacınız olur.  
3. **Birden çok dil.** `RecognitionLanguage`'a virgülle ayrılmış bir liste gönderin, örn., `RecognitionLanguage.ENGLISH_FRENCH`.

```java
ocrEngine.recognizeImage("multilang.png",
        RecognitionLanguage.ENGLISH_FRENCH);
```

## Beklenen Çıktı

`large_invoice.png` üzerinde tam `GpuExample` sınıfını çalıştırmak aşağıdaki gibi bir çıktı vermelidir:

```
Detected text:
Invoice #12345
Date: 2025‑12‑31
Total: $1,234.56
...
```

Eğer anlamsız karakterler görürseniz, `gpuSettings.setEnable(true)`'ın gerçekten etkili olup olmadığını iki kez kontrol edin (hata ayıklama kaydını etkinleştirirseniz konsol GPU cihazını listeleyecektir).

## Yaygın Tuzaklar ve Pro İpuçları

- **GPU cihaz kimliğini ayarlamayı unuttunuz.** Çoklu GPU sistemlerinde `setDeviceId(1)` gerekebilir.  
- **NVIDIA çalışma zamanı olmadan Docker içinde çalıştırma.** `docker run` komutuna `--gpus all` ekleyin.  
- **CPU‑only ve GPU‑enabled kod yollarını karıştırma.** Durum çakışmalarını önlemek için her iş parçacığında tek bir `AsposeOCR` örneği tutun.  
- **Bellek sızıntıları.** Özellikle uzun süren hizmetlerde işi bitirdiğinizde `ocrEngine.dispose()` çağırın.

## Sıkça Sorulan Sorular

**S: Ücretsiz deneme GPU hızlandırmasını destekliyor mu?**  
C: Evet, Aspose OCR denemesi tam GPU desteği içerir; sadece kodda etkinleştirmeniz gerekir.

**S: PDF'leri doğrudan, görüntülere dönüştürmeden işleyebilir miyim?**  
C: Aspose OCR PDF sayfalarını dahili olarak rasterleştirebilir, ancak en iyi performans için önce yüksek çözünürlüklü PNG'ye dönüştürün.

**S: Hangi CUDA sürümü gerekiyor?**  
C: CUDA 11.2 veya daha yenisi önerilir; eski sürümler çalışabilir ancak resmi olarak test edilmemiştir.

**S: Güvenilmeyen kullanıcı yüklemelerinde OCR çalıştırmak güvenli mi?**  
C: İşleme başlamadan önce dosya boyutunu ve tipini doğrulayın ve riskleri azaltmak için OCR'yi sandbox'lanmış bir iş parçacığında çalıştırın.

**S: GPU kullanımını doğrulamak için kaydı nasıl etkinleştiririm?**  
C: `ocrEngine.setDebugMode(true)` ayarlayın; konsol seçilen GPU cihazını ve bellek istatistiklerini listeleyecektir.

## Sonuç

Java'da Aspose OCR için **GPU'yu nasıl etkinleştirileceğini** adım adım inceledik, **görüntüden metni nasıl tanıyacağınızı** gösterdik, **PNG'den metin çıkarmanın** en basit yolunu gösterdik, **görüntü işleme seçeneklerini nasıl ayarlayacağınızı** açıkladık ve gerçek dünyadaki dosyalarda **metni nasıl tanıyacağınızı** detaylandırdık. GPU etkinleştirildiğinde OCR hattınız belirgin şekilde daha hızlı olacaktır; bu da toplu fatura işleme veya canlı belge tarama gibi yüksek hacimli senaryolar için uygundur.

Bir sonraki adıma hazır mısınız? Varsayılan İngilizce modeli çok dilli bir modelle değiştirin veya gürültülü makbuzlar için özel ön işleme boru hatlarıyla deney yapın. Gökyüzü sınırdır—özellikle ağır işleri GPU üstlendiğinde.

**Son Güncelleme:** 2026-08-22  
**Test Edilen Versiyon:** Aspose OCR for Java 24.10  
**Yazar:** Aspose

## İlgili Öğreticiler

- [Aspose OCR Tam Java OCR Öğreticisi ile Görüntüden Metin Tanıma](/ocr/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Java'da Aspose OCR Lisansını Ayarlama ve Doğrulama](/ocr/java/ocr-basics/set-license/)
- [Aspose.OCR Detect Areas Modu ile Java'da Görüntüden Metin Çıkarma](/ocr/java/ocr-operations/perform-ocr-detect-areas-mode/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}