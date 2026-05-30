---
category: general
date: 2026-05-06
description: Java'da OCR kullanarak görüntüden metin çıkarma. OCR görüntüden metne
  dönüşümünü öğrenin, OCR hatalarını düzeltin ve Aspose OCR ile OCR için görüntüyü
  yükleyin.
draft: false
keywords:
- how to use ocr
- extract text from image
- ocr image to text
- correct ocr errors
- load image for ocr
language: tr
og_description: Java'da OCR kullanarak görüntüden metin çıkarma, OCR hatalarını düzeltme
  ve Aspose OCR ile OCR için görüntü yükleme.
og_title: Java’da OCR Nasıl Kullanılır – Tam Kılavuz
tags:
- OCR
- Java
- Aspose
title: Java'da OCR Nasıl Kullanılır – Görüntüden Metin Çıkarma ve Yazım Düzeltmesi
url: /tr/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java’da OCR Nasıl Kullanılır – Görüntüden Metin Çıkarma ve Yazım Düzeltmesi

Bulanık bir fiş fotoğrafını temiz, aranabilir bir metne **nasıl OCR kullanarak** dönüştürebileceğinizi hiç merak ettiniz mi? Tek başınıza değilsiniz. Birçok projede—gider takibi uygulamaları, fatura dijitalleştirme hatları veya hızlı bir not alma betiği—bir görüntüden güvenilir metin elde etmek ilk engeldir.  

Bu öğretici, OCR’u Java’da nasıl kullanacağınızı adım adım gösteriyor; görüntüyü OCR’a yüklemekten OCR hatalarını düzeltmeye kadar her şeyi kapsıyor, böylece sonuç bir insan tarafından yazılmış gibi görünecek. Sonunda **görüntüden metin çıkarma**, **OCR görüntüden metne** dönüşümü yapabilecek ve yaygın tanıma hatalarını otomatik olarak düzeltebileceksiniz.

## Ne Oluşturacaksınız

Küçük bir Java konsol programı oluşturacağız:

1. PNG (veya desteklenen herhangi bir format) dosyasını Aspose OCR motoruna yükleyecek.  
2. Dahili yazım‑düzeltme özelliğini etkinleştirerek **OCR hatalarını düzeltecek**.  
3. Tanıma sürecini çalıştırıp temizlenmiş metni ekrana basacak.  

Harici hizmetler, ağır çerçeveler yok—tek bir JAR ve birkaç satır kod yeterli.

### Ön Koşullar

- Java Development Kit (JDK) 8 veya daha yeni bir sürüm.  
- Maven (veya herhangi bir build aracı) ile Aspose OCR kütüphanesini çekmek.  
- Analiz etmek istediğiniz bir görüntü dosyası (ör. `receipt.png`).  

Eğer Aspose OCR JAR’ınız yoksa, `pom.xml` dosyanıza şu bağımlılığı ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

> **Pro ipucu:** Ücretsiz değerlendirme sürümü test için çalışır, ancak bir lisans değerlendirme filigranını kaldırır.

## Adım 1 – OCR Motorunu Başlatma (Primary Keyword in Action)

İlk yapmanız gereken `OcrEngine` örneği oluşturmaktır. Bunu, pikselleri okuyup karakterlere dönüştürecek beyin olarak düşünün.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Initialise the OCR engine – this is where we start using OCR
        OcrEngine ocrEngine = new OcrEngine();
```

*Neden önemli:* Motorun başlatılması iç kaynakları (dil modelleri, sözlükler vb.) hazırlar. Bu adımı atlamak, bir görüntü yüklemeye çalıştığınızda `NullPointerException` almanıza sebep olur.

## Adım 2 – OCR İçin Görüntüyü Yükleme

Şimdi **OCR için görüntüyü yükleyeceğiz**. Aspose, kullanışlı bir `ImageStream.fromFile` yardımcı metodu sağlar, ama isterseniz bir `byte[]` de verebilirsiniz.

```java
        // Load the image you want to analyse – replace the path with your own file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));
```

*Yaygın tuzak:* Dosya yolu mutlak ya da çalışma dizinine göre göreceli olmalıdır. Görüntü bulunamazsa motor bir `IOException` fırlatır. Özellikle bir IDE’den çalıştırırken ya da paketlenmiş JAR’dan çalıştırırken yolu iki kez kontrol edin.

## Adım 3 – **OCR Hatalarını Düzeltmek** İçin Yazım Düzeltmeyi Etkinleştirme

Kutudan çıkar çıkmaz OCR gürültülü olabilir—“l0ve” yerine “love” ya da “O” yerine “0”. Yazım düzeltmeyi etkinleştirmek, motorun tipik hataları düzelten bir son‑işlem aşaması çalıştırmasını sağlar.

```java
        // Turn on the spell‑correction feature – this helps to correct OCR errors
        ocrEngine.getSettings().setEnableSpellCorrection(true);
```

*Neden tercih etmelisiniz:* Yazım düzeltme olmadan çıktıyı manuel olarak temizlemeniz gerekir, bu da otomasyon amacını bozar. Dahili sözlük İngilizce ve birkaç diğer dil için iyi çalışır.

## Adım 4 – Tanıma İşlemini Gerçekleştirme (**OCR Görüntüden Metne**)

Görüntü yüklendi ve yazım düzeltme etkinleştirildi, artık motoru metni tanıması için isteyebiliriz.

```java
        // Run the OCR process – this converts the image to text
        OcrResult ocrResult = ocrEngine.recognize();
```

*Köşe durumu:* Görüntü düşük kontrastlı ya da çok eğikse sonuç hâlâ anlamsız karakterler içerebilir. Motoru beslemeden önce ön‑işleme (ör. ikilileştirme, eğrilik düzeltme) yapmayı düşünün.

## Adım 5 – Temizlenmiş Metni Çıktı Olarak Verme

Son adım sadece sonucu ekrana basmaktır. Gerçek bir uygulamada bunu bir veritabanına ya da dosyaya yazabilirsiniz, ancak bu demo için `System.out` yeterlidir.

```java
        // Display the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

### Beklenen Çıktı

`receipt.png` net bir ürün listesi içeriyorsa, aşağıdaki gibi bir çıktı görebilirsiniz:

```
Corrected text:
Item           Qty   Price
Apple          2     $1.20
Banana         5     $0.75
Total               $5.55
```

Orijinal taramada “Qy” gibi bir hata olsa bile “Qty” ve “Price” doğru şekilde yazılmıştır.

## Tam Çalışan Örnek

Aşağıda `SpellCorrectDemo.java` adlı bir dosyaya kopyalayıp yapıştırabileceğiniz tam program yer alıyor. Aspose OCR JAR’ın sınıf yolunda olduğundan emin olun.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // Replace "YOUR_DIRECTORY/receipt.png" with the actual path
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));

        // Step 3: Enable spell correction to improve accuracy
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Step 4: Perform OCR recognition (OCR image to text)
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

Şu komutla çalıştırın:

```bash
javac -cp "aspose-ocr-23.9.jar" SpellCorrectDemo.java
java -cp ".:aspose-ocr-23.9.jar" SpellCorrectDemo
```

Artık temizlenmiş metnin konsolda çıktısını göreceksiniz.

## Bonus: Daha İyi Doğruluk İçin Ayarları İnce Ayarlama

Varsayılan yapılandırma çoğu basılı belge için işe yarasa da, özel senaryolar için birkaç parametreyi ayarlamanız gerekebilir:

| Ayar | Ne İşe Yarar | Ne Zaman Değiştirilir |
|------|--------------|-----------------------|
| `setLanguage(OcrLanguage.English)` | İngilizce sözlüğü zorlar (yanlış pozitifleri azaltır) | Görüntünüz sadece İngilizce metin içeriyorsa. |
| `setResolution(300)` | Kaynak görüntünün DPI değerini belirtir | Yüksek çözünürlüklü taramalar için. |
| `setEnableAutoSkewCorrection(true)` | Hafif eğik sayfaları otomatik döndürür | Görüntüler telefonla çekildiyse. |

```java
ocrEngine.getSettings().setLanguage(OcrLanguage.English);
ocrEngine.getSettings().setResolution(300);
ocrEngine.getSettings().setEnableAutoSkewCorrection(true);
```

## Sık Sorulan Sorular

**S: Bu PDF’lerle çalışır mı?**  
C: Evet. Her PDF sayfasını bir görüntüye dönüştürün (ör. Aspose PDF kullanarak) ve görüntüyü OCR motoruna besleyin.

**S: Görüntüm BMP formatında ise ne yapmalıyım?**  
C: `ImageStream.fromFile` PNG, JPEG, BMP, TIFF ve GIF formatlarını kutudan çıkar çıkmaz destekler. Sadece dosya uzantısını değiştirin.

**S: Yazım düzeltmeyi devre dışı bırakabilir miyim?**  
C: Kesinlikle—`setEnableSpellCorrection(false)` ayarını yaparak ham OCR çıktısını alabilirsiniz.

## Sonuç

Artık **Java’da OCR nasıl kullanılır** ve **görüntüden metin çıkarma**, **OCR hatalarını otomatik düzeltme** ve Aspose OCR ile **OCR için görüntü yükleme** konularını biliyorsunuz. Başlatma, yükleme, yazım düzeltme etkinleştirme, tanıma ve çıktı adımlarından oluşan beş adımlık akış, günlük OCR görevlerinin çoğunu kapsar.  

Bundan sonra bu mantığı bir veritabanına yazma, bir REST uç noktası ya da toplu işleyiciyle birleştirerek yüzlerce fişi aynı anda işleyebilirsiniz. Yukarıdaki ek ayarlar tablosunu deneyerek doğruluğu en üst seviyeye çıkarmayı unutmayın.

İyi kodlamalar, ve OCR sonuçlarınız her zaman kahve lekeli fişlerinizden daha temiz olsun! 

![ocr kullanma diyagramı: görüntü → OCR motoru → düzeltilmiş metin akışı]

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}