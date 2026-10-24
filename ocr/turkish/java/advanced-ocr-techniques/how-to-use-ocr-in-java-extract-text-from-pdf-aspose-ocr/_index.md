---
category: general
date: 2026-10-24
description: Aspose OCR Java örneğini çalıştırarak PDF dosyalarından metin çıkarma,
  parallel OCR processing, password‑protected PDFs yönetme ve scanned PDFs'yi searchable
  text'e dönüştürme konularını öğrenin.
draft: false
keywords:
- aspose ocr java example
- parallel ocr processing
- extract text pdf java
- ocr password protected pdf
- convert scanned pdf searchable
lastmod: 2026-10-24
og_description: Aspose OCR Java örneğini çalıştırarak PDF'den metni hızlıca çıkarın.
  Bu rehber, parallel OCR processing, password‑protected PDFs ve scanned PDFs'yi searchable
  documents'e dönüştürmeyi kapsar.
og_image_alt: Screenshot of a Java console showing extracted text after parallel OCR
  processing with Aspose OCR
og_title: Aspose OCR Java örneği – PDF'den metni hızlıca çıkarın
schemas:
- author: Aspose
  dateModified: '2026-10-24'
  description: Learn how to run an Aspose OCR Java example that extracts text from
    PDF files, including parallel OCR processing, handling password‑protected PDFs,
    and converting scanned PDFs to searchable text.
  headline: 'Aspose OCR Java example: extract text from PDF quickly'
  type: TechArticle
- description: Learn how to run an Aspose OCR Java example that extracts text from
    PDF files, including parallel OCR processing, handling password‑protected PDFs,
    and converting scanned PDFs to searchable text.
  name: 'Aspose OCR Java example: extract text from PDF quickly'
  steps:
  - name: set up your project
    text: 'Add the Aspose OCR dependency to your `pom.xml`: If you prefer Gradle,
      replace the snippet with the equivalent `implementation` line. After the dependency
      resolves, you can import the required classes in your Java source file.'
  - name: create and configure the OCR engine
    text: '`OcrEngine` is the core class that performs optical character recognition.
      The `OcrEngine` class is Aspose OCR''s primary object that encapsulates all
      OCR settings and execution logic. Enable parallel processing and optionally
      limit the thread pool: **Why this matters:** - `setParallelProcessing(true'
  - name: load the PDF you want to process
    text: '`OcrInput` represents the collection of files (PDFs, images, or mixed media)
      that the engine will analyze. The `OcrInput` class aggregates one or more input
      sources, allowing you to feed PDFs, TIFFs, or JPEGs to the OCR engine in a single
      batch. Add your PDF (or a set of PDFs) to the input collectio'
  - name: run OCR across all pages in parallel
    text: '`OcrResult` holds the combined text output and per‑page confidence information
      after recognition completes. The `OcrResult` object contains the concatenated
      plain‑text result and a list of `PageResult` objects that expose confidence
      scores for each processed page. Execute the recognition: **Under th'
  - name: retrieve and display the combined text
    text: '`OcrResult.getText()` returns the full searchable string. The `getText()`
      method of `OcrResult` returns a single `String` that contains the OCR‑extracted
      text from every page, with line breaks preserved as they appeared in the source
      PDF. **Expected output:** The console prints one continuous string'
  - name: handle special scenarios
    text: '#### How does the engine deal with password‑protected PDFs? Supply the
      password when adding the file to `OcrInput`: The `add` method overload that
      accepts a password decrypts the document on the fly, allowing seamless OCR without
      manual decryption.'
  type: HowTo
- questions:
  - answer: Yes, the Aspose OCR free trial works for development and testing; a commercial
      license is required for production deployments.
    question: Can I use this example with a free trial license?
  - answer: Absolutely – pass the password to `OcrInput.add(filePath, password)` and
      the engine will decrypt the document automatically.
    question: Does the example support OCR on password‑protected PDFs?
  - answer: Over 70 languages, including right‑to‑left scripts such as Arabic and
      Hebrew.
    question: How many languages does Aspose OCR recognise?
  - answer: The engine can handle multi‑hundred‑page PDFs; you can set a memory limit
      to keep RAM usage predictable.
    question: What is the maximum PDF size I can process?
  - answer: Yes, by configuring `setMaxThreadCount` you control the maximum number
      of concurrent threads, preventing resource exhaustion.
    question: Is parallel OCR safe on shared servers?
  type: FAQPage
tags:
- ocr
- java
- aspose
- pdf
title: 'Aspose OCR Java örneği: PDF''den metni hızlıca çıkarın'
url: /tr/java/advanced-ocr-techniques/how-to-use-ocr-in-java-extract-text-from-pdf-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR Java örneği: PDF'den metni hızlıca çıkarın

Bu öğreticide **Aspose OCR Java örneğini nasıl kullanacağınızı** keşfedecek ve taranmış PDF'leri aranabilir, makine tarafından okunabilir metne dönüştüreceksiniz. Tek bir çok sayfalı dosyanız ya da şifre korumalı PDF'lerden oluşan bir toplu dosyanız olsun, aşağıdaki adımlar OCR motorunu nasıl yapılandıracağınızı, paralel işleme nasıl etkinleştireceğinizi ve yalnızca birkaç Java kod satırıyla birleşik çıktıyı nasıl alacağınızı gösterir.

İş parçacığı sayısını optimal performans için ne zaman ayarlamanız gerektiğini, şifreli PDF'lerle nasıl başa çıkacağınızı ve bu yaklaşımın taranmış PDF belgelerini aranabilir arşivlere dönüştürmek için neden ideal olduğunu da öğreneceksiniz.

![Aspose OCR Java ile OCR nasıl kullanılır](/images/ocr-parallel.png "Java'da paralel OCR işleme illüstrasyonu – OCR nasıl kullanılır")
[Aspose OCR Java ile OCR nasıl kullanılır](/images/ocr-parallel.png "Java'da paralel OCR işleme illüstrasyonu – OCR nasıl kullanılır")

## Hızlı cevaplar
- **Aspose OCR Java örneği ne yapar?** Bir PDF yükler, her sayfada paralel olarak OCR çalıştırır ve tam aranabilir metni tek bir dize olarak döndürür.  
- **Şifre korumalı PDF'leri işleyebilir mi?** Evet – dosyayı `OcrInput`'a eklerken belge şifresini sağlayabilirsiniz.  
- **Paralel OCR işleme değer mi?** 4 çekirdekli bir makinede, beş sayfadan fazla PDF'lerde işleme süresini %30‑70 oranında azaltır.  
- **Hangi diller destekleniyor?** İngilizce, Fransızca, Almanca, Çince ve Arapça dahil olmak üzere 70'ten fazla dil.  
- **Üretim için lisansa ihtiyacım var mı?** Ticari bir Aspose OCR lisansı, deneme dışı kullanım için gereklidir; ücretsiz deneme değerlendirme için çalışır.

## Aspose OCR Java örneği nedir?
**Aspose OCR Java örneği**, `OcrEngine`'i nasıl örnekleyeceğinizi, paralel yürütmeyi nasıl yapılandıracağınızı ve Aspose OCR for Java kütüphanesini kullanarak PDF dosyalarından metin nasıl çıkarılacağını gösteren kısa, çalıştırılabilir bir programdır. Ayrıca şifre korumalı belgeler, bellek sınırı ayarlaması ve dil seçimi gibi yaygın senaryoların nasıl ele alınacağını gösterir ve daha büyük belge işleme hatları oluşturmak için sağlam bir temel sağlar.

## Neden paralel OCR işleme kullanmalı?
Aspose OCR, çok sayfalı bir PDF'i ayrı sayfalara bölüp her sayfayı kendi iş parçacığında işleyebilir. 8 çekirdekli bir sunucuda, 120 sayfalık bir belge genellikle 30 saniyenin altında işlenir; sıralı çalıştırıldığında ise bir dakikadan uzun sürer. Bu hız artışı, toplu olarak **taranmış PDF'leri aranabilir** arşivlere dönüştürmeniz gerektiğinde özellikle değerlidir.

## Önkoşullar
- Java 8 veya daha yeni bir sürüm yüklü.  
- Maven veya Gradle yapı aracı (örnek Maven kullanır).  
- Aspose OCR for Java lisansı (ücretsiz deneme test için çalışır).  

## Aspose OCR Java örneğini adım adım nasıl çalıştırılır

### Adım 1: projenizi kurun

`pom.xml` dosyanıza Aspose OCR bağımlılığını ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.11</version>
</dependency>
```

Gradle tercih ediyorsanız, kod parçacığını eşdeğer `implementation` satırıyla değiştirin.  
Bağımlılık çözüldükten sonra, Java kaynak dosyanıza gerekli sınıfları içe aktarabilirsiniz.

### Adım 2: OCR motorunu oluşturun ve yapılandırın

`OcrEngine`, optik karakter tanıma (OCR) yapan temel sınıftır.

`OcrEngine` sınıfı, tüm OCR ayarlarını ve yürütme mantığını kapsülleyen Aspose OCR'nin ana nesnesidir.  
Paralel işleme etkinleştirin ve isteğe bağlı olarak iş parçacığı havuzunu sınırlayın:

```java
// Step 2: Initialise the OCR engine and enable parallel processing
OcrEngine ocrEngine = new OcrEngine();

// Turn on parallel processing – this is the key to faster PDF extraction
ocrEngine.setParallelProcessing(true);

// Optional: limit the number of threads (helps on low‑end machines)
ocrEngine.setMaxThreadCount(4);
```

**Neden önemli:**  
- `setParallelProcessing(true)` sayfaları birden fazla CPU çekirdeğine dağıtarak çok çekirdekli donanımlarda çalışma süresini büyük ölçüde kısar.  
- `setMaxThreadCount` motorun tüm çekirdekleri tek başına kullanmasını önleyerek sunucu kaynaklarını korur; bu, paylaşımlı barındırma veya CI ortamlarında kritiktir.

### Adım 3: İşlemek istediğiniz PDF'i yükleyin

`OcrInput`, motorun analiz edeceği dosya (PDF, görüntü veya karışık medya) koleksiyonunu temsil eder.

`OcrInput` sınıfı bir veya daha fazla giriş kaynağını birleştirir ve PDF, TIFF veya JPEG'leri tek bir toplu işlemde OCR motoruna beslemenizi sağlar.

PDF'inizi (veya PDF setinizi) giriş koleksiyonuna ekleyin:

```java
// Step 3: Prepare the input – add your multi‑page PDF
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/multi_page_document.pdf");

// If the PDF is password‑protected, supply the password like this:
// ocrInput.add("protected.pdf", "mySecretPassword");
```

**İpucu:** `FileNotFoundException` hatasından kaçınmak için mutlak bir yol ya da çalışma dizinine göre bir yol kullanın. `add` yöntemi, toplu işleme için birden fazla belgeyi sıraya eklemek amacıyla tekrar tekrar çağrılabilir.

### Adım 4: Tüm sayfalarda paralel OCR çalıştırın

`OcrResult`, tanıma tamamlandıktan sonra birleşik metin çıktısını ve sayfa başına güven puanlarını tutar.

`OcrResult` nesnesi, birleştirilmiş düz metin sonucunu ve işlenen her sayfa için güven puanlarını gösteren `PageResult` nesnelerinin bir listesini içerir.

Tanıma işlemini yürütün:

```java
// Step 4: Perform OCR – this will run on multiple threads
OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Arka planda:** Her sayfa, tanımladığınız `maxThreadCount` değerine kadar ayrı bir işçi iş parçacığına gönderilir. Kütüphane sonuçları senkronize eder, böylece son `OcrResult` orijinal sayfa sırasını korur.

### Adım 5: Birleşik metni alın ve görüntüleyin

`OcrResult.getText()` tam aranabilir dizeyi döndürür.

`OcrResult`'in `getText()` yöntemi, kaynak PDF'de olduğu gibi satır sonlarını koruyarak her sayfadan OCR ile çıkarılan metni içeren tek bir `String` döndürür.

```java
// Step 5: Output the combined OCR result
System.out.println("Combined text from all pages:");
System.out.println(ocrResult.getText());
```

**Beklenen çıktı:** Konsol, tüm sayfalardan okunabilir metni içeren tek bir sürekli dizeyi yazdırır; bu, indeksleme, depolama veya daha ileri işleme hazırdır.

### Adım 6: Özel senaryoları ele alın

#### Motor şifre korumalı PDF'lerle nasıl başa çıkar?

Dosyayı `OcrInput`'a eklerken şifreyi sağlayın:

```java
ocrEngine.getLanguageEngine().setLanguage(OcrLanguage.FRENCH);
```

Şifre kabul eden `add` yöntemi aşırı yüklemesi, belgeyi anında çözer ve manuel deşifre gerektirmeden sorunsuz OCR sağlar.

#### Çok büyük dosyalar için bellek kullanımını nasıl sınırlayabilirim?

RAM tüketimini 256 MB ile sınırlamak için `ocrEngine.setMemoryLimit(256);` çağırın. Motor, fazla veriyi otomatik olarak geçici dosyalara yazar; bu, çok sayfalı PDF'lerde bile bellek yetersizliği çöküşlerini önler.

## Yaygın sorular ve uç durumlar

### Gerçekten paralel işleme ihtiyacım var mı?
PDF'iniz **birkaç sayfadan fazla** içeriyorsa ve en az dört CPU çekirdeğiniz varsa, paralel işleme etkinleştirmek genellikle toplam çalışma süresini **%30‑70** oranında azaltır. Tek sayfalı bir tarama için iş parçacığı ek yükü faydayı aşabilir; bu durumda `ocrEngine.setParallelProcessing(false)` ile devre dışı bırakabilirsiniz.

### Bir sayfa OCR başarısız olduğunda ne olur?
Aspose OCR, bozuk dosya gibi ölümcül hatalar için yalnızca bir `OcrException` fırlatır. Tanınamayan sayfalar sadece boş bir dize döndürür; motor bunu sessizce birleştirir. `ocrResult.getPageResults()`'ı inceleyerek sayfa bazında güven puanlarını alabilir ve düşük güvenilirlikli sayfaları manuel olarak işleyebilirsiniz.

### Tanıma dilini nasıl değiştiririm?
Motor varsayılan olarak İngilizce'dir, ancak dilleri şu şekilde değiştirebilirsiniz:

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

`Language.FRENCH` ifadesini desteklenen herhangi bir dil enum'ı ile değiştirin. Bu, çok dilli belgelerden **PDF Java metni çıkarmak** gerektiğinde önemlidir.

## Üretime hazır OCR için profesyonel ipuçları
- **Toplu işleme:** Akışı, bir dizinden dosya adlarını okuyan bir döngü içinde sarın; böylece demoyu ölçeklenebilir bir hizmete dönüştürür.  
- **Günlükleme:** Üretimde ayrıntılı çıktıyı bastırmak için `ocrEngine.setLogLevel(LogLevel.ERROR)` ayarlayın.  
- **Sonuç temizliği:** `ocrResult.getText()`'i düzenli ifadelerle işleyerek gereksiz boşlukları veya artefaktları kaldırın.  
- **İş parçacığı havuzu ayarı:** Çok çekirdekli sunucularda maksimum verim için `ocrEngine.setMaxThreadCount(Runtime.getRuntime().availableProcessors())` kullanın.  
- **Performans ölçütü:** 8 çekirdekli Intel Xeon'da, 200 sayfalık (300 MB) bir PDF, paralel OCR etkinleştirildiğinde yaklaşık 22 saniyede işlenir.

## Sonuç
Artık herhangi bir taranmış PDF'den aranabilir metin çıkaran, şifre korumalı dosyaları destekleyen ve hız için paralel işleme kullanan eksiksiz bir **Aspose OCR Java örneği**'ne sahipsiniz. Bu kodu kendi uygulamalarınıza entegre ederek güçlü belge dijitalleştirme hatları oluşturabilir, OCR çıktısını arama indekslerine besleyebilir veya çok dilli arşivler için çeviri hizmetleriyle birleştirebilirsiniz.

Bir sonraki adıma hazır mısınız? Çıkarılan metni tam metin arama için Elasticsearch'e gönderin veya çıktıyı bir dil çeviri API'siyle zincirleyerek çok dilli bir aranabilir depo oluşturun. Kodlamanın tadını çıkarın!

---

**Son Güncelleme:** 2026-10-24  
**Test Edilen Versiyon:** Aspose OCR for Java 24.11  
**Yazar:** Aspose  

## Sıkça Sorulan Sorular

**S: Bu örneği ücretsiz deneme lisansı ile kullanabilir miyim?**  
C: Evet, Aspose OCR ücretsiz deneme geliştirme ve test için çalışır; üretim dağıtımları için ticari bir lisans gereklidir.

**S: Örnek şifre korumalı PDF'lerde OCR'ı destekliyor mu?**  
C: Kesinlikle – şifreyi `OcrInput.add(filePath, password)`'a geçirerek motor belgeyi otomatik olarak çözer.

**S: Aspose OCR kaç dili tanıyor?**  
C: Arapça ve İbranice gibi sağdan sola yazılan diller dahil 70'ten fazla dil.

**S: İşleyebileceğim maksimum PDF boyutu nedir?**  
C: Motor, çok sayfalı PDF'leri işleyebilir; RAM kullanımını öngörülebilir tutmak için bir bellek sınırı ayarlayabilirsiniz.

**S: Paylaşımlı sunucularda paralel OCR güvenli mi?**  
C: Evet, `setMaxThreadCount` yapılandırarak aynı anda çalışan iş parçacığı sayısını kontrol eder ve kaynak tükenmesini önlersiniz.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

```bash
javac -cp "path/to/aspose-ocr.jar" ParallelOcrDemo.java
java -cp ".:path/to/aspose-ocr.jar" ParallelOcrDemo
```

## İlgili Öğreticiler

- [Java'da Paralel İşleme ile Aspose Kullanarak OCR Nasıl Kullanılır](/ocr/java/advanced-ocr-techniques/how-to-use-ocr-in-java-parallel-processing-with-aspose/)
- [Aspose OCR Java Rehberi ile Aranabilir PDF Oluşturma](/ocr/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-java-guide/)
- [Java'da OCR Kullanarak PDF'den Metin Çıkarma Aspose OCR](/ocr/java/advanced-ocr-techniques/how-to-use-ocr-in-java-extract-text-from-pdf-aspose-ocr/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}