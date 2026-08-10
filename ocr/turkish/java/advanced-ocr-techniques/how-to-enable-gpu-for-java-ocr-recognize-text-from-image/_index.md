---
category: general
date: 2026-02-22
description: Java OCR'de GPU'yu nasıl etkinleştireceğinizi öğrenin ve Aspose OCR kullanarak
  görüntüden metin tanıma ile faturadan metni hızlıca çıkarın.
draft: false
keywords:
- how to enable gpu
- recognize text from image
- extract text from invoice
- java ocr example
- load image for ocr
language: tr
og_description: Java OCR'de GPU'yu nasıl etkinleştirir, görüntüden metni tanır ve
  fatura üzerindeki metni tam bir Java OCR örneğiyle nasıl çıkarırız.
og_title: Java OCR için GPU'yu Etkinleştirme – Hızlı Rehber
tags:
- Java
- OCR
- GPU
- Aspose
title: Java OCR için GPU'yu Nasıl Etkinleştirirsiniz – Görüntüden Metin Tanıma
url: /tr/java/advanced-ocr-techniques/how-to-enable-gpu-for-java-ocr-recognize-text-from-image/
---

accelerated OCR pipeline – how to enable GPU for Java OCR". Must translate alt text but keep URL unchanged. Title also translate.

- The final shortcodes remain.

We must ensure not to translate URLs, file paths, code block placeholders.

Also keep markdown formatting.

Let's produce translation.

Be careful with Turkish characters.

Let's start.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java OCR için GPU'yu Nasıl Etkinleştirirsiniz – Görüntüden Metin Tanıma

Java'da OCR yaparken **GPU'yu nasıl etkinleştirirsiniz** diye hiç merak ettiniz mi? Tek başınıza değilsiniz—birçok geliştirici, faturalar gibi büyük ve yüksek çözünürlüklü belgeleri işlerken performans sınırına takılıyor. İyi haber? Aspose OCR ile tek bir anahtarı çevirerek grafik kartının ağır işi üstlenmesini sağlayabilirsiniz. Bu öğreticide, bir **java ocr example** üzerinden bir görüntüyü yükleyip GPU işleme etkinleştirerek faturadan metni anında çıkaracağız.

Kütüphanenin kurulumu, eksik GPU sürücüleri gibi kenar durumlarının ele alınması gibi her şeyi kapsayacağız. Sonunda **görüntüden metin tanıma** dosyalarını anında tanıyabilecek ve gelecekteki OCR projeleriniz için sağlam bir şablona sahip olacaksınız. Harici referanslara gerek yok—sadece çalıştırılabilir kod.

## Önkoşullar

- **Java Development Kit (JDK) 11** veya daha yeni bir sürüm makinenizde kurulu.  
- **Maven** (veya Gradle) bağımlılık yönetimi için.  
- **GPU‑destekli bir sistem** ve güncel sürücüler (NVIDIA, AMD veya Intel).  
- Bir fatura görüntüsü dosyası (ör. `large_invoice_300dpi.png`).  

Eğer bunlardan birine sahip değilseniz önce temin edin; rehberin geri kalanı bu koşulların mevcut olduğunu varsayar.

## Adım 1: Aspose OCR'ı Projeye Ekleyin

İlk olarak Aspose OCR kütüphanesine ihtiyacımız var. Maven kullanıyorsanız, aşağıdaki kodu `pom.xml` dosyanıza ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Use the latest version available -->
</dependency>
```

> **İpucu:** Sürüm numarası düzenli olarak değişir; en yeni sürümü almak için Maven Central'i kontrol edin.

Gradle tercih ediyorsanız eşdeğeri şu şekildedir:

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

Bağımlılık çözüldükten sonra OCR motoruyla iletişim kuracak koda hazırsınız.

## Adım 2: Aspose OCR Motorunda GPU'yu Nasıl Etkinleştirirsiniz

Şimdi gösterinin yıldızı—GPU işleme açma zamanı. Aspose OCR üç işleme modu sunar:

| Mod | Açıklama |
|------|-------------|
| `CPU_ONLY` | Sadece CPU, her makinede güvenli. |
| `GPU_ONLY` | GPU'yu zorlar, uyumlu cihaz yoksa hata verir. |
| `AUTO_GPU` | GPU var mı kontrol eder ve mevcutsa kullanır, aksi takdirde CPU'ya döner. |

Çoğu senaryo için **`AUTO_GPU`** önerilir; çünkü iki dünyanın en iyisini sunar. İşte etkinleştirme şekli:

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

> **Neden önemli:** GPU'yu etkinleştirmek, 300 dpi bir faturanın işleme süresini donanımınıza bağlı olarak birkaç saniyeden bir saniyenin altına indirebilir.

## Adım 3: OCR İçin Görüntüyü Yükleyin – Görüntüden Metin Tanıma

Motorun bir şey okuyabilmesi için ona bir görüntü sağlamalısınız. Aspose OCR’ın `OcrInput` sınıfı dosya yollarını, akışları veya hatta `BufferedImage` nesnelerini kabul eder. Basitlik açısından dosya yolunu kullanacağız:

```java
// Step 3.1: Prepare the input image
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/large_invoice_300dpi.png"); // <-- replace with your actual path
```

> **Kenar durumu:** Görüntü 5 MB'den büyükse, GPU’da bellek hatalarıyla karşılaşmamak için önce ölçeklendirmeyi düşünün.

## Adım 4: OCR'ı Gerçekleştirin ve Faturadan Metni Çıkarın

Şimdi motorun sihrini çalıştıralım. `recognize` metodu, çıkarılan metin, güven skorları ve düzen bilgilerini içeren bir `OcrResult` nesnesi döndürür.

```java
// Step 4.1: Run the recognition
OcrResult ocrResult = ocrEngine.recognize(ocrInput);

// Step 4.2: Print the extracted text to console
System.out.println("=== Extracted Text ===");
System.out.println(ocrResult.getText());
```

Programı çalıştırdığınızda aşağıdakine benzer bir çıktı görmelisiniz:

```
=== Extracted Text ===
Invoice #12345
Date: 2026-02-20
Total: $1,245.67
...
```

Çıktı bozuk görünüyorsa, görüntünün net olduğundan ve OCR dilinin doğru ayarlandığından emin olun (Aspose varsayılan olarak İngilizce kullanır, ancak `ocrEngine.setLanguage(OcrEngine.Language.SPANISH)` gibi değiştirilebilir).

## Adım 5: Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda eksiksiz, bağımsız bir Java sınıfı bulunuyor. IDE’nize yapıştırın, görüntü yolunu ayarlayın ve **Run** tuşuna basın.

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

### Beklenen Çıktı

Temiz bir 300 dpi faturada kodu çalıştırmak genellikle belgenin her satırının düz metin temsilini üretir. Tam çıktı fatura düzenine bağlıdır, ancak *Invoice Number*, *Date*, *Total Amount* ve satır‑item açıklamaları gibi alanları göreceksiniz.

## Yaygın Tuzaklar & Çözüm Yolları

| Belirti | Muhtemel Neden | Çözüm |
|---------|----------------|-------|
| **`java.lang.UnsatisfiedLinkError`** | GPU sürücüsü eksik veya uyumsuz | NVIDIA/AMD/Intel'ten en yeni sürücüyü kurun. |
| **Çok yavaş işleme** | GPU sessizce CPU'ya geri dönüyor | `ocrEngine.getProcessingMode()`'un `AUTO_GPU` döndürdüğünden ve `SystemInfo.isGpuAvailable()`'ın true olduğundan emin olun. |
| **Boş çıktı** | Görüntü çok karanlık veya düşük kontrastlı | OCR'a vermeden önce görüntüyü ön‑işleyin (kontrast artırın, ikilileştirin). |
| **Bellek dışı hata** | Çok büyük görüntü (>10 MP) | Görüntüyü yeniden boyutlandırın veya parçalara bölün; her parçayı ayrı ayrı işleyin. |

## Adım‑Adım Özet (Hızlı Başvuru)

| Adım | Ne Yaptınız |
|------|--------------|
| 1 | Aspose OCR bağımlılığını eklediniz |
| 2 | `OcrEngine` oluşturup `AUTO_GPU` ayarladınız |
| 3 | `OcrInput` ile bir fatura görüntüsü yüklediniz |
| 4 | `recognize` çağırıp `ocrResult.getText()`'i yazdırdınız |
| 5 | Yaygın hataları ele aldınız ve çıktıyı doğruladınız |

## Daha İleri – Sonraki Adımlar

- **Toplu işleme:** Bir klasördeki tüm faturaları döngüye alıp her sonucu bir veritabanına kaydedin.  
- **Dil desteği:** Çok dilli faturalar için `ocrEngine.setLanguage(OcrEngine.Language.FRENCH)` gibi ayarlar yapın.  
- **Son‑işleme:** Düz metinden *Invoice Number* veya *Total Amount* gibi alanları çıkarmak için düzenli ifadeler kullanın.  
- **GPU ayarı:** Birden fazla GPU'nuz varsa, en hızlısını seçmek için `ocrEngine.setGpuDeviceId(int id)`'yi keşfedin.

## Sonuç

**GPU'yu nasıl etkinleştirirsiniz** gösterdik, temiz bir **java ocr example** sunduk ve **görüntüden metin tanıma** ile **faturadan metin çıkarma** sürecinin tamamını adım adım anlattık. Aspose’un `AUTO_GPU` modunu kullanarak performans artışı elde ederken uyumluluktan ödün vermiyorsunuz—geliştirme makineleri ve üretim sunucuları için mükemmel.

Deneyin, görüntü ön‑işlemesini ayarlayın ve toplu işler deneyin. GPU hızlandırması ile sağlam bir OCR kütüphanesini birleştirdiğinizde sınır yoktur.

---

![GPU‑hızlandırmalı OCR boru hattını gösteren diyagram – Java OCR için GPU nasıl etkinleştirilir](https://example.com/images/gpu-ocr-pipeline.png "Java OCR için GPU nasıl etkinleştirilir")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}