---
category: general
date: 2026-09-06
description: Aspose.OCR kullanarak C#'ta OCR görüntüyü JSON'a dönüştürme – görüntüden
  metin çıkarmak ve JSON çıktısı almak için adım adım rehber.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- ocr image to json
- extract text from image
- convert image to text
- recognize text from photo
- load image for ocr
language: tr
lastmod: 2026-09-06
og_description: C# ile Aspose.OCR kullanarak OCR görüntüsünü JSON’a dönüştürün. OCR
  için bir görüntüyü nasıl yükleyeceğinizi, fotoğraftan metni nasıl tanıyacağınızı
  ve sonucu JSON’a nasıl dönüştüreceğinizi öğrenin.
og_image_alt: Screenshot of C# code that converts an OCR image to JSON using Aspose.OCR
og_title: OCR görüntüsünü C#'ta JSON'a dönüştürün – tam Aspose.OCR rehberi
schemas:
- author: Aspose
  dateModified: '2026-09-06'
  description: ocr image to json conversion in C# using Aspose.OCR – step‑by‑step
    guide to extract text from image and get JSON output.
  headline: How to convert an OCR image to JSON in C# with Aspose.OCR
  type: TechArticle
- description: ocr image to json conversion in C# using Aspose.OCR – step‑by‑step
    guide to extract text from image and get JSON output.
  name: How to convert an OCR image to JSON in C# with Aspose.OCR
  steps:
  - name: Place an image named `input.jpg` in the project root.
    text: Place an image named `input.jpg` in the project root.
  - name: Execute `dotnet run`.
    text: Execute `dotnet run`.
  - name: Observe the console output and open `output.json` to see the structured
      data.
    text: Observe the console output and open `output.json` to see the structured
      data.
  type: HowTo
- questions:
  - answer: Yes. Use `ocrEngine.SaveJson(Stream)` to write directly to a `MemoryStream`,
      then call `stream.ToArray()`.
    question: Can I get the OCR result as a byte array instead of a file?
  - answer: Aspose.OCR can accept PDF pages converted to images via Aspose.PDF, but
      the OCR engine itself works on raster images. Convert PDFs to images first,
      then **load image for ocr**.
    question: Does the engine support PDF input?
  - answer: 'Set `ocrEngine.Language = OcrLanguage.Arabic`. The JSON includes the
      correct text direction, which you can render in UI frameworks that support RTL.
      ## Conclusion You now have a complete solution for **ocr image to json** in
      C#. By loading an image, configuring the language, running the OCR engine, '
    question: How do I handle right‑to‑left scripts like Arabic?
  type: FAQPage
tags:
- Aspose.OCR
- C#
- JSON
- Image processing
title: Aspose.OCR ile C#’ta OCR görüntüsünü JSON’a nasıl dönüştürürsünüz
url: /tr/net/text-recognition/how-to-convert-an-ocr-image-to-json-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile Aspose.OCR kullanarak OCR görüntüsünü JSON’a dönüştürme

Bir .NET uygulamasında **ocr image to json** işlemi yapmanız gerekiyorsa, bu rehber Aspose.OCR ile nasıl yapılacağını gösterir. Görüntüyü OCR için yükleme, fotoğraftan metin tanıma ve sonucu JSON’a dönüştürme adımlarını, API’lerde veya veritabanlarında kullanabileceğiniz şekilde ele alacağız.

Görüntü dosyalarından metin çıkarma, fatura işleme, fiş tarama ve arşiv projeleri için yaygın bir gereksinimdir. Bu öğreticinin sonunda **convert image to text** yapabilecek, düz metin sonucunu alabilecek ve düzen bilgilerini koruyan yapılandırılmış bir JSON yükü oluşturabileceksiniz.

## Prerequisites

Başlamadan önce şunların yüklü olduğundan emin olun:

- .NET 6.0 SDK veya daha yeni bir sürüm  
- Visual Studio 2022 (veya .NET destekleyen herhangi bir editör)  
- Projenize eklenmiş bir Aspose.OCR NuGet paketi (`Aspose.OCR`)  
- Koddaki referansla erişebileceğiniz bir klasörde bulunan örnek bir görüntü (`input.jpg`)  

Ek bir OCR motoruna ihtiyacınız yok; Aspose.OCR içsel olarak tüm ağır işleri halleder.

## Step 1: Install the Aspose.OCR NuGet package

Proje klasörünüzde bir terminal açın ve şu komutu çalıştırın:

```bash
dotnet add package Aspose.OCR
```

Paket, **load image for ocr** işlemi, dil seçimi ve sonuç dışa aktarımı sağlayan `Aspose.OCR.OcrEngine` sınıfını içerir.

## Step 2: Create a new C# console project

Henüz bir projeniz yoksa, bir tane oluşturun:

```bash
dotnet new console -n OcrToJsonDemo
cd OcrToJsonDemo
```

İhtiyacınız olacak `using` yönergelerini ekleyin:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using System.IO;
```

## Step 3: Load the image and configure the OCR engine

Aşağıdaki kod, **load image for ocr**, dili ayarlama ve motoru işleme için hazırlama adımlarını gösterir. Bu örnekte Kiril alfabesini kullanıyoruz, ancak kaynağın diline göre `OcrLanguage.English`, `OcrLanguage.French` vb. dillerle değiştirebilirsiniz.

```csharp
// Step 3: Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Choose the language that matches the text in the image.
// Replace OcrLanguage.Cyrillic with the language you need.
ocrEngine.Language = OcrLanguage.Cyrillic;

// Load the image file. The ImageStream class abstracts file, stream, or byte[] sources.
string imagePath = Path.Combine(Environment.CurrentDirectory, "input.jpg");
ocrEngine.Image = ImageStream.FromFile(imagePath);
```

> **Why this matters:** Doğru dili ayarlamak, **recognize text from photo** işlemi sırasında doğruluğu büyük ölçüde artırır. Motor, dile özgü sözlükler ve karakter setleri kullanır.

## Step 4: Run the OCR process and retrieve results

Şimdi OCR motorunu çalıştırın. İşlem başarılı olursa, **extract text from image** sonucunu düz metin, HTML veya JSON olarak alabilirsiniz. Aspose.OCR, yapılandırılmış sonucu bir dosyaya yazan `SaveJson` metodunu sunar.

```csharp
// Step 4: Execute the OCR process
if (ocrEngine.Process())
{
    // Plain‑text output
    string plainText = ocrEngine.Text;
    Console.WriteLine("=== Plain Text ===");
    Console.WriteLine(plainText);

    // JSON output – includes bounding boxes, confidence scores, and line information
    string jsonPath = Path.Combine(Environment.CurrentDirectory, "output.json");
    ocrEngine.SaveJson(jsonPath);
    Console.WriteLine($"\nJSON result saved to: {jsonPath}");
}
else
{
    Console.WriteLine("OCR processing failed. Check the image path and format.");
}
```

### Expected JSON structure

Tipik bir `output.json` dosyası aşağıdaki gibi görünür (okunabilirlik için biçimlendirilmiş):

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Пример текста",
          "Confidence": 0.96,
          "Rect": { "X": 45, "Y": 120, "Width": 210, "Height": 30 }
        },
        {
          "Text": "Еще одна строка",
          "Confidence": 0.93,
          "Rect": { "X": 45, "Y": 160, "Width": 230, "Height": 28 }
        }
      ]
    }
  ]
}
```

JSON yükü, her satırın metnini, güven puanını ve orijinal fotoğrafta satırı çevreleyen dikdörtgeni içerir. Bu sayede OCR sonucunu UI öğeleri veya veritabanı alanlarıyla eşleştirmek kolaylaşır.

## Step 5: Full source code for the demo

Aşağıda **ocr image to json** iş akışını gerçekleştiren, çalıştırmaya hazır tam program yer almaktadır. `Program.cs` dosyasına kopyalayıp `dotnet run` komutuyla çalıştırın.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrToJsonDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Select the language (Cyrillic in this example)
            ocrEngine.Language = OcrLanguage.Cyrillic;

            // 3️⃣ Load the image you want to process
            string imagePath = Path.Combine(Environment.CurrentDirectory, "input.jpg");
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found: {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 4️⃣ Run the OCR process
            if (ocrEngine.Process())
            {
                // 5️⃣ Retrieve plain text (optional)
                string plainText = ocrEngine.Text;
                Console.WriteLine("=== Plain Text ===");
                Console.WriteLine(plainText);

                // 6️⃣ Save the result as JSON
                string jsonPath = Path.Combine(Environment.CurrentDirectory, "output.json");
                ocrEngine.SaveJson(jsonPath);
                Console.WriteLine($"\nJSON result saved to: {jsonPath}");
            }
            else
            {
                Console.WriteLine("OCR processing failed. Verify the image format and language settings.");
            }
        }
    }
}
```

### Running the example

1. Proje kök dizinine `input.jpg` adlı bir görüntü yerleştirin.  
2. `dotnet run` komutunu yürütün.  
3. Konsol çıktısını inceleyin ve yapılandırılmış veriyi görmek için `output.json` dosyasını açın.

## Pro tips and common pitfalls

| Situation | Recommendation |
|-----------|----------------|
| **Low‑resolution photos** | İşleme başlamadan önce DPI değerini artırın veya `ocrEngine.Image = ImageStream.FromFile(path, 300)` kullanarak 300 DPI zorlayın. |
| **Mixed languages** | `ocrEngine.Language = OcrLanguage.Multilingual` ayarlayın ve isteğe bağlı olarak `ocrEngine.Language = new[] { OcrLanguage.English, OcrLanguage.Cyrillic }` gibi bir dil listesi sağlayın. |
| **Large documents** | Bellek kullanımını düşük tutmak için bir seferde bir sayfa işleyin; motor çok sayfalı TIFF'leri destekler. |
| **Incorrect characters** | Doğru `OcrLanguage` seçildiğinden emin olun; yanlış dil seçimi **convert image to text** sırasında doğruluğu azaltır. |
| **JSON missing fields** | Aspose.OCR sürüm 23.6 veya üzeri kullandığınızdan emin olun; eski sürümlerde `SaveJson` metodu bulunmuyordu. |

## Frequently asked questions

**S: OCR sonucunu bir dosya yerine bayt dizisi olarak alabilir miyim?**  
C: Evet. `ocrEngine.SaveJson(Stream)` metodunu kullanarak doğrudan bir `MemoryStream`e yazın, ardından `stream.ToArray()` ile bayt dizisini elde edin.

**S: Motor PDF girişini destekliyor mu?**  
C: Aspose.OCR, PDF sayfalarını Aspose.PDF ile görüntülere dönüştürerek kabul edebilir, ancak OCR motoru kendisi raster görüntüler üzerinde çalışır. PDF'leri önce görüntülere dönüştürün, ardından **load image for ocr** yapın.

**S: Arapça gibi sağ‑dan‑sol (RTL) scriptleri nasıl ele alırım?**  
C: `ocrEngine.Language = OcrLanguage.Arabic` ayarlayın. JSON, doğru metin yönünü içerir; bunu RTL destekleyen UI çerçevelerinde render edebilirsiniz.

## Conclusion

Artık C# içinde **ocr image to json** için eksiksiz bir çözümünüz var. Bir görüntüyü yükleyip, dili yapılandırıp, OCR motorunu çalıştırıp ve sonucu JSON olarak dışa aktararak **extract text from image**, **convert image to text** ve **recognize text from photo** işlemlerini tek bir akışta gerçekleştirebilirsiniz.  

İleride şunları keşfedebilirsiniz:

- JSON çıktısını bir Web API (`ASP.NET Core`) ile bütünleştirme  
- Sonucu MongoDB gibi NoSQL veritabanına kaydetme  
- Yaygın OCR hatalarını düzeltmek için son‑işlem ekleme  

Farklı diller, görüntü formatları ve çıktı seçenekleriyle denemeler yaparak projenizin ihtiyaçlarına en uygun çözümü oluşturun. Kodlamanın tadını çıkarın!

## What Should You Learn Next?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmeniz ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım‑adım açıklamalı tam çalışan kod örnekleri içerir.

- [recognize text from image in C# – Complete Guide to OCR and JSON](/ocr/english/net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/)
- [Convert Image to Text in C# with Aspose OCR – Step‑by‑Step Guide](/ocr/english/net/text-recognition/convert-image-to-text-in-c-with-aspose-ocr-step-by-step-guid/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}