---
category: general
date: 2026-10-30
description: Java'da Aspose OCR GPU desteğiyle görüntüden metni hızlı bir şekilde
  çıkarmayı öğrenin. Bu rehber, GPU device ID'yi ayarlamayı ve yüksek performanslı
  OCR elde etmeyi gösterir.
draft: false
keywords:
- extract text from image
- how to extract text
- aspose ocr gpu
- recognize text image java
- gpu acceleration OCR
lastmod: 2026-10-30
og_description: Java'da Aspose OCR GPU desteğiyle görüntüden metni hızlı bir şekilde
  çıkarmayı öğrenin. Bu rehber, optimal performans için GPU device ID'yi ayarlamayı
  gösterir.
og_image_alt: 'Developer guide: extract text from image using Aspose OCR GPU in Java'
og_title: Java'da Aspose OCR GPU ile görüntüden metin çıkarma
schemas:
- author: Aspose
  dateModified: '2026-10-30'
  description: Learn how to extract text from image quickly with Aspose OCR GPU support
    in Java. This guide shows how to set GPU device ID and achieve high‑performance
    OCR.
  headline: How to extract text from image with Aspose OCR GPU in Java
  type: TechArticle
- questions:
  - answer: Yes—just install a valid Aspose OCR license. The free trial is for evaluation
      only.
    question: Can I use this in a commercial application?
  - answer: Absolutely; as long as the NVIDIA driver and CUDA toolkit are installed,
      the library runs on headless Linux environments.
    question: Does the GPU version work on Linux servers?
  - answer: Aspose OCR can process images up to **5000 × 5000 px** without loading
      the whole file into memory.
    question: What is the maximum image size supported?
  - answer: Replace the old JAR with the new one and update your Maven/Gradle dependency
      version number.
    question: How do I upgrade to the latest Aspose OCR version?
  - answer: Yes—`OcrResult` provides layout information, including word‑level bounding
      boxes, when you enable the `setIncludeLayout(true)` option.
    question: Is there a way to get bounding‑box coordinates for each word?
  type: FAQPage
tags:
- Java
- OCR
- Aspose
- GPU
title: Java'da Aspose OCR GPU ile görüntüden metin çıkarma
url: /tr/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR GPU ile Java'da Görüntüden Metin Çıkarma

Java uygulamasında **görüntüden metin çıkarma** işlemini denediyseniz ve CPU'nun yüksek çözünürlüklü taramalarda zorlandığını gördüyseniz, yalnız değilsiniz. Birçok geliştirici büyük belgeleri işlerken performans darboğazlarıyla karşılaşıyor. Aspose OCR for Java, OCR'yi GPU'da çalıştırmanıza olanak tanıyarak bu engeli ortadan kaldırır ve işleme süresini büyük ölçüde azaltır. Bu öğreticide, lisansı nasıl ayarlayacağınızı, GPU hızlandırmayı nasıl etkinleştireceğinizi ve birden fazla grafik kartı bulunduğunda **gpu cihaz kimliğini ayarlamayı** gösteren tam, çalıştırmaya hazır bir örnek göreceksiniz.

## Hızlı cevaplar
- **Java'da görüntüden metin çıkarmanın en hızlı yolu nedir?** Aspose OCR'yi GPU hızlandırmasıyla kullanın ve uygun GPU cihaz kimliğini ayarlayın.  
- **Hangi Java sürümü gereklidir?** En iyi performans için Java 17 veya daha yenisi önerilir.  
- **GPU desteği için lisansa ihtiyacım var mı?** Evet—GPU özellikleri yalnızca geçerli bir Aspose OCR lisansı ile açılır.  
- **Bunu başsız bir sunucuda çalıştırabilir miyim?** Kesinlikle; yalnızca GPU sürücüsü ve CUDA araç seti gereklidir.  
- **Kaç dil destekleniyor?** İngilizce, Çince, Arapça ve Hintçe dahil olmak üzere 30'dan fazla dil.

## Görüntüden metin çıkarma nedir?
Görüntüden metin çıkarma, PNG, JPG veya TIFF gibi bitmap formatlarında depolanan karakterlerin görsel temsilini düzenlenebilir, aranabilir Unicode metnine dönüştürmek anlamına gelir. Optik Karakter Tanıma (OCR) olarak bilinen bu süreç, indeksleme, çeviri ve veri çıkarma gibi sonraki görevleri mümkün kılar.

## Neden Aspose OCR GPU'yi kullanmalısınız?
Aspose OCR, GPU hızlandırmasını kullanarak büyük, yüksek çözünürlüklü görüntüleri CPU‑only işleme göre çok daha verimli bir şekilde işler. 30'dan fazla giriş formatını destekler ve bellek kullanımını düşük tutarak 5000 × 5000 px'e kadar görüntüleri işleyebilir; modern NVIDIA GPU'larda tanıma süresini beş katına kadar hızlandırır.

## İhtiyacınız olanlar
- **Java 17** veya daha yenisi (Java 8+ ile uyumlu, ancak LTS sürümleri daha iyi JIT performansı sağlar).  
- **Aspose OCR for Java** kütüphanesi (JAR'ı Aspose web sitesinden indirin).  
- Geçerli bir **Aspose OCR lisans dosyası** (`Aspose.OCR.lic`). Ücretsiz deneme çalışır, ancak GPU özellikleri lisanslı bir sürüm gerektirir.  
- Açık, makine tarafından okunabilir metin içeren bir görüntü dosyası (`sample-image.png`).  
- Uygun sürücü yüklü CUDA uyumlu bir NVIDIA GPU (veya eşdeğeri).

Eğer bunlardan herhangi biri size yabancı geliyorsa, endişelenmeyin—her maddeyi ilerledikçe açıklayacağız.

## Adım 1: Aspose OCR'yi projenize ekleyin
İlk olarak, Aspose OCR JAR'ını sınıf yolunuza ekleyin. Maven kullanıyorsanız, `pom.xml` dosyasına aşağıdaki bağımlılığı ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

Gradle için ise şu şekilde ekleyin:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

Manuel yöntemi tercih ediyorsanız, JAR'ı bir `libs/` klasörüne koyup IDE'nizin modül yoluna ekleyin.

> **Pro tip:** Sürüm numarasını sürüm notlarıyla uyumlu tutun; yeni sürümler genellikle GPU işleme için performans iyileştirmeleri içerir.

## Adım 2: Aspose OCR lisansını yükleyin (GPU kullanımı için gerekli)
Lisans olmadan `setEnableGpu(true)` çağrısı sessizce CPU moduna geri döner. Lisansı `main` metodunun başında yükleyin:

```java
import com.aspose.ocr.License;

// ...

License ocrLicense = new License();
ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

`YOUR_DIRECTORY` ifadesini `.lic` dosyasını sakladığınız mutlak ya da göreli yol ile değiştirin. Yanlış bir yol `FileNotFoundException` hatasına neden olur, bu yüzden yazımını iki kez kontrol edin.

## Adım 3: OCR motorunu oluşturun ve GPU hızlandırmayı etkinleştirin
`OcrEngine` sınıfı, görüntüler üzerinde OCR işlemlerini gerçekleştiren çekirdek bileşendir.

```java
import com.aspose.ocr.OcrEngine;

// ...

OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getDevice().setEnableGpu(true);       // activate GPU support
ocrEngine.getDevice().setGpuDeviceId(0);        // optional: choose GPU index (0 = first card)
```

Cihaz kimliğiyle neden uğraşıyorsunuz? Çoklu‑GPU ortamında bir kartı ön işleme, diğerini OCR için ayırabilirsiniz. Kimliği ayarlamak, yoğun işlemlerin istenen donanımda çalışmasını sağlar.

## Adım 4: Giriş görüntüsünü hazırlayın
`OcrInput` sınıfı, işlemek istediğiniz görüntü koleksiyonunu temsil eder.

```java
import com.aspose.ocr.OcrInput;

// ...

OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/sample-image.png"); // path to the image you want to process
```

Bir akışı (ör. yüklenen bir dosya) işlemek istiyorsanız, bunun yerine `ocrInput.add(InputStream)` kullanın.

## Adım 5: Tanıma sürecini çalıştırın ve sonucu alın
`OcrResult` sınıfı, motor tarafından döndürülen düz metin, güven skorları ve isteğe bağlı düzen bilgilerini kapsar.

```java
import com.aspose.ocr.OcrResult;

// ...

OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("Recognized text:\n" + ocrResult.getText());
```

Konsol aşağıdaki gibi bir çıktı verir:

```
Recognized text:
Hello, world!
This is a sample image.
```

Görüntü bulanıktaysa veya dil desteklenmiyorsa sonuç boş olabilir. Bu durumda, `ocrResult.getConfidence()` değerini (0‑100) inceleyerek ön işleme ile yeniden denemeniz gerekip gerekmediğine karar verin.

## Tam, çalıştırılabilir örnek
Tüm parçaları bir araya getirerek IDE'nize kopyalayıp yapıştırabileceğiniz tek bir Java sınıfı elde edersiniz:

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license – required for GPU usage
        License ocrLicense = new License();
        ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");

        // 2️⃣ Create OCR engine and turn on GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getDevice().setEnableGpu(true);      // enable GPU acceleration
        ocrEngine.getDevice().setGpuDeviceId(0);       // optional: select GPU index

        // 3️⃣ Load the image you want to process
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/sample-image.png");

        // 4️⃣ Perform recognition
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // 5️⃣ Output the recognized text
        System.out.println("Recognized text:\n" + ocrResult.getText());
    }
}
```

> **Beklenen çıktı:** Konsol, `sample-image.png` içinde görünen tam metni yazdırır. GPU aktif olduğunda, tipik bir 300 dpi tarama için işleme süresi birkaç saniyeden (CPU) bir saniyenin altına düşer.

## Sık sorulan sorular ve uç durumlar

### Bu başsız bir sunucuda çalışır mı?
Evet. GPU sürücüsü kurulmuş olmalı, ancak bir ekran gerekmiyor. `CUDA` araç setinin (veya GPU'nuz için eşdeğerinin) sistem `PATH`'inde olduğundan emin olun. Bu yapılandırma, OCR'yi grafik arayüzü olmayan bulut ya da konteyner ortamlarında çalıştırmanıza olanak tanır.

### Birden fazla GPU'm var ve GPU 1'i kullanmak istiyorum, ne yapmalıyım?
Aşağıdaki gibi cihaz kimliğini değiştirin:

```java
ocrEngine.getDevice().setGpuDeviceId(1); // selects the second GPU (zero‑based index)
```

Kimliği `1` olarak ayarlamak, OCR motorunun sistemdeki ikinci GPU'yu kullanmasını sağlar; bu, ilk GPU başka işler için ayrılmışsa faydalıdır.

### Farklı bir dilde görüntüden metin nasıl çıkarılır?
`recognize` metodunu çağırmadan önce dili ayarlayın:

```java
ocrEngine.setLanguage(OcrLanguage.FRENCH);
```

Aspose OCR, **30'dan fazla dili** destekler; Arapça ve İbranice gibi sağ‑dan‑sol scriptleri de içerir. Doğru dili seçmek doğruluğu büyük ölçüde artırır.

### Görüntü birden fazla sayfa içeriyorsa (ör. PDF görüntülere dönüştürüldüyse) ne olur?
Her sayfa için ayrı bir `OcrInput` girdisi oluşturun veya dosyalar üzerinde döngü yapın:

```java
for (String path : imagePaths) {
    ocrInput.add(path);
}
```

Motor, sonuçları sırasıyla birleştirir ve sayfa dizilimini nihai çıktıda korur.

### Düşük güvenilirlik sonuçları nasıl ele alınır?
Güven skorunu kontrol edin:

```java
if (ocrResult.getConfidence() < 70) {
    System.out.println("Low confidence – consider preprocessing the image.");
}
```

Tipik ön işleme adımları arasında ikilileştirme, gürültü azaltma veya 300 dpi'ye yeniden boyutlandırma bulunur. Bu tür ön işleme sonrası OCR'yi yeniden çalıştırmak genellikle güven seviyesini yükseltir.

## Performans ipuçları
- **Batch processing:** Birçok görüntüyü tek bir `OcrInput` içine eklemek, GPU bağlamının tekrar tekrar başlatılmasından kaynaklanan ek yükü azaltır.  
- **Warm‑up:** JVM başlatıldıktan sonra bir deneme tanıma çalıştırın; ilk çağrı sürücü başlatma gecikmesini içerir.  
- **Memory management:** İşiniz bittiğinde büyük `OcrInput` nesnelerini (`ocrInput.clear()`) serbest bırakarak GPU belleğini temizleyin.  

## Sonuç
Artık Aspose OCR'nin GPU motorunu kullanarak Java'da **görüntüden metin çıkarma** işlemini verimli bir şekilde nasıl yapacağınızı, birden fazla grafik kartı ile çalışırken **gpu cihaz kimliğini ayarlamayı** ve çok dilli senaryoları nasıl yöneteceğinizi biliyorsunuz. Yukarıdaki tam, çalıştırılabilir kod kutusunu doğrudan kullanabilirsiniz—sadece lisans ve görüntü yollarını kendi ortamınıza göre değiştirin.

Bir sonraki adıma hazır mısınız? Taranmış PDF'lerin bulunduğu bir klasörü işleyin, farklı `setLanguage` seçenekleriyle deneyler yapın veya OCR çıktısını bir makine‑öğrenme modeliyle birleştirerek sonrası işleme uygulayın. GPU hızlandırması sayesinde büyük ölçekli projeler artık mümkün.

İyi kodlamalar, ve bir sorunla karşılaşırsanız yorum bırakmaktan çekinmeyin!

## Sıkça Sorulan Sorular

**S: Bu uygulamayı ticari bir projede kullanabilir miyim?**  
C: Evet—geçerli bir Aspose OCR lisansı kurmanız yeterli. Ücretsiz deneme sadece değerlendirme amaçlıdır.

**S: GPU sürümü Linux sunucularda çalışır mı?**  
C: Kesinlikle; NVIDIA sürücüsü ve CUDA araç seti kurulu olduğu sürece kütüphane başsız Linux ortamlarında da çalışır.

**S: Desteklenen maksimum görüntü boyutu nedir?**  
C: Aspose OCR, **5000 × 5000 px**'e kadar görüntüyü, dosyanın tamamını belleğe yüklemeden işleyebilir.

**S: En son Aspose OCR sürümüne nasıl yükseltirim?**  
C: Eski JAR'ı yeniyle değiştirin ve Maven/Gradle bağımlılık sürüm numarasını güncelleyin.

**S: Her kelime için sınırlayıcı kutu (bounding‑box) koordinatlarını alabilir miyim?**  
C: Evet—`OcrResult`, `setIncludeLayout(true)` seçeneği etkinleştirildiğinde kelime‑seviye sınırlayıcı kutular dahil düzen bilgilerini sağlar.

---

**Son Güncelleme:** 2026-10-30  
**Test Edilen Versiyon:** Aspose OCR for Java 24.11  
**Yazar:** Aspose

## İlgili Öğreticiler

- [GPU Hızlandırmalı Java OCR ile Görüntüden Metin Tanıma](/ocr/java/advanced-ocr-techniques/recognize-text-from-image-java-ocr-with-gpu-acceleration/)
- [Java'da OCR için GPU'yu Etkinleştirme ve Görüntüden Metin Çıkarma](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)
- [Aspose OCR Java ile Görüntüden Metin Çıkarma Hızlı Kılavuz](/ocr/java/ocr-basics/extract-text-from-image-with-aspose-ocr-java-quick-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}