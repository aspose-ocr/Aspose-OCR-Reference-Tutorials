---
category: general
date: 2026-05-03
description: Java’da sabit bir iş parçacığı havuzu oluşturarak görüntülerden metni
  hızlıca çıkarın. OCR nasıl çalıştırılır, görüntüyü metne dönüştürür ve paralel OCR
  işleme ile performansı nasıl artırırsınız öğrenin.
draft: false
keywords:
- create fixed thread pool
- extract text from images
- how to run OCR
- convert image to text
- parallel OCR processing
language: tr
og_description: Java'da sabit bir iş parçacığı havuzu oluşturarak görüntülerden metni
  hızlıca çıkarın. OCR nasıl çalıştırılır, görüntüyü metne dönüştürür ve paralel OCR
  işleme ile performansı nasıl artırırsınız öğrenin.
og_title: Java'da Paralel OCR için Sabit İş Parçacığı Havuzu Oluştur
tags:
- Java
- OCR
- Multithreading
title: Java'da Paralel OCR için Sabit İş Parçacığı Havuzu Oluştur
url: /tr/java/advanced-ocr-techniques/create-fixed-thread-pool-for-parallel-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Paralel OCR için Sabit İş Parçacığı Havuzu Oluşturma (Java)

**Sabit iş parçacığı havuzu** oluşturup OCR görevlerini hızlandırmanız gerektiğinde nereden başlayacağınızı bilemediğiniz oldu mu? Yalnız değilsiniz. Görüntü‑ağırlıklı birçok projede darboğaz tek iş parçacıklı OCR çağrısıdır ve çözüm şaşırtıcı derecede basittir: bir çalışan iş parçacığı havuzu oluşturun ve dosyaları paralel olarak işleyin.  

Bu öğreticide **görüntülerden metin çıkarma** işlemini Aspose OCR kullanarak, **OCR çalıştırma** verimliliğini ve **görüntüyü metne dönüştürme** işlemini CPU’nuzu zorlamadan nasıl yapacağınızı öğreneceksiniz. Sonunda, birkaç örnek resim üzerinde **paralel OCR işleme** gösteren çalıştırmaya hazır bir Java programına sahip olacaksınız.

## Ne Oluşturacaksınız

Küçük bir konsol uygulaması oluşturacağız:

* Görüntü yollarının (PNG, JPG, TIFF, BMP) bir listesini okur.
* **CPU çekirdek sayısına** göre **sabit bir iş parçacığı havuzu** oluşturur.
* Her görüntü için bir OCR görevi gönderir.
* Tanınan metni toplar ve konsola yazdırır.
* Executor’ı temiz bir şekilde kapatır.

Harici derleme araçları, süslü framework’ler yok—sadece saf Java ve Aspose OCR kütüphanesi. Java 8+ ve bir IDE’niz varsa hazırsınız.

## Ön Koşullar

* **Java Development Kit (JDK) 8 veya daha yeni** – kod lambda kullandığı için eski sürümler derlenmez.
* **Aspose OCR for Java** – JAR dosyasını Aspose web sitesinden indirin veya Maven ile ekleyin (`com.aspose:aspose-ocr`).
* Birkaç test görüntüsü içeren bir klasör (kod `YOUR_DIRECTORY` konumuna işaret eder).  
* Java eşzamanlılığına temel aşinalık (gerisini açıklayacağız).

> *İpucu:* Maven kullanıyorsanız, bağımlılığı `pom.xml` dosyanıza ekleyin ve IDE’nin sınıf yolunu yönetmesine izin verin.  

---

## Adım 1: Gerekli İçe Aktarmaları Ekleyin

İlk olarak, ihtiyacımız olan sınıfları kapsam içine alalım. Bu sadece bir şablon değildir; her bir import JVM’e OCR motorunu, görüntü işleme yardımcılarını ve **sabit iş parçacığı havuzu** oluşturmayı sağlayan eşzamanlılık araçlarını nereden bulacağını söyler.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;
```

* `com.aspose.ocr.*` – temel OCR API’si.  
* `java.util.*` – görüntü yolları ve sonuçları depolamak için koleksiyonlar.  
* `java.util.concurrent.*` – `ExecutorService` ve `Future` gibi sınıfları barındıran eşzamanlılık paketi.

---

## Adım 2: İşlenecek Görüntüleri Tanımlayın

Şimdi **görüntülerden metin çıkarma** istediğimiz dosyaları listeleyelim. `Arrays.asList` kullanımı kodu kısa tutar ve mantıksal olarak kendi klasörünüzü eklemenize izin verir.

```java
List<String> imagePaths = Arrays.asList(
        "YOUR_DIRECTORY/image1.png",
        "YOUR_DIRECTORY/image2.jpg",
        "YOUR_DIRECTORY/image3.tif",
        "YOUR_DIRECTORY/image4.bmp"
);
```

Daha fazla giriş eklemekten çekinmeyin; iş parçacığı havuzu CPU çekirdek sayınıza göre otomatik olarak ölçeklenecektir.

---

## Adım 3: **CPU Çekirdeklerine Uygun Sabit İş Parçacığı Havuzu** Oluşturun

İşte öğreticinin kalbi. Çalışma zamanına kaç çekirdek bulunduğunu sorar ve `Executors` fabrikasından tam bu sayı kadar bir havuz isteriz. Neden sabit? Çünkü öngörülebilir bir iş parçacığı sayısı, işletim sistemini kaynak sıkıntısına sürükleyen “iş parçacığı patlamasını” önler.

```java
int coreCount = Runtime.getRuntime().availableProcessors();
ExecutorService executor = Executors.newFixedThreadPool(coreCount);
```

* `availableProcessors()` mantıksal çekirdek sayısını (hiper‑iş parçacıkları dahil) döndürür.  
* `newFixedThreadPool(coreCount)` CPU kapasitesini aşmayacağımızı garanti eder; bu da **paralel OCR çalıştırma** için en güvenli yoldur.

---

## Adım 4: Her Görüntü İçin Bir OCR Görevi Gönderin

Şimdi her dosya yolunu **OCR çalıştıran**, metni tanıyan ve sonucu döndüren bir callable’a dönüştürelim. Lambda içinde yeni bir `OcrEngine` örneği oluşturduğumuza dikkat edin—bu, motor durumunun iş parçacığı güvenli olmayan paylaşımını önler.

```java
List<Future<String>> ocrResults = new ArrayList<>();
for (String path : imagePaths) {
    ocrResults.add(executor.submit(() -> {
        OcrEngine engine = new OcrEngine();          // fresh engine per task
        engine.setImage(ImageStream.fromFile(path));
        engine.getLanguage().setEnglish(true);
        return engine.recognize() ? engine.getText()
                                   : "Failed: " + path;
    }));
}
```

* Her `submit` çağrısı lambda’yı havuza verir, havuz boş bir iş parçacığında çalıştırır.  
* `Future<String>` nesneleri, tanınan metni daha sonra almanıza olanak tanır; gerekirse sıralamayı korur.

---

## Adım 5: Tanınan Metni Alın ve Görüntüleyin

Tüm görevler kuyruğa alındıktan sonra, `Future` listesi üzerinde döngü kurup `get()` çağrısı yaparız; bu, her OCR işi bitene kadar bloklanmamızı sağlar. İşte **görüntüyü metne dönüştürme** adımının size görünür hâle geldiği yer: `engine.getText()` çağrısı ham dizeyi döndürür.

```java
for (Future<String> result : ocrResults) {
    System.out.println("OCR result:\n" + result.get());
}
```

Tipik konsol çıktısı şöyle görünür:

```
OCR result:
Hello world!
OCR result:
Invoice #12345
Date: 2026‑04‑30
...
```

Bir dosya başarısız olursa (örneğin bozuksa), `Failed:` ile başlayan ve ardından yol gelen bir satır görürsünüz—hızlı hata ayıklama için kullanışlıdır.

---

## Adım 6: Executor Servisini Temizleyin

Havuzu kapatmayı asla unutmayın; aksi takdirde JVM hâlâ çalışıyor olduğunu düşünerek kapanmayabilir. Zarif bir kapatma, çalışan görevlerin süreci sonlandırmadan önce bitmesini sağlar.

```java
executor.shutdown();
```

Zaman aşımı uygulamanız gerekiyorsa `awaitTermination` da çağırabilirsiniz, ancak çoğu komut‑satırı aracında basit bir `shutdown()` yeterlidir.

---

## Tam Çalışan Örnek

Aşağıda eksiksiz, çalıştırmaya hazır program yer alıyor. `ParallelOcrTutorial.java` adlı bir dosyaya kopyalayıp yapıştırın, görüntü yollarını ayarlayın ve normal şekilde `javac` + `java` komutlarıyla çalıştırın.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;

public class ParallelOcrTutorial {
    public static void main(String[] args) throws Exception {
        // Step 2: Define the images to be processed
        List<String> imagePaths = Arrays.asList(
                "YOUR_DIRECTORY/image1.png",
                "YOUR_DIRECTORY/image2.jpg",
                "YOUR_DIRECTORY/image3.tif",
                "YOUR_DIRECTORY/image4.bmp"
        );

        // Step 3: Create a fixed‑size thread pool matching the CPU cores
        int coreCount = Runtime.getRuntime().availableProcessors();
        ExecutorService executor = Executors.newFixedThreadPool(coreCount);

        // Step 4: Submit an OCR task for each image
        List<Future<String>> ocrResults = new ArrayList<>();
        for (String path : imagePaths) {
            ocrResults.add(executor.submit(() -> {
                OcrEngine engine = new OcrEngine();          // fresh engine per task
                engine.setImage(ImageStream.fromFile(path));
                engine.getLanguage().setEnglish(true);
                return engine.recognize() ? engine.getText()
                                           : "Failed: " + path;
            }));
        }

        // Step 5: Retrieve and display the recognized text
        for (Future<String> result : ocrResults) {
            System.out.println("OCR result:\n" + result.get());
        }

        // Step 6: Clean up the executor service
        executor.shutdown();
    }
}
```

**Beklenen sonuç:** her görüntünün metin içeriği konsola, `imagePaths` listesindeki aynı sırayla yazdırılır. İşlenemeyen bir görüntü varsa, boş satır yerine bir hata bildirimi görürsünüz.

---

## Yaygın Sorular & Kenar Durumları

### Daha fazla görüntüm olduğunda iş parçacıklarından az kalırsa ne olur?

Sabit iş parçacığı havuzu fazla görevleri otomatik olarak kuyruğa alır. Bir iş parçacığı mevcut OCR görevini bitirdiğinde bir sonraki görevi alır. Bu kuyruklama davranışı **paralel OCR işleme** nin özüdür—CPU’yu aşırı yüklemeden maksimum verim elde edersiniz.

### Dili değiştirebilir miyim?

Kesinlikle. `engine.getLanguage().setEnglish(true);` satırını uygun dil bayrağıyla değiştirin; örneğin `setFrench(true)` ya da `recognize()` öncesinde birden fazla dil etkinleştirmek için birkaç setter çağırın.

### Çok büyük görüntülerle nasıl başa çıkılır?

Büyük dosyalar iş parçacığı başına çok bellek tüketebilir. `OutOfMemoryError` alırsanız, motoru beslemeden önce görüntüyü küçültmeyi ya da `-Xmx` ile yığın boyutunu artırmayı düşünün. Başka bir yaklaşım **cached thread pool** kullanmaktır (`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}