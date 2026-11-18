---
category: general
date: 2026-03-26
description: Aspose.OCR Java kullanarak aranabilir PDF oluşturun – görüntü OCR'sını
  yüklemeyi, birincil dili ayarlamayı, görüntüden metin çıkarmayı ve OCR PDF'sini
  kaydetmeyi öğrenin.
draft: false
keywords:
- create searchable pdf
- set primary language
- extract text from image
- load image ocr
- save ocr pdf
language: tr
og_description: Aspose.OCR Java ile aranabilir PDF oluşturun. Görüntüyü OCR ile yükleme,
  birincil dili ayarlama, görüntüden metin çıkarma ve OCR PDF'sini kaydetme adım adım
  rehberi.
og_title: Aspose.OCR ile Aranabilir PDF Oluşturma – Java Rehberi
tags:
- Aspose.OCR
- Java
- PDF
- OCR
title: Aspose.OCR ile Aranabilir PDF Oluşturma – Java Rehberi
url: /tr/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.OCR ile Aranabilir PDF Oluşturma – Java Rehberi

Tarama belgesinden **create searchable pdf** oluşturmanız gerektiğinde nereden başlayacağınızı bilemediniz mi? Yalnız değilsiniz—birçok geliştirici Java’da OCR ile ilk kez uğraştığında bu engelle karşılaşıyor. İyi haber şu ki, Aspose.OCR tüm süreci—bir görüntüyü yüklemekten, birincil dili ayarlamaya ve sonunda OCR‑destekli bir PDF kaydetmeye—oldukça sorunsuz hâle getiriyor. Bu öğreticide **extracts text from image** yapan, **set primary language** ayarlamanıza izin veren ve herhangi bir okuyucuda açabileceğiniz bir **save OCR pdf** ile biten tam, çalıştırılabilir bir örnek üzerinden ilerleyeceğiz.

Ayrıca, daha hızlı işleme için GPU hızlandırmasını etkinleştirme ve karışık‑dil belgelerini (bizim örneğimizde Tamil + English) işleme gibi birkaç pratik ipucunu da ele alacağız. Sonunda, projenize ekleyebileceğiniz sağlam, üretim‑hazır bir kod parçacığına sahip olacaksınız.

## Gereksinimler

- **Java 17** (veya herhangi bir yeni JDK; Aspose.OCR Java 8+ destekler)
- **Aspose.OCR for Java** kütüphanesi (resmi siteden indirin veya Maven ile ekleyin)
- Bir **license file** (veya 30‑günlük deneme sürümü)
- Metin içeren bir görüntü dosyası (demo `sample-mixed-tamil-eng.jpg` kullanır)

Ekstra çerçeve yok, yerel bağımlılık yok—sadece saf Java ve Aspose.JAR'lar.

---

## Adım 1: Aranabilir PDF Oluşturma – Projeyi Kurma

Koda girmeden önce, projenin **create searchable pdf** dosyaları oluşturmak için hazır olduğundan emin olalım.

```bash
# Maven dependency (add to pom.xml)
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check the latest version -->
</dependency>
```

> **Pro tip:** Sürüm numarasını güncel tutun; yeni sürümler genellikle GPU kullanımı için performans düzeltmeleri içerir.

Şimdi `RecentFeaturesDemo` adlı basit bir Java sınıfı oluşturun. Bu sınıf, **load image OCR** yapmak, dil ayarlarını yapılandırmak ve sonunda **save OCR pdf** gerçekleştirmek için gereken tüm mantığı tutacak.

---

## Adım 2: Görüntüyü OCR ile Yükleme ve Motoru Başlatma

İş akışındaki ilk gerçek adım **load image OCR** yapmaktır. Bu, Aspose.OCR'a hangi dosyanın analiz edileceğini söyler.

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // 2️⃣ Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Enable GPU acceleration – speeds up recognition dramatically
        ocrEngine.getEngineSettings().setUseGpu(true);
        // Use all available CPU cores for parallel processing
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);
```

> **Neden önemli:** GPU'yu etkinleştirmek (`setUseGpu(true)`) modern donanımlarda işleme süresini %70'e kadar azaltabilir, paralel işleme ise GPU meşgulken CPU'nun boşta kalmamasını sağlar.

---

## Adım 3: Birincil Dili Ayarlama (ve İkincil Bir Dil)

Bu adımı atlayarsanız, Aspose.OCR dili tahmin etmeye çalışır; bu daha yavaş ve daha az doğru olur. İşte **set primary language**'ı Tamil olarak ayarlayıp İngilizceyi yedek olarak eklemenin yolu.

```java
        // 3️⃣ Define languages – primary is Tamil, secondary is English
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English);
```

> **Explanation:** Birincil dil, tanıma sırasında kullanılan karakter seti ve sözlüğü etkiler. İkincil dil eklemek, karışık‑yazı belgeleri için kritiktir (örneğin hem Tamil hem İngilizce metin içeren bir fiş düşünün).  
> **Edge case:** Belgenizde iki dilden fazla dil varsa, her ek dil için `addAdditionalLanguage(...)` metodunu çağırabilirsiniz.

---

## Adım 4: Görüntüyü Ön‑işleme – Eğrilik Düzeltme ve Gürültü Azaltma

Tarama görüntüleri genellikle döndürme veya arka plan gürültüsü sorunları yaşar. Ön‑işleme, OCR motorunun **extract text from image** işlemini daha güvenilir hâle getirir.

```java
        // 4️⃣ Pre‑processing options
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // auto‑rotate tilted pages
                 .setDenoise(true); // suppress speckles and background patterns
```

> **İpucu:** Görüntünün zaten temiz olduğunu biliyorsanız, birkaç milisaniye tasarruf etmek için `setDenoise(true)`'ı atlayabilirsiniz.

---

## Adım 5: Görüntü Dosyasını Yükleme

Motor hazır olduğuna göre, analiz etmek istediğimiz dosyayı ona gösteriyoruz.

```java
        // 5️⃣ Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

> **Yol yanlış olursa ne olur?** Aspose.OCR net bir `FileNotFoundException` fırlatır. Daha nazik bir hata yönetimi için çağrıyı bir try‑catch bloğuna sarabilirsiniz.

---

## Adım 6: OCR Çalıştırma ve Görüntüden Metin Çıkarma

Her şey yapılandırıldıktan sonra, tanıma işlemini gerçekten çalıştırma zamanı. Bu adım hem **extract text from image** yapar hem de PDF oluşturmak için gereken verileri hazırlar.

```java
        // 6️⃣ Perform recognition
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Print the raw OCR output – handy for debugging
            System.out.println("Recognized text:");
            System.out.println(recognizedText);
```

Demo görüntüsü için tipik konsol çıktısı şu şekildedir:

```
வணக்கம் World
This is a mixed language sample.
```

Tamil satırının doğru şekilde, ardından İngilizce'nin çıktığını göreceksiniz. Bu, **set primary language**'ı doğru ayarlamanın karşılığıdır.

---

## Adım 7: OCR PDF Kaydetme – Son Parça

Bulmacanın son parçası **save OCR pdf** işlemidir. Aspose.OCR, orijinal görüntünün üzerine görünmez bir metin katmanı ekleyerek PDF'yi aranabilir hâle getirir.

```java
            // 7️⃣ (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

`searchable.pdf` dosyasını Adobe Reader'da açın, **Ctrl + F** tuşlarına basın ve hem Tamil hem de İngilizce kelimeleri arayabilirsiniz—tam da bir **create searchable pdf** iş akışının vaat ettiği şey.

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır)

Aşağıda olduğu gibi derleyip doğrudan çalıştırabileceğiniz tam program yer alıyor. Yer tutucu yolları kendi dizinlerinizle değiştirin.

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // Step 2: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getEngineSettings().setUseGpu(true);                     // enable CUDA GPU acceleration
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);     // use multiple CPU cores
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);      // primary language
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English); // secondary language
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // correct image rotation
                 .setDenoise(true); // reduce background noise

        // Step 3: Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 4: Run OCR and obtain the plain‑text result
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Step 5: (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("Recognized text:");
            System.out.println(recognizedText);
            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

Şu şekilde çalıştırın:

```bash
javac -cp "path/to/aspose-ocr.jar" RecentFeaturesDemo.java
java -cp ".:path/to/aspose-ocr.jar" RecentFeaturesDemo
```

Konsola çıkarılan metni göreceksiniz, ardından **searchable pdf**'in diske yazıldığına dair bir onay mesajı alacaksınız.

---

## Yaygın Sorular ve Kenar Durumları

### **load image OCR**'ı bir bayt dizisinden almam gerekirse ne yapmalıyım?

`ImageStream.fromFile(imagePath)` ifadesini `ImageStream.fromBytes(byteArray)` ile değiştirebilirsiniz. Bu, görüntünün bir veritabanı ya da web servisinden geldiği durumlarda kullanışlıdır.

### Zaten görüntü içeren PDF'leri nasıl işleyebilirim?

Aspose.OCR doğrudan PDF sayfaları üzerinde çalışabilir: `ocrEngine.setDocument(PdfDocument.fromFile("input.pdf"))`. Motor, tanımadan önce her sayfayı dahili olarak rasterleştirir.

### GPU'm algılanmadı—`setUseGpu(true)`'ı tutmalı mıyım?

`setUseGpu(true)` başarısız olursa, Aspose.OCR otomatik olarak CPU'ya geçer. Etkinleştirmeden önce `ocrEngine.getEngineSettings().isGpuAvailable()` ile kontrol edebilirsiniz.

### **save OCR pdf**'i özel meta verilerle kaydedebilir miyim?

Evet. Tanıma sonrasında, `save` çağrısından önce `ocrEngine.getPdfSaveOptions().setTitle("My Document")` ya da `setAuthor("John Doe")` kullanarak özel meta veriler ekleyebilirsiniz.

---

## Büyük Partiler İçin Performans İpuçları

- **Batch processing:** Birden çok görüntüde aynı `OcrEngine` örneğini yeniden kullanın. Çalıştırmalar arasında sadece `ocrEngine.clear()` çağırın.
- **Thread pool:** Her görüntü görevini bir `Callable` içinde sarın ve bir `ExecutorService`'e gönderin. Paralel işleme etkin olduğu için her iş parçacığı çok çekirdekli kullanımından fayda sağlar.
- **Memory management:** Gigapiksel görüntüler için RAM kullanımını makul tutmak amacıyla `ocrEngine.getPreprocessingSettings().setResizeFactor(0.5)` ile ölçek küçültmeyi düşünün.

---

## Sonuç

Aspose.OCR for Java kullanarak tam bir **create searchable pdf** iş akışını adım adım inceledik. **load image OCR** ile başlayarak, biz

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}