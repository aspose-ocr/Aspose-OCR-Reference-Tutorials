---
category: general
date: 2026-06-16
description: Java kullanarak birkaç adımda belge üzerinde OCR çalıştırın. OCR'ı nasıl
  yapılandıracağınızı, TIFF'ten metin tanımayı ve çok sayfalı görüntülerden metin
  çıkarmayı öğrenin.
draft: false
keywords:
- run OCR on document
- how to configure OCR
- recognize text from TIFF
- extract text from multi-page
language: tr
og_description: Java ile belgelerde OCR çalıştırın. Bu kılavuz, OCR'ı nasıl yapılandıracağınızı,
  TIFF dosyalarından metin tanımayı ve çok sayfalı görüntülerden metin çıkarmayı gösterir.
og_title: Java'da Belge Üzerinde OCR Çalıştırma – Adım Adım Öğretici
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Run OCR on document using Java in just a few steps. Learn how to configure
    OCR, recognize text from TIFF, and extract text from multi‑page images.
  headline: Run OCR on Document in Java – Complete Guide
  type: TechArticle
- description: Run OCR on document using Java in just a few steps. Learn how to configure
    OCR, recognize text from TIFF, and extract text from multi‑page images.
  name: Run OCR on Document in Java – Complete Guide
  steps:
  - name: '**Streamed processing** – Some OCR SDKs let you feed pages one‑by‑one instead
      of loading the entire TIFF into memory. Look for methods like `engine.setImageStream(...)`
      that accept an `InputStream`.'
    text: '**Streamed processing** – Some OCR SDKs let you feed pages one‑by‑one instead
      of loading the entire TIFF into memory. Look for methods like `engine.setImageStream(...)`
      that accept an `InputStream`.'
  - name: '**Memory limits** – If you hit `OutOfMemoryError`, lower the thread count
      or increase the JVM heap (`-Xmx2g`).'
    text: '**Memory limits** – If you hit `OutOfMemoryError`, lower the thread count
      or increase the JVM heap (`-Xmx2g`).'
  - name: '**Post‑processing** – Use regex or natural‑language libraries to clean
      up line breaks, remove headers/footers, or extract specific fields (e.g., invoice
      numbers).'
    text: '**Post‑processing** – Use regex or natural‑language libraries to clean
      up line breaks, remove headers/footers, or extract specific fields (e.g., invoice
      numbers).'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Java'da Belge Üzerinde OCR Çalıştırma – Tam Kılavuz
url: /tr/java/ocr-operations/run-ocr-on-document-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java’da Belge Üzerinde OCR Çalıştırma – Tam Kılavuz

Her zaman **belge üzerindeki OCR** çalıştırmanız gerektiğinde nereden başlayacağınızı bilemediniz mi? Tek başınıza değilsiniz. Eski arşivleri dijitalleştiriyor ya da taranmış formlardan veri çekiyorsanız, görüntülerden güvenilir metin elde etmek yaygın bir zorluktur.

Bu öğreticide, **OCR nasıl yapılandırılır**, **TIFF’ten metin tanıma** ve **çok sayfalı** belgelerden **metin çıkarma** konularını sadece birkaç Java satırıyla gösteren pratik, uçtan‑uca bir örnek üzerinden ilerleyeceğiz. Gereksiz ayrıntı yok, bugün projenize ekleyebileceğiniz çalışan bir çözüm.

## Öğrenecekleriniz

- Java’da bir OCR motoru örneği oluşturma  
- İşlenecek çok sayfalı TIFF görüntüsünü yükleme  
- Motoru thread sayısını ayarlayarak optimize etme ( “OCR nasıl yapılandırılır” bölümü)  
- Tanıma işlemini gerçekleştirme ve çıkarılan metni çıktı olarak alma  
- Büyük dosyalar ve bellek limitleri gibi kenar durumlarını ele alma  

Bu rehberi tamamladığınızda **belge üzerindeki OCR**’ı güvenle çalıştırabilecek ve çözümü PDF, PNG ya da canlı kamera akışlarına genişletmek için sağlam bir temele sahip olacaksınız.

## Önkoşullar

- Java 17 veya üzeri (kod, kısalık için `var` anahtar kelimesi kullanıyor)  
- `OcrEngine` sınıfını sunan bir OCR kütüphanesi (ör. *Aspose.OCR for Java* veya *Tesseract‑Java* sarmalayıcısı).  
- Bilinen bir dizinde bulunan `multi_page.tif` adlı çok sayfalı TIFF dosyası.  

OCR kütüphaneniz yoksa, `pom.xml` (Maven) ya da `build.gradle` (Gradle) dosyanıza ekleyin – tam koordinatlar sağlayıcıya göre değişir, ancak çoğu tek bir JAR dosyası sunar.

---

## Adım 1: OCR Motorunu Başlatma – Belge Üzerinde OCR Nasıl Çalıştırılır

İlk iş olarak, ağır işi yapacak bir motor nesnesine ihtiyacınız var. Bunu işlemin beyni olarak düşünün.

```java
import com.example.ocr.OcrEngine;   // Replace with your actual package
import com.example.ocr.ImageStream;
import com.example.ocr.OcrResult;

public class OcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();
```

> **Neden önemli:** `OcrEngine`, tüm tanıma ayarlarını, dil paketlerini ve donanım kullanım seçeneklerini kapsar. Motoru bir kez oluşturup birden çok görüntüde yeniden kullanmak, her seferinde yeni bir örnek yaratmaktan daha verimlidir.

---

## Adım 2: Çok Sayfalı TIFF’i Yükleme – Çok Sayfalı Görüntülerden Metin Çıkarma

Şimdi motoru işlemek istediğimiz dosyaya yönlendiriyoruz. TIFF, bir dosyada birden fazla sayfa depolayabildiği için taranmış belgeler için yaygın bir formattır.

```java
        // Step 2: Load the multi‑page image to be processed
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multi_page.tif"));
```

> **Pro ipucu:** TIFF’iniz bir ağ paylaşımında bulunuyorsa, `ImageStream.fromUrl(...)` kullanın. Bu, OCR başlamadan önce tüm dosyanın belleğe kopyalanmasını önler.

---

## Adım 3: OCR’u Maksimum Performans İçin Nasıl Yapılandırılır

Kutudan çıktığı gibi OCR kütüphaneleri genellikle tek bir thread üzerinde çalışır; bu, modern çok çekirdekli makinelerde darboğaz oluşturabilir. İşte “**OCR nasıl yapılandırılır**” sorusunun cevabı burada.

```java
        // Step 3: Configure the engine to use all available CPU cores
        int availableCores = Runtime.getRuntime().availableProcessors();
        engine.getRecognitionSettings().setThreadCount(availableCores);
```

> **Neden işe yarar:** Thread sayısını mantıksal işlemci sayısına eşitleyerek OCR motoru farklı sayfaları paralel işleyebilir. 4 çekirdekli bir dizüstü bilgisayarda çok sayfalı belgelerle çalışırken yaklaşık 3‑4 kat hız artışı göreceksiniz.

> **Kenar durumu:** Bazı ortamlar (ör. CPU kotası sınırlı Docker konteynerleri) kullanılabilir çekirdek sayısından daha fazlasını raporlayabilir. Böyle durumlarda thread sayısını manuel olarak sınırlayın: `engine.getRecognitionSettings().setThreadCount(Math.min(availableCores, 2));`

---

## Adım 4: TIFF’ten Metin Tanıma – Çekirdek OCR Çağrısı

Her şey bağlandı, şimdi tanıma işlemini çalıştırma zamanı. Bu tek çağrı, TIFF’in her sayfasını yineleyip dil modellerini uygular ve birleşik bir sonuç döndürür.

```java
        // Step 4: Perform the OCR recognition
        OcrResult result = engine.recognize();
```

> **Arka planda ne oluyor?** Motor, TIFF’i ayrı raster görüntülerine bölerek her birini OCR sinir ağına gönderir ve metin çıktısını birleştirir. Sayfa bazında ayrıntı isterseniz, `result.getPages()` size `OcrPageResult` nesnelerinin bir listesini verir.

---

## Adım 5: Tanınan Metni Çıktı Olarak Verme – Çıkarma İşlemini Doğrulama

Son olarak, çıkarılan metni konsola yazdırıyoruz. Gerçek bir uygulamada muhtemelen bir veritabanına ya da JSON dosyasına kaydedersiniz.

```java
        // Step 5: Output the recognized text
        System.out.println(result.getText());
    }
}
```

**Beklenen çıktı (kısaltılmış):**

```
Page 1:
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00

Page 2:
Terms and Conditions...
```

Eğer temiz karakterler yerine anlamsız karakterler görüyorsanız, doğru dil paketlerinin yüklü olduğundan ve görüntünün çok gürültülü olmadığından emin olun. Maskeleme, eğrilik giderme gibi ön‑işleme adımları doğruluğu büyük ölçüde artırabilir.

---

## Büyük Çok Sayfalı Dosyalarla Çalışma – Çıkarma İçin İpuçları

Temel akışı zaten gösterdik, ancak gerçek dünyadaki belgeler devasa olabilir. İşte birkaç ek öneri:

1. **Akış tabanlı işleme** – Bazı OCR SDK’ları tüm TIFF’i belleğe yüklemek yerine sayfaları tek tek beslemenize izin verir. `engine.setImageStream(...)` gibi `InputStream` kabul eden metodları arayın.  
2. **Bellek limitleri** – `OutOfMemoryError` alırsanız, thread sayısını azaltın ya da JVM heap’ini artırın (`-Xmx2g`).  
3. **Son‑işleme** – Regex ya da doğal dil kütüphaneleriyle satır sonlarını temizleyin, başlık/altbilgi kaldırın veya fatura numarası gibi belirli alanları çıkarın.

---

## Tam Çalışan Örnek (Tüm Adımlar Birleştirildi)

Aşağıda, doğrudan çalıştırabileceğiniz tam Java sınıfı yer alıyor. IDE’nize yapıştırın, paket/ithalatları ayarlayın ve çalıştırın.

```java
package com.example.ocrdemo;

import com.example.ocr.OcrEngine;
import com.example.ocr.ImageStream;
import com.example.ocr.OcrResult;

/**
 * Demonstrates how to run OCR on document images, configure the engine,
 * recognize text from TIFF files, and extract text from multi‑page documents.
 */
public class OcrDemo {
    public static void main(String[] args) throws Exception {
        // Create the OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Load the multi‑page TIFF image
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multi_page.tif"));

        // Configure the engine to use all CPU cores (how to configure OCR)
        int cores = Runtime.getRuntime().availableProcessors();
        engine.getRecognitionSettings().setThreadCount(cores);

        // Perform recognition (recognize text from TIFF)
        OcrResult result = engine.recognize();

        // Output the extracted text (extract text from multi‑page)
        System.out.println(result.getText());
    }
}
```

> **Pro ipucu:** `recognize()` çağrısını bir `try‑catch` bloğu içinde tutarak `OcrException`’ı nazikçe ele alın; özellikle bozuk görüntü dosyalarıyla çalışırken bu faydalı olur.

---

## Sonuç

Java kullanarak **belge üzerindeki OCR**’ı nasıl çalıştıracağınızı, motor başlatmadan çok sayfalı metin çıkarımına kadar her adımı gösterdik. **OCR nasıl yapılandırılır** konusunu anladığınızda modern CPU’ların tüm gücünden yararlanabilir, **TIFF’ten metin tanıma** ve **çok sayfalı dosyalardan metin çıkarma** adımlarıyla herhangi bir belge‑dijitalleştirme projesi için sağlam bir temel oluşturursunuz.

Sırada ne var? TIFF’i PDF ile değiştirin, özel dil modelleriyle deney yapın ya da çıktıyı bir arama indeksine yönlendirin. Bu temele sahip olduğunuzda sınır yoktur.

Seçtiğiniz OCR kütüphanesi farklı bir API sunuyorsa—örneğin farklı metod isimleri—aşağıya yorum bırakın. İyi kodlamalar, taranmış sayfalarınızı aranabilir metne dönüştürmenin tadını çıkarın!

## Bir Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayalı olarak ilgili konuları ayrıntılı bir şekilde ele alır. Her kaynak, adım‑adım açıklamalar ve tam çalışan kod örnekleri içerir; böylece ek API özelliklerini öğrenebilir ve projelerinizde alternatif uygulama yaklaşımlarını keşfedebilirsiniz.

- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to recognize tiff with Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-tiff/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}