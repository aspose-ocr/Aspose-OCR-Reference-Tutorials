---
category: general
date: 2026-03-28
description: Java'da Aspose OCR kullanarak PNG dosyalarından metin tanımayı öğrenin.
  Görüntüden metin çıkarma ve karışık diller için otomatik dil algılamayı etkinleştirme
  özelliklerini içerir.
draft: false
keywords:
- recognize text from png
- extract text from image
- enable auto language detection
language: tr
og_description: PNG'den metni anında tanıyın. Bu kılavuz, görüntüden metin çıkarmayı
  ve karışık dilli PDF'lerde otomatik dil algılamayı nasıl etkinleştireceğinizi gösterir.
og_title: Aspose OCR ile PNG'den metin tanıma – Tam Java Öğreticisi
tags:
- Aspose OCR
- Java
- Image Processing
title: Aspose OCR ile PNG'den Metin Tanıma – Tam Java Rehberi
url: /tr/java/ocr-operations/recognize-text-from-png-with-aspose-ocr-full-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# png'den metin tanıma – Aspose OCR ile Tam Java Öğreticisi

Hiç **png dosyalarından metin tanıma** ihtiyacı duydunuz mu ama karışık dilleri sorunsuz bir şekilde işleyebilecek kütüphaneyi bulamadınız mı? Yalnız değilsiniz—uygulamalarının makbuz, pasaport veya çok dilli tabelaları okuması gerektiğinde birçok geliştirici bu sorunla karşılaşıyor.  

İyi haber şu ki Aspose OCR bunu çocuk oyuncağı haline getiriyor: sadece birkaç satırla **görüntüden metin çıkarabilir**, PNG'yi aranabilir veri haline getirebilir ve hatta **otomatik dil algılamayı etkinleştirebilirsiniz**, böylece motor anında doğru betiği seçer.  

Bu öğreticide, başlamanız için ihtiyacınız olan her şeyi adım adım inceleyeceğiz: önkoşullar, adım adım kod, her ayarın neden önemli olduğu ve çıktıyı nasıl doğrulayacağınız. Sonunda, İngilizce, Rusça ve Çince metin içeren bir PNG'yi okuyabilen çalıştırılabilir bir Java programına sahip olacaksınız—dil paketlerini manuel olarak değiştirmeye gerek kalmadan.

---

## Gereksinimleriniz

- **Java Development Kit (JDK) 8+** – kod, herhangi bir yeni JDK ile derlenir.
- **Aspose.OCR for Java** kütüphanesi (2026 itibarıyla en son sürüm). Maven Central'dan veya Aspose web sitesinden edinebilirsiniz.
- Çok dilli metin içeren bir görüntü dosyası (ör. `mixed-lang.png`).
- İyi bir IDE (IntelliJ IDEA, Eclipse veya hatta VS Code) – ancak basit bir metin düzenleyicisi de iş görür.

> **Pro tip:** Maven kullanıyorsanız, aşağıdaki bağımlılığı ekleyin; aksi takdirde JAR'ı indirip sınıf yolunuza ekleyin.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the newest version -->
</dependency>
```

---

## Adım 1: OCR Motorunu png'den metin tanıma için başlatma

Motor herhangi bir işlem yapmadan önce bir `OcrEngine` örneğine ihtiyacınız var. Bu nesne tüm yapılandırma seçeneklerini tutar ve ağır işi gerçekleştirir.

```java
import com.aspose.ocr.*;

public class MixedLangExample {
    public static void main(String[] args) throws Exception {

        // Create the OCR engine – this is the entry point for all operations
        OcrEngine ocrEngine = new OcrEngine();

        // --------------------------------------------------------------
        // Step 2 and 3 are configured here (see next sections)
        // --------------------------------------------------------------

        // Recognize the image and get the result object
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/mixed-lang.png");

        // Print the extracted text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

> **Neden önemli:** `OcrEngine`, temel OCR algoritmasını soyutlar. Bir kez örnekleyip birçok görüntüde yeniden kullanmak, dosya başına yeni bir motor oluşturmak yerine daha verimlidir.

---

## Adım 2: Otomatik dil algılamayı etkinleştirme

Bu adımı atladığınızda motor tek bir varsayılan dili (genellikle İngilizce) varsayar ve bu da Kiril veya Çince betikler için bozuk karakterlere yol açar. Otomatik algılamayı açmak, Aspose'un görüntüyü taramasını ve en iyi dil modelini otomatik olarak seçmesini sağlar.

```java
// Enable automatic language detection – the engine will sniff the script
ocrEngine.getRecognitionSettings().setAutoDetectLanguage(true);
```

> **Arka planda ne oluyor?** Aspose OCR, karakter sıklığını ve Unicode aralıklarını kontrol eden hafif bir ön‑analiz çalıştırır. Baskın bir dil tespit ettiğinde, ağır OCR işleminden önce ilgili dil modelini devreye alır.

---

## Adım 3: (İsteğe Bağlı) Algılamayı olası dillere sınırlama – hızı artırma

Beklediğiniz diller kümesini bildiğinizde motoru bir ipucu ile yönlendirebilirsiniz. Bu, arama alanını daraltır, CPU kullanımını azaltır ve genellikle daha hızlı sonuçlar verir.

```java
// Suggest candidate languages – only English, Russian, and Chinese will be considered
ocrEngine.getRecognitionSettings()
         .setCandidateLanguages(new String[] { "en", "ru", "zh" });
```

> **İpucu:** Bu adımı atladığınızda motor yine de çalışır, ancak tüm desteklenen dilleri değerlendirir; bu da büyük toplularda birkaç saniye ekleyebilir.

---

## Adım 4: PNG'yi tanıma ve görüntüden metin çıkarma

Motor yapılandırıldıktan sonra `recognizeImage` metodunu çağırın. Bu yöntem bir dosya yolu, bir `java.io.File` veya hatta bir `java.io.InputStream` kabul eder; bu da web yüklemeleri veya bulut depolama için esneklik sağlar.

```java
// Perform OCR on the specified PNG file
OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/mixed-lang.png");

// The result object holds the raw text, confidence scores, and layout info
String extractedText = ocrResult.getText();
```

> **Köşe durumu:** Görüntü döndürülmüşse, Aspose OCR otomatik döndürme yapabilir. Çıktının hizalanmadığını fark ederseniz `setDetectOrientation(true)` ile manuel olarak ayarlayabilirsiniz.

---

## Adım 5: Sonucu gösterme – çıktıyı doğrulama

Konsola yazdırmak hızlı bir demo için uygundur, ancak gerçek bir uygulamada metni bir veritabanına kaydedebilir, bir arama indeksine besleyebilir veya bir REST API üzerinden döndürebilirsiniz. Aşağıda minimal bir doğrulama kod parçası bulunuyor.

```java
System.out.println("=== Recognized Text ===");
System.out.println(extractedText);
```

### Beklenen konsol çıktısı

`mixed-lang.png` dosyasının üç satır içerdiğini varsayalım:

```
Hello world!
Привет мир!
你好，世界！
```

Şuna benzer bir şey görmelisiniz:

```
=== Recognized Text ===
Hello world!
Привет мир!
你好，世界！
```

Çıktı karışık görünüyorsa, `setAutoDetectLanguage(true)`'ın etkin olduğundan ve aday diller listesinin ihtiyacınız olan betikleri içerdiğinden emin olun.

---

## Tam Çalışan Örnek (Tüm Adımlar Birleştirildi)

```java
import com.aspose.ocr.*;

public class MixedLangExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable automatic language detection
        ocrEngine.getRecognitionSettings().setAutoDetectLanguage(true);

        // Step 3: (Optional) Limit detection to likely languages
        ocrEngine.getRecognitionSettings()
                 .setCandidateLanguages(new String[] { "en", "ru", "zh" });

        // Step 4: Recognize the PNG image
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/mixed-lang.png");

        // Step 5: Output the recognized text
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

> **Çalıştırın:** `javac MixedLangExample.java` ile derleyin ve `java MixedLangExample` ile çalıştırın. Aspose OCR JAR'ının sınıf yolunuzda olduğundan emin olun (ör. Windows'ta `-cp aspose-ocr-23.12.jar;.` veya Linux/macOS'ta `-cp aspose-ocr-23.12.jar:.`).

---

## Yaygın Sorular & Dikkat Edilmesi Gerekenler

| Soru | Cevap |
|----------|--------|
| **Görüntüm PNG yerine JPEG olsaydı ne olur?** | Aynı `recognizeImage` yöntemi JPEG, BMP, TIFF vb. için çalışır. Sadece dosya uzantısını değiştirin. |
| **Bir HTTP isteğinden gelen akışı işleyebilir miyim?** | Kesinlikle. `recognizeImage(InputStream)` kullanın ve isteğin giriş akışını doğrudan besleyin. |
| **Benzer betikler için (ör. Sırp Kirilcesi vs Rusça) otomatik dil algılamanın doğruluğu nedir?** | Genellikle çok doğru olur, ancak `candidateLanguages` listesine ekleyip diğerlerini çıkararak bir dili zorlayabilirsiniz. |
| **Aspose OCR için lisansa ihtiyacım var mı?** | Ücretsiz bir değerlendirme lisansı test için çalışır, ancak üretim kullanımı için filigranı kaldırmak ve tam özellikleri açmak amacıyla ücretli bir lisans gerekir. |
| **Büyük toplularda performans nasıl?** | Tek bir `OcrEngine` örneğini yeniden kullanın ve görüntüleri sıralı ya da bir iş parçacığı havuzunda işleyin. Motor, yalnızca okuma işlemleri için iş parçacığı güvenlidir. |

---

## Sonraki Adımlar & İlgili Konular

- **Görüntüden metin çıkarma** PDF dosyalarında – taranmış belgeler için Aspose PDF ile OCR'ı birleştirin.
- **Toplu işleme** – binlerce PNG'yi paralelleştirmek için Java'nın `ExecutorService`'ini kullanın.
- **Post‑işleme** – çıkarımdan sonra yazım denetimi veya dile özgü tokenizasyon uygulayın.
- **Bulut depolama ile bütünleştirme** – akışları kullanarak PNG'leri doğrudan AWS S3 veya Azure Blob Storage'dan okuyun.

Denemekten çekinmeyin: döndürülmüş taramalarınız varsa `setDetectOrientation(true)` ekleyin, ya da aday dil listesine Japonca (`"ja"`) veya Arapça (`"ar"`) ekleyin. API, çoğu OCR‑odaklı proje için yeterince esnektir.

---

## Sonuç

Artık Aspose OCR kullanarak **png'den metin tanıma**, **görüntüden metin çıkarma** ve karışık‑dilli içerik için **otomatik dil algılamayı etkinleştirme** nasıl yapılır gösteren sağlam, uçtan uca bir örneğiniz var. Kod eksiksiz, açıklamalar hem “nasıl” hem de “neden” yönlerini kapsıyor ve beklenen çıktıyı gördünüz, böylece her şeyin makinenizde çalıştığını doğrulayabilirsiniz.

Farklı bir kullanım senaryonuz mu var? Bir yorum bırakın, bulgularınızı paylaşın veya yukarıdaki sonraki adımları keşfedin. İyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}