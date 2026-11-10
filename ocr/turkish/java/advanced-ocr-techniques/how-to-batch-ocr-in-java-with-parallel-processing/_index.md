---
category: general
date: 2026-04-26
description: Java ve Aspose OCR kullanarak toplu OCR nasıl yapılır – görüntülerden
  metin tanıma, PNG'den metin çıkarma ve paralel OCR işleme için tüm CPU çekirdeklerini
  kullanma.
draft: false
keywords:
- how to batch OCR
- recognize text from images
- extract text from PNG
- use all CPU cores
- parallel OCR processing
language: tr
og_description: Java'da toplu OCR nasıl yapılır. Görüntülerden metin tanımayı öğrenin,
  PNG'den metin çıkarın ve hızlı paralel OCR işleme için tüm CPU çekirdeklerini kullanın.
og_title: Java'da Toplu OCR Nasıl Yapılır – Paralel İşleme Rehberi
tags:
- OCR
- Java
- Aspose
- Performance
title: Java'da Paralel İşleme ile Toplu OCR Nasıl Yapılır
url: /tr/java/advanced-ocr-techniques/how-to-batch-ocr-in-java-with-parallel-processing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da Toplu OCR Nasıl Yapılır – Tam Kılavuz

On binlerce PNG ekran görüntüsüyle karşı karşıya kaldığınızda **toplu OCR nasıl yapılır** diye merak ettiniz mi? Yalnız değilsiniz. Çoğu geliştirici, tek‑resim demosu çalıştıktan ve gerçek iş yükü—yüzlerce dosya—CPU'yu boğmaya başladığında bir duvara çarpar.  

Bu öğreticide, **görüntülerden metin tanıyan**, her PNG'nin içeriğini çıkaran ve **tüm CPU çekirdeklerini** kullanarak işi hızlandıran pratik, uçtan uca bir çözümü adım adım inceleyeceğiz. Sonunda, bir klasördeki resimleri paralel işleyen, çok‑iş parçacıklı bir motorun hızını size sağlayan yeniden kullanılabilir bir Java sınıfına sahip olacaksınız, kendi iş parçacığı havuzlarınızı yönetme derdi olmadan.

> **Ne elde edeceksiniz:** tamamen çalıştırılabilir bir Java programı (Aspose OCR), adım adım açıklamalar, uç durumlar için ipuçları ve beklenen konsol çıktısının bir ön izlemesi.

---

## Önkoşullar

- **Java 17** (veya herhangi bir yeni JDK) yüklü ve `JAVA_HOME` yapılandırılmış.  
- **Aspose OCR for Java** kütüphanesi (sürüm 23.10 veya daha yeni). Maven Central'dan alabilirsiniz:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

- İşlemek istediğiniz bir avuç **PNG görüntüsü** içeren bir klasör.  
- Java sözdizimi hakkında temel bir aşinalık—karmaşık bir şey gerekmez.

Eğer bunlardan biri size yabancı geliyorsa, burada durup kurulumunu yapın; rehberin geri kalanı bunların hazır olduğunu varsayar.

## Adım 1 – Tek‑İş Parçacıklı OCR Motoru Oluşturun (Temel Çizgi)

İlk olarak, `OcrEngine` nesnesini örnekleyin. Bu nesne ağır işi yapar—görüntüyü yükler, sinir ağını çalıştırır ve düz metin döndürür.

```java
import com.aspose.ocr.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **Neden önemli:** Aynı motoru birçok dosyada yeniden kullanmak, dil modellerini tekrar tekrar yükleme yükünden kaçınır; bu, **toplu işleme** yaptığınızda performans düşürücü olabilir.

## Adım 2 – Tüm Kullanılabilir Çekirdeklerle Paralel İşlemeyi Etkinleştirin

Şimdi Aspose OCR'ye işi, makinenizin sunduğu her mantıksal işlemciye yaymasını söylüyoruz. `Runtime.getRuntime().availableProcessors()` çağrısı, 4‑çekirdekli bir dizüstü bilgisayar ya da 32‑çekirdekli bir sunucu olsun, bu sayıyı döndürür.

```java
        // Step 2: Enable parallel processing by using all available logical processors
        ocrEngine.getRecognitionSettings()
                 .setNumberOfThreads(Runtime.getRuntime().availableProcessors());
```

> **Pro ipucu:** Hyper‑threaded bir CPU'da çekirdek sayısının iki katını göreceksiniz, ancak kütüphane iş parçacığı havuzunu akıllıca sınırlıyor, bu yüzden elle ince ayar yapmanıza gerek yok.

## Adım 3 – İşlemek İstediğiniz Görüntüleri Toplayın

Küçük bir dizi sabit kodlamak bir demo için işe yarar, ancak gerçek‑dünya toplu işinde muhtemelen bir dizini tararsınız. Aşağıda her iki yaklaşımı da gösteriyoruz.

```java
        // Step 3a: Define a static list (quick demo)
        String[] imageFiles = {
            "YOUR_DIRECTORY/image1.png",
            "YOUR_DIRECTORY/image2.png",
            "YOUR_DIRECTORY/image3.png"
        };

        // Step 3b: Or, dynamically load every PNG in a folder
        // File folder = new File("YOUR_DIRECTORY");
        // String[] imageFiles = folder.list((dir, name) -> name.toLowerCase().endsWith(".png"));
```

> **Neden buna ihtiyacınız olabilir:** Yükleme hattı üzerinden gelen **PNG'den metin çıkarmak** zorundaysanız, dinamik sürüm kod değişikliği yapmadan yeni dosyaları otomatik olarak yakalar.

## Adım 4 – Aynı Motoru Kullanarak Her Görüntüde OCR Çalıştırın

Aşağıdaki döngü mevcut resmi ayarlar, `recognize()` metodunu çalıştırır ve sonucu yazdırır. Daha önce çok‑iş parçacıklı çalışmayı etkinleştirdiğimiz için, her çağrı sahne arkasında ayrı bir işçi iş parçacığında çalışabilir.

```java
        // Step 4: Recognize text from each image (reusing the same engine instance)
        for (String imagePath : imageFiles) {
            ocrEngine.setImage(imagePath);
            String recognizedText = ocrEngine.recognize().getText();
            System.out.println("Result for " + imagePath + ":\n" + recognizedText);
        }
    }
}
```

### Beklenen Konsol Çıktısı

```
Result for YOUR_DIRECTORY/image1.png:
Welcome to the OCR demo.
Result for YOUR_DIRECTORY/image2.png:
Invoice #12345
Total: $567.89
Result for YOUR_DIRECTORY/image3.png:
© 2026 MyCompany. All rights reserved.
```

Görüntüler Latin dışı alfabeler içeriyorsa ya da düşük çözünürlüklü ekran görüntüleri ise bozuk karakterler görebilirsiniz—motorun DPI veya gürültü‑azaltma ayarlarını buna göre düzenleyin (aşağıdaki “Gelişmiş Ayarlamalar” bölümüne bakın).

## Gelişmiş Ayarlamalar – Gerçek‑Dünya Toplu İşler İçin İnce Ayar

| Durum | Önerilen Ayar | Kod Parçası |
|-----------|-------------------|--------------|
| Düşük çözünürlüklü PNG'ler | `setResolution` artır | `ocrEngine.getRecognitionSettings().setResolution(300);` |
| Karışık dil belgeleri | Dil paketleri ekle | `ocrEngine.getRecognitionSettings().addLanguage(OcrLanguage.Spanish);` |
| Çok büyük toplular (10k+ dosya) | Tüm adları bir kerede yüklemek yerine dosyaları akış olarak işleyin | Use `Files.walk(Paths.get("YOUR_DIRECTORY"))` with a filter. |
| Bellek kısıtlamaları | Her N dosyadan sonra motoru serbest bırak | `if (counter % 500 == 0) ocrEngine.dispose();` |

> **Unutmayın:** **Tüm CPU çekirdeklerini** kullansak da, işletim sistemi hâlâ iş parçacığı zamanlamasını yönetir. Makinenizin yavaşladığını fark ederseniz, iş parçacıklarını `availableProcessors() - 1` değerine sınırlamayı düşünün.

## Yaygın Tuzaklar ve Nasıl Kaçınılır

1. **Dosya tanıtıcılarının tükenmesi** – Java, süreç başına açık dosya sayısını sınırlar. `Too many open files` hatası alırsanız her görüntüyü açıkça kapatın:

   ```java
   ocrEngine.setImage(imagePath);
   String text = ocrEngine.recognize().getText();
   ocrEngine.getImage().close(); // releases the handle
   ```

2. **Windows'ta yanlış yol ayırıcıları** – Platform‑bağımsız kalmak için `File.separator` ya da `Paths.get()` kullanın.

3. **İş parçacığı‑güvensiz özel geri çağırmalar** – Bir ilerleme dinleyicisi ekliyorsanız, bunun iş parçacığı‑güvenli olduğundan emin olun (ör. `AtomicInteger`).

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

```java
import com.aspose.ocr.*;
import java.io.File;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable parallelism – use every logical CPU core
        ocrEngine.getRecognitionSettings()
                 .setNumberOfThreads(Runtime.getRuntime().availableProcessors());

        // 3️⃣ Locate PNG files (adjust the folder path)
        File folder = new File("YOUR_DIRECTORY");
        String[] imageFiles = folder.list((dir, name) ->
                name.toLowerCase().endsWith(".png"));

        if (imageFiles == null || imageFiles.length == 0) {
            System.out.println("No PNG files found in the directory.");
            return;
        }

        // 4️⃣ Process each image – same engine, multi‑threaded under the hood
        for (String imageName : imageFiles) {
            String imagePath = folder.getAbsolutePath() + File.separator + imageName;
            ocrEngine.setImage(imagePath);
            String recognizedText = ocrEngine.recognize().getText();

            System.out.println("Result for " + imagePath + ":\n" + recognizedText);
            // Optional: free the image handle (good for huge batches)
            ocrEngine.getImage().close();
        }

        // Clean up
        ocrEngine.dispose();
    }
}
```

> **Bu ne yapar:** `YOUR_DIRECTORY` içinde bulunan her `.png` dosyasını tarar, OCR'yi paralel olarak çalıştırır, her sonucu yazdırır ve sonunda kaynakları serbest bırakır. Bu sınıfı herhangi bir Maven projesine ekleyebilir, `mvn exec:java` komutunu çalıştırabilir ve tek‑iş parçacıklı bir döngüye göre hız artışını izleyebilirsiniz.

## Sonuç

Artık Java'da **toplu OCR nasıl yapılır** konusunda sağlam, üretim‑hazır bir deseniniz var. Tek bir `OcrEngine` yeniden kullanarak, **paralel OCR işleme**yi etkinleştirerek ve **tüm CPU çekirdeklerini** kullanarak, **görüntülerden metin tanıma** işlemini naif bir döngünün alacağı sürenin bir kısmına indirgemiş olacaksınız.  

Bundan sonra şunları yapabilirsiniz:

- Çıktıyı hızlı arama için bir arama indeksine (Elasticsearch) bağlayın.  
- PDF‑to‑PNG dönüştürücü ile birleştirerek taranmış belgelerde gömülü **PNG'den metin çıkarmak** işlemini gerçekleştirin.  
- Güvenilir olmayan ağ‑bağlı sürücüler için hata yönetimi ve yeniden deneme mantığı ekleyin.

Denemeye devam edin—JPEG'lere geçin, DPI'yi ayarlayın ya da gerçek‑zamanlı transkripsiyon için video karelerini besleyin. Temel fikirler aynı kalır ve performans kazanımları genellikle çarpıcıdır.

Kodlamanın tadını çıkarın, OCR boru hatlarınız kahve makineniz kadar hızlı çalışsın! 🚀

![Paralel OCR iş akışını gösteren diyagram – birden fazla CPU çekirdeği üzerinde toplu OCR nasıl yapılır]

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}