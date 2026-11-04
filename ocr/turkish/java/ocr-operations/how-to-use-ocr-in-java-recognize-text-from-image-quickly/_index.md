---
category: general
date: 2026-02-17
description: Java'da OCR kullanarak görüntü dosyalarından metin tanımayı, PNG makbuzlarından
  metin çıkarmayı ve makbuzu Aspose OCR ile JSON'a dönüştürmeyi öğrenin.
draft: false
keywords:
- how to use OCR
- recognize text from image
- extract text from png
- convert receipt to json
language: tr
og_description: Görüntüden metin tanıma, PNG makbuzlardan metin çıkarma ve makbuzu
  JSON'a dönüştürme için Java'da OCR kullanımına yönelik adım adım rehber.
og_title: Java'da OCR Nasıl Kullanılır – Görüntüden Metin Tanıma
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Java'da OCR Nasıl Kullanılır – Görüntüden Metni Hızlıca Tanıma
url: /tr/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da OCR Nasıl Kullanılır – Görüntüden Metni Hızlıca Tanıma

Hiç **how to use OCR**'ı bir makbuz fotoğrafından metin çıkarmak için kullandınız mı? Belki birkaç çevrimiçi araç denediniz, ancak karışık karakterler ya da işleyemediğiniz bir formatla karşılaştınız. İyi haber şu ki, birkaç Java satırıyla **recognize text from image** dosyalarından **extract text from PNG** makbuzlarından metin çıkarabilir ve hatta **convert receipt to JSON** yaparak sonraki işlemler için kullanabilirsiniz.  

Bu öğreticide, Aspose OCR kütüphanesinin lisanslanmasından temiz bir JSON yükü elde etmeye kadar tam iş akışını adım adım göstereceğiz; bu JSON'u bir veritabanına ya da makine‑öğrenimi modeline besleyebilirsiniz. Gereksiz ayrıntı yok, sadece IDE'nize kopyalayıp yapıştırabileceğiniz pratik, çalıştırılabilir bir örnek. Sonunda, `receipt.png` dosyasını alıp kullanıma hazır bir JSON dizesi üreten bağımsız bir programınız olacak.

## Gereksinimler

- **Java Development Kit (JDK) 8+** – herhangi bir yeni sürüm yeterlidir.  
- **Aspose OCR for Java** kütüphanesi (Maven bağımlılığı `com.aspose:aspose-ocr`).  
- **Geçerli bir Aspose OCR lisans dosyası** (`Aspose.OCR.lic`). Ücretsiz deneme sürümü test için çalışır, ancak tam lisans değerlendirme sınırlamalarını kaldırır.  
- Metni okumak istediğiniz bir görüntü dosyası (PNG, JPEG vb.) – buna `receipt.png` diyelim ve bilinen bir klasöre koyun.  
- Sevdiğiniz IDE (IntelliJ IDEA, Eclipse, VS Code…) – seçiminiz serbest.

> **Pro tip:** Lisans dosyanızı kaynak klasörünün dışına koyun ve mutlak ya da göreli bir yol ile referans verin; böylece sürüm kontrolüne eklenmesini önlersiniz.

Şimdi ön koşullar net, gerçek koda dalalım.

## OCR Nasıl Kullanılır – Temel Adımlar

Aşağıda gerçekleştireceğimiz eylemlerin yüksek‑seviye bir özetini bulabilirsiniz:

1. **Aspose OCR kütüphanesini yükleyin** ve lisansınızı uygulayın.  
2. **`OcrEngine` örneği oluşturun** – bu, ağır işi yapan motor.  
3. **İşlemek istediğiniz görüntüyü işaret eden bir `OcrInput` nesnesi hazırlayın**.  
4. **`ResultFormat.JSON` ile `recognize` çağırın** ve çıkarılan metnin JSON temsilini alın.  
5. **JSON çıktısını işleyin** – ekrana yazdırın, dosyaya kaydedin ya da daha ileri işleyin.

Her adım, aşağıdaki bölümlerde ayrıntılı olarak açıklanmıştır.

## Adım 1 – Aspose OCR'yi Kurun ve Lisansınızı Uygulayın

İlk olarak, Maven kullanıyorsanız `pom.xml` dosyanıza Aspose OCR bağımlılığını ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

Şimdi, Java kodunuzda lisansı yükleyin. Bu adım çok önemlidir; lisans olmadan kütüphane değerlendirme modunda çalışır ve çıktıya filigran ekleyebilir.

```java
import com.aspose.ocr.*;

public class OcrSetup {
    public static void applyLicense() throws Exception {
        // Replace the path with the actual location of your Aspose.OCR.lic file
        License ocrLicense = new License();
        ocrLicense.setLicense("C:/licenses/Aspose.OCR.lic");
    }
}
```

> **Why this matters:** `License` nesnesi OCR motoruna tam özellik setini (yüksek doğruluklu tanıma ve JSON dışa aktarma dahil) kullanma yetkisi verildiğini bildirir. Bu adımı atlamak **recognize text from image** yapmanıza izin verir, ancak sonuçlar kısıtlanabilir.

## Adım 2 – OCR Motoru Örneğini Oluşturun

`OcrEngine` sınıfı tüm OCR işlemlerinin giriş noktasıdır. Bunu, pikselleri okuyup hangi karakterleri temsil ettiklerine karar veren “beyin” olarak düşünebilirsiniz.

```java
import com.aspose.ocr.*;

public class OcrEngineFactory {
    public static OcrEngine createEngine() {
        // No special configuration needed for basic usage
        return new OcrEngine();
    }
}
```

Motoru (örneğin dil ayarlamak, eğikliği düzeltmek) daha sonra özelleştirebilirsiniz; makbuzlarınız Latin dışı betikler içeriyorsa ya da açıyla taranmışsa bu faydalı olur. Çoğu ABD‑tabanlı makbuz için varsayılan ayarlar gayet yeterlidir.

## Adım 3 – İşlemek İstediğiniz Görüntüyü Yükleyin

Şimdi OCR motorunu makbuzu tutan dosyaya yönlendireceğiz. `OcrInput` sınıfı birden fazla görüntüyü kabul edebilir, ancak bu öğreticide tek bir PNG ile basit tutacağız.

```java
import com.aspose.ocr.*;

public class ImageLoader {
    public static OcrInput loadImage(String imagePath) {
        OcrInput input = new OcrInput();
        // Add the PNG receipt – this is where we **extract text from PNG**
        input.add(imagePath);
        return input;
    }
}
```

Eğer toplu olarak **extract text from PNG** dosyalarına ihtiyacınız olursa, sadece `input.add()` metodunu tekrar tekrar çağırın ya da bir dosya yolu listesi geçirin.

## Adım 4 – Metni Tanıyın ve Makbuzu JSON'a Dönüştürün

İşte öğreticinin kalbi. Motoru metni tanıması ve sonucu JSON formatında döndürmesi için istiyoruz. `ResultFormat.JSON` bayrağı tüm ağır işi bizim için yapar.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.output.*;

public class JsonRecognizer {
    public static String recognizeToJson(OcrEngine engine, OcrInput input) throws Exception {
        // Perform OCR and request JSON output
        OcrResult result = engine.recognize(input, ResultFormat.JSON);
        // Retrieve the JSON string
        return result.getJson();
    }
}
```

JSON yükü, tanınan her satırı, sınırlayıcı kutusunu, güven skorunu ve ham metni içerir. Bu yapı, **convert receipt to JSON** işlemini son derece basit hâle getirir ve ardından herhangi bir downstream API'ye besleyebilirsiniz.

## Adım 5 – Hepsini Bir Araya Getirin ve Programı Çalıştırın

Aşağıda, her şeyi birleştiren tam, çalıştırılabilir Java sınıfı yer alıyor. `JsonExportDemo.java` (ya da istediğiniz başka bir ad) olarak kaydedin ve IDE'nizden ya da komut satırından çalıştırın.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.output.*;

public class JsonExportDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply your Aspose OCR license (replace with your actual license file)
        License ocrLicense = new License();
        ocrLicense.setLicense("Aspose.OCR.lic"); // <-- adjust path if needed

        // 2️⃣ Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Prepare the input image that contains the text to be recognized
        OcrInput ocrInput = new OcrInput();
        // Replace with the absolute or relative path to your receipt PNG
        ocrInput.add("YOUR_DIRECTORY/receipt.png"); // <-- **extract text from PNG** here

        // 4️⃣ Perform recognition and request the result in JSON format
        OcrResult ocrResult = ocrEngine.recognize(ocrInput, ResultFormat.JSON);

        // 5️⃣ Retrieve the JSON string from the result
        String jsonResult = ocrResult.getJson();

        // 6️⃣ Output the JSON (or save it to a file for further processing)
        System.out.println(jsonResult);
    }
}
```

### Beklenen Çıktı

Programı çalıştırdığınızda aşağıdakine benzer bir JSON dizesi yazdırılır (içerik makbuzunuza bağlı olarak değişir):

```json
{
  "pages": [
    {
      "lines": [
        {
          "text": "Store Name",
          "confidence": 0.99,
          "boundingBox": [12, 34, 200, 45]
        },
        {
          "text": "Date: 2024-02-15",
          "confidence": 0.98,
          "boundingBox": [12, 60, 180, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.97,
          "boundingBox": [12, 120, 150, 45]
        }
      ]
    }
  ]
}
```

Artık bu JSON'u bir veritabanına, bir REST uç noktasına ya da bir veri‑analiz hattına besleyebilirsiniz. **convert receipt to JSON** adımı zaten sizin için tamamlanmış durumda.

## Yaygın Sorular ve Kenar Durumları

### Görüntü döndürülmüşse ne olur?

Aspose OCR hafif döndürmeleri otomatik olarak algılar ve düzeltir. Şiddetli eğik görüntüler için tanımadan önce `engine.getImagePreprocessingOptions().setDeskew(true)` çağırın.

### Birden fazla dili nasıl yönetirim?

İstediğiniz dili ayarlamak için `engine.getLanguage()` kullanın, örneğin `engine.setLanguage(Language.FRENCH)`. Bu, **recognize text from image** içeren çok dilli makbuzlarla çalışırken işe yarar.

### JSON yerine düz metin çıkışı alabilir miyim?

Kesinlikle. `ResultFormat.JSON` yerine `ResultFormat.TEXT` kullanın ve `result.getText()` çağırın.

### OCR'yi belirli bir bölgeyle sınırlamanın bir yolu var mı?

Evet—`ocrInput.add(imagePath, new Rectangle(x, y, width, height))` kullanarak sadece makbuz alanına odaklanın; bu hız ve doğruluğu artırabilir.

## Üretim‑Hazır OCR için Pro İpuçları

- **Cache the license** nesnesini, bir döngü içinde çok sayıda dosya işliyorsanız saklayın; sürekli oluşturmak ek yük getirir.  
- **Batch process**: tüm makbuz yollarını tek bir `OcrInput` içine yükleyin ve `recognize` metodunu bir kez çağırın. JSON, her sayfanın kendi satırlarını içeren bir dizi barındırır.  
- **Validate JSON**: dizeyi aldıktan sonra Jackson gibi bir kütüphane ile ayrıştırarak iyi biçimlendirilmiş olduğundan emin olun, ardından depolayın.  
- **Monitor confidence**: JSON, satır başına bir `confidence` alanı içerir. 0.85 gibi bir eşik altında kalan satırları filtreleyerek hatalı veriyi önleyin.  
- **Secure your license**: `Aspose.OCR.lic` dosyasını güvenli bir kasada ya da ortam değişkeninde saklayın, özellikle bulut dağıtımlarında.

## Sonuç

**how to use OCR**'ı Java’da **recognize text from image**, **extract text from PNG** makbuzları ve **convert receipt to JSON** yapmak için kapsamlı, uçtan uca bir örnekle ele aldık. Adımlar basit, kod tamamen çalıştırılabilir ve JSON çıktısı, herhangi bir downstream sistem için hazır yapılandırılmış bir temsil sunar.

Sonraki adımda daha gelişmiş senaryoları keşfedebilirsiniz: JSON'u gerçek‑zamanlı işleme için Apache Kafka'ya beslemek, satır‑item toplamlarını çekmek için regex desenleri uygulamak ya da ölçeklenebilirlik için bir bulut OCR hizmetiyle bütünleştirmek. Ne seçerseniz seçin, yeni öğrendiğiniz temeller aynı kalacak.

Sorularınız mı var, yoksa deneme sırasında bir sorun mu yaşadınız? Aşağıya yorum bırakın, birlikte çözümleyelim. Mutlu kodlamalar, ve o dağınık makbuz görüntülerini temiz, aranabilir verilere dönüştürmenin tadını çıkarın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}