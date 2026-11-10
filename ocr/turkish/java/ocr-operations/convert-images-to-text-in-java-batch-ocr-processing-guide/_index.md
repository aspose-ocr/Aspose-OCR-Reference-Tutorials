---
category: general
date: 2026-08-28
description: Aspose OCR kullanarak Java'da png görüntülerinden metin çıkarmayı öğrenin.
  Bu öğreticide toplu OCR işleme, bir klasörden görüntü okuma ve dosyaları uzantıya
  göre filtreleme konuları ele alınmaktadır.
draft: false
keywords:
- extract text from png
- read images from folder
- filter files by extension
- how to batch ocr
- aspose ocr java tutorial
lastmod: 2026-08-28
og_description: Aspose OCR kullanarak Java'da png görüntülerinden metin çıkarmayı
  öğrenin. Bu öğreticide toplu OCR işleme, bir klasörden görüntü okuma ve dosyaları
  uzantıya göre filtreleme konuları ele alınmaktadır.
og_image_alt: 'Developer guide: extract text from png images in Java using Aspose
  OCR'
og_title: Java'da png'den metin çıkarma – toplu OCR rehberi
schemas:
- author: Aspose
  dateModified: '2026-08-28'
  description: Learn how to extract text from png images in Java using Aspose OCR.
    This tutorial covers batch OCR processing, reading images from a folder, and filtering
    files by extension.
  headline: How to extract text from png in Java – batch OCR guide
  type: TechArticle
- questions:
  - answer: Absolutely. Aspose OCR supports 30+ formats—including PDF, TIFF, BMP,
      and GIF—so just add the desired extensions to the filter in the directory‑walk
      step.
    question: Can I process PDFs or TIFFs as well?
  - answer: Change `RecognitionLanguage.ENGLISH` to `RecognitionLanguage.SPANISH`
      (or any supported language). The language packs are bundled with the library,
      so no extra download is required.
    question: What if I need a language other than English, such as Spanish?
  - answer: Yes. `Files.walk` traverses the entire tree recursively, so every nested
      PNG/J
    question: My folder contains sub‑folders—will they be scanned?
  - answer: Enable streaming mode by calling `ocrEngine.setUseStreaming(true)`. This
      tells the engine to read the image in chunks, dramatically reducing peak memory
      usage.
    question: How do I handle extremely large images that exceed 200 MB?
  - answer: Yes. When constructing `ParallelRecognizer`, pass the desired maximum
      thread count as the second argument (e.g., `new ParallelRecognizer(ocrEngine,
      4)`).
    question: Is there a way to limit the number of concurrent OCR threads?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: Java'da png'den metin çıkarma – toplu OCR rehberi
url: /tr/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java’da PNG’den Metin Çıkarma – Toplu OCR Kılavuzu

Eğer **PNG dosyalarından metin çıkarmak** gerektiğinde ancak işlemi birkaç resimle sınırlı tutmanın ötesine nasıl ölçeklendireceğinizi bilmiyorsanız, doğru yerdesiniz. Birçok geliştirici tek bir görüntü OCR çağrısıyla başlar ve klasör onlarca ya da yüzlerce dosyaya ulaştığında performans sınırlarına çabucak çarpar. Aspose OCR for Java ile bir dizini dolaşan, yalnızca ilgilendiğiniz görüntü türlerini filtreleyen, tanıma işlemini paralel olarak yürüten ve sonuçları kaynak dosyalarla aynı sırada döndüren sağlam bir toplu OCR hattı oluşturabilirsiniz. Bu kılavuzun sonunda **toplu OCR işleme**yi güvenilir ve verimli bir şekilde yöneten, doğrudan kullanıma hazır bir Java kod parçacığına sahip olacaksınız.

![Görüntüleri metne dönüştürme örneği](https://example.com/convert-images-to-text.png "Java konsol çıktısının PNG dosyalarından dönüştürülmüş metni gösteren ekran görüntüsü")

## Hızlı Yanıtlar
- **OCR'ı hangi kütüphane yönetir?** Aspose OCR for Java.
- **PNG ve JPG'yi birlikte işleyebilir miyim?** Evet – örnek her iki uzantıyı da filtreliyor.
- **OCR motoru iş parçacığı‑güvenli mi?** Tek bir paylaşılan `AsposeOCR` örneği eşzamanlı kullanım için güvenlidir.
- **Test için lisansa ihtiyacım var mı?** Aspose'tan ücretsiz geçici bir anahtar temin edilebilir.
- **Alt klasörler otomatik olarak taranacak mı?** `Files.walk` tüm ağacı özyinelemeli olarak dolaşır.

## PNG’den metin çıkarma nedir?

`extract text from png`, Portable Network Graphics (PNG) dosyalarına optik karakter tanıma (OCR) uygulama sürecine denir; böylece görünen karakterler aranabilir, düzenlenebilir dizeler haline gelir. Aspose OCR motoru piksel verilerini okur, glif şekillerini tanır ve tek bir metod çağrısında Unicode metin döndürür.

## Neden Aspose OCR for Java Kullanmalı?

Aspose OCR, **30+ dil** destekler, standart 8 çekirdekli bir sunucuda **dakikada 500 görüntüye** kadar işleyebilir ve **200 MB**'a kadar dosyaları tüm görüntüyü belleğe yüklemeden işleyebilir. Bu ölçülen yetenekler, bellek sınırlarına takılmadan sıradan donanımda büyük ölçekli toplu işleri güvenilir bir şekilde çalıştırabileceğiniz anlamına gelir.

## Önkoşullar
- Java 17 (veya herhangi bir güncel LTS sürümü).
- Bağımlılık yönetimi için Maven veya Gradle.
- İşlemek istediğiniz PNG/JPG görüntülerini içeren bir dizin.
- Java akışları ve `java.nio.file` paketi hakkında temel bilgi.
- (İsteğe bağlı) Değerlendirme için bir Aspose OCR geçici lisans anahtarı.

> **Pro ipucu:** Ücretsiz geçici anahtar 30 gün sonra sona erer, ancak test için tam API erişimi sağlar.

## Toplu OCR hattı sıralamayı nasıl korur?

`Future<OcrResult>` işleme tamamlandığında alınabilecek bekleyen bir OCR sonucunu temsil eder. Hattı, `Future<OcrResult>` nesnelerini giriş `Path` koleksiyonunun sırasını yansıtan bir listede saklayarak orijinal dosya sırasını korur. Daha sonra futures üzerinde döngü yaptığınızda ve `get()` çağırdığınızda, her çağrı yalnızca ilgili görüntü için bloklanır, böylece ek sıralama mantığı olmadan çıktı dizisi giriş dizisiyle eşleşir.

## Aspose OCR for Java nedir?

`AsposeOCR`, tüm dil paketlerini, tanıma ayarlarını ve dahili yerel kaynakları kapsayan Aspose OCR kütüphanesinin çekirdek sınıfıdır. Uygulama ömrü boyunca bir kez örneklenmesi ve birden çok iş parçacığı arasında güvenli bir şekilde paylaşılması için tasarlanmıştır. Dil verilerini yalnızca bir kez yüklediği için aynı örneğin yeniden kullanılması, başlangıç yükünü azaltır ve toplu işlemler için verimliliği artırır.

## Projeyi nasıl kurar ve Aspose OCR eklenir

İlk olarak, bir Maven (veya Gradle) projesi oluşturun ve Aspose OCR bağımlılığını `pom.xml` dosyanıza ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.10</version>
</dependency>
```

> **Neden önemli:** Bağımlılığı önceden bildirerek derleyicinin `AsposeOCR`, `ParallelRecognizer` ve ilgili sınıfları görmesini sağlarsınız. Ayrıca aynı sürümün tüm makinelerde kullanılmasını garantiler; bu, tekrarlanabilir **toplu OCR işleme** için kritiktir.

Derleme tamamlandıktan sonra IDE'nizi yenileyin; artık Aspose paketlerini **External Libraries** altında görmelisiniz.

## OCR motorunu nasıl başlatır – tek bir örnek paylaşılır

`AsposeOCR`, Aspose OCR kütüphanesi tarafından sağlanan ana OCR motoru sınıfıdır. Tüm çalışma için yalnızca **bir** OCR motoru örneğine ihtiyacımız var. Bunu iş parçacıkları arasında paylaşmak belleği tasarruf ettirir ve motorun dil paketlerini yalnızca bir kez yüklemesi sayesinde hızı artırır.

```java
AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");
```

`AsposeOCR` iş parçacığı‑güvenlidir, bu yüzden onu güvenle bir `ParallelRecognizer`'a verebilir ve bu sınıf işçi iş parçacığı havuzunu yönetecektir.

> **Açıklama:** `ParallelRecognizer`, motoru bir iş parçacığı havuzunda sarar. Birçok dosya gönderdiğinizde, her biri kendi işçi iş parçacığına sahip olur ve çok çekirdekli CPU'larda gerçek paralellik sağlar.

## Klasörden görüntüleri nasıl okur – dizin ağacını dolaşır

`Files.walk`, bir dosya ağacını özyinelemeli olarak dolaşan ve `Path` nesnelerinin bir akışını döndüren bir Java NIO metodudur. Şimdi **klasörden görüntüleri okumamız** ve her PNG veya JPG'yi toplamalıyız. `Files.walk` API'si bunu tek satırda yapar, ancak yalnızca gerektiğinde **PNG’den metin çıkarma** için bir filtre ekleyeceğiz.

```java
List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
    .filter(Files::isRegularFile)
    .filter(p -> {
        String lower = p.toString().toLowerCase();
        return lower.endsWith(".png") || lower.endsWith(".jpg");
    })
    .collect(Collectors.toList());
```

> **Neden burada filtreliyoruz:** `filter` kullanarak **dosyaları uzantılarına göre erken filtreleyebilir** ve böylece sonradan gereksiz I/O'yu azaltırız. Ayrıca kod okunabilir kalır—karmaşık regex'lere gerek yok.

## OCR görevlerini asenkron olarak nasıl göndeririz

`recognizeAsync`, bir görüntüyü OCR motoruna asenkron işleme göndermek için kullanılır ve bekleyen sonucu temsil eden bir `Future<OcrResult>` döndürür. Dosya listesi hazır olduğunda, her yolu `ParallelRecognizer`'a göndeririz. `recognizeAsync` metodu, daha sonra alınmak üzere sakladığımız bir `Future<OcrResult>` döndürür.

```java
ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine, Runtime.getRuntime().availableProcessors());
List<Future<OcrResult>> futures = new ArrayList<>();

for (Path imagePath : imagePaths) {
    futures.add(recognizer.recognizeAsync(imagePath));
}
```

> **Arka planda ne oluyor?** Her çağrı, tanıyıcının dahili yürütücü servisine bir görev ekler. Görevler paralel çalışır, böylece 100 görüntülü bir klasör tek iş parçacıklı bir döngünün alacağı sürenin bir kısmında işlenebilir.

## Dosya sırasını koruyarak sonuçları nasıl alırız

`Future<OcrResult>` asenkron bir OCR görevinin sonucunu tutar ve tanınan metni elde etmek için bir `get()` metodu sağlar. Futures'ları `imagePaths` ile aynı sırada sakladığımız için, listeyi basitçe döngüleyip `get()` çağırabiliriz. Çağrı yalnızca o belirli görüntü tamamlanana kadar bloklanır, ek bir kayıt tutmadan sıralamayı korur.

```java
for (int i = 0; i < futures.size(); i++) {
    try {
        OcrResult result = futures.get(i).get();
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println("Text: " + result.getText());
    } catch (Exception e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

**Örnek konsol çıktısı** (kısaltılmıştır):

```
File: invoice1.png
Text: Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...
```

> **Köşe durumları yönetimi:** Belirli bir görüntü bir istisna (bozuk dosya, desteklenmeyen format) fırlatırsa, bunu yakalar ve geri kalanları işlemeye devam ederiz—güvenilir **toplu OCR işleme** hatları için temel bir alışkanlıktır.

## Kaynakları nasıl temizleriz – tanıyıcıyı kapatırız

`ParallelRecognizer.shutdown()` iç dahili iş parçacığı havuzunu durdurur ve uygulama çıkmadan önce tüm OCR görevlerinin tamamlanmasını sağlar. İç iş parçacığı havuzunu kapatmayı asla unutmayın; aksi takdirde JVM çıkışta takılabilir.

```java
recognizer.shutdown();
```

Hepsi bu! Program artık herhangi bir dizini dolaşıyor, PNG/JPG dosyalarını filtreliyor, OCR'ı paralel olarak çalıştırıyor ve sonuçları orijinal sırada yazdırıyor.

---

## Tam çalışan örnek (kopyala‑yapıştır)

Aşağıda eksiksiz, çalıştırmaya hazır Java sınıfı bulunmaktadır. `"YOUR_DIRECTORY"` ifadesini görüntü klasörünüzün yolu ile değiştirin ve IDE'nizden ya da komut satırından çalıştırın.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.*;

public class BatchOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine (single shared instance)
        AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");

        // Create a parallel recognizer that uses a thread pool
        ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine,
                Runtime.getRuntime().availableProcessors());

        // Walk the directory and collect PNG/JPG files
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(Files::isRegularFile)
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        // Submit OCR jobs asynchronously
        List<Future<OcrResult>> futures = new ArrayList<>();
        for (Path imagePath : imagePaths) {
            futures.add(recognizer.recognizeAsync(imagePath));
        }

        // Retrieve results in the original order
        for (int i = 0; i < futures.size(); i++) {
            try {
                OcrResult result = futures.get(i).get();
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println("Text: " + result.getText());
            } catch (Exception e) {
                System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Clean up the recognizer's thread pool
        recognizer.shutdown();
    }
}
```

Sınıfı çalıştırın, konsolun çıkarılan dizelerle dolduğunu izleyin ve **görüntüleri metne dönüştürdüğünüz** için tek bir I/O bloklayan döngü yazmadan kutlama yapın.

---

## Sıkça Sorulan Sorular (SSS)

**S: PDF'leri veya TIFF'leri de işleyebilir miyim?**  
C: Kesinlikle. Aspose OCR 30+ formatı destekler—PDF, TIFF, BMP ve GIF dahil—bu yüzden dizin‑yürütme adımındaki filtreye istediğiniz uzantıları eklemeniz yeterlidir.

**S: İngilizce dışındaki bir dil, örneğin İspanyolca gerekirse?**  
C: `RecognitionLanguage.ENGLISH` yerine `RecognitionLanguage.SPANISH` (veya desteklenen herhangi bir dil) olarak değiştirin. Dil paketleri kütüphane ile birlikte gelir, ek indirme gerekmez.

**S: Klasörüm alt klasörler içeriyor—tarama yapılacak mı?**  
C: Evet. `Files.walk` tüm ağacı özyinelemeli olarak dolaşır, böylece her iç içe PNG/J

**S: 200 MB'ı aşan çok büyük görüntülerle nasıl başa çıkabilirim?**  
C: `ocrEngine.setUseStreaming(true)` çağırarak akış modunu etkinleştirin. Bu, motorun görüntüyü parçalar halinde okumasını sağlar ve tepe bellek kullanımını büyük ölçüde azaltır.

**S: Eşzamanlı OCR iş parçacığı sayısını sınırlamanın bir yolu var mı?**  
C: Evet. `ParallelRecognizer` oluştururken ikinci argüman olarak istenen maksimum iş parçacığı sayısını geçirin (örneğin, `new ParallelRecognizer(ocrEngine, 4)`).

---

**Son Güncelleme:** 2026-08-28  
**Test Edilen:** Aspose OCR for Java 24.10  
**Yazar:** Aspose  






```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

// ...

// Step 2: Create a single OCR engine instance and a parallel recognizer that uses it
AsposeOCR ocrEngine = new AsposeOCR();               // Loads language data internally
ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);
```

```java
import java.nio.file.*;
import java.util.*;
import java.util.stream.Collectors;

// ...

// Step 3: Find all PNG and JPG images in the target directory
Path imagesRoot = Paths.get("YOUR_DIRECTORY"); // <-- replace with your path
List<Path> imagePaths = Files.walk(imagesRoot)
        .filter(p -> {
            String name = p.toString().toLowerCase();
            return name.endsWith(".png") || name.endsWith(".jpg");
        })
        .collect(Collectors.toList());

if (imagePaths.isEmpty()) {
    System.out.println("No PNG or JPG files found in " + imagesRoot);
    return;
}
```

```java
import java.util.concurrent.*;

// ...

// Step 4: Submit each image for asynchronous recognition
List<Future<OcrResult>> recognitionFutures = new ArrayList<>();

for (Path image : imagePaths) {
    Future<OcrResult> future = parallelRecognizer.recognizeAsync(
            image.toString(),
            RecognitionLanguage.ENGLISH); // Change language if needed
    recognitionFutures.add(future);
}
```

```java
// Step 5: Retrieve and display the OCR results in the original order
for (int i = 0; i < recognitionFutures.size(); i++) {
    try {
        OcrResult result = recognitionFutures.get(i).get(); // blocks if not ready
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println(result.getText()); // The extracted text
        System.out.println("-----");
    } catch (InterruptedException | ExecutionException e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

```
File: invoice_001.png
Invoice #001
Date: 2024‑03‑15
Total: $1,250.00
-----
File: receipt_202403.jpg
Receipt
Item A - $45.00
Item B - $30.00
Grand Total: $75.00
-----
```

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.Collectors;

public class BatchParallelExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a single OCR engine instance and a parallel recognizer that uses it
        AsposeOCR ocrEngine = new AsposeOCR();
        ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);

        // Step 2: Find all PNG and JPG images in the target directory
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        if (imagePaths.isEmpty()) {
            System.out.println("No images found – nothing to convert.");
            parallelRecognizer.shutdown();
            return;
        }

        // Step 3: Submit each image for asynchronous recognition
        List<Future<OcrResult>> recognitionFutures = new ArrayList<>();
        for (Path image : imagePaths) {
            recognitionFutures.add(
                    parallelRecognizer.recognizeAsync(
                            image.toString(),
                            RecognitionLanguage.ENGLISH));
        }

        // Step 4: Retrieve and display the OCR results in the original order
        for (int i = 0; i < recognitionFutures.size(); i++) {
            try {
                OcrResult result = recognitionFutures.get(i).get(); // blocks until processed
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println(result.getText());
                System.out.println("-----");
            } catch (InterruptedException | ExecutionException e) {
                System.err.println("Error processing " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Step 5: Shut down the recognizer to clean up its internal thread pool
        parallelRecognizer.shutdown();
    }
}
```

## İlgili Eğitimler

- [Java’da Görüntüleri Metne Dönüştürme – Toplu OCR İşleme Kılavuzu](/ocr/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/)
- [Java’da Görüntüden Metin Okuma – Tam Aspose OCR Kılavuzu](/ocr/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Aspose.OCR Kullanarak Görüntülerden Metin Çıkarma – İzin Verilen Karakterler](/ocr/java/advanced-ocr-techniques/specify-allowed-characters/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}