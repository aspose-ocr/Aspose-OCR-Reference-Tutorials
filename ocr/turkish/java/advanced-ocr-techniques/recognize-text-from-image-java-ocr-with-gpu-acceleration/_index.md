---
category: general
date: 2026-04-29
description: Java'da Aspose OCR kullanarak görüntüden metin tanımayı öğrenin. JPG'den
  metin çıkarma, OCR için görüntüyü yükleme ve GPU cihaz kimliğini ayarlama adımlarını
  içerir.
draft: false
keywords:
- recognize text from image
- extract text from jpg
- how to extract text image
- load image for OCR
- set GPU device ID
language: tr
og_description: Aspose OCR ile görüntüden metni hızlıca tanıyın. Bu kılavuz, OCR için
  görüntünün nasıl yükleneceğini, jpg'den metnin nasıl çıkarılacağını ve GPU cihaz
  kimliğinin nasıl ayarlanacağını gösterir.
og_title: görüntüden metin tanıma – GPU Hızlandırmalı Java OCR
tags:
- Java
- OCR
- GPU
- Aspose
title: Görüntüden Metni Tanıma – GPU Hızlandırmalı Java OCR
url: /tr/java/advanced-ocr-techniques/recognize-text-from-image-java-ocr-with-gpu-acceleration/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# görüntüden metin tanıma – Java OCR GPU Hızlandırması ile

Görüntüden metin tanımaya çalıştınız ve karışık bir çıktı mı aldınız? Tek başınıza değilsiniz. Makbuzları dijitalleştiriyor, pasaportları tarıyor ya da ürün etiketlerinden veri çekiyor olun, OCR kalitesi birçok projede tüm süreci ya başarılı kılar ya da başarısız eder.  

İyi haber? Aspose OCR ile **görüntüden metin tanıyabilirsiniz** sadece birkaç saniye içinde ve eğer CUDA‑uyumlu bir GPU’nuz varsa işleme süresini daha da azaltabilirsiniz. Bu öğreticide OCR için bir görüntüyü yüklemeyi, GPU hızlandırmasını etkinleştirmeyi ve sonunda bir JPG dosyasından metni çıkarmayı adım adım göstereceğiz. Sonunda jpg dosyalarından metin nasıl çıkarılır, GPU cihaz kimliği nasıl ayarlanır ve her adımın önemi ne olduğu konusunda tam bilgi sahibi olacaksınız.

## Gerekenler

- **Java Development Kit (JDK) 11+** – kod standart Java dil özelliklerini kullanır.
- **Aspose OCR for Java** kütüphanesi (2026 itibarıyla en son sürüm). Maven Central'dan alabilir ya da Aspose web sitesinden JAR dosyasını indirebilirsiniz.
- **CUDA‑destekli GPU** sürücü 11+ (isteğe bağlı ama hız için şiddetle tavsiye edilir).
- Örnek bir görüntü, örn. `sample.jpg`, kodunuzdan referans verebileceğiniz bir klasöre yerleştirilmiş.

Harici hizmetler, bulut anahtarları yok—sadece yerel bir Java projesi ve GPU‑hazır bir makine.

## Adım 1 – OCR için Görüntüyü Yükleme

Metni tanıyebilmeniz için OCR motoruna bir şeyler vermeniz gerekir. İşte **OCR için görüntü yükleme** adımının devreye girdiği yer.

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and load the image
        OcrEngine engine = new OcrEngine();

        // Load a JPG file – this is the “extract text from jpg” part
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

> **Neden önemli:** `ImageStream.fromFile` yöntemi birçok formatı (JPG, PNG, BMP) destekler. JPG kullanmak dosya boyutunu küçük tutar, bu da GPU’da yüzlerce görüntü işlediğinizde özellikle kullanışlıdır.

## Adım 2 – GPU Hızlandırmasını Etkinleştirme ve GPU Cihaz Kimliğini Ayarlama

Makinenizde CUDA‑uyumlu bir GPU varsa, Aspose OCR'ye yoğun işlemleri grafik kartında çalıştırmasını söyleyebilirsiniz. Bu, **GPU cihaz kimliğini ayarlama** adımıdır.

```java
        // Step 2: Enable GPU acceleration (requires CUDA 11+ and a compatible driver)
        engine.getProcessingSettings().setUseGpu(true);

        // Optional: Choose a specific GPU device (0 = first GPU)
        engine.getProcessingSettings().setGpuDeviceId(0);
```

> **Pro ipucu:** Birden fazla GPU'nuz varsa, farklı `gpuDeviceId` değerleriyle deney yaparak hangisinin en iyi verimi verdiğini görebilirsiniz. Varsayılan (`0`) genellikle birincil GPU'yu işaret eder.

## Adım 3 – OCR İşlemini Çalıştırma

Görüntü yüklendi ve motor GPU çalışması için hazır olduğuna göre, karakterleri gerçekten tanıma zamanı geldi.

```java
        // Step 3: Run the OCR process
        OcrResult result = engine.recognize();
```

> **Arka planda ne oluyor?** OCR motoru görüntüyü metin satırlarına ayırır, her segmentte bir sinir ağı çalıştırır ve sonuçları birleştirir. `setUseGpu(true)` aktif olduğunda, bu sinir ağı CPU yerine GPU’da çalışır ve gecikmeyi büyük ölçüde azaltır.

## Adım 4 – Tanınan Metni Çıkarma ve Görüntüleme

Bulmacanın son parçası **jpg dosyasından metin çıkarmak** ve bunu kullanıcıya göstermek. `OcrResult` nesnesi düz metni, güven skorlarını ve gerekirse daha sonra kullanabileceğiniz sınırlama kutularını içerir.

```java
        // Step 4: Display the recognized text
        System.out.println("Recognized text:");
        System.out.println(result.getText());

        // Optional: Print confidence (helps with quality checks)
        System.out.println("Overall confidence: " + result.getConfidence());
    }
}
```

### Beklenen Çıktı

`sample.jpg` dosyası “Hello World” cümlesini içeriyorsa, konsol şu çıktıyı vermelidir:

```
Recognized text:
Hello World
Overall confidence: 0.98
```

Güven değeri 0 ile 1 arasında değişir; 0.8’in üzerindeki değerler genellikle temiz taramalar için güvenilirdir.

## Adım 5 – Yaygın Varyasyonlar ve Kenar Durumları

### PNG veya BMP Dosyalarıyla Çalışma

Kaynak görüntünüz JPG değilse, sadece dosya uzantısını değiştirin:

```java
engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.png"));
```

İş akışının geri kalanı aynı kalır—**görüntüden metin nasıl çıkarılır** dosya formatına bağlı değildir, Aspose desteklediği sürece.

### Düşük Çözünürlüklü Görüntülerle Baş Etme

Düşük çözünürlüklü resimler genellikle daha düşük güven skorları üretir. Sonuçları şu yollarla iyileştirebilirsiniz:

1. Görüntüyü Aspose'a göndermeden önce OpenCV gibi bir kütüphane ile ölçeklendirmek.
2. `engine.getProcessingSettings().setResolution(300);` ayarını değiştirerek dahili işleme için daha yüksek DPI zorlamak.

### Yalnızca CPU’da Çalıştırma

CUDA‑uyumlu bir GPU’nuz yoksa, GPU satırlarını atlayın:

```java
engine.getProcessingSettings().setUseGpu(false);
```

OCR CPU’ya geri dönecek, bu daha yavaş ama hâlâ tamamen işlevsel.

## Üretim İçin Pratik İpuçları

- **Toplu İşleme:** OCR mantığını bir döngü içinde sarın ve aynı `OcrEngine` örneğini yeniden kullanın. Bu, yerel kütüphanelerin tekrar tekrar yüklenmesinden kaynaklanan ek yükü azaltır.
- **Hata Yönetimi:** Bozuk dosyaları nazikçe ele almak için her zaman `IOException` ve `OcrException` yakalayın.
- **Bellek Yönetimi:** İşlemden sonra `engine.dispose();` çağırarak yerel GPU belleğini serbest bırakın, özellikle binlerce görüntü işliyorsanız.

```java
        // Clean up resources
        engine.dispose();
```

- **Günlükleme:** `result.getConfidence()` değerini çıkarılan metinle birlikte saklayın. Düşük güvenli girdiler manuel inceleme kuyruğuna gönderilebilir.

## Tam Çalışan Örnek

Aşağıda IDE'nize kopyalayıp yapıştırabileceğiniz tam, bağımsız program yer alıyor. `YOUR_DIRECTORY` ifadesini görüntü klasörünüzün yolu ile değiştirin.

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Create the OCR engine
        OcrEngine engine = new OcrEngine();

        // Load a JPG image – this is how you extract text from jpg
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));

        // Enable GPU acceleration (requires CUDA 11+ and a compatible driver)
        engine.getProcessingSettings().setUseGpu(true);

        // Optional: Select a specific GPU device (0 = first GPU)
        engine.getProcessingSettings().setGpuDeviceId(0);

        // Run the OCR process
        OcrResult result = engine.recognize();

        // Show the recognized text
        System.out.println("Recognized text:");
        System.out.println(result.getText());

        // Show confidence for quality checks
        System.out.println("Overall confidence: " + result.getConfidence());

        // Release native resources
        engine.dispose();
    }
}
```

> **Sonuç doğrulama:** Yazdırılan metni orijinal görüntüyle karşılaştırın. Güven düşükse, “Yaygın Varyasyonlar ve Kenar Durumları” bölümündeki ipuçlarını değerlendirin.

## Sonuç

Aspose OCR kullanarak Java’da **görüntüden metin tanıma** için dosyayı yüklemekten GPU hızlandırmasını etkinleştirmeye ve sonunda metni çıkarmaya kadar ihtiyacınız olan her şeyi ele aldık. Bu adımları izleyerek **jpg dosyalarından metin çıkarabilir**, **GPU cihaz kimliğini ayarlama** ile hangi GPU’nun işi yapacağını kontrol edebilir ve akışı diğer görüntü formatları için bile uyarlayabilirsiniz.

Bir sonraki meydan okumaya hazır mısınız? Bu OCR hattını bir veritabanı eklemesiyle zincirleyin ya da sonuçları otomatik sınıflandırma için bir doğal dil işleme modeline besleyin. Olanaklar sınırsızdır ve temel desen—**OCR için görüntü yükle → GPU'yu etkinleştir → tanı → çıkar**—aynı kalır.

Herhangi bir sorunla karşılaşırsanız, CUDA sürücü sürümünüzü iki kez kontrol edin, Aspose OCR JAR dosyasının JDK’nizle uyumlu olduğundan emin olun ve her toplu işlemden sonra motoru serbest bırakmayı unutmayın. İyi kodlamalar, OCR’nuz her zaman doğru olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}