---
date: 2026-04-23
description: Aspose OCR for .NET ile OCR doğruluğunu artırın; imla kontrolü, OCR dil
  paketi desteği ve özel sözlüklerden yararlanarak taranmış belgelerde OCR kalitesini
  yükseltin.
keywords:
- improve ocr accuracy
- ocr language pack
- process scanned documents
- boost ocr quality
- ocr spell checking
linktitle: Görüntülerde Yazım Denetimi ile OCR Doğruluğunu Artırın
second_title: Aspose.OCR .NET API
title: Görsellerde Yazım Denetimi ile OCR Doğruluğunu Artırın
url: /tr/net/ocr-optimization/result-correction-with-spell-checking/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntülerde Yazım Denetimi ile OCR Doğruluğunu Artırma

Optik Karakter Tanıma (OCR) ile çalıştığınızda nihai hedef **OCR doğruluğunu artırmak** ve çıkarılan metnin orijinal görüntüyle mükemmel bir şekilde eşleşmesini sağlamaktır. Yanlış yazılmış kelimeler, gürültülü arka planlar ve alışılmadık yazı tipleri sonucu bozan yaygın suçlular arasındadır. Aspose.OCR’nin yerleşik yazım denetimi motorunu geniş OCR dil paketiyle birleştirerek herhangi bir taranmış belge için **OCR kalitesini büyük ölçüde artırabilirsiniz**.

## Yazım Denetimi ile OCR Doğruluğunu Nasıl İyileştirirsiniz

Bu bölümde, bir görüntüyü yüklemekten yazım denetimini uygulamaya ve son olarak özel bir kullanıcı sözlüğüyle çıktıyı parlatmaya kadar tam iş akışını adım adım inceleyeceğiz. Gerçek dünyadan önce‑ve‑sonra örneklerini görecek, taranmış belgeleri işlerken bunun neden önemli olduğunu anlayacak ve OCR yazım denetimi özelliğinden en iyi şekilde yararlanmak için ipuçlarını keşfedeceksiniz.

## Hızlı Yanıtlar
- **Yazım denetimi OCR için ne yapar?** OCR çıktısındaki yanlış yazılmış kelimeleri otomatik olarak algılar ve en olası doğru alternatiflerle değiştirir.  
- **Bu özelliği hangi kütüphane sağlar?** Aspose.OCR for .NET, kullanıma hazır bir yazım denetimi API'si içerir.  
- **İnternet bağlantısına ihtiyacım var mı?** Hayır, yazım denetimi motoru tamamen çevrim dışı çalışır.  
- **Kendi terminolojimi ekleyebilir miyim?** Evet, alan‑spesifik kelimeler için özel bir kullanıcı sözlüğü sağlayabilirsiniz.  
- **Hangi diller destekleniyor?** Ayrıntılar için “aspose ocr language support” bölümüne bakın.

## OCR'da Yazım Denetimi Nedir?

Yazım denetimi, OCR motoru tarafından döndürülen ham metni inceler, seçilen dil sözlüğünde tanımlı olmayan tokenları belirler ve düzeltmeler önerir veya uygular. Bu adım, özellikle taranmış belgeler, makbuzlar veya formlarda OCR karakterleri yanlış yorumlayabildiğinde **OCR doğruluğunu artırmak** için esastır.

## Neden Aspose OCR Dil Paketi Kullanmalı?

Aspose.OCR, kapsamlı dil paketleriyle birlikte gelir ve ek sözlükler takmanıza olanak tanır. **aspose ocr language support**’u kullanmak, özel ayrıştırıcılar yazmadan çok dilli belgelerle çalışmanızı sağlar ve tanıma kalitesini daha da artıran dile özgü kurallara erişmenizi sağlar.

## Önkoşullar

Büyülü yazım denetimi işlevine geçmeden önce aşağıdaki önkoşulları yerine getirdiğinizden emin olun:

- Aspose.OCR for .NET Kütüphanesi: Aspose.OCR kütüphanesini [release page](https://releases.aspose.com/ocr/net/) adresinden indirin ve kurun.

- Belge Dizini: Belgeleriniz için belirlenmiş bir dizininiz olduğundan emin olun. Kod parçacıklarındaki `"Your Document Directory"` ifadesini gerçek yol ile değiştirin.

## Ad Alanlarını İçe Aktarın

Gerekli ad alanlarını .NET projenizde içe aktarmaya başlayalım:

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## Adım 1: Aspose.OCR'yi Başlatın

OCR sürecini başlatmak için bir Aspose.OCR örneği oluşturun.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Adım 2: Görüntüyü Tanıma

Sonra, Aspose.OCR kullanarak bir görüntüdeki metni tanıyın. İşte bu süreci gösteren bir kod parçacığı:

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## Adım 3: Düzeltmeden Önce

Düzeltmeden önceki OCR sonucunu alarak düzeltilmiş sürümle karşılaştırın.

```csharp
// Get result
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## Adım 4: Düzeltmeden Sonra

Yazım denetimini uygulayarak düzeltilmiş sonucu elde edin. Aşağıdaki kod parçacığı bu adımı gösterir:

```csharp
// Get corrected result
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## Adım 5: Yanlış Yazılmış Kelimeler ve Öneriler

Aşağıdaki kodu kullanarak yanlış yazılmış kelimelerin ve önerilen düzeltmelerin bir listesini alın:

```csharp
// Get list of misspelled words with suggestions
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

## Adım 6: Kullanıcı Metnini Düzelt

Aspose.OCR kütüphanesini kullanarak belirli kullanıcı sağladığı metni düzeltin:

```csharp
// Correct user text
Console.WriteLine("recogniition -> " + api.CorrectSpelling("recogniition"));
```

## Adım 7: Kullanıcı Sözlüğü ile Düzeltme

Özel bir kullanıcı sözlüğü ekleyerek düzeltmeyi daha da geliştirin:

```csharp
// Get corrected result with user dictionary
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## OCR Kalitesini Artırmak İçin İpuçları

- **Kaynak belgeye uygun doğru OCR dil paketini seçin**. Fransızca bir belge için `Language.Eng` kullanmak doğruluğu büyük ölçüde düşürür.  
- **Görüntüleri ön‑işlemden geçirin** (eğriltme düzeltme, gürültü azaltma, kontrast artırma) OCR motoruna göndermeden önce; daha temiz görüntüler daha az yanlış yazım üretir.  
- **Kısa bir kullanıcı sözlüğü tutun**—her satırda bir kelime—böylece yazım denetleyicisi özel terimleri hızlıca bulur ve büyük toplularda yavaşlamaz.  
- **Çok sayfalı PDF'lerle çalışırken sayfaları toplu işleyin**; bu bellek kullanımını azaltır ve yazım denetimi aşamasını hızlandırır.

## Yaygın Sorunlar ve Çözümleri

| Sorun | Neden Oluşur | Nasıl Düzeltilir |
|-------|----------------|------------|
| Öneri döndürülmedi | Dil paketi yüklenmemiş veya metin çok kısa. | Kaynak görüntünün diliyle eşleşecek şekilde `RecognitionSettings(Language.Eng)` ayarlandığından ve OCR sonucunun yeterli karakter içerdiğinden emin olun. |
| Özel sözlük uygulanmadı | Yanlış yol veya dosya biçimi. | `dictionary.txt` dosyasının belirtilen konumda bulunduğunu ve her satırda bir kelime kullandığını doğrulayın. |
| Yazım denetleyicisi büyük belgelerde yavaşlıyor | Her kelimeyi ayrı ayrı işlemek ek yük getirir. | Sayfaları toplu işleyin veya .NET Core üzerinde çalışıyorsanız bellek tahsisatını artırın. |

## Sık Sorulan Sorular

### Q1: Aspose.OCR'yi İngilizce dışındaki dillerde kullanabilir miyim?
A1: Evet, Aspose.OCR birden fazla dili destekler. Dil ayarlarını buna göre değiştirin.

### Q2: Aspose.OCR'yi .NET projemde nasıl entegre ederim?
A2: Ayrıntılı entegrasyon adımları için [documentation](https://reference.aspose.com/ocr/net/) adresine bakın.

### Q3: Aspose.OCR için bir deneme sürümü mevcut mu?
A3: Evet, özellikleri [free trial version](https://releases.aspose.com/) adresinden keşfedebilirsiniz.

### Q4: Yazım denetimi için özel bir sözlük yükleyebilir miyim?
A4: Kesinlikle! Eğitim, kullanıcı tarafından sağlanan bir sözlük kullanarak düzeltmeyi nasıl geliştirebileceğinizi gösterir.

### Q5: Aspose.OCR için nereden destek alabilirim?
A5: Topluluk desteği ve rehberlik için [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) adresini ziyaret edin.

---

**Son Güncelleme:** 2026-04-23  
**Test Edilen:** Aspose.OCR for .NET latest version  
**Yazar:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}