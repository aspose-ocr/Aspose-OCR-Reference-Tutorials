---
date: 2026-06-24
description: Aspose.OCR for Java kullanarak dil seçeneğiyle görüntü metnini OCR'lamak
  nasıl öğrenilir. Bu adım adım rehber, extract text java, OCR skew correction ve
  daha fazlasını kapsar.
keywords:
- ocr skew correction
- ocr language support
- improve ocr accuracy
- extract text image java
- ocr image java
linktitle: Aspose.OCR ile OCR Eğik Düzeltme ve Dil Seçimini Nasıl Yapılır
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Learn how to OCR image text with language selection using Aspose.OCR
    for Java. This step‑by‑step guide covers extract text java, OCR skew correction,
    and more.
  headline: How to Perform OCR Skew Correction and Language Selection with Aspose.OCR
  type: TechArticle
- description: Learn how to OCR image text with language selection using Aspose.OCR
    for Java. This step‑by‑step guide covers extract text java, OCR skew correction,
    and more.
  name: How to Perform OCR Skew Correction and Language Selection with Aspose.OCR
  steps:
  - name: Set up Your Document Directory
    text: Create a `File` object that points to the folder containing your source
      image. This makes the path handling portable across operating systems. Replace
      `"Your Document Directory"` with the absolute path where `p3.png` resides.
  - name: Define the Image Path
    text: Instantiate a `File` object for the specific image you want to process.
      Using a `File` object gives you easy access to file metadata if you need it
      later. Make sure the `file` variable points to the exact image you intend to
      process.
  - name: Create Aspose.OCR API Instance
    text: The `AsposeOCR` class is the entry point for all OCR operations. It encapsulates
      the engine, manages resources, and provides the `recognizePage` method. The
      `AsposeOCR` object gives you access to all OCR operations.
  - name: Set Recognition Options (Language Selection)
    text: '`RecognitionSettings` is Aspose.OCR''s configuration container that lets
      you fine‑tune the OCR process. Here we: 1. Disable auto‑skew because we provide
      a manual skew value. 2. Define a rectangular region (`RecognitionAreas`) to
      limit OCR to the part of the image that actually contains text. 3. Set t'
  - name: Perform OCR and Retrieve Results
    text: Calling `recognizePage` runs the OCR engine using the image and the settings
      you defined. The outcome is stored in a `RecognitionResult` object, which aggregates
      all useful data. The `RecognizePage` call runs the OCR engine using the image
      and the settings you defined. The outcome is stored in a `Re
  - name: Print and Utilize Results
    text: 'The console output shows: - The full extracted text (`recognitionText`).
      - Text for each defined rectangle (`recognitionAreasText`). - Bounding rectangle
      coordinates. - A JSON representation for easy downstream processing. - Detected
      skew angle and any warnings. The console output shows the full ext'
  type: HowTo
- questions:
  - answer: Yes. Use `settings.setLanguage(Language.Eng | Language.Fra)` to enable
      multilingual recognition.
    question: Can I recognize multiple languages in a single OCR call?
  - answer: PNG, JPEG, BMP, TIFF, GIF, and several others. Just provide the correct
      file path.
    question: Which image formats does Aspose.OCR support?
  - answer: There’s no hard limit, but processing images larger than 10 MB can increase
      memory usage and runtime. Consider resizing large files.
    question: Is there a size limit for the image?
  - answer: Purchase a license from the Aspose website and apply it via the `License`
      class as shown in the Aspose documentation.
    question: How do I obtain a production license?
  - answer: Not directly with Aspose.OCR. Convert the PDF page to an image first (e.g.,
      using Aspose.PDF) and then run OCR.
    question: Can I extract text from a PDF page directly?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Aspose.OCR ile OCR Eğik Düzeltme ve Dil Seçimini Nasıl Yapılır
url: /tr/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.OCR ile OCR Çarpıklık Düzeltmesi ve Dil Seçimini Nasıl Gerçekleştirirsiniz

## Giriş

Resim dosyalarından metin çıkarmak, taranmış belgeleri dijitalleştiriyor, fişleri işliyor ya da aranabilir arşivler oluşturuyor olsanız da yaygın bir gereksinimdir. Bu öğreticide, belirli bir dil ayarıyla **resim metnini OCR ile nasıl okuyacağınızı** gösteren eksiksiz, uygulamalı bir örnek üzerinden geçeceğiz, böylece güvenilir OCR'ı Java uygulamalarınıza bugün entegre edebilirsiniz. Ayrıca **OCR çarpıklık düzeltmesini** ve bölge‑tabanlı tanımayı optimal doğruluk için nasıl yöneteceğinizi göreceksiniz; bu birlikte **OCR doğruluğunu** eğimli taramalarda %30'a kadar artırabilir.

## Hızlı Yanıtlar
- **Java'da OCR işlemini hangi kütüphane yönetir?** Aspose.OCR for Java  
- **Hangi ayar dili seçer?** `settings.setLanguage(Language.Eng)` (veya desteklenen herhangi bir dil)  
- **Geliştirme için lisansa ihtiyacım var mı?** Ücretsiz deneme lisansı test için çalışır; üretim için ticari lisans gereklidir.  
- **OCR'ı görüntünün bir bölgesiyle sınırlayabilir miyim?** Evet, dikdörtgenlerle `RecognitionSettings.setRecognitionAreas()` kullanın.  
- **Tipik çalışma süresi nedir?** Görüntü boyutu ve dil karmaşıklığına bağlı olarak standart bir dizüstü bilgisayarda sayfa başına birkaç saniye.  

`Language` Aspose.OCR tarafından desteklenen OCR dillerini listeleyen bir enumdur; örneğin İngilizce, Fransızca, İspanyolca vb.

## OCR Çarpıklık Düzeltmesi Nedir?

OCR çarpıklık düzeltmesi, karakter tanımından önce eğik metin satırlarını tespit edip düzleştirme sürecidir. Metin taban çizgisini hizalayarak OCR motoru dil modellerini daha etkili bir şekilde uygulayabilir ve eğimli taramalardan kaynaklanan hatalı tanımlamaları azaltır. Bu adım, giriş görüntüsünün görsel kalitesini artırır, tanıma algoritmalarının gerçek karakter şekillerine odaklanmasını sağlar, döndürmeden kaynaklanan bozulmaları ortadan kaldırır.

## Neden OCR Çarpıklık Düzeltmesi Doğruluğu Artırır

Metin çarpık olduğunda karakter şekilleri bozulur ve hata oranı %20'ye kadar artabilir. **ocr çarpıklık düzeltmesi** bu bozulmayı ortadan kaldırarak motorun gerçek gliflere odaklanmasını sağlar. Benchmark testlerinde Aspose.OCR, %10‑15° döndürülmüş belgelerde çarpıklık düzeltmesi uygulandıktan sonra tanıma doğruluğunda %15‑30 artış elde etti.

## Neden Dil Seçimiyle Aspose.OCR Kullanmalısınız?

Kaynak metnin tam dilini seçmek, OCR motorunun dil‑özel sözlük ve karakter modellerini kullanmasını sağlar; bu da tanıma hassasiyetini büyük ölçüde artırır ve işleme süresini azaltır. Ayrıca Aspose.OCR, çarpıklık düzeltmesi, bölge seçimi ve çıktı formatları üzerinde ince ayarlı kontrol sunar, çok dilli belge işleme hatları için çok yönlü bir seçimdir.

- **Çok dilli destek** – Görüntünüzdeki tam dil(ler)i seçerek doğruluğu artırın.  
- **İnce ayarlı kontrol** – Çarpıklığı ayarlayın, tanıma alanlarını tanımlayın ve otomatik çarpıklık davranışını belirleyin.  
- **Saf Java API** – Yerel bağımlılık yok, herhangi bir Java projesine kolayca entegre edilebilir.  
- **Zengin sonuç verileri** – Tek bir çağrıda düz metin, JSON, sınırlayıcı dikdörtgenler ve uyarılar alın.  
- **Nicel yetenek** – Aspose.OCR **50+** giriş ve çıkış formatını destekler ve tüm belgeyi belleğe yüklemeden **500 sayfalık** görüntü toplularını işleyebilir.

## Önkoşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

- **Java Development Kit (JDK)** yüklü (JDK 8 veya daha yeni).  
- **Aspose.OCR for Java** kütüphanesi – resmi siteden [burada](https://reference.aspose.com/ocr/java/) indirebilirsiniz.  
- Metnini çıkarmak istediğiniz bir görüntü dosyası, ör. `p3.png`.  

## Paketleri İçe Aktarma

Aşağıdaki içe aktarmalar, temel OCR sınıflarına ve standart Java yardımcı programlarına erişim sağlar.  
`import com.aspose.ocr.*;` – ana OCR motorunu getirir.  
`import com.aspose.ocr.config.*;` – `RecognitionSettings` gibi yapılandırma nesnelerini içerir.  
`import java.awt.Rectangle;` – tanıma alanlarını tanımlamak için kullanılır.  

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Java'da OCR Çarpıklık Düzeltmesi Nasıl Uygulanır?

Görüntüyü yükleyin, otomatik çarpıklık algılamayı devre dışı bırakın ve ya ölçülmüş bir açı sağlayın ya da motorun `settings.setAutoSkew(false)` ile hesaplamasını bekleyin. OCR motoru önce sağlanan ya da tespit edilen açıyla görüntüyü düzleştirir, ardından karakter tanımına geçer. Bu iki adımlı yaklaşım, dil modelleri uygulanmadan önce tüm eğimin kaldırılmasını sağlar, daha temiz metin çıktısı ve daha az hatalı tanıma elde edilir.

## Adım‑Adım Kılavuz

### Adım 1: Belge Dizinini Ayarlayın

Kaynak görüntünüzün bulunduğu klasöre işaret eden bir `File` nesnesi oluşturun. Bu, yol yönetimini işletim sistemleri arasında taşınabilir kılar.

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

`"Your Document Directory"` ifadesini `p3.png` dosyasının bulunduğu mutlak yol ile değiştirin.

### Adım 2: Görüntü Yolunu Tanımlayın

İşlemek istediğiniz belirli görüntü için bir `File` nesnesi örnekleyin. Bir `File` nesnesi, gerektiğinde dosya meta verilerine kolay erişim sağlar.

```java
// The image path
String file = dataDir + "p3.png";
```

`file` değişkeninin işlemek istediğiniz tam görüntüyü işaret ettiğinden emin olun.

### Adım 3: Aspose.OCR API Örneğini Oluşturun

`AsposeOCR` sınıfı, tüm OCR işlemleri için giriş noktasını temsil eder. Motoru kapsüller, kaynakları yönetir ve `recognizePage` metodunu sunar.

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

`AsposeOCR` nesnesi tüm OCR işlemlerine erişim sağlar.

### Adım 4: Tanıma Seçeneklerini Ayarlayın (Dil Seçimi)

`RecognitionSettings`, OCR sürecini ince ayarlamanıza olanak tanıyan Aspose.OCR yapılandırma kapsayıcısıdır.  

```java
// Set recognition options
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

Burada:

1. Manuel bir çarpıklık değeri sağladığımız için otomatik çarpıklığı devre dışı bırakıyoruz.  
2. OCR'ı yalnızca metin içeren görüntü kısmıyla sınırlamak için dikdörtgen bir bölge (`RecognitionAreas`) tanımlıyoruz.  
3. **Dili** İngilizce (`Language.Eng`) olarak ayarlayın. Kaynak görüntünüze bağlı olarak bunu `Language.Fra`, `Language.Spa` vb. olarak değiştirin.

### Adım 5: OCR'ı Gerçekleştir ve Sonuçları Al

`recognizePage` çağrısı, tanımladığınız görüntü ve ayarlarla OCR motorunu çalıştırır. Sonuç, tüm faydalı verileri bir araya getiren bir `RecognitionResult` nesnesinde saklanır.

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

`RecognizePage` çağrısı, görüntüyü ve tanımladığınız ayarları kullanarak OCR motorunu çalıştırır. Sonuç, tüm faydalı verileri bir araya getiren bir `RecognitionResult` nesnesinde saklanır.

### Adım 6: Sonuçları Yazdır ve Kullan

Konsol çıktısı şunları gösterir:

- Tam çıkarılan metin (`recognitionText`).  
- Her tanımlı dikdörtgen için metin (`recognitionAreasText`).  
- Sınırlayıcı dikdörtgen koordinatları.  
- Kolay downstream işleme için JSON temsili.  
- Tespit edilen çarpıklık açısı ve olası uyarılar.

```java
// Print result
System.out.println("Result: \n" + result.recognitionText + "\n\n");
for (String n : result.recognitionAreasText) {
    System.out.println(n);
}
for (Rectangle n : result.recognitionAreasRectangles) {
    System.out.println(n.height + ":" + n.width + ":" + n.x + ":" + n.y);
}
System.out.println("\nJSON:" + result.GetJson());
System.out.println("Angle:" + result.skew);
for (String n : result.warnings) {
    System.out.println(n);
}

System.out.println("OCROperationWithLanguageSelection: execution complete");
```

Konsol çıktısı tam çıkarılan metni, bölge‑spesifik metni, sınırlayıcı kutuları, JSON'u, çarpıklık açısını ve uyarıları gösterir. Artık `result.recognitionText` değerini iş mantığınıza besleyebilirsiniz—saklayın, indeksleyin veya başka bir servise gönderin.

## Yaygın Sorunlar ve Çözümler

| Sorun | Neden | Çözüm |
|-------|-------|-----|
| **Garbage characters** | Yanlış dil seçildi | Doğru `Language` enumunu ayarlayın (ör. Fransızca için `Language.Fra`). |
| **No text returned** | Tanıma alanı metni kapsamaz | `Rectangle` koordinatlarını ayarlayın veya tüm görüntüyü işlemek için `RecognitionAreas` kaldırın. |
| **Slow performance** | Çok büyük görüntü veya yüksek çözünürlük | OCR öncesinde görüntüyü küçültün veya JVM bellek tahsisatını artırın. |
| **Warnings about unsupported format** | Görüntü formatı tanınmadı | İşleme öncesinde görüntüyü PNG, JPEG veya TIFF formatına dönüştürün. |

## Sıkça Sorulan Sorular

**S: Tek bir OCR çağrısında birden fazla dili tanıyabilir miyim?**  
C: Evet. Çok dilli tanıma için `settings.setLanguage(Language.Eng | Language.Fra)` gibi birleştirilmiş dil enumu kullanın.

**S: Aspose.OCR hangi görüntü formatlarını destekler?**  
C: PNG, JPEG, BMP, TIFF, GIF ve birkaç diğer format. Doğru dosya yolunu sağlayın.

**S: Görüntü için bir boyut sınırı var mı?**  
C: Katı bir sınır yok, ancak 10 MB'den büyük görüntüler bellek kullanımını ve çalışma süresini artırabilir. Büyük dosyaları yeniden boyutlandırmayı düşünün.

**S: Üretim lisansını nasıl elde ederim?**  
C: Aspose web sitesinden lisans satın alın ve Aspose belgelerinde gösterildiği gibi `License` sınıfı aracılığıyla uygulayın.

**S: PDF sayfasından doğrudan metin çıkarabilir miyim?**  
C: Aspose.OCR ile doğrudan mümkün değildir. Önce PDF sayfasını bir görüntüye (ör. Aspose.PDF kullanarak) dönüştürün, ardından OCR çalıştırın.

## Sonuç

Artık Aspose.OCR for Java kullanarak **görüntüden metin çıkarma**, uygun dili seçme ve **OCR çarpıklık düzeltmesi** uygulama konusunda bilgi sahibisiniz. Bu yaklaşım, belge yönetim sistemlerinden veri yakalama hatlarına kadar herhangi bir Java‑tabanlı iş akışına yerleştirilebilecek doğru, yüksek‑performanslı OCR sağlar. Farklı `Language` enumlarını deneyin, `RecognitionAreas` ayarlarını ince ayarlayın ve JSON çıktısını downstream analizlerinize entegre ederek tam uçlu bir çözüm oluşturun.

---

**Last Updated:** 2026-06-24  
**Tested With:** Aspose.OCR 24.11 for Java  
**Author:** Aspose

## İlgili Öğreticiler

- [Aspose.OCR kullanarak Java'da çarpıklık açısını nasıl hesaplanır](/ocr/java/ocr-basics/calculate-skew-angle/)
- [Aspose.OCR Kullanarak Dil ile Görüntü Metnini OCR Yapma](/ocr/java/ocr-operations/perform-ocr-language-selection/)
- [Aspose.OCR for Java'da PDF Belgelerini OCR ile Tanıma](/ocr/java/ocr-operations/recognize-pdf/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}