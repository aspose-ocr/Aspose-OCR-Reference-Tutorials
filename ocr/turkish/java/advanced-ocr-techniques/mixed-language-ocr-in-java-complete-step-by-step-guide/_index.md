---
category: general
date: 2026-07-05
description: Java geliştiricileri için çok dilli OCR öğreticisi. Çok dilli OCR örneğiyle
  görüntülerden OCR metni alarak Java projelerinde metne dönüştürmeyi öğrenin.
draft: false
keywords:
- mixed language OCR
- get OCR text
- image to text Java
- java OCR example
- multi language OCR
language: tr
og_description: Java'da karışık dil OCR'ı açıklandı. Çok dilli OCR örneğiyle görüntülerden
  OCR metni alın; bugün kopyala‑yapıştır yapabilirsiniz.
og_title: Java'da Karışık Dil OCR – Tam Programlama Rehberi
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Mixed language OCR tutorial for Java developers. Learn how to get OCR
    text from images to text Java projects with a multi language OCR example.
  headline: Mixed Language OCR in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Mixed language OCR tutorial for Java developers. Learn how to get OCR
    text from images to text Java projects with a multi language OCR example.
  name: Mixed Language OCR in Java – Complete Step‑by‑Step Guide
  steps:
  - name: 1. Create a Maven Project
    text: 'Open a terminal and run:'
  - name: 2. Add the Aspose.OCR Dependency
    text: 'Edit the generated `pom.xml` and insert the following inside the `<dependencies>`
      block:'
  - name: How It Works
    text: '| Step | What Happens | Why It Matters | |------|--------------|----------------|
      | **1** | `OcrEngine` object is created. | The engine encapsulates all OCR functionality;
      without it you can’t call any methods. | | **2** | `setRecognitionLanguage`
      receives `ENGLISH` and `MALAYALAM`. | Supplying both'
  - name: Low‑Quality Images
    text: 'If the image is blurry or has poor contrast, OCR accuracy drops dramatically.
      Consider these remedies:'
  - name: Unsupported Languages
    text: Aspose currently supports over 70 scripts, but Malayalam may require a language
      pack. If `RecognitionLanguage.MALAYALAM` throws an exception, download the additional
      language data from Aspose’s portal and place it in `resources/ocr-data`.
  - name: Large PDFs
    text: When processing multi‑page PDFs, feed each page as a separate image or use
      `OcrEngine.recognizePdf`. The same `setRecognitionLanguage` call applies to
      every page, giving you a seamless **multi language OCR** experience across a
      whole document.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Java'da Karışık Dil OCR – Tam Adım Adım Kılavuz
url: /tr/java/advanced-ocr-techniques/mixed-language-ocr-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da Karışık Dil OCR – Tam Adım‑Adım Kılavuz

Hiç **mixed language OCR**'a ihtiyaç duydunuz ama Java'da nasıl yapacağınızı bilemediniz mi? Tek başınıza değilsiniz. İngilizce ve Malayalam arasında geçiş yapan eski belgeleri dijitalleştiriyor olun ya da birden fazla betiği destekleyen bir tarayıcı uygulaması geliştiriyor olun, zorluk gerçektir. Bu öğreticide, her iki dili içeren bir bitmap'ten **get OCR text**'i nasıl alacağınızı, öz bir **image to text Java** iş akışıyla göstereceğiz.

Hazır‑hazır **java OCR example** üzerinden adım adım ilerleyecek, her satırın neden önemli olduğunu açıklayacak ve **multi language OCR**'ın inceliklerini ele alacağız, böylece yaygın tuzaklardan kaçınabilirsiniz. Sonunda, çıkarılan metni konsola yazdıran çalışan bir programınız olacak – açıklanmayan gizemli kütüphaneler kalmayacak.

## İhtiyacınız Olanlar

* **Java Development Kit (JDK) 17** veya daha yeni – kod modern modül sistemini kullanıyor ancak JDK 11+ üzerinde de çalışır.  
* **Maven** (veya Gradle) – OCR kütüphanesini otomatik olarak çekmek için.  
* Birden fazla dili destekleyen bir OCR motoru – bu kılavuzda **Aspose.OCR for Java**'ı kullanacağız, bu motor kutudan çıkar çıkmaz İngilizce ve Malayalam desteği sunar. (Tesseract'ı tercih ederseniz, adımlar benzerdir; sadece import ifadelerini değiştirin.)  
* Projenizin içinde `resources` adlı bir klasöre yerleştirilmiş `mixed_english_malayalam.png` adlı örnek bir resim.  
* Biraz merak – geri kalan aşağıda ele alınmıştır.

> **Pro tip:** Windows kullanıyorsanız, Maven'in PATH'te olduğunu doğrulamak için bir Komut İstemi'nden `mvn -v` çalıştırın.

## Projeyi Kurma

### 1. Maven Projesi Oluşturun

Open a terminal and run:

```bash
mvn archetype:generate -DgroupId=com.example.ocr \
    -DartifactId=mixed-ocr-demo -DarchetypeArtifactId=maven-archetype-quickstart \
    -DinteractiveMode=false
```

Bu, standart `src/main/java` düzenine sahip temel bir Java projesi oluşturur.

### 2. Aspose.OCR Bağımlılığını Ekleyin

Edit the generated `pom.xml` and insert the following inside the `<dependencies>` block:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- latest as of July 2026 -->
</dependency>
```

Run `mvn clean install` to download the JARs. Maven will handle everything, so you won’t need to hunt down native DLLs.

## Karışık Dil OCR Kodunu Yazma

Create a new class `MixedLanguageOcrDemo.java` under `src/main/java/com/example/ocr/` and paste the complete code below. Every line is commented so you can see **why** we do what we do.

```java
package com.example.ocr;

import com.aspose.ocr.*;
import com.aspose.ocr.recognition.*;

public class MixedLanguageOcrDemo {

    public static void main(String[] args) {
        // Step 1: Initialise the OCR engine – this is the entry point for all operations.
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Tell the engine which languages to look for.
        // We pass both English and Malayalam; the engine will automatically switch
        // between scripts as it encounters them.
        ocrEngine.setRecognitionLanguage(
                RecognitionLanguage.ENGLISH,
                RecognitionLanguage.MALAYALAM);

        // Step 3: Load the image that contains mixed text.
        // Using a relative path keeps the example portable across machines.
        String imagePath = "resources/mixed_english_malayalam.png";

        // Optional: improve accuracy on low‑resolution scans.
        // Uncomment the next line if your image is under 300 DPI.
        // ocrEngine.setResolution(300);

        // Step 4: Perform the actual OCR operation.
        RecognitionResult result = ocrEngine.recognizeImage(imagePath);

        // Step 5: Extract the plain text – this is the "get OCR text" part.
        String extractedText = result.getText();

        // Step 6: Output the result to the console.
        System.out.println("=== Extracted Text ===");
        System.out.println(extractedText);
    }
}
```

### Nasıl Çalışır

| Adım | Ne Olur | Neden Önemli |
|------|--------------|----------------|
| **1** | OcrEngine nesnesi oluşturulur. | Motor, tüm OCR işlevselliğini kapsüller; olmadan hiçbir yöntemi çağıramazsınız. |
| **2** | `setRecognitionLanguage` `ENGLISH` ve `MALAYALAM` alır. | Her iki dili sağlamak **multi language OCR**'ı etkinleştirir; motor betik değişikliklerini anında algılar. |
| **3** | Görsel yolu tanımlanır. | Yolun göreceli tutulması, mutlak konumları sabitlemekten kaçınır ve **java OCR example**'ı yeniden kullanılabilir kılar. |
| **4** | `recognizeImage` bitmap'i işler. | Ağır işin burada gerçekleştiği yerdir – motor pikselleri analiz eder, sinir ağlarını çalıştırır ve bir `RecognitionResult` döndürür. |
| **5** | `getText()` düz metni çıkarır. | Bu, **get OCR text**'i daha sonraki işlem (örn. DB'ye kaydetme) için ihtiyaç duyduğunuz tam yöntemdir. |
| **6** | `System.out.println` dizeyi yazdırır. | Anında görsel geri bildirim, **image to text Java** hattının çalıştığını doğrulamanıza yardımcı olur. |

> **Not:** `java.lang.UnsatisfiedLinkError` ile karşılaşırsanız, yerel kütüphane klasörünün `java.library.path` içinde olduğundan emin olun. Aspose, Windows, macOS ve Linux için gerekli ikili dosyaları sağlar.

## Demoyu Çalıştırma

Compile and execute with Maven:

```bash
mvn compile exec:java -Dexec.mainClass="com.example.ocr.MixedLanguageOcrDemo"
```

You should see output similar to:

```
=== Extracted Text ===
Welcome to the conference.
സ്വാഗതം
```

İlk satır İngilizce, ikinci satır Malayalam – **mixed language OCR**'ımızın başarılı olduğunu gösterir.

## Yaygın Kenar Durumlarını Ele Alma

### Düşük Kaliteli Görseller

If the image is blurry or has poor contrast, OCR accuracy drops dramatically. Consider these remedies:

* **Ön‑işlem** yapın; OpenCV gibi bir kütüphane ile resmi gri tonlamaya dönüştürün, adaptif eşikleme uygulayın ve en az 300 DPI'ye yükseltin.  
* Dönen metni düzeltmek için `ocrEngine.setAutoSkewCorrection(true)`'ı etkinleştirin.  
* Daha katı güven eşiği için `ocrEngine.setConfidenceThreshold(0.6f)` değerini artırın.

### Desteklenmeyen Diller

Aspose şu anda 70'ten fazla betiği destekliyor, ancak Malayalam bir dil paketi gerektirebilir. `RecognitionLanguage.MALAYALAM` bir istisna fırlatırsa, Aspose portalından ek dil verilerini indirip `resources/ocr-data` içine yerleştirin.

### Büyük PDF'ler

Çok sayfalı PDF'leri işlerken, her sayfayı ayrı bir resim olarak besleyin veya `OcrEngine.recognizePdf` kullanın. Aynı `setRecognitionLanguage` çağrısı her sayfaya uygulanır, böylece tüm belge boyunca kesintisiz bir **multi language OCR** deneyimi elde edersiniz.

## Örneği Genişletmek: Konsoldan Web Servisine

If you want to expose this functionality via a REST endpoint, add Spring Boot:

```java
@RestController
@RequestMapping("/api/ocr")
public class OcrController {

    @PostMapping(value = "/extract", consumes = MediaType.MULTIPART_FORM_DATA_VALUE)
    public String extractText(@RequestParam("file") MultipartFile file) throws IOException {
        OcrEngine engine = new OcrEngine();
        engine.setRecognitionLanguage(RecognitionLanguage.ENGLISH, RecognitionLanguage.MALAYALM);
        // Save multipart file to a temporary location
        Path temp = Files.createTempFile("upload-", ".png");
        Files.write(temp, file.getBytes());
        RecognitionResult res = engine.recognizeImage(temp.toString());
        return res.getText();
    }
}
```

Şimdi herhangi bir istemci bir resmi `POST` edebilir ve **get OCR text** sonucunu düz JSON olarak alabilir. Bu küçük genişletme, aynı **java OCR example**'ın tek‑dosyalı demodan üretime hazır bir servise nasıl ölçeklendiğini gösterir.

## Tam Kaynak Ağacı Görüntüsü

```
mixed-ocr-demo/
├─ pom.xml
└─ src/
   └─ main/
      ├─ java/
      │  └─ com/example/ocr/
      │     └─ MixedLanguageOcrDemo.java
      └─ resources/
         └─ mixed_english_malayalam.png
```

Makaledeki tüm proje yapısının bulunması, okuyucuların yapıyı IDE'lerine kopyalayıp anında çalıştırmasını kolaylaştırır.

![karışık dil OCR örnek çıktısı](https://example.com/assets/mixed-ocr-output.png "karışık dil OCR örnek çıktısı")

*Görsel alt metni:* karışık dil OCR örnek çıktısı – aynı resimden çıkarılan İngilizce ve Malayalam metni gösterir.

## Özet & Sonraki Adımlar

We’ve covered a **mixed language OCR** pipeline in Java from start to finish:

* Maven projesi kuruldu ve Aspose OCR bağımlılığı eklendi.  
* Motor İngilizce + Malayalam için yapılandırıldı, tanıma gerçekleştirildi ve **got OCR text** alındı.  
* Görsel kalitesi, dil paketleri ve konsol uygulamasını web servisine dönüştürme konuları tartışıldı.

If you’re ready to push further, try these ideas:

* Aspose'u **Tesseract** ile değiştirerek açık kaynak motorunun **multi language OCR**'ı nasıl yönettiğini görün.  
* Hindi veya Tamil gibi ek dillerle deney yapın – sadece `setRecognitionLanguage`'a ekleyin.  
* Sonucu bir arama indeksine (örn. Elasticsearch) entegre ederek taranmış arşivlerde **image to text Java** destekli aramayı etkinleştirin.

Beklediğiniz gibi çalışmayan bir şey olursa yorum bırakmaktan çekinmeyin ya da kendi düzenlemelerinizi paylaşın. Kodlamanın tadını çıkarın ve taramalarınız her zaman kristal‑net olsun!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Metin Görsellerini Çıkar – Aspose.OCR for Java ile OCR Temelleri](/ocr/english/java/ocr-basics/)
- [Aspose.OCR Kullanarak Dil ile Görsel Metni OCR Nasıl Yapılır](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Aspose OCR ile Metin Görselini Tanıma – Tam Java OCR Öğreticisi](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}