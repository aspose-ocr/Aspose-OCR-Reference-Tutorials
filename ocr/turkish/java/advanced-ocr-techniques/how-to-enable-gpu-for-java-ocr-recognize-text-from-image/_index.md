---
category: general
date: 2026-10-19
description: Aspose OCR kullanarak, Java OCR'de GPU'yu nasıl etkinleştirip görüntüden
  metin tanıyacağınızı ve faturadan hızlıca metin çıkaracağınızı öğrenin.
draft: false
keywords:
- recognize text from image
- load image for ocr
- java ocr example aspose
- enable gpu java ocr
- aspose ocr performance
lastmod: 2026-10-19
og_description: Aspose kullanarak Java OCR'de GPU hızlandırmasıyla görüntüden metin
  tanımayı öğrenin. Bu kılavuz, tam bir java ocr example, performans ipuçları ve sorun
  giderme yöntemlerini gösterir.
og_image_alt: Diagram of GPU‑accelerated OCR pipeline for Java showing image loading,
  GPU processing, and text extraction
og_title: GPU hızlandırmalı Java OCR ile görüntüden metin tanıma – Hızlı Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-10-19'
  description: Learn how to enable GPU in Java OCR to recognize text from image and
    extract text from invoice fast using Aspose OCR.
  headline: How to Enable GPU for Java OCR – Recognize Text from Image
  type: TechArticle
- questions:
  - answer: Yes, Aspose OCR runs in a headless environment as long as the GPU drivers
      are installed.
    question: Does this work on headless servers?
  - answer: Convert each PDF page to an image (e.g., using Aspose.PDF) and feed the
      images to the OCR engine.
    question: Can I process PDFs directly?
  - answer: The engine will automatically fall back to `CPU_ONLY` mode; you can also
      force CPU mode to avoid unexpected errors.
    question: What if my GPU is older and not supported?
  - answer: Load each page as a separate `OcrInput` instance, run `recognize` on each,
      and concatenate the results.
    question: How do I handle multi‑page invoices?
  - answer: There is no hard limit, but processing extremely large batches may require
      streaming to keep memory usage low.
    question: Is there a limit on the number of pages I can process in one run?
  type: FAQPage
tags:
- Java
- OCR
- GPU
- Aspose
- image processing
title: Java OCR için GPU'yu Nasıl Etkinleştirirsiniz – Görüntüden Metin Tanıma
url: /tr/java/advanced-ocr-techniques/how-to-enable-gpu-for-java-ocr-recognize-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java OCR için GPU'yu nasıl etkinleştirirsiniz – görüntüden metin tanıma

Java'da OCR yaparken **GPU'yu nasıl etkinleştirileceğini** hiç merak ettiniz mi? Yalnız değilsiniz—birçok geliştirici, faturalar gibi büyük, yüksek çözünürlüklü belgeleri işlerken performans sınırına takılıyor. İyi haber? Aspose OCR ile tek bir anahtarı çevirerek grafik kartının ağır işi yapmasını sağlayabilirsiniz. Bu öğreticide, bir **java ocr örneği** üzerinden bir görüntüyü yükleyen, GPU işlemeyi etkinleştiren ve bir faturadan metni anında çıkaran bir örnek üzerinden ilerleyeceğiz.

Kitaplığı kurmaktan eksik GPU sürücüleri gibi uç durumları ele almaya kadar her şeyi kapsayacağız. Sonunda **görüntüden metin tanıma** dosyalarını anında yapabilecek ve gelecekteki OCR projeleri için sağlam bir şablona sahip olacaksınız. Harici referans gerekmez—sadece saf, çalıştırılabilir kod.

## Hızlı cevaplar
- **Bu sadece CPU'lu bir makinede çalıştırabilir miyim?** Evet, işleme modunu `CPU_ONLY` olarak ayarlayın ve kod GPU olmadan çalışır.  
- **Hangi GPU markaları destekleniyor?** NVIDIA, AMD ve Intel GPU'ları, sürücü güncel olduğu sürece desteklenir.  
- **GPU modu ne kadar daha hızlı?** Tipik bir 300 dpi fatura üzerinde, GPU işlem süresini ~4 saniyeden <1 saniyeye düşürebilir.  
- **Aspose OCR için lisans gerekiyor mu?** Geliştirme için ücretsiz deneme çalışır; üretim için ticari lisans gerekir.  
- **Görüntü ön işleme gerekli mi?** Yalnızca çok düşük kontrastlı veya gürültülü görüntüler için; aksi takdirde motor çoğu durumu otomatik olarak işler.

## Görüntüden metin tanıma nedir?
**Görüntüden metin tanıma**, bir bitmap (PNG, JPEG vb.) içindeki görsel karakterleri optik karakter tanıma (OCR) kullanarak düzenlenebilir, aranabilir Unicode metnine dönüştürmek anlamına gelir.  

Aspose OCR motoru piksel desenlerini analiz eder, bunları dil modelleriyle eşleştirir ve güven puanlarıyla birlikte düz metin dizeleri döndürür. Bu yetenek, faturalar, makbuzlar ve taranmış formların dijitalleştirilmesi için esastır.

## Java'da GPU hızlandırmalı OCR neden kullanılmalı?
GPU kullanmak, hesaplama açısından yoğun konvolüsyon işlemlerini özel donanıma devreder. Aspose OCR, orta sınıf bir RTX 3060'da ** saniyede 50+ sayfa** işleyebilir, yüksek sınıf bir CPU'da ise saniyede 12 sayfa. Bu hız artışı, toplu işlem hatlarındaki gecikmeyi azaltır ve satış noktası terminalleri gibi gerçek zamanlı tarama senaryolarını mümkün kılar.

## Önkoşullar

- **Java Development Kit (JDK) 11** veya daha yeni bir sürüm makinenizde kurulu olmalı.  
- **Maven** (veya Gradle) bağımlılık yönetimi için.  
- Güncel sürücülere (NVIDIA, AMD veya Intel) sahip **GPU destekli bir sistem**.  
- Bir fatura görüntü dosyası (ör. `large_invoice_300dpi.png`).  

Eğer bunlardan herhangi biri eksikse, önce temin edin; rehberin geri kalanı bunların mevcut olduğunu varsayar.

## Adım 1: Projenize Aspose OCR ekleyin

İlk olarak Aspose OCR kütüphanesine ihtiyacımız var. Maven ile, aşağıdaki kod parçacığını `pom.xml` dosyanıza ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Use the latest version available -->
</dependency>
```

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Use the latest version available -->
</dependency>
```

> **Pro ipucu:** Sürüm numarası düzenli olarak değişir; güncel kalmak için Maven Central'da en yeni sürümü kontrol edin.

Gradle tercih ediyorsanız, eşdeğeri şudur:

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

Bağımlılık çözüldükten sonra, OCR motoru ile iletişim kuracak kodu yazmaya hazırsınız.

## Aspose OCR'de GPU nasıl etkinleştirilir?

`OcrEngine`, OCR işleme ve yapılandırmayı kontrol eden ana sınıftır. OCR motorunu yükleyin, işleme modunu `AUTO_GPU` olarak ayarlayın ve isteğe bağlı olarak belirli bir GPU cihazı seçin. Motor, mevcut GPU'ları otomatik olarak algılar ve kaynakları buna göre tahsis eder. Bu tek yapılandırma, kütüphaneye GPU'yu tercih etmesini, ancak uyumlu bir cihaz bulunamazsa CPU'ya geri dönmesini söyler.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2.1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2.2: Enable GPU processing (AUTO_GPU uses GPU when available)
        ocrEngine.setProcessingMode(OcrEngine.ProcessingMode.AUTO_GPU);

        // The rest of the steps follow...
    }
}
```

> **Neden önemli:** GPU'yu etkinleştirmek, donanımınıza bağlı olarak 300 dpi bir faturanın işlem süresini birkaç saniyeden bir saniyenin altına düşürebilir.

## OCR için görüntü nasıl yüklenir – görüntüden metin tanıma

`OcrInput`, OCR motoru için giriş kaynağını temsil eder; dosyaları, akışları ve görüntüleri destekler. Motorun bir şey okuyabilmesi için ona bir görüntü sağlamalısınız. Aspose OCR'in `OcrInput` sınıfı dosya yollarını, akışları veya hatta `BufferedImage` nesnelerini kabul eder. Basitlik açısından bir dosya yolu kullanacağız. Bu yöntem, çoğu yaygın görüntü formatı için çalışır ve verimli bellek kullanımı sağlar.

```java
// Step 3.1: Prepare the input image
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/large_invoice_300dpi.png"); // <-- replace with your actual path
```

> **Uç durum:** Görüntü 5 MB'den büyükse, GPU'da bellek dışı hataları önlemek için önce çözünürlüğünü düşürmeyi düşünün.

## OCR nasıl yapılır ve faturadan metin nasıl çıkarılır

`recognize`, verilen girdi üzerinde OCR analizini çalıştırır ve bir `OcrResult` döndürür. `recognize` yöntemi, çıkarılan metin, güven puanları ve düzen bilgilerini içeren bir `OcrResult` nesnesi döndürür. `OcrResult` çıkarılan metni, güven puanlarını ve düzen bilgilerini tutar. Ardından, ihtiyacınıza göre düz metni veya yapılandırılmış veriyi almak için sonuç üzerinde döngü kurabilirsiniz.

```java
// Step 4.1: Run the recognition
OcrResult ocrResult = ocrEngine.recognize(ocrInput);

// Step 4.2: Print the extracted text to console
System.out.println("=== Extracted Text ===");
System.out.println(ocrResult.getText());
```

Programı çalıştırdığınızda, aşağıdakine benzer bir şey görmelisiniz:

```
=== Extracted Text ===
Invoice #12345
Date: 2026-02-20
Total: $1,245.67
...
```

Çıktı bozuk görünüyorsa, görüntünün net olduğundan ve OCR dilinin doğru ayarlandığından (Aspose varsayılan olarak İngilizce'dir, ancak `ocrEngine.setLanguage(OcrEngine.Language.SPANISH)` gibi değiştirilebilir) iki kez kontrol edin.

## Tam çalışan örnek (kopyala-yapıştır hazır)

Aşağıda eksiksiz, bağımsız bir Java sınıfı bulunmaktadır. IDE'nize yapıştırın, görüntü yolunu ayarlayın ve **Run** tuşuna basın.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU (auto‑detect)
        ocrEngine.setProcessingMode(OcrEngine.ProcessingMode.AUTO_GPU);

        // 3️⃣ Load the image you want to process
        OcrInput ocrInput = new OcrInput();
        // 👉 Replace with the absolute or relative path to your invoice image
        ocrInput.add("YOUR_DIRECTORY/large_invoice_300dpi.png");

        // 4️⃣ Run OCR
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // 5️⃣ Output the text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

### Beklenen çıktı

Temiz bir 300 dpi fatura üzerinde kodu çalıştırmak, genellikle belgedeki her satırın düz metin temsilini verir. Tam çıktı fatura düzenine bağlıdır, ancak *Invoice Number*, *Date*, *Total Amount* ve satır öğesi açıklamaları gibi alanları göreceksiniz.

## Yaygın tuzaklar ve nasıl düzeltileceği

| Semptom | Muhtemel neden | Çözüm |
|---------|----------------|-------|
| **`java.lang.UnsatisfiedLinkError`** | GPU sürücüsü eksik veya uyumsuz | NVIDIA/AMD/Intel'den en son sürücüyü yükleyin. |
| **Çok yavaş işleme** | GPU sessizce CPU'ya geri dönüyor | `ocrEngine.getProcessingMode()`'un `AUTO_GPU` döndürdüğünü ve `SystemInfo.isGpuAvailable()`'ın true olduğunu doğrulayın. |
| **Boş çıktı** | Görüntü çok karanlık veya düşük kontrastlı | OCR'ye vermeden önce görüntüyü ön işleme tabi tutun (kontrastı artırın, ikilileştirin). |
| **Bellek dışı** | Çok büyük görüntü (>10 MP) | Görüntüyü yeniden boyutlandırın veya parçalara bölün; her parçayı ayrı ayrı işleyin. |

## Adım adım özet (hızlı referans)

| Adım | Yaptığınız şey |
|------|----------------|
| 1 | Aspose OCR bağımlılığı eklendi |
| 2 | `OcrEngine` oluşturuldu ve `AUTO_GPU` ayarlandı |
| 3 | `OcrInput` ile bir fatura görüntüsü yüklendi |
| 4 | `recognize` çağrıldı ve `ocrResult.getText()` yazdırıldı |
| 5 | Yaygın hatalar ele alındı ve çıktı doğrulandı |

## İleriye doğru – sonraki adımlar

- **Toplu işleme:** Faturaların bir klasöründe döngü yapın ve her sonucu bir veritabanına kaydedin.  
- **Dil desteği:** Çok dilli faturalar için `ocrEngine.setLanguage(OcrEngine.Language.FRENCH)`'a geçin.  
- **Son işlem:** Düz metinden *Invoice Number* veya *Total Amount* gibi alanları çıkarmak için düzenli ifadeler kullanın.  
- **GPU ayarı:** Birden fazla GPU'nuz varsa, en hızlısını seçmek için `ocrEngine.setGpuDeviceId(int id)`'yi keşfedin.

## Sonuç

**Java OCR için GPU'yu nasıl etkinleştireceğinizi** gösterdik, temiz bir **java ocr örneği** sunduk ve **OCR için görüntü yükleme**'den **faturadan metin çıkarma**'ya kadar tüm akışı adım adım anlattık. Aspose'un `AUTO_GPU` modunu kullanarak uyumluluğu kaybetmeden bir performans artışı elde edersiniz—geliştirme makineleri ve üretim sunucuları için mükemmeldir.

Deneyin, görüntü ön işleme ayarlarını değiştirin ve toplu işler ile deney yapın. GPU hızlandırması ile sağlam bir OCR kütüphanesini birleştirdiğinizde sınır yoktur.

![GPU hızlandırmalı OCR boru hattını gösteren diyagram – Java OCR için GPU nasıl etkinleştirilir](https://example.com/images/gpu-ocr-pipeline.png "Java OCR için GPU nasıl etkinleştirilir")

[GPU hızlandırmalı OCR boru hattını gösteren diyagram – Java OCR için GPU nasıl etkinleştirilir](https://example.com/images/gpu-ocr-pipeline.png "Java OCR için GPU nasıl etkinleştirilir")

## Sıkça Sorulan Sorular

**Q: Bu, başsız sunucularda çalışır mı?**  
**A: Evet, GPU sürücüleri yüklü olduğu sürece Aspose OCR başsız bir ortamda çalışır.**

**Q: PDF'leri doğrudan işleyebilir miyim?**  
**A: Her PDF sayfasını bir görüntüye dönüştürün (ör. Aspose.PDF kullanarak) ve görüntüleri OCR motoruna besleyin.**

**Q: GPU'm eski ve desteklenmiyorsa ne olur?**  
**A: Motor otomatik olarak `CPU_ONLY` moduna geri dönecektir; beklenmeyen hatalardan kaçınmak için CPU modunu zorlayabilirsiniz.**

**Q: Çok sayfalı faturaları nasıl ele alırım?**  
**A: Her sayfayı ayrı bir `OcrInput` örneği olarak yükleyin, her birinde `recognize` çalıştırın ve sonuçları birleştirin.**

**Q: Tek bir çalıştırmada işleyebileceğim sayfa sayısında bir limit var mı?**  
**A: Katı bir limit yoktur, ancak çok büyük toplu işlemler bellek kullanımını düşük tutmak için akış gerektirebilir.**

**Son Güncelleme:** 2026-10-19  
**Test Edilen:** Aspose.OCR 24.11 for Java  
**Yazar:** Aspose

## İlgili Öğreticiler

- [Görüntüden Metin Çıkarma Java Tam OCR Rehberi](/ocr/java/advanced-ocr-techniques/extract-text-from-image-java-complete-ocr-guide/)
- [Aspose OCR Java Hızlı Kılavuzu ile Görüntüden Metin Çıkarma](/ocr/java/ocr-basics/extract-text-from-image-with-aspose-ocr-java-quick-guide/)
- [Aspose.OCR for Java kullanarak URL'den görüntüden metin çıkarma](/ocr/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}