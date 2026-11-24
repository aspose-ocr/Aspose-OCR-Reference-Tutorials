---
category: general
date: 2026-06-22
description: Aspose OCR ile Java’da aranabilir PDF oluşturun. Tar scanned PDF’yi nasıl
  dönüştüreceğinizi, karışık dil OCR’ını nasıl yöneteceğinizi ve doğruluğu nasıl artıracağınızı
  öğrenin.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- how to ocr document
- mixed language ocr
- aspose ocr java
language: tr
og_description: Aspose OCR kullanarak Java’da aranabilir PDF oluşturun. Bu öğretici,
  bir belgeyi OCR ile işleme, karışık dil metnini yönetme ve aranabilir bir PDF çıktısı
  alma yöntemlerini gösterir.
og_title: Tarama Görüntülerinden Aranabilir PDF Oluşturma – Java OCR Rehberi
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Create searchable PDF in Java with Aspose OCR. Learn how to convert
    scanned PDF, handle mixed language OCR and boost accuracy.
  headline: Create Searchable PDF from Scanned Images – Java OCR Guide
  type: TechArticle
- description: Create searchable PDF in Java with Aspose OCR. Learn how to convert
    scanned PDF, handle mixed language OCR and boost accuracy.
  name: Create Searchable PDF from Scanned Images – Java OCR Guide
  steps:
  - name: Expected Output
    text: 'When you open `processed.pdf` in Adobe Reader (or any PDF viewer), you
      should be able to:'
  - name: 1. What if my document contains more than two languages?
    text: '`config.setLanguage` accepts a var‑args list, so you can pass as many `OcrLanguage`
      constants as you need:'
  - name: 2. Can I run this on a headless server without a GPU?
    text: Absolutely. Set `config.setUseGpu(false)` or simply omit the call. The engine
      will fall back to multi‑core CPU processing, which is still fast thanks to the
      thread pool we configured.
  - name: 3. How do I handle huge PDFs (hundreds of pages)?
    text: Aspose OCR streams pages one‑by‑one, so memory usage stays modest. However,
      you might want to split the PDF into smaller chunks using Aspose PDF’s `split`
      method, process each chunk, then merge the results back together.
  - name: 4. Is there a way to keep the original PDF’s metadata (author, creation
      date)?
    text: 'Yes. After you obtain `searchablePdf`, you can copy metadata from the original
      PDF:'
  type: HowTo
tags:
- OCR
- Java
- PDF
title: Tarama Görüntülerinden Aranabilir PDF Oluşturma – Java OCR Rehberi
url: /tr/java/advanced-ocr-techniques/create-searchable-pdf-from-scanned-images-java-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tarama Görüntülerinden Aranabilir PDF Oluşturma – Java OCR Rehberi

Hiç bir yığın taranmış sayfadan **aranabilir PDF** oluşturmanın üçüncü‑taraf hizmetlerine para harcamadan nasıl yapılacağını merak ettiniz mi? Yalnız değilsiniz. Birçok geliştirici, **tarama PDF** dosyalarını kullanıcıların gerçekten arayabileceği bir şeye dönüştürmeleri gerektiğinde aynı duvara çarpıyor.  

Bu rehberde, **Aspose OCR for Java** kullanarak **belge‑düzeyinde OCR** görevlerini nasıl yapacağınızı, **karışık dil OCR**'unu nasıl yöneteceğinizi ve sonunda cilalı bir aranabilir PDF elde edeceğinizi gösteren tam, çalıştırılabilir bir örnek üzerinden ilerleyeceğiz. Sonuna geldiğinizde, herhangi bir Maven veya Gradle projesine ekleyebileceğiniz ve hemen belgeleri işlemeye başlayabileceğiniz bağımsız bir programınız olacak.

## Gereksinimler – Neye İhtiyacınız Olacak

Koda geçmeden önce aşağıdakilerin kurulu olduğundan emin olun:

- Java 17 (veya daha yeni bir JDK) PATH’inizde yapılandırılmış.  
- Rahat ettiğiniz bir IDE veya editör (IntelliJ IDEA, Eclipse, VS Code…).  
- Aspose.OCR for Java kütüphanesi – en yeni JAR dosyasını [Aspose Maven deposundan](https://repo.aspose.com/repo/com/aspose/aspose-ocr/) alabilirsiniz.  
- Aranabilir hâle getirmek istediğiniz çok sayfalı taranmış PDF.  
- (İsteğe bağlı) `setUseGpu(true)` ile daha hızlı işleme yapmak istiyorsanız GPU‑destekli bir makine.

Bu bileşenler hazır olduğunda, aşağıdaki kodu kopyalayıp **Run** tuşuna basarak eksik bağımlılık aramadan çalıştırabilirsiniz.

## Adım 1: Projeyi Oluşturun ve Aspose OCR’u İçe Aktarın

İlk olarak yeni bir Maven modülü (veya Gradle projesi) oluşturun ve Aspose OCR bağımlılığını ekleyin:

```xml
<!-- pom.xml snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- replace with the latest version -->
</dependency>
```

Gradle tercih ediyorsanız eşdeğer satır şu şekildedir:

```gradle
implementation 'com.aspose:aspose-ocr:23.10'
```

Derleme senkronize olduğunda, ihtiyacımız olan sınıfları içe aktarabileceksiniz.

## Adım 2: OCR Motorunu Başlatın

Motoru oluşturmak oldukça basit, ancak erken başlatmamızın nedenini anlamak faydalı. `OcrEngine` nesnesi, sonraki tüm işlemleri etkileyen yapılandırma, iş parçacığı ve GPU ayarlarını tutar.

```java
import com.aspose.ocr.*;

public class AdvancedOcr {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine – this is the heart of the create searchable pdf process
        OcrEngine ocrEngine = new OcrEngine();
```

> **İpucu:** Motoru bir kez örnekleyip birden çok dosya için yeniden kullanmak, özellikle bir PDF topluluğu işliyorsanız, ek yükü azaltır.

## Adım 3: Taran PDF’yi (veya Görüntü Akışını) Yükleyin

Aspose OCR görüntü akışlarıyla çalışır, bu yüzden taranmış PDF’yi doğrudan besleriz. Kütüphane her sayfayı dahili olarak rasterleştirir; bu sayede bir PDF’den başlayıp tek adımda aranabilir PDF elde edebilirsiniz.

```java
        // Load the source PDF – replace the path with your actual file location
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/multi_page_scanned.pdf"));
```

Eğer koleksiyonunuz TIFF veya JPEG dosyalarından oluşuyorsa, `ImageStream.fromFile` metodunu bu dosyalara yönlendirin; akışın geri kalanı aynı kalır.

## Adım 4: Karışık Dil Desteği İçin OCR Ayarlarını İnce Ayarlayın

İşte **karışık dil OCR**unun parladığı yer. Birden fazla `OcrLanguage` enum’u geçirerek motorun aynı sayfada İngilizce ve Rusça (veya başka kombinasyonlar) aramasını sağlarsınız.

```java
        // Grab the mutable config object
        OcrConfig config = ocrEngine.getConfig();

        // Enable English + Russian detection – you can add more languages as needed
        config.setLanguage(OcrLanguage.ENGLISH, OcrLanguage.RUSSIAN);

        // Speed vs. accuracy trade‑off: use all available cores
        config.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Turn on GPU acceleration if the runtime detects a compatible device
        config.setUseGpu(true);

        // Spell‑check improves accuracy for noisy scans
        config.setEnableSpellCorrection(true);

        // Tell Aspose we want a searchable PDF as the final output
        config.setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE);
```

> **Neden bu önemli:** Diller belirtilmezse motor varsayılan olarak yalnızca İngilizceyi kullanır; bu da Kiril alfabesi veya diğer yazı sistemlerini içeren belgelerde tanıma oranını büyük ölçüde düşürür.

## Adım 5: Taramayı Temizlemek İçin Ön‑İşleme Filtreleri Ekleyin

Taran PDF’ler genellikle eğrilik, lekeler veya düşük kontrast gibi sorunlar yaşar. `DeskewFilter` ve `DenoiseFilter` eklemek, OCR motorunun karakterleri daha net görmesini sağlar.

```java
        // Set up image preprocessing
        ImagePreprocessOptions preprocess = new ImagePreprocessOptions();
        preprocess.addFilter(new DeskewFilter());   // Straighten tilted pages
        preprocess.addFilter(new DenoiseFilter()); // Reduce background noise
        ocrEngine.setPreprocessOptions(preprocess);
```

Kaynak materyaliniz özellikle kirli ise `ContrastFilter` ya da `BinarizationFilter` gibi ek filtreleri zincirleyebilirsiniz.

## Adım 6: OCR’u Çalıştırın ve Aranabilir PDF’i Oluşturun

Şimdi asıl iş başlıyor. `recognizeToPdf()` çağrısı OCR akışını yürütür, ön‑işleme adımlarını uygular ve tanınan metni PDF içinde görünmez bir metin katmanı olarak yazar.

```java
        // Perform OCR and retrieve a searchable PDF document object
        PdfDocument searchablePdf = ocrEngine.recognizeToPdf();
```

Dönen `PdfDocument` tam teşekküllü bir Aspose PDF nesnesidir; bu sayede kaydetmeden önce meta verileri düzenleyebilir, yer imleri ekleyebilir veya diğer PDF’lerle birleştirebilirsiniz.

## Adım 7: Sonucu Kaydedin ve Doğrulayın

Son olarak çıktıyı diske kalıcı hale getirin. Konsol mesajı, her şeyin sorunsuz çalıştığını hızlıca görmenizi sağlar.

```java
        // Save the searchable PDF to the desired location
        searchablePdf.save("YOUR_DIRECTORY/processed.pdf");
        System.out.println("OCR completed – searchable PDF saved at YOUR_DIRECTORY/processed.pdf");
    }
}
```

### Beklenen Çıktı

`processed.pdf` dosyasını Adobe Reader (veya herhangi bir PDF görüntüleyici) ile açtığınızda şunları yapabilmelisiniz:

1. **Metni seçin** – herhangi bir kelimeyi sürükleyip kopyalayın.  
2. **Arama yapın** – `Ctrl+F` tuşlarına basıp orijinal taramalarda geçen bir ifadeyi yazın.  
3. **Orijinal düzeni koruyun** – görsel görünüm taranan kaynağa birebir aynı kalır; sadece görünmez bir metin katmanı eklenir.

Eğer bozuk karakterler ya da eksik sayfalar görürseniz, dil ayarlarını tekrar kontrol edin ve kaynak PDF’nin şifre korumalı olmadığından emin olun.

## Sık Sorulan Sorular ve Kenar Durumları

### 1. Belgem iki dilden fazla dil içeriyorsa ne yapmalıyım?

`config.setLanguage` bir var‑args listesi kabul eder, bu yüzden ihtiyacınız kadar `OcrLanguage` sabiti geçirebilirsiniz:

```java
config.setLanguage(OcrLanguage.ENGLISH, OcrLanguage.RUSSIAN, OcrLanguage.CHINESE_SIMPLIFIED);
```

Her ek dil, işleme süresini biraz artırır, bunu aklınızda bulundurun.

### 2. GPU olmadan, başsız (headless) bir sunucuda çalıştırabilir miyim?

Kesinlikle. `config.setUseGpu(false)` ayarlayın ya da çağrıyı tamamen kaldırın. Motor, yapılandırdığınız iş parçacığı havuzunu kullanarak çok çekirdekli CPU işlemine geri döner; bu da hâlâ hızlıdır.

### 3. Yüzlerce sayfalık dev PDF’lerle nasıl başa çıkabilirim?

Aspose OCR sayfaları tek tek akıtarak işler, bu sayede bellek kullanımı düşük kalır. Yine de PDF’yi Aspose PDF’nin `split` metodu ile daha küçük parçalara ayırıp her birini işleyip sonuçları birleştirmek isteyebilirsiniz.

### 4. Orijinal PDF’nin meta verilerini (yazar, oluşturma tarihi vb.) korumak mümkün mü?

Evet. `searchablePdf` elde ettikten sonra orijinal PDF’den meta verileri kopyalayabilirsiniz:

```java
PdfDocument original = new PdfDocument("YOUR_DIRECTORY/multi_page_scanned.pdf");
searchablePdf.getInfo().setAuthor(original.getInfo().getAuthor());
// repeat for other metadata fields
```

## Üretim‑Hazır OCR için İpuçları

- **Toplu işleme:** Akışı bir dizindeki dosyalar üzerinde dönen bir döngüye alın. Tek bir `OcrEngine` örneğini yeniden kullanarak tekrar tekrar başlatma yükünden kaçının.  
- **Hata yönetimi:** `OcrException` yakalayarak başarısız dosyaları loglayın, ardından bir sonraki belgeye geçin.  
- **Performans takibi:** `recognizeToPdf()` öncesi ve sonrası `System.nanoTime()` ile zamanlayın; bu, dosya başına işleme süresini kaydetmenize ve bulut işçi havuzuna ölçeklendirme ihtiyacını belirlemenize yardımcı olur.  
- **Güvenlik:** Hassas belgelerle çalışıyorsanız, kaydetmeden önce `searchablePdf.encrypt(...)` ile çıktıyı şifrelemeyi düşünün.

## Sonuç

Bu rehberde, **Aspose OCR for Java** kullanarak taranmış kaynaklardan **aranabilir PDF** dosyaları oluşturmak için bilmeniz gereken her şeyi ele aldık. **Taran PDF**yi nasıl **dönüştüreceğinizi**, **karışık dil OCR** yapılandırmasını ve ön‑işleme filtrelerini nasıl ince ayarlayacağınızı gösterdik; tüm bunları üretim ortamına hazır, kısa ve anlaşılır bir kodla sunduk.  

Bundan sonra OCR‑oluşmuş küçük resimler eklemeyi, bir belge yönetim sistemiyle bütünleştirmeyi ya da çıkarılan metni Elasticsearch gibi bir arama indeksine beslemeyi keşfedebilirsiniz. Dijitalleştirmeniz gereken belgeler kadar çok seçenek sizleri bekliyor.

Java’da **belgeyi OCR ile nasıl tarayacağınız** hakkında daha fazla sorunuz varsa ya da PDF manipülasyonu üzerine daha derin bir inceleme görmek istiyorsanız, aşağıya yorum bırakın ve mutlu kodlamalar!

## Sonra Ne Öğrenmelisiniz?


Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakın konuları ele alır. Her kaynak, ek API özelliklerini ustalaşmanız ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım‑adım açıklamalı tam çalışan kod örnekleri içerir.

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [OCR Recognizing PDF Documents in Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}