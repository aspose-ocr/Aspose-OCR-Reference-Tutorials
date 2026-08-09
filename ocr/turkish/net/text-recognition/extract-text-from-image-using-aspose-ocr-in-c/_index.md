---
category: general
date: 2026-08-09
description: Aspose OCR ile C#’ta görüntüden metin çıkarın. OCR için görüntüyü nasıl
  yükleyeceğinizi, OCR dilini nasıl ayarlayacağınızı, görüntü OCR işlemini nasıl gerçekleştireceğinizi
  ve görüntüyü verimli bir şekilde metne dönüştürmeyi öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert image to text
- load image for ocr
- process image ocr
- set ocr language
language: tr
lastmod: 2026-08-09
og_description: Aspose OCR kullanarak C#'ta görüntüden metin çıkarın. Bu öğreticide,
  OCR için görüntünün nasıl yükleneceği, OCR dilinin nasıl ayarlanacağı, görüntünün
  OCR işlemi ve görüntünün birkaç satır kodla metne dönüştürülmesi gösterilmektedir.
og_image_alt: Screenshot of C# console output showing extracted text from an image
  using Aspose OCR
og_title: Aspose OCR ile görüntüden metin çıkarma – C# rehberi
schemas:
- author: Aspose
  dateModified: '2026-08-09'
  description: Extract text from image with Aspose OCR in C#. Learn how to load image
    for OCR, set OCR language, process image OCR, and convert image to text efficiently.
  headline: Extract text from image using Aspose OCR in C#
  type: TechArticle
- description: Extract text from image with Aspose OCR in C#. Learn how to load image
    for OCR, set OCR language, process image OCR, and convert image to text efficiently.
  name: Extract text from image using Aspose OCR in C#
  steps:
  - name: '**Create an OCR engine instance** – The `OcrEngine` encapsulates all OCR
      functionality. Disposing it promptly frees native resources, which is critical
      for long‑running services.'
    text: '**Create an OCR engine instance** – The `OcrEngine` encapsulates all OCR
      functionality. Disposing it promptly frees native resources, which is critical
      for long‑running services.'
  - name: '**Set OCR language** – Selecting the correct language module dramatically
      improves accuracy. Aspose provides over 30 language packs; the default is English.
      The example uses Cyrillic to demonstrate a non‑Latin script.'
    text: '**Set OCR language** – Selecting the correct language module dramatically
      improves accuracy. Aspose provides over 30 language packs; the default is English.
      The example uses Cyrillic to demonstrate a non‑Latin script.'
  - name: '**Load image for OCR** – The engine works with an `ImageStream`. Supplying
      a high‑resolution image (≥300 dpi) reduces misrecognition, especially for complex
      scripts.'
    text: '**Load image for OCR** – The engine works with an `ImageStream`. Supplying
      a high‑resolution image (≥300 dpi) reduces misrecognition, especially for complex
      scripts.'
  - name: '**Process image OCR** – This is where the heavy lifting occurs. The method
      returns an `OcrResult` containing the extracted text, confidence scores, and
      optional layout data.'
    text: '**Process image OCR** – This is where the heavy lifting occurs. The method
      returns an `OcrResult` containing the extracted text, confidence scores, and
      optional layout data.'
  - name: '**Convert image to text** – `result.Text` is a plain `string`. You can
      write it to a file, feed it into a search index, or pass it to downstream NLP
      pipelines.'
    text: '**Convert image to text** – `result.Text` is a plain `string`. You can
      write it to a file, feed it into a search index, or pass it to downstream NLP
      pipelines.'
  - name: Instantiates `OcrEngine`.
    text: Instantiates `OcrEngine`.
  - name: '**Sets OCR language** to Cyrillic (or any language you choose).'
    text: '**Sets OCR language** to Cyrillic (or any language you choose).'
  - name: '**Loads image for OCR** from disk.'
    text: '**Loads image for OCR** from disk.'
  - name: '**Processes image OCR** to obtain the textual result.'
    text: '**Processes image OCR** to obtain the textual result.'
  - name: '**Converts image to text** and prints it.'
    text: '**Converts image to text** and prints it.'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: C#'ta Aspose OCR kullanarak görüntüden metin çıkarma
url: /tr/net/text-recognition/extract-text-from-image-using-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Resimden metin çıkarma Aspose OCR ile C#'ta

Bir .NET uygulamasında **resimden metin çıkarma** ihtiyacınız varsa, bu kılavuz size eksiksiz, hemen çalıştırılabilir bir çözüm sunar. **OCR için resmi yükleme**, doğru dil modülünü seçme, OCR motorunu çalıştırma ve sonunda sadece birkaç C# satırıyla **resmi metne dönüştürme** nasıl yapılır göreceksiniz.

Bu öğretici, Aspose.OCR ile güvenilir sonuçlar elde etmek için gereken her şeyi kapsar; desteklenmeyen resim formatları ve dile özgü nüanslar gibi yaygın tuzakları da içerir. Sonunda, tanınan metni konsola yazdıran bağımsız bir programınız olacak.

## Başaracaklarınız

* Aspose OCR motoruna bir resim dosyası yükleyin.  
* **OCR dilini ayarlayın** (örnekte Kiril alfabesi, ancak desteklenen herhangi bir dil çalışır).  
* **Resim OCR'ını işleyin** ve metinsel temsili elde edin.  
* **Resmi metne dönüştürün** ve görüntüleyin, sonraki işleme veya depolamaya hazır.  

**Önkoşullar**

* .NET 6.0 veya üzeri (kod .NET Framework 4.6+ üzerinde de çalışır).  
* Visual Studio 2022 (veya C# destekleyen herhangi bir IDE).  
* Aspose.OCR NuGet paketi (`Install-Package Aspose.OCR`).  

---

## Resimden metin çıkarma – tam kod yürütmesi

Aşağıda eksiksiz, çalıştırılabilir program bulunmaktadır. Yeni bir konsol projesine kopyalayın ve `YOUR_DIRECTORY/sample_cyrillic.jpg` ifadesini kendi resminizin yolu ile değiştirin.

```csharp
using System;
using Aspose.OCR;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create an OCR engine instance.
            // The using block ensures the engine is disposed correctly.
            using (var engine = new OcrEngine())
            {
                // Step 2: Set OCR language.
                // Change OcrLanguage.Cyrillic to any other supported language,
                // e.g., OcrLanguage.English, OcrLanguage.Chinese, OcrLanguage.Hindi.
                engine.Language = OcrLanguage.Cyrillic;

                // Step 3: Load image for OCR.
                // ImageStream.FromFile reads the image from disk.
                // Supported formats: JPEG, PNG, BMP, TIFF, GIF.
                engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/sample_cyrillic.jpg");

                // Step 4: Process image OCR.
                // The Process method runs the recognition engine and returns an OcrResult.
                var result = engine.Process();

                // Step 5: Convert image to text.
                // The recognized text is available via result.Text.
                Console.WriteLine("=== Recognized Text ===");
                Console.WriteLine(result.Text);
            }
        }
    }
}
```

### Her adımın önemi

1. **Bir OCR motoru örneği oluşturun** – `OcrEngine`, tüm OCR işlevselliğini kapsar. Hemen dispose edilmesi, yerel kaynakları serbest bırakır; bu, uzun süre çalışan hizmetler için kritiktir.  
2. **OCR dilini ayarlayın** – Doğru dil paketinin seçilmesi doğruluğu büyük ölçüde artırır. Aspose 30'dan fazla dil paketi sunar; varsayılan İngilizcedir. Örnek, Latin dışı bir betimleme göstermek için Kiril alfabesini kullanır.  
3. **OCR için resmi yükleyin** – Motor, bir `ImageStream` ile çalışır. Yüksek çözünürlüklü bir resim (≥300 dpi) sağlamak, özellikle karmaşık betimlemelerde hatalı tanımayı azaltır.  
4. **Resim OCR'ını işleyin** – İşin yoğun kısmının gerçekleştiği yerdir. Metodu, çıkarılan metin, güven puanları ve isteğe bağlı yerleşim verilerini içeren bir `OcrResult` döndürür.  
5. **Resmi metne dönüştürün** – `result.Text` düz bir `string`'dir. Bunu bir dosyaya yazabilir, bir arama indeksine besleyebilir veya sonraki NLP boru hatlarına aktarabilirsiniz.  

---

## OCR için resmi yükleme

`ImageStream.FromFile` metodu yaygın raster formatlarını destekler. Resimleri bayt dizileri olarak alıyorsanız (ör. bir web API'sinden), bunun yerine `ImageStream.FromBytes(byte[])` kullanın:

```csharp
byte[] imageBytes = File.ReadAllBytes("path/to/image.png");
engine.Image = ImageStream.FromBytes(imageBytes);
```

**Pro ipucu:** Motorun önüne resmi göndermeden önce her zaman bozulmadığını doğrulayın. Hızlı bir `try { Image.FromFile(...); } catch { ... }` koruması çalışma zamanı istisnalarını önler.

---

## OCR dilini ayarlama

Aspose.OCR, çalışma zamanında etkinleştirebileceğiniz dil paketleriyle birlikte gelir. Mevcut tüm dilleri listelemek için:

```csharp
foreach (var lang in Enum.GetValues(typeof(OcrLanguage)))
{
    Console.WriteLine(lang);
}
```

Aynı belgede birden fazla dili tanımanız gerekiyorsa, bunları bitwise OR operatörüyle birleştirin:

```csharp
engine.Language = OcrLanguage.English | OcrLanguage.Russian;
```

**Köşe durum:** Sağ‑dan‑sola (RTL) dilleri (ör. Arapça) ile soldan‑sağa betimlemeleri karıştırmak ek yerleşim işleme gerektirebilir. Aspose yönü otomatik algılar, ancak `engine.PageSegmentationMode` ile ince ayar yapabilirsiniz.

---

## Resim OCR'ını işleme

`Process` çağrısı eşzamanlıdır ve motor bitene kadar bloklar. Büyük toplular veya UI uygulamaları için, asenkron aşırı yüklemeyi düşünün:

```csharp
var task = engine.ProcessAsync();
OcrResult result = await task;
```

**Yaygın tuzak:** `Process` çağrısından önce `engine.Image`'i ayarlamayı unutmak bir `InvalidOperationException` fırlatır. Her zaman önce resmi atayın.

---

## Resmi metne dönüştürme

Çıkarılan string, diğer .NET `string`'ler gibi işlenebilir. Örneğin, çıktıyı bir dosyaya yazmak için:

```csharp
File.WriteAllText("output.txt", result.Text);
```

Resimdeki satır sonlarını tam olarak korumanız gerekiyorsa, doğrudan `result.Text` kullanın. Sonradan işleme (ör. fazla boşlukları kaldırma) için standart string metodlarını uygulayın:

```csharp
string cleaned = result.Text
    .Replace("\r\n", "\n")
    .Trim();
```

---

## Tam örnek özeti

Her şeyi bir araya getirdiğimizde, program:

1. `OcrEngine`'i örnekler.  
2. **OCR dilini** Kiril alfabesine (veya seçtiğiniz herhangi bir dile) ayarlar.  
3. **OCR için resmi** diskinizden yükler.  
4. **Resim OCR'ını** işleyerek metinsel sonucu elde eder.  
5. **Resmi metne dönüştürür** ve yazdırır.  

Örnek, net bir Kiril alfabesi resmiyle çalıştırıldığında aşağıdaki gibi bir çıktı üretir:

```
=== Recognized Text ===
Пример текста на кириллице
```

Resim İngilizce metin içeriyorsa, sadece `engine.Language = OcrLanguage.English;` satırını değiştirin ve aynı kod **resimden metin çıkarma** işlemini doğru yapar.

---

## Sonuç

Artık Aspose OCR ile C#'ta **resimden metin çıkarma** yöntemini biliyorsunuz. Öğreticide resmi yükleme, uygun dili seçme, OCR sürecini çalıştırma ve sonraki kullanım için **resmi metne dönüştürme** konuları ele alındı.  

Bundan sonra şunları yapabilirsiniz:

* Diğer dillerle deney yapın (`load image for OCR` → `set OCR language` → `process image OCR`).  
* OCR adımını daha büyük bir boru hattına entegre edin (ör. belge alımı, aranabilir PDF'ler).  
* Görüntüleri toplu işleyerek veya asenkron API'yi kullanarak performansı optimize edin.  

Özel sözlükler, sayfa bölütleme modları ve OCR doğruluk ayarı gibi gelişmiş özellikler için Aspose.OCR belgelerini incelemekten çekinmeyin. Kodlamanın tadını çıkarın!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalarla tam çalışan kod örnekleri içerir.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}