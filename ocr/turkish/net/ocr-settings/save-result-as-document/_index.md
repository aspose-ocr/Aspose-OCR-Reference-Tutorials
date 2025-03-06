---
title: Sonucu OCR Görüntü Tanıma'da Belge Olarak Kaydet
linktitle: Sonucu OCR Görüntü Tanıma'da Belge Olarak Kaydet
second_title: Aspose.OCR .NET API'si
description: Aspose.OCR for .NET'in potansiyelini ortaya çıkarın. Resimlerdeki metni kolayca tanıyın ve sonuçları çeşitli belge formatlarında kaydedin.
weight: 10
url: /tr/net/ocr-settings/save-result-as-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sonucu OCR Görüntü Tanıma'da Belge Olarak Kaydet

## giriiş

Aspose.OCR for .NET ile optik karakter tanımanın (OCR) heyecan verici dünyasına hoş geldiniz! Bu kapsamlı eğitimde, resimlerdeki metni tanımak için Aspose.OCR kullanmanın inceliklerini inceleyeceğiz ve sonuçların çeşitli belge formatlarında nasıl kaydedileceğini göstereceğiz.

## Önkoşullar

Bu OCR yolculuğuna çıkmadan önce aşağıdaki önkoşulların mevcut olduğundan emin olun:

-  .NET için Aspose.OCR. Aspose.OCR kütüphanesinin kurulu olduğundan emin olun. İndirebilirsin[Burada](https://releases.aspose.com/ocr/net/).

-  Belge Dizini: Belgeleriniz için belirlenmiş bir dizine sahip olun ve bu dizini güncelleyin.`dataDir` buna göre sağlanan koddaki değişken.

## Ad Alanlarını İçe Aktar

Gerekli ad alanlarını içe aktararak başlayın. Bunlar kodunuzu OCR yetenekleriyle güçlendirecek yapı taşlarıdır.

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

Şimdi örneği birden çok adıma ayıralım:

## Adım 1: Aspose.OCR'ı başlatın

```csharp
// Belgeler dizininin yolu.
string dataDir = "Your Document Directory";

// AsposeOcr örneğini başlat
AsposeOcr api = new AsposeOcr();
```

Bu adım Aspose.OCR API'sini başlatarak ortamı hazırlar.

## Adım 2: Görüntüyü Tanıyın

```csharp
// Resmi tanı
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

Burada, belirtilen görselin içindeki metni tanımak için Aspose.OCR'ı kullanıyoruz ("sample.png"yi görsel dosyanızla değiştirin).

## 3. Adım: Sonucu Farklı Formatlarda Kaydedin

```csharp
// Sonucu tercih ettiğiniz formatta kaydedin
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

Bu adımı ihtiyaçlarınıza göre özelleştirin. Aspose.OCR, tanınan metni DOCX, TXT, PDF ve XLSX gibi çeşitli belge formatlarında kaydetmenize olanak tanır.

## Adım 4: Başarı Mesajını Görüntüleyin

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

İşlemin herhangi bir aksama olmadan tamamlandığını bildiren basit bir onay mesajı.

Bu adımları izleyerek Aspose.OCR for .NET'in resimlerdeki metni tanıma ve sonuçları farklı belge formatlarında kaydetme gücünden başarıyla yararlandınız.

## Çözüm

Sonuç olarak Aspose.OCR for .NET, görüntülerde metin tanıma konusunda birçok olanak sunuyor. İster veri çıkarıyor olun ister aranabilir belgeler oluşturuyor olun Aspose.OCR, sezgisel API'si ile süreci basitleştirir.

## SSS'ler

### S1. Aspose.OCR farklı görüntü formatlarıyla uyumlu mu?

Cevap1: Evet, Aspose.OCR çok çeşitli görüntü formatlarını destekleyerek OCR görevlerinizde esneklik sağlar.

### S2: Daha iyi doğruluk için tanıma ayarlarını özelleştirebilir miyim?

A2: Kesinlikle! Aspose.OCR, OCR sürecine özel gereksinimlerinize göre ince ayar yapmak için tanıma ayarları sağlar.

### S3: Ücretsiz deneme sürümü mevcut mu?

 C3: Evet, ücretsiz deneme sürümüyle başlayabilirsiniz[Burada](https://releases.aspose.com/).

### S4: Aspose.OCR için nasıl geçici lisans alabilirim?

 Cevap4: Geçici lisanslar alınabilir[Burada](https://purchase.aspose.com/temporary-license/).

### S5: Nereden yardım isteyebilirim veya toplulukla bağlantı kurabilirim?

 Cevap5: Aspose.OCR topluluğuna şu adresten katılın:[Aspose Forumu](https://forum.aspose.com/c/ocr/16) Destek ve tartışmalar için.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
