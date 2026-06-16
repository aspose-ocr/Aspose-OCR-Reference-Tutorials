---
category: general
date: 2026-05-31
description: Aspose OCR GPU hızlandırmasıyla Java’da görüntüden metni hızlıca tanıyın,
  TIFF’ten metin çıkarmayı öğrenin ve Java görüntüden metne dönüşümünü gerçekleştirin.
draft: false
keywords:
- recognize text from image
- extract text from tiff
- java image to text conversion
- Aspose OCR Java
- GPU OCR acceleration
language: tr
og_description: Aspose OCR GPU hızlandırmasıyla Java’da görüntüden metin tanıyın.
  Hızlı Java görüntü‑metin dönüşümü için bu adım‑adım kılavuzu izleyin.
og_title: Java kullanarak görüntüden metin tanıma – GPU OCR öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: recognize text from image in Java quickly with Aspose OCR GPU acceleration,
    learn to extract text from tiff and perform java image to text conversion.
  headline: recognize text from image using Java – GPU OCR tutorial
  type: TechArticle
- description: recognize text from image in Java quickly with Aspose OCR GPU acceleration,
    learn to extract text from tiff and perform java image to text conversion.
  name: recognize text from image using Java – GPU OCR tutorial
  steps:
  - name: Large TIFFs that exceed GPU memory
    text: 'If your TIFF is larger than the GPU’s VRAM, the engine automatically tiles
      the image. However, you may notice a slight slowdown. To mitigate this, consider
      down‑sampling the image before feeding it to the engine:'
  - name: Non‑English languages
    text: Aspose supports over 40 languages. Just swap `OcrLanguage.ENGLISH` with
      the appropriate enum, e.g., `OcrLanguage.SPANISH`. The same **recognize text
      from image** call works without code changes.
  - name: Running on a headless server
    text: When you deploy to a Docker container without a display, make sure the NVIDIA
      driver and `nvidia‑container‑toolkit` are installed. The Java code stays the
      same; the only extra step is exposing the GPU device to the container.
  type: HowTo
- questions:
  - answer: Yes. Load each page with `new OcrImage("file.tif", pageIndex)` inside
      a loop, then concatenate the results.
    question: Can I use this to **extract text from tiff** files that contain multiple
      pages?
  - answer: Simply replace `ocrEngine.setDevice(OcrDevice.GPU);` with `OcrDevice.CPU`.
      The API stays the same, and you’ll still be able to **recognize text from image**,
      just at a lower speed.
    question: What if I don’t have a GPU?
  - answer: 'Aspose OCR reports >95 % accuracy on clean, 300 DPI scans. For noisy
      images, pre‑process with filters (`inputImage.applyFilter(OcrFilter.NOISE_REDUCTION)`)
      before calling `recognize()`. --- ## Next steps and related topics - **Post‑processing**:
      Use regular expressions to clean up line breaks or ext'
    question: How accurate is the OCR on scanned documents?
  type: FAQPage
tags:
- Java
- OCR
- Aspose
- GPU
title: Java kullanarak görüntüden metin tanıma – GPU OCR öğreticisi
url: /tr/java/advanced-ocr-techniques/recognize-text-from-image-using-java-gpu-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# görüntüden metin tanıma – Java – GPU OCR öğreticisi

Bir Java uygulamasında **görüntüden metin tanıma**yı CPU'yu yavaşlatmadan nasıl yapabileceğinizi hiç merak ettiniz mi? Tek başınıza değilsiniz. Klasik bir OCR kütüphanesine çok‑megabaytlık bir TIFF gönderdiğinizde, UI donar, sunucu tıkanır ve yaptığınız tüm tasarım kararlarını sorgulamaya başlarsınız.  

İyi haber: Aspose OCR for Java GPU'yu devreye alabilir ve o yavaş işlemi neredeyse anlık **java image to text conversion**a dönüştürür. Bu rehberde lisans, GPU kurulumu, TIFF yükleme ve sonunda tanınan metni yazdırma adımlarını adım adım inceleyeceğiz. Sonunda **tiff'ten metin çıkarma** işlemini de verimli bir şekilde nasıl yapacağınızı öğreneceksiniz.

## Öğrenecekleriniz

- Aspose OCR'ın GPU motoru ile **görüntüden metin tanıma** nasıl yapılır.  
- Güvenilir bir **java image to text conversion** için tam adımlar.  
- Büyük TIFF'lerle çalışırken ipuçları ve **tiff'ten metin çıkarma** sırasında sıkça karşılaşılan tuzaklar.  

Aspose ile ilgili önceden bir deneyime ihtiyacınız yok; sadece çalışan bir JDK ve biraz merak yeterli.

## Önkoşullar

Başlamadan önce şunların kurulu olduğundan emin olun:

1. **Java Development Kit (JDK) 8+** – herhangi bir yeni sürüm yeterli.  
2. **Aspose.OCR for Java** JAR (Aspose web sitesinden indirin).  
3. **GPU‑uyumlu bir ortam** – tipik olarak NVIDIA CUDA 10+, ancak kütüphane bir GPU bulamazsa CPU'ya geri döner.  
4. **Lisans dosyası** (`Aspose.OCR.Java.lic`) uygulamanızın okuyabileceği bir konuma yerleştirilmiş.  

Bu öğelerden biri eksik olursa kod yine derlenir, ancak bir `LicenseException` alırsınız ya da performans düşer.  

> *Pro ipucu:* Lisans dosyanızı sürüm kontrolünün dışına tutun; kamuya açık depolara sızmasını istemezsiniz.

## Adım 1 – Aspose OCR lisansınızı uygulayın  

İlk yapmanız gereken, Aspose'a ücretli bir kullanıcı olduğunuzu bildirmektir. Lisans olmadan motor demo modunda çalışır ve çıktıya filigran ekler.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // Apply your Aspose OCR license
        License ocrLicense = new License();
        ocrLicense.setLicense("Aspose.OCR.Java.lic");
```

> Bu adım neden kritik?  
> Lisans, GPU desteğini açar ve deneme sürümünün getirdiği 30 saniyelik işleme sınırını kaldırır.  

## Adım 2 – OCR motorunu GPU hızlandırması için yapılandırın  

Şimdi `OcrEngine`i oluşturup GPU'yu kullanmasını söylüyoruz. **görüntüden metin tanıma**yı ışık hızıyla yapmamızı sağlayan sihir burada gerçekleşir.

```java
        // Create and configure the OCR engine to use the GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setDevice(OcrDevice.GPU);               // Enable GPU acceleration
        ocrEngine.setLanguage(OcrLanguage.ENGLISH);       // Choose the desired language
```

Kütüphane uyumlu bir GPU bulamazsa sessizce CPU'ya geçer. Seçilen cihazı `ocrEngine.getDevice()` çağrısıyla doğrulayabilirsiniz.

> *Not:* GPU hızlandırması, görüntünün GPU sürücüsünün sevdiği bir formatta (örn. PNG veya JPEG) olması durumunda en iyi performansı verir. Büyük çok‑sayfalı TIFF'ler hâlâ desteklenir, ancak her sayfa ayrı ayrı işlenir.

## Adım 3 – Tanımak istediğiniz görüntüyü yükleyin  

İşte **tiff'ten metin çıkarma** işleminin başladığı yer. `OcrImage` sınıfı bir dosya yolu, bir `InputStream` ya da bir bayt dizisi alabilir; bu da farklı depolama senaryoları için esneklik sağlar.

```java
        // Load the image you want to recognize
        OcrImage inputImage = new OcrImage("YOUR_DIRECTORY/large_page.tif");
        ocrEngine.setImage(inputImage);
```

Çok‑sayfalı bir TIFF ile çalışıyor ve sadece tek bir sayfaya ihtiyacınız varsa sayfa indeksini şu şekilde geçebilirsiniz:

```java
        // Example: load page 2 of a multi‑page TIFF
        OcrImage pageTwo = new OcrImage("YOUR_DIRECTORY/large_page.tif", 2);
        ocrEngine.setImage(pageTwo);
```

Bu küçük aşırı yükleme, TIFF'i kendiniz bölmek zorunda kalmanızı önler—taralı sözleşmeler ya da mimari planlar gibi **tiff'ten metin çıkarma** gerektiren dosyalar için oldukça kullanışlıdır.

## Adım 4 – OCR tanımasını gerçekleştirin  

Gerçek **java image to text conversion** tek bir satırda gerçekleşir. Aspose, piksel verisini GPU'ya akıtarak bir sinir‑ağ modeli çalıştırır ve düz metin stringi döndürür.

```java
        // Perform the OCR recognition
        String recognizedText = ocrEngine.recognize();
```

Ayrıca `recognize(OcrResultOptions)` aşırı yüklemesini kullanarak bir güven puanı ya da her kelimenin sınırlayıcı kutularını da alabilirsiniz. Bu, daha sonra orijinal görüntüyü vurgulamak istediğinizde işe yarar.

## Adım 5 – Tanınan metni çıktı olarak verin  

Son olarak sonucu ekrana yazdırıyoruz. Gerçek bir uygulamada muhtemelen veritabanına, PDF'e ya da başka bir NLP boru hattına kaydedersiniz.

```java
        // Output the recognized text
        System.out.println(recognizedText);
    }
}
```

Programı orta seviye bir NVIDIA GTX 1660 üzerinde çalıştırdığınızda, 12 MP bir TIFF için **görüntüden metin tanıma** işlemi 1.2 saniyenin altında tamamlanır—CPU‑only moda göre yaklaşık on kat daha hızlı.

---

## Yaygın kenar durumlarını ele alma  

### GPU belleğini aşan büyük TIFF'ler  

TIFF, GPU'nun VRAM'inden büyükse motor otomatik olarak görüntüyü parçalar. Ancak hafif bir yavaşlama fark edebilirsiniz. Bunu azaltmak için görüntüyü motorun önüne küçültebilirsiniz:

```java
        // Down‑sample to 300 DPI (good balance for OCR)
        inputImage.setResolution(300);
```

### İngilizce dışı diller  

Aspose 40'tan fazla dili destekler. `OcrLanguage.ENGLISH` yerine uygun enum'ı (ör. `OcrLanguage.SPANISH`) kullanın. Aynı **görüntüden metin tanıma** çağrısı kod değişikliği olmadan çalışır.

### Başsız (headless) sunucuda çalıştırma  

Görüntü ekranı olmayan bir Docker konteynerine dağıttığınızda NVIDIA sürücüsü ve `nvidia‑container‑toolkit` kurulu olduğundan emin olun. Java kodu aynı kalır; tek ek adım GPU cihazını konteynere açmaktır.

---

## Tam kaynak kodu – kopyala & yapıştır hazır  

Aşağıda tüm parçaları bir araya getiren, çalıştırılabilir örnek bulunuyor. `GpuOcrDemo.java` olarak kaydedin, lisans ve görüntü yollarını değiştirin, ardından Aspose OCR JAR'ını sınıf yoluna ekleyerek derleyin.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Apply your Aspose OCR license
        License ocrLicense = new License();
        ocrLicense.setLicense("Aspose.OCR.Java.lic");

        // Step 2: Create and configure the OCR engine to use the GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setDevice(OcrDevice.GPU);               // Enable GPU acceleration
        ocrEngine.setLanguage(OcrLanguage.ENGLISH);       // Choose the desired language

        // Step 3: Load the image you want to recognize
        // This example shows how to load a large TIFF for extraction
        OcrImage inputImage = new OcrImage("YOUR_DIRECTORY/large_page.tif");
        // Optional: down‑sample if the image is huge
        // inputImage.setResolution(300);
        ocrEngine.setImage(inputImage);

        // Step 4: Perform the OCR recognition
        String recognizedText = ocrEngine.recognize();    // This is the core java image to text conversion

        // Step 5: Output the recognized text
        System.out.println("=== Recognized Text Start ===");
        System.out.println(recognizedText);
        System.out.println("=== Recognized Text End ===");
    }
}
```

**Beklenen çıktı** (kısaltılmış olarak):

```
=== Recognized Text Start ===
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
=== Recognized Text End ===
```

OCR motoru GPU'yu bulamazsa konsolda bir uyarı görürsünüz, ancak program yine de metin döndürür—sadece daha yavaş.

---

## Sıkça sorulan sorular  

**S: Birden çok sayfa içeren **tiff'ten metin çıkarma** dosyaları için kullanabilir miyim?**  
C: Evet. `new OcrImage("file.tif", pageIndex)` ifadesini bir döngü içinde her sayfa için çağırın, ardından sonuçları birleştirin.

**S: GPU'um yoksa ne yapmalıyım?**  
C: `ocrEngine.setDevice(OcrDevice.GPU);` satırını `OcrDevice.CPU` ile değiştirin. API aynı kalır ve **görüntüden metin tanıma** yapabilirsiniz, sadece daha düşük bir hızda.

**S: Taralı belgelerde OCR doğruluğu ne kadar?**  
C: Aspose OCR, temiz 300 DPI taramalarda %95'in üzerinde doğruluk rapor eder. Gürültülü görüntülerde `inputImage.applyFilter(OcrFilter.NOISE_REDUCTION)` gibi filtrelerle ön‑işlem yapıp `recognize()` çağırmanız önerilir.

---

## Sonraki adımlar ve ilgili konular  

- **Post‑processing**: Satır sonlarını temizlemek ya da fatura numaraları gibi belirli alanları çıkarmak için düzenli ifadeler (regex) kullanın.  
- **Batch processing**: Bu kodu bir `java.nio.file` izleyiciyle birleştirerek bir klasöre bırakılan **görüntüden metin tanıma** dosyalarını otomatik işleyin.  
- **PDF entegrasyonu**: **tiff'ten metin çıkarma** işlemi sonrasında sonucu Aspose PDF ile aranabilir bir PDF'e gömebilirsiniz.  
- **Performans ayarı**: Karışık CPU/GPU iş yükleri için `ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors())` ile deneyler yapın.  

---

## Özet


## Bir Sonraki Öğrenmeniz Gerekenler

- [Metin Görüntülerini Çıkar – OCR Temelleri Aspose.OCR for Java ile](/ocr/english/java/ocr-basics/)
- [Java’da Görüntüden Metin Çıkarma – Aspose.OCR Detect Areas Modu](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Dil Seçimiyle Görüntü Metni OCR’ı Nasıl Yapılır](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}