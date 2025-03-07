---
title: Aspose.OCR'da Metin Alanlarıyla Dikdörtgenler Alma
linktitle: Aspose.OCR'da Metin Alanlarıyla Dikdörtgenler Alma
second_title: Aspose.OCR Java API'si
description: Aspose.OCR for Java'nın gücünün kilidini açın. Bu adım adım kılavuzda resimlerden metni sorunsuz bir şekilde nasıl çıkaracağınızı öğrenin. Etkili metin tanıma için hemen indirin.
weight: 12
url: /tr/java/ocr-basics/get-rectangles-with-text-areas/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.OCR'da Metin Alanlarıyla Dikdörtgenler Alma

## giriiş

Güçlü optik karakter tanıma (OCR) yeteneklerini Java uygulamanıza entegre etmek mi istiyorsunuz? Aspose.OCR for Java, görüntülerden doğru ve etkili metin çıkarımı için başvuracağınız çözümdür. Bu eğitim, Aspose.OCR kullanarak metin alanlarına sahip dikdörtgenler elde etme sürecinde size rehberlik edecek ve bu Java OCR kütüphanesinin tüm potansiyelinden yararlanmanıza yardımcı olacaktır.

## Önkoşullar

Eğiticiye dalmadan önce aşağıdaki önkoşulların mevcut olduğundan emin olun:

- Java Geliştirme Ortamı: Sisteminizde Java'nın kurulu olduğundan emin olun.
-  Aspose.OCR for Java Library: Aspose.OCR kütüphanesini indirin ve kurun. İndirme linkini bulabilirsiniz[Burada](https://releases.aspose.com/ocr/java/).

## Paketleri İçe Aktar

Aspose.OCR'ın işlevlerinden yararlanmak için Java projenize gerekli paketleri içe aktarın:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AreasType;
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## 1. Adım: Projenizi Kurun

Hazır bir Java projeniz olduğundan ve Aspose.OCR kütüphanesinin entegre olduğundan emin olun.

## 2. Adım: Belge Dizinini ve Görüntü Yolunu Tanımlayın

```java
// Belgeler dizininin yolu.
String dataDir = "Your Document Directory";

// Görüntü yolu
String imagePath = dataDir + "p3.png";
```

## Adım 3: Aspose.OCR Örneği Oluşturun

```java
// Aspose.OCR örneği oluştur
AsposeOCR api = new AsposeOCR();
```

## 4. Adım: Görüntüdeki Metni Tanıyın

```java
try {
    // Sayfayı dosyanın tam yoluna göre tanı
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

## Adım 5: Metin Alanlarıyla Dikdörtgenler Alın

```java
// Görüntüde metin alanlarına sahip dikdörtgenler elde edin.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Her metin alanı dikdörtgenini yazdır
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

## Çözüm

Bu eğitimde, resimlerden verimli bir şekilde metin çıkarmak için Aspose.OCR for Java'yı projenize nasıl entegre edeceğinizi öğrendiniz. Aspose.OCR, kusursuz bir kullanıcı deneyimi için doğru sonuçlar sağlayarak OCR görevlerini basitleştirir.

## SSS'ler

### S1: Aspose.OCR Java 11 ile uyumlu mu?

Cevap1: Evet, Aspose.OCR, Java 11 ve sonraki sürümlerle uyumludur.

### S2: Aspose.OCR'ı hem kişisel hem de ticari projeler için kullanabilir miyim?

 C2: Evet, Aspose.OCR hem kişisel hem de ticari projeler için kullanılabilir. Lisans ayrıntıları için şu adresi ziyaret edin:[Burada](https://purchase.aspose.com/buy).

### S3: Aspose.OCR için geçici lisansı nasıl edinebilirim?

 Cevap3: Geçici bir lisans alabilirsiniz[Burada](https://purchase.aspose.com/temporary-license/).

### S4: Aspose.OCR desteğini nerede bulabilirim?

 Cevap4: Destek ve tartışmalar için şu adresi ziyaret edin:[Aspose.OCR forumu](https://forum.aspose.com/c/ocr/16).

### S5: Aspose.OCR çoklu iş parçacığını destekliyor mu?

Cevap5: Evet, Aspose.OCR eşzamanlı ortamlarda gelişmiş performans için çoklu iş parçacığını destekler.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
