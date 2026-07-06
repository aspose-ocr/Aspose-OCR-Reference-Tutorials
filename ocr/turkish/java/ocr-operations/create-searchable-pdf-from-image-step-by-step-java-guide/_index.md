---
category: general
date: 2026-05-06
description: Aspose OCR kullanarak bir görüntüden aranabilir PDF oluşturun. Görüntüyü
  PDF'ye dönüştürmeyi, görüntüyü OCR ile PDF'ye çevirmeyi ve görüntüden metin çıkarmayı
  dakikalar içinde öğrenin.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- ocr image to pdf
- extract text from image
- convert jpg to searchable pdf
language: tr
og_description: Aspose OCR ile bir görüntüden aranabilir PDF oluşturun. JPG'yi aranabilir
  PDF'ye dönüştürmek, görüntüden metin çıkarmak ve daha fazlası için bu kılavuzu izleyin.
og_title: Görüntüden Aranabilir PDF Oluşturma – Tam Java Öğreticisi
tags:
- Java
- OCR
- PDF
- Aspose
title: Görüntüden Aranabilir PDF Oluşturma – Adım Adım Java Rehberi
url: /tr/java/ocr-operations/create-searchable-pdf-from-image-step-by-step-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüden Aranabilir PDF Oluşturma – Tam Java Öğreticisi

Tarayıcıdan bir fotoğrafla **create searchable PDF** oluşturmanız gerektiğinde ama hangi kütüphaneyi seçeceğinizi bilemediğiniz oldu mu? Yalnız değilsiniz. Birçok projede—gider raporu otomasyonu ya da dijital arşivleme gibi—düz bir görüntüyü gerçekten arayabileceğiniz bir PDF'ye dönüştürme yeteneği oyunu değiştiren bir özelliktir.

Bu yüzden bu öğreticide **convert image to PDF** sürecinin tamamını adım adım gösterecek, üzerine OCR çalıştıracak ve herhangi bir belge iş akışına ekleyebileceğiniz bir **searchable PDF** elde edeceğiz. Ayrıca **extract text from image** konusuna değinecek ve **convert jpg to searchable pdf** işlemini çok fazla kalıp kodu olmadan nasıl yapacağınızı göstereceğiz.

## Öğrenecekleriniz

- Aspose OCR için ihtiyacınız olan tam Maven/Gradle bağımlılığını.
- Bir JPG'yi (veya desteklenen herhangi bir görüntüyü) OCR motoruna nasıl yükleyeceğinizi.
- `OcrSaveFormat.PDF_SEARCHABLE` ile kaydetmenin neden önemli olduğunu.
- Ortak tuzaklar (büyük görüntüler, desteklenmeyen formatlar) ve bunlardan nasıl kaçınılacağını.
- Oluşturulan PDF'in gerçekten aranabilir metin içerdiğini nasıl doğrulayacağınızı.

Bu rehberin sonunda, tek bir metod çağrısıyla aranabilir bir PDF üreten, çalıştırmaya hazır bir Java sınıfına sahip olacaksınız. Harici komut satırı araçları yok, ekstra OCR motorları yok—sadece saf Java.

---

## Önkoşullar

| Gereksinim | Neden Önemli |
|-------------|----------------|
| Java 8 or newer | Aspose OCR modern dil özelliklerini kullanır. |
| Maven or Gradle (for dependency management) | Aspose OCR JAR'ını çekmeyi çok basit hale getirir. |
| A sample image (`input.jpg`) placed in a known folder | Kod bir dosya yolu bekler; PNG, BMP vb. ile değiştirebilirsiniz. |
| Optional: a PDF viewer with search capability (Adobe Reader, Foxit, etc.) | PDF'in gerçekten aranabilir olduğunu doğrulamak için. |

Eğer bunlara zaten sahipseniz, harika—hadi başlayalım.

---

## Adım 1: Aspose OCR'yi Projenize Ekleyin

### Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check Maven Central for the latest -->
</dependency>
```

### Gradle

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

> **Pro tip:** Ücretsiz değerlendirme sürümü ilk sayfaya küçük bir filigran ekler. Üretim için, Aspose'tan bir lisans alın ve `OcrEngine`'i örneklemeden önce `License license = new License(); license.setLicense("Aspose.OCR.lic");` kodunu çalıştırın.

---

## Adım 2: Dönüştürmek İstediğiniz Görüntüyü Yükleyin

`ImageStream.fromFile`'ı kullanarak görüntüyü doğrudan diskte okuyacağız. Bu yöntem JPG, PNG, TIFF ve birçok diğer formatı destekler, böylece kaynağa bakılmaksızın **convert image to PDF** yapabilirsiniz.

```java
// Step 2: Load the source image that contains the text
String inputPath = "YOUR_DIRECTORY/input.jpg"; // replace with your actual path
ocrEngine.setImage(ImageStream.fromFile(inputPath));
```

> **Bu adım neden?** OCR motoru metnin bitmap temsiline ihtiyaç duyar. Yüksek çözünürlüklü bir görüntü (300 dpi veya daha yüksek) sağlamak tanıma doğruluğunu büyük ölçüde artırır, bu da size daha iyi **extract text from image** sonuçları verir.

---

## Adım 3: OCR'yi Çalıştırın ve Aranabilir PDF Olarak Kaydedin

Sihir, `save` metodunu `PDF_SEARCHABLE` formatı ile çağırdığınızda gerçekleşir. Aspose OCR, orijinal görüntünün üzerine yerleştirilen gizli bir metin katmanı oluşturur ve statik bir resmi **searchable PDF**'ye dönüştürür.

```java
// Step 3: Recognize the text and embed it into a searchable PDF
String outputPath = "YOUR_DIRECTORY/searchable.pdf";
ocrEngine.save(outputPath, OcrSaveFormat.PDF_SEARCHABLE);
```

Gizli katman olmadan düz bir PDF tercih ediyorsanız, `PDF_SEARCHABLE` yerine `PDF` kullanın. Ancak çoğu arşivleme senaryosunda, istediğiniz şey aranabilir versiyondur.

---

## Adım 4: Sonucu Doğrulayın

Program tamamlandıktan sonra, `searchable.pdf` dosyasını herhangi bir PDF görüntüleyicide açın ve yerleşik aramayı (Ctrl + F) deneyin. Görüntüde yalnızca bulunan kelimeleri bulabiliyorsanız, tebrikler—başarıyla **ocr image to pdf** yaptınız.

```java
System.out.println("Searchable PDF created at: " + outputPath);
```

> **Köşe durum:** Çok büyük görüntüler (> 10 MB) `OutOfMemoryError` oluşturabilir. Bunu azaltmak için, görüntüyü önceden `java.awt.Image` veya Thumbnailator gibi bir kütüphane kullanarak küçültün.

---

## Tam Çalışan Örnek

Aşağıda tam ve bağımsız bir Java sınıfı bulunmaktadır. IDE'nize kopyalayıp yapıştırın, yolları ayarlayın ve çalıştırın—ekstra adım gerekmez.

```java
import com.aspose.ocr.*;

public class ImageToSearchablePdf {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the source image (JPG, PNG, etc.)
        //    Replace YOUR_DIRECTORY with the folder that holds your image.
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));

        // 3️⃣ Perform OCR and save as a searchable PDF
        //    The PDF will contain the original image plus a hidden text layer.
        ocrEngine.save("YOUR_DIRECTORY/searchable.pdf", OcrSaveFormat.PDF_SEARCHABLE);

        // 4️⃣ Simple console feedback
        System.out.println("Searchable PDF created.");
    }
}
```

**Beklenen çıktı:**  

```
Searchable PDF created.
```

`YOUR_DIRECTORY/searchable.pdf` dosyasını açtığınızda, `input.jpg` içinde yer alan herhangi bir kelimeyi arayabilmelisiniz. Bu, **convert jpg to searchable pdf**'nin özüdür.

---

## Sıkça Sorulan Sorular (SSS)

### Birden fazla görüntüyü aynı anda işleyebilir miyim?
Evet. Dosya yolu listesini döngüye alın, her biri için `setImage` çağırın ve ya tek bir PDF'ye sayfalar ekleyin (`PDF_SEARCHABLE`) ya da ayrı PDF'ler oluşturun. Yinelemeler arasında motor durumunu sıfırlamayı unutmayın (`ocrEngine.clear()`).

### OCR doğruluğu düşük olursa ne yapmalıyım?
- Kaynak görüntünün en az 300 dpi olduğundan emin olun.
- `ocrEngine.getConfig().setLanguage(OcrLanguage.ENGLISH);` kullanarak dili kilitleyin.
- Görüntüyü (eğikliği düzeltme, kontrast artırma) OpenCV gibi bir kütüphane ile ön işleme tabi tutun.

### Aspose OCR diğer dilleri destekliyor mu?
Kesinlikle. `OcrLanguage` enum'ı Fransızca, Almanca, Çince, Arapça ve daha birçok dili içerir. `save` çağırmadan önce dili değiştirin.

### Aranabilir PDF'i mevcut bir belgeye nasıl gömebilirim?
Çıktıyı normal bir PDF gibi ele alın. Diğer PDF'lerle birleştirmek için bir PDF birleştirici kütüphane (ör. iText veya Aspose PDF) kullanın.

---

## Saha İpuçları ve Püf Noktaları

- **Pro tip:** Küçük bir dosya boyutu istiyorsanız, kaydetmeden önce `ocrEngine.getConfig().setCompress(true);` çağırın.
- **Dikkat edin:** Şeffaf arka planlı görüntüler—Aspose OCR şeffaflığı beyaz olarak değerlendirir, bu da kontrasti etkileyebilir.
- **Unutmayın:** Aranabilir PDF hâlâ altında bir raster görüntüdür. Tamamen vektör tabanlı bir PDF'ye ihtiyacınız varsa, yerleşimi manuel olarak yeniden oluşturmanız gerekir.

---

## Sonuç

Aspose OCR kullanarak Java'da görüntülerden **create searchable PDF** dosyaları oluşturmak için ihtiyacınız olan her şeyi ele aldık. Maven bağımlılığını eklemekten gizli metin katmanını doğrulamaya kadar süreç basit ve tamamen programlanabilir. Artık **convert image to pdf**, **ocr image to pdf** ve hatta **extract text from image** işlemlerini IDE'nizin konforundan çıkmadan yapabilirsiniz.

Bir sonraki adıma hazır mısınız? Tar scanned receipt'lerin bulunduğu bir klasörü toplu işleyin ya da bu iş akışını bir bulut depolama tetikleyicisi (AWS Lambda, Azure Functions) ile birleştirerek belge alım hatlarını otomatikleştirin. Olasılıklar sonsuz—devam edin ve deneyin!

Eğer herhangi bir sorunla karşılaşırsanız veya geliştirme önerileriniz varsa, aşağıya yorum bırakın. Mutlu kodlamalar!  

![Diagram showing the flow: image → OCR engine → searchable PDF](image-placeholder.png "create searchable pdf flowchart")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}