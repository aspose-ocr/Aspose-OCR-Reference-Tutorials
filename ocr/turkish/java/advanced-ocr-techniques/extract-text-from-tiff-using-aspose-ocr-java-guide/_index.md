---
category: general
date: 2026-07-05
description: Tiff dosyalarından metin çıkarma, Aspose OCR Java ile paralel OCR işleme
  ortamında. Bu özlü Aspose OCR Java örneği, çok çekirdekli iş parçacığıyla performansı
  nasıl artıracağınızı gösterir.
draft: false
keywords:
- extract text from tiff
- aspose ocr java example
- parallel ocr processing
- java ocr multithreading
- tiff image recognition
language: tr
og_description: Aspose OCR Java ve paralel OCR işleme ile tiff'ten metin çıkarın.
  Çok sayfalı görüntü tanımasını hızlandırmak için bu adım adım Java örneğini izleyin.
og_title: Aspose OCR Java ile tiff dosyasından metin çıkarma – Rehber
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from tiff using Aspose OCR Java in a parallel OCR processing
    setup. This concise Aspose OCR Java example shows how to boost performance with
    multi‑core threading.
  headline: Extract text from tiff using Aspose OCR Java – Guide
  type: TechArticle
tags:
- Java
- OCR
- Aspose
- TIFF
title: Aspose OCR Java ile TIFF'ten metin çıkarma – Rehber
url: /tr/java/advanced-ocr-techniques/extract-text-from-tiff-using-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tiff dosyalarından metin çıkarma Aspose OCR Java – Kılavuz

Hiç **tiff dosyalarından metin çıkarma** ihtiyacı duydunuz ama sürecin salyangoz hızında ilerlediğini gördünüz mü? Tek başınıza değilsiniz. Çok sayfalı bir TIFF'i tek iş parçacıklı bir OCR motoruna verdiğinizde, bekleme süresi sonsuz gibi gelebilir—özellikle toplu iş senaryolarında.

Şöyle bir şey var: Aspose OCR for Java, makinenizdeki her mantıksal çekirdeği kullanabilir ve o yavaş tek‑iş parçacıklı süreci sorunsuz, paralel bir OCR işleme hattına dönüştürür. Bu öğreticide, motoru nasıl yapılandıracağınızı, çok sayfalı bir TIFF'i nasıl besleyeceğinizi ve **tiff dosyalarından metin çıkarma** işlemini orijinal sürenin bir kısmında nasıl yapacağınızı gösteren eksiksiz bir **Aspose OCR Java örneği** üzerinden ilerleyeceğiz.

## Öğrenecekleriniz

- Aspose OCR ile **paralel OCR işleme** gösteren çalıştırılabilir bir Java sınıfı.
- Her yapılandırmanın neden önemli olduğuna dair net açıklamalar, sadece ne yazılacağını değil.
- Farklı sayfa sayıları, büyük görüntü dosyaları ve bellek kısıtlamaları gibi uç durumları ele alma ipuçları.
- Kendi belge‑otomasyon projeleriniz için kodu uyarlamanıza yardımcı olacak sağlam bir temel.

> **Önkoşullar**  
> • Java 8 veya daha yeni bir sürüm yüklü (kod JDK 11 ile de derlenebilir).  
> • Aspose OCR for Java kütüphanesini çekmek için Maven veya Gradle.  
> • Çok sayfalı bir TIFF görüntüsü (herhangi bir görüntü düzenleyiciyle oluşturabilir veya Aspose ile gelen örnek `multi_page.tif` dosyasını kullanabilirsiniz).  

Bu temelleri karşıladıysanız, hemen başlayalım.

![Aspose OCR Java kullanarak tiff dosyalarından metin çıkarma – paralel işleme diyagramı](image.png "Paralel OCR işleme, tiff dosyalarından metin çıkarma sürecini gösteren diyagram")

## Adım 1: Projenizi Kurun – en hızlı Aspose OCR Java örneği

**paralel OCR işleme**'nin kalbine geçmeden önce, Aspose OCR JAR'larını görebilecek bir Java projesine ihtiyacımız var. En basit yol Maven kullanmaktır:

```xml
<!-- pom.xml snippet -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.12</version> <!-- check for the latest version -->
    </dependency>
</dependencies>
```

Gradle tercih ediyorsanız eşdeğeri şudur:

```groovy
implementation 'com.aspose:aspose-ocr:23.12'
```

> **Pro ipucu:** Bağımlılığı Maven Central üzerinden eklemek, her zaman en yeni, güvenlik‑düzeltmeli sürümü çekmenizi sağlar. JAR dosyalarını manuel olarak indirmeye gerek yok.

Derleme dosyanız hazır olduğunda `mvn clean compile` (veya `gradle build`) komutunu çalıştırın; Aspose sınıflarının sınıf yolunda olduğundan emin olun. Hata almazsanız, hazırsınız demektir.

## Adım 2: OCR motorunu oluşturun ve çok‑çekirdekli çalışmayı etkinleştirin

Şimdi OCR işlemini gerçekleştirecek Java sınıfını yazacağız. Normal bir OCR motorunu **paralel OCR işleme** gücüne dönüştüren ana satır `setThreadCount`. Bu, Aspose OCR'e kaç mantıksal çekirdek kullanabileceğini söyler.

```java
package com.example.ocr;

import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.RecognitionResult;

/**
 * ParallelOcrDemo – a concise Aspose OCR Java example that extracts text from tiff
 * images using multiple threads.
 */
public class ParallelOcrDemo {

    public static void main(String[] args) throws Exception {
        // Step 2.1: Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2.2: Tell the engine to use 4 logical cores (adjust to your CPU)
        // This is the heart of parallel OCR processing.
        ocrEngine.setThreadCount(4);

        // Step 2.3: Point the engine at a multi‑page TIFF file.
        // Replace the path with the location of your own TIFF.
        String tiffPath = "YOUR_DIRECTORY/multi_page.tif";

        // Step 2.4: Run the recognition. The method returns a RecognitionResult
        // which holds the extracted text and additional metadata.
        RecognitionResult result = ocrEngine.recognizeImage(tiffPath);

        // Step 2.5: Output the extracted text – this is where we finally
        // extract text from tiff and show it on the console.
        System.out.println("=== Extracted Text Start ===");
        System.out.println(result.getText());
        System.out.println("=== Extracted Text End ===");
    }
}
```

### `setThreadCount` neden önemlidir

Aspose OCR, çok sayfalı bir TIFF'in her sayfasını ayrı görevler olarak bölüştürür. Varsayılan olarak tek bir iş parçacığında çalışır; bu da her sayfanın bir öncekinin bitmesini beklemesi anlamına gelir. `threadCount` değerini fiziksel çekirdek sayısına (veya UI'nin yanıt verebilir kalması için biraz daha azına) ayarlamak, motorun birden fazla sayfayı aynı anda işlemesini sağlar. Benchmark'larda, 4‑çekirdekli bir makine, varsayılan tek‑iş parçacıklı moda göre toplam işleme süresini **%70'e kadar** azaltabiliyor.

> **Not:** İş parçacığı sayısını mevcut çekirdek sayısından yüksek ayarlarsanız, OS zaman dilimlemesi yapar ve bu da performansı düşürebilir. Güvenli bir üst sınır olarak `Runtime.getRuntime().availableProcessors()` kullanın.

## Adım 3: Büyük TIFF'leri ve bellek kısıtlamalarını yönetin

**tiff dosyalarından metin çıkarma** işlemi, onlarca yüksek çözünürlüklü sayfa içerdiğinde bellek kullanımı artabilir. Aspose OCR, işleri düzenli tutmak için birkaç ayar sunar:

```java
// Optional: Reduce memory footprint by lowering image resolution before OCR
ocrEngine.getImagePreprocessingOptions().setResolution(150); // DPI

// Optional: Enable streaming mode for massive TIFFs (>500 MB)
ocrEngine.setEnableStreaming(true);
```

- **Çözünürlük azaltma** biraz doğruluk kaybı karşılığında büyük bir bellek tasarrufu sağlar. Çoğu basılı belge 150 DPI'da hâlâ okunaklıdır.
- **Akış modu** tüm TIFF'i RAM'e yüklemeden sayfaları tek tek işler. Sunucu‑tarafı toplu işler için vazgeçilmezdir.

## Adım 4: Çıktıyı doğrulayın ve yaygın sorunları giderin

Demo'yu çalıştırdıktan sonra, “=== Extracted Text Start ===” işaretleriyle çevrelenmiş çıkarılan metni görmelisiniz. Çıktı boş ya da bozuk görünüyorsa, aşağıdaki kontrolleri değerlendirin:

| Belirti | Muhtemel Neden | Hızlı Çözüm |
|---------|----------------|-------------|
| Metin hiç yok | Yanlış dosya yolu veya desteklenmeyen TIFF sıkıştırması | `tiffPath`'i doğrulayın ve TIFF'in özel bir sıkıştırma (ör. CCITT Group 4 uygundur; JPEG‑2000 ek codec gerektirebilir) kullanmadığından emin olun. |
| Eksik karakterler (ör. aksanlı harfler) | OCR dili ayarlanmamış | `ocrEngine.setLanguage(OcrEngine.Language.English);` çağırın veya özel bir dil paketi yükleyin. |
| Bellek dışı hatalar | Akış modu olmadan çok büyük TIFF | `setEnableStreaming(true)` etkinleştirin ve/veya çözünürlüğü düşürün. |
| `setThreadCount` despite yavaş performans | CPU hiper‑threading devre dışı veya JVM sınırlamaları | JVM'in `-Xmx` bayraklarıyla kısıtlanmadığından emin olun; yeterli yığını (ör. `-Xmx2g`) sağlayın. |

## Adım 5: Ölçeklendirin – bir klasördeki TIFF'leri paralel işleyin

Tek dosya demosu öğrenmek için harika, ancak üretimde genellikle toplu iş gerekir. Aşağıda, bir dizini gezip bir iş parçacığı havuzu oluşturup OCR motorunu her dosya üzerinde eşzamanlı çalıştıran hafif bir uzantı bulunuyor. Bu, uygulama seviyesinde **paralel OCR işleme**'yi gösterir.



## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım‑adım açıklamalarla tam çalışan kod örnekleri içerir.

- [Metin Çıkarma Görüntüleri – Aspose.OCR for Java ile OCR Temelleri](/ocr/english/java/ocr-basics/)
- [Görüntüden Metin Çıkarma Java – Aspose.OCR Detect Areas Modu](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [URL'den Görüntüyle Metin Çıkarma – Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}