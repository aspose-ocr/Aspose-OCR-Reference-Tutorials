---
date: 2025-12-25
description: Aspose OCR for .NET ile OCR doğruluğunu artırın, yazım denetimi ve dil
  desteğinden yararlanarak hatalı yazımları düzeltin ve hatasız metin tanıma için
  sözlükleri özelleştirin.
linktitle: Improve OCR Accuracy with Spell Checking in Images
second_title: Aspose.OCR .NET API
title: Görüntülerde Yazım Denetimi ile OCR Doğruluğunu Artırın
url: /tr/net/ocr-optimization/result-correction-with-spell-checking/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntülerde Yazım Denetimi ile OCR Doğruluğunu Artırma

## Introduction

Optik Karakter Tanıma (OCR) ile çalıştığınızda nihai hedef **OCR doğruluğunu artırmak** ve elde edilen metnin orijinal görüntüyle mükemmel bir şekilde eşleşmesini sağlamaktır. Yanlış yazılmış kelimeler, özellikle kaynak görüntü gürültülü olduğunda veya alışılmadık yazı tipleri içerdiğinde yaygın bir hata kaynağıdır. Aspose.OCR for .NET, yalnızca bu hataları düzeltmekle kalmayıp aynı zamanda motoru özel sözlüklerle genişletmenize olanak tanıyan yerleşik yazım denetimi özellikleri sunar. Bu öğreticide, OCR sonuçlarını iyileştirmek için yazım denetimini nasıl kullanacağınızı, ön‑ve‑sonuç çıktısını göreceğinizi ve düzeltme sürecini belirli dil ihtiyaçlarınıza göre nasıl özelleştirebileceğinizi öğreneceksiniz.

## Quick Answers
- **What does spell checking do for OCR?** OCR çıktısındaki yanlış yazılmış kelimeleri otomatik olarak tespit eder ve en olası doğru alternatiflerle değiştirir.  
- **Which library provides this feature?** Aspose.OCR for .NET, kullanıma hazır bir yazım denetimi API’si içerir.  
- **Do I need an internet connection?** Hayır, yazım denetimi motoru tamamen çevrim dışı çalışır.  
- **Can I add my own terminology?** Evet, alan‑spesifik kelimeleri işlemek için özel bir kullanıcı sözlüğü sağlayabilirsiniz.  
- **What languages are supported?** Detaylar için “aspose ocr language support” bölümüne bakın.

## What is Spell Checking in OCR?

Yazım denetimi, OCR motoru tarafından döndürülen ham metni inceler, seçilen dil sözlüğünde bulunmayan tokenları belirler ve düzeltmeler önerir ya da uygular. Bu adım, özellikle taranmış belgeler, fişler veya formlarda OCR karakterleri yanlış yorumladığında **OCR doğruluğunu artırmak** için hayati öneme sahiptir.

## Why Use Aspose OCR Language Support?

Aspose.OCR, kapsamlı dil paketleriyle birlikte gelir ve ek sözlüklerin takılmasına izin verir. **aspose ocr language support**’u kullanmak, çok‑dilli belgeleri özel ayrıştırıcılar yazmadan işleyebilmenizi sağlar ve tanıma kalitesini daha da artıran dile özgü kurallara erişim sunar.

## Prerequisites

Spell‑checking sihrine dalmadan önce aşağıdaki ön koşulların yerine getirildiğinden emin olun:

- Aspose.OCR for .NET Library: Aspose.OCR kütüphanesini [release page](https://releases.aspose.com/ocr/net/) adresinden indirip kurun.  
- Document Directory: Belgeleriniz için ayrılmış bir dizin olduğundan emin olun. Kod parçacıklarındaki `"Your Document Directory"` ifadesini gerçek yol ile değiştirin.

## Import Namespaces

.NET projenizde gerekli ad alanlarını içe aktararak başlayalım:

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## Step 1: Initialize Aspose.OCR

OCR sürecini başlatmak için bir Aspose.OCR örneği başlatın.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Step 2: Recognize Image

Aspose.OCR kullanarak bir görüntüdeki metni tanıyın. İşte bu süreci gösteren bir örnek:

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## Step 3: Before Correction

Düzeltmeden önceki OCR sonucunu alın ve düzeltilmiş versiyonla karşılaştırın.

```csharp
// Get result
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## Step 4: After Correction

Yazım denetimini uygulayarak düzeltilmiş sonucu elde edin. Aşağıdaki kod bu adımı göstermektedir:

```csharp
// Get corrected result
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## Step 5: Misspelled Words and Suggestions

Aşağıdaki kodu kullanarak yanlış yazılmış kelimelerin bir listesini ve önerilen düzeltmeleri alın:

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

## Step 6: Correct User Text

Aspose.OCR kütüphanesiyle kullanıcı tarafından sağlanan belirli bir metni düzeltin:

```csharp
// Correct user text
Console.WriteLine("recogniition -> " + api.CorrectSpelling("recogniition"));
```

## Step 7: Correction with User Dictionary

Özel bir kullanıcı sözlüğü ekleyerek düzeltmeyi daha da geliştirin:

```csharp
// Get corrected result with user dictionary
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## Common Issues and Solutions

| Issue | Why It Happens | How to Fix |
|-------|----------------|------------|
| No suggestions returned | Dil paketi yüklenmemiş veya metin çok kısa. | `RecognitionSettings(Language.Eng)` ayarının kaynak görüntünün diliyle eşleştiğinden ve OCR sonucunun yeterli karakter içerdiğinden emin olun. |
| Custom dictionary not applied | Yanlış yol veya dosya formatı. | `dictionary.txt` dosyasının belirtilen konumda bulunduğunu ve her satırda bir kelime olacak şekilde biçimlendirildiğini doğrulayın. |
| Spell checker slows down large documents | Her kelime ayrı ayrı işlendiği için ek yük oluşur. | Sayfaları toplu olarak işleyin veya .NET Core üzerinde çalışıyorsanız bellek tahsisatını artırın. |

## Frequently Asked Questions

### Q1: Can I use Aspose.OCR for languages other than English?

A1: Evet, Aspose.OCR birden fazla dili destekler. Dil ayarlarını buna göre yapılandırın.

### Q2: How do I integrate Aspose.OCR into my .NET project?

A2: Ayrıntılı entegrasyon adımları için [documentation](https://reference.aspose.com/ocr/net/) sayfasına bakın.

### Q3: Is there a trial version available for Aspose.OCR?

A3: Evet, özellikleri keşfetmek için [free trial version](https://releases.aspose.com/) adresinden ücretsiz deneme sürümünü indirebilirsiniz.

### Q4: Can I upload a custom dictionary for spell checking?

A4: Kesinlikle! Öğreticide, kullanıcı tarafından sağlanan bir sözlükle düzeltmeyi nasıl geliştirebileceğiniz gösterilmektedir.

### Q5: Where can I seek support for Aspose.OCR?

A5: Topluluk desteği ve rehberlik için [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) adresini ziyaret edin.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Last Updated:** 2025-12-25  
**Tested With:** Aspose.OCR for .NET latest version  
**Author:** Aspose