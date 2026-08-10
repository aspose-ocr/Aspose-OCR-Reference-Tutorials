---
category: general
date: 2026-02-14
description: Aspose OCR Java'da GPU'yu etkinleştirerek görüntüden hızlı bir şekilde
  metin çıkarmayı öğrenin. TIFF'i metne dönüştürmeyi, GPU cihaz kimliğini ayarlamayı
  ve TIFF dosyalarından metin okumayı keşfedin.
draft: false
keywords:
- how to enable gpu
- extract text from image
- convert tiff to text
- set gpu device id
- read text from tiff
language: tr
og_description: Aspose OCR Java'da GPU'yu etkinleştirerek görüntüden hızlı bir şekilde
  metin çıkarmak. TIFF'i metne dönüştürmek, GPU cihaz kimliğini ayarlamak ve TIFF'ten
  metin okumak için bu kılavuzu izleyin.
og_title: GPU'yu OCR için nasıl etkinleştirirsiniz – TIFF'ten Metin Çıkarma
tags:
- OCR
- Java
- GPU acceleration
title: GPU'yu OCR için nasıl etkinleştirir ve TIFF'ten metin çıkarılır
url: /tr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-and-extract-text-from-tiff/
---

.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# GPU'yi OCR için nasıl etkinleştirir ve TIFF'ten metin çıkarılır

Büyük TIFF dosyalarında OCR yaparken **GPU'yi nasıl etkinleştireceğinizi** hiç merak ettiniz mi? Tek başınıza değilsiniz—geliştiriciler özellikle kaynak görüntü çok megabaytlık bir TIFF olduğunda ekstra hız artışı peşinde koşuyor. İyi haber? Aspose OCR for Java ile bir anahtarı çevirip, doğru GPU'yu işaretleyebilir ve motorun görüntü üzerinden koştuğunu izleyebilirsiniz.

Bu öğreticide tüm iş akışını adım adım inceleyeceğiz: bir TIFF'i yükleme, GPU hızlandırmasını açma, isteğe bağlı olarak belirli bir GPU cihazı seçme, OCR çalıştırma ve sonunda **görüntüden metin çıkarma**. Sonunda birkaç satır kodla **TIFF'i metne dönüştürebilecek** ve ayrıca **TIFF dosyalarından metin okuma** konusunda desteklenen herhangi bir platformda nasıl yapılacağını göreceksiniz.

## Gereksinimler

- Java 17 veya daha yenisi (kod Java 8+ ile de çalışır)
- Aspose OCR for Java 23.10 (veya yazım anındaki en son sürüm)
- En son sürücü yüklü CUDA‑uyumlu bir GPU
- Çok sayfalı bir örnek TIFF (`sample_large.tif` olarak adlandıralım)

Maven sihirbazı yok mu? Sorun değil—JAR dosyasını sınıf yolunuza (classpath) bırakın, hazırsınız.

![Java'da OCR için GPU'yu nasıl etkinleştirir](gpu-ocr.png)

*Görsel alt metni: Java'da OCR için GPU'yu nasıl etkinleştirir*

## Adım 1: OCR için bir TIFF görüntüsü yükleyin

İlk olarak bir `OcrEngine` örneğine ve bir kaynak görüntüye ihtiyacınız var. Aspose OCR neredeyse tüm raster formatlarını okuyabilir, ancak TIFF taranmış belgeler için yaygındır.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the TIFF file – this is where we "read text from TIFF"
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample_large.tif"));
```

> **Neden önemli:** `setImage` çağrısı dosyayı bir `ImageStream` içinde sarar, bu sayede motor çok sayfalı TIFF'leri manuel olarak bölmenize gerek kalmadan işleyebilir. Dosya bulunamazsa net bir `FileNotFoundException` alırsınız—bu yüzden yolu iki kez kontrol edin.

## Adım 2: GPU hızlandırmasını etkinleştirin

Şimdi sihir gerçekleşiyor. GPU'yu açmak sadece bir boolean bayrağıdır, ancak işleme süresini saniyeler—hatta dakikalar—kısaltabilir.

```java
        // Enable GPU acceleration (requires a supported driver)
        ocrEngine.getEngineOptions().setUseGpu(true);
```

> **Pro ipucu:** Makinenizde birden fazla GPU varsa, varsayılan genellikle ilkidir (cihaz 0). Aspose'un en iyi cihazı otomatik seçmesine izin verebilirsiniz, ancak belirtmek çoklu GPU iş istasyonlarında sürprizleri önleyebilir.

## Adım 3: GPU cihaz kimliğini ayarla (isteğe bağlı)

Bazen hangi GPU'yu kullanacağınızı tam olarak biliyorsunuzdur—belki ikinci kart AI iş yüklerine ayrılmıştır. İşte `setGpuDeviceId` burada devreye girer.

```java
        // Optional: select the GPU device (0 = first device, 1 = second, etc.)
        ocrEngine.getEngineOptions().setGpuDeviceId(0);
```

> **Köşe durumu:** Geçersiz bir kimlik gönderirseniz, motor `IllegalArgumentException` fırlatır. Hızlı bir `System.out.println(ocrEngine.getEngineOptions().getAvailableGpuDevices())` çağrısı size kimlikleri listeleyebilir.

## Adım 4: Görüntüyü işleyin ve **görüntüden metin çıkarın**

Motor yapılandırıldıktan sonra OCR çalıştırma zamanı. Sonuç nesnesi ham dizeyi verir, ayrıca ihtiyacınız olursa güven puanlarını da içerir.

```java
        // Perform OCR – this is where we "convert TIFF to text"
        OcrResult ocrResult = ocrEngine.process();

        // Output the recognized text
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

### Beklenen çıktı

TIFF içinde “Hello, World!” ifadesi varsa aşağıdakine benzer bir şey görmelisiniz:

```
Recognized text:
Hello, World!
```

Motor satır sonlarını, noktalama işaretlerini ve hatta temel düzen algılamasını yönetir. Daha ayrıntılı kontrol için (ör. sayfa başına metin çıkarma) `ocrResult.getPages()`'i inceleyin.

## Adım 5: Çıktıyı doğrulayın ve yaygın sorunları ele alın

### GPU neden kullanılmayabilir?

- **Sürücü uyumsuzluğu:** GPU sürücüsü Aspose tarafından önerilen sürümden en az olmalıdır (sürüm notlarını kontrol edin).
- **Yetersiz bellek:** Çok büyük görüntüler GPU VRAM'ını aşabilir. Bu durumda motor, uyarıyı konsolda göstererek sorunsuz bir şekilde CPU'ya geri döner.
- **Desteklenmeyen donanım:** Entegre grafikler genellikle gereken hesaplama yeteneğine sahip değildir.

### Programatik olarak CPU'ya nasıl geri dönülür

```java
if (!ocrEngine.getEngineOptions().isGpuAvailable()) {
    System.out.println("GPU not available – switching to CPU.");
    ocrEngine.getEngineOptions().setUseGpu(false);
}
```

### Döngü içinde TIFF'ten metin okuma

Eğer bir klasörde çok sayıda TIFF varsa, döngüyle işleyebilirsiniz:

```java
File folder = new File("YOUR_DIRECTORY");
for (File file : folder.listFiles((dir, name) -> name.toLowerCase().endsWith(".tif"))) {
    ocrEngine.setImage(ImageStream.fromFile(file.getAbsolutePath()));
    OcrResult result = ocrEngine.process();
    System.out.println("File: " + file.getName());
    System.out.println(result.getText());
}
```

Bu kod parçacığı, **TIFF dosyalarından toplu olarak metin okuma** işlemini gösterir ve aynı zamanda GPU hızlandırmasından faydalanmaya devam eder.

## Sıkça Sorulan Sorular (SSS)

**S: Bu Linux'ta çalışır mı?**  
C: Kesinlikle—Aspose OCR çapraz platformdur. Sadece CUDA araç seti ve sürücülerin yüklü olduğundan emin olun.

**S: GPU'm yoksa ne olur?**  
C: `setUseGpu(false)` ayarlayın veya çağrıyı tamamen atlayın. Motor varsayılan olarak CPU'yu kullanır.

**S: Başka formatlardan metin çıkarabilir miyim?**  
C: Evet, aynı `setImage` metodu JPEG, PNG, BMP ve hatta PDF akışlarını kabul eder.

**S: Düşük çözünürlüklü TIFF'lerde OCR doğruluğu ne kadar?**  
C: Doğruluk 300 dpi'nin altına düştüğünde azalır. Görüntüyü motorun önüne göndermeden önce ön işleme (ikiliye çevirme, eğikliği düzeltme) yapmayı düşünün.

## Sonuç

Artık Aspose OCR Java için **GPU'yu nasıl etkinleştireceğinizi**, **GPU cihaz kimliğini nasıl ayarlayacağınızı** ve en önemlisi **görüntü dosyalarından metin nasıl çıkaracağınızı**, özellikle **TIFF'i metne dönüştürme** ve **TIFF'ten metin okuma** konularını biliyorsunuz. Tek bir bayrağı değiştirerek ve isteğe bağlı olarak bir cihaz seçerek, OCR mantığını yeniden yazmadan büyük performans artışları elde edersiniz.

Bir sonraki adıma hazır mısınız? Şunları deneyin:

- Yüzlerce TIFF'i paralel iş parçacıklarında **toplu işleme**.
- Özelleştirilmiş belgelerde tanıma iyileştirmek için **özel dil paketleri**.
- Çıkarılan dizeyi biçimlendirmeyi temizlemek için regex ile **son işleme**.

Herhangi bir sorunla karşılaşırsanız yorum bırakmaktan çekinmeyin, iyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}