---
category: general
date: 2026-03-18
description: Aspose OCR for Java kullanarak OCR'yi hızlı bir şekilde nasıl etkinleştirirsiniz.
  Görüntüden metin tanımayı, maksimum paralellik ayarlamayı, PNG'den metin çıkarmayı
  ve OCR için görüntü yüklemeyi öğrenin.
draft: false
keywords:
- how to enable OCR
- recognize text from image
- set max parallelism
- extract text from png
- load image for OCR
language: tr
og_description: Aspose OCR for Java ile OCR'yi nasıl etkinleştirirsiniz. Bu kılavuz,
  görüntüden metin tanıma, maksimum paralellik ayarlama, PNG'den metin çıkarma ve
  OCR için görüntü yükleme konularını gösterir.
og_title: Java'da OCR Nasıl Etkinleştirilir – Tam Kılavuz
tags:
- Aspose OCR
- Java
- Parallel Processing
title: Aspose ile Java’da OCR’yi Etkinleştirme – Tam Adım Adım Rehber
url: /tr/java/ocr-operations/how-to-enable-ocr-in-java-with-aspose-complete-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da OCR'ı Etkinleştirme – Tam Adım‑Adım Kılavuz

Java uygulamanızda **OCR'ı nasıl etkinleştireceğinizi** API belgelerinde günlerce araştırmadan merak ettiniz mi? Tek başınıza değilsiniz. Çoğu geliştirici, özellikle büyük PNG dosyalarında **görüntüden metin tanıma** ihtiyacıyla karşılaştığında performansı kabul edilebilir seviyede tutmakta zorlanıyor.  

İyi haber? Aspose OCR ile düğmeyi çevirip OCR için bir görüntü yükleyebilir ve hatta CPU çekirdeklerini artırarak işlemleri hızlandırabilirsiniz. Bu öğreticide ihtiyacınız olan her şeyi adım adım göstereceğiz: kütüphaneyi kurma, PNG yükleme, maksimum paralellik derecesini ayarlama ve sonunda metni çıkarma. Sonunda **PNG dosyalarından metin çıkaran** çalıştırılabilir bir programınız olacak.

### İhtiyacınız Olanlar

- Java 17 veya üzeri (kod eski sürümlerle de derlenebilir, ancak 17 en uygun sürümdür)
- Maven veya Gradle, Aspose OCR JAR'ını çekmek için (Maven örneğini göstereceğiz)
- Aranabilir metin içeren bir PNG görüntüsü (paralellik için ne kadar büyükse o kadar iyi)
- Biraz merak—önceden OCR deneyimi gerekmez

Eğer bunlardan herhangi biri size yabancı geliyorsa panik yapmayın. Girişten hemen sonra ön koşulları ele alacağız ve kurulumu hızlıca yapmanız için komutları vereceğiz.

---

## Adım 1: Java için Aspose OCR'ı Kurun

**OCR'ı etkinleştirmeden** önce, kütüphanenin sınıf yolunuzda (classpath) olması gerekir. En kolay yol, Maven bağımlılığını eklemektir:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

> **Pro ipucu:** Gradle kullanıyorsanız eşdeğeri  
> `implementation 'com.aspose:aspose-ocr:23.12'`.  

Bağımlılık çözüldükten sonra IDE'niz JAR'ları otomatik olarak indirecek. Manuel JAR işlemi gerekmez.

## Adım 2: OCR için Görüntüyü Yükleyin

İlk pratik adım **OCR için görüntüyü yüklemektir**. Aspose, dosya yolu ya da akış kabul eden statik bir `Image.load` metodu sunar. Basit tutalım ve bir dosya yolu kullanalım:

```java
import com.aspose.ocr.Image;

// ...

// Replace with the absolute or relative path to your PNG
String imagePath = "src/main/resources/large-document.png";
Image image = Image.load(imagePath);
```

> **Neden önemli:** Görüntüyü bir kez yükleyip aynı `Image` örneğini yeniden kullanmak, aynı dosya üzerinde (ör. farklı dil ayarları) birden fazla tanıma çalıştırdığınızda ekstra G/Ç'yi önler.

Dosya bulunamazsa Aspose bir `IOException` fırlatır. Üretimde bunu bir try‑catch bloğuna alır ve belki varsayılan bir görüntüye geri dönersiniz.

## Adım 3: OCR Motorunu Oluşturun ve Paralel İşlemeyi Etkinleştirin

Şimdi konunun özüne geliyoruz—**paralellik ile OCR'ı nasıl etkinleştireceğiniz**. `OcrEngine` sınıfı ağır işi yapar ve `ParallelSettings` ile iş parçacıklarını kontrol edebilirsiniz.

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.ParallelSettings;

// ...

OcrEngine ocrEngine = new OcrEngine();

// Turn on parallel processing
ParallelSettings parallelSettings = new ParallelSettings();
parallelSettings.setEnabled(true);

// Set the maximum number of threads to the number of available CPU cores
int cores = Runtime.getRuntime().availableProcessors();
parallelSettings.setMaxDegreeOfParallelism(cores);

// Apply the settings to the engine
ocrEngine.setParallelSettings(parallelSettings);
```

### Neden `MaxDegreeOfParallelism` ayarlamalısınız?

- **Performans:** Büyük PNG'ler binlerce metin parçacığı içerebilir. Varsayılan olarak Aspose bunları sıralı işler, bu da çok çekirdekli makinelerde yavaş olabilir.
- **Kontrol:** Paylaşımlı bir sunucuda diğer hizmetlerin kaynak bulamamasını önlemek için iş parçacıklarını sınırlamak isteyebilirsiniz. `cores` değerini buna göre ayarlayın.

## Adım 4: Görüntüden Metni Tanıyın

Motor hazır olduğunda, gerçek OCR çağrısı tek satırdır:

```java
String recognizedText = ocrEngine.recognize(image);
```

Arka planda Aspose görüntüyü bloklara ayırır, her bloğu sinir ağı üzerinden çalıştırır ve sonuçları birleştirir. Paralelliği etkinleştirdiğimiz için bu bloklar eşzamanlı olarak işlenir.

## Adım 5: Çıkarılan Metni Çıktılayın veya Saklayın

Son olarak, sonuçla ne yapacağınıza karar verin. Hızlı bir demo için konsola yazdıracağız, ancak bir dosyaya, veritabanına yazabilir ya da bir sonraki NLP hattına besleyebilirsiniz.

```java
System.out.println("=== OCR Result ===");
System.out.println(recognizedText);
```

Eğer toplu olarak **PNG dosyalarından metin çıkarmanız** gerekiyorsa, yukarıdaki adımları bir dizini dolaşan bir döngüye sarın. Aynı `OcrEngine` örneğini yeniden kullanmayı unutmayın—her dosya için yeni bir motor oluşturmak paralelliğin amacını bozar.

## Tam Çalışan Örnek

Her şeyi bir araya getirerek, işte tam, çalıştırmaya hazır bir Java sınıfı. `src/main/java/com/example/ParallelOcrDemo.java` içine kopyalayıp yapıştırın ve `mvn compile exec:java` komutunu çalıştırın.

```java
package com.example;

import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.ParallelSettings;
import com.aspose.ocr.Image;

/**
 * Demonstrates how to enable OCR with Aspose, set max parallelism,
 * load an image for OCR, and extract text from a PNG file.
 */
public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable parallel processing to speed up recognition
        ParallelSettings parallelSettings = new ParallelSettings();
        parallelSettings.setEnabled(true);
        // Use all available CPU cores; adjust if you need to limit resources
        parallelSettings.setMaxDegreeOfParallelism(
                Runtime.getRuntime().availableProcessors()
        );
        ocrEngine.setParallelSettings(parallelSettings);

        // Step 3: Load the image that contains the text to be recognized
        // Replace the path with your own PNG file location
        Image image = Image.load("src/main/resources/large-document.png");

        // Step 4: Perform OCR on the loaded image
        String recognizedText = ocrEngine.recognize(image);

        // Step 5: Output the recognized text
        System.out.println("=== OCR Result ===");
        System.out.println(recognizedText);
    }
}
```

### Beklenen Çıktı

`large-document.png` dosyası “Hello World” ifadesini içeriyorsa, aşağıdaki gibi bir çıktı göreceksiniz:

```
=== OCR Result ===
Hello World
```

Çok sayfalı taramalar için çıktı, her metin satırını ayıran satır sonları (`\n`) içeren tek bir dize olacaktır.

## Yaygın Sorular & Kenar Durumları

| Soru | Cevap |
|------|-------|
| **PNG çok büyük olursa (ör. 10 000 × 10 000 px)?** | Aspose görüntüyü otomatik olarak döşer. Daha ince kontrol gerekiyorsa `OcrEngine.setTileSize(int width, int height)` ile döşeme boyutunu ayarlayabilirsiniz. |
| **Bellek kullanımını sınırlayabilir miyim?** | Evet—düşük donanımlı makinelerde OutOfMemory hatalarını önlemek için `ocrEngine.setMemoryLimit(long bytes)` ayarlayın. |
| **Paralellik Windows ve Linux'ta aynı şekilde çalışıyor mu?** | Kesinlikle. `ParallelSettings` soyutlaması Java’nın `ForkJoinPool`'unu kullanır ve bu platformlar arasıdır. |
| **Hangi diller destekleniyor?** | Kutudan çıkar çıkmaz 100'den fazla dil desteklenir. İngilizce için `ocrEngine.setLanguage("eng")`, İspanyolca için `"spa"` gibi çağırın. |
| **Sadece sayıları tanımak istiyorum.** | Karakter kümesini sınırlamak için `ocrEngine.setCharacterWhitelist("0123456789")` kullanın. |

## Üretim‑Hazır OCR için İpuçları

1. **`OcrEngine`'i önbellekle** – Tekrar tekrar oluşturmak ek yük getirir. Birçok görüntü işliyorsanız tek bir örnek (singleton) tutun.
2. **Girdiyi doğrula** – Motorun içine vermeden önce dosya boyutunu ve boyutlarını kontrol edin; çok büyük dosyalar paralellik olmasına rağmen JVM'i zorlayabilir.
3. **İş Parçacığı Havuzu Ayarı** – Uygulamanız JVM'i diğer hizmetlerle paylaşıyorsa, iyi bir vatandaş olmak için `parallelSettings.setMaxDegreeOfParallelism(Runtime.getRuntime().availableProcessors() / 2)` ayarlamayı düşünün.
4. **Son‑İşleme** – OCR mükemmel değildir. Özellikle taranmış tablolar için doğruluğu artırmak amacıyla bir yazım denetleyicisi veya regex temizliği kullanın.

## Sonuç

Aspose kullanarak Java'da **OCR'ı nasıl etkinleştireceğinizi** ele aldık, **görüntüden metin tanımayı** gösterdik, daha hızlı işleme için **maksimum paralelliği nasıl ayarlayacağınızı** anlattık, **PNG'den metin çıkarmayı** açıkladık ve **OCR için görüntüyü nasıl yükleyeceğinizi** doğru şekilde gösterdik. Yukarıdaki tam kod örneği çalıştırmaya hazır ve kavramlar hızlı, güvenilir metin çıkarımı gerektiren herhangi bir Java projesine uygulanabilir.

Bir sonraki adıma hazır mısınız? Tüm bir PNG klasörünü işlemeyi deneyin, farklı dil paketleriyle deney yapın ya da OCR çıktısını bir arama indeksine yönlendirin. Temelleri kavradığınızda sınır yok.

Sorularınız mı var ya da bir sorunla mı karşılaştınız? Yorum bırakın, birlikte çözümleyelim. Kodlamanın tadını çıkarın!  

![OCR'ı etkinleştirme görseli](https://example.com/placeholder-image.png "Java'da Aspose ile OCR'ı nasıl etkinleştireceğiniz")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}