---
category: general
date: 2026-02-27
description: Aspose OCR'nin paralel işleme özelliğini kullanarak Java'da OCR nasıl
  kullanılır, TIFF ve PDF dosyalarından görüntü metni çıkarılır öğrenin. Hızlı, basit
  rehber.
draft: false
keywords:
- how to use ocr
- perform ocr on pdf
- extract text from tiff
- extract image text java
language: tr
og_description: Aspose OCR'nin paralel işleme özelliğini kullanarak Java'da OCR ile
  TIFF ve PDF dosyalarından görüntü metni çıkarmayı öğrenin.
og_title: Java'da OCR Nasıl Kullanılır – Aspose ile Paralel İşleme
tags:
- OCR
- Java
- Aspose
title: Java'da OCR Nasıl Kullanılır – Aspose ile Paralel İşleme
url: /tr/java/advanced-ocr-techniques/how-to-use-ocr-in-java-parallel-processing-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java’da OCR Nasıl Kullanılır – Aspose ile Paralel İşleme

Hiç **OCR nasıl kullanılır** diye merak ettiniz mi, taranmış bir belgeden metni zahmetsizce çıkarmak? Tek başınıza değilsiniz. Geliştiriciler, özellikle TIFF ve PDF dosyalarından metin okuma ihtiyacı duyduklarında ve performansı kontrol altında tutmak zorunda kaldıklarında sürekli bir engelle karşılaşıyor.  

Bu öğreticide, Aspose OCR kullanarak **extracts image text in Java** yapan, paralel işleme açan ve hatta iş parçacığı sayısını sınırlamanıza izin veren eksiksiz, çalıştırmaya hazır bir çözüm göstereceğiz. Sonunda, **perform OCR on PDF** dosyaları ve **extract text from TIFF** görüntülerinden metin çıkarabilen tek bir sınıfa sahip olacaksınız; bu, tek iş parçacıklı bir yaklaşımın alacağı sürenin bir kısmı kadar sürecek.

> **Neler Öğreneceksiniz**  
> * Paralel OCR neden önemli, bunun net bir açıklaması.  
> * Eksiksiz bir Java programı (eksik import yok).  
> * İş parçacığı kullanımını ayarlama ve yaygın tuzakları ele alma ipuçları.  

## Önkoşullar

- Java 8 ve üzeri (kod JDK 11 ile de derlenir).  
- Aspose.OCR for Java kütüphanesi – en son JAR dosyasını Maven Central’dan (`com.aspose:aspose-ocr`) alabilirsiniz.  
- İşlemek istediğiniz bir görüntü dosyası (`.tif`, `.tiff`) veya PDF.  
- Makul bir RAM miktarı—paralel işleme birkaç iş parçacığı başlatacak, ancak Aspose bellek‑verimli.

Eğer bunlara sahipseniz, başlayalım.

![OCR işlem hattını gösteren diyagram – Java’da paralel işleme ile OCR nasıl kullanılır](how-to-use-ocr-pipeline.png)

*Görsel alt metni: OCR örnek diyagramı*

---

## Adım 1: Projenizi Kurun ve Aspose OCR’yi Ekleyin

### Bunun Önemi

PDF üzerinde **perform OCR on PDF** ya da herhangi bir görüntü işleyebilmeniz için kütüphane sınıf yolunuzda (classpath) bulunmalıdır. Olmazsa derleyici `ClassNotFoundException` hatası verir ve ikinci adımda takılı kalırsınız.

### Nasıl Yapılır

Eğer Maven kullanıyorsanız, bağımlılığı ekleyin:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check for the newest version -->
</dependency>
```

Gradle için:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Pro tip:** Versiyon numarasını Aspose sürüm notlarıyla senkronize tutun; yeni sürümler genellikle paralel işleme için performans iyileştirmeleri içerir.

---

## Adım 2: OCR Motorunu Oluşturun ve Paralel İşlemeyi Etkinleştirin

### Bunun Önemi

Varsayılan olarak Aspose OCR tek bir iş parçacığında çalışır. Çok sayfalı bir PDF ya da bir dizi TIFF dosyası verdiğinizde, motor her sayfayı sırayla işler—yavaş ve verimsiz. Paralel işleme etkinleştirildiğinde CPU aynı anda birkaç sayfayı işleyebilir, bu da çalışma süresini büyük ölçüde azaltır.

### Kod

```java
import com.aspose.ocr.*;

public class ParallelOcrDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Path to the input file (TIFF or PDF)
        String inputPath = "YOUR_DIRECTORY/input.tif";

        // 2️⃣ Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Turn on parallel processing – this is the core of how to use OCR efficiently
        ocrEngine.getConfig().setUseParallelProcessing(true);

        // 4️⃣ (Optional) Limit threads – you can cap it to the number of cores you have
        // ocrEngine.getConfig().setMaxThreads(Runtime.getRuntime().availableProcessors());

        // 5️⃣ Run OCR
        OcrResult ocrResult = ocrEngine.processImage(inputPath);

        // 6️⃣ Output the recognised text
        System.out.println(ocrResult.getText());
    }
}
```

**Ana satırların açıklaması**

- `setUseParallelProcessing(true)`: Aspose’a iş yükünü mevcut CPU çekirdekleri arasında bölmesini söyler.  
- `setMaxThreads(...)`: Paylaşımlı bir sunucuda iseniz veya diğer hizmetler için kaynak bırakmak istiyorsanız iş parçacığı havuzunu sınırlayabilirsiniz.  
- `processImage(inputPath)`: hem görüntü dosyaları hem de PDF belgeleri için çalışır, bu yüzden aynı çağrı **perform OCR on PDF** ve TIFF için de aynı şekilde çalışır.

---

## Adım 3: Farklı Girdi Türlerini İşleme – PDF vs. TIFF

### Bunun Önemi

`processImage` bir yol dizesi kabul etse de, altında yatan işleme farklılık gösterir. PDF'ler genellikle birden çok sayfa içerir ve her biri ayrı bir OCR işi olur. TIFF'ler tek sayfa ya da çok sayfalı olabilir; Aspose her çerçeveyi bir sayfa olarak ele alır.

### Dikkat Edilmesi Gerekenler

| Girdi | Tipik Sorun | Önerilen Çözüm |
|------|----------------|-----------------|
| PDF | Büyük PDF'ler tüm sayfalar aynı anda yüklendiğinde belleği tüketebilir. | `ocrEngine.getConfig().setMemoryOptimization(true);` kullanın (yeni sürümlerde mevcut). |
| Çok‑sayfalı TIFF | Bazı eski TIFF'ler desteklenmeyen sıkıştırma kullanır. | Önce desteklenen bir formata dönüştürün veya Aspose’un `TiffImage` yardımcı sınıfını kullanın. |

İşte dosya tipini tespit edip dostça bir mesaj kaydeden hızlı bir kod parçacığı:

```java
import java.nio.file.*;

String ext = Files.probeContentType(Paths.get(inputPath)).toLowerCase();
if (ext.contains("pdf")) {
    System.out.println("Processing a PDF – expect multiple pages.");
} else if (ext.contains("tiff") || ext.contains("tif")) {
    System.out.println("Processing a TIFF image.");
} else {
    System.out.println("Unsupported file type. This demo works with PDF and TIFF.");
}
```

---

## Adım 4: Çıktıyı Doğrulama – Ne Görmelisiniz?

Program tamamlandığında, ham çıkarılan metin konsola yazdırılır. Basit bir taranmış faturada çıktı şu şekilde görünebilir:

```
Invoice #12345
Date: 02/15/2026
Total Amount: $1,250.00
Thank you for your business!
```

OCR belirli bir sayfada zorlanırsa, Aspose `[Unrecognizable]` gibi bir yer tutucu satır ekler. Temiz veri ihtiyacınız varsa daha sonra bunları filtreleyebilirsiniz.

**Hızlı doğrulama**

```java
if (ocrResult.getText().trim().isEmpty()) {
    System.err.println("No text detected – verify the image quality or try a different language.");
}
```

---

## Adım 5: Performansı Ayarlama – İş Parçacığı Sayısını Ne Zaman Değiştirmeli

### Bunun Önemi

Daha fazla iş parçacığı her zaman daha hızlı sonuç anlamına gelmez. 4 çekirdekli bir dizüstü bilgisayarda 8 iş parçacığı başlatmak bağlam geçişi yükü oluşturabilir. Öte yandan, 32 çekirdekli bir sunucuda tam gücü ortaya çıkarmak isteyebilirsiniz.

### En Uygun Ayarı Nasıl Bulursunuz

```java
int cores = Runtime.getRuntime().availableProcessors();
System.out.println("Available processors: " + cores);

// Experiment: set max threads to half the cores first
ocrEngine.getConfig().setMaxThreads(Math.max(1, cores / 2));
```

Programı farklı ayarlarla çalıştırın ve süresini ölçün:

```java
long start = System.nanoTime();
ocrEngine.processImage(inputPath);
long elapsed = System.nanoTime() - start;
System.out.println("Elapsed time (ms): " + elapsed / 1_000_000);
```

Zamanları kaydedin, size en yüksek verimi veren yapılandırmayı seçin ve üretimde bunu sabitleyin.

---

## Adım 6: Demo’yu Genişletme – Birden Çok Dosyayı Toplu İşleme

Eğer bir klasörden **extract image text java** almanız gerekiyorsa, temel mantığı bir döngüye sarın:

```java
Path folder = Paths.get("YOUR_DIRECTORY");
try (DirectoryStream<Path> stream = Files.newDirectoryStream(folder, "*.{tif,tiff,pdf}")) {
    for (Path file : stream) {
        System.out.println("\n--- Processing: " + file.getFileName() + " ---");
        OcrResult result = ocrEngine.processImage(file.toString());
        // Save or further process result.getText()
    }
}
```

Bu desen iyi ölçeklenir çünkü motor zaten her dosyanın sayfalarını paralel olarak çalıştırır. Dış döngü sıralı çalışır, ancak büyük bir CPU çiftliğini doldurmak isterseniz her dosyayı bir `ExecutorService`'e de gönderebilirsiniz.

---

## Yaygın Tuzaklar ve Nasıl Kaçınılır

| Belirti | Muhtemel neden | Çözüm |
|---------|----------------|------|
| `OutOfMemoryError` | Çok sayıda sayfa aynı anda yükleniyor (özellikle büyük PDF'lerde). | Bellek optimizasyonunu etkinleştirin (`setMemoryOptimization(true)`) veya PDF'leri sayfa‑sayfa işlemek için `processPage` kullanın. |
| Bozuk karakterler | Yanlış dil/karakter seti yapılandırması. | `ocrEngine.getConfig().setLanguage(OcrLanguage.English);` gibi uygun dil enumunu çağırın. |
| Paralel bayrağına rağmen yavaş performans | OS iş parçacığı oluşturma limitleri veya JVM düşük heap boyutuyla çalışıyor. | `-Xmx` heap bayrağını artırın ve OS iş parçacığı limitlerini (`ulimit -u`) kontrol edin. |
| Boş çıktı | Girdi görüntü çözünürlüğü 300 dpi'den düşük. | OCR öncesinde görüntüyü yükseltin veya daha yüksek çözünürlükte tarama yapan bir tarayıcı kullanın. |

---

## Özet – Neler Ele Aldık

- **How to use OCR** in Java with Aspose’s `OcrEngine`.  
- **parallel processing** etkinleştirerek **perform OCR on PDF** ve **extract text from TIFF** hızlandırması.  
- Optimum performans için iş parçacığı sayısının ayarlanması.  
- Büyük PDF'ler, çok‑sayfalı TIFF'ler ve dil ayarları gibi uç durumların ele alınması.  
- Tek dosya demosunu gerçek dünya iş yükleri için toplu işleyiciye genişletmek.

---

## Sonraki Adımlar

Artık temelleri kavradığınıza göre, aşağıdaki ilgili konuları keşfetmeyi düşünün:

- **Extract image text java** el yazısı notlardan ( `setHandwritingRecognition(true)` etkinleştirin).  
- OCR çıktısını meta veri çıkarımı için Apache Tika ile bütünleştirme.  
- Sonuçları aranabilir belge arşivleri için Elasticsearch'te saklama.  
- Aspose OCR'yi Python veya .NET gibi diğer dillerle kullanma—prensipler aynı kalır.

Farklı iş parçacığı limitleri, görüntü formatları ve dil paketleriyle denemeler yapmaktan çekinmeyin. Ne kadar çok denerseniz, hız ve doğruluk arasındaki dengeyi o kadar iyi anlarsınız.

### Kodlamaktan keyif alın!

Eğer bir sorunla karşılaşırsanız veya daha fazla optimizasyon fikriniz varsa, aşağıya yorum bırakın. OCR ipuçları üzerine her zaman bir tartışmaya hazırım—zorluk yok, sadece kod.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}