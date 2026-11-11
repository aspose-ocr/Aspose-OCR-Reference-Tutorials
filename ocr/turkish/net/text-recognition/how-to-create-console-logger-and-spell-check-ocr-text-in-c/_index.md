---
category: general
date: 2026-08-18
description: C#'ta konsol günlüğü oluşturmayı öğrenin ve Aspose AI'ı kullanarak OCR
  metnini bir imla denetimi sonrası işlemcisiyle düzeltin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create console logger
- correct ocr text
- spell check ocr
language: tr
lastmod: 2026-08-18
og_description: C#'ta konsol günlüğü oluşturun ve Aspose AI kullanarak OCR metnini
  düzeltin. OCR hattınıza bir yazım denetimi sonrası işlemci eklemek için bu kapsamlı
  rehberi izleyin.
og_image_alt: Illustration of creating a console logger in C# code editor
og_title: C#'ta Konsol Günlüğü Oluşturma ve OCR Metnini Yazım Denetimi – Adım Adım
  Rehber
schemas:
- author: Aspose
  dateModified: '2026-08-18'
  description: Learn how to create console logger in C# and use Aspose AI to correct
    OCR text with a spell‑check post‑processor.
  headline: How to create console logger and spell‑check OCR text in C#
  type: TechArticle
tags:
- C#
- OCR
- AI
- logging
title: C#'ta konsol logger oluşturma ve OCR metnini imla denetimi yapma
url: /tr/net/text-recognition/how-to-create-console-logger-and-spell-check-ocr-text-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta konsol günlüğü oluşturma ve OCR metnini yazım denetimi ile düzeltme

Eğer taranmış belgeleri işlerken tanı teşhis çıktısı için **konsol günlüğü oluşturmanız** gerekiyorsa, bu kılavuz eksiksiz bir çözüm sunar. Eğitim sonunda **OCR metnini** yerleşik bir yazım denetimi sonrası işlemcisiyle **düzeltmeyi** Aspose AI SDK kullanarak yapabileceksiniz.

OCR sonuçlarını işlemek çoğu zaman aşağı akış analizlerini etkileyen yazım hataları bırakır. Bir yazım denetimi adımı eklemek, metnin temiz ve indeksleme, çeviri ya da veri çıkarımı için hazır olmasını sağlar. Aşağıdaki bölümler, günlüğün oluşturulmasından son doğrulamaya kadar gereken tüm parçaları adım adım gösterir.

## Önkoşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

* .NET 6.0 veya daha yeni bir sürüm  
* Visual Studio 2022 (veya C# uyumlu herhangi bir IDE)  
* Projenize eklenmiş Aspose.AI NuGet paketi (`dotnet add package Aspose.AI`)  

Ek bir dış hizmete ihtiyaç yoktur; çünkü Aspose AI modeli otomatik olarak indirilebilir.

## Adım 1: Tanı amaçlı konsol günlüğü nasıl oluşturulur

Bir logger çalışma zamanı bilgilerini yakalar, model yükleme ya da post‑processor çalıştırma sırasında sorun gidermeyi kolaylaştırır. `ILogger` arayüzü, kodun geri kalanını değiştirmeden uygulamaları değiştirmenize olanak tanır.

```csharp
// Step 1: (Optional) Create a logger for diagnostic output
ILogger logger = new ConsoleLogger();   // set to null if logging is not needed
```

`ConsoleLogger` her log kaydını standart çıktı akışına yazar. Bir arayüz kullanmak kodun test edilebilir olmasını sağlar ve logger'ı daha sonra dosya‑tabanlı ya da bulut tabanlı bir logger ile değiştirebilmenize imkan verir.

## Adım 2: Otomatik indirmeyi etkinleştirmek için AI modelini yapılandırma

Aspose AI, ihtiyaç duyulan model dosyalarını isteğe bağlı olarak indirebilir. Yerel bir klasör belirtmek, tekrarlanan ağ trafiğini önler ve depolama üzerinde kontrol sağlar.

```csharp
// Step 2: Configure the AI model – enable automatic download and specify a local folder
AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
{
    AllowAutoDownload = true,
    DirectoryModelPath = "YOUR_DIRECTORY"
};
```

`AllowAutoDownload`, SDK'nın modeli ilk çalıştırmada indirmesini garanti eder. `DirectoryModelPath` ise makinenizde kalıcı bir konuma işaret eder; bu CI boru hatları için faydalıdır.

## Adım 3: Logger ile AsposeAI motorunu başlatma

Logger'ı motora geçirmek, model yükleme ve post‑processor çalıştırma dahil her iç işlem için tanı çıktısını bağlar.

```csharp
// Step 3: Initialise the AsposeAI engine with the logger
AsposeAI ai = new AsposeAI(logger);
```

`AsposeAI` yapıcı metodu bir `ILogger` örneği alır. Adım 1'de `null` verdiyseniz, motor sessiz çalışır.

## Adım 4: Yerleşik yazım denetimi post‑processor'ını oluşturma

Aspose AI, OCR sonuçları üzerinde doğrudan çalışan hazır bir yazım denetimi bileşeni sunar. Örneği oluşturmak için ek bir yapılandırma gerekmez.

```csharp
// Step 4: Create the built‑in spell‑check post‑processor
SpellCheckAIProcessor spellChecker = new SpellCheckAIProcessor();
```

`SpellCheckAIProcessor`, `IAIProcessor` arayüzünü uygular; bu sayede model yapılandırmasıyla birlikte kaydedilebilir.

## Adım 5: Yazım denetimi işlemcisini model yapılandırmasıyla birlikte kaydetme

İşlemciyi motora bağlamak, OCR sonuçlarının otomatik olarak yazım denetimi aşamasından geçmesini sağlar.

```csharp
// Step 5: Register the spell‑check processor together with the model configuration
ai.SetPostProcessor(spellChecker, modelConfig);
```

`SetPostProcessor`, `spellChecker`'ı `modelConfig`'e bağlar. Daha sonra `RunPostprocessor` çağırdığınızda, motor indirilen modeli kullanarak yazım denetimi mantığını çalıştırır.

## Adım 6: Önceden elde edilmiş OCR sonuçları üzerinde post‑processor'ı çalıştırma

`ocrResult` değişkeninde OCR çıktısı zaten saklanmış varsayımıyla, post‑processor'ı çağırarak düzeltilmiş metni elde edin.

```csharp
// Step 6: Execute the post‑processor on previously obtained OCR results (variable `ocrResult`)
ai.RunPostprocessor(ocrResult);
```

`RunPostprocessor`, `ocrResult`'un her sayfasını işler. Yazım denetimi algoritması tanı dizelerini analiz eder, dil‑özel sözlükleri uygular ve düzeltilmiş bir versiyon üretir.

## Adım 7: Düzeltlenmiş metni alıp görüntüleme

İşleme tamamlandıktan sonra `SpellCheckAIProcessor` temizlenmiş sonuçları tutar. Bunları alıp konsola yazdırabilirsiniz.

```csharp
// Step 7: Retrieve and display the corrected text
Console.WriteLine("CORRECTED RESULT\n");
Console.WriteLine(spellChecker.GetResult()[0].RecognitionText);
```

`GetResult()`'ın ilk öğesi OCR belgesinin ilk sayfasına karşılık gelir. Çok sayfalı bir dosya işlediyseniz, koleksiyonu döngüyle gezerek her sayfanın düzeltilmiş metnini görüntüleyin.

## Adım 8: İş bittiğinde kaynakları temizleme

`AsposeAI` örneğini dispose etmek, yönetilmeyen kaynakları serbest bırakır ve açık dosya tutamaçlarını kapatır.

```csharp
// Clean up resources when finished
ai.Dispose();
```

`Dispose` çağrısı, özellikle yerel kütüphanelerle çalışırken `IDisposable` uygulayan her nesne için en iyi uygulamadır.

## Beklenen çıktı

Program sorunsuz çalıştığında aşağıdaki gibi bir çıktı görürsünüz:

```
CORRECTED RESULT

The quick brown fox jumps over the lazy dog.
```

Yukarıdaki metin, orijinal OCR girdisinin yazım hataları yazım denetimi post‑processor'ı tarafından düzeltilmiş hâlini yansıtır.

## Yaygın sorular ve kenar durumları

**OCR sonucu boş olduğunda ne olur?**  
Post‑processor boş sayfaları sorunsuz bir şekilde ele alır ve boş bir string döndürür. İstisna fırlatılmaz.

**Özel bir sözlük kullanabilir miyim?**  
`SpellCheckAIProcessor` isteğe bağlı bir `CustomDictionaryPath` özelliği kabul eder. Alan‑özgü terimler gerekiyorsa, `SetPostProcessor`'ı çağırmadan önce bu yolu ayarlayın.

**Konsol logger'ı thread‑safe mi?**  
`ConsoleLogger`, .NET runtime tarafından senkronize edilen `Console.Out`'a yazar. Yüksek hacimli senaryolarda mesajları tamponlayan farklı bir logger ile değiştirebilirsiniz.

**Birçok belgeyi aynı anda işlemek istersem ne yapmalıyım?**  
Her thread için ayrı bir `AsposeAI` örneği oluşturun ya da thread‑safe bir havuz deseni kullanın. Tek bir örneği paylaşmak, iç model durumunun thread‑local olmaması nedeniyle yarış koşullarına yol açabilir.

## Sonuç

Artık C#'ta **konsol günlüğü oluşturmayı** ve **OCR metnini düzeltmek** için bir **yazım denetimi post‑processor** entegrasyonunu biliyorsunuz. Logger başlatmadan model yapılandırmasına, işleme ve temizlik aşamasına kadar eksiksiz bir iş akışı, sağlam bir OCR düzeltme hattı için gerekli tüm adımları kapsar.

Sonraki adım olarak, bu hattı dil tespiti ya da varlık çıkarımı gibi ek post‑processor'larla genişletebilirsiniz. Ayrıca, daha zengin tanı verileri yakalamak için Serilog gibi alternatif logging çerçevelerini deneyebilirsiniz. İyi kodlamalar!

## Bir Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Create Searchable PDF with Aspose OCR Batch Processing – C# Guide](/ocr/english/net/ocr-optimization/create-searchable-pdf-with-batch-ocr-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}