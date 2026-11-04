---
category: general
date: 2026-02-09
description: Aspose OCR'i Java'da kullanarak görüntüden metin tanımayı öğrenin. Bu
  adım adım öğretici ayrıca yazım denetimini, özel sözlükleri ve OCR motoru yapılandırmasını
  da kapsar.
draft: false
keywords:
- recognize text from image
- Aspose OCR Java
- OCR spell checking
- custom OCR dictionary
- Java image processing
language: tr
og_description: Aspose OCR kullanarak Java’da görüntüden metin tanıyın. Yazım denetimini
  etkinleştirmek, dili ayarlamak ve anında düzeltilmiş çıktıyı almak için bu rehberi
  izleyin.
og_title: Aspose OCR ile Görüntüden Metin Tanıma – Tam Java Öğreticisi
tags:
- OCR
- Java
- Aspose
title: Aspose OCR ile Görüntüden Metin Tanıma – Tam Java Rehberi
url: /tr/java/advanced-ocr-techniques/recognize-text-from-image-with-aspose-ocr-full-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Resimden Metin Tanıma – Tam Java Öğreticisi

Hiç **resimden metin tanıma** ihtiyacı duydunuz ama hangi API'ye güveneceğinizi bilemediniz mi? Tek başınıza değilsiniz. Birçok projede—fatura tarama, el yazısı notları dijitalleştirme veya aranabilir bir arşiv oluşturma—bir resimden temiz, okunabilir metin çıkarabilme oyunu değiştiren bir özelliktir.  

İyi haber? Aspose OCR for Java ile bunu sadece birkaç satırda yapabilirsiniz ve OCR çıktısını temizlemek için yerleşik yazım denetimi bile alırsınız. Bu öğreticide, OCR motorunu oluşturmaktan düzeltilmiş sonucu yazdırmaya kadar tüm süreci adım adım inceleyeceğiz. Sonunda, **resimden metin tanıma** işlemini güvenilir bir şekilde yapan hazır bir Java sınıfına sahip olacaksınız.

---

## Gereksinimler

- **Java 8+** (kod, herhangi bir yeni JDK ile çalışır)
- **Aspose OCR for Java** kütüphanesi – en son JAR dosyasını Aspose Maven deposundan alabilir veya doğrudan Aspose web sitesinden indirebilirsiniz.
- Yazılı veya basılı metin içeren bir görüntü dosyası (ör. `typed_scanned_doc.png`).
- Makul bir RAM miktarı; OCR ağır bir işlem değildir, ancak çoğu tarama için 1 GB heap yeterlidir.

> *Pro ipucu:* Maven kullanıyorsanız, aşağıdaki bağımlılığı `pom.xml` dosyanıza ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

Şimdi ön koşullar halledildiğine göre, koda dalalım.

---

## Adım 1: OCR Motorunu Başlatın ve Yapılandırmasını Alın

İlk olarak bir `OcrEngine` örneği oluşturursunuz. Bu nesne, kütüphanenin kalbidir; daha sonra ayarlayacağınız tüm ayarları tutar.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.enums.*;

public class SpellCheckExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and obtain its configuration object
        OcrEngine ocrEngine = new OcrEngine();
        OcrEngineConfiguration ocrConfig = ocrEngine.getConfiguration();
```

Neden önemli: Yapılandırma nesnesi, dil seçimi, yazım denetimi bayrakları ve sözlük yollarına doğrudan erişim sağlar. Onsuz varsayılan ayarlarla kalırsınız ve bu ayarlar kaynak materyalinize uymayabilir.

---

## Adım 2: Dili Seçin ve Yazım Denetimini Açın

Sonra, motorun görüntüde hangi dili beklediğini belirtin. Burada İngilizce seçiyoruz, ancak Aspose onlarca yerel dili destekler.

```java
        // Step 2: Choose the language for recognition and turn on spell‑checking
        ocrConfig.setLanguage(Language.ENGLISH);
        ocrConfig.setSpellCheckEnabled(true);
```

Yazım denetimini etkinleştirmek isteğe bağlıdır, ancak çıktının okunabilirliğini büyük ölçüde artırır—özellikle OCR motorunun “0” karakterini “O” olarak yorumlayabileceği taranmış belgelerde.

---

## Adım 3: (İsteğe Bağlı) Özel Bir Yazım Denetimi Sözlüğü Yükleyin

Sektöre özgü jargonla çalışıyorsanız—örneğin tıbbi terimler, hukuki kısaltmalar veya özel ürün kodları—Aspose kendi sözlüğünüzü eklemenize izin verir.

```java
        // Step 3: (Optional) Provide a custom spell‑check dictionary
        ocrConfig.setSpellCheckDictionary("en_US"); // use a locale‑specific dictionary
```

Eğer özel bir `.dic` dosyanız varsa `setSpellCheckDictionary` metodunu tam yol ile gösterebilirsiniz. Motor, özel kelimelerinizi yerleşik sözlükle birleştirerek alan‑spesifik kelime hazinesinin korunmasını sağlar.

---

## Adım 4: Görüntü Dosyanızda OCR Çalıştırın

Şimdi gerçek iş başlıyor. Görüntünün yolunu sağlayın ve motorun sihrini izleyin.

```java
        // Step 4: Run OCR on the input image file
        RecognitionResult recognitionResult = ocrEngine.recognize("YOUR_DIRECTORY/typed_scanned_doc.png");
```

Arka planda, Aspose bir dizi ön işleme adımı uygular—eğrilik düzeltme, ikilileştirme ve karakter segmentasyonu—sonra piksel verilerini sinir ağı tanıyıcısına gönderir. Sonuç, ham ve düzeltilmiş metni içeren bir `RecognitionResult` nesnesi içinde paketlenir.

---

## Adım 5: Düzeltlenmiş Metni Görüntüleyin

Son olarak, temizlenmiş dizeyi konsola yazdırın. OCR çıktısını **yazım denetimi uygulanmış** olarak göreceksiniz; bu genellikle doğrudan bir veritabanına kaydedilebilir veya bir arama indeksine beslenebilir.

```java
        // Step 5: Display the corrected text returned by the engine
        System.out.println("Corrected text:");
        System.out.println(recognitionResult.getText());
    }
}
```

### Beklenen Çıktı

`typed_scanned_doc.png` dosyasının *“The quick brown fox jumps over the lazy dog.”* cümlesini içerdiğini varsayarsak, konsol şu şekilde gösterir:

```
Corrected text:
The quick brown fox jumps over the lazy dog.
```

Orijinal taramada “quick” kelimesi “qu1ck” olarak bozulmuş olsaydı, yazım denetleyicisi otomatik olarak “quick”e düzeltirdi.

---

## Yaygın Kenar Durumlarını Ele Alma

### 1. Düşük Çözünürlüklü Görüntüler

OCR doğruluğu 150 dpi altında keskin bir şekilde düşer. Kaynak görüntüleriniz düşük çözünürlüklüyse, önce (ör. OpenCV ile) ölçeklendirmeyi düşünün veya daha yüksek kaliteli bir tarama isteyin.  

### 2. Çok Dilli Belgeler

Aspose OCR, dilleri anlık olarak değiştirebilir, ancak her `recognize` çağrısından önce uygun `Language` enum'ını ayarlamanız gerekir. Karışık dilli sayfalar için motoru iki kez çalıştırmanız—her dil için bir kez—ve ardından sonuçları birleştirmeniz gerekebilir.

### 3. Büyük PDF'ler veya Çok Sayfalı TIFF'ler

PDF'lerde gömülü **resimden metin tanıma** dosyalarına ihtiyacınız varsa, her sayfayı bir görüntü olarak çıkarın (Aspose PDF veya başka bir kütüphane kullanarak) ve OCR motoruna tek tek besleyin. Motor durum‑sızdır, bu yüzden aynı `OcrEngine` örneğini sayfalar arasında yeniden kullanabilirsiniz.

### 4. Yazım Denetimi Hassasiyetini Özelleştirme

Varsayılan yazım denetimi eşiği çoğu İngilizce metin için yeterlidir. Çok teknik belgeler için iç `SpellCheckOptions` ayarlarını değiştirerek hassasiyeti düşürebilirsiniz—ancak bu, Aspose’un ileri seviye API'sine dalmayı gerektirir ve bu başlangıç kılavuzunun kapsamı dışındadır.

---

## Tam Çalışan Örnek (Kopyala-Yapıştır Hazır)

Aşağıda, derlenip çalıştırılmaya hazır tam Java sınıfı yer alıyor. `YOUR_DIRECTORY/typed_scanned_doc.png` ifadesini gerçek görüntü yolunuzla değiştirin.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.enums.*;

public class SpellCheckExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and obtain its configuration object
        OcrEngine ocrEngine = new OcrEngine();
        OcrEngineConfiguration ocrConfig = ocrEngine.getConfiguration();

        // Step 2: Choose the language for recognition and turn on spell‑checking
        ocrConfig.setLanguage(Language.ENGLISH);
        ocrConfig.setSpellCheckEnabled(true);

        // Step 3: (Optional) Provide a custom spell‑check dictionary
        ocrConfig.setSpellCheckDictionary("en_US"); // or a full path to your .dic file

        // Step 4: Run OCR on the input image file
        RecognitionResult recognitionResult = ocrEngine.recognize("YOUR_DIRECTORY/typed_scanned_doc.png");

        // Step 5: Display the corrected text returned by the engine
        System.out.println("Corrected text:");
        System.out.println(recognitionResult.getText());
    }
}
```

Derlemek için:

```bash
javac -cp "path/to/aspose-ocr.jar" SpellCheckExample.java
java -cp ".;path/to/aspose-ocr.jar" SpellCheckExample
```

Konsolda düzeltilmiş metnin yazdırıldığını görmelisiniz; bu, **resimden metin tanıma** işlemini başarıyla gerçekleştirdiğinizi ve yazım denetimini uyguladığınızı doğrular.

---

## Sıkça Sorulan Sorular

**S: Aspose OCR el yazısını destekliyor mu?**  
C: Kütüphane basılı metin için optimize edilmiştir. El yazısı tanıma, ayrı bir modül (`aspose-ocr-handwriting`) içinde mevcuttur ve benzer şekilde entegre edilebilir.

**S: Görüntüyü yerel dosya yerine bir URL'den işleyebilir miyim?**  
C: Evet. Görüntüyü geçici bir tamponda indirin (ör. `java.net.URL` kullanarak) ve bayt dizisini `ocrEngine.recognize(InputStream)` metoduna gönderin.

**S: Görüntünün yalnızca belirli bölgelerini çıkarmam gerekirse ne yapmalıyım?**  
C: `recognize` çağrısından önce `ocrEngine.setRegion(Rectangle)` metodunu kullanın. Bu, OCR'ı tanımlı dikdörtgene sınırlar, zamanı tasarruf eder ve yanlış pozitifleri azaltır.

---

## Sonuç

Aspose OCR for Java kullanarak **resimden metin tanıma** işlemini nasıl yapacağınızı baştan sona gösteren tam bir örnek üzerinden geçtik. OCR motorunu yapılandırarak, yazım denetimini etkinleştirerek ve isteğe bağlı olarak özel bir sözlük yükleyerek, gürültülü taramaları az kodla temiz, aranabilir metne dönüştürebilirsiniz.

Bundan sonra keşfedebilecekleriniz:

- **Batch processing** – bir klasördeki görüntüler üzerinde döngü kurup her sonucu bir veritabanına kaydedin.  
- **Integration with Aspose PDF** – PDF'lerden görüntü çıkarın ve OCR motoruna besleyin.  
- **Advanced language support** – çok dilli projeler için `ocrConfig.setLanguage` değerini `Language.FRENCH` veya `Language.SPANISH` gibi diğer dillere değiştirin.  

Deneyin, ayarları ince ayarlayın ve kaliteyi kendi kullanım senaryonuza göre nasıl artırdığını görün. İyi kodlamalar, ve taramalarınız her zaman net olsun!  

![OCR iş akışını gösteren diyagram](/images/ocr-workflow.png "resimden metin tanıma iş akışı")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}