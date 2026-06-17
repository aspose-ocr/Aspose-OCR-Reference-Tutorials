---
category: general
date: 2026-02-17
description: Sabit bir iş parçacığı havuzu Java'sını kullanarak PNG görüntülerinden
  metin çıkarmak için paralel OCR işleme ve yürütücü hizmetini düzgün bir şekilde
  kapatmayı öğrenin.
draft: false
keywords:
- fixed thread pool java
- extract text from png
- parallel ocr processing
- convert scanned pages text
- shut down executor service
language: tr
og_description: Bir sabit iş parçacığı havuzu Java'sının PNG görüntülerinden paralel
  olarak metin çıkarabildiğini, taranmış sayfaların metnini dönüştürebildiğini ve
  yürütücü hizmetini güvenli bir şekilde kapatabildiğini keşfedin.
og_title: Sabit iş parçacığı havuzu Java – PNG için paralel OCR
tags:
- java
- ocr
- multithreading
- aspose
title: Sabit iş parçacığı havuzu Java – PNG için paralel OCR
url: /tr/java/advanced-ocr-techniques/fixed-thread-pool-java-parallel-ocr-for-png/
---

other bold: **Java 17**, **Aspose.OCR for Java**, **PNG**. Keep.

Now check any italic: *fixed* we translated "*fixed*". We wrote "*Fixed*". Keep.

Now check any code formatting inside text: `OcrEngine`, `var`, etc. Keep.

Now final output must include all shortcodes and placeholders unchanged.

Let's assemble final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# sabit iş parçacığı havuzu java – PNG için paralel OCR

Birçok PNG dosyasında OCR'ı **fixed thread pool java** kullanarak nasıl hızlandırabileceğinizi hiç merak ettiniz mi? Bu öğreticide **extract text from PNG** görüntülerini paralel olarak işleyip, **convert scanned pages text**'i düzenlenebilir string'lere dönüştüreceğiz ve iş tamamlandığında güvenli bir şekilde **shut down executor service** yapacağız.

Eğer dakikalarca süren tek‑iş parçacıklı bir döngüye baktıysanız, bir sonraki sayfa başlamadan önce her sayfanın bitmesini beklemenin hayal kırıklığını biliyorsunuzdur. İyi haber? Birkaç satır Java ve Aspose OCR ile tüm CPU çekirdeklerinizin gücünü ortaya çıkarabilir, bu taranmış sayfaları aranabilir metne dönüştürebilir ve uygulamanızın yanıt vermesini sağlayabilirsiniz.  

Aşağıda tamamen çalıştırılabilir bir örnek, her parçanın neden önemli olduğuna dair açıklamalar, yaygın tuzaklar ve herhangi bir OCR kütüphanesine uygulayabileceğiniz ipuçları bulacaksınız.

---

## İhtiyacınız Olanlar

- **Java 17** (veya herhangi bir yeni JDK) – kod, modern `var` sözdizimini nadiren kullanır, ancak eski sürümlerde de çalışır.  
- **Aspose.OCR for Java** kütüphanesi – Maven Central'dan alabilir veya Aspose'tan bir deneme sürümü indirebilirsiniz.  
- İşlemek istediğiniz **PNG** dosyalarının bir seti – taranmış makbuzlar, kitap sayfaları veya ekran görüntüleri gibi düşünün.  
- Java eşzamanlılığına temel bir aşinalık – zorunlu değil, ancak faydalı.

Hepsi bu. Harici hizmetler yok, Docker yok, sadece saf Java ve biraz çoklu iş parçacığı sihri.

## Adım 1: Aspose OCR Bağımlılığını ve Lisansı Ekleyin (İsteğe Bağlı)

İlk olarak, Aspose OCR JAR dosyasının sınıf yolunuzda olduğundan emin olun. Maven kullanıyorsanız, ekleyin:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

Bir lisansınız yoksa, kütüphane değerlendirme modunda çalışır; kod aynı şekilde çalışır. Bir lisans yüklemek (üretim için önerilir) için `Aspose.OCR.lic` dosyasını kaynak klasörünüze koyun ve şu şekilde kullanın:

```java
// Load the Aspose OCR license (optional)
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

> **Pro ipucu:** Lisans dosyasını sürüm kontrolünün dışına tutarak yanlışlıkla ifşa edilmesini önleyin.

## Adım 2: Thread‑Safe `OcrEngine` Örneği Oluşturun

Aspose OCR’nin `OcrEngine`i, aynı örneği görevler arasında yeniden kullandığınız sürece thread‑safe'dir. Bir kez oluşturmak bellek tasarrufu sağlar ve motoru her görüntü için yeniden başlatma yükünden kaçınır.

```java
// One shared OcrEngine for all threads
OcrEngine ocrEngine = new OcrEngine();
```

Neden yeniden kullanmalı? Motoru, dil modellerini belleğe yükleyen ağır bir çalışan olarak düşünün. Görüntü başına yeni bir motor oluşturmak, her küçük iş için yeni bir uzman işe almak gibi olur – maliyetli ve gereksiz.

## Adım 3: Sabit İş Parçacığı Havuzu Java'yı Kurun

Şimdi gösterinin yıldızı geliyor: bir **fixed thread pool java**. Mantıksal işlemci sayısına göre boyutlandıracağız, böylece her çekirdek iş alır ve aşırı yüklenmez.

```java
// Determine available processors and create a fixed pool
int threadCount = Runtime.getRuntime().availableProcessors();
ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);
```

*Fixed* bir havuz (önbellekli bir havuz yerine) size öngörülebilir kaynak kullanımı sağlar ve yüzlerce görüntü aynı anda geldiğinde korkulan “bellek yetersizliği” dalgalanmalarını önler.

## Adım 4: İşlemek İstediğiniz PNG Dosyalarını Listeleyin (Extract Text from PNG)

OCR yapmak istediğiniz görüntülerin yollarını toplayın. Gerçek bir projede bir dizini tarayabilir veya bir veritabanından okuyabilirsiniz; burada birkaç örnek sabit kodlayacağız.

```java
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/page1.png",
        "YOUR_DIRECTORY/page2.png",
        "YOUR_DIRECTORY/page3.png"
);
```

> **Not:** Dosya uzantısı **png** önemlidir çünkü Aspose OCR formatı otomatik olarak algılar, ancak JPEG veya TIFF da verebilirsiniz.

## Adım 5: OCR Görevlerini Gönderin – Paralel OCR İşleme

Her görüntü, tanınan metni döndüren bir callable olur. `OcrEngine` paylaşıldığı için, göreve sadece dosya yolunu geçmemiz yeterlidir.

```java
List<Future<String>> ocrFutures = new ArrayList<>();

for (String imagePath : imageFiles) {
    ocrFutures.add(threadPool.submit(() -> {
        // Prepare input for this image
        OcrInput input = new OcrInput();
        input.add(imagePath);

        // Perform OCR using the shared engine
        OcrResult result = ocrEngine.recognize(input);

        // Return the plain text
        return result.getText();
    }));
}
```

`Future` içinde neden sarmalıyız? Tüm işleri anında başlatmamızı sağlar, ardından sonuçları gönderildikleri sırayla toplar – **convert scanned pages text**'i bir belgeye geri dönüştürürken sayfa sırasını korumak için mükemmeldir.

## Adım 6: Sonuçları Alın ve Görüntüleyin (Convert Scanned Pages Text)

Şimdi her `Future`'ın bitmesini bekliyor ve çıktıyı yazdırıyoruz. `get()` çağrısı sadece ilgili görev tamamlanana kadar bloklar, tüm havuzu değil.

```java
for (Future<String> future : ocrFutures) {
    System.out.println("----");
    System.out.println(future.get()); // prints OCR result for one PNG
}
```

Tipik konsol çıktısı şu şekildedir:

```
----
The quick brown fox jumps over the lazy dog.
----
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
----
Page 3 content goes here…
```

Sonuçları dosyalara yazmayı tercih ederseniz, `System.out.println` ifadesini bir `Files.writeString` çağrısı ile değiştirin.

## Adım 7: Executor Service'i Temiz Bir Şekilde Kapatın

Tüm görevler tamamlandığında, **shut down executor service** yapmak çok önemlidir; aksi takdirde JVM, daemon olmayan iş parçacıklarını canlı tutabilir ve sorunsuz bir çıkışı engelleyebilir.

```java
threadPool.shutdown();               // No new tasks accepted
if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
    threadPool.shutdownNow();        // Force shutdown after timeout
}
```

`awaitTermination` deseni, zorlamadan önce havuzun devam eden işleri bitirme şansı verir. Bu adımı atlamak, uzun süren uygulamalarda yaygın bir bellek sızıntısı kaynağıdır.

## Tam Çalışan Örnek

Hepsini bir araya getirerek, `ParallelBatchDemo.java` dosyasına kopyalayıp yapıştırabileceğiniz ve çalıştırabileceğiniz tam program aşağıdadır:

```java
import com.aspose.ocr.*;

import java.util.*;
import java.util.concurrent.*;

public class ParallelBatchDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license (optional)
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // 2️⃣ Shared, thread‑safe OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Fixed thread pool java – one thread per core
        int threadCount = Runtime.getRuntime().availableProcessors();
        ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);

        // 4️⃣ Files to process – extract text from png
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/page1.png",
                "YOUR_DIRECTORY/page2.png",
                "YOUR_DIRECTORY/page3.png"
        );

        // 5️⃣ Submit tasks – parallel OCR processing
        List<Future<String>> ocrFutures = new ArrayList<>();
        for (String imagePath : imageFiles) {
            ocrFutures.add(threadPool.submit(() -> {
                OcrInput input = new OcrInput();
                input.add(imagePath);
                OcrResult result = ocrEngine.recognize(input);
                return result.getText();
            }));
        }

        // 6️⃣ Retrieve and print – convert scanned pages text
        for (Future<String> future : ocrFutures) {
            System.out.println("----");
            System.out.println(future.get());
        }

        // 7️⃣ Shut down executor service cleanly
        threadPool.shutdown();
        if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
            threadPool.shutdownNow();

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}