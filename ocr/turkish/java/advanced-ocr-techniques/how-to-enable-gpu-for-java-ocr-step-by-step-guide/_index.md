---
category: general
date: 2026-11-17
description: Java OCR'de GPU'yu etkinleştirerek görüntüden hızlı bir şekilde metin
  çıkarın. GPU'yu yapılandırmayı, metin çıkarmayı ve Aspose OCR ile Java metin tanımayı
  öğrenin.
draft: false
keywords:
- how to enable gpu
- high resolution ocr
- aspose ocr java
- extract text image java
- gpu acceleration ocr
lastmod: 2026-11-17
og_description: Java OCR için GPU'yu hızlı bir şekilde etkinleştirin. Bu kılavuz,
  GPU'yu yapılandırmayı, görüntüden metin çıkarmayı ve Aspose OCR kullanarak Java
  ile metin tanımayı gösterir.
og_image_alt: 'Developer guide: Enable GPU for Java OCR using Aspose OCR library'
og_title: Java OCR için GPU'yu nasıl etkinleştirirsiniz – adım adım kılavuz
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: How to enable GPU in Java OCR to extract text from image fast. Learn
    how to configure GPU, extract text and recognize text java with Aspose OCR.
  headline: How to enable GPU for Java OCR – step‑by‑step guide
  type: TechArticle
- questions:
  - answer: Yes, you can pass a PDF file directly to `setImage`; the library rasterizes
      each page before OCR.
    question: Does Aspose OCR support PDF input?
  - answer: Use `ocrEngine.getConfiguration().setCustomDictionary(List<String>)` to
      improve recognition of specialized vocabulary.
    question: How do I add custom dictionaries for domain‑specific terms?
  - answer: Currently only CUDA‑compatible NVIDIA GPUs on Windows and Linux are supported;
      macOS users fall back to CPU.
    question: Is GPU acceleration available on macOS?
  - answer: Absolutely—`OcrResult` includes a `getConfidence()` method for each `OcrWord`
      object.
    question: Can I retrieve the confidence score for each recognized word?
  - answer: A commercial Aspose OCR license is required for production deployments;
      a free evaluation license works for development and testing.
    question: What license is required for production use?
  type: FAQPage
tags:
- gpu ocr
- java ocr
- aspose ocr
- high resolution ocr
- java image processing
title: Java OCR için GPU'yu nasıl etkinleştirirsiniz – adım adım kılavuz
url: /tr/java/advanced-ocr-techniques/how-to-enable-gpu-for-java-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java OCR için GPU'yu nasıl etkinleştirirsiniz – adım adım kılavuz

Java ile görüntülerden metin çıkarırken **GPU'yu nasıl etkinleştirirsiniz** sorusunun cevabını arıyorsanız doğru yerdesiniz. GPU hızlandırması, OCR işleme süresini birkaç saniyeden bir saniyenin çok altına düşürebilir, özellikle yüksek çözünürlüklü taramalarda. Bu kılavuzda Aspose OCR'ı kurmayı, GPU cihazını yapılandırmayı ve GPU destekli ve sadece CPU çalışan makinelerde güvenilir şekilde çalışan tam bir metin çıkarma programını çalıştırmayı adım adım göstereceğiz.

## Hızlı cevaplar
- **Java minimum sürümü nedir?** Java 17 veya daha yeni.
- **Hangi GPU tipi gereklidir?** CUDA uyumlu herhangi bir NVIDIA GPU (CUDA 11+).
- **Örneği çalıştırmak için lisans gerekiyor mu?** Geliştirme için ücretsiz deneme yeterlidir; üretim için ticari lisans gerekir.
- **GPU OCR ne kadar daha hızlı?** CPU'ya kıyasla 4 MP bir görüntüde 5 katına kadar hız artışı.
- **CPU'ya otomatik olarak geri dönülebilir mi?** Evet—Aspose OCR, GPU bulunamadığında CPU'ya geçer.

## OCR için GPU hızlandırması nedir?
OCR için GPU hızlandırması, sinir ağı çıkarım adımlarını CPU yerine bir grafik işlemci üzerinde çalıştırmak anlamına gelir; bu da binlerce paralel işlem yapılmasını sağlar. Bu, özellikle CPU'nun darboğaz oluşturabileceği yüksek çözünürlüklü görüntülerde çıkarım gecikmesini büyük ölçüde azaltır.

## Java için Aspose OCR neden kullanılmalı?
Aspose OCR **50+ giriş formatını** (PNG, JPEG, TIFF, PDF dahil) destekler ve tüm dosyayı belleğe yüklemeden çok sayfalı belgeleri işleyebilir. Java API'si, düşük seviyeli CUDA çağrılarını soyutlayan tek bir `OcrEngine` sınıfı sunar, böylece iş mantığınıza odaklanabilirsiniz.

## Önkoşullar
- Java 17+ JDK kurulu.
- Bağımlılık yönetimi için Maven 3.6+ veya Gradle 7+.
- CUDA uyumlu NVIDIA GPU ve CUDA 11.x veya daha yeni sürücüleri.
- Aspose OCR kütüphanesini indirmek için internet erişimi.

## Java OCR için GPU nasıl etkinleştirilir?
Aspose OCR kütüphanesini yükleyin, bir `OcrEngine` oluşturun ve sadece birkaç satır kodla GPU desteğini açın. Motor, mevcut cihazları otomatik olarak algılar; çoklu GPU ortamlarında belirli bir GPU'yu hedeflemek için cihaz kimliği de belirtebilirsiniz.

## OcrEngine nasıl çalışır?
`OcrEngine`, görüntü ön işleme, sinir ağı çıkarımı ve sonuç toplama işlemlerini yöneten merkezi sınıftır. Görüntüleri dosya yolu, `java.io.File` nesnesi veya `java.awt.image.BufferedImage` örnekleri olarak kabul eder, böylece veriyi pipeline'a nasıl besleyeceğiniz konusunda esneklik sağlar.

## GPU hızlandırmasını nasıl yapılandırılır (GPU nasıl yapılandırılır)
Aspose OCR'ı GPU'yu kullanacak şekilde ve hangi cihazı seçeceğinizi burada belirtirsiniz.

GPU hızlandırmasını etkinleştirmek için bir `GpuConfiguration` örneği oluşturur, `setEnable(true)` çağırır, isteğe bağlı olarak `setDeviceId(int)` ile bir cihaz seçer ve `setGpuConfiguration` ile `OcrEngine`e ekleriz. Konfigürasyon ayrıca, istenen cihaz mevcut değilse CPU'ya geri dönme stratejisini tanımlamanıza da olanak tanır, böylece uygulama kararlı kalır.  

```java
        // Step 3: Enable GPU acceleration (optional: select a specific device)
        GpuConfiguration gpuConfig = new GpuConfiguration();
        gpuConfig.setEnabled(true);          // turn on GPU support
        gpuConfig.setDeviceId(0);            // choose GPU 0 (default first device)

        // Attach the GPU config to the OCR engine
        ocrEngine.setGpuConfiguration(gpuConfig);
```

GPU'yu neden etkinleştirirsiniz? OCR pipeline'ı birkaç konvolüsyonel sinir ağı çalıştırır. Bu ağları bir GPU'da çalıştırmak, binlerce paralel çekirdeği kullanarak çıkarım süresini CPU'da 3–5 saniyeden modern bir RTX 3080'de 4 MP bir görüntü için 1 saniyenin altına düşürür. Belirtilen cihaz bulunamazsa, Aspose sessizce CPU'ya geçer ve çökme riskini önler.

### Kenar‑durum işleme

GPU çalışması denemeden önce bir CUDA sürücüsünün kurulu olduğunu doğrulamak gerekir.

```java
        // Verify that a GPU was actually engaged
        if (!gpuConfig.isEnabled() || !gpuConfig.isDeviceAvailable()) {
            System.out.println("GPU not detected – falling back to CPU. " +
                               "Performance will be slower.");
        }
```

## Adım 1 – Aspose OCR'ı kurun ve görüntünüzü hazırlayın (GPU'yu nasıl etkinleştirirsiniz)

İlk olarak Aspose OCR bağımlılığını projenize ekleyin. Maven kullanıyorsanız şunu ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- latest as of Jan 2026 -->
</dependency>
```

Gradle kullanıcıları şunu ekleyebilir:

```groovy
implementation 'com.aspose:aspose-ocr:23.9'
```

Koddan referans verebileceğiniz bir klasöre yüksek çözünürlüklü bir dosya (ör. `sample-highres.png`) koyun. En iyi OCR doğruluğu için görüntünün en az 300 dpi olması gerekir.

> **İpucu:** Ayrı bir GPU'su olmayan bir dizüstü bilgisayarda test ediyorsanız, kod hâlâ çalışır; motor otomatik olarak CPU'ya geri döner.

![GPU'yu etkinleştirme illüstrasyonu](placeholder.png "GPU hızlandırmalı Java OCR pipeline'ını gösteren diyagram – GPU'yu etkinleştirme")
[GPU'yu etkinleştirme illüstrasyonu](placeholder.png "GPU hızlandırmalı Java OCR pipeline'ını gösteren diyagram – GPU'yu etkinleştirme")

## Adım 2 – OCR motorunu oluşturun ve görüntüyü yükleyin (görüntüden metin çıkarma)

`OcrEngine` sınıfı, tek bir OCR oturumunu temsil eden üst‑seviye nesnedir.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.gpu.*;

public class GpuOcrTutorial {
    public static void main(String[] args) throws Exception {

        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image you want to process
        // Replace with the absolute or relative path to your PNG/JPEG/TIFF
        ocrEngine.setImage("YOUR_DIRECTORY/sample-highres.png");
```

`setImage` metodu bir dosya yolu, bir `java.io.File` veya bir `java.awt.image.BufferedImage` kabul eder. Yüksek çözünürlüklü bir kaynak sağlamak, GPU'nun tüm çekirdeklerini meşgul tutar ve bu da belirgin hız artışına dönüşür.

## Adım 3 – GPU hızlandırmasını yapılandırın (GPU nasıl yapılandırılır)

`GpuConfiguration` nesnesi, GPU kullanımını etkinleştirmenize, bir cihaz seçmenize ve OCR motoru için geri dönüş davranışını tanımlamanıza olanak verir.

```java
        // Step 3: Enable GPU acceleration (optional: select a specific device)
        GpuConfiguration gpuConfig = new GpuConfiguration();
        gpuConfig.setEnabled(true);          // turn on GPU support
        gpuConfig.setDeviceId(0);            // choose GPU 0 (default first device)

        // Attach the GPU config to the OCR engine
        ocrEngine.setGpuConfiguration(gpuConfig);
```

## Adım 4 – Metin tanıma gerçekleştirin (java metin tanıma)

Motor ve GPU hazır olduğunda karakterleri nihayet çıkarabilirsiniz.

`recognize()` metodu OCR pipeline'ını çalıştırır ve düz metin, güven puanları ve isteğe bağlı sınırlama kutusu verileri içeren bir `OcrResult` döndürür.  

```java
        // Step 4: Perform the recognition
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the recognized text
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

**Beklenen çıktı** (kısaltılmış):

```
Recognized text:
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
```

Görüntünüz birden fazla dil içeriyorsa, `recognize()` çağırmadan önce dil paketlerini ekleyebilirsiniz:

```java
ocrEngine.getLanguage().add(OcrLanguage.FRENCH);
ocrEngine.getLanguage().add(OcrLanguage.SPANISH);
```

## Adım 5 – Çıktıyı gözden geçirin ve sonraki adımlara geçin

Programı şu şekilde çalıştırın:

```bash
mvn compile exec:java -Dexec.mainClass=GpuOcrTutorial
```

İyi bir GPU'ya sahip bir makinede OCR, **4 MP bir görüntü için bir saniyenin altında** tamamlanır; CPU'da ise 3–5 saniye sürer. Bu hız artışı, toplu işleme senaryoları veya gerçek zamanlı belge alım hatları için özellikle değerlidir.

### Yaygın sorular

* **“CUDA sürücü sürümü yetersiz” hatası alırsam ne yapmalıyım?**  
  NVIDIA sürücünüzü, Aspose ile paketlenen CUDA araç setiyle (genellikle 2026 itibarıyla CUDA 11.x) eşleşen en son sürüme güncelleyin.

* **Bir dizi görüntüyü işleyebilir miyim?**  
  Evet. Tek bir `OcrEngine` örneğini bir döngü içinde yeniden kullanarak GPU bağlamı oluşturma maliyetini azaltabilir ve verimliliği artırabilirsiniz.

* **Bellek sınırı var mı?**  
  GPU bellek kullanımı görüntü boyutuyla orantılıdır; çok büyük TIFF'ler için resmi motorun içine beslemeden önce parçalara bölerek tipik 8 GB GPU bellek sınırları içinde kalın.

### Pro ipuçları

* **GPU'yu sabitleyin** – çoklu GPU sunucularında `gpuConfig.setDeviceId(1)` ile ikinci GPU'yu OCR için ayırın, birincisi diğer işler için kullanılabilir.  
* **Isınma** – başlangıçta küçük bir dummy görüntüde `ocrEngine.recognize()` çağırın; bu, sinir ağlarını GPU'ya yükleyerek ilk çağrı gecikmesini ortadan kaldırır.  
* **İş parçacığı güvenliği** – her iş parçacığı kendi `OcrEngine` örneğine sahip olmalı; sınıf iş parçacığı güvenli değildir, paylaşım yarış koşullarına yol açabilir.

## Sıkça Sorulan Sorular

**S: Aspose OCR PDF girişini destekliyor mu?**  
C: Evet, bir PDF dosyasını doğrudan `setImage` ile geçirebilirsiniz; kütüphane her sayfayı rasterleştirip OCR uygular.

**S: Alan‑spesifik terimler için özel sözlükler ekleyebilir miyim?**  
C: `ocrEngine.getConfiguration().setCustomDictionary(List<String>)` kullanarak özelleştirilmiş sözlük ekleyebilir ve belirli terminoloji tanımasını iyileştirebilirsiniz.

**S: macOS'ta GPU hızlandırması mevcut mu?**  
C: Şu anda sadece Windows ve Linux'ta CUDA uyumlu NVIDIA GPU'lar destekleniyor; macOS kullanıcıları CPU'ya geri döner.

**S: Tanınan her kelime için güven puanını alabilir miyim?**  
C: Kesinlikle—`OcrResult` her `OcrWord` nesnesi için bir `getConfidence()` metodu içerir.

**S: Üretim kullanımı için hangi lisans gerekir?**  
C: Üretim dağıtımları için ticari bir Aspose OCR lisansı gereklidir; geliştirme ve test için ücretsiz bir değerlendirme lisansı yeterlidir.

---

**Son Güncelleme:** 2026-11-17  
**Test Edildi:** Aspose OCR 24.11 for Java  
**Yazar:** Aspose  






```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- latest as of Jan 2026 -->
</dependency>
```

```groovy
implementation 'com.aspose:aspose-ocr:23.9'
```

## İlgili Eğitimler

- [Aspose Ocr Java Örneği GPU ile Görüntüden Metin Çıkarma](/ocr/java/advanced-ocr-techniques/aspose-ocr-java-example-extract-text-from-image-with-gpu/)
- [GPU Hızlandırmalı Java Ocr ile Görüntüden Metin Tanıma](/ocr/java/advanced-ocr-techniques/recognize-text-from-image-java-ocr-with-gpu-acceleration/)
- [GPU Hızlandırmalı Ocr Eğitim Java Rehberi Hızlı Görüntüden Metne](/ocr/java/advanced-ocr-techniques/gpu-accelerated-ocr-tutorial-java-guide-to-fast-image-to-tex/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}