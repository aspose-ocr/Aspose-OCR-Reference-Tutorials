---
category: general
date: 2026-02-22
description: Aspose kullanarak çok dilli OCR gerçekleştirme ve görüntü dosyalarından
  metin çıkarma—OCR için görüntüyü nasıl yükleyeceğinizi öğrenin ve OCR'ı görüntü
  üzerinde verimli bir şekilde çalıştırın.
draft: false
keywords:
- how to use aspose
- multi language ocr
- extract text from image
- load image for ocr
- run ocr on image
language: tr
og_description: Aspose kullanarak birden fazla dildeki görüntülerde OCR çalıştırma
  – OCR için görüntüyü yükleme ve görüntüden metin çıkarma adım adım rehberi.
og_title: Java'da Çok Dilli OCR için Aspose Nasıl Kullanılır
tags:
- Aspose
- OCR
- Java
title: Java'da Çok Dilli OCR için Aspose Nasıl Kullanılır
url: /tr/java/advanced-ocr-techniques/how-to-use-aspose-for-multi-language-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose ile Çok Dilli OCR'yi Java'da Nasıl Kullanılır

Resminizde aynı anda İngilizce, Ukraynaca ve Arapça metin bulunduğunda **Aspose'u nasıl kullanacağınızı** hiç merak ettiniz mi? Tek başınıza değilsiniz—birçok geliştirici, *görüntüden metin çıkarma* işlemini tek dilli olmayan dosyalarla yapmaya çalışırken bu engelle karşılaşıyor.  

Bu öğreticide, **OCR için resmi yükleme**, *çok dilli OCR* etkinleştirme ve sonunda **görüntüde OCR çalıştırma** adımlarını gösteren, çalıştırılmaya hazır tam bir örnek üzerinden ilerleyeceğiz. Belirsiz referanslar yok, sadece somut kod ve her satırın ardındaki mantık var.

## Öğrenecekleriniz

- Aspose OCR kütüphanesini bir Java projesine ekleme (Maven veya Gradle).
- OCR motorunu doğru şekilde başlatma.
- Motoru *çok dilli OCR* için yapılandırma ve otomatik algılamayı etkinleştirme.
- Karışık betik içeren bir resmi yükleme.
- Tanıma işlemini yürütme ve **görüntüden metin çıkarma**.
- Desteklenmeyen diller veya eksik dosyalar gibi yaygın sorunları ele alma.

Bu adımları tamamladığınızda, herhangi bir projeye ekleyebileceğiniz ve anında görüntü işlemeye başlayabileceğiniz bağımsız bir Java sınıfına sahip olacaksınız.

---

## Ön Koşullar

Başlamadan önce şunların olduğundan emin olun:

| Gereksinim | Neden Önemli |
|-------------|----------------|
| Java 8 ve üzeri | Aspose OCR, Java 8+ hedefler. |
| Maven veya Gradle (herhangi bir yapı aracı) | Aspose OCR JAR dosyasını otomatik olarak çekmek için. |
| Karışık‑dilli metin içeren bir görüntü dosyası (ör. `mixed_script.jpg`) | **OCR için resmi yükleme** işlemini burada yapacağız. |
| Geçerli bir Aspose OCR lisansı (isteğe bağlı) | Lisans olmadan su işareti eklenmiş çıktı alırsınız, ancak kod aynı şekilde çalışır. |

Hepsi hazır mı? Harika—başlayalım.

---

## Adım 1: Aspose OCR'yi Projenize Ekleyin

### Maven

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- latest as of Feb 2026 -->
</dependency>
```

### Gradle

```groovy
// build.gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

> **İpucu:** Sürüm numarasına dikkat edin; yeni sürümler dil paketleri ve performans iyileştirmeleri ekler.

Bağımlılığı eklemek, **Aspose'u nasıl kullanacağınız** konusundaki ilk somut adımdır—kütüphane, daha sonra ihtiyaç duyacağımız `OcrEngine`, `OcrInput` ve `OcrResult` sınıflarını getirir.

---

## Adım 2: OCR Motorunu Başlatın

```java
import com.aspose.ocr.*;

public class MultiLangOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2.1: Create the OCR engine – the core object that does all the heavy lifting.
        OcrEngine engine = new OcrEngine();

        // Step 2.2: (Optional) Apply your license to avoid watermarks.
        // engine.setLicense("Aspose.Total.lic");
```

**Neden Önemli:**  
`OcrEngine`, tanıma algoritmalarını kapsüller. Bu adımı atlayınca, daha sonra *görüntüde OCR çalıştırma* için bir nesneye sahip olmazsınız ve `NullPointerException` ile karşılaşırsınız.

---

## Adım 3: Çok‑Dilli Desteği ve Otomatik Algılamayı Yapılandırın

```java
        // Step 3.1: Tell the engine which languages you expect.
        engine.setRecognitionLanguages(new String[] { "en", "uk", "ar" });

        // Step 3.2: Enable automatic language detection – crucial for mixed‑script images.
        engine.setAutoDetectLanguage(true);
```

**Açıklama:**  
- `"en"` = İngilizce, `"uk"` = Ukraynaca, `"ar"` = Arapça.  
- Otomatik algılama, Aspose'un resmi taramasını, her segmentin hangi dile ait olduğunu belirlemesini ve doğru OCR modelini uygulamasını sağlar. Bunu kapatırsanız üç ayrı tanıma çalıştırmak zorunda kalırsınız—hem zahmetli hem de hata eğilimli.

---

## Adım 4: OCR için Resmi Yükleyin

```java
        // Step 4.1: Prepare an OcrInput container.
        OcrInput input = new OcrInput();

        // Step 4.2: Add the image file. Replace the path with your actual location.
        input.add("YOUR_DIRECTORY/mixed_script.jpg");
```

> **Neden `OcrInput` kullanıyoruz:** Birden fazla sayfa veya görüntüyü tutabilir, böylece *OCR için resmi yükleme* işlemini ileride toplu modda da yapabilirsiniz.

Dosya bulunamazsa Aspose `FileNotFoundException` fırlatır. `if (!new File(path).exists())` gibi bir kontrol, hata ayıklama sürenizi kısaltır.

---

## Adım 5: Görüntüde OCR Çalıştırın

```java
        // Step 5.1: Execute the recognition process.
        OcrResult result = engine.recognize(input);
```

Bu noktada motor resmi analiz eder, dil bloklarını tespit eder ve tanınan metni içeren bir `OcrResult` nesnesi üretir.

---

## Adım 6: Görüntüden Metin Çıkarın ve Görüntüleyin

```java
        // Step 6.1: Pull the plain text out of the result.
        String extractedText = result.getText();

        // Step 6.2: Print it to the console – you could also write it to a file.
        System.out.println("=== Extracted Text ===");
        System.out.println(extractedText);
    }
}
```

**Gördükleriniz:**  
`mixed_script.jpg` içinde “Hello мир مرحبا” varsa, konsol çıktısı şöyle olur:

```
=== Extracted Text ===
Hello мир مرحبا
```

Bu, **Aspose'u nasıl kullanacağınız** konusunda çoklu dillerle *görüntüden metin çıkarma* işleminin tam çözümüdür.

---

## Kenar Durumları ve Yaygın Sorular

### Bir dil tanınmazsa ne olur?

Aspose yalnızca kendi OCR modelleriyle gelen dilleri destekler. Örneğin Japonca’ya ihtiyacınız varsa, `setRecognitionLanguages` içine `"ja"` ekleyin. Model mevcut değilse motor varsayılan (genellikle İngilizce) modele geri döner ve bozuk karakterler elde edersiniz.

### Düşük çözünürlüklü görüntülerde doğruluğu nasıl artırabilirim?

- Görüntüyü ön‑işleme (DPI artırma, ikilileştirme) yapın.  
- `engine.setResolution(300)` ile motorun beklenen DPI değerini belirtin.  
- Döndürülmüş taramalar için `engine.setPreprocessOptions(OcrEngine.PreprocessOptions.AutoRotate)` etkinleştirin.

### Bir klasördeki tüm görüntüleri işleyebilir miyim?

Kesinlikle. `input.add()` çağrısını, bir dizindeki tüm dosyalar üzerinde dönen bir döngüye yerleştirin. Aynı `engine.recognize(input)` çağrısı, her sayfa için birleştirilmiş metin döndürür.

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

```java
import com.aspose.ocr.*;

public class MultiLangOcrDemo {
    public static void main(String[] args) throws Exception {

        // Create the OCR engine
        OcrEngine engine = new OcrEngine();

        // Optional: apply your license to avoid watermarks
        // engine.setLicense("Aspose.Total.lic");

        // Configure languages (English, Ukrainian, Arabic) and enable auto‑detect
        engine.setRecognitionLanguages(new String[] { "en", "uk", "ar" });
        engine.setAutoDetectLanguage(true);

        // Load the image that contains mixed‑language text
        OcrInput input = new OcrInput();
        input.add("YOUR_DIRECTORY/mixed_script.jpg"); // <-- replace with your path

        // Run the recognition process
        OcrResult result = engine.recognize(input);

        // Print the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(result.getText());
    }
}
```

Bunu `MultiLangOcrDemo.java` olarak kaydedin, `javac` ile derleyin ve `java MultiLangOcrDemo` ile çalıştırın. Her şey doğru kurulduysa, tanınan metin konsola yazdırılacaktır.

---

## Sonuç

**Aspose'u nasıl kullanacağınız** konusunu baştan sona ele aldık: kütüphaneyi eklemek, *çok dilli OCR* yapılandırmak, **OCR için resmi yükleme**, **görüntüde OCR çalıştırma** ve sonunda **görüntüden metin çıkarma**. Yaklaşım ölçeklenebilir—daha fazla dil kodu ekleyin ya da bir dosya listesi besleyin, dakikalar içinde sağlam bir OCR hattına sahip olacaksınız.

Sırada ne var? Şu fikirleri deneyin:

- **Toplu işleme:** Bir klasör üzerinde döngü kurup her sonucu ayrı bir `.txt` dosyasına yazın.  
- **Son‑işleme:** Çıktıyı temizlemek için regex ya da NLP kütüphaneleri kullanın (gereksiz satır sonlarını kaldırma, yaygın OCR hatalarını düzeltme).  
- **Entegrasyon:** OCR adımını bir Spring Boot REST uç noktasına bağlayarak diğer servislerin görüntü gönderip JSON‑kodlu metin almasını sağlayın.

Deney yapmaktan, hatalar üretmekten ve ardından düzeltmekten çekinmeyin—bu, Aspose ile OCR konusunda gerçekten uzmanlaşmanın yoludur. Herhangi bir sorunla karşılaşırsanız, aşağıya yorum bırakın. Kodlamanın tadını çıkarın!  

---

![aspose OCR kullanımını gösteren ekran görüntüsü](/images/aspose-ocr-demo.png){alt="aspose OCR kullanımını gösteren ekran görüntüsü"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}