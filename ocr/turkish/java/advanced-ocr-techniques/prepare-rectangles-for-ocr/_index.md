---
date: 2026-02-20
description: Aspose.OCR for Java kullanarak sayfa dikdörtgenlerini nasıl tanıyacağınızı
  öğrenin, metin görüntüsü Java projelerini çıkarın ve kesin OCR için bu Aspose OCR
  Java eğitimini izleyin.
linktitle: How to Recognize Page Rectangles for OCR Text Recognition in Aspose.OCR
second_title: Aspose.OCR Java API
title: Aspose.OCR'de OCR Metin Tanıma İçin Sayfa Dikdörtgenlerini Nasıl Tanıyabilirsiniz
url: /tr/java/advanced-ocr-techniques/prepare-rectangles-for-ocr/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.OCR'da OCR Metin Tanıma İçin Sayfa Dikdörtgenlerini Nasıl Tanımlarsınız

Modern belge‑otomasyon hatlarında, **sayfa dikdörtgenlerini tanıma** OCR motoruna tam olarak nerede bakması gerektiğini söyleyen temel tekniktir. Aspose.OCR'ı yalnızca metin içeren bölgelere sınırlayarak hız artırır, gürültüyü azaltır ve daha temiz sonuçlar elde edersiniz. Bu öğreticide, kütüphaneyi kurma, lisanslama, dikdörtgenleri tanımlama ve sonunda OCR API'sini çağırma adımlarını adım adım göstereceğiz; böylece herhangi bir görüntüden metin çıkarmayı güvenle yapabilirsiniz.

## Hızlı Yanıtlar
- **Java'da OCR metin tanımasını hangi kütüphane yönetir?** Aspose.OCR for Java.  
- **Üretim kullanımında lisansa ihtiyacım var mı?** Evet – geçerli bir Aspose.OCR lisansı tam işlevselliği açar.  
- **OCR'ı bir görüntünün belirli bölümleriyle sınırlayabilir miyim?** Kesinlikle; hedef bölgeleri sınırlayan dikdörtgenler tanımlarsınız.  
- **Ana önkoşullar nelerdir?** JDK 17+, Aspose.OCR for Java ve bir Java IDE.  
- **Bu yaklaşım görüntülerden metin çıkarmak için uygun mu?** Evet, **extract text image java** projeleri için verimli bir yoldur.

## “Sayfa dikdörtgenlerini tanıma” nedir?
Bu ifade, OCR motoruna yalnızca sayfadaki belirli bölgeleri işleyebilmesi için bir `java.awt.Rectangle` nesneleri listesi sağlamayı ifade eder. Bu odaklanmış yaklaşım, özellikle faturalar veya formlar gibi karmaşık belgelerde işlem süresini azaltır ve doğruluğu artırır.

## Neden OCR Metin Tanıma İçin Dikdörtgenler Hazırlamalıyız?
Dikdörtgenleri tanımlamak, motoru gerçekten metin içeren bölgelere odaklar; bu:
* İşlem süresini azaltır.  
* Gürültülü arka planları görmezden gelerek doğruluğu artırır.  
* Sadece ihtiyacınız olan veriyi çıkarmanıza olanak tanır – formlar, faturalar ve makbuzlar için mükemmeldir.  

## Önkoşullar

Başlamadan önce şunların olduğundan emin olun:

- **Java Development Kit (JDK)** – Aspose.OCR for Java, JDK 17 veya daha yeni sürümlerle çalışır. Oracle web sitesinden indirin.  
- **Aspose.OCR for Java kütüphanesi** – En son JAR dosyasını resmi indirme sayfasından [burada](https://releases.aspose.com/ocr/java/) alın. Kurulum rehberini [burada](https://reference.aspose.com/ocr/java/) izleyin.  
- **Geliştirme Ortamı** – Herhangi bir Java IDE (IntelliJ IDEA, Eclipse, VS Code vb.) yeterlidir.

## Paketleri İçe Aktarma

Java kaynak dosyanızda, gerekli Aspose.OCR sınıflarını ve standart Java yardımcılarını içe aktarın:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

> *`java.awt.Rectangle`'ı içe aktarıyoruz çünkü OCR API'si taranacak bölgeleri tanımlayan dikdörtgenleri bekler.*

## Adım 1: Lisansı Ayarlama

```java
SetLicense.main(null);
```

`SetLicense` çağrısı, Aspose.OCR lisansınızı etkinleştirir, değerlendirme sınırlamalarını kaldırır ve tam özellikli OCR metin tanımayı sağlar.

## Adım 2: Belge Dizini ve Görüntü Yolunu Tanımlama

```java
String dataDir = "Your Document Directory";
String imagePath = dataDir + "p.png";
```

`"Your Document Directory"` ifadesini, görüntünüzün (`p.png`) bulunduğu mutlak yol ile değiştirin. İşlenecek görüntü budur.

## Adım 3: Aspose.OCR Örneği Oluşturma

```java
AsposeOCR api = new AsposeOCR();
```

`AsposeOCR` nesnesi oluşturmak, gerçek OCR işlemini yapan `RecognizePage` metoduna erişmenizi sağlar.

## Adım 4: Metin İçeren Dikdörtgenleri Hazırlama

```java
ArrayList<Rectangle> rectArray = new ArrayList<Rectangle>();
rectArray.add(new Rectangle(138, 352, 2033, 537));
rectArray.add(new Rectangle(147, 890, 2033, 1157));
rectArray.add(new Rectangle(923, 2045, 465, 102));
rectArray.add(new Rectangle(104, 2147, 2076, 819));
```

Her `Rectangle(x, y, width, height)` Aspose.OCR'a metnin nerede aranacağını tam olarak söyler. Koordinatları, kaynak görüntünüzün düzenine göre ayarlayın.

## Adım 5: OCR Tanımasını Gerçekleştirme

```java
try {
    String result = api.RecognizePage(imagePath, rectArray);
    System.out.println("Result with rect: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

`RecognizePage` çağrısı yalnızca tanımlanan dikdörtgenleri işler ve çıkarılan dizeyi döndürür. Konsol çıktısı, **ocr text recognition** sonucunu anında doğrulamanızı sağlar.

## Yaygın Sorunlar ve İpuçları

| Sorun | Neden | Çözüm |
|-------|-------|----------|
| **Çıktı yok** | Yanlış dikdörtgen koordinatları veya görüntü yolu | `dataDir` değerini iki kez kontrol edin ve dikdörtgenlerin gerçekten metin bölgelerini kapsadığından emin olun. |
| **Bozuk karakterler** | Düşük çözünürlüklü görüntü veya desteklenmeyen yazı tipi | Daha yüksek çözünürlüklü bir kaynak kullanın veya görüntü ön işleme (ör. ikilileştirme) uygulayın. |
| **Lisans uygulanmadı** | OCR'dan önce `SetLicense` çağrılmadı | `SetLicense.main(null);` kodunun herhangi bir API çağrısından önce çalıştığından emin olun. |
| **Performans yavaşlığı** | Çok fazla büyük dikdörtgen | Dikdörtgen sayısını sınırlayın ve metnin etrafını mümkün olduğunca sıkı tutun. |

## Sık Sorulan Sorular

**S:** *Aspose.OCR diğer programlama dilleriyle uyumlu mu?*  
**C:** Evet, Aspose.OCR .NET, C++ ve Python'ı da destekler. Dil‑spesifik örnekler için resmi belgeleri inceleyin.

**S:** *Aspose.OCR'ı ticari bir projede kullanabilir miyim?*  
**C:** Kesinlikle. Ticari bir lisansı [Aspose mağazası](https://purchase.aspose.com/buy) üzerinden satın alabilirsiniz.

**S:** *Ücretsiz deneme sürümü mevcut mu?*  
**C:** Evet, deneme sürümünü [buradan](https://releases.aspose.com/) indirebilirsiniz.

**S:** *Değerlendirme için geçici bir lisans nasıl alınır?*  
**C:** Geçici lisanslar, [Aspose geçici‑lisans portalı](https://purchase.aspose.com/temporary-license/) üzerinden sağlanır.

**S:** *Topluluk desteği nereden alınır?*  
**C:** Sorular, ipuçları ve kod örnekleri için Aspose.OCR [forumunu](https://forum.aspose.com/c/ocr/16) ziyaret edin.

## Sonuç

Artık Aspose.OCR for Java ile **sayfa dikdörtgenlerini tanıma**, lisans ayarlama, görüntü yollarını tanımlama ve en önemlisi OCR'ı ihtiyaç duyduğunuz görüntü bölümlerine odaklamak için sıkı dikdörtgenler hazırlama konularını öğrendiniz. Bu teknik, kesin ve yüksek performanslı metin çıkarımı gerektiren herhangi bir **aspose ocr java tutorial** için idealdir.

---

**Son Güncelleme:** 2026-02-20  
**Test Edilen:** Aspose.OCR for Java 24.12  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}