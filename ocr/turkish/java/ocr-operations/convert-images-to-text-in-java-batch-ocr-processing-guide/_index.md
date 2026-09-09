---
category: general
date: 2026-01-02
description: Java kullanarak Aspose OCR ile görüntüleri metne dönüştürün. Toplu OCR
  işleme konusunda uzmanlaşın, klasörden görüntüleri okuyun ve dosyaları uzantıya
  göre filtreleyin.
draft: false
keywords:
- convert images to text
- batch ocr processing
- read images from folder
- extract text from png
- filter files by extension
language: tr
og_description: Java ile görüntüleri hızlıca metne dönüştürün. Bu öğreticide toplu
  OCR işleme, bir klasörden görüntü okuma ve dosyaları uzantıya göre filtreleme konuları
  ele alınmaktadır.
og_title: Java'da Görüntüleri Metne Dönüştür – Tam Batch OCR Kılavuzu
tags:
- OCR
- Java
- Aspose
title: Java'da Görüntüleri Metne Dönüştür – Toplu OCR İşleme Rehberi
url: /tr/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java’da Görüntüleri Metne Dönüştürme – Toplu OCR İşleme Kılavuzu

Hiç **görüntüleri metne dönüştürmek** istediğinizde, aynı anda onlarca dosyayla nasıl başa çıkacağınızı bilemediniz mi? Yalnız değilsiniz—geliştiriciler sürekli PNG, JPG ve diğer taramalardan veri çıkarmakla uğraşıyor. İyi haber? Aspose OCR ile dakikalar içinde bir toplu OCR işleme hattı oluşturabilir, klasör yapılarından görüntüleri okuyabilir ve yalnızca önemli olanları çalışmak için dosyaları uzantılarına göre filtreleyebilirsiniz.

Bu öğreticide, bir dizini dolaşan, her `.png` ve `.jpg` dosyasını seçen, her resmi Aspose OCR’a asenkron olarak gönderen ve çıkarılan metni orijinal sırada yazdıran bağımsız bir Java programı oluşturacağız. Sonunda, ölçekli **görüntüleri metne dönüştürme** ihtiyacı olan herhangi bir projeye ekleyebileceğiniz yeniden kullanılabilir bir kod parçacığına sahip olacaksınız.

---

![Convert images to text example](https://example.com/convert-images-to-text.png "Screenshot of Java console output showing converted text from PNG files")

## Oluşturacağınız Şey

- Tek bir `AsposeOCR` motoru, tüm thread'ler arasında paylaşılan (verimli ve thread‑güvenli).  
- Paralel OCR görevlerini aynı anda çalıştıran bir `ParallelRecognizer`, **toplu OCR işleme** için mükemmel.  
- `java.nio.file.Files` kullanarak **klasörden görüntü okuyan** mantık.  
- JPG'leri de işleyerek **PNG dosyalarından metin çıkarmak** için basit filtreler.  
- Kaynak sızıntılarını önlemek için iç thread havuzunun temiz kapatılması.

### Önkoşullar

- Java 17 (veya herhangi bir güncel LTS sürümü).  
- Aspose OCR kütüphanesini çekmek için Maven veya Gradle.  
- İşlemek istediğiniz PNG/JPG görüntülerle dolu bir klasör.  
- Java stream'lerine temel aşinalık—karmaşık bir şey gerekmez.

> **Pro ipucu:** Henüz bir lisansınız yoksa, Aspose test için kullanabileceğiniz ücretsiz geçici bir anahtar sunar.

---

## Step 1 – Projeyi Kurun ve Aspose OCR’ı Ekleyin

İlk olarak yeni bir Maven projesi oluşturun (veya Gradle, tercih size). `pom.xml` dosyasına Aspose OCR bağımlılığını ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

> **Neden önemli:** Bağımlılığı önceden bildirmeniz, derleyicinin `AsposeOCR`, `ParallelRecognizer` ve ilgili sınıfları görmesini sağlar. Ayrıca aynı sürümün tüm makinelerde kullanılmasını garantileyerek tekrarlanabilir **toplu OCR işleme** için kritik bir adımdır.

Derleme tamamlandığında IDE’nizi yenileyin; `External Libraries` altında Aspose paketlerini görmelisiniz.

---

## Step 2 – Görüntüleri Metne Dönüştür – OCR Motorunu Başlatın

Tüm çalışma süresi boyunca **tek** bir OCR motoru örneğine ihtiyacımız var. Motoru thread’ler arasında paylaşmak bellek tasarrufu sağlar ve motorun dil paketlerini yalnızca bir kez yüklemesi sayesinde hız kazanılır.

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

> **Açıklama:** `ParallelRecognizer` motoru bir thread‑havuzunda sarar. Birçok dosya gönderdiğinizde, her biri kendi çalışan thread’ine sahip olur ve çok çekirdekli CPU’larda gerçek paralellik elde edilir.

---

## Step 3 – Klasörden Görüntüleri Oku – Dizin Ağacını Dola

Şimdi **klasörden görüntü okuma** ve her PNG ya da JPG dosyasını toplama zamanı. `Files.walk` API’si bunu tek satırda yapar, ancak **PNG’den metin çıkarma** gerektiğinde filtre ekleyeceğiz.

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

> **Neden burada filtreliyoruz:** `filter` kullanarak **dosyaları uzantılarına göre filtreleme** erken aşamada yapılır, böylece gereksiz I/O azaltılır. Kod da okunabilir kalır—karmaşık regex’lere gerek kalmaz.

---

## Step 4 – Toplu OCR İşleme – İşleri Asenkron Gönder

Dosya listesi hazır olduğunda, her yolu `ParallelRecognizer`a göndeririz. `recognizeAsync` metodu bir `Future<OcrResult>` döndürür; bu da daha sonra alınmak üzere saklanır.

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

> **Arka planda ne oluyor?** Her çağrı, tanıyıcının dahili executor servisine bir görev ekler. Görevler paralel çalışır, böylece 100 resim içeren bir klasör tek‑thread’li bir döngüye göre çok daha kısa sürede işlenir.

---

## Step 5 – Sonuçları Orijinal Sırada Al – Dosya Sırasını Koruyun

`imagePaths` ile aynı sırada futures sakladığımız için, listeyi dolaşıp `get()` çağırmak yeterlidir. Bu çağrı yalnızca ilgili resim tamamlandığında bloklanır, ekstra bir sıralama yönetimi gerektirmez.

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

**Örnek konsol çıktısı** (kısaltılmış):

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

> **Köşe durumları:** Belirli bir resim bir istisna fırlatırsa (bozuk dosya, desteklenmeyen format), yakalar ve geri kalan dosyaları işlemeye devam ederiz—güvenilir **toplu OCR işleme** hatları için vazgeçilmez bir alışkanlıktır.

---

## Step 6 – Temizleme – Tanıyıcıyı Kapatın

İç thread havuzunu kapatmayı asla unutmayın; aksi takdirde JVM çıkışta takılı kalabilir.

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

Hepsi bu! Program artık herhangi bir dizini dolaşacak, PNG/JPG dosyalarını filtreleyecek, OCR’u paralel çalıştıracak ve sonuçları yazdıracak.

---

## Tam Çalışan Örnek

Aşağıda kopyala‑yapıştır‑hazır Java sınıfı yer alıyor. `"YOUR_DIRECTORY"` kısmını görüntülerinizin klasör yoluyla değiştirin ve IDE’nizden ya da komut satırından çalıştırın.

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

Sınıfı çalıştırın, konsolda çıkarılan metinlerin akışını izleyin ve **görüntüleri metne dönüştürme** işlemini tek bir I/O‑bloklayan döngü yazmadan başardığınız için kendinizi kutlayın.

---

## Sıkça Sorulan Sorular (SSS)

**S: PDF veya TIFF dosyalarını da işleyebilir miyim?**  
C: Kesinlikle. Aspose OCR birçok formatı destekler—adım 2’deki filtreye ilgili dosya uzantılarını eklemeniz yeterli.

**S: Farklı bir dil, örneğin İspanyolca, kullanmam gerekirse?**  
C: `RecognitionLanguage.ENGLISH` ifadesini `RecognitionLanguage.SPANISH` olarak değiştirin. Dil paketinin kurulu olduğundan emin olun (Aspose çoğu büyük dili kutudan çıkar çıkmaz içerir).

**S: Klasörüm alt klasörler içeriyor—taranacak mı?**  
C: Evet. `Files.walk` tüm ağaç yapısını rekürsif olarak dolaşır, bu yüzden iç içe PNG/J

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}