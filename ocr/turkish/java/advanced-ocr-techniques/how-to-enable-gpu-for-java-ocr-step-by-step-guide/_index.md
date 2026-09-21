---
category: general
date: 2026-01-12
description: Java OCR'de GPU'yu etkinleştirerek görüntüden hızlı metin çıkarma. GPU'yu
  nasıl yapılandıracağınızı, metin çıkarımını ve Aspose OCR ile Java'da metin tanımayı
  öğrenin.
draft: false
keywords:
- how to enable gpu
- extract text from image
- how to extract text
- how to configure gpu
- recognize text java
language: tr
og_description: Java OCR'de GPU'yu hızlıca nasıl etkinleştirirsiniz. Bu rehber, GPU'yu
  nasıl yapılandıracağınızı, görüntüden metin çıkartmayı ve Aspose OCR kullanarak
  Java'da metni tanımayı gösterir.
og_title: Java OCR için GPU Nasıl Etkinleştirilir – Tam Rehber
tags:
- OCR
- Java
- GPU
- Aspose
title: Java OCR için GPU'yu Etkinleştirme – Adım Adım Rehber
url: /tr/java/advanced-ocr-techniques/how-to-enable-gpu-for-java-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java OCR için GPU Nasıl Etkinleştirilir – Tam Kılavuz

Bir görüntüden Java ile metin çıkarırken **GPU'yu nasıl etkinleştirirsiniz** diye hiç merak ettiniz mi? Tek başınıza değilsiniz. Birçok geliştirici yüksek çözünürlüklü taramaları işlerken performans sınırına takılıyor ve tek bir GPU'nun OCR çalışma süresini saniyeler—hatta dakikalar—kısaltabileceğini keşfediyor.

Bu öğreticide, GPU hızlandırmasını açma, istediğiniz cihazı yapılandırma ve sonunda Aspose OCR kütüphanesini kullanarak **java‑style metin tanıma** işlemini gerçekleştirme adımlarını adım adım göstereceğiz. Sonunda, görüntüden ışık hızında metin çıkaran çalıştırılabilir bir programınız olacak.

## Neler Öğreneceksiniz

Şunları kapsayacağız:

* Aspose OCR SDK for Java’yı nasıl kuracağınız.  
* Bir `OcrEngine` oluşturup yüksek çözünürlüklü bir PNG'yi nasıl yükleyeceğiniz.  
* **GPU'yu nasıl yapılandıracağınız** – etkinleştirme, cihaz kimliğini seçme ve GPU bulunmadığında geri dönüşü yönetme.  
* **Görüntüden metin çıkarma** ve sonucu yazdırma için tam kod.  
* Sorun giderme ipuçları, kenar‑durum yönetimi ve sonraki adımlar.

**Önkoşullar** – Java 17+ JDK, Maven veya Gradle ve en az bir CUDA‑uyumlu GPU’ya sahip bir makine. Başka bir kütüphane gerekmez.

---

![GPU'yu etkinleştirme illüstrasyonu](placeholder.png "GPU hızlandırmalı Java OCR boru hattını gösteren diyagram – GPU'yu nasıl etkinleştirirsiniz")

## Adım 1 – Aspose OCR'ı Kurun ve Görüntünüzü Hazırlayın (GPU'yu Nasıl Etkinleştirirsiniz)

İlk olarak, Aspose OCR bağımlılığını projenize ekleyin. Maven kullanıyorsanız şunu ekleyin:

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

JAR sınıf yolunuza eklendikten sonra, koddan referans verebileceğiniz bir klasöre yüksek çözünürlüklü bir dosya (ör. `sample-highres.png`) koyun. En iyi OCR doğruluğu için görüntünün en az 300 dpi olması gerekir.

> **Pro ipucu:** Ayrı bir GPU'su olmayan bir dizüstü bilgisayarda test ediyorsanız bile kodu çalıştırabilirsiniz; motor otomatik olarak CPU'ya geri dönecektir.

## Adım 2 – OCR Motorunu Oluşturun ve Görüntüyü Yükleyin (Görüntüden Metin Çıkarma)

Şimdi temel OCR nesnesini başlatıp resmimize yönlendireceğiz. Bu, herhangi bir **görüntüden metin çıkarma** işleminin temelidir.

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

`setImage` çağrısı bir dosya yolu, bir `java.io.File` veya hatta bir `java.awt.image.BufferedImage` alabilir. Yüksek çözünürlüklü bir kaynak kullanmak, GPU'nun yeterli veri almasını sağlar ve bu da belirgin hız artışına dönüşür.

## Adım 3 – GPU Hızlandırmasını Yapılandırın (GPU'yu Nasıl Yapılandırırsınız)

İşte sihrin gerçekleştiği yer. `GpuConfiguration` sınıfı, Aspose'a GPU kullanıp kullanmayacağını ve hangi cihazı seçeceğini söyler. Birden fazla GPU'nuz varsa (ör. entegre Intel GPU ve NVIDIA RTX), en yüksek verimi sağlayanı seçebilirsiniz.

```java
        // Step 3: Enable GPU acceleration (optional: select a specific device)
        GpuConfiguration gpuConfig = new GpuConfiguration();
        gpuConfig.setEnabled(true);          // turn on GPU support
        gpuConfig.setDeviceId(0);            // choose GPU 0 (default first device)

        // Attach the GPU config to the OCR engine
        ocrEngine.setGpuConfiguration(gpuConfig);
```

**GPU'yu neden etkinleştirirsiniz?** OCR boru hattı bir dizi konvolüsyonel sinir ağı çalıştırır. Bu ağları bir GPU’da çalıştırmak paralel çekirdeklerden yararlanır ve çıkarım süresini dramatik şekilde azaltır. Belirtilen cihaz mevcut değilse, Aspose sessizce CPU'ya geri döner, böylece uygulamanız çökmez.

### Kenar‑Durum Yönetimi

```java
        // Verify that a GPU was actually engaged
        if (!gpuConfig.isEnabled() || !gpuConfig.isDeviceAvailable()) {
            System.out.println("GPU not detected – falling back to CPU. " +
                               "Performance will be slower.");
        }
```

`isDeviceAvailable()` yöntemi CUDA sürücüsü varlığını kontrol eder; bu da kodun geliştirme makineleri ve CI boru hatları arasında dayanıklı olmasını sağlar.

## Adım 4 – Metin Tanıma Gerçekleştirin (Java’da Metin Tanıma)

Motor ve GPU hazır olduğunda, Aspose’dan karakterleri okumasını isteyebiliriz.

```java
        // Step 4: Perform the recognition
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the recognized text
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

`recognize()` çağrısı, düz metin, güven skorları ve gerekirse aşağı akış işlemleri için sınırlayıcı kutu koordinatlarını içeren bir `OcrResult` nesnesi döndürür.

**Beklenen çıktı** (kısaltılmış):

```
Recognized text:
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
```

Görüntü birden fazla dil içeriyorsa şunu ekleyebilirsiniz:

```java
ocrEngine.getLanguage().add(OcrLanguage.FRENCH);
ocrEngine.getLanguage().add(OcrLanguage.SPANISH);
```

## Adım 5 – Çıktıyı İnceleyin ve Sonraki Adımları Planlayın

Programı şu şekilde çalıştırın:

```bash
mvn compile exec:java -Dexec.mainClass=GpuOcrTutorial
```

İyi bir GPU’ya sahip bir makinede, OCR 4 MP bir görüntü için bir saniyenin altında tamamlanmalıdır—CPU’da yalnızca 3‑5 saniyeye kıyasla.

### Yaygın Sorular

* **`CUDA driver version is insufficient` hatası alırsam ne yapmalıyım?**  
  NVIDIA sürücünüzü, Aspose ile gelen CUDA araç setiyle (genellikle 2026 itibarıyla 11.x) eşleşen en yeni sürüme güncelleyin.

* **Bir grup görüntüyü işleyebilir miyim?**  
  Evet. Motor başlatmayı bir döngü içinde sarın, ancak aynı `OcrEngine` örneğini yeniden kullanarak GPU bağlamı oluşturmayı tekrarlamaktan kaçının.

* **Bellek sınırı var mı?**  
  GPU belleği gereksinimi görüntü boyutuyla orantılıdır. Çok büyük TIFF dosyaları için, motorun içine beslemeden önce görüntüyü döşemeyi (tiling) düşünün.

### Pro İpuçları

* **GPU'yu sabitleyin** – çok‑GPU sunucularda, `gpuConfig.setDeviceId(1)` ile ikinci GPU’yu OCR için ayırın, birinci GPU diğer iş yüklerini yönetebilir.  
* **Isınma** – başlangıçta küçük bir dummy görüntüde `ocrEngine.recognize()` çağırın; bu sinir ağlarını GPU’ya yükler ve ilk çağrı gecikmesini ortadan kaldırır.  
* **İş parçacığı güvenliği** – her iş parçacığı kendi `OcrEngine` örneğine sahip olmalı; sınıf iş parçacığı‑güvenli değildir.

---

## Sonuç

Sadece birkaç adımda **Java OCR için GPU'yu nasıl etkinleştirirsiniz** gösterdik, Aspose ile **GPU'yu nasıl yapılandırırsınız** örnekledik ve **görüntüden metin çıkarma** ve **java‑style metin tanıma** yapan tam, çalıştırılabilir bir örnek sunduk. `GpuConfiguration`’ı değiştirerek herhangi bir CUDA‑uyumlu cihazda anında performans artışı elde ederken, CPU geri dönüşü uygulamanızın dayanıklılığını korur.

Sırada ne var? PDF’leri beslemeyi deneyin, OCR dil paketleriyle oynayın veya çıktıyı aranabilir bir Elastic indeksine entegre edin. GPU‑hızlandırmalı OCR’u Java’da ustalaştıktan sonra sınır yoktur.

İyi kodlamalar, GPU’larınız serin kalsın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}