---
title: OCR Görüntü Tanıma'da Yazım Denetimi ile Sonuç Düzeltme
linktitle: OCR Görüntü Tanıma'da Yazım Denetimi ile Sonuç Düzeltme
second_title: Aspose.OCR .NET API'si
description: Aspose.OCR for .NET ile OCR doğruluğunu artırın. Yazımları düzeltin, sözlükleri özelleştirin ve hatasız metin tanıma işlemini zahmetsizce gerçekleştirin.
weight: 13
url: /tr/net/ocr-optimization/result-correction-with-spell-checking/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Görüntü Tanıma'da Yazım Denetimi ile Sonuç Düzeltme

## giriiş

Optik Karakter Tanıma (OCR) alanında, görüntülerden anlamlı bilgiler çıkarmak için doğru sonuçlara ulaşmak çok önemlidir. Yaygın zorluklardan biri, tanıma sürecinde yanlış yazılan kelimelerle uğraşmaktır. Neyse ki Aspose.OCR for .NET, yazım denetimi yoluyla OCR sonuçlarını iyileştirmek için güçlü bir çözüm sunuyor.

Bu eğitim, Aspose.OCR for .NET'i kullanarak yazım denetimiyle sonuç düzeltme sürecinde size rehberlik edecektir. Sonunda, OCR'dan türetilmiş metnin doğruluğunu artıracak donanıma sahip olacak, böylece daha hassas ve hatasız bir çıktı elde edeceksiniz.

## Önkoşullar

Yazım denetimi büyüsüne dalmadan önce aşağıdaki önkoşulların mevcut olduğundan emin olun:

-  Aspose.OCR for .NET Library: Aspose.OCR kütüphanesini şu adresten indirip yükleyin:[yayın sayfası](https://releases.aspose.com/ocr/net/).

- Belge Dizini: Belgeleriniz için belirlenmiş bir dizininiz olduğundan emin olun. Kod parçacıklarındaki "Belge Dizininiz"i gerçek yolla değiştirin.

## Ad Alanlarını İçe Aktar

.NET projenize gerekli ad alanlarını içe aktararak başlayalım:

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## Adım 1: Aspose.OCR'ı başlatın

OCR sürecini başlatmak için Aspose.OCR örneğini başlatın.

```csharp
// Belgeler dizininin yolu.
string dataDir = "Your Document Directory";

// AsposeOcr örneğini başlat
AsposeOcr api = new AsposeOcr();
```

## Adım 2: Görüntüyü Tanıyın

Daha sonra Aspose.OCR kullanarak görüntüdeki metni tanıyın. İşte bu süreci gösteren bir pasaj:

```csharp
// Resmi tanı
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## Adım 3: Düzeltmeden Önce

Düzeltilmiş sürümle karşılaştırmak için düzeltmeden önce OCR sonucunu alın.

```csharp
// Sonuç al
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## Adım 4: Düzeltmeden Sonra

Düzeltilmiş sonucu elde etmek için yazım denetimi uygulayın. Aşağıdaki kod parçacığı bu adımı göstermektedir:

```csharp
// Düzeltilmiş sonucu alın
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## Adım 5: Yanlış Yazılan Kelimeler ve Öneriler

Aşağıdaki kodu kullanarak yanlış yazılan kelimelerin bir listesini ve önerilen düzeltmeleri edinin:

```csharp
// Yanlış yazılan kelimelerin listesini önerilerle birlikte alın
List<SpellCheckError> errorsList = result.GetSpellCheckErrorList(SpellCheckLanguage.Eng);
foreach (var word in errorsList)
{
	Console.Write("Word:" + word.Word);
	Console.Write(" StartPosition:" + word.StartPosition);
	Console.WriteLine(" Length:" + word.Length);
	Console.WriteLine("SuggestedWords:");
	foreach (var suggest in word.SuggestedWords)
	{
		Console.Write(suggest.Word + " ");
	}
	Console.WriteLine();
}
```

## Adım 6: Kullanıcı Metnini Doğrulayın

Aspose.OCR kitaplığını kullanarak kullanıcı tarafından sağlanan belirli metni düzeltin:

```csharp
// Kullanıcı metnini düzeltin
Console.WriteLine("recogniition -> " + api.CorrectSpelling("recogniition"));
```

## Adım 7: Kullanıcı Sözlüğü ile Düzeltme

Özel bir kullanıcı sözlüğü ekleyerek düzeltmeyi daha da geliştirin:

```csharp
// Kullanıcı sözlüğüyle düzeltilmiş sonucu alın
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## Çözüm

Tebrikler! Aspose.OCR for .NET'in yazım denetimi özelliklerini başarıyla kullandınız. Bu özellik, OCR sonuçlarını hassaslaştırmanıza olanak tanıyarak doğruluğu garanti eder ve hataları ortadan kaldırır.

## SSS'ler

### S1: Aspose.OCR'ı İngilizce dışındaki diller için de kullanabilir miyim?

Cevap1: Evet, Aspose.OCR birden fazla dili destekler. Dil ayarlarını buna göre yapın.

### S2: Aspose.OCR'ı .NET projeme nasıl entegre edebilirim?

 A2: Bkz.[dokümantasyon](https://reference.aspose.com/ocr/net/) ayrıntılı entegrasyon adımları için.

### S3: Aspose.OCR'ın deneme sürümü mevcut mu?

 A3: Evet, özellikleri keşfedebilirsiniz.[ücretsiz deneme sürümü](https://releases.aspose.com/).

### S4: Yazım denetimi için özel bir sözlük yükleyebilir miyim?

Cevap4: Kesinlikle! Eğitimde, kullanıcı tarafından sağlanan bir sözlük kullanılarak düzeltmenin nasıl geliştirileceği gösterilmektedir.

### S5: Aspose.OCR için nereden destek alabilirim?

 A5: ziyaret edin[Aspose.OCR forumu](https://forum.aspose.com/c/ocr/16) topluluk desteği ve rehberlik için.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
