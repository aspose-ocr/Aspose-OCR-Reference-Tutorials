---
category: general
date: 2026-03-28
description: Aspose OCR kullanarak Java'da görüntü metnini tanımayı, metin PNG dosyalarını
  çıkarmayı ve büyük görüntülerde hızlı OCR için GPU hızlandırmasını nasıl kullanacağınızı
  öğrenin.
draft: false
keywords:
- recognize image text
- extract text png
- use gpu acceleration
- ocr large image
- java ocr example
language: tr
og_description: Java'da görüntü metnini nasıl tanıyacağınızı, metin içeren PNG dosyalarını
  nasıl çıkaracağınızı ve büyük görüntülerde OCR için GPU hızlandırmasını nasıl kullanacağınızı
  keşfedin.
og_title: Java OCR ile görüntü metnini tanıma – GPU Hızlandırmalı Örnek
tags:
- OCR
- Java
- GPU
title: Java OCR ile Görüntü Metnini Tanıma – GPU Hızlandırmalı Örnek
url: /tr/java/advanced-ocr-techniques/recognize-image-text-with-java-ocr-gpu-accelerated-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java OCR ile Görüntü Metni Tanıma – GPU‑Hızlandırmalı Örnek

Büyük bir PNG dosyasından **görüntü metni tanıma** ihtiyacı duyup CPU sürümünün çok yavaş çalıştığını gördünüz mü? Tek başınıza değilsiniz. Gerçek dünyadaki birçok işlem hattında—fatura tarama ya da tarihi belgelerin arşivlenmesi gibi—görüntü boyutu çok büyük olabilir ve varsayılan OCR motoru yeterli gelmez.  

İyi haber: Aspose OCR for Java, **GPU hızlandırması** kullanarak süreci turbo‑şarj etmenizi sağlar ve kod şaşırtıcı derecede kompakt. Bu öğreticide, **extract text PNG** dosyalarını işleyen, CUDA‑destekli bir GPU kullanan ve **OCR large image** işlemini sadece birkaç satır kodla gerçekleştiren tam, çalıştırılabilir bir Java OCR örneği göreceksiniz. Sonunda, bunu kendi Java projenize nasıl entegre edeceğinizi ve her ayarın neden önemli olduğunu tam olarak bileceksiniz.

## Öğrenecekleriniz

- Aspose OCR'ı bir Maven ya da Gradle projesine nasıl ekleyeceğinizi.  
- **Görüntü metni tanıma** işlemini GPU üzerinde adım adım nasıl yapacağınızı.  
- GPU akış sayısını yapılandırmanın verimliliği nasıl artırabileceğini.  
- Çıktıyı nasıl doğrulayacağınızı ve yaygın sorunları nasıl gidereceğinizi.  

> **Önkoşullar** – Java 17 (veya daha yeni), en son sürücüye sahip CUDA‑uyumlu bir GPU ve geçerli bir Aspose OCR for Java lisansı (değerlendirme için ücretsiz deneme sürümü yeterlidir). Başka harici kütüphane gerekmez.

---

## Adım 1: Aspose OCR Bağımlılığını Ekleyin

İlk olarak, Aspose OCR kütüphanesini projenize dahil edin. **Maven** kullanıyorsanız, aşağıdaki kodu `pom.xml` dosyanıza ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check Maven Central for the latest version -->
</dependency>
```

**Gradle** için ise bu satırları `build.gradle` dosyanıza yerleştirin:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **İpucu:** Mart 2026 itibarıyla en yeni sürüm, GPU iş yükleri için performans iyileştirmeleri içerir; bu yüzden her zaman en yeni sürümü çekin.

---

## Adım 2: OCR Motorunu Başlatın ve GPU'yu Etkinleştirin

Bir OCR motoru oluşturmak basittir. Kritik kısım GPU bayrağını açmaktır—aksi takdirde motor CPU moduna geri döner.

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU acceleration (requires a CUDA‑enabled GPU and driver)
        ocrEngine.getRecognitionSettings().setUseGpu(true);

        // 3️⃣ (Optional) Set the number of GPU streams for parallel processing
        //    More streams can improve throughput on multi‑core GPUs.
        ocrEngine.getRecognitionSettings().setGpuStreams(2);
```

### Neden GPU Etkinleştirilmeli?

`setUseGpu(true)` çağrısını yaptığınızda, Aspose ağır konvolüsyonel sinir ağı hesaplamalarını grafik kartına devreder. Bu, **ocr large image** işleme süresinden saniyeler kazandırabilir, özellikle görüntü 4000 × 4000 px'i aştığında. Ortamınızda uyumlu bir GPU yoksa, bu çağrı basitçe etkisiz kalır ve motor CPU’da çalışmaya devam eder—çökmez, sadece daha yavaş olur.

---

## Adım 3: PNG Görüntüsünü Tanıyın ve Metnini Çıkarın

Şimdi motoru işlemek istediğiniz dosyaya yönlendirin. Örnekte `sample-large.png` kullanılıyor, ancak istediğiniz herhangi bir PNG ya da JPEG dosyasını koyabilirsiniz.

```java
        // 4️⃣ Perform OCR on the input image
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/sample-large.png");

        // 5️⃣ Print the recognized text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Programı çalıştırdığınızda aşağıdakine benzer bir çıktı görmelisiniz:

```
=== Recognized Text ===
Invoice #12345
Date: 2026‑03‑27
Total: $1,234.56
...
```

Bu çıktı, **recognize image text** işleminin başarılı olduğunu ve **extract text png** içeriğini başarıyla elde ettiğinizi doğrular.

---

## Adım 4: GPU Kullanımını Doğrulayın (İsteğe Bağlı ama Faydalı)

GPU'nun gerçekten kullanılıp kullanılmadığını merak ediyorsanız, sisteminizin GPU izleme aracını (ör. Linux'ta `nvidia-smi`) açın. Java süreci çalışırken bellek kullanımı ve işlemci kullanımında hafif bir artış görmelisiniz.

```bash
$ nvidia-smi
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   PID   Type   Process name                  GPU Memory               |
|  0    12345 C++    java                           1024MiB                  |
+-----------------------------------------------------------------------------+
```

Eğer herhangi bir aktivite görmüyorsanız, şu noktaları kontrol edin:

1. CUDA sürücüsü GPU modeliyle eşleşiyor mu?  
2. `setUseGpu(true)` çağrısı kodun ilerleyen bölümlerinde üzerine yazılmadı mı?  
3. Lisans dosyanız (varsa) GPU kullanımını kısıtlamıyor mu?

---

## Adım 5: Yaygın Kenar Durumlarını Ele Alma

### GPU Belleğini Aşan Büyük Görüntüler

Bir görüntü çok büyük olduğunda (ör. 8000 × 8000 px), GPU belleği tükenebilir. Hızlı bir çözüm, görüntüyü Aspose'a göndermeden önce küçültmektir:

```java
import java.awt.image.BufferedImage;
import javax.imageio.ImageIO;
import java.io.File;

BufferedImage original = ImageIO.read(new File("sample-large.png"));
int maxDim = 4000; // target max dimension
int width = original.getWidth();
int height = original.getHeight();

float scale = Math.min((float)maxDim / width, (float)maxDim / height);
int newWidth = Math.round(width * scale);
int newHeight = Math.round(height * scale);

BufferedImage resized = new BufferedImage(newWidth, newHeight, original.getType());
// Simple scaling (for demo purposes)
resized.getGraphics().drawImage(original, 0, 0, newWidth, newHeight, null);
ImageIO.write(resized, "png", new File("sample-resized.png"));
```

Ardından `recognizeImage` metoduna `"sample-resized.png"` gönderin. Bu, OCR doğruluğunu korurken GPU sınırları içinde kalmanızı sağlar.

### Çok Sayfalı PDF'ler

Aspose OCR, PDF'leri sayfa sayfa da işleyebilir. Her sayfayı bir görüntüye dönüştürüp motora besleyin. Aynı **use gpu acceleration** bayrağı geçerlidir ve PDF‑to‑text hattınızı hızlandırır.

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda, derlenip çalıştırılmaya hazır tam Java sınıfı yer alıyor. `YOUR_DIRECTORY` kısmını PNG dosyanızın yolu ile değiştirin.

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable GPU acceleration (requires a CUDA‑enabled GPU and driver)
        ocrEngine.getRecognitionSettings().setUseGpu(true);

        // Step 3: (Optional) Set the number of GPU streams for parallel processing
        // Using 2 streams works well on most modern GPUs.
        ocrEngine.getRecognitionSettings().setGpuStreams(2);

        // Step 4: Perform OCR on the input image
        // This will **recognize image text** from a PNG file.
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/sample-large.png");

        // Step 5: Print the recognized text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**Beklenen çıktı** – motorun görüntüden okuyabildiği her şeyi düz metin olarak verir. Görüntü bir tablo içeriyorsa, hücre içerikleri satır sonlarıyla birleştirilir; Aspose düzeni korumaz, ancak isterseniz dize sonrası işleme yapabilirsiniz.

---

## Sıkça Sorulan Sorular

| Soru | Cevap |
|------|-------|
| **Ücretli bir lisansa ihtiyacım var mı?** | Deneme sürümü 200 sayfaya kadar çalışır ve OCR için filigranı kaldırır. Üretim ortamında lisans, sınırlamaları kaldırır ve tam GPU yığınına erişim sağlar. |
| **GPU'm eski bir model (ör. GTX 750) ise?** | Eski GPU'lar hâlâ çalışabilir ancak daha düşük hızda; en az Compute Capability 3.0 olduğundan emin olun. |
| **JPG veya BMP dosyalarını işleyebilir miyim?** | Kesinlikle—`recognizeImage` Java ImageIO tarafından desteklenen tüm formatları kabul eder. |
| **Birden çok resmi toplu işleme yapabilir miyim?** | OCR çağrısını bir döngü içinde sarın ve aynı anda çalıştırmak istediğiniz akış sayısına göre `setGpuStreams` değerini artırın. |
| **Düzeni korumam gerekiyor, ne yapmalıyım?** | Aspose OCR’ın `LayoutOptions` sınıfı ile sınırlama kutularını alabilirsiniz; bu konu bu hızlı kılavuzun kapsamı dışında ancak API belgelerinde detaylıdır. |

---

## Sonuç

Artık **java ocr example** olarak **recognize image text**, **extract text png** ve **use GPU acceleration** özelliklerini içeren kısa, uçtan uca bir örneğe sahipsiniz. GPU akış sayısını ayarlayarak ve gerekirse aşırı büyük görüntüleri küçülterek, çözümü neredeyse her donanım konfigürasyonuna uyarlayabilirsiniz.

Bir sonraki adıma hazır mısınız? Aynı hattı taranmış makbuzların bulunduğu bir klasöre uygulayın ya da Aspose’un `TextRegion` API’siyle orijinal düzeni korumayı deneyin. Herhangi bir sorunla karşılaşırsanız, Aspose forumları ve Javadoc mükemmel kaynaklardır—burada ele aldığımız temelleri aklınızda tutun.

İyi kodlamalar, OCR’unuz yıldırım hızıyla çalışsın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}