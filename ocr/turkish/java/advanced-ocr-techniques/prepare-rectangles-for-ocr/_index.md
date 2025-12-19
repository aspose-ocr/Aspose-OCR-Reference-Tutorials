---
date: 2025-12-06
description: Aspose.OCR for Java'ı kullanarak OCR metin tanıma işlemi yapmayı, görüntülerden
  metin çıkarmayı ve hedefli tanıma için dikdörtgenler hazırlamayı öğrenin.
linktitle: Preparing Rectangles for OCR Text Recognition in Aspose.OCR
second_title: Aspose.OCR Java API
title: Aspose.OCR'de OCR Metin Tanıma İçin Dikdörtgenleri Hazırlama
url: /tr/java/advanced-ocr-techniques/prepare-rectangles-for-ocr/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.OCR'de OCR Metin Tanıma için Dikdörtgenleri Hazırlama

## Giriş

Günümüzün veri odaklı dünyasında, **ocr text recognition** taranmış belgeleri, ekran görüntülerini ve fotoğrafları aranabilir, düzenlenebilir içeriğe dönüştürmenin temel taşıdır. Aspose.OCR for Java bu süreci hızlı ve güvenilir hâle getirir, özellikle bir görüntünün belirli alanlarına odaklanmanız gerektiğinde. Bu öğreticide, OCR'ı ilgilendiğiniz bölgelere sınırlayan dikdörtgenleri hazırlamak için gereken tüm adımları adım adım göstereceğiz; bu sayede kesin kontrol ve daha iyi performans elde edeceksiniz.

## Hızlı Yanıtlar
- **Java'da OCR metin tanımasını hangi kütüphane yönetir?** Aspose.OCR for Java.  
- **Üretim kullanımında lisansa ihtiyacım var mı?** Evet – geçerli bir Aspose.OCR lisansı tam işlevselliği açar.  
- **OCR'ı bir görüntünün belirli bölümleriyle sınırlayabilir miyim?** Kesinlikle; hedef bölgeleri sınırlayan dikdörtgenler tanımlarsınız.  
- **Ana önkoşullar nelerdir?** JDK 17+, Aspose.OCR for Java ve bir Java IDE.  
- **Bu yaklaşım görüntülerden metin çıkarmak için uygun mu?** Evet, **extract text image java** projeleri için verimli bir yoldur.

## OCR Metin Tanıması Nedir?

OCR (Optik Karakter Tanıma) metin tanıması, piksel tabanlı görüntüleri makine tarafından okunabilir karakterlere dönüştürür. Bu sayede yalnızca resim olarak var olan içeriği arayabilir, düzenleyebilir ve analiz edebilirsiniz.

## OCR Metin Tanıması için Dikdörtgenleri Neden Hazırlamalısınız?

Dikdörtgenleri tanımlamak, motoru gerçekten metin içeren bölgelere odaklar; bu:
* İşleme süresini azaltır.
* Gürültülü arka planları görmezden gelerek doğruluğu artırır.
* Sadece ihtiyacınız olan verileri çıkarmanıza olanak tanır—formlar, faturalar ve makbuzlar için mükemmeldir.

## Önkoşullar

Başlamadan önce şunların kurulu olduğundan emin olun:

- **Java Development Kit (JDK)** – Aspose.OCR for Java, JDK 17 veya daha yeni sürümlerle çalışır. Oracle web sitesinden indirin.
- **Aspose.OCR for Java kütüphanesi** – Resmi indirme sayfasından en son JAR'ı alın [burada](https://releases.aspose.com/ocr/java/). Kurulum rehberini [burada](https://reference.aspose.com/ocr/java/) izleyin.
- **Geliştirme Ortamı** – Herhangi bir Java IDE (IntelliJ IDEA, Eclipse, VS Code vb.) yeterlidir.

## Paketleri İçe Aktarma

Java kaynak dosyanızda gerekli Aspose.OCR sınıflarını ve standart Java yardımcılarını içe aktarın:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

> *OCR API'sinin taranacak bölgeleri tanımlayan dikdörtgenleri beklediği için `java.awt.Rectangle`'ı içe aktarıyoruz.*

## Adım 1: Lisansı Ayarlama

```java
SetLicense.main(null);
```

`SetLicense` çağrısı, Aspose.OCR lisansınızı etkinleştirir, değerlendirme sınırlamalarını kaldırır ve tam özellikli OCR metin tanımasını sağlar.

## Adım 2: Belge Dizini ve Görüntü Yolunu Tanımlama

```java
String dataDir = "Your Document Directory";
String imagePath = dataDir + "p.png";
```

`"Your Document Directory"` ifadesini, görüntünüzün (`p.png`) bulunduğu mutlak yol ile değiştirin. İşlenecek olan bu görüntüdür.

## Adım 3: AsposeOCR Örneği Oluşturma

```java
AsposeOCR api = new AsposeOCR();
```

`AsposeOCR` örneği oluşturmak, gerçek OCR işlemini yapan `RecognizePage` metoduna erişmenizi sağlar.

## Adım 4: Metinlerle Dikdörtgenleri Hazırlama

```java
ArrayList<Rectangle> rectArray = new ArrayList<Rectangle>();
rectArray.add(new Rectangle(138, 352, 2033, 537));
rectArray.add(new Rectangle(147, 890, 2033, 1157));
rectArray.add(new Rectangle(923, 2045, 465, 102));
rectArray.add(new Rectangle(104, 2147, 2076, 819));
```

Her `Rectangle(x, y, width, height)` Aspose.OCR'a metni nerede arayacağını tam olarak söyler. Koordinatları, kaynak görüntünüzün düzenine göre ayarlayın.

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
| **Çıktı Yok** | Yanlış dikdörtgen koordinatları veya görüntü yolu | `dataDir` değerini iki kez kontrol edin ve dikdörtgenlerin gerçekten metin bölgelerini kapsadığından emin olun. |
| **Bozuk Karakterler** | Düşük çözünürlüklü görüntü veya desteklenmeyen yazı tipi | Daha yüksek çözünürlüklü bir kaynak kullanın veya görüntü ön işleme (ör. ikilileştirme) uygulayın. |
| **Lisans Uygulanmadı** | `SetLicense` OCR'dan önce çağrılmadı | `SetLicense.main(null);` kodunun tüm API çağrılarından önce çalıştığından emin olun. |
| **Performans Gecikmesi** | Çok fazla büyük dikdörtgen | Dikdörtgen sayısını sınırlayın ve metnin etrafında mümkün olduğunca sıkı tutun. |

## Sonuç

Artık Aspose.OCR for Java'ı nasıl entegre edeceğinizi, lisansı nasıl ayarlayacağınızı, görüntü yollarını nasıl tanımlayacağınızı ve en önemlisi **ocr text recognition**'ı bir görüntünün belirli bölümlerine odaklamak için dikdörtgenleri nasıl hazırlayacağınızı öğrendiniz. Bu teknik, kesin ve yüksek performanslı metin çıkarımı gerektiren herhangi bir **java ocr tutorial** için idealdir.

## Sıkça Sorulan Sorular

**S: Aspose.OCR diğer programlama dilleriyle uyumlu mu?**  
C: Evet, Aspose.OCR .NET, C++ ve Python'ı da destekler. Dil‑spesifik örnekler için resmi belgeleri inceleyin.

**S: Aspose.OCR'ı ticari bir projede kullanabilir miyim?**  
C: Kesinlikle. Ticari bir lisansı [Aspose mağazası](https://purchase.aspose.com/buy) üzerinden satın alın.

**S: Ücretsiz bir deneme sürümü mevcut mu?**  
C: Evet, deneme sürümünü [buradan](https://releases.aspose.com/) indirebilirsiniz.

**S: Değerlendirme için geçici bir lisans nasıl alabilirim?**  
C: Geçici lisanslar [Aspose geçici‑lisans portalı](https://purchase.aspose.com/temporary-license/) üzerinden sağlanır.

**S: Topluluk desteğini nereden alabilirim?**  
C: Sorular, ipuçları ve kod örnekleri için Aspose.OCR [forumunu](https://forum.aspose.com/c/ocr/16) ziyaret edin.

---

**Son Güncelleme:** 2025-12-06  
**Test Edilen Versiyon:** Aspose.OCR for Java 24.12  
**Yazar:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
