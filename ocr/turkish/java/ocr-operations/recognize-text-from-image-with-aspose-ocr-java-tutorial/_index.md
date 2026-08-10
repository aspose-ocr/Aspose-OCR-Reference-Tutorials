---
category: general
date: 2026-02-17
description: Aspose OCR Java kütüphanesini kullanarak görüntüden metin tanımayı ve
  OCR için görüntüyü yüklemeyi öğrenin. Yazım düzeltmeli adım adım kılavuz.
draft: false
keywords:
- recognize text from image
- load image for OCR
- Aspose OCR Java
- spell corrector OCR
- OCR engine setup
language: tr
og_description: Aspose OCR Java kullanarak görüntüden metin tanıma. Bu öğreticide
  OCR için görüntünün nasıl yükleneceği, yazım düzeltmesinin nasıl etkinleştirileceği
  ve temiz metnin nasıl çıktılanacağı gösterilmektedir.
og_title: görüntüden metin tanıma – Tam Aspose OCR Java Rehberi
tags:
- Java
- OCR
- Aspose
title: Aspose OCR ile görüntüden metin tanıma – Java Öğreticisi
url: /tr/java/ocr-operations/recognize-text-from-image-with-aspose-ocr-java-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# recognize text from image with Aspose OCR – Java Tutorial

Hiç **görüntüden metin tanıma** yapmak istediniz ama hangi kütüphaneyi seçeceğinizi bilemediniz mi? Tek başınıza değilsiniz. Gerçek dünyadaki birçok projede—faturaları tarama, el yazısı notları dijitalleştirme ya da ekran görüntülerinden altyazı çıkarma gibi—doğru OCR sonuçları elde etmek çok önemlidir.  

Bu rehberde bir resmi OCR için yüklemeyi, Aspose OCR’ın yerleşik imla düzelticisini açmayı ve sonunda temizlenmiş metni yazdırmayı adım adım göstereceğiz. Sonunda sadece birkaç satır kodla **görüntüden metin tanıma** yapabilen çalışır bir Java programınız olacak.

## What This Tutorial Covers

- Aspose OCR lisansınızı nasıl uygulayacağınız (demo su işareti olmadan çalışır)  
- Bir `OcrEngine` örneği oluşturup tanıma dili olarak İngilizce seçmek  
- **Load image for OCR** işlemini `OcrInput` ile yapmak ve içinde hatalı kelimeler bulunan bir PNG’ye işaret etmek  
- İmla düzelticiyi etkinleştirmek, isteğe bağlı olarak özel bir sözlüğe yönlendirmek  
- Tanıma işlemini çalıştırıp düzeltilmiş sonucu yazdırmak  

Harici hizmetler, gizli yapılandırma dosyaları yok—sadece saf Java ve Aspose OCR JAR.

> **Pro tip:** Aspose’a yeniyseniz, Aspose web sitesinden ücretsiz 30‑günlük deneme lisansını alın ve `.lic` dosyasını kodunuzdan referans verebileceğiniz bir klasöre koyun.

## Prerequisites

- Java 8 veya daha yeni (kod JDK 11 ile de derlenir)  
- Aspose.OCR for Java JAR’ı sınıf yolunuzda  
- Geçerli bir `Aspose.OCR.lic` dosyası (ya da değerlendirme modunda çalışabilirsiniz, ancak demo bir su işareti ekleyecektir)  
- Bilerek yazım hataları içeren bir görüntü dosyası (`misspelled.png`)—imla düzelticinin nasıl çalıştığını görmek için ideal  

Hepsi hazır mı? Harika—hadi başlayalım.

## Step 1: Apply Your Aspose OCR License

Motor ağır işi yapmadan önce lisanslı olduğunuzu bilmesi gerekir. Aksi takdirde çıktıda “Trial version” bannerı görürsünüz.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {
        // Load the license – replace the path with where you stored your .lic file
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

*Bu neden önemli:* Lisans, deneme su işaretini devre dışı bırakır ve tam imla‑düzeltici sözlüğünün kilidini açar. Bu adımı atlamak çalışır, ancak çıktınız “Aspose OCR Demo” metniyle kirlenir.

## Step 2: Create and Configure the OCR Engine

Şimdi motoru başlatıp hangi dili kullanacağını söylüyoruz. İngilizce en yaygın olanıdır, ancak Aspose onlarca dili destekler.

```java
        // Step 2: Instantiate the OCR engine
        OcrEngine engine = new OcrEngine();

        // Choose English for recognition – you could pick French, German, etc.
        engine.getLanguage().setLanguage(OcrLanguage.ENGLISH);
```

*Dili neden ayarlıyoruz:* Dil modeli karakter setini belirler ve imla‑düzelticinin önerilerini etkiler. Yanlış dil seçimi doğruluğu büyük ölçüde düşürebilir.

## Step 3: Enable Spell Correction and (Optionally) Point to a Custom Dictionary

Aspose OCR, yerleşik bir İngilizce sözlükle gelir, ancak alan‑özgü terimleriniz (örneğin tıbbi jargon ya da ürün kodları) varsa kendi sözlüğünüzü de sağlayabilirsiniz.

```java
        // Step 3: Turn on the spell corrector
        engine.getSpellCorrector().setEnable(true); // activate spell‑checking

        // Optional: use a custom dictionary folder
        // engine.getSpellCorrector().setDictionaryPath("YOUR_DIRECTORY/dictionaries/english");
```

*Düzelticinin yaptığı:* OCR motoru sözlükte bulunmayan bir kelime gördüğünde, en yakın eşleşmeyle değiştirmeye çalışır. Bu yüzden demo “recieve” kelimesini otomatik olarak “receive” yapabilir.

## Step 4: Load the Image for OCR

İşte **load image for OCR** sorusunun doğrudan cevabı. Bir `OcrInput` nesnesi oluşturup PNG dosyamızı ekliyoruz.

```java
        // Step 4: Prepare the image input
        OcrInput input = new OcrInput();
        input.add("YOUR_DIRECTORY/misspelled.png"); // path to the image you want to process
```

*`OcrInput` neden kullanıyoruz:* Dosya okuma mantığını soyutlar ve ileride çok sayfalı PDF ya da bir dizi görüntü işlemek isterseniz birden fazla sayfa eklemenize olanak tanır.

## Step 5: Run the Recognition and Retrieve Corrected Text

Motor şimdi ağır işi yapıyor—karakterleri tanıyor, dil modelini uyguluyor ve sonunda imla düzeltmesi yapıyor.

```java
        // Step 5: Perform OCR and obtain the corrected result
        OcrResult result = engine.recognize(input);

        // Step 6: Output the corrected text to the console
        System.out.println("Corrected text:\n" + result.getText());
    }
}
```

*Beklenen çıktı:* `misspelled.png` içinde “Ths is a smple test” ifadesi varsa, konsol şu şekilde yazdırır:

```
Corrected text:
This is a simple test
```

Yanlış yazılmış kelimelerin (`Ths`, `smple`) otomatik olarak düzeltildiğine dikkat edin.

## Full, Ready‑to‑Run Example

Aşağıda tüm program tek bir blokta verilmiştir. Kopyalayıp yapıştırın, yolları ayarlayın ve **Run** tuşuna basın.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {
        // Apply the Aspose.OCR license (replace with your license file)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");

        // Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Select the language for recognition (e.g., English)
        engine.getLanguage().setLanguage(OcrLanguage.ENGLISH);

        // Enable the built‑in spell corrector and optionally set a custom dictionary
        engine.getSpellCorrector().setEnable(true);                     // activate spell‑checking
        // engine.getSpellCorrector().setDictionaryPath("YOUR_DIRECTORY/dictionaries/english"); // optional

        // Prepare the input image containing the text to be recognized
        OcrInput input = new OcrInput();
        input.add("YOUR_DIRECTORY/misspelled.png"); // load image for OCR

        // Perform OCR and obtain the corrected result
        OcrResult result = engine.recognize(input);

        // Output the corrected text
        System.out.println("Corrected text:\n" + result.getText());
    }
}
```

**İpucu:** PNG yerine JPEG ya da BMP işlemek isterseniz sadece dosya uzantısını değiştirin—Aspose OCR tüm yaygın raster formatlarını destekler.

## Common Questions & Edge Cases

- **Görüntüm düşük çözünürlükte ise ne yapmalıyım?**  
  Aspose’a vermeden önce DPI’yı artırmak için `java.awt.Image` gibi bir kütüphane ile yeniden ölçeklendirin. Daha yüksek DPI, motorun daha fazla pikselle çalışmasını sağlar ve genellikle doğruluğu artırır.

- **Aynı görüntüde birden fazla dili tanıyabilir miyim?**  
  Evet. `engine.getLanguage().setLanguage(OcrLanguage.MULTI_LANGUAGE);` çağırın ve isteğe bağlı olarak `engine.getLanguage().addLanguage(OcrLanguage.SPANISH);` gibi bir dil listesi ekleyin.

- **Özel sözlüğüm kullanılmıyor—neden?**  
  Klasörün her satırda bir kelime olacak şekilde düz metin dosyaları içerdiğinden ve yolun mutlak ya da çalışma dizinine göre doğru olduğundan emin olun.

- **Güven skorlarını nasıl çıkarırım?**  
  `result.getConfidence()` tüm sayfa için 0 ile 1 arasında bir float döndürür. Karakter bazında güven için `result.getWordList()` metodunu inceleyin.

## Conclusion

Artık Aspose OCR for Java kullanarak **görüntüden metin tanıma**, **load image for OCR** ve yaygın yazım hatalarını temizleyen imla‑düzelticiyi nasıl etkinleştireceğinizi biliyorsunuz. Yukarıdaki tam örnek, herhangi bir Maven ya da Gradle projesine eklenmeye hazır ve birkaç ayarlama ile klasörleri toplu işlemek, bir web servisine bağlamak ya da bir belge yönetim sistemiyle bütünleştirmek mümkün.

Bir sonraki adıma hazır mısınız? Çok sayfalı bir PDF deneyin, sektöre özgü terimler için özel bir sözlükle oynayın ya da çıktıyı bir çeviri API’sine zincirleyin. Olasılıklar sınırsız ve temel akış—lisans → motor → dil → imla‑düzeltici → giriş → tanıma → çıktı—her zaman aynı kalır.

İyi kodlamalar, OCR sonuçlarınız her zaman kusursuz olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}