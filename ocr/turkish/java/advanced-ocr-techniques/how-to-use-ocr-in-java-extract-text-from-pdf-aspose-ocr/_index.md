---
category: general
date: 2026-02-22
description: Aspose OCR ile Java’da PDF’den metni hızlıca çıkarmak için OCR nasıl
  kullanılır – paralel işleme ve tam kod örneği içeren adım adım rehber.
draft: false
keywords:
- how to use OCR
- extract text from pdf
- aspose ocr java example
- parallel OCR processing
- Java PDF extraction
language: tr
og_description: Java'da OCR kullanarak PDF'den metni hızlıca çıkarmak için Aspose
  OCR ile nasıl yapılır – paralel işleme ve çalıştırılabilir kod içeren tam rehber.
og_title: Java'da OCR Nasıl Kullanılır – PDF'den Metin Çıkarma (Aspose OCR)
tags:
- OCR
- Java
- Aspose
- PDF
title: Java'da OCR Nasıl Kullanılır – PDF'den Metin Çıkarma (Aspose OCR)
url: /tr/java/advanced-ocr-techniques/how-to-use-ocr-in-java-extract-text-from-pdf-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da OCR Nasıl Kullanılır – PDF'ten Metin Çıkarma (Aspose OCR)

Hiç **OCR nasıl kullanılır** diye Java'da, arşivinizdeki taranmış PDF yığınlarını aranabilir hâle getirmek istediğinizde merak ettiniz mi? Tek başınıza değilsiniz. Birçok projede darboğaz, çok sayfalı bir belgeden temiz, aranabilir metni CPU döngülerini yakmadan çıkarmaktır. Bu öğreticide **OCR nasıl kullanılır** sorusunun cevabını Aspose OCR for Java ile gösteriyor, paralel işleme olanak tanıyarak PDF dosyalarından metni anında çıkarabilirsiniz.

Çalışan bir **Aspose OCR Java örneği**nin her satırını adım adım inceleyecek, her ayarın neden önemli olduğunu açıklayacak ve gerçek dünyada karşılaşabileceğiniz birkaç uç durumu ele alacağız. Sonunda, herhangi bir PDF'i okuyabilen, tüm sayfalarında aynı anda OCR çalıştırabilen ve birleşik sonucu konsola yazdırabilen hazır bir programınız olacak.

![Aspose OCR Java ile OCR nasıl kullanılır](/images/ocr-parallel.png "Java'da paralel OCR işleme illüstrasyonu – OCR nasıl kullanılır")

## Neler Başaracaksınız

- Aspose OCR kütüphanesinden bir `OcrEngine` başlatmak.  
- **Paralel işleme**yi açmak ve isteğe bağlı olarak iş parçacığı havuzunu sınırlamak.  
- `OcrInput` aracılığıyla çok sayfalı bir PDF yüklemek.  
- Tüm sayfalarda aynı anda OCR çalıştırmak ve birleşik metni toplamak.  
- Sonucu yazdırmak ya da istediğiniz herhangi bir downstream sisteme yönlendirmek.

Ayrıca iş parçacığı sayısını ne zaman ayarlamanız gerektiğini, şifre korumalı PDF'leri nasıl ele alacağınızı ve küçük dosyalar için paralelliği neden kapatmak isteyebileceğinizi öğreneceksiniz.

---

## Aspose OCR Java ile OCR Nasıl Kullanılır

### Adım 1: Projenizi Hazırlayın

Kod yazmaya başlamadan önce, Aspose OCR for Java kütüphanesinin sınıf yolunuzda (classpath) olduğundan emin olun. En kolay yol Maven kullanmaktır:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Gradle tercih ediyorsanız, snippet'i ona göre değiştirin. Bağımlılık çözüldükten sonra ihtiyacınız olan sınıfları içe aktarabilirsiniz.

### Adım 2: OCR Motorunu Oluşturun ve Yapılandırın

`OcrEngine`, kütüphanenin kalbidir. Paralel işleme özelliğini etkinleştirmek, Aspose'un her bir sayfayı ayrı bir iş parçacığıyla işlemesini sağlar.

```java
// Step 2: Initialise the OCR engine and enable parallel processing
OcrEngine ocrEngine = new OcrEngine();

// Turn on parallel processing – this is the key to faster PDF extraction
ocrEngine.setParallelProcessing(true);

// Optional: limit the number of threads (helps on low‑end machines)
ocrEngine.setMaxThreadCount(4);
```

**Neden önemli:**  
- `setParallelProcessing(true)` iş yükünü bölerek çok çekirdekli CPU'larda işleme süresini önemli ölçüde azaltabilir.  
- `setMaxThreadCount` motorun tüm çekirdekleri ele geçirmesini engeller; paylaşımlı sunucular veya CI pipeline'ları için kullanışlı bir koruma sağlar.

### Adım 3: İşlemek İstediğiniz PDF'i Yükleyin

Aspose OCR, herhangi bir görüntü formatıyla çalışır, ancak PDF'leri doğrudan `OcrInput` aracılığıyla da kabul eder. Aynı toplu iş içinde birden fazla dosya ekleyebilir ya da görüntü ve PDF'leri karıştırabilirsiniz.

```java
// Step 3: Prepare the input – add your multi‑page PDF
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/multi_page_document.pdf");

// If the PDF is password‑protected, supply the password like this:
// ocrInput.add("protected.pdf", "mySecretPassword");
```

**İpucu:** `FileNotFoundException` almamak için PDF yolunu mutlak ya da çalışma dizinine göre göreceli tutun. Ayrıca, birden fazla PDF'i tek seferde işlemek istiyorsanız `add` metodunu tekrarlı olarak çağırabilirsiniz.

### Adım 4: Tüm Sayfalarda Paralel Olarak OCR Çalıştırın

Şimdi motor ağır işi üstleniyor. `recognize` çağrısı, her sayfadan gelen metni birleştiren bir `OcrResult` döndürür.

```java
// Step 4: Perform OCR – this will run on multiple threads
OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Arka planda:** Her sayfa ayrı bir iş parçacığına (belirlediğiniz `maxThreadCount` değerine kadar) verilir. Kütüphane senkronizasyonu halleder, böylece son `OcrResult` zaten doğru sırada olur.

### Adım 5: Birleştirilmiş Metni Alın ve Görüntüleyin

Son olarak düz metin çıktısını alın. Bunu bir dosyaya yazabilir, bir arama indeksine itebilir ya da hızlı doğrulama için sadece konsola basabilirsiniz.

```java
// Step 5: Output the combined OCR result
System.out.println("Combined text from all pages:");
System.out.println(ocrResult.getText());
```

**Beklenen çıktı:** Konsol, orijinal PDF'te göründüğü gibi satır sonları korunmuş, her sayfadan okunabilir metni içeren tek bir dize gösterecek.

---

## Tam Aspose OCR Java Örneği – Çalıştırmaya Hazır

Tüm parçaları bir araya getirerek, `ParallelOcrDemo.java` dosyasına kopyalayıp çalıştırabileceğiniz eksiksiz, bağımsız bir program aşağıdadır.

```java
import com.aspose.ocr.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable parallel processing and optionally limit threads
        ocrEngine.setParallelProcessing(true);
        ocrEngine.setMaxThreadCount(4); // Adjust based on your hardware

        // Step 3: Load the multi‑page PDF to be processed
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/multi_page_document.pdf");
        // Uncomment and set password if needed:
        // ocrInput.add("protected.pdf", "mySecretPassword");

        // Step 4: Recognize text from all pages in parallel
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // Step 5: Display the combined OCR result
        System.out.println("Combined text from all pages:");
        System.out.println(ocrResult.getText());
    }
}
```

Şu komutla çalıştırın:

```bash
javac -cp "path/to/aspose-ocr.jar" ParallelOcrDemo.java
java -cp ".:path/to/aspose-ocr.jar" ParallelOcrDemo
```

Her şey doğru kurulduysa, program başladıktan kısa bir süre sonra çıkarılan metin konsolda görüntülenecektir.

---

## Sık Sorulan Sorular & Uç Durumlar

### Paralel işleme gerçekten gerekli mi?

PDF'iniz **birkaç sayfadan fazla** ve en az 4 çekirdeğe sahip bir makinede çalışıyorsa, paralel işleme toplam çalışma süresini **%30‑70** oranında azaltabilir. Tek sayfalı bir tarama için iş parçacığı yönetiminin ek yükü faydayı aşabilir; bu durumda sadece `ocrEngine.setParallelProcessing(false)` çağırabilirsiniz.

### Bir sayfa OCR'da başarısız olursa ne olur?

Aspose OCR, yalnızca ölümcül hatalar (ör. bozuk dosya) için bir `OcrException` fırlatır. Tanınamayan sayfalar sadece o sayfa için boş bir dize döndürür; motor bunu sessizce birleştirir. `ocrResult.getPageResults()` ile sayfa bazında güven skorlarını inceleyebilir ve düşük güvenilirlikli sayfaları manuel olarak işleyebilirsiniz.

### Çıktı dilini nasıl kontrol ederim?

Motor varsayılan olarak İngilizce'dir, ancak dilleri şu şekilde değiştirebilirsiniz:

```java
ocrEngine.getLanguageEngine().setLanguage(OcrLanguage.FRENCH);
```

`FRENCH` yerine desteklenen herhangi bir dil enum'ını koyun. Bu, **PDF'ten metin çıkarma** işlemini birden çok yerel dilde gerçekleştirmek istediğinizde çok işe yarar.

### Bellek kullanımını sınırlayabilir miyim?

Evet. `ocrEngine.setMemoryLimit(256);` ile bellek ayak izini 256 MB ile sınırlayabilirsiniz. Kütüphane, fazladan veriyi geçici dosyalara yazarak büyük PDF'lerde out‑of‑memory çöküşlerini önler.

---

## Üretim‑Hazır OCR İçin Pro İpuçları

- **Toplu işleme:** Tüm akışı, bir dizinden dosya adlarını okuyan bir döngüye sarın. Böylece demoyu ölçeklenebilir bir servise dönüştürmüş olursunuz.  
- **Loglama:** Aspose OCR, bir `setLogLevel` metodu sunar – üretimde gürültülü çıktıyı önlemek için `LogLevel.ERROR` olarak ayarlayın.  
- **Sonuç temizliği:** `ocrResult.getText()` çıktısını istenmeyen boşlukları veya satır sonu artefaktlarını temizlemek için sonradan işleyin. Düzenli ifadeler (regex) bu iş için çok uygundur.  
- **İş parçacığı havuzu ayarı:** Çok çekirdekli bir sunucuda, optimal verim için `setMaxThreadCount(Runtime.getRuntime().availableProcessors())` ile deneme yapın.  

---

## Sonuç

Java'da Aspose OCR ile **OCR nasıl kullanılır** sorusunu ele aldık, tam bir **PDF'ten metin çıkarma** akışı gösterdik ve paralel hız için çalışan eksiksiz bir **Aspose OCR Java örneği** sunduk. Yukarıdaki adımları izleyerek, taranmış herhangi bir PDF'i sadece birkaç satır kodla aranabilir metne dönüştürebilirsiniz.

Bir sonraki meydan okumaya hazır mısınız? OCR çıktısını Elasticsearch'e göndererek tam metin arama ekleyebilir ya da bir dil‑çeviri API'siyle birleştirerek çok dilli belge hattı oluşturabilirsiniz. Temelleri kavradığınızda sınır yoktur.

Herhangi bir sorunla karşılaşırsanız, aşağıya yorum bırakın—mutlu kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}