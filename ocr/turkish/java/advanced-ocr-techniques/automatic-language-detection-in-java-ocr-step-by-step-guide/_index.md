---
category: general
date: 2026-02-27
description: Otomatik dil algılama, Java’da PNG gibi görüntü dosyalarından metin çıkarmanıza
  olanak tanır—otomatik dil algılamayı etkinleştiren bir Java OCR örneğine bakın.
draft: false
keywords:
- automatic language detection
- extract text from image
- convert png to text
- java ocr example
- enable auto language detection
language: tr
og_description: Java OCR'de otomatik dil algılama, görüntü dosyalarından metin çıkarmayı
  kolaylaştırır. Tam bir Java OCR örneğiyle otomatik dil algılamayı nasıl etkinleştireceğinizi
  öğrenin.
og_title: Java OCR'de Otomatik Dil Algılama – Tam Kılavuz
tags:
- Java
- OCR
- Aspose
title: Java OCR'de Otomatik Dil Tespiti – Adım Adım Rehber
url: /tr/java/advanced-ocr-techniques/automatic-language-detection-in-java-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java OCR'da Otomatik Dil Algılama – Tam Kılavuz

İngilizce ve Rusça karışık bir ekran görüntüsünden metin çıkarırken **otomatik dil algılamaya** hiç ihtiyaç duydunuz mu? Tek başınıza değilsiniz. Gerçek dünyadaki birçok uygulamada—örneğin fiş tarayıcıları, çok dilli formlar veya sosyal medya görüntü botları—dili önceden elle seçmek bir sorun.

İyi haber şu ki Aspose OCR for Java sizin için dili algılayabilir, böylece **extract text from image** dosyalarını manuel bir yapılandırma olmadan basitçe çıkarabilirsiniz. Bu öğreticide **java ocr example** göstererek **auto language detection** özelliğini etkinleştiren, karışık dilli bir PNG işleyen ve sonucu konsola yazdıran bir örnek sunacağız. Sonunda sadece birkaç satır kodla **convert png to text** nasıl yapılacağını tam olarak öğreneceksiniz.

## Gereksinimler

- Java 17 (veya herhangi bir yeni JDK) – API Java 8+ ile çalışır ancak daha yeni çalışma zamanları daha iyi performans sağlar.
- Aspose OCR for Java kütüphanesi (2026‑02‑27 itibarıyla en son sürüm). Maven Central'dan edinebilirsiniz:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version>
</dependency>
```

- Birden fazla dil içeren bir görüntü dosyası. Demo için `mixed-eng-rus.png` (İngilizce + Rusça) kullanacağız.  
- İyi bir IDE (IntelliJ IDEA, Eclipse, VS Code…) – herhangi biri yeterli.

> **Pro tip:** Test görüntünüz yoksa, sadece birkaç İngilizce kelime ve bunların Rusça karşılıklarını içeren bir PNG oluşturun. OCR motoru kaynağa değil, sadece piksel verisine bakar.

Aşağıda tam, çalıştırmaya hazır program bulunmaktadır.

![Karışık dilli PNG üzerinde otomatik dil algılama](/images/mixed-eng-rus.png "otomatik dil algılama örneği")

## Adım 1: OCR Motorunu Kurun

İlk olarak `OcrEngine` bir örnek oluşturun. Bu nesne kütüphanenin kalbidir; tüm yapılandırma seçeneklerini tutar, **automatic language detection** özelliğini açan seçeneği de içerir.

```java
import com.aspose.ocr.*;

public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable automatic language detection
        ocrEngine.setAutoDetectLanguage(true);
```

Neden burada etkinleştiriyoruz?  
`setAutoDetectLanguage(true)` olmadan, motor varsayılan bir dili (genellikle İngilizce) varsayar. Görüntünüz farklı alfabeler karıştırdığında, algılama adımı doğruluğu büyük ölçüde artırır—bunu, OCR'ın çok dilli bir tercümanın çeviriden önce dinlemesi gibi düşünün.

## Adım 2: Görüntüyü Besleyin ve OCR İşlemini Çalıştırın

Şimdi motoru PNG dosyasına yönlendirin. `processImage` metodu, tanınan metni, güven skorlarını ve hatta algılanan dil kodunu içeren bir `OcrResult` nesnesi döndürür.

```java
        // Step 3: Process the image that contains both English and Russian text
        OcrResult ocrResult = ocrEngine.processImage("YOUR_DIRECTORY/mixed-eng-rus.png");
```

İki önemli nokta:

- **Path handling:** Mutlak bir yol kullanın veya görüntüyü projenizin resources klasörüne koyup `getResourceAsStream` ile yükleyin.
- **Performance tip:** Birçok görüntü işliyorsanız, her seferinde yeni bir `OcrEngine` oluşturmak yerine aynı örneği yeniden kullanın. Motor dil modellerini önbelleğe alır, böylece sonraki çağrılar daha hızlı olur.

## Adım 3: Tanınan Metni Alın ve Görüntüleyin

Son olarak, `OcrResult` içinden düz metni alın. `getText()` metodu tüm düzen bilgilerini kaldırır ve saklayabileceğiniz, arama yapabileceğiniz veya başka bir sisteme besleyebileceğiniz temiz bir dize verir.

```java
        // Step 4: Print the recognized text to the console
        System.out.println(ocrResult.getText());
    }
}
```

Programı çalıştırdığınızda aşağıdakine benzer bir çıktı görmelisiniz:

```
Hello world!
Привет мир!
```

Bu çıktı, motorun **automatic language detection** sayesinde hem İngilizce hem de Rusça bölümleri doğru şekilde tanımladığını doğrular. Bayrağı kapatırsanız, muhtemelen bozuk Kiril karakterleri alırsınız; bu da otomatik algılama özelliğinin karışık dil senaryolarında neden hayati olduğunu gösterir.

## Yaygın Varyasyonlar ve Kenar Durumları

### Dil Algılaması Olmadan PNG'yi Metne Dönüştürme

Görüntünün yalnızca tek bir dil içerdiğini biliyorsanız, otomatik algılama adımını atlayabilirsiniz:

```java
ocrEngine.setLanguage(OcrLanguage.English);
```

Ancak unutmayın, başka bir alfabeden bir karakter bile göründüğünde doğruluk keskin bir şekilde düşer.

### Büyük Görüntüleri İşleme

Yüksek çözünürlüklü taramalar için, görüntüyü beslemeden önce maksimum 300 DPI'ye küçültmeyi düşünün. OCR motoru 150‑300 DPI aralığında en iyi performansı gösterir; bu aralığın üzerindeki DPI'ler ölçülebilir bir kazanç sağlamadan belleği boşa harcar.

```java
BufferedImage original = ImageIO.read(new File("large.png"));
BufferedImage resized = ImageUtil.resize(original, 1024, 0); // keep aspect ratio
ocrEngine.processImage(resized);
```

### Web Servisinde Görüntüden Metin Çıkarma

Bu işlevi bir REST uç noktası üzerinden sunuyorsanız, şunları unutmayın:

- Yüklenen dosya tipini doğrulayın (sadece PNG/JPEG kabul edin).
- OCR'ı bir arka plan iş parçacığında veya async görevde çalıştırın, böylece istek iş parçacığını engellemez.
- Metni JSON olarak döndürün:

```json
{ "extractedText": "Hello world!\nПривет мир!" }
```

## Tam Çalışan Örnek (Tüm Adımlar Birleştirildi)

Aşağıda `MixedLanguageDemo.java` dosyasına kopyalayıp yapıştırabileceğiniz tam program bulunmaktadır. İçe aktarma ifadelerini, hata yönetimini ve her satırı açıklayan bir yorumu içerir.

```java
import com.aspose.ocr.*;
import java.io.File;

/**
 * Demonstrates automatic language detection with Aspose OCR for Java.
 * This example loads a PNG that contains both English and Russian text,
 * enables auto‑detect, and prints the extracted text.
 */
public class MixedLanguageDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Enable automatic language detection so the engine picks the right script(s)
        ocrEngine.setAutoDetectLanguage(true);

        // Path to the image – replace with your actual location
        String imagePath = "YOUR_DIRECTORY/mixed-eng-rus.png";

        // Process the image and obtain the result
        OcrResult ocrResult = ocrEngine.processImage(imagePath);

        // Output the recognized text – should contain both English and Russian lines
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Şu şekilde çalıştırın:

```bash
mvn compile exec:java -Dexec.mainClass=MixedLanguageDemo
```

Her şey doğru şekilde ayarlandıysa, konsol İngilizce satırı ve ardından Rusça karşılığını gösterecektir.

## Özet ve Sonraki Adımlar

Bir **java ocr example** üzerinden **automatic language detection** özelliğini **etkinleştiren**, karışık dilli bir PNG işleyen ve **extract text from image** dosyalarını manuel dil seçimi olmadan çıkaran bir örnek gösterdik. Temel çıkarımlar:

1. `setAutoDetectLanguage(true)`'ı açarak Aspose'un çok dilli içeriği yönetmesini sağlayın.
2. Herhangi bir PNG (veya JPEG) beslemek ve `getText()` ile temiz bir dize almak için `processImage` kullanın.
3. Aynı desen PDF'ler, TIFF'ler veya hatta canlı kamera akışları için de çalışır—sadece giriş kaynağını değiştirin.

Daha ileri gitmek mi istiyorsunuz? Şu fikirleri deneyin:

- **Batch processing:** PNG klasörünün üzerinden döngü kurup her sonucu bir veritabanına kaydedin.
- **Language‑specific post‑processing:** Algılamadan sonra İngilizce metni bir yazım denetleyicisine, Rusça metni ise bir transliterasyon hizmetine yönlendirin.
- **Combine with AI:** Çıkarılan metni özetleme veya çeviri için bir dil modeline besleyin.

Şimdilik hepsi bu. Herhangi bir sorunla karşılaşırsanız—örneğin motor beklediğiniz dili algılamıyorsa—görüntünün net olduğundan ve en son Aspose OCR sürümünü kullandığınızdan emin olun. İyi kodlamalar ve Java projelerinizde **automatic language detection** gücünün tadını çıkarın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}