---
category: general
date: 2026-04-29
description: Aspose OCR kullanarak Java'da görüntüden metin tanıma – faturadan metin
  nasıl çıkarılır, OCR için görüntü nasıl yüklenir ve dakikalar içinde bir Java OCR
  eğitimine hâkim olun.
draft: false
keywords:
- recognize text from image
- extract text from invoice
- load image for ocr
- java ocr tutorial
language: tr
og_description: Java'da Aspose OCR ile görüntüden metin tanıma. Bu rehber, faturadan
  metin çıkarma, OCR için görüntü yükleme ve bir Java OCR öğreticisini tamamlama adımlarını
  size gösterir.
og_title: Java'da görüntüden metin tanıma – Tam OCR Eğitimi
tags:
- OCR
- Java
- Aspose
title: Java’da Görüntüden Metin Tanıma – Tam OCR Öğreticisi
url: /tr/java/ocr-basics/recognize-text-from-image-in-java-complete-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüden Metin Tanıma Java’da – Tam OCR Öğreticisi

Görüntüden **metin tanıma** ihtiyacı hiç duydunuz mu ama hangi Java kütüphanesinin bu işi yapacağından emin değildiniz? Yalnız değilsiniz. Birçok geliştirici, taranmış faturalar veya makbuzlardan veri çekmeye çalışırken aynı duvara çarpıyor.  

Bu rehberde, Aspose OCR kullanarak **görüntüden metin tanıma**, **faturadan metin çıkarma** dosyalarını ve temiz bir **java ocr tutorial** içinde **OCR için görüntü yükleme** nasıl yapılacağını adım adım göstereceğiz. Sonunda, düzeltilmiş metni doğrudan konsola yazdıran çalıştırılabilir bir programınız olacak—hiçbir gizem, eksik parça yok.

## Gereksinimler

- **Java Development Kit (JDK) 8+** – kod standart Java API'lerini kullanır.
- **Aspose.OCR for Java** JAR (sürüm 23.9 veya daha yeni). Aspose Maven deposundan alın ya da resmi siteden ZIP'i indirin.
- Test etmek istediğiniz bir **fatura görüntüsü** (JPEG, PNG, TIFF) – ona `invoice.jpg` diyelim.
- Favori IDE'niz (IntelliJ, Eclipse, VS Code) – herhangi biri çalışır.

Hepsi bu. Ekstra framework yok, karmaşık yapı araçları yok. Maven'ınız varsa sadece Aspose bağımlılığını ekleyin; aksi takdirde JAR'ı sınıf yolunuza bırakın.

İlk olarak, yeni bir Maven projesi oluşturun (ya da isterseniz basit bir klasör). Aspose OCR bağımlılığını `pom.xml` dosyasına ekleyin:

```xml
<!-- pom.xml -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.9</version>
        <classifier>jdk17</classifier> <!-- adjust if you use a different JDK -->
    </dependency>
</dependencies>
```

Maven kullanmıyorsanız, `aspose-ocr-23.9.jar` dosyasını `libs/` klasörünüze koyun ve derlerken sınıf yoluna ekleyin.

> **Pro ipucu:** Maven, geçişli bağımlılıkları otomatik olarak yönetir, böylece ileride “class not found” hatalarından kurtulursunuz.

## Adım 1 – Projenizi Kurun ve Aspose OCR'yi İçe Aktarın

Kütüphane hazır olduğuna göre, **OCR için görüntüyü yükleyelim**. Bu adım çok önemlidir çünkü motorun okuyabileceği bir akışa ihtiyacı vardır. Düşük seviyeli `FileInputStream`i soyutlayan Aspose'un `ImageStream.fromFile` yardımcı metodunu kullanacağız.

```java
import com.aspose.ocr.*;

public class SpellCheckTutorial {
    public static void main(String[] args) throws Exception {

        // Step 2: Load the image you want to process
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.jpg"));
```

> **Neden önemli:** Uygun bir görüntü akışı sağlamak, OCR motorunun görüntünün boş olduğunu düşündüğü sessiz hataları önler.

## Adım 2 – Motorun Hangi Dili Bekleyeceğini Belirtin

Metnin dilini motora söylediğinizde OCR doğruluğu büyük ölçüde artar. Çoğu fatura için İngilizce yeterli olur.

```java
        // Step 3: Specify the language (English)
        ocrEngine.getLanguageSettings().setLanguage("en");
```

Çok dilli bir grup işlemek isterseniz, sadece `"en"` yerine `"fr"` ya da `"de"` koyun—Aspose 40'tan fazla dili destekler.

## Adım 3 – Yazım Düzeltmeyi Açın (Gerçek Büyü)

Aspose OCR, yerleşik bir yazım‑düzeltme modülü ile gelir. Bunu etkinleştirmek, “AcmeCprp”yi “AcmeCorp”a dönüştürmeye yardımcı olur; bu, faturalardaki şirket adları için özellikle kullanışlıdır.

```java
        // Step 4: Enable spell correction
        ocrEngine.getPostProcessingSettings().setEnableSpellCorrection(true);
```

> **Köşe durumu:** Belgeleriniz çok fazla alan‑spesifik jargon içeriyorsa, bu terimleri özel bir sözlüğe (sonraki adım) eklemek isteyeceksiniz. Aksi takdirde, varsayılan sözlük onları yanlış “düzeltme” yapabilir.

## Adım 4 – Sözlüğe Özel Kelimeler Ekleyin

**Faturadan metin çıkarma** işlemi yapalım; içinde özel bir şirket adı ve `Invoice#` gibi bir etiket olsun. Bunları özel sözlüğe eklemek, yazım‑düzelticinin onları dokunmadan bırakmasını sağlar.

```java
        // Step 5: Add custom words so the spell‑corrector knows them
        ocrEngine.getPostProcessingSettings()
                 .getCustomDictionary()
                 .add("AcmeCorp")
                 .add("Invoice#");
```

Gösterildiği gibi `.add()` çağrılarını zincirleyebilir ya da tekrarlayarak çağırabilirsiniz. Sözlük, `OcrEngine` örneği yaşamı boyunca var olur, bu yüzden ihtiyacınız kadar giriş ekleyebilirsiniz.

## Adım 5 – OCR'yi Çalıştırın ve Tanınan Metni Yazdırın

Son olarak, `recognize()` metodunu çağırın ve sonucu çıktı olarak verin. Dönen `OcrResult`, ham metni ve gerekirse daha sonra kullanabileceğiniz güven skorlarını içerir.

```java
        // Step 6: Perform OCR and display the spell‑corrected text
        OcrResult ocrResult = ocrEngine.recognize();
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

### Beklenen Çıktı

`invoice.jpg` dosyasının aşağıdaki satırı içerdiğini varsayalım:

```
AcmeCorp
Invoice# 2024-04-01
Total: $1,250.00
```

Şuna benzer bir çıktı görmelisiniz:

```
=== Recognized Text ===
AcmeCorp
Invoice# 2024-04-01
Total: $1,250.00
```

Eğer yazım‑düzeltme kapalı olsaydı, “AcmeCprp” almış olabilirdiniz—özel sözlüğümüz bunu engelledi.

## Tam Çalışan Örnek

Aşağıda, `SpellCheckTutorial.java` dosyasına kopyalayıp yapıştırmaya hazır tam program yer alıyor. `"YOUR_DIRECTORY/invoice.jpg"` ifadesini test görüntünüzün mutlak yolu ile değiştirin.

```java
import com.aspose.ocr.*;

public class SpellCheckTutorial {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.jpg"));

        // Step 3: Set the language (English)
        ocrEngine.getLanguageSettings().setLanguage("en");

        // Step 4: Enable the built‑in spell correction
        ocrEngine.getPostProcessingSettings().setEnableSpellCorrection(true);

        // Step 5: Add custom dictionary entries
        ocrEngine.getPostProcessingSettings()
                 .getCustomDictionary()
                 .add("AcmeCorp")
                 .add("Invoice#");

        // Step 6: Run OCR and print the result
        OcrResult ocrResult = ocrEngine.recognize();
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Şununla çalıştırın:

```bash
javac -cp "libs/*" SpellCheckTutorial.java
java -cp ".:libs/*" SpellCheckTutorial
```

Temizlenmiş fatura metninin konsola yazdırıldığını göreceksiniz.

## Sık Sorulan Sorular & Dikkat Edilmesi Gerekenler

### Görüntü bulanıktıysa ne olur?

Kaynak görüntünün düşük kontrastı veya gürültüsü olduğunda OCR doğruluğu düşer. Görüntüyü OpenCV gibi bir kütüphane ile ön‑işlemden geçirin: kontrastı artırın, medyan bulanıklığı uygulayın veya Aspose'a göndermeden önce siyah‑beyaz dönüştürün. `setImage` metodu bir `BufferedImage` kabul eder, böylece önce onu manipüle edebilirsiniz.

### PDF'leri doğrudan işleyebilir miyim?

Evet. Aspose OCR, PDF sayfalarını dahili olarak görüntü olarak okuyabilir. Sadece `ocrEngine.setImage(ImageStream.fromFile("file.pdf"))` çağırın. Motor, her sayfayı rasterleştirip OCR'yi çalıştırır. Büyük PDF'lerde bellek tüketimine dikkat edin.

### Her kelime için güven skorlarını nasıl alırım?

`OcrResult`, `getWords()` metodunu sunar ve bu metod `OcrWord` nesnelerinin bir koleksiyonunu döndürür. Her kelimenin `getConfidence()` metodu (0‑100) vardır. Düşük güvenilirlikli satırları manuel inceleme için işaretlemeniz gerekiyorsa, bunlar üzerinde döngü kurabilirsiniz.

```java
for (OcrWord word : ocrResult.getWords()) {
    System.out.println(word.getText() + " – confidence: " + word.getConfidence());
}
```

### Birçok faturayı toplu işlemek için bir yol var mı?

Kesinlikle. Yukarıdaki kodu, bir klasördeki görüntüler üzerinde dönen bir `for` döngüsü içinde sarın. Her seferinde yerel kütüphaneleri yeniden başlatma yükünden kaçınmak için aynı `OcrEngine` örneğini yeniden kullanmayı unutmayın.

## Sorunsuz bir java ocr tutorial Deneyimi İçin Pro İpuçları

- **Motoru yeniden kullanın**: Dosya başına yeni bir `OcrEngine` oluşturmak maliyetlidir. Bir kez örnekleyin, görüntüyü değiştirin ve `recognize()` metodunu tekrar tekrar çağırın.
- **Bellek yönetimi**: Büyük bir görüntüyü işledikten sonra `ocrEngine.dispose()` çağırın ya da motorun kapsam dışı kalmasına izin vererek yerel kaynakları serbest bırakın.
- **İş parçacığı güvenliği**: `OcrEngine` **thread‑safe** değildir. Paralel işleme ihtiyacınız varsa, her iş parçacığı için ayrı bir motor oluşturun.
- **Özel sözlük boyutu**: Binlerce giriş eklemek yazım‑düzeltmeyi yavaşlatabilir. Sözlüğü hafif tutun—sadece faturalarınızda gerçekten görülen terimleri ekleyin.

## Sonuç

Artık Aspose'un yazım‑düzeltme yeteneklerini kullanarak **görüntüden metin tanıma**, **OCR için görüntü yükleme** ve **faturadan metin çıkarma** nasıl yapılır gösteren somut, uçtan uca bir **java ocr tutorial**'a sahipsiniz. Örnek kod çalıştırmaya hazır, açıklamalar her adımın “nedenini” kapsıyor ve ipuçları karşılaşabileceğiniz yaygın sorunları ele alıyor.

What’s next? Try expanding the solution:

- Parse the recognized text into structured fields (

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}