---
date: 2025-12-13
description: Aspose.OCR for Java kullanarak dil seçimiyle görüntüden metin çıkarma
  yöntemini öğrenin. Bu adım adım Aspose OCR Java öğreticisi, hassas OCR yapılandırmasını
  gösterir.
linktitle: How to Extract Text from Image with Language Selection Using Aspose.OCR
second_title: Aspose.OCR Java API
title: Aspose.OCR Kullanarak Dil Seçimiyle Görüntüden Metin Çıkarma
url: /tr/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.OCR Kullanarak Dil Seçimiyle Görüntüden Metin Çıkarma

## Giriş

Görüntü dosyalarından metin çıkarmak, taranmış belgeleri dijitalleştirirken, fişleri işlerken ya da aranabilir arşivler oluştururken yaygın bir gereksinimdir. Aspose.OCR for Java bu görevi basitleştirir ve dil seçimi, eğikliği düzeltme ve tanıma alanları üzerinde ince ayar yapma imkanı sunar. Bu öğreticide, **görüntüden metin çıkarma** işlemini belirli bir dil ayarıyla nasıl yapacağınızı adım adım gösterecek bir örnek üzerinden geçeceğiz; böylece güvenilir OCR'ı Java uygulamalarınıza hemen entegre edebilirsiniz.

## Hızlı Yanıtlar
- **Java’da OCR işlemini hangi kütüphane yönetir?** Aspose.OCR for Java  
- **Dil seçimini hangi ayar yapar?** `settings.setLanguage(Language.Eng)` (veya desteklenen herhangi bir dil)  
- **Geliştirme için lisansa ihtiyacım var mı?** Test için ücretsiz deneme lisansı çalışır; üretim için ticari lisans gereklidir.  
- **OCR’ı görüntünün sadece bir bölgesiyle sınırlayabilir miyim?** Evet, dikdörtgenlerle `RecognitionSettings.setRecognitionAreas()` kullanın.  
- **Tipik çalışma süresi nedir?** Görüntü boyutu ve dil karmaşıklığına bağlı olarak standart bir dizüstü bilgisayarda sayfa başına birkaç saniye.

## “Görüntüden metin çıkarma” nedir?
Görüntüden metin (OCR) çıkarmak, karakterlerin görsel temsillerini makine‑okunur dizelere dönüştürür. Bu, manuel transkripsiyon gerektirecek arama, analiz ve veri çıkarma iş akışlarını mümkün kılar.

## Aspose.OCR’ı dil seçimiyle neden kullanmalısınız?
- **Çok dilli destek** – Görüntünüzde bulunan tam dil(ler)i seçerek doğruluğu artırın.  
- **İnce ayar kontrolü** – Eğikliği ayarlayın, tanıma alanlarını tanımlayın ve otomatik eğiklik davranışını belirleyin.  
- **Saf Java API** – Yerel bağımlılık yok, herhangi bir Java projesine kolayca entegre edilir.  
- **Zengin sonuç verisi** – Tek bir çağrıda düz metin, JSON, sınırlayıcı dikdörtgenler ve uyarılar alın.

## Ön Koşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

- **Java Development Kit (JDK)** (JDK 8 veya üzeri) yüklü.  
- **Aspose.OCR for Java** kütüphanesi – resmi siteden [buradan](https://reference.aspose.com/ocr/java/) indirebilirsiniz.  
- Metin çıkarmak istediğiniz bir görüntü dosyası, örneğin `p3.png`.

## Paketleri İçe Aktarma

Java kaynak dosyanıza gerekli Aspose.OCR sınıflarını ve standart Java yardımcılarını ekleyin:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Adım‑Adım Kılavuz

### Adım 1: Belge Dizinini Ayarlama

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

`"Your Document Directory"` ifadesini `p3.png` dosyasının bulunduğu mutlak yol ile değiştirin.

### Adım 2: Görüntü Yolunu Tanımlama

```java
// The image path
String file = dataDir + "p3.png";
```

`file` değişkeninin işlemek istediğiniz tam görüntüyü işaret ettiğinden emin olun.

### Adım 3: Aspose.OCR API Örneği Oluşturma

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

`AsposeOCR` nesnesi tüm OCR işlemlerine erişim sağlar.

### Adım 4: Tanıma Seçeneklerini Ayarlama (Dil Seçimi)

```java
// Set recognition options
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

Burada:

1. Manuel bir eğiklik değeri sağladığımız için otomatik‑eğikliği devre dışı bırakıyoruz.  
2. OCR’ı yalnızca metin içeren bölgeye sınırlamak için dikdörtgen bir bölge (`RecognitionAreas`) tanımlıyoruz.  
3. **Dili** İngilizce (`Language.Eng`) olarak ayarlıyoruz. Kaynak görüntünüze göre bunu `Language.Fra`, `Language.Spa` vb. olarak değiştirin.

### Adım 5: OCR’ı Çalıştırma ve Sonuçları Alma

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

`RecognizePage` çağrısı, tanımladığınız ayarlarla görüntü üzerinde OCR motorunu çalıştırır. Sonuç bir `RecognitionResult` nesnesinde saklanır.

### Adım 6: Sonuçları Yazdırma ve Kullanma

```java
// Print result
System.out.println("Result: \n" + result.recognitionText + "\n\n");
for (String n : result.recognitionAreasText) {
    System.out.println(n);
}
for (Rectangle n : result.recognitionAreasRectangles) {
    System.out.println(n.height + ":" + n.width + ":" + n.x + ":" + n.y);
}
System.out.println("\nJSON:" + result.GetJson());
System.out.println("Angle:" + result.skew);
for (String n : result.warnings) {
    System.out.println(n);
}

System.out.println("OCROperationWithLanguageSelection: execution complete");
```

Konsol çıktısı şunları gösterir:

- Tam çıkarılan metin (`recognitionText`).  
- Her tanımlı dikdörtgen için metin (`recognitionAreasText`).  
- Sınırlayıcı dikdörtgen koordinatları.  
- Kolay downstream işleme için JSON temsili.  
- Algılanan eğiklik açısı ve olası uyarılar.

Artık `result.recognitionText` değerini iş mantığınıza besleyebilirsiniz—saklayın, indeksleyin veya başka bir servise gönderin.

## Yaygın Sorunlar ve Çözümleri

| Sorun | Neden | Çözüm |
|-------|-------|------|
| **Bozuk karakterler** | Yanlış dil seçildi | Doğru `Language` enum’ını ayarlayın (ör. Fransızca için `Language.Fra`). |
| **Metin dönmedi** | Tanıma alanı metni kapsamaz | `Rectangle` koordinatlarını ayarlayın veya tüm görüntüyü işlemek için `RecognitionAreas`’ı kaldırın. |
| **Yavaş performans** | Çok büyük veya yüksek çözünürlüklü görüntü | OCR’dan önce görüntüyü küçültün veya JVM için hafıza tahsisinizi artırın. |
| **Desteklenmeyen format uyarısı** | Görüntü formatı tanınmadı | Görüntüyü PNG, JPEG veya TIFF gibi desteklenen bir formata dönüştürün. |

## Sık Sorulan Sorular

**S: Tek bir OCR çağrısında birden fazla dili tanıyabilir miyim?**  
C: Evet. Çok dilli tanıma için `settings.setLanguage(Language.Eng | Language.Fra)` kullanın.

**S: Aspose.OCR hangi görüntü formatlarını destekler?**  
C: PNG, JPEG, BMP, TIFF, GIF ve birkaç başka format. Doğru dosya yolunu sağlayın.

**S: Görüntü boyutu için bir sınırlama var mı?**  
C: Katı bir sınır yok, ancak çok büyük görüntüler bellek kullanımını ve işleme süresini artırır. Büyük dosyaları yeniden boyutlandırmayı düşünün.

**S: Üretim lisansını nasıl alabilirim?**  
C: Aspose web sitesinden lisans satın alın ve Aspose dokümantasyonunda gösterildiği gibi `License` sınıfı ile uygulayın.

**S: PDF sayfasından doğrudan metin çıkarabilir miyim?**  
C: Aspose.OCR ile doğrudan mümkün değildir. Önce PDF sayfasını bir görüntüye (ör. Aspose.PDF kullanarak) dönüştürün, ardından OCR çalıştırın.

## Sonuç

Artık **görüntüden metin çıkarma** işlemini Aspose.OCR for Java ile, uygun dili seçerek ve tanıma alanlarını sınırlayarak nasıl yapacağınızı gördünüz. Bu yaklaşım, herhangi bir Java‑tabanlı iş akışına—belge yönetim sistemlerinden veri yakalama hatlarına—yerleştirilebilecek doğru, yüksek‑performanslı OCR sağlar.

---

**Son Güncelleme:** 2025-12-13  
**Test Edilen Versiyon:** Aspose.OCR 24.11 for Java  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}