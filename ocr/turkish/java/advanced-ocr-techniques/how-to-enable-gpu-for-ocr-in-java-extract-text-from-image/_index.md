---
category: general
date: 2026-02-27
description: Aspose OCR Java kodunda GPU'yu etkinleştirerek görüntüden metin çıkarma
  yöntemini öğrenin. Fotoğrafı metne dönüştürün ve fotoğraftan metni verimli bir şekilde
  tanıyın.
draft: false
keywords:
- how to enable gpu
- extract text from image
- convert photo to text
- how to extract text
- recognize text from photo
language: tr
og_description: Aspose OCR Java'da GPU'yu nasıl etkinleştirir ve görüntüden hızlıca
  metin çıkarırsınız. Fotoğrafı metne dönüştürün ve fotoğraftan metni kolayca tanıyın.
og_title: Java'da OCR için GPU'yu Nasıl Etkinleştirirsiniz – Hızlı Metin Çıkarma
tags:
- OCR
- Java
- GPU
- Aspose
title: Java'da OCR için GPU'yu Nasıl Etkinleştirirsiniz – Görüntüden Metin Çıkarma
url: /tr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da OCR için GPU'yu Nasıl Etkinleştirirsiniz – Görüntüden Metin Çıkarma

Yüksek çözünürlüklü bir fotoğrafta OCR çalıştırırken **GPU'nun nasıl etkinleştirileceğini** hiç merak ettiniz mi? Yalnız değilsiniz. Birçok Java geliştiricisi, OCR boru hattı yalnızca CPU ortamında yavaşladığında, özellikle görüntü boyutu birkaç megapikseli aştığında bir duvara çarpar. İyi haber? Aspose OCR ile GPU hızlandırmasını etkinleştirmek çok kolay ve **görüntüden metin çıkarma** dosyalarını çok daha kısa sürede yapmanızı sağlar.

Bu öğreticide tüm süreci adım adım inceleyeceğiz: Aspose OCR kütüphanesini kurmaktan, GPU bayrağını açmaya, büyük bir resmi beslemeye ve sonunda **fotoğrafı metne dönüştürmeye** kadar. Sonunda **metni nasıl çıkaracağınızı** güvenilir bir şekilde öğrenecek ve çoklu GPU'lu makinelerde **fotoğraftan metin tanıma** nasıl yapılacağını göreceksiniz. Harici referanslara gerek yok—gereken her şey burada.

## Önkoşullar

* Java 17 veya daha yeni bir sürüm yüklü (en son LTS sürümü en iyisidir).
* Desteklenen bir NVIDIA veya AMD GPU ve güncel sürücüler (NVIDIA için CUDA 12.x, AMD için ROCm).
* Aspose OCR for Java JAR'ları—en son 23.x sürümünü Aspose web sitesinden indirin.
* Bağımlılıkları yönetmek için Maven veya Gradle (bir Maven örneği göstereceğiz).
* İşlemek istediğiniz yüksek çözünürlüklü bir görüntü (ör. `high-res-photo.jpg`).

Bu öğelerden herhangi biri eksikse, kod hâlâ derlenecek ancak GPU bayrağı göz ardı edilecek ve CPU işleme geri döneceksiniz.

## 1. Adım – Aspose OCR'ı Build'ınıza Ekleyin (GPU'yu Nasıl Etkinleştirirsiniz)

İlk iş olarak: projenize OCR kütüphanesinin nerede olduğunu söyleyin. Maven'da `pom.xml` dosyanıza aşağıdaki bağımlılığı ekleyin:

```xml
<!-- Step 1: Include Aspose OCR for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

> **Pro tip:** Gradle kullanıyorsanız eşdeğeri `implementation 'com.aspose:aspose-ocr:23.10'` şeklindedir. Kütüphaneyi güncel tutmak, en yeni GPU çekirdeklerini ve hata düzeltmelerini almanızı sağlar.

Artık kütüphane sınıf yolunda olduğuna göre, OCR motorunda **GPU'yu etkinleştirebiliriz**.

## 2. Adım – OCR Motorunu Oluşturun ve GPU'yu Açın (GPU'yu Nasıl Etkinleştirirsiniz)

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2.1: Instantiate the OCR engine – this is the core object.
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2.2: Enable GPU acceleration.
        // This is the line that answers the question "how to enable gpu".
        ocrEngine.getConfig().setUseGpu(true);

        // Optional: If your system has more than one GPU, pick the one you want.
        // The device ID is zero‑based, so 0 refers to the first GPU.
        // ocrEngine.getConfig().setGpuDeviceId(0);

        // Step 2.3: Process the image and get the result.
        OcrResult ocrResult = ocrEngine.processImage("YOUR_DIRECTORY/high-res-photo.jpg");

        // Step 2.4: Print the recognized text – now you have converted photo to text.
        System.out.println(ocrResult.getText());
    }
}
```

> **Neden önemli:** `setUseGpu(true)` ayarı, yerel kütüphaneye yoğun konvolüsyonel sinir ağı işini GPU'ya devretmesini söyler. Modern bir RTX 3080'de, CPU'da 8 saniye süren aynı görüntü 1 saniyenin altında işlenebilir. Bu adımı atlayıp **fotoğraftan metin tanıma** yapabilirsiniz, ancak performans artışını kaçırırsınız.

## 3. Adım – GPU'nun Gerçekten Kullanıldığını Doğrulayın

“GPU gerçekten işi yapıyor mu?” diye merak edebilirsiniz. En kolay yol, debug kaydını etkinleştirdiğinizde Aspose OCR kütüphanesinin konsol çıktısına bakmaktır:

```java
// Enable verbose logging – helpful for confirming GPU usage.
ocrEngine.getConfig().setLogLevel(com.aspose.ocr.Config.LogLevel.DEBUG);
```

Programı çalıştırdığınızda şu satırları göreceksiniz:

```
[DEBUG] Using GPU device 0 (NVIDIA GeForce RTX 3080) for OCR processing.
```

Bu mesajı görmüyorsanız, sürücü kurulumunuzu tekrar kontrol edin ve GPU'nun minimum hesaplama yeteneğini (NVIDIA için 3.5, AMD için 6.0) karşıladığından emin olun.

## 4. Adım – Çoklu GPU'lar ve Kenar Durumlarını Yönetme

### Farklı Bir GPU Seçme

İş istasyonunuzda birden fazla GPU varsa (örneğin entegre bir Intel GPU ve ayrı bir NVIDIA kartı), daha hızlı olanı hedefleyebilirsiniz:

```java
ocrEngine.getConfig().setGpuDeviceId(1); // 1 = second GPU in the system
```

### GPU Algılanmazsa Ne Olur?

Aspose OCR, uygun bir GPU bulamadığında sorunsuzca CPU'ya geri döner. Sessiz geri dönüşü önlemek için bir koruma ekleyebilirsiniz:

```java
if (!ocrEngine.getConfig().isGpuAvailable()) {
    throw new IllegalStateException("No compatible GPU found – cannot enable GPU acceleration.");
}
```

### Büyük Görüntüler ve Bellek Sınırları

100 MP bir görüntüyü işlemek hâlâ GPU belleğini tüketebilir. Pratik bir taktik, metin netliğini korurken **yeterince** küçültmek ve bellek sınırları içinde kalmaktır:

```java
ocrEngine.getConfig().setMaxImageDimension(4096); // caps width/height to 4096px
```

### Desteklenen Görüntü Formatları

Aspose OCR JPEG, PNG, BMP, TIFF ve hatta PDF formatlarını anlar. Farklı bir formatta **görüntüden metin çıkarma** dosyalarınız varsa, önce ImageIO gibi bir kütüphane ile dönüştürün.

## 5. Adım – Beklenen Çıktı ve Doğrulama

Program tamamlandığında, konsol ham OCR metnini yazdıracaktır. Tipik bir fiş fotoğrafı için şöyle bir şey görebilirsiniz:

```
Store: Coffee Corner
Date: 2026-02-25
Items:
  - Latte $4.50
  - Croissant $2.75
Total: $7.25
```

Çıktı bozuk görünüyorsa, şunları göz önünde bulundurun:

* Görüntünün iyi aydınlatılmış ve aşırı sıkıştırılmamış olduğundan emin olun.
* Metin İngilizce değilse `setLanguage` seçeneğini ayarlayın.
* GPU çekirdek sürümünün sürücünüzle eşleştiğini doğrulayın (eşleşmeyen sürücüler ince hatalara yol açabilir).

## 6. Adım – Ötesine Geçmek: Toplu İşleme ve Asenkron Çağrılar

Gerçek dünyadaki projeler genellikle **görüntüden metin çıkarma** koleksiyonlarıyla çalışır. Yukarıdaki mantığı bir döngü içinde sarabilir veya Java’nın `CompletableFuture`'ını kullanarak birden fazla OCR işini paralel olarak, her birini ayrı bir GPU akışı üzerinde (donanım destekliyorsa) çalıştırabilirsiniz. İşte hızlı bir taslak:

```java
import java.util.concurrent.*;
import java.nio.file.*;

public class BatchGpuOcr {
    public static void main(String[] args) throws Exception {
        ExecutorService pool = Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors());

        Files.list(Paths.get("photos/"))
             .filter(p -> p.toString().endsWith(".jpg"))
             .forEach(path -> pool.submit(() -> {
                 OcrEngine engine = new OcrEngine();
                 engine.getConfig().setUseGpu(true);
                 OcrResult result = engine.processImage(path.toString());
                 System.out.println("Result for " + path.getFileName() + ":\n" + result.getText());
             }));

        pool.shutdown();
        pool.awaitTermination(1, TimeUnit.HOURS);
    }
}
```

Bu yaklaşım, **fotoğrafı metne dönüştürme** işlemini ölçekli bir şekilde yaparken GPU hızlandırmasından yararlanmanızı sağlar.

## Sıkça Sorulan Sorular (SSS)

**S: Bu macOS'ta çalışır mı?**  
C: Evet, Metal‑uyumlu bir GPU ve macOS için uygun Aspose OCR ikili dosyası olduğu sürece çalışır. Aynı `setUseGpu(true)` çağrısı geçerlidir.

**S: Ücretsiz Community Edition'ı kullanabilir miyim?**  
C: Community Edition yalnızca CPU‑tabanlı çıkarım içerir. GPU'yu açmak için lisanslı bir sürüm (veya GPU desteği olan bir deneme) gerekir.

**S: İngilizce dışındaki bir dilde **fotoğraftan metin tanıma** yapmam gerekirse ne yapmalıyım?**  
C: `ocrEngine.getConfig().setLanguage("spa")` gibi bir çağrı yaparak İspanyolca, `"fra"` ile Fransızca vb. dilleri seçebilirsiniz. Dil paketleri kütüphane ile birlikte gelir.

**S: Her kelime için güven skorları almak mümkün mü?**  
C: Evet—`ocrResult.getWords()` bir koleksiyon döndürür ve her `Word` nesnesinin `getConfidence()` metodu bulunur.

## Sonuç

Aspose OCR için Java'da **GPU'yu nasıl etkinleştirileceğini** ele aldık, çalıştırılabilir bir örnek üzerinden geçtik ve **görüntüden metin çıkarma**, **fotoğrafı metne dönüştürme** veya **fotoğraftan metin tanıma** istediğinizde karşılaşabileceğiniz yaygın sorunları inceledik. Tek bir bayrağı değiştirip sürücülerinizi güncel tutarak, her OCR çağrısında saniyeler kazanabilir ve büyük görüntü topluluklarını sorunsuzca ölçeklendirebilirsiniz.

Bir sonraki adıma hazır mısınız? OCR çıktısını bir doğal dil işleme hattına besleyin ya da doğruluğu artırmak için farklı görüntü ön‑işleme filtreleri deneyin. GPU‑destekli OCR ile modern Java araçlarını birleştirdiğinizde sınır yoktur.

---

![Diagram showing how to enable GPU in Aspose OCR Java code – how to enable gpu](gpu-ocr-diagram.png)

*Görsel alt metni:* "Aspose OCR Java kodunda GPU'nun nasıl etkinleştirileceğini gösteren diyagram – nasıl GPU etkinleştirilir"

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}