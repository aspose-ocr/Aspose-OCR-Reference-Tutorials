---
category: general
date: 2026-01-12
description: Aspose OCR'i Java'da kullanarak görüntülerden metin tanımayı ve png dosyalarından
  metin çıkarmayı öğrenin. Paralel işleme sayesinde hızlıdır.
draft: false
keywords:
- recognize text from images
- extract text from png
language: tr
og_description: Java'da görüntülerden metin tanımanın en kolay yolunu keşfedin ve
  Aspose OCR'ı paralel işleme ile kullanarak png dosyalarından metin çıkarın.
og_title: Java ile görüntülerden metin tanıma – Paralel OCR Rehberi
tags:
- OCR
- Java
- Aspose
title: Java ile görüntülerden metin tanıma – Paralel OCR Öğreticisi
url: /tr/java/advanced-ocr-techniques/recognize-text-from-images-with-java-parallel-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görsellerden Metin Tanıma Java ile – Paralel OCR Eğitimi

Hiç **görsellerden metin tanıma** ihtiyacı hissettiniz ama “bunu nasıl yaparım?” sorusunda takıldınız mı? Tek başınıza değilsiniz. Faturaları dijitalleştiriyor, ekran görüntülerinden veri çekiyor ya da aranabilir bir arşiv oluşturuyorsanız, *görsellerden metin tanıma* bir dönüm noktasıdır.  

Bu rehberde, sadece **görsellerden metin tanıma** yapmayı değil, aynı zamanda Aspose OCR’ın yerleşik paralel motorunu kullanarak **png dosyalarından metin çıkarma** (extract text from png) nasıl yapılacağını gösteren, tamamen çalıştırılabilir bir Java örneği üzerinden ilerleyeceğiz. Harici betikler, eksik parçalar yok—sadece net kod ve açıklamalar.

## Öğrenecekleriniz

- Java projesinde Aspose OCR kurulumunu yapma  
- Toplu işleri hızlandırmak için paralel işleme etkinleştirme  
- PNG dosyalarının bir koleksiyonunu yükleyip **png dosyalarından metin çıkarma** işlemini verimli bir şekilde gerçekleştirme  
- Yaygın sorunları (büyük dosyalar, boş sonuçlar, iş parçacığı limitleri) ele alma  
- Makalenin sonunda tam, çalıştırılabilir kaynak kodu görme  

Bu bölümü tamamladığınızda, herhangi bir görsel‑tabanlı metin çıkarma iş akışına uyarlayabileceğiniz bir kopyala‑yapıştır çözümünüz olacak.

## Ön Koşullar

İlerlemeye başlamadan önce şunların olduğundan emin olun:

| Gereksinim | Neden Önemli |
|------------|--------------|
| Java 8 ve üzeri | Aspose OCR’ın Java API’si Java 8+ hedefler |
| Maven veya Gradle (bağımlılık yönetimi için) | Aspose OCR kütüphanesini eklemeyi basitleştirir |
| İşlemek istediğiniz birkaç PNG görüntüsü | Eğitimde `doc1.png`‑`doc4.png` örnek olarak kullanılıyor |
| Java sözdizimi hakkında temel bilgi | Kod basit, ancak derleyip çalıştırmanız gerekecek |

Eğer bunlardan birine sahip değilseniz, Oracle ya da AdoptOpenJDK’den en yeni JDK’yı indirin ve basit bir Maven projesi kurun—çok karmaşık bir şey değil.

![görsellerden metin tanıma diyagramı](image.png){alt="görsellerden metin tanıma diyagramı"}

## Adım 1 – Aspose OCR’ı Projenize Ekleyin

Öncelikle Maven (veya Gradle)’a Aspose OCR kütüphanesini indirmesini söyleyin. `pom.xml` dosyanıza şunu ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Gradle tercih ediyorsanız eşdeğeri:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Pro ipucu:** En yeni sürüm için [Aspose OCR Maven deposunu](https://repo.aspose.com/repo) kontrol edin. Kütüphaneyi güncel tutmak, en son OCR iyileştirmeleri ve hata düzeltmelerini almanızı sağlar.

## Adım 2 – Paralel İşlemeyi Etkinleştirin (gizli sos)

Aspose OCR, işi birden fazla CPU çekirdeği arasında dağıtabilir. Bu sayede **görsellerden metin tanıma** işlemini, onlarca PNG dosyanız olsa bile hızlı tutarız.

```java
// Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Configure parallel options – up to 4 cores in this demo
ParallelOptions parallelOptions = new ParallelOptions();
parallelOptions.setMaxDegreeOfParallelism(4); // Adjust based on your machine
ocrEngine.setParallelOptions(parallelOptions);
```

Neden bir limit koyuyoruz? İş parçacıklarını aşırı tahsis etmek, özellikle paylaşımlı sunucularda diğer süreçleri aç bırakabilir. Çoğu masaüstü bilgisayar için dört çekirdek güvenli bir varsayılandır; donanımınız daha fazlasını kaldırabiliyorsa artırabilirsiniz.

## Adım 3 – PNG Dosyalarının Listesini Hazırlayın

Eğitim, **png dosyalarından metin çıkarma** üzerine odaklansa da aynı kod JPEG, BMP vb. formatlarda da çalışır. Görsellerinizi bir klasöre koyun ve aşağıdaki gibi referans verin:

```java
String[] imageFiles = {
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png",
    "YOUR_DIRECTORY/doc4.png"
};
```

> **Not:** `YOUR_DIRECTORY` ifadesini PNG dosyalarınızın bulunduğu mutlak ya da göreli yol ile değiştirin. Dinamik bir klasörü işlemek isterseniz, `Files.list(Paths.get("YOUR_DIRECTORY"))` kullanarak diziyi otomatik oluşturabilirsiniz.

## Adım 4 – Her Görüntüde OCR’ı Çalıştırın (motor ağır işi yapar)

Paralelliği etkinleştirmiş olsak da dosya dizisi üzerinde hâlâ bir döngüyle ilerliyoruz. Aspose OCR, yapılandırdığımız iş parçacıkları arasında tanıma işini dahili olarak dağıtır.

```java
for (String imagePath : imageFiles) {
    // Load the image into the engine
    ocrEngine.setImage(imagePath);
    
    // Perform recognition
    OcrResult result = ocrEngine.recognize();
    
    // Guard against empty results
    String text = result.getText();
    if (text == null || text.isEmpty()) {
        System.out.println("[" + imagePath + "] => No text found.");
        continue;
    }
    
    // Print a short preview (first 50 characters)
    System.out.println("[" + imagePath + "] => " +
        text.substring(0, Math.min(50, text.length())) + "...");
}
```

### Neden bir döngü ve paralel akış (stream) değil?

Aspose OCR, `ParallelOptions` temelinde görüntü işleme işini zaten dahili olarak bölüyor. Dış bir paralel akışla çağrıyı sarmak işi iki kez sarmalayarak performansı düşürebilir. İş parçacıklarını yönetmesi için kütüphaneye güvenin.

## Adım 5 – Kenar Durumları ve Pratik İpuçları

| Durum | Ne Yapmalı |
|-------|------------|
| **Büyük PNG ( > 10 MB )** | JVM yığın alanını (`-Xmx2g`) artırın veya motorun önüne göndermeden önce görüntüyü yeniden boyutlandırın. |
| **Karışık görüntü formatları** | `ocrEngine.setImage(new File(imagePath))` kullanın – motor formatı otomatik algılar. |
| **Tam metne ihtiyacınız var, sadece ön izleme değil** | `result.getText()` değerini bir `StringBuilder` içinde saklayın ya da daha sonra analiz için bir dosyaya yazın. |
| **GUI’siz bir CI sunucusunda çalıştırma** | Ek bir adım gerekmez—Aspose OCR tamamen başsız (headless) çalışır. |
| **Lisans süresi dolmuş** | `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` kodu ile geçici bir lisans kaydedin, değerlendirme filigranlarından kaçının. |

## Tam Çalışan Örnek

Aşağıda kopyalayıp yapıştırıp çalıştırabileceğiniz tam Java sınıfı yer alıyor. Tartıştığımız tüm parçalar ve birkaç açıklama yorum satırı içeriyor.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.parallel.*;

public class ParallelOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create and initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable parallel processing (up to 4 CPU cores)
        ParallelOptions parallelOptions = new ParallelOptions();
        parallelOptions.setMaxDegreeOfParallelism(4); // Adjust as needed
        ocrEngine.setParallelOptions(parallelOptions);

        // Step 3: Define the PNG files to be processed
        String[] imageFiles = {
            "YOUR_DIRECTORY/doc1.png",
            "YOUR_DIRECTORY/doc2.png",
            "YOUR_DIRECTORY/doc3.png",
            "YOUR_DIRECTORY/doc4.png"
        };

        // Step 4: Recognize text from each image (engine handles parallelism internally)
        for (String imagePath : imageFiles) {
            // Load the image
            ocrEngine.setImage(imagePath);

            // Perform OCR
            OcrResult result = ocrEngine.recognize();

            // Extract the recognized text
            String text = result.getText();

            // Guard against empty results
            if (text == null || text.isEmpty()) {
                System.out.println("[" + imagePath + "] => No text found.");
                continue;
            }

            // Step 5: Output a short preview (first 50 characters)
            System.out.println("[" + imagePath + "] => " +
                text.substring(0, Math.min(50, text.length())) + "...");
        }
    }
}
```

### Beklenen Çıktı

`doc1.png` içinde “Invoice #12345 – Total $250.00” ifadesi varsa, aşağıdakine benzer bir çıktı göreceksiniz:

```
[YOUR_DIRECTORY/doc1.png] => Invoice #12345 – Total $250.00...
[YOUR_DIRECTORY/doc2.png] => No text found.
[YOUR_DIRECTORY/doc3.png] => Customer Name: John Doe...
[YOUR_DIRECTORY/doc4.png] => ...
```

Ön izleme 50 karakterde kesilir, ancak tam metin `result.getText()` içinde bulunur ve ihtiyacınız olan tüm sonraki işlemler için kullanılabilir.

## Sonuç

Artık Aspose OCR kullanarak Java’da **görsellerden metin tanıma** için sağlam, üretim‑hazır bir deseniniz var ve **png dosyalarından metin çıkarma** işlemini paralel hızlandırmalarla nasıl yapacağınızı gördünüz. Temel adımlar—motor kurulumu, paralel yapılandırma, görüntü listesi hazırlama ve sonuç işleme—tamamen kapsandı, ayrıca yaygın baş ağrılarından kaçınmanız için pratik ipuçları da verildi.

Sırada ne var? PNG listesini dinamik bir klasör taramasıyla değiştirin, OCR çıktısını Elasticsearch gibi bir arama indeksine yönlendirin ya da dil‑spesifik OCR ayarlarıyla deneyler yapın (`ocrEngine.getLanguage().setLanguage(OcrLanguage.FRENCH)`). Temel iş akışını kavradığınızda, sınır yok.

Bu öğreticiyi genişletmek için fikirleriniz ya da karşılaştığınız tuhaflıklar varsa, aşağıya bir yorum bırakın. Kodlamanın tadını çıkarın ve inatçı görselleri aranabilir metne dönüştürmenin keyfini yaşayın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}