---
category: general
date: 2026-06-19
description: Aspose OCR ile Java’da görüntüden metin tanıyın. Yazım denetimini nasıl
  etkinleştireceğinizi, sözlük ekleyeceğinizi ve tek bir öğreticide yazım denetimli
  OCR nasıl yapacağınızı öğrenin.
draft: false
keywords:
- recognize text from image
- how to enable spellcheck
- how to add dictionary
- ocr with spell check
language: tr
og_description: Java'da Aspense OCR kullanarak görüntüden metin tanıyın. Bu kılavuz,
  yazım denetimini etkinleştirmeyi, sözlük eklemeyi ve yazım denetimiyle OCR çalıştırmayı
  gösterir.
og_title: Görüntüden Metin Tanıma – Aspose OCR Yazım Denetimi Öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Recognize text from image with Aspose OCR in Java. Learn how to enable
    spellcheck, add dictionary, and perform OCR with spell check in a single tutorial.
  headline: Recognize Text from Image in Java – Complete Aspose OCR Spell‑Check Guide
  type: TechArticle
- description: Recognize text from image with Aspose OCR in Java. Learn how to enable
    spellcheck, add dictionary, and perform OCR with spell check in a single tutorial.
  name: Recognize Text from Image in Java – Complete Aspose OCR Spell‑Check Guide
  steps:
  - name: How to Enable SpellCheck
    text: 'The spell checker lives inside the engine, but it’s disabled by default.
      Flip the switch with a single line:'
  - name: Expected Output
    text: 'Assuming `receipt.png` contains the line “Totel: $12.99” and your custom
      dictionary includes “Total”, the console will display:'
  - name: What if I need multiple languages?
    text: You can call `ocrEngine.setLanguage(Language.English, Language.French)`
      to enable multilingual recognition. Spell‑checking will follow each language’s
      rules, but you still need to enable it with `setEnable(true)`.
  - name: How does the engine handle unknown words?
    text: If a word isn’t in the internal dictionary *and* not in your custom dictionary,
      the spell checker attempts a best‑guess correction based on Levenshtein distance.
      For truly unknown terms, add them to `my-terms.txt`.
  - name: Does the spell checker work on numbers?
    text: By default, numeric strings are left untouched. If you have alphanumeric
      codes (e.g., “AB12C”), add them to your custom dictionary; otherwise the engine
      may try to “fix” them to real words.
  - name: Performance considerations
    text: Enabling spell checking adds a modest overhead—roughly 10‑15 % extra CPU
      per page. For batch processing, consider disabling it on the first pass, then
      re‑run only on pages that failed quality checks.
  type: HowTo
tags:
- OCR
- Java
- SpellCheck
title: Java'da Görüntüden Metin Tanıma – Tam Aspose OCR Yazım Denetimi Rehberi
url: /tr/java/advanced-ocr-techniques/recognize-text-from-image-in-java-complete-aspose-ocr-spell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüden Metin Tanıma Java’da – Tam Aspose OCR Yazım Kontrol Kılavuzu

Hiç **görüntüden metin tanıma** yapmak isterken çıktının hatalarla dolu olacağından endişe ettiniz mi? Yalnız değilsiniz. Birçok fiş tarama veya belge dijitalleştirme projesinde ham OCR metni, uykulu bir kedinin yazdığı izlenimini verir. İyi haber? Aspose OCR ile bu gürültülü dökümanı temiz, yazım‑kontrolü yapılmış metne dönüştürebilirsiniz—tamamen Java içinde.

Bu öğreticide, **yazım kontrolünü nasıl etkinleştirileceğini**, **alan‑spesifik terimler için sözlük nasıl ekleneceğini** ve nihayetinde **yazım kontrolüyle OCR** nasıl yapılacağını gösteren çalıştırılabilir bir örnek üzerinden ilerleyeceğiz. Sonunda, bir görüntü dosyasını okuyup anında yazım hatalarını düzelten ve düzeltilmiş sonucu ekrana yazdıran bağımsız bir programınız olacak.

## Öğrenecekleriniz

- Aspose OCR lisansını nasıl uygulayacağınızı ve API’nin tam hızda çalışmasını sağlayacağınızı.  
- OCR motorunda **yazım kontrolünü etkinleştirme** adımlarını.  
- Ürün kodları veya marka adları gibi terimler için **özel bir sözlük** eklemenin doğru yolunu.  
- `recognizeImage` metodunu çağırarak temiz, düzeltilmiş metni nasıl alacağınızı.  

Harici araçlar yok, el yapımı yazım‑kontrol kütüphaneleri yok—sadece saf Java ve Aspose OCR.

## Ön Koşullar

- Java 8+ (kod, herhangi bir güncel JDK ile derlenebilir).  
- Bir Aspose OCR lisans dosyası (`Aspose.OCR.lic`). Sadece deneme yapıyorsanız, ücretsiz değerlendirme sürümü çalışır ancak filigran ekler.  
- `aspose-ocr` bağımlılığını çekmek için Maven ya da Gradle, ya da JAR dosyalarını manuel olarak ekleyebilirsiniz.  
- Örnek bir görüntü (ör. bir fiş PNG’si) ve özel terimleri içeren bir metin dosyası.

> **Pro ipucu:** Özel sözlüğünüzü UTF‑8 formatında ve satır başına bir terim olacak şekilde tutun—Aspose OCR dosya sisteminden doğrudan okur.

---

## Adım 1: Projeyi Kurun ve Aspose OCR Bağımlılığını Ekleyin

Maven kullanıyorsanız, `pom.xml` dosyanıza aşağıdaki snippet’i ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.8</version> <!-- use the latest version -->
</dependency>
```

Gradle için aynı fikir geçerlidir:

```groovy
implementation 'com.aspose:aspose-ocr:23.8'
```

Bağımlılık çözüldükten sonra, sihrin gerçekleşeceği yeni bir Java sınıfı oluşturun ve adını `SpellCheckDemo` koyun.

## Adım 2: Aspose OCR Lisansını Uygulayın

Herhangi bir OCR işlemine başlamadan önce, Aspose’a sınırsız çalışmasına izin verdiğinizi söylemelisiniz. Bu adımı atlamak, çalışma zamanı istisnasına yol açar.

```java
// Apply the Aspose OCR license – this removes evaluation watermarks
License license = new License();
license.setLicense("Aspose.OCR.lic");   // path to your .lic file
```

> **Neden önemli:** Lisans, dahili yazım‑kontrol modülü dahil olmak üzere tam OCR motorunun kilidini açar. Lisans olmadan motor çalışır ancak bazı premium özellikleri kullanamaz.

## Adım 3: OCR Motorunu Oluşturun ve Yapılandırın

Şimdi temel `OcrEngine` nesnesini örnekleyip dili İngilizce olarak ayarlıyoruz. Bu, tanıma ve yazım‑kontrolü için temel oluşturur.

```java
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.setLanguage(Language.English);   // choose the language that matches your image
```

### Yazım Kontrolünü Nasıl Etkinleştirirsiniz

Yazım denetleyicisi motorun içinde bulunur, ancak varsayılan olarak kapalıdır. Tek bir satırla açabilirsiniz:

```java
ocrEngine.getSpellChecker().setEnable(true);   // enables spell‑checking
```

Bu satır, **yazım kontrolünü nasıl etkinleştirirsiniz** gereksinimini karşılar. Etkinleştirildiğinde, motor her tanınan kelimeyi iç sözlüğüyle otomatik olarak karşılaştırır ve düzeltme önerir.

## Adım 4: Özel Sözlük Yükleyin (Sözlük Nasıl Eklenir)

Belgeleriniz jargon içeriyorsa—ör. ürün SKU’ları, tıbbi terimler veya marka adları—yazım denetleyicisine bunları öğretmek isteyeceksiniz. Aspose OCR, satır başına bir terim olacak düz metin dosyasına işaret etmenize izin verir.

```java
// Load a custom word list for spell‑checking
Path customDict = java.nio.file.Paths.get("YOUR_DIRECTORY/my-terms.txt");
ocrEngine.getSpellChecker().addUserDictionary(customDict);
```

> **Dosya bulunamazsa ne olur?** API bir `FileNotFoundException` fırlatır. Daha nazik bir hata yönetimi için çağrıyı `try/catch` bloğuna alın.

Artık motor “AcmeWidget” veya “RX‑9000” gibi kelimeleri hatalı olarak işaret etmeyecek.

## Adım 5: Görüntüden Metin Tanıyın

Motor hazır olduğuna göre, nihayet **görüntüden metin tanıma** işlemini gerçekleştirebilirsiniz. `recognizeImage` metodu, ham ve düzeltilmiş metni içeren bir `OcrResult` nesnesi döndürür.

```java
// Recognize text from the image file
OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/receipt.png");
```

Yazım kontrolünü daha önce açtığımız için, `getText()` çağrısı zaten düzeltilmiş versiyonu verir.

## Adım 6: Düzeltlenmiş Metni Çıktılayın

Kalan tek şey, temizlenmiş dizeyi yazdırmak (veya saklamaktır).

```java
// Output the corrected, spell‑checked text
System.out.println(ocrResult.getText());
```

Programı çalıştırdığınızda, orijinal görüntüde lekeli karakterler olsa bile düzgün bir şekilde biçimlendirilmiş ve doğru yazımlı bir fiş görmelisiniz.

---

## Tam Çalışan Örnek

Aşağıda, tamamen çalıştırılabilir Java programı yer alıyor. IDE’nize kopyalayıp yapıştırın, dosya yollarını ayarlayın ve **Run** tuşuna basın.

```java
import com.aspose.ocr.*;

import java.nio.file.Path;
import java.nio.file.Paths;

public class SpellCheckDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Apply the Aspose OCR license
        License license = new License();
        license.setLicense("Aspose.OCR.lic");   // <-- replace with your license path

        // Step 2: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setLanguage(Language.English);

        // Step 3: Load a custom word list for spell‑checking
        Path dictPath = Paths.get("YOUR_DIRECTORY/my-terms.txt"); // <-- your dictionary file
        ocrEngine.getSpellChecker().addUserDictionary(dictPath);
        ocrEngine.getSpellChecker().setEnable(true); // <-- how to enable spellcheck

        // Step 4: Recognize text from the image
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/receipt.png"); // <-- your image

        // Step 5: Output the corrected text
        System.out.println(ocrResult.getText());
    }
}
```

### Beklenen Çıktı

`receipt.png` dosyasının “Totel: $12.99” satırını içerdiğini ve özel sözlüğünüzde “Total” kelimesinin bulunduğunu varsayalım; konsol şu şekilde görüntülenecek:

```
Total: $12.99
```

“Totel” yazım hatası, **yazım kontrolüyle OCR** sayesinde otomatik olarak düzeltilmiştir.

---

## Yaygın Sorular & Kenar Durumları

### Birden fazla dil gerekir mi?

`ocrEngine.setLanguage(Language.English, Language.French)` şeklinde çağırarak çok‑dilli tanımayı etkinleştirebilirsiniz. Yazım‑kontrolü her dilin kurallarına göre çalışır, ancak yine de `setEnable(true)` ile açılmalıdır.

### Motor bilinmeyen kelimeleri nasıl ele alır?

Bir kelime hem iç sözlükte *hem* özel sözlüğünüzde yoksa, yazım denetleyicisi Levenshtein mesafesine dayalı en iyi tahmini yapar. Gerçekten bilinmeyen terimler için `my-terms.txt` dosyasına ekleyin.

### Sayılar üzerinde yazım denetleyicisi çalışır mı?

Varsayılan olarak sayısal dizgiler dokunulmaz. Alfanümerik kodlar (ör. “AB12C”) varsa, bunları özel sözlüğe ekleyin; aksi takdirde motor bunları gerçek kelimelere “düzeltmeye” çalışabilir.

### Performans düşünceleri

Yazım kontrolünün etkinleştirilmesi, sayfa başına yaklaşık %10‑15 ekstra CPU yükü getirir. Toplu işleme için ilk geçişte devre dışı bırakıp, kalite kontrolünden geçen sayfalarda tekrar çalıştırmayı düşünebilirsiniz.

---

## Özet

Aspose OCR kullanarak Java’da **görüntüden metin tanıma** yaparken çıktıyı temiz tutmak için ihtiyacınız olan her şeyi ele aldık. Adımlar şunlardı:

1. Lisansı uygulayın.  
2. `OcrEngine` oluşturun ve dili ayarlayın.  
3. **Sözlük Nasıl Eklenir** – özel kelime listesini yükleyin.  
4. **Yazım Kontrolü Nasıl Etkinleştirilir** – denetleyiciyi açın.  
5. `recognizeImage` (temel **yazım kontrolüyle OCR** çağrısı) çalıştırın.  
6. Düzeltlenmiş metni yazdırın.

Böylece ham piksellerden cilalı, yazım‑kontrolü yapılmış satırlara kadar tam bir akış elde ettik.

---

## Sıradaki Adımlar

- **Toplu işleme:** Bir klasördeki tüm görüntüleri döngüye alıp her sonucu ayrı bir `.txt` dosyasına yazın.  
- **PDF çıktısı:** Aspose PDF kullanarak düzeltilmiş metni aranabilir bir PDF’e gömün.  
- **Gelişmiş sözlükler:** Farklı alanlar (ör. finans vs. tıp) için birden fazla kullanıcı sözlüğü yükleyin.  
- **Güven skorları:** `ocrResult.getConfidence()` ile düşük güvenilirlikli sonuçları filtreleyin.

Denemeler yapmaktan çekinmeyin—dili değiştirin, sözlüğü ayarlayın veya görüntü‑ön işleme kütüphaneleriyle birleştirerek doğruluğu artırın.

Herhangi bir sorunla karşılaşırsanız, aşağıya yorum bırakın. İyi kodlamalar, ve OCR’unuz her zaman yazım‑kontrolüyle olsun!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanarak ilgili konuları derinleştirir. Her kaynak, tam çalışan kod örnekleri ve adım‑adım açıklamalar içerir, böylece API özelliklerini daha iyi kavrayabilir ve projelerinizde alternatif yaklaşımları keşfedebilirsiniz.

- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to extract text from image from URL using Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}