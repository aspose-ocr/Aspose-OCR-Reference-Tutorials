---
category: general
date: 2026-09-23
description: Aspose OCR for Java'da GPU hızlandırmasını etkinleştirerek tiff dosyasından
  metni hızlıca nasıl çıkaracağınızı öğrenin. Adım adım kılavuz, TIFF yüklemeyi, GPU
  cihaz kimliğini ayarlamayı ve metni okumayı kapsar.
draft: false
keywords:
- extract text from tiff file
- gpu acceleration java
- ocr tiff java
- aspose ocr gpu
lastmod: 2026-09-23
og_description: Aspose OCR for Java'da GPU hızlandırmasını etkinleştirerek tiff dosyasından
  metni hızlıca nasıl çıkaracağınızı öğrenin. Kılavuz, TIFF yüklemeyi, bir GPU cihazı
  seçmeyi ve çıkarılan metni okumayı gösterir.
og_image_alt: 'Tutorial image: enabling GPU for OCR in Java'
og_title: GPU hızlandırmasıyla OCR Java'da tiff dosyasından metin çıkarma
schemas:
- author: Aspose
  dateModified: '2026-09-23'
  description: Learn how to extract text from tiff file quickly by enabling GPU acceleration
    in Aspose OCR for Java. Step‑by‑step guide covers loading TIFF, setting GPU device
    ID, and reading text.
  headline: How to extract text from tiff file using GPU in OCR Java
  type: TechArticle
- questions:
  - answer: Absolutely—Aspose OCR runs on Windows, Linux, and macOS as long as the
      CUDA toolkit and drivers are installed.
    question: Does this work on Linux?
  - answer: Omit the `setUseGpu(true)` call or explicitly call `setUseGpu(false)`;
      the engine will run on CPU.
    question: What if I don’t have a GPU?
  - answer: Yes. `setImage` accepts JPEG, PNG, BMP, PDF, and more.
    question: Can I extract text from other formats?
  - answer: Accuracy drops sharply below 300 dpi. Pre‑process the image (binarization,
      deskew) for better results.
    question: How accurate is OCR on low‑resolution TIFFs?
  - answer: The library handles 30+ raster and document formats, including TIFF, JPEG,
      PNG, BMP, PDF, and GIF.
    question: How many formats does Aspose OCR support?
  type: FAQPage
tags:
- OCR
- Java
- GPU acceleration
title: GPU kullanarak OCR Java'da tiff dosyasından metin çıkarma
url: /tr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-and-extract-text-from-tiff/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# GPU kullanarak OCR Java'da tiff dosyasından metin çıkarma

tiff dosyasından **metin çıkarmak** istiyorsanız, Aspose OCR for Java'da GPU hızlandırmasını etkinleştirmek en hızlı yoldur. İlk 100 kelimede GPU'nun neden önemli olduğunu açıklayacağız, ardından bir TIFF dosyasını yükleme, GPU'yu etkinleştirme, isteğe bağlı olarak belirli bir cihaz seçme, OCR çalıştırma ve sonunda çıkarılan metni okuma adımlarını göstereceğiz. Sonunda sadece birkaç satır kodla TIFF'i metne dönüştürebileceksiniz.

## Hızlı cevaplar
- **GPU OCR'un temel faydası nedir?** Büyük çok sayfalı TIFF'ler için işlem süresi 5 kat daha hızlı.  
- **Hangi Java sürümü gereklidir?** Java 17 veya daha yeni (Java 8+ da çalışır).  
- **Özel bir lisansa ihtiyacım var mı?** Üretim kullanımı için geçerli bir Aspose OCR for Java lisansı gereklidir.  
- **Bunu Linux'ta çalıştırabilir miyim?** Evet—Aspose OCR çok platformlu; sadece CUDA araç setini kurmanız yeterlidir.  
- **GPU isteğe bağlı mı?** `setUseGpu(false)` çağırarak CPU'ya geri dönebilirsiniz.

## OcrEngine Nedir?
`OcrEngine` sınıfı Aspose OCR for Java'ın merkezi bileşenidir. Tüm OCR işlevselliğini kapsar, görüntüleri yüklemenize, dil ve GPU kullanımı gibi işleme seçeneklerini yapılandırmanıza ve tanınan metin ile güven skorlarını kullanışlı bir nesnede almanıza olanak tanır.

`OcrEngine`, OCR işleme motorunu temsil eden Aspose OCR'un çekirdek sınıfıdır ve görüntüleri yükleme, seçenekleri yapılandırma ve sonuçları alma yöntemlerini sağlar.

## Java'da OCR için GPU'yu nasıl etkinleştirirsiniz?
Görüntünüzü yükleyin, GPU'yu açın ve `recognize` çağırın—bu kadar yeter. `setUseGpu(true)` ile GPU'yu etkinleştirmek, motorun piksel yoğun işlerini grafik kartına devretmesini sağlar ve işlem süresini büyük ölçüde azaltır, özellikle yüksek çözünürlüklü veya çok sayfalı TIFF'ler için.

## Gereksinimler

- Java 17 veya daha yeni (kod Java 8+ üzerinde de çalışır).  
- Aspose OCR for Java 23.10 (veya en son sürüm).  
- En son sürücü yüklü CUDA uyumlu bir GPU.  
- Örnek çok sayfalı TIFF dosyası (örneğin `sample_large.tif`).  

Maven yok mu? JAR dosyasını sınıf yolunuza (classpath) bırakmanız yeterlidir.

![GPU'yu etkinleştirme öğreticisi](gpu-ocr.png)

[GPU'yu etkinleştirme öğreticisi](gpu-ocr.png)

*Görsel alt metni: Java'da OCR için GPU'yu etkinleştirme*

## Adım 1: OCR için TIFF görüntüsü yükleme

`setImage` yöntemi dosyayı bir `ImageStream` içinde sarar ve motorun çok sayfalı TIFF'leri manuel bölme yapmadan işlemesine olanak tanır. Dosya bulunamazsa, net bir `FileNotFoundException` fırlatılır.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the TIFF file – this is where we "read text from TIFF"
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample_large.tif"));
```

> **Neden önemli:** `setImage` çağrısı sayfa yönetimini soyutlar, böylece tek bir motor örneğiyle tüm belgeyi işleyebilirsiniz.

## Adım 2: GPU hızlandırmasını etkinleştirme

GPU'yu açmak tek bir boolean bayrağıdır. Çoğu sistemde varsayılan GPU cihaz 0'dır, ancak Aspose'un otomatik olarak en uygun cihazı seçmesine izin verebilirsiniz.

```java
        // Enable GPU acceleration (requires a supported driver)
        ocrEngine.getEngineOptions().setUseGpu(true);
```

> **Pro ipucu:** Birden fazla GPU'ya sahip iş istasyonlarında, cihaz kimliğini belirtmek, beklenmedik bir şekilde daha yavaş entegre GPU'ya geri dönmeyi önler.

## Adım 3: GPU cihaz kimliğini ayarla (isteğe bağlı)

OCR'ı hangi GPU'nun işleyeceğini biliyorsanız—belki özel bir AI kartı—`setGpuDeviceId` ile açıkça ayarlayabilirsiniz.  

```java
        // Optional: select the GPU device (0 = first device, 1 = second, etc.)
        ocrEngine.getEngineOptions().setGpuDeviceId(0);
```

> **Köşe durumu:** Geçersiz bir kimlik gönderildiğinde `IllegalArgumentException` fırlatılır. Geçerli kimlikleri listelemek için `ocrEngine.getEngineOptions().getAvailableGpuDevices()` kullanın.

## Adım 4: Görüntüyü işleyin ve görüntüden metin çıkarın

OCR çalıştırmak, düz metin ve isteğe bağlı güven skorlarını içeren bir `OcrResult` döndürür.  

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

TIFF “Hello, World!” içeriyorsa sonuç şu şekilde görünecektir:

```
Recognized text:
Hello, World!
```

Motor otomatik olarak satır sonlarını, noktalama işaretlerini ve temel düzen algılamasını yönetir. Sayfa başına çıkarım için `ocrResult.getPages()`'ı inceleyin.

## Adım 5: Çıktıyı doğrulama ve yaygın sorunları ele alma

GPU çeşitli nedenlerle atlanabilir. Yüklü sürücü sürümü minimum gereksinimin altında ise kütüphane CUDA'yı başlatamaz. Yetersiz video belleği motorun CPU'ya geri dönmesine neden olabilir ve bazı entegre grafikler OCR hızlandırması için gerekli hesaplama yeteneğine sahip değildir.

### GPU neden kullanılmayabilir?

- **Sürücü uyumsuzluğu:** GPU sürücüsü Aspose sürüm notlarında listelenen minimum sürümü karşılamalıdır.  
- **Yetersiz bellek:** Çok büyük görüntüler VRAM'i aşabilir; motor bu durumda CPU'ya geri döner ve bir uyarı kaydeder.  
- **Desteklenmeyen donanım:** Entegre grafikler genellikle gerekli hesaplama yeteneğine sahip değildir.

### Programlı olarak CPU'ya geri dönme

CPU işleme zorunluluğu varsa, motorun seçenek ayarlayıcısını false bayrağıyla çağırın. Bu, GPU denemelerini devre dışı bırakır ve OCR işlem hattını tamamen ana işlemci üzerinde çalıştırır; uyumlu grafik kartı olmayan makinelerde faydalıdır.

```java
if (!ocrEngine.getEngineOptions().isGpuAvailable()) {
    System.out.println("GPU not available – switching to CPU.");
    ocrEngine.getEngineOptions().setUseGpu(false);
}
```

### Döngü içinde TIFF'ten metin okuma

Birçok dosya işlenirken, GPU hızlandırmasını açık tutarak bir dizini yineleyin.

```java
File folder = new File("YOUR_DIRECTORY");
for (File file : folder.listFiles((dir, name) -> name.toLowerCase().endsWith(".tif"))) {
    ocrEngine.setImage(ImageStream.fromFile(file.getAbsolutePath()));
    OcrResult result = ocrEngine.process();
    System.out.println("File: " + file.getName());
    System.out.println(result.getText());
}
```

Bu kod parçacığı, **TIFF dosyalarından** toplu olarak metin okumanın performans artışını kaybetmeden nasıl yapılacağını gösterir.

## Sıkça Sorulan Sorular (SSS)

**S: Bu Linux'ta çalışır mı?**  
C: Kesinlikle—Aspose OCR, CUDA araç seti ve sürücüler yüklü olduğu sürece Windows, Linux ve macOS'ta çalışır.

**S: GPU'um yoksa ne olur?**  
C: `setUseGpu(true)` çağrısını atlayın veya açıkça `setUseGpu(false)` çağırın; motor CPU'da çalışacaktır.

**S: Başka formatlardan metin çıkarabilir miyim?**  
C: Evet. `setImage` JPEG, PNG, BMP, PDF ve daha fazlasını kabul eder.

**S: Düşük çözünürlüklü TIFF'lerde OCR ne kadar doğru?**  
C: Doğruluk 300 dpi altında keskin bir şekilde düşer. Daha iyi sonuçlar için görüntüyü ön işleme tabi tutun (ikiliye çevirme, eğikliği düzeltme).

**S: Aspose OCR kaç formatı destekliyor?**  
C: Kütüphane TIFF, JPEG, PNG, BMP, PDF ve GIF dahil olmak üzere 30'dan fazla raster ve belge formatını işler.

## Sonuç

Artık Aspose OCR for Java'da GPU hızlandırmasıyla **tiff dosyasından metin çıkarma**, belirli bir GPU cihaz kimliğini ayarlama ve tek ya da birden fazla TIFF'i verimli bir şekilde işleme konularını biliyorsunuz. Tek bir bayrağı değiştirerek OCR mantığını değiştirmeden büyük hız artışı elde edersiniz.

Denemek isteyebileceğiniz sonraki adımlar:

- Yüzlerce TIFF'i paralel iş parçacıklarında toplu işleme.  
- Özel dil paketleri yükleyerek uzmanlaşmış kelime dağarcıklarının tanınmasını iyileştirme.  
- Çıkarılan metni regex ile işleyerek biçimlendirmeyi temizleme.

Herhangi bir sorunla karşılaşırsanız, aşağıya yorum bırakın. Kodlamanın tadını çıkarın!

---

**Son Güncelleme:** 2026-09-23  
**Test Edilen:** Aspose OCR for Java 23.10  
**Yazar:** Aspose

## İlgili Öğreticiler

- [Java OCR için GPU'yu Etkinleştirme Adım Adım Kılavuzu](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-java-ocr-step-by-step-guide/)
- [Aspose OCR ile Görüntüden Metin Tanıma Tam Java Kılavuzu](/ocr/java/advanced-ocr-techniques/recognize-text-from-image-with-aspose-ocr-full-java-guide/)
- [Java'da Görüntü OCR Ön İşleme ile Doğruluğu Artırma ve Metin Çıkarma](/ocr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}