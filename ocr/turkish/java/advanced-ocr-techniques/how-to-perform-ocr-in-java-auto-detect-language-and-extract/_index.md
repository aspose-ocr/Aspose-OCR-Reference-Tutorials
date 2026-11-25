---
category: general
date: 2026-04-26
description: Aspose OCR kullanarak OCR nasıl yapılır ve görüntüden metin nasıl çıkarılır
  öğrenin. Bu kılavuz, OCR için görüntünün nasıl yükleneceğini, otomatik dil algılamanın
  nasıl etkinleştirileceğini ve dilin otomatik olarak algılanmasını gösterir.
draft: false
keywords:
- how to perform OCR
- extract text from image
- load image for OCR
- enable automatic language detection
- auto detect language OCR
language: tr
og_description: Aspose OCR ile Java’da OCR nasıl yapılır. OCR için görüntüyü nasıl
  yükleyeceğinizi, otomatik dil algılamayı nasıl etkinleştireceğinizi ve görüntüden
  metin çıkarmayı öğrenin.
og_title: Java'da OCR Nasıl Yapılır – Otomatik Dil Algılama
tags:
- OCR
- Java
- Aspose
title: Java’da OCR Nasıl Yapılır – Dili Otomatik Algıla ve Metni Çıkar
url: /tr/java/advanced-ocr-techniques/how-to-perform-ocr-in-java-auto-detect-language-and-extract/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java’da OCR Nasıl Yapılır – Otomatik Dil Algılama ve Metin Çıkarma

Bir fotoğrafta İngilizce, İspanyolca ve belki biraz Japonca karakterlerin karıştığını **OCR nasıl yapılır** diye merak ettiniz mi? Tek başınıza değilsiniz—geliştiriciler, uygulamalarının taranmış belgeler, makbuzlar veya çok dilli işaretlerden metin okuması gerektiğinde bu engelle sık sık karşılaşıyor.  

İyi haber? Birkaç satır Java ve Aspose OCR ile **görüntüyü OCR için yükleyebilir**, **otomatik dil algılamayı etkinleştirebilir** ve dili önceden tahmin etmeden anında **görüntüden metin çıkarabilirsiniz**. Bu öğreticide tam çalışan örneği adım adım inceleyecek, her adımın neden önemli olduğunu açıklayacak ve **otomatik dil algılamalı OCR** sonucunu nasıl doğrulayacağınızı göstereceğiz.

> **Edinecekleriniz**  
> * Karışık‑dilli bir PNG dosyasını okuyan çalışan bir Java programı.  
> * Dil algılamayı zahmetsiz hâle getiren temel OCR ayarları bilgisi.  
> * Eksik dosyalar, desteklenmeyen diller ve performans ayarlarıyla başa çıkma ipuçları.

---

## Önkoşullar

Başlamadan önce şunların olduğundan emin olun:

| Gereksinim | Neden Önemli |
|------------|--------------|
| Java 17 (veya daha yeni) | Aspose OCR modern JVM’leri hedefler; eski sürümler API özelliklerini kaçırabilir. |
| Aspose OCR for Java kütüphanesi (en son sürüm) | `OcrEngine` ve dil‑otomatik‑algılama yeteneklerini sağlar. |
| En az iki dil içeren bir görüntü dosyası (`mixed_lang.png`) | **otomatik dil algılamalı OCR** özelliğini gösterir. |
| Bir Java IDE’si veya basit komut‑satırı ortamı | Örnek kodu derleyip çalıştırmak için. |

Aspose OCR JAR dosyasını henüz indirmediyseniz, resmi Maven deposundan alın:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- replace with the latest -->
</dependency>
```

---

## Adım 1: OCR Motoru Örneğini Oluşturma – OCR Nasıl Yapılır

**OCR yapmak** istediğinizde ilk yaptığınız şey motoru örneklemektir. `OcrEngine`i, bitmap’i analiz edip pikselleri karaktere dönüştüren beyin olarak düşünün.

```java
// Step 1: Initialize the OCR engine
import com.aspose.ocr.*;

public class AutoDetectDemo {
    public static void main(String[] args) throws Exception {

        // Create a fresh OcrEngine object – this is where the magic starts
        OcrEngine ocrEngine = new OcrEngine();
```

> **Pro ipucu:** Aynı `OcrEngine`i birden çok görüntüde yeniden kullanmak, motorun dil modellerini dahili olarak önbelleğe alması sayesinde performansı artırabilir.

---

## Adım 2: Otomatik Dil Algılamayı Etkinleştirme – Enable Automatic Language Detection

Varsayılan olarak Aspose OCR İngilizceyi varsayar. Çok dilli resimler için her metin bloğu başına “dil tahmini” yapmasını söylemeniz gerekir. İşte **otomatik dil algılamayı etkinleştirme** bayrağının yaptığı şey.

```java
        // Step 2: Turn on auto‑language detection for each region
        ocrEngine.getRecognitionSettings()
                 .setLanguage(OcrLanguage.AUTO_DETECT);
```

Neden önemli: Motor artık görüntünün her segmentini inceler, en olası dili seçer ve doğru karakter setini uygular. Bunu yapmazsanız İngilizce dışı bölümler bozuk çıkacaktır.

---

## Adım 3: Görüntüyü OCR İçin Yükleme – Load Image for OCR

Şimdi gerçekten **görüntüyü OCR için yüklüyoruz**. Yol mutlak ya da göreli olabilir; dosyanın var olduğundan emin olun, aksi takdirde `FileNotFoundException` alırsınız.

```java
        // Step 3: Point the engine at the image that contains mixed‑language text
        ocrEngine.setImage("YOUR_DIRECTORY/mixed_lang.png");
```

> **Köşe durumu:** Görüntünüz bir Maven projesinin resources klasöründeyse, sabit yolları önlemek için `getClass().getResource("/mixed_lang.png")` kullanın.

---

## Adım 4: Tanıma Çalıştırma ve Görüntüden Metin Çıkarma – Extract Text from Image

Motor yapılandırıldı ve resim yüklendi, şimdi **OCR’i gerçekten çalıştırma** zamanı. `recognize()` çağrısı ağır işi yapar, `getText()` ise basit bir `String` döndürür.

```java
        // Step 4: Execute OCR and fetch the recognized text
        String recognizedText = ocrEngine.recognize().getText();
```

Bu noktada kütüphane zaten **otomatik dil algılamalı OCR**i her blok için gerçekleştirmiştir, dolayısıyla `recognizedText` değişkeni temiz, dil‑bilinçli bir transkripsiyon içerir.

---

## Adım 5: Sonucu Gösterme – Verify Auto‑Detect Language OCR Output

Son olarak sonucu konsola yazdırıyoruz. Gerçek bir uygulamada bunu bir dosyaya, veritabanına yazabilir ya da bir çeviri servisine besleyebilirsiniz.

```java
        // Step 5: Show the output – you’ll see language tags if you enable them
        System.out.println("Auto‑detected language output:\n" + recognizedText);
    }
}
```

### Beklenen Çıktı

`mixed_lang.png` içinde “Hello” (İngilizce) ve “¡Hola!” (İspanyolca) olduğunu varsayalım; aşağıdakine benzer bir şey göreceksiniz:

```
Auto‑detected language output:
Hello
¡Hola!
```

Ayarlar içinde `setShowLanguage(true)` etkinleştirirseniz, motor her satırı bir dil kodu ile önekler, örn. `[en] Hello` ve `[es] ¡Hola!]`.

---

## Yaygın Sorular & Tuzaklar

### Görüntü yolu yanlış olursa ne olur?

Motor bir `FileNotFoundException` fırlatır. Çağrıyı try‑catch bloğuna alın ve kullanıcıya dostça bir mesaj gösterin:

```java
try {
    ocrEngine.setImage("path/to/image.png");
} catch (FileNotFoundException e) {
    System.err.println("Image not found – check the file path!");
    return;
}
```

### Algılamayı hızlandırmak için dilleri sınırlayabilir miyim?

Evet. `AUTO_DETECT` yerine bir liste sağlayabilirsiniz:

```java
ocrEngine.getRecognitionSettings()
         .setLanguage(new OcrLanguage[]{OcrLanguage.ENGLISH, OcrLanguage.SPANISH});
```

Bu, arama alanını daraltır ve büyük toplu işlemlerde performansı artırabilir.

### **otomatik dil algılamalı OCR** el yazısı metni nasıl ele alır?

Aspose OCR basılı metne odaklanır. El yazısı karakterler genellikle farklı bir motor (örneğin Aspose OCR for Handwriting) gerektirir. Algılamayı zorlamak kötü sonuçlar verir.

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda tüm program yer alıyor, derlenip çalıştırılmaya hazır. `YOUR_DIRECTORY` kısmını `mixed_lang.png` dosyasının bulunduğu gerçek klasörle değiştirin.

```java
import com.aspose.ocr.*;

public class AutoDetectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialize the OCR engine – this is where the magic starts
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable automatic language detection for each text block
        ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.AUTO_DETECT);

        // Step 3: Load the image that contains mixed‑language text
        // Make sure the file exists; otherwise an exception is thrown
        ocrEngine.setImage("YOUR_DIRECTORY/mixed_lang.png");

        // Step 4: Run the recognition process and obtain the extracted text
        String recognizedText = ocrEngine.recognize().getText();

        // Step 5: Display the auto‑detected language output
        System.out.println("Auto‑detected language output:\n" + recognizedText);
    }
}
```

Şu komutla çalıştırın:

```bash
javac -cp "aspose-ocr-23.10.jar" AutoDetectDemo.java
java -cp ".:aspose-ocr-23.10.jar" AutoDetectDemo
```

Konsolda daha önce açıklanan çıktıyı görmelisiniz.

---

## Çözümü Genişletmek

Artık **OCR nasıl yapılır** bildiğinize göre şu adımları düşünebilirsiniz:

* **Toplu işleme** – Bir klasördeki görüntüler üzerinde döngü kurun, hız için aynı `OcrEngine` örneğini yeniden kullanın.  
* **Sonuçları kaydetme** – Çıkarılan metni `.txt` dosyalarına yazın ya da bir veritabanına depolayın.  
* **Son‑işleme** – Satır sonlarını temizlemek veya istenmeyen karakterleri kaldırmak için düzenli ifadeler (regex) kullanın.  
* **Entegrasyon** – Çıktıyı bir çeviri API’sine (Google Translate, Azure Translator) besleyerek çok dilli uygulamalar geliştirin.

Bu uzantıların hepsi, ele aldığımız temel kavramlara dayanır: görüntüyü yükleme, dil algılamayı etkinleştirme ve metni çıkarma.

---

## Sonuç

Java’da **OCR nasıl yapılır** sorusuna, dilleri otomatik algılayarak tam bir uçtan‑uca örnekle yanıt verdik. Motoru oluşturma, otomatik dil algılamayı etkinleştirme, görüntüyü yükleme, tanıma çalıştırma ve sonuçları gösterme adımlarını izleyerek çoklu betik içeren **görüntüden metin çıkarma** işlemini güvenilir bir şekilde yapabilirsiniz.  

Unutmayın, sorunsuz **otomatik dil algılamalı OCR** için motorun her blokta karar vermesine izin vermek gerekir; tek bir dili zorlamak genellikle bozuk çıktılara yol açar. Farklı görüntü kaliteleri, dil listeleri ve performans ayarlarıyla deneyler yaparak çözümünüzü ihtiyacınıza göre ince ayarlayın.

Burada ele alınmayan bir senaryonuz mu var? Yorum bırakın, birlikte sorun giderelim. Mutlu kodlamalar!  

![how to perform OCR example](/images/ocr-demo.png "Aspose OCR ile Java’da OCR nasıl yapılır gösteren ekran görüntüsü")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}