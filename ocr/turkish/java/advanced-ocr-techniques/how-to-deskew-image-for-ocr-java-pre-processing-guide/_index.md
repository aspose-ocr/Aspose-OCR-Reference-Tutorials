---
category: general
date: 2026-03-18
description: Aspose OCR Java kullanarak görüntünün eğriliğini hızlıca nasıl düzeltirsiniz.
  OCR için görüntüyü ön işleme, taranmış görüntüyü temizleme ve sadece birkaç adımda
  OCR doğruluğunu artırmayı öğrenin.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- extract text from image
- clean scanned image
- improve ocr accuracy
language: tr
og_description: Aspose OCR Java ile görüntüyü eğriltmeyi düzeltme, OCR için görüntüyü
  ön işleme, taranmış görüntüyü temizleme ve OCR doğruluğunu artırma.
og_title: OCR için Görüntüyü Düzeltme – Java Rehberi
tags:
- OCR
- Java
- Image Processing
title: OCR için Görüntüyü Düzeltme – Java Ön İşleme Kılavuzu
url: /tr/java/advanced-ocr-techniques/how-to-deskew-image-for-ocr-java-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR için Görüntüyü Düzeltme – Java Ön‑İşleme Kılavuzu

Tarayıcıdan garip bir açıyla çıkan **görüntüyü nasıl düzeltiriz** dosyalarını hiç merak ettiniz mi? Tek başınıza değilsiniz—çok sayıda geliştirici, görüntü ağırlıklı belgelerden metin çıkarmaya çalışırken bu soruna takılıyor. İyi haber? Birkaç Java satırı ve Aspose OCR ile görüntüyü düzeltebilir, gürültüyü azaltabilir ve temiz metni zahmetsizce elde edebilirsiniz.

Bu öğreticide tüm iş akışını adım adım inceleyeceğiz: gürültülü ve döndürülmüş bir taramayı yüklemek, bir düzeltme filtresi uygulamak, görsel dağınıklığı kaldırmak ve sonunda **görüntüden metin çıkarmak**. Sonunda **OCR için görüntüyü ön işleme**, **tarama görüntülerini temizleme** ve **OCR doğruluğunu artırma** konularını öğrenmiş olacaksınız; böylece güvenilir metin çıkarımı gerektiren her projede bu becerileri kullanabilirsiniz.

## Gereksinimler

- Java 17 (veya herhangi bir güncel JDK) – kod standart dil özelliklerini kullanır.
- Aspose OCR for Java kütüphanesi (ücretsiz deneme sürümü deneyler için yeterlidir).
- Hem gürültülü hem de döndürülmüş bir örnek görüntü (ör. `noisy-rotated.png`).
- Sevdiğiniz IDE (IntelliJ IDEA, Eclipse, VS Code…) – Java derleyebilen herhangi bir şey.

Ekstra çerçeve, Maven/Gradle sihri gerekmez; tek gerekli import ifadeleri aşağıda gösterilenlerdir.

---

## Aspose OCR ile Görüntüyü Nasıl Düzeltiriz

İlk ele alınması gereken şey görüntünün eğimidir. Metin satırları yatay değilse, OCR motoru karakterleri yanlış okuyacaktır. `DeskewFilter` bu işi halleder.

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.Image;
import com.aspose.ocr.preprocess.DeskewFilter;
import com.aspose.ocr.preprocess.DenoiseFilter;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the raw scanned image
        Image scannedImage = Image.load("YOUR_DIRECTORY/noisy-rotated.png");

        // Step 3: Correct the image orientation (deskew)
        DeskewFilter deskewFilter = new DeskewFilter();
        scannedImage = deskewFilter.apply(scannedImage);

        // Step 4: Reduce visual noise (denoise)
        DenoiseFilter denoiseFilter = new DenoiseFilter();
        scannedImage = denoiseFilter.apply(scannedImage);

        // Step 5: Perform OCR on the cleaned image
        String recognizedText = ocrEngine.recognize(scannedImage);

        // Step 6: Output the extracted text
        System.out.println(recognizedText);
    }
}
```

> **Why this matters:** `DeskewFilter` görüntünün geometrisini analiz eder, dönüş açısını tahmin eder ve bitmap'i düz bir ufka geri döndürür. Bu adım olmadan çoğu OCR motoru eğik harfleri tamamen farklı glifler olarak algılar ve **OCR doğruluğunu artırma** çabalarınızı zorlaştırır.

> **Pro tip:** Belgelerinizin baş aşağı olma ihtimali varsa, `DeskewFilter` üzerindeki `setAutoRotate` bayrağını etkinleştirin (yeni Aspose sürümlerinde bulunur). Gerekli olduğunda otomatik olarak 180° döndürür.

![Dönüşüm öncesi ve sonrası diyagramı – görüntüyü nasıl düzeltiriz](https://example.com/deskew-diagram.png "görüntüyü nasıl düzeltiriz örneği")

*Görsel alt metni: görüntüyü nasıl düzeltiriz örneği*

---

## OCR için Görüntüyü Ön İşleme – Gürültü Azaltma ve Temizleme

Görüntü düzeldikten sonra bir sonraki engel görsel gürültüdür—OCR motorunu şaşırtan nokta lekeleri, sıkıştırma artefaktları veya soluk arka plan desenleri. `DenoiseFilter` kenarları (harfleri) koruyan, taneleri temizleyen hafif bir yumuşatma algoritması uygular.

```java
// Step 4 (continued): Reduce visual noise (denoise)
DenoiseFilter denoiseFilter = new DenoiseFilter();
scannedImage = denoiseFilter.apply(scannedImage);
```

### Gürültü Azaltma Ayarlarını Ne Zaman Düzenlemelisiniz

- **Çok karanlık taramalar:** Arka plan gölgelerini temizlemek için filtrenin gücünü artırın (`denoiseFilter.setStrength(2)`).
- **İnce baskı fontları:** Küçük seriflerin bulanıklaşmasını önlemek için gücü azaltın.
- **Renkli belgeler:** Önce gri tonlamaya dönüştürün (`scannedImage = scannedImage.toGrayscale();`)—OCR motoru tek kanallı görüntülerde en iyi performansı gösterir.

Bu ayarlamalar **tarama görüntülerini temizleme** en iyi uygulamalarının bir parçasıdır; daha temiz bir bitmap, OCR motorundan daha yüksek güven puanları elde edilmesini sağlar.

---

## Görüntüden Metin Çıkarma – OCR Motorunu Çalıştırma

Resim artık düz ve sessiz olduğuna göre, **görüntüden metin çıkarmanın** zamanı geldi. `OcrEngine` sınıfı her şeyi arka planda yönetir: segmentasyon, karakter sınıflandırması ve dil modellemesi.

```java
// Step 5: Perform OCR on the cleaned image
String recognizedText = ocrEngine.recognize(scannedImage);
System.out.println(recognizedText);
```

#### Beklenen Çıktı

Kaynak dosyanızda “**Invoice # 12345**” satırı varsa, konsol şu şekilde bir şey yazdırmalıdır:

```
Invoice # 12345
Date: 2026-03-18
Total: $1,250.00
```

Çıktı bozuk görünüyorsa, önceki adımları tekrar kontrol edin—özellikle düzeltmeyi. 1 derece bile sayıları ve sembolleri bozabilir.

---

## Yaygın Tuzaklar ve **OCR Doğruluğunu Artırma** İpuçları

| Sorun | Doğruluğu Neden Zarar Görür | Hızlı Çözüm |
|-------|----------------------------|-------------|
| **Kalan dönüş** | OCR yatay temel çizgileri bekler. | `deskewFilter.getAngle()` ile doğrulayın ve değeri kaydedin. |
| **Aşırı gürültü azaltma** | İnce çizgileri bulanıklaştırır, “i” harfini “l” ye dönüştürür. | İnce fontlar için `setStrength(0.5)` kullanın. |
| **Yanlış görüntü formatı** | JPEG sıkıştırması artefakt ekler. | Kayıpsız depolama için PNG veya TIFF tercih edin. |
| **Yanlış dil** | Motor varsayılan olarak İngilizce; diğer alfabeler açık ayar gerektirir. | `ocrEngine.setLanguage(OcrEngine.Language.Spanish);` |
| **Düşük DPI (≤150)** | Güvenilir segmentasyon için yeterli piksel verisi yok. | İşleme öncesi 300 DPI'ye yeniden örnekleyin (`scannedImage = scannedImage.resample(300);`). |

### Bonus: Toplu İşleme

Eğer bir klasör tarama dosyanız varsa, demoyu bir döngüye sarın:

```java
File folder = new File("YOUR_DIRECTORY");
for (File file : folder.listFiles((dir, name) -> name.endsWith(".png"))) {
    Image img = Image.load(file.getAbsolutePath());
    img = new DeskewFilter().apply(img);
    img = new DenoiseFilter().apply(img);
    String text = ocrEngine.recognize(img);
    System.out.println("=== " + file.getName() + " ===");
    System.out.println(text);
}
```

Bu desen, **OCR için görüntüyü ön işleme** işlemini ölçekli olarak yapmanızı sağlar, kod tabanını düzenli tutar ve performansı öngörülebilir kılar.

---

## Özet ve Sonraki Adımlar

Aspose OCR Java kullanarak **görüntüyü nasıl düzeltiriz** dosyalarını, **OCR için görüntüyü ön işleme** ve sonunda **görüntüden metin çıkarma** konularını ele aldık. Taramayı düzeltip, gürültüyü temizleyip, motoru kusursuz bir bitmap ile besleyerek, **OCR doğruluğunu artırma** konusunda belirgin bir iyileşme göreceksiniz.

Sırada ne var? Şu genişletmeleri düşünün:

- **Dil algılama** – algılanan betiğe göre `ocrEngine.setLanguage` değiştirin.
- **PDF çıktısı** – tanınan metni aranabilir belgeler için bir PDF oluşturucuya besleyin.
- **Makine‑öğrenimi sonrası işleme** – OCR sonucunda yazım denetimi veya özel sözlükler çalıştırın.

Bu fikirleri deneyin, farklı filtre güçleriyle oynayın ve kısa sürede herhangi bir belge‑dijitalleştirme projesi için sağlam bir işlem hattına sahip olacaksınız.

---

*Kodlamada iyi eğlenceler! Bir sorunla karşılaşırsanız, aşağıya yorum bırakın—düzeltme ve gürültü azaltma parametrelerini ince ayarlamanıza yardımcı olurum.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}