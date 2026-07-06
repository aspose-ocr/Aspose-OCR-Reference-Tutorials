---
category: general
date: 2026-02-19
description: GPU'yu hızlı OCR işleme için nasıl etkinleştirirsiniz. Yüksek çözünürlüklü
  görüntüyü yüklemeyi, metin görüntüsünü tanımayı ve Aspose OCR kullanarak metni çıkarmayı
  öğrenin.
draft: false
keywords:
- how to enable gpu
- load high resolution image
- recognize text image
- how to extract text
- enable gpu processing
language: tr
og_description: GPU'yi hızlı OCR işleme için nasıl etkinleştirirsiniz. Bu rehber,
  yüksek çözünürlüklü bir görüntüyü nasıl yükleyeceğinizi, metin görüntüsünü tanıyacağınızı
  ve Aspose OCR ile metni nasıl çıkaracağınızı gösterir.
og_title: Java’da OCR için GPU’yu Etkinleştirme – Tam Rehber
tags:
- OCR
- Java
- GPU
- Aspose
title: Java'da OCR için GPU'yu Nasıl Etkinleştirirsiniz – Tam Kılavuz
url: /tr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java’da OCR için GPU Nasıl Etkinleştirilir – Tam Kılavuz

OCR hattınızda **GPU'yu nasıl etkinleştireceğinizi** merak ettiniz mi ve işleme süresinden saniyeler kazandırmak istediniz? Tek başınıza değilsiniz. Görüntü ağırlıklı birçok projede darboğaz, CPU‑bağlı metin çıkarma adımıdır ve GPU'ya geçmek bir oyun değiştirici olabilir.

Bu öğreticide **yüksek çözünürlüklü bir görüntü** yüklemeyi, Aspose OCR'yi GPU üzerinde çalışacak şekilde yapılandırmayı ve sonunda sadece birkaç Java satırıyla **metin görüntüsünü tanıma** ve **metni çıkarma** işlemlerini göstereceğiz. Sonunda, **GPU işleme etkinleştirme** sürecini uçtan uca gösteren çalıştırmaya hazır bir programınız olacak.

## Gereksinimler

- Java 17 veya daha yeni (kod modül sistemini kullanıyor ancak küçük ayarlamalarla daha eski JDK'larda da çalışır)  
- Aspose OCR for Java 23.10 (veya en son sürüm) – Maven koordinatlarını Aspose sitesinden alabilirsiniz  
- CUDA 12+ sürücüleri yüklü bir NVIDIA GPU (aksi takdirde kütüphane başlatılamaz)  
- Metin okumak istediğiniz yüksek çözünürlüklü örnek bir görüntü (PNG veya JPEG)  

Hepsi bu. Harici hizmetler, bulut kredileri yok, sadece makineniz ve doğru sürücü yığını.

![GPU OCR workflow – how to enable GPU processing](gpu-ocr-workflow.png)

*Görsel alt metni: Java’da OCR işleme için GPU'nun nasıl etkinleştirileceğini gösteren diyagram.*

## Adım‑Adım Uygulama

Aşağıda çözümü mantıksal parçalara ayırıyoruz. Her bölüm, kısa bir kod parçacığı, adımın **neden** önemli olduğuna dair bir açıklama ve muhtemelen ileride takdir edeceğiniz birkaç pratik ipucu içerir.

### GPU'yu OCR için Etkinleştirme – Adım 1: Bağımlılıkları Kurun ve CUDA'yı Doğrulayın

Herhangi bir Java kodu çalıştırılmadan önce, yerel CUDA çalışma zamanı bulunabilir olmalıdır. Windows'ta şu komutla doğrulayabilirsiniz:

```bat
nvcc --version
```

Linux'ta:

```bash
nvidia-smi
```

Komut sürücü sürümünü ve GPU detaylarını yazdırıyorsa, hazırsınız demektir. Aksi takdirde NVIDIA'nın web sitesine gidin, uygun sürücüyü indirin ve CUDA araç setini kurun (sürümün Aspose OCR gereksinimleriyle – şu anda 12.x – eşleştiğinden emin olun).

**İpucu:** GPU sürücünüzü güncel tutun ancak “en son‑beta” sürümlerinden kaçının; bazen Aspose yerel kütüphaneleriyle ikili uyumluluğu bozabilirler.

### GPU'yu OCR için Etkinleştirme – Adım 2: Aspose OCR Maven Bağımlılığını Ekleyin

`pom.xml` dosyanıza aşağıdakileri ekleyin. Bu, çekirdek OCR motorunu ve Windows, Linux ve macOS için yerel GPU ikili dosyalarını getirir.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

Gradle tercih ediyorsanız eşdeğeri şudur:

```gradle
implementation 'com.aspose:aspose-ocr:23.10'
```

Projenizi yeniledikten sonra `OcrEngine`, `OcrDeviceType` ve `ImageStream` sınıfları kullanılabilir hâle gelir.

### GPU'yu OCR için Etkinleştirme – Adım 3: OCR Motorunu Oluşturun ve GPU'yu Etkinleştirin

Şimdi Aspose'ye GPU üzerinde çalışmasını söylüyoruz. `OcrEngine`, işleme cihaz tipini değiştirebileceğimiz bir `Device` nesnesi sunar.

```java
import com.aspose.ocr.*;

public class GpuOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 3.1: Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 3.2: Enable GPU processing (requires a CUDA‑enabled driver & runtime)
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);

        // Optional: limit the number of GPU streams for better resource control
        ocrEngine.getDevice().setStreamCount(2);

        // Step 3.3: Load the high‑resolution image to be recognized
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample-highres.png"));

        // Step 3.4: Perform OCR and retrieve the recognized text
        String recognizedText = ocrEngine.recognize().getText();

        // Step 3.5: Display the extracted text
        System.out.println("=== OCR RESULT ===");
        System.out.println(recognizedText);
    }
}
```

**Neden önemli:** `OcrDeviceType.GPU` ayarı, temel çıkarım motorunu yalnızca CPU tabanlı bir uygulamadan CUDA hızlandırmalı birine değiştirir. İsteğe bağlı `setStreamCount` çağrısı paralelliği kontrol etmenizi sağlar; iki akış, çoğu tüketici kartı için güvenli bir varsayılandır.

### GPU'yu OCR için Etkinleştirme – Adım 4: Yüksek Çözünürlüklü Görüntüyü Yükleyin

Yüksek çözünürlüklü kaynaklar OCR modeline daha fazla görsel detay sağlar; bu da özellikle küçük yazı tipleri veya karmaşık betikler için daha yüksek doğruluk anlamına gelir. `ImageStream.fromFile` yardımcı işlevi dosyayı motorun beklediği formata okur.

Bir URL'den veya bellek içi bayt dizisinden **yüksek çözünürlüklü görüntü** yüklemeniz gerekiyorsa, şu şekilde kullanabilirsiniz:

```java
byte[] imageBytes = java.nio.file.Files.readAllBytes(Paths.get("remote-image.png"));
ocrEngine.setImage(ImageStream.fromBytes(imageBytes));
```

**Köşe durumu:** Bazı GPU'ların maksimum doku boyutu vardır (genellikle 16384 × 16384). Görüntünüz bunu aşıyorsa, okunabilirliği koruyan bir boyuta (ör. 3000 × 2000) küçültmeyi düşünün. Görüntüyü yüklemeden önce `ocrEngine.setResizeFactor(0.5)` çağırırsanız OCR motoru otomatik olarak yeniden boyutlandırır.

### GPU'yu OCR için Etkinleştirme – Adım 5: Metin Görüntüsünü Tanıyın ve Metni Çıkarın

`ocrEngine.recognize()` çağrısı, GPU üzerinde sinir ağı çıkarımını tetikler. Metot bir `OcrResult` nesnesi döndürür; `getText()` düz metni çıkarır. Daha zengin veri gerekiyorsa sınırlayıcı kutuları, güven skorlarını veya ham JSON'u da alabilirsiniz.

```java
OcrResult result = ocrEngine.recognize();
String plainText = result.getText();
System.out.println("Detected text length: " + plainText.length());

// Optional: iterate over each line with its confidence
result.getPages().forEach(page -> {
    page.getLines().forEach(line -> {
        System.out.printf("Line: \"%s\" (Confidence: %.2f%%)%n",
                line.getText(), line.getConfidence() * 100);
    });
});
```

**Neden isteyebilirsiniz:** `recognize text image` adımı, GPU'nun parladığı yerdir—CPU'da saniyeler sürecek büyük görüntüler, çok daha kısa sürede işlenir. Güven skorları, düşük kalite sonuçları filtrelemenizi sağlar; bu, daha sonra **metni nasıl çıkaracağınız** konusunda faydalı bir hiledir.

### Profesyonel İpuçları ve Yaygın Tuzaklar

| Durum | Ne Yapmalı |
|-----------|------------|
| **GPU'da bellek yetersizliği hataları** | `setStreamCount` değerini 1'e düşürün veya görüntüyü motorun içine beslemeden önce küçültün. |
| **Yüksek çözünürlüğe rağmen tanınmayan karakterler** | Dil modelinin (`ocrEngine.setLanguage(OcrLanguage.ENGLISH)`) metin diliyle eşleştiğinden emin olun. |
| **CUDA sürüm uyumsuzluğu** | CUDA araç seti sürümünü Aspose OCR ile gelen sürümle eşleştirin (sürüm notlarını kontrol edin). |
| **Birden fazla GPU** | İlk GPU meşgulse ikinci GPU'yu seçmek için `ocrEngine.getDevice().setDeviceId(1)` kullanın. |
| **Ekransız bir sunucuda çalıştırma** | Ek bir adım gerekmez; GPU sürücüsü ekran olmadan da çalışır. |

## Metni Çıkarma – Çıktıyı Doğrulama

Yukarıdaki sınıfı çalıştırdığınızda aşağıdakine benzer bir çıktı görmelisiniz:

```
=== OCR RESULT ===
Welcome to the Aspose OCR demo!
Your GPU is now accelerating text extraction.
```

Çıktı bozuk görünüyorsa, görüntünün gerçekten yüksek çözünürlüklü olduğundan ve GPU sürücüsünün doğru kurulduğundan iki kez kontrol edin. Ayrıntılı günlüklemeyi de etkinleştirebilirsiniz:

```java
ocrEngine.setLogLevel(OcrLogLevel.DEBUG);
```

Günlükler, yerel CUDA çekirdeklerinin başarıyla yüklenip yüklenmediğini gösterecek.

## Sonraki Adımlar ve İlgili Konular

- **Toplu işleme:** `OcrEngine`'i bir döngü içinde sarın ve bir görüntü yolu listesi besleyin. Tekrarlanan GPU başlatma maliyetinden kaçınmak için aynı motor örneğini yeniden kullanmayı unutmayın.  
- **Dil algılama:** Aspose OCR 30'dan fazla dili destekler. `ocrEngine.setLanguage(OcrLanguage.FRENCH)` ile değiştirin.  
- **Son işleme:** Çıkarılan dizeyi temizlemek için düzenli ifadeler kullanın veya bir sonraki NLP hattına besleyin.  
- **Alternatif cihazlar:** CUDA‑uyumlu bir GPU'nuz yoksa `OcrDeviceType.CPU`'ya geri dönebilirsiniz. Aynı kod çalışır; sadece cihaz tipini değiştirin.  
- **Performans ölçümü:** `recognize()` öncesi ve sonrası `System.nanoTime()` ile zaman farkını ölçerek **GPU işleme etkinleştirme** kazancını nicel olarak belirleyin.

---

### Özet

Java'da Aspose OCR için **GPU'yu nasıl etkinleştireceğinizi** doğru sürücüleri kurmaktan **yüksek çözünürlüklü bir görüntü** yüklemeye, **metin görüntüsünü tanımaya** ve sonunda sonuçtan **metni nasıl çıkaracağınızı** kapsadık. Yukarıdaki tam, çalıştırılabilir örnek, modern bir NVIDIA GPU'da sorunsuz çalışmalıdır.

Deneyin, farklı görüntü boyutlarıyla oynayın ve OCR verimliliğinizin nasıl yükseldiğini izleyin. Herhangi bir sorunla karşılaşırsanız, ipuçları bölümüne geri dönün veya en yeni **GPU işleme etkinleştirme** önerileri için Aspose sürüm notlarını kontrol edin.

Kodlamaktan keyif alın ve GPU'nuz metni işlerken serin kalmaya devam etsin!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}