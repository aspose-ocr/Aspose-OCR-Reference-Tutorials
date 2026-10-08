---
category: general
date: 2026-01-07
description: Java'da bir görüntüden aranabilir PDF oluşturun. Görüntüyü PDF'ye dönüştürmeyi,
  görüntüden metin çıkarmayı ve Aspose OCR kullanarak PNG'den metin tanımayı öğrenin.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- image to searchable pdf
- recognize text from png
language: tr
og_description: Aspose OCR ile Java’da aranabilir PDF oluşturun. Bu kılavuz, görüntüyü
  PDF’ye dönüştürmeyi, görüntüden metin çıkarmayı ve PNG’den metin tanımayı gösterir.
og_title: PNG'den Aranabilir PDF Oluştur – Java Öğreticisi
tags:
- OCR
- Java
- PDF
title: PNG'den Aranabilir PDF Oluşturma – Tam Java Rehberi
url: /tr/java/ocr-operations/create-searchable-pdf-from-png-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNG'den Aranabilir PDF Oluşturma – Tam Java Rehberi

Tarama resminden **create searchable pdf** oluşturmanız gerektiğinde ama nereden başlayacağınızı bilemediğiniz oldu mu? Tek başınıza değilsiniz—geliştiriciler belge‑yönetimi boru hatları oluştururken sürekli bu engelle karşılaşıyor. İyi haber? Birkaç Java satırı ve Aspose OCR ile **convert image to pdf** yapabilir, gizli metin ekleyebilir ve tamamen aranabilir bir belge elde edebilirsiniz.

Bu öğreticide tüm süreci adım adım göstereceğiz: bir PNG'yi yüklemek, OCR çalıştırmak ve sonucu aranabilir bir PDF olarak kaydetmek. Sonuna geldiğinizde **extract text from image** dosyalarından metin çıkarabilecek, bunları **image to searchable pdf** varlıklarına dönüştürebilecek ve hatta çok sayfalı TIFF gibi kenar durumlarını da yönetebileceksiniz. Hiçbir harici hizmet yok, sadece bugün çalıştırabileceğiniz saf Java kodu.

## Aranabilir PDF Oluşturma – Genel Bakış

Koda dalmadan önce, “searchable PDF”nin gerçekte ne anlama geldiğini açıklayalım. Aranabilir bir PDF iki katmandan oluşur:

1. **Visible image layer** – orijinal resim (PNG, JPEG vb.).
2. **Hidden text layer** – görüntünün arkasında duran, belgeyi herhangi bir PDF görüntüleyicide aranabilir kılan OCR‑tarafından oluşturulan metin.

Neden ikisine de ihtiyacımız var? Görüntü orijinal görünümü korurken, metin katmanı kopyala‑yapıştır, indeksleme ve tam metin aramayı mümkün kılar. Bu, arşivleme, yasal uyumluluk ve aranabilir arşivler oluşturma için ideal noktadır.

## Adım 1: Java Projenizde Aspose OCR'ı Kurun

İlk olarak—Aspose OCR kütüphanesine ihtiyacınız var. En basit yol Maven bağımlılığını eklemektir:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

Maven kullanmıyorsanız, Aspose web sitesinden JAR dosyasını indirip sınıf yolunuza ekleyin. **Pro tip:** kütüphane sürümünü Java çalışma zamanınızla (Java 8+ sorunsuz çalışır) uyumlu tutun.

### Neden Önemli

Aspose OCR, kutudan çıkar çıkmaz çok çeşitli görüntü formatlarını ve dilleri destekler, böylece kendi piksel‑işleme kodunuzu yazmanız gerekmez. Ayrıca daha sonra aranabilir PDF oluşturmak için kullanacağımız `OcrOutputFormat.PDF` enum'ını sağlar.

## Adım 2: İşlemek İstediğiniz Görüntüyü Yükleyin

Sonra, OCR motoruna hangi dosyayı okuyacağını söylememiz gerekiyor. API, bir dosya yolu, bir `java.io.InputStream` veya hatta bir bayt dizisinden oluşturulabilen bir `ImageStream` kabul eder.

```java
import com.aspose.ocr.*;

public class PdfOutputExample {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the PNG (or any supported image) from disk
        String inputPath = "YOUR_DIRECTORY/input.png"; // replace with your actual path
        ocrEngine.setImage(ImageStream.fromFile(inputPath));
```

`ImageStream.fromFile` kullandığımıza dikkat edin. Bir akıştan **convert image to pdf** yapmanız gerekirse (örneğin, yüklenmiş bir dosya), bu çağrıyı `ImageStream.fromInputStream(yourInputStream)` ile değiştirebilirsiniz.

### Kenar Durumu Uyarısı

Görseliniz 10 MB'den büyükse, önce ölçeklendirmeyi düşünün. Büyük görseller OCR süresini önemli ölçüde artırır ve düşük kapasiteli sunucularda bellek dışı hatalarına yol açabilir.

## Adım 3: OCR'ı Çalıştırın ve Sonucu Yakalayın

Şimdi sihir gerçekleşir. `recognize()` çağrısı OCR algoritmasını çalıştırır ve tanınan metin ile düzen bilgilerini içeren bir `OcrResult` nesnesi döndürür.

```java
        // Perform OCR recognition
        OcrResult ocrResult = ocrEngine.recognize();

        // Optional: print extracted text to console (useful for debugging)
        System.out.println("Extracted Text:");
        System.out.println(ocrResult.getText());
```

Burada ayrıca **extract text from image** yapıyor ve çıktısını alıyoruz. Bu adım, PDF oluşturmadan sadece ham metne ihtiyacınız olduğunda kullanışlıdır. Aynı `ocrResult` nesnesi daha sonra aranabilir PDF oluşturmak için yeniden kullanılır.

### Neden Bu Adım Kritik

OCR motoru sadece karakterleri okumakla kalmaz, aynı zamanda konumlarını da korur; bu, son PDF'deki gizli metin katmanını mümkün kılar. Bu adımı atlamak, aranabilirlik özelliğini kaybetmek anlamına gelir.

## Adım 4: Sonucu Aranabilir PDF Olarak Kaydedin

Son olarak, Aspose OCR'a çıktıyı PDF formatında yazmasını söylüyoruz. `save` metodu hedef dosya adını ve bir `OcrOutputFormat` enum'ını alır.

```java
        // Save the OCR result as a searchable PDF (image + hidden text layer)
        String outputPath = "YOUR_DIRECTORY/output.pdf"; // replace with your desired output
        ocrResult.save(outputPath, OcrOutputFormat.PDF);

        System.out.println("Searchable PDF created at: " + outputPath);
    }
}
```

`output.pdf` dosyasını Adobe Reader veya herhangi bir modern PDF görüntüleyicide açtığınızda, orijinal PNG'yi göreceksiniz, ancak görüntüde yer alan herhangi bir kelimeyi de arayabilirsiniz. Bu, **create searchable pdf**'nin özüdür.

### İhtiyacınız Olabilecek Varyasyonlar
- **Multiple pages:** Çok sayfalı bir TIFF'iniz varsa, her sayfayı döngüye alıp, her biri için `ocrEngine.setImage` çağırın ve kaydetmeden önce sonuçları aynı `OcrResult`'a ekleyin.
- **Different languages:** `recognize()` çağırmadan önce `ocrEngine.getLanguage().setLanguage(OcrLanguage.FRENCH);` (veya desteklenen herhangi bir dil) kullanın.
- **Custom DPI:** Bulanık taramalar için, `ocrEngine.getImage().setResolution(300);` ayarlayarak doğruluğu artırabilirsiniz.

## Adım 5: Çıktıyı Doğrulayın (Ne Beklenir)

Program çalıştıktan sonra `output.pdf` dosyasını kontrol edin:

1. **Visual layer:** PDF, sağladığınız tam PNG'yi gösterir.
2. **Text layer:** `Ctrl+F` (veya Cmd+F) tuşlarına basıp, görüntüde bulunduğunu bildiğiniz bir kelimeyi arayın. Anında bulunmalıdır.
3. **Copy‑paste:** Bir paragrafı seçip bir metin editörüne kopyalamayı deneyin; temiz, aranabilir bir metin elde edeceksiniz.

Arama başarısız olursa, görüntünün çok düşük çözünürlükte olmadığını veya doğru dilin ayarlandığını iki kez kontrol edin. Çoğu zaman basit bir DPI artırması sorunu çözer.

## Yaygın Sorular & Pro İpuçları

- **Do I need a license?**  
  Aspose OCR, bir filigranla deneme modunda çalışır. Üretim için bir lisans satın alın ve `License license = new License(); license.setLicense("Aspose.OCR.lic");` kodu ile ayarlayın.

- **Can I **convert image to pdf** without OCR?**  
  Evet—`recognize()`'den önce `ocrEngine.setRecognizeText(false);` ile `OcrOutputFormat.PDF` kullanın. Bu, sadece görüntü içeren bir PDF verir.

- **What if I want only the extracted text?**  
  `save` çağrısını atlayın ve `ocrResult.getText()` kullanın; bunu bir `.txt` dosyasına yazabilir veya bir arama indeksine besleyebilirsiniz.

- **Performance tip:**  
  Birden fazla görüntü için aynı `OcrEngine` örneğini yeniden kullanın; bu, başlatma yükünü azaltır.

## Tam Çalışan Örnek (Hepsi Bir Arada)

Aşağıda eksiksiz, çalıştırmaya hazır Java programı yer alıyor. Yer tutucu yolları kendi dizinlerinizle değiştirin, Maven bağımlılığını ekleyin ve hazırsınız.

```java
import com.aspose.ocr.*;

public class PdfOutputExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the image (PNG, JPG, TIFF, etc.)
        String inputPath = "YOUR_DIRECTORY/input.png"; // <-- change this
        ocrEngine.setImage(ImageStream.fromFile(inputPath));

        // 3️⃣ Run OCR to get text and layout
        OcrResult ocrResult = ocrEngine.recognize();

        // Optional: display extracted text in console
        System.out.println("Extracted Text:");
        System.out.println(ocrResult.getText());

        // 4️⃣ Save as searchable PDF (image + hidden text layer)
        String outputPath = "YOUR_DIRECTORY/output.pdf"; // <-- change this
        ocrResult.save(outputPath, OcrOutputFormat.PDF);

        System.out.println("Searchable PDF created at: " + outputPath);
    }
}
```

**Expected output:**  
```
Extracted Text:
[...the plain text that was recognized from the PNG...]
Searchable PDF created at: YOUR_DIRECTORY/output.pdf
```

`output.pdf` dosyasını herhangi bir PDF görüntüleyicide açın ve çıkarılan metinden bir kelimeyi aramayı deneyin—vurgulanmış olarak görmelisiniz, bu da **create searchable pdf** işlemini başarıyla gerçekleştirdiğinizi doğrular.

## Sonuç

Size Java ve Aspose OCR kullanarak bir PNG'den **create searchable pdf** oluşturmayı gösterdik. Adımlar basittir: kütüphaneyi kurun, görüntüyü yükleyin, OCR'ı çalıştırın ve sonucu PDF olarak kaydedin. Bu süreçte ayrıca **convert image to pdf**, **extract text from image** ve daha gelişmiş senaryolar için **recognize text from png** nasıl yapılır da öğrendiniz.

Sırada ne var? Tarama faturalarından oluşan bir toplu işleme döngüsü oluşturun, gizli metni tam metin araması için bir veritabanına kaydedin veya farklı diller ve görüntü ön işleme teknikleriyle deneyler yapın. Aynı desen diğer formatlarda da çalışır—giriş dosyasını değiştirmeniz yeterli, böylece **image to searchable pdf**'yi kısa sürede yapabilirsiniz.

Sorularınız mı var ya da bir sorunla mı karşılaştınız? Aşağıya yorum bırakın, iyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}