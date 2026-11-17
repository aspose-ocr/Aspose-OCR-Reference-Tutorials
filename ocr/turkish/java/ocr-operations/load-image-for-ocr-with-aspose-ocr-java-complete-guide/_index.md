---
category: general
date: 2026-05-31
description: Aspose OCR Java kütüphanesini kullanarak OCR için görüntü yükleme – imla
  düzeltme, dil ayarları ve en iyi 3 öneri içeren adım adım kılavuz.
draft: false
keywords:
- load image for OCR
- Aspose OCR Java
- spell correction OCR
- OCR engine Java
- set OCR language
- max suggestions OCR
language: tr
og_description: Aspose OCR ile Java’da OCR için görüntü yükleyin. Yazım düzeltmeyi
  nasıl etkinleştireceğinizi, dili nasıl ayarlayacağınızı ve önerileri en üst üçe
  sınırlayacağınızı öğrenin.
og_title: Aspose OCR Java ile OCR için Görüntü Yükleme – Tam Rehber
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Load image for OCR using Aspose OCR Java library – step‑by‑step guide
    with spell correction, language settings, and top‑3 suggestions.
  headline: Load Image for OCR with Aspose OCR Java – Complete Guide
  type: TechArticle
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Aspose OCR Java ile OCR için Görüntü Yükleme – Tam Kılavuz
url: /tr/java/ocr-operations/load-image-for-ocr-with-aspose-ocr-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR için Görüntü Yükleme – Aspose OCR Java – Tam Kılavuz

Bir Java uygulamasında **OCR için görüntü yüklemek** mi istiyorsunuz? Bu konuda yalnız değilsiniz. Neyse ki, Aspose OCR for Java, özellikle hece düzeltmesini de eklediğinizde, süreci neredeyse sorunsuz hâle getiriyor.

Bu öğreticide, hatalı yazılmış metnin bir resmini OCR motoruna nasıl aktaracağınızı, **hece düzeltmesini** nasıl açacağınızı, önerileri en iyi üçe sınırlayacağınızı ve sonunda düzeltilmiş sonucu nasıl yazdıracağınızı adım adım göstereceğiz. Sonunda, herhangi bir projeye ekleyebileceğiniz çalıştırılabilir bir programınız olacak.

## Öğrenecekleriniz

- **Aspose OCR Java** lisansınızı nasıl uygulayacağınızı ve kütüphanenin filigran olmadan çalışmasını sağlayacağınızı.  
- `OcrImage` kullanarak **OCR için görüntü yüklemenin** tam yolunu.  
- OCR dilini ayarlama (evet, bir anda İngilizceden Fransızcaya geçebilirsiniz).  
- **Hece düzeltme OCR** özelliğini etkinleştirme ve `max suggestions` sınırını yapılandırma.  
- Motoru çalıştırma ve temiz, düzeltilmiş metni elde etme.  

Aspose ile daha önce çalışmış olmanız gerekmez; sadece Java‑uyumlu bir IDE ve küçük bir görüntü dosyası yeterli. Hadi başlayalım.

![Diagram showing the flow of loading an image for OCR, applying spell correction, and retrieving text](load-image-ocr.png "load image for OCR diagram")

## Adım 1 – OCR için Görüntü Yükleme

İlk yapmanız gereken, okumak istediğiniz metni içeren resmi motora göstermek. Aspose’da bu tek bir satırdır:

```java
// Step 1: Load the image that contains misspelled text
engine.setImage(new OcrImage("YOUR_DIRECTORY/misspelled.png"));
```

`OcrImage` bir dosya yolu, bir akış (stream) ya da hatta bir `BufferedImage` kabul eder. Görüntünüz sınıf yolunda (classpath) ise, birim testleri için ideal olan `getResourceAsStream` kullanabilirsiniz.  

> **Pro ipucu:** Görüntü dosyalarınızı 2 MB’ın altında tutun; daha büyük dosyalar bellek kullanımını önemli ölçüde artırır ve OCR motorunu yavaşlatabilir.

## Adım 2 – Aspose OCR Lisansını Başlatma

Motor faydalı bir şey yapmadan önce geçerli bir lisansa ihtiyacınız var; aksi takdirde filigranlı çıktı ve konsolda bir uyarı alırsınız.

```java
// Step 2: Apply your Aspose OCR license
License license = new License();
license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");
```

Henüz bir lisansınız yoksa, Aspose portalından ücretsiz geçici bir lisans talep edebilirsiniz. `.lic` dosyasını uygulamanızın okuyabileceği bir yere koyun, hepsi bu kadar.

## Adım 3 – OCR Motorunu ve Dili Yapılandırma

Dil ayarı olmayan bir OCR motoru, haritasız bir GPS gibidir—kaybolur. İngilizce için şu şekilde ayarlarız:

```java
// Step 3: Create an OCR engine and set the language to English
OcrEngine engine = new OcrEngine();
engine.setLanguage(OcrLanguage.ENGLISH);
```

Dilleri değiştirmek, `OcrLanguage.ENGLISH` yerine `OcrLanguage.FRENCH`, `OcrLanguage.SPANISH` vb. kullanmak kadar kolaydır. Kütüphane, onlarca yerleşik dil paketini içerir.

## Adım 4 – Hece Düzeltmeyi Etkinleştir ve Maksimum Öneri Sayısını Ayarla

Şimdi demomuzu sıradan bir OCR çalıştırmasından ayıran sihirli kısım: **hece düzeltme OCR**. Varsayılan olarak kapalıdır; açıp önerileri üçe sınırladığınızda düzenli, okunabilir bir çıktı elde edersiniz.

```java
// Step 4: Enable spell correction and limit suggestions to the top 3
engine.getSpellCorrector().setEnabled(true);
engine.getSpellCorrector().setMaxSuggestions(3);
```

`max suggestions` parametresi, motorun her hatalı kelime için kaç alternatif kelime önereceğini kontrol eder. Düşük tutmak, özellikle kaynak görüntü bulanıksa, gürültüyü azaltır.

## Adım 5 – OCR’ı Çalıştır ve Düzeltmiş Metni Al

Her şey bağlandıktan sonra, gerçek tanıma tek bir metod çağrısıdır. Motor, zaten düzeltilmiş metni içeren bir `String` döndürür.

```java
// Step 5: Perform OCR and obtain the corrected text
String correctedText = engine.recognize();
```

Arka planda Aspose, bir sinir ağı tabanlı sınıflandırıcı çalıştırır, ardından ham sonuçları hece düzelticiden geçirir. Tipik 300 × 200 px bir görüntü için bütün işlem birkaç milisaniye içinde tamamlanır.

## Adım 6 – Düzeltmiş Sonucu Çıktı Al

Son olarak, dizeyi yazdırın—ya da bir veritabanına, bir REST yanıtına vb. gönderin.

```java
// Step 6: Output the corrected result
System.out.println(correctedText);
```

### Beklenen Çıktı

`misspelled.png` içinde “Ths is a smple test” ifadesi varsa, konsol şu şekilde gösterir:

```
This is a simple test
```

Hatalı “Ths” ve “smple” kelimelerinin otomatik olarak düzeltildiğine ve sadece en iyi üç önerinin dikkate alındığına dikkat edin.

## Yaygın Tuzaklar ve İpuçları

| Sorun | Neden Oluşur | Nasıl Çözülür |
|------|----------------|------------|
| **Boş çıktı** | Lisans yüklenmemiş veya görüntü yolu hatalı. | `.lic` dosya yolunu ve `misspelled.png` dosyasının varlığını doğrulayın. |
| **Bozuk karakterler** | Görüntü DPI’sı çok düşük (70’in altında). | Daha yüksek çözünürlüklü bir kaynak kullanın veya `ImageMagick` ile yükseltin. |
| **Çok fazla öneri** | `setMaxSuggestions` varsayılan (0 = sınırsız) bırakılmış. | Örnekte gösterildiği gibi `setMaxSuggestions(3)` çağrısını açıkça yapın. |
| **Yanlış dil** | `setLanguage` çağrılmamış veya yanlış enum kullanılmış. | `OcrLanguage` enum değerinin metninize uygun olduğundan emin olun. |

### Pro ipucu: Toplu işleme

Yüzlerce dosyayı OCR’a tabi tutmanız gerekiyorsa, adım 1‑5’i bir döngü içinde sarın ve aynı `OcrEngine` örneğini yeniden kullanın. Motoru yeniden kullanmak, iç sinir ağının yalnızca bir kez yüklenmesi sayesinde belleği tasarruf ettirir.

```java
OcrEngine engine = new OcrEngine();
engine.setLanguage(OcrLanguage.ENGLISH);
engine.getSpellCorrector().setEnabled(true);
engine.getSpellCorrector().setMaxSuggestions(3);

for (String path : imagePaths) {
    engine.setImage(new OcrImage(path));
    System.out.println(engine.recognize());
}
```

## Özet

Aspose OCR Java ile **OCR için görüntü yükleme**, lisanslama, dil seçimi, **hece düzeltme OCR**’u açma ve çıktıyı en iyi üç alternatifle sınırlama konularını baştan sona ele aldık. Tam, çalıştırılabilir program sadece birkaç satır uzunluğunda, ancak büyük bir güç barındırıyor.

Sırada ne var? `OcrLanguage.ENGLISH` yerine başka bir dil deneyin, farklı görüntü formatları (`.tif`, `.bmp`) ile oynayın ya da sonucu bir PDF oluşturucuya bağlayın. Olasılıklar sınırsız ve aynı desen—lisans → motor → görüntü → ayarlar → tanıma—her senaryo için geçerli.

Kodlamanın tadını çıkarın, OCR sonuçlarınız her zaman kristal berraklığında olsun!

## Sonraki Öğrenmeniz Gerekenler

- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}