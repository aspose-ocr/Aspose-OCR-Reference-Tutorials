---
category: general
date: 2026-02-19
description: Java OCR kullanarak görüntüden metin çıkarın. OCR için bir görüntü yükleyen
  ve sadece birkaç adımda fatura dosyalarından metin çıkaran bir Java OCR örneğini
  öğrenin.
draft: false
keywords:
- extract text from image
- java ocr example
- load image for ocr
- extract text from invoice
language: tr
og_description: Java OCR kullanarak görüntüden metin çıkarın. Bu kılavuz, OCR için
  görüntünün nasıl yükleneceğini ve basit bir Java OCR örneğiyle faturalardan metnin
  nasıl alınacağını gösterir.
og_title: Java’da Görüntüden Metin Çıkarma – Tam OCR Örneği
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Java'da Görüntüden Metin Çıkarma – Tam OCR Örneği
url: /tr/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-example/
---

yi farklı alanlar (tarih, satıcı adı) için değiştirin, çok dilli faturalar için dil paketleriyle deney yapın veya OCR adımını bir Spring Boot mikroservisine entegre edin. Aynı desen makbuzlar, pasaportlar veya kesin metin çıkarımı gereken herhangi bir belge için çalışır."

"If you’ve got questions about scaling this solution or handling noisy scans, drop a comment below—happy coding!" => "Bu çözümü ölçeklendirme veya gürültülü taramalarla başa çıkma konusunda sorularınız varsa, aşağıya yorum bırakın—iyi kodlamalar!"

Now ensure we keep shortcodes at start and end.

Let's assemble final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüden Metin Çıkarma Java’da – Tam OCR Örneği

Görüntüden **metin çıkarma** ihtiyacı hiç duydunuz mu ama hangi kütüphaneyi seçeceğinizden emin değildiniz? Tek başınıza değilsiniz—birçok geliştirici fatura işleme otomasyonu veya aranabilir arşivler oluştururken bu engelle karşılaşıyor. İyi haber? Birkaç Java satırıyla bir resmi OCR için yükleyebilir, ilgi bölgesi (ROI) tanımlayabilir ve ihtiyacınız olan tam metni alabilirsiniz.  

Bu öğreticide **java ocr example** üzerinden **load image for OCR**, ROI ayarlama ve Aspose.OCR kullanarak **extract text from invoice** dosyalarını nasıl çıkaracağınızı adım adım göstereceğiz. Sonunda, herhangi bir Java projesine ekleyebileceğiniz çalıştırılabilir bir programınız olacak.

## Öğrenecekleriniz

- `OcrEngine` örneği oluşturmanın önemi ve nasıl yapılacağı.
- Aspose’un `ImageStream` ile **load image for OCR** doğru yöntemi.
- **region of interest (ROI)** ayarlayarak sadece fatura tutarının bulunduğu bölgeyi işleme.
- Tanınan metni çıkarma ve konsola yazdırma.
- Yaygın tuzaklar (ör. yanlış dikdörtgen koordinatları) ve hızlı çözümler.

**Önkoşullar**

- Java 8 veya daha yeni bir sürüm yüklü.
- Aspose.OCR kütüphanesini (`com.aspose:aspose-ocr`) çekmek için Maven veya Gradle.
- Bilinen bir dizine yerleştirilmiş örnek fatura resmi (`invoice.png`).

Hepsi hazır mı? Harika—hadi başlayalım.

![Extract text from image using Java OCR](/images/extract-text-from-image-java.png "görüntüden metin çıkarma örneği")

## Görüntüden Metin Çıkarma – Adım Adım Java OCR Örneği

Aşağıda tam kaynak kodu bulunuyor. `RoiOcrExample.java` dosyasına kopyalayıp doğrudan çalıştırabilirsiniz.

```java
import com.aspose.ocr.*;

public class RoiOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance.
        // The engine holds all configuration and performs the heavy lifting.
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the source image.
        // You can point to any PNG, JPG, or TIFF file. Here we use a sample invoice.
        String imagePath = "YOUR_DIRECTORY/invoice.png";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 3: Define the region of interest (ROI) you want to recognize.
        // x = 120, y = 340, width = 500, height = 120 – tweak these values for your own layout.
        Rectangle regionOfInterest = new Rectangle(120, 340, 500, 120);
        ocrEngine.setRegionOfInterest(regionOfInterest);

        // Step 4: Perform OCR on the specified ROI and retrieve the text.
        // recognize() returns an OcrResult object; getText() extracts the plain string.
        String extractedText = ocrEngine.recognize().getText();

        // Step 5: Output the recognized text.
        System.out.println("ROI text: " + extractedText);
    }
}
```

### Her Adım Neden Önemli

1. **OCR motoru oluşturma** – motor olmadan görüntü işleme bağlamı yoktur. Nesne ayrıca çok‑dilli destek gerekiyorsa dil paketlerini ayarlamanıza olanak tanır.  
2. **Görüntüyü yükleme** – `ImageStream.fromFile` dosya formatını soyutlayarak motorun baytları doğru okumasını sağlar. Bunu atlayınca `NullPointerException` alırsınız.  
3. **ROI ayarlama** – tüm sayfayı işlemek gereksizdir. Dikdörtgeni fatura toplamı alanına daraltarak tanıma süresini kısar ve gürültüyü azaltırsınız.  
4. **`recognize()` çağrısı** – işin sihri burada gerçekleşir. Metod, ROI üzerinde OCR algoritmasını çalıştırır ve bir sonuç nesnesi üretir.  
5. **Çıktıyı yazdırma** – gerçek projelerde metni bir veritabanına kaydedebilirsiniz, ancak `System.out.println` hızlı bir demo için idealdir.

## OCR için Görüntü Yükleme

Yolun mutlak mı yoksa göreli mi olması gerektiğini merak ediyorsanız, her ikisi de çalışır—sadece Java sürecinin dosyayı okuyabildiğinden emin olun. Windows’ta ters eğik çizgileri kaçırmanız gerekir (`C:\\images\\invoice.png`) ya da ileri eğik çizgileri (`C:/images/invoice.png`) kullanabilirsiniz.  

**İpucu:** Döngüde birçok fatura işliyorsanız aynı `OcrEngine` örneğini yeniden kullanın; dahili kaynakları önbelleğe alır ve verimliliği artırır.

## İlgi Bölgesi (ROI) Tanımlama

Doğru dikdörtgeni bulmak biraz deneme yanılma gerektirebilir. Koordinatları öğrenmenin pratik bir yolu, görüntüyü herhangi bir grafik editöründe (GIMP, Paint.NET vb.) açıp bölge üzerine gelmek; durum çubuğunda X/Y değerlerini görebilirsiniz.  

Köşe durum: bazı faturaların düzeni değişken olabilir. Bu durumda tüm görüntüde hızlı bir ön‑tarama yapıp, “Total:” gibi anahtar kelimeleri regex ile bulabilir ve ROI'yi dinamik olarak ayarlayabilirsiniz.

## OCR Yap ve Metni Al

`recognize()` çağrısı eşzamanlıdır—motor bitene kadar threadiniz bloklanır. Büyük partiler için bir thread havuzu oluşturup görüntüleri paralel işleyebilirsiniz. Her thread’in kendi `OcrEngine` örneğine ihtiyacı olduğunu unutmayın; motor thread‑güvenli değildir.

## Çalıştır ve Çıktıyı Doğrula

Derleyin ve çalıştırın:

```bash
javac -cp "path/to/aspose-ocr.jar" RoiOcrExample.java
java -cp ".:path/to/aspose-ocr.jar" RoiOcrExample
```

Şuna benzer bir çıktı görmelisiniz:

```
ROI text: $1,254.00
```

Çıktı bozuk görünüyorsa, ROI koordinatlarını tekrar kontrol edin ve görüntü kalitesinin yüksek (300 dpi veya daha fazla) olduğundan emin olun.  

### Yaygın Tuzaklar ve Çözüm Yolları

| Belirti | Muhtemel Neden | Çözüm |
|---------|----------------|------|
| Boş string | ROI, görüntü sınırları dışında | Dikdörtgen değerlerini görüntü boyutlarıyla karşılaştırın |
| Yanlış yazılmış kelimeler | Düşük çözünürlük | Daha yüksek çözünürlüklü kaynak kullanın veya görüntü ön‑işleme (ör. ikilileştirme) uygulayın |
| `java.lang.NoClassDefFoundError` | Aspose JAR’ı sınıf yolunda yok | `aspose-ocr.jar` dosyasını `-cp`’ye ekleyin veya Maven/Gradle bağımlılık yönetimini kullanın |

## Sonuç

Artık Java’da **extract text from image** işlemini kısa bir **java ocr example** ile nasıl yapacağınızı biliyorsunuz. Görüntüyü doğru şekilde yükleyip, odaklı bir ROI tanımlayıp ve `recognize()` çağırarak **extract text from invoice** dosyalarından güvenilir bir şekilde metin çıkarabilir ve bu veriyi sonraki sistemlere aktarabilirsiniz.

Sırada ne var? ROI'yi farklı alanlar (tarih, satıcı adı) için değiştirin, çok dilli faturalar için dil paketleriyle deney yapın veya OCR adımını bir Spring Boot mikroservisine entegre edin. Aynı desen makbuzlar, pasaportlar veya kesin metin çıkarımı gereken herhangi bir belge için çalışır.

Bu çözümü ölçeklendirme veya gürültülü taramalarla başa çıkma konusunda sorularınız varsa, aşağıya yorum bırakın—iyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}