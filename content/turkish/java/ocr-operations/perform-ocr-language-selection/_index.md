---
title: Aspose.OCR'da Dil Seçimi ile OCR Gerçekleştirme
linktitle: Aspose.OCR'da Dil Seçimi ile OCR Gerçekleştirme
second_title: Aspose.OCR Java API'si
description: Aspose.OCR for Java ile görsellerden hassas metin çıkarmanın kilidini açın. Dil seçimiyle doğru OCR için adım adım kılavuzumuzu izleyin.
type: docs
weight: 11
url: /tr/java/ocr-operations/perform-ocr-language-selection/
---
## giriiş

Sürekli gelişen teknoloji ortamında, Optik Karakter Tanıma (OCR), görüntülerden anlamlı bilgilerin çıkarılmasında önemli bir rol oynamaktadır. Aspose.OCR for Java, geliştiricilerin OCR özelliklerini Java uygulamalarına sorunsuz bir şekilde entegre etmelerini sağlayan güçlü bir araç olarak öne çıkıyor. Bu adım adım kılavuzda, Aspose.OCR kullanarak dil seçimiyle OCR'nin nasıl gerçekleştirileceğini keşfederek çeşitli içerikleri hassasiyetle işleme potansiyelini ortaya çıkaracağız.

## Önkoşullar

Eğiticiye dalmadan önce aşağıdaki önkoşulların mevcut olduğundan emin olun:

- Java Geliştirme Ortamı: Sisteminizde Java'nın kurulu olduğundan ve geliştirme ortamınızın kurulduğundan emin olun.

-  Aspose.OCR Kütüphanesi: Java için Aspose.OCR kütüphanesini indirip yükleyin. Kütüphaneyi ve ilgili belgeleri bulabilirsiniz.[Burada](https://reference.aspose.com/ocr/java/).

- Resim Dosyası: Çıkarmak istediğiniz metni içeren bir resim dosyası hazırlayın. Örneğin "p3.png" adlı bir dosya kullanalım.

## Paketleri İçe Aktar

Aspose.OCR işlevselliğinden yararlanmak için Java projenizde gerekli paketleri içe aktarın. Java dosyanızın başına aşağıdaki satırları ekleyin:

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

## 1. Adım: Belge Dizininizi Kurun

```java
// Belgeler dizininin yolu.
String dataDir = "Your Document Directory";
```

"Belge Dizininiz"i, görüntü dosyanızın bulunduğu dizine giden gerçek yolla değiştirin.

## Adım 2: Görüntü Yolunu Tanımlayın

```java
// Görüntü yolu
String file = dataDir + "p3.png";
```

Dosya değişkenini, özel görüntü dosyanızı işaret edecek şekilde ayarlayın.

## 3. Adım: Aspose.OCR API Örneği Oluşturun

```java
// API örneği oluştur
AsposeOCR api = new AsposeOCR();
```

Özelliklerine erişmek için AsposeOCR nesnesini başlatın.

## 4. Adım: Tanıma Seçeneklerini Ayarlayın

```java
// Tanıma seçeneklerini ayarlayın
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

Tanıma ayarlarını gereksinimlerinize göre özelleştirin. Eğim, dil ve tanıma alanları gibi parametreleri ayarlayın.

## Adım 5: OCR Yapın ve Sonuçları Alın

```java
// Sonuç nesnesini al
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

Belirtilen görüntü dosyasını ve ayarları kullanarak OCR işlemini yürütün. Sonucu RecognitionResult nesnesinde yakalayın.

## Adım 6: Sonuçları Yazdırın ve Kullanın

```java
// Sonucu yazdır
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

Çıkarılan metni, tanıma alanlarını, JSON gösterimini, eğrilik açısını ve tüm uyarıları yazdırın. Sonuçları uygulamanızda gerektiği gibi kullanın.

## Çözüm

Bu eğitimde, dil seçimiyle OCR gerçekleştirmek için Aspose.OCR for Java'nın kusursuz entegrasyonunu inceledik. Bu güçlü kütüphane, görsellerden metni doğru bir şekilde çıkarmayı amaçlayan geliştiriciler için bir fırsatlar dünyasının kapılarını açıyor.

## SSS'ler

### S1: Aspose.OCR'ı tek bir tanıma sürecinde birden fazla dil için kullanabilir miyim?

C1: Evet, çok dilli içerik için tanıma doğruluğunu artırmak amacıyla Tanıma Ayarları'nda birden çok dil ayarlayabilirsiniz.

### S2: Aspose.OCR ile farklı görüntü formatlarını nasıl işleyebilirim?

Cevap2: Aspose.OCR PNG, JPEG ve TIFF dahil olmak üzere çeşitli görüntü formatlarını destekler. Görüntü yolu değişkeninde doğru dosya yolunu girmeniz yeterlidir.

### S3: Aspose.OCR'ın işleyebileceği görüntünün boyutunda bir sınır var mı?

Cevap3: Aspose.OCR farklı boyutlardaki görselleri işleyebilir ancak daha büyük görseller daha fazla işlem süresi ve kaynak gerektirebilir.

### S4: Bir görüntüdeki belirli bölgeler için tanıma ayarlarına ince ayar yapabilir miyim?

A4: Kesinlikle. Hedefli tanıma amacıyla görüntü içinde belirli dikdörtgenler tanımlamak için RecognitionAreas özelliğini kullanın.

### S5: Aspose.OCR hem kişisel hem de ticari projeler için uygun mudur?

Cevap5: Evet, Aspose.OCR esnek lisanslama seçenekleri sunarak hem kişisel hem de ticari kullanıma uygun hale getiriyor.