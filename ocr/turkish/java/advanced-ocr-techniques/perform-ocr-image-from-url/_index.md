---
title: Aspose.OCR for Java'da URL'den Resim üzerinde OCR gerçekleştirme
linktitle: Aspose.OCR for Java'da URL'den Resim üzerinde OCR gerçekleştirme
second_title: Aspose.OCR Java API'si
description: Aspose.OCR ile Java'da kesintisiz görüntü metni çıkarmanın kilidini açın. Kolay entegrasyonla yüksek doğrulukta OCR.
weight: 11
url: /tr/java/advanced-ocr-techniques/perform-ocr-image-from-url/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.OCR for Java'da URL'den Resim üzerinde OCR gerçekleştirme

## giriiş

Aspose.OCR for Java kullanarak bir URL'deki görüntü üzerinde Optik Karakter Tanıma (OCR) gerçekleştirmeye ilişkin adım adım kılavuzumuza hoş geldiniz. Bu eğitim, Aspose.OCR'ı Java uygulamalarınıza sorunsuz bir şekilde entegre etmenize yardımcı olmak ve görüntülerden kolaylıkla metin çıkarmanıza olanak sağlamak için tasarlanmıştır. Aspose.OCR, çeşitli görüntü formatlarını destekleyen güçlü bir OCR kitaplığıdır ve bu da onu metin çıkarma gerektiren uygulamalar için değerli bir araç haline getirir.

## Önkoşullar

Eğiticiye dalmadan önce aşağıdaki önkoşullara sahip olduğunuzdan emin olun:

1. Java Geliştirme Ortamı: Makinenizde çalışan bir Java geliştirme ortamının kurulu olduğundan emin olun.

2.  Aspose.OCR Kütüphanesi: Aspose.OCR for Java kütüphanesini indirip yükleyin. Kütüphaneyi ve ilgili belgeleri şu adreste bulabilirsiniz:[Aspose.OCR web sitesi](https://reference.aspose.com/ocr/java/).

## Paketleri İçe Aktar

Aspose.OCR için gerekli paketleri Java projenize aktarın:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## 1. Adım: API Örneği Oluşturun

AsposeOCR sınıfının bir örneğini başlatın:

```java
AsposeOCR api = new AsposeOCR();
```

## 2. Adım: Resim URL'sini tanımlayın

OCR gerçekleştirmek istediğiniz görüntünün URL'sini belirtin:

```java
String uri = "https://www.example.com/resiminiz.png";
```

## 3. Adım: Tanıma Seçeneklerini Ayarlayın

Otomatik eğrilmeyi devre dışı bırakma ve tanıma alanlarını tanımlama gibi tanıma ayarlarını yapılandırın:

```java
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);

// Dikdörtgenleri kullanarak tanıma alanlarını tanımlayın
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
```

## 4. Adım: OCR gerçekleştirin

OCR tanıma sürecini çağırın:

```java
RecognitionResult result = null;
try {
    result = api.RecognizePageFromUri(uri, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

## Adım 5: Sonuçları Yazdır

Çıkarılan metin, tanıma alanı metni, JSON çıktısı ve tüm uyarılar dahil olmak üzere tanıma sonuçlarını görüntüleyin:

```java
System.out.println("Result: \n" + result.recognitionText + "\n\n");
System.out.println("RecognitionAreasText: \n");
for (String text : result.recognitionAreasText) {
    System.out.println(text);
}
System.out.println("JSON: \n" + result.GetJson());
System.out.println("Warnings: \n");
for (String warning : result.warnings) {
    System.out.println(warning);
}
```

Aspose.OCR'ı Java uygulamanıza entegre etmek ve görsellerden metni hassas bir şekilde çıkarmak için bu adımları tekrarlayın.

## Çözüm

Sonuç olarak Aspose.OCR for Java'dan yararlanmak, OCR görevleri için sağlam bir çözüm sunarak geliştiricilerin görüntülerden sorunsuz bir şekilde metin çıkarmasına olanak tanıyor. Adım adım kılavuz, sorunsuz bir entegrasyon süreci sağlayarak her düzeydeki geliştiricinin erişebilmesini sağlar.

## SSS'ler

### S1: Aspose.OCR'ın resimlerdeki metinleri tanıması ne kadar doğrudur?

Cevap1: Aspose.OCR, özellikle hassas tanıma alanlarıyla yapılandırıldığında metin tanımada yüksek doğruluk sunar.

### S2: Aspose.OCR, OCR tanıma sırasında birden fazla dili işleyebilir mi?

C2: Evet, Aspose.OCR birden çok dildeki metnin tanınmasını destekleyerek çeşitli uygulamalar için çok yönlülük sağlar.

### S3: Aspose.OCR'ı ticari projelerde kullanmak için herhangi bir lisanslama hususu var mı?

C3: Evet, ticari kullanım için Aspose.OCR lisanslama şartlarına uygunluğu sağlayın. Bakınız[satın alma.aspose.com](https://purchase.aspose.com/buy) lisans ayrıntıları için.

### S4: Aspose.OCR ile ilgili sorunlar için nasıl destek alabilirim?

 A4: Ziyaret edin[Aspose.OCR forumu](https://forum.aspose.com/c/ocr/16) topluluk desteği ve tartışmalar için. Premium destek için adresinden geçici bir lisans almayı düşünün.[Geçici Lisans](https://purchase.aspose.com/temporary-license/).

### S5: Aspose.OCR for Java'nın ücretsiz deneme sürümü mevcut mu?

 Cevap5: Evet, Aspose.OCR'ın özelliklerini şu adresteki ücretsiz deneme sürümüyle keşfedin:[bültenleri.aspose.com](https://releases.aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
