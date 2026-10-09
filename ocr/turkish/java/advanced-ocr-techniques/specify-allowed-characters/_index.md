---
date: 2026-02-20
description: Aspose.OCR for Java kullanarak görüntülerden metin nasıl çıkarılır, izin
  verilen karakterler nasıl ayarlanır ve geçici lisans nasıl uygulanır – eksiksiz
  bir Aspose OCR Java öğreticisi.
linktitle: Specifying Allowed Characters in Aspose.OCR
second_title: Aspose.OCR Java API
title: Aspose.OCR Kullanarak Görsellerden Metin Çıkarma – İzin Verilen Karakterler
url: /tr/java/advanced-ocr-techniques/specify-allowed-characters/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntülerden Metin Çıkarma – Aspose.OCR – İzin Verilen Karakterler

## Giriş

Görüntülerden metin çıkarma, modern uygulamalarda yaygın bir gereksinimdir—faturaları işliyor, makbuzları tarıyor veya basılı belgeleri dijitalleştiriyor olun. Bu öğreticide, Aspose.OCR for Java ile **görüntülerden metin çıkarma**, izin verilen karakterleri ayarlama ve sadece kütüphaneyi test ederken geçici bir lisans uygulama adımlarını gösteren eksiksiz bir **aspose ocr java tutorial** üzerinden geçeceğiz.

## Hızlı Yanıtlar
- **Aspose.OCR ne yapar?** Görüntülerden yüksek doğrulukla metin çıkarır ve özel karakter setlerini destekler.  
- **Lisans gerekiyor mu?** Üretim kullanımı için geçici veya kalıcı bir lisans gereklidir.  
- **Hangi JDK sürümü destekleniyor?** En yeni JDK sürümleri tam uyumludur.  
- **Tanıyan karakterleri sınırlayabilir miyim?** Evet—çıktıyı kısıtlamak için `setAllowedCharacters` API'sini kullanın.  
- **Kurulum ne kadar sürer?** Temel bir uygulama için yaklaşık 10‑15 dakikadır.

## “Görüntülerden metin çıkarma” nedir?
Görüntülerden metin çıkarma, görsel metni (ör. basılı veya el yazması) makine‑okunur dizeye dönüştürme sürecidir. Bu, arama, indeksleme veya veri analizi gibi sonraki görevleri mümkün kılar.

## Neden Aspose.OCR for Java Kullanmalı?
- **Birden çok dil ve yazı tipi** için yüksek doğruluk.  
- **Basit API**, herhangi bir Java projesine kolayca entegre olur.  
- **Özelleştirilebilir** karakter setleri, dil paketleri ve görüntü ön işleme.  
- **Harici bağımlılık yok**—kütüphane kendi içinde çalışır.

## Ön Koşullar

Başlamadan önce aşağıdakilerin kurulu olduğundan emin olun:

### Java Development Kit (JDK)

Sisteminize en son Java Development Kit'in yüklü olduğundan emin olun. İndirmek için [buraya](https://www.oracle.com/java/technologies/javase-downloads.html) tıklayın.

### Aspose.OCR for Java Library

Aspose.OCR for Java kütüphanesini [indirme bağlantısından](https://releases.aspose.com/ocr/java/) indirin ve kurun.

### Aspose.OCR Lisansı

Aspose.OCR'ün tam potansiyelini kullanmak için geçerli bir lisans edinin. Lisansı [buradan](https://purchase.aspose.com/buy) alabilir veya deneme süresi için bir [geçici lisans](https://purchase.aspose.com/temporary-license/) inceleyebilirsiniz.

## Geçici lisans nasıl uygulanır

Ürünü değerlendirirken, geçici lisans değerlendirme filigranını kaldırır ve sınırlı bir süre için tam işlevselliği açar. Lisans dizesini Aspose portalında oluşturup, aşağıdaki kod örneğinde gösterildiği gibi `AsposeOCR` yapıcısına aktarın. Üretim dağıtımlarında geçici anahtarı kalıcı lisansınızla değiştirin.

## OCR görüntü ön işleme ipuçları

İyi görüntü kalitesi tanıma sonuçlarını büyük ölçüde iyileştirir. OCR motorunu çağırmadan önce şunları göz önünde bulundurun:

- Görüntüyü gri tonlamaya dönüştürün.  
- Karakterlerin öne çıkması için kontrastı artırın.  
- Arka plan gürültüsünü bir ikilileştirme filtresiyle kaldırın.  
- Düşük çözünürlüklü görüntüleri en az 300 dpi’ye yeniden boyutlandırın.

Bu adımlar **ocr image preprocessing** kapsamında olup, Aspose.OCR'ü çağırmadan önce herhangi bir standart Java görüntüleme kütüphanesiyle gerçekleştirilebilir.

## Paketleri İçe Aktarma

Ön koşullar hazır olduğunda, Java projenize gerekli paketleri şu şekilde içe aktarın:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import java.io.IOException;
```

## Adım‑Adım Kılavuz

### Adım 1: Belge Dizinini Ayarlayın

OCR‑işlenmiş sonuçları saklayacağınız bir klasör tanımlayın. Bu yol, daha sonra görüntü dosyasını bulmak için kullanılacaktır.

```java
String dataDir = "Your Document Directory";
```

### Adım 2: Görüntü Yolunu Belirtin

API'yi analiz etmek istediğiniz görüntüye yönlendirin.

```java
String imagePath = dataDir + "0001460985.Jpeg";
```

### Adım 3: Bir Aspose.OCR Örneği Oluşturun

Lisans anahtarınızla OCR motorunu başlatın. Anahtar geçici ya da kalıcı bir lisans dizesi olabilir.

```java
AsposeOCR api = new AsposeOCR("YourLicenseKey");
```

### Adım 4: OCR Tanıma İşlemini Gerçekleştirin

`RecognizeLine` metodunu çağırarak görüntüden bir satır metin çıkarın. Sonuç, daha fazla işleyebileceğiniz veya depolayabileceğiniz düz bir dizedir.

```java
try {
    String result = api.RecognizeLine(imagePath);
    System.out.println("File: " + imagePath);
    System.out.println("Result line: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **Pro ipucu:** Çıktıyı belirli bir karakter setiyle (ör. sadece rakamlar) sınırlamanız gerekiyorsa, `RecognizeLine` metodunu çağırmadan önce `AsposeOCR` örneği üzerinde `setAllowedCharacters` metodunu kullanın. Bu, motorun tanımlı set dışındaki karakterleri yok saymasını sağlar.

## Yaygın Sorunlar ve Çözümler

| Sorun | Sebep | Çözüm |
|-------|--------|-----|
| **Çıktı yok veya boş dize** | Yanlış görüntü yolu veya desteklenmeyen görüntü formatı | `imagePath` değerini doğrulayın ve desteklenen bir format (JPEG, PNG, BMP) kullanın |
| **Tanıma hataları** | Düşük çözünürlüklü görüntü veya gürültülü arka plan | OCR'den önce görüntüyü ön işleyin (kontrast artırın, ikilileştirin) |
| **Lisans uygulanmadı** | Eksik veya geçersiz lisans anahtarı | Lisans dizesinin doğru olduğundan ve `AsposeOCR` yapıcısına yerleştirildiğinden emin olun |

## Sık Sorulan Sorular

**S: Aspose.OCR için geçici lisans nasıl alınır?**  
C: Deneme lisansı talep etmek için [geçici lisans sayfasını](https://purchase.aspose.com/temporary-license/) ziyaret edin.

**S: Aspose.OCR için destek nereden bulunur?**  
C: Yardım ve tartışmalar için [Aspose.OCR Forumuna](https://forum.aspose.com/c/ocr/16) katılın.

**S: Aspose.OCR'de izin verilen karakterler belirtilebilir mi?**  
C: Evet, `setAllowedCharacters` API'siyle karakter setini özelleştirebilirsiniz. Ayrıntılar için resmi belgelere bakın.

**S: Aspose.OCR en yeni JDK sürümleriyle uyumlu mu?**  
C: Kesinlikle—Aspose.OCR, en yeni Java sürümleriyle uyumlu kalacak şekilde düzenli olarak güncellenir.

**S: Satır tanımanın ötesinde ek OCR özellikleri var mı?**  
C: Evet, kütüphane blok, paragraf ve tam‑sayfa tanıma, dil paketleri ve görüntü ön işleme seçeneklerini destekler.

## Sonuç

Bu **aspose ocr java tutorial**'ı izleyerek artık **görüntülerden metin çıkarma** ve hangi karakterlerin tanınacağını kontrol etme konusunda çalışan bir çözüme sahipsiniz. Gelişmiş çok‑dilli destek, özel ön işleme ve toplu işleme gibi özellikleri keşfetmek için tam [belgelere](https://reference.aspose.com/ocr/java/) göz atın.

---

**Son Güncelleme:** 2026-02-20  
**Test Edilen Versiyon:** Aspose.OCR for Java 24.11  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}