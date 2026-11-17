---
category: general
date: 2026-05-02
description: C# OCR öğreticisi, C# ile metin görüntüsü nasıl çıkarılır ve PNG metni
  nasıl tanınır, ardından JsonSerializer C# kullanarak girintili JSON nasıl yazılır
  gösterir. Geliştiriciler için adım adım rehber.
draft: false
keywords:
- c# ocr tutorial
- extract text image c#
- recognize png text
- write indented json
- use jsonserializer c#
language: tr
og_description: c# ocr öğreticisi, c# ile metin görüntüsünden metin çıkarmayı ve png
  metnini tanımayı gösterir, ardından JsonSerializer c# ile girintili json yazar.
  Tam, çalıştırılabilir örnek.
og_title: c# ocr öğretici – Metni Çıkar ve Girintili JSON Olarak Dışa Aktar
tags:
- OCR
- C#
- Aspose
- JSON
title: c# OCR öğretici – Görüntülerden Metin Çıkar ve Girintili JSON Olarak Dışa Aktar
url: /tr/net/text-recognition/c-ocr-tutorial-extract-text-from-images-and-export-as-indent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Görüntülerden Metin Çıkar ve Girintili JSON Olarak Dışa Aktar

Hiç **c# ocr tutorial**'a ihtiyaç duydunuz mu, ki metin fotoğrafından doğrudan güzel formatlanmış bir JSON dosyasına gitsin? Tek başınıza değilsiniz. Birçok projede – fatura tarama, fiş ayrıştırma ya da hatta basit meme‑metni çıkarma gibi – bir PNG dosyası elde eder ve özel bir tanıyıcı yazmadan kelimeleri nasıl çıkaracağınızı merak edersiniz.  

Bu rehber size uygulamalı bir çözüm sunuyor: Aspose.OCR kullanarak **extract text image c#** yapacağız, **recognize png text** gerçekleştireceğiz ve ardından C#'ta `JsonSerializer` ile **write indented json** yazacağız. Sonunda, herhangi bir .NET çözümüne ekleyebileceğiniz bağımsız bir konsol uygulamanız olacak. Belirsiz “belgelere bak” bağlantıları yok, sadece eksiksiz, kopyala‑yapıştır hazır bir örnek.

## Gereksinimler

- **.NET 6** (veya herhangi bir yeni .NET sürümü). Eski framework'ler çalışır, ancak gösterilen sözdizimi .NET 6+ hedefler.
- **Aspose.OCR for .NET** – NuGet üzerinden kurun: `dotnet add package Aspose.OCR`.
- Açık, makine‑okunabilir metin içeren örnek bir PNG görüntüsü (`text.png`).
- Tercih ettiğiniz IDE veya editör – Visual Studio, VS Code, Rider vb.

> **Pro ipucu:** Birçok görüntüyü işleyecekseniz, dosya başına yeni bir `OcrEngine` örneği oluşturmak yerine tek bir `OcrEngine` örneğini yeniden kullanmayı düşünün. Bu, aşırı yükü azaltır ve verimliliği artırır.

## Adım 1: c# ocr tutorial Projesi Oluşturun

İlk olarak, bir konsol projesi oluşturun. Aşağıdaki komutlar iskeleti oluşturur ve OCR kütüphanesini ekler:

```bash
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo
dotnet add package Aspose.OCR
```

Şimdi oluşturulan `Program.cs` dosyasını açın. İçeriğini daha sonra tam örnekle değiştireceğiz, ancak şimdilik projenin derlendiğinden emin olun:

```bash
dotnet build
```

Eğer hata görmüyorsanız, devam etmeye hazırsınız.

## Adım 2: Görüntüden PNG Metnini Tanıma

Herhangi bir **c# ocr tutorial**'ın kalbi OCR motorudur. Aspose.OCR düşük seviyeli detayları soyutlayarak size temiz bir `OcrEngine` sınıfı sunar. Aşağıda motoru oluşturuyor, bir PNG dosyasına işaret ediyor ve metni tanımasını istiyoruz.

```csharp
using Aspose.OCR;
using System;
using System.Text.Json;

class JsonExportExample
{
    public static void Run()
    {
        // 1️⃣ Create an OCR engine instance – this is the entry point for all OCR work.
        var ocrEngine = new OcrEngine();

        // 2️⃣ Recognize text from the input image. 
        //    The method automatically detects the language (default is English) and returns an OcrResult.
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/text.png");

        // If the image couldn't be read, handle it gracefully.
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("No text detected – double‑check the file path and image quality.");
            return;
        }

        // Continue to serialization...
```

### Neden Bu Çalışır

- **`RecognizeImage`** birçok formatı (PNG, JPEG, BMP) kabul eder. Biz özellikle **recognize png text** yapıyoruz çünkü PNG kayıpsız detayları korur, bu da OCR için idealdir.
- Dönen `OcrResult` sadece düz metni değil, aynı zamanda her glif için bir güven puanı içerir; düşük güvenilirlikli karakterleri sonradan filtrelemeniz gerektiğinde faydalıdır.

## Adım 3: JsonSerializer c# ile Girintili JSON Yazma

Şimdi `ocrResult`'a sahip olduğumuza göre, **c# ocr tutorial**'ımızdaki bir sonraki mantıklı adım bu nesneyi insan tarafından okunabilir JSON'a dönüştürmektir. Dahili `System.Text.Json` serileştiricisi işi yapar ve biz bunu **write indented json** olacak şekilde yapılandıracağız.

```csharp
        // 3️⃣ Serialize the OCR result (including confidence per glyph) to indented JSON.
        var jsonOptions = new JsonSerializerOptions
        {
            WriteIndented = true // This makes the output pretty‑printed.
        };

        string jsonOutput = JsonSerializer.Serialize(ocrResult, jsonOptions);

        // 4️⃣ Display the JSON result – you could also write it to a file if you prefer.
        Console.WriteLine(jsonOutput);
    }
}
```

### `JsonSerializer`'ı Doğru Kullanma

- `WriteIndented` bayrağı, üçüncü‑taraf kütüphaneler eklemeden **write indented json** yapmanın en basit yoludur.
- Eğer camel‑case özellik adlarına ihtiyacınız olursa, seçeneklere `PropertyNamingPolicy = JsonNamingPolicy.CamelCase` ekleyin.
- `jsonOutput` dizesi `File.WriteAllText("result.json", jsonOutput);` ile kaydedilebilir – gerçek dünya veri akışları için kullanışlı bir ayar.

## Adım 4: Çalıştır ve Çıktıyı Doğrula

Programı derleyip çalıştırın:

```bash
dotnet run
```

`text.png` dosyasının *“Hello, OCR World!”* ifadesini içerdiğini varsayarsak, aşağıdakine benzer bir şey görmelisiniz:

```json
{
  "Text": "Hello, OCR World!",
  "Confidence": 0.9875,
  "Lines": [
    {
      "Text": "Hello, OCR World!",
      "Confidence": 0.9875,
      "Words": [
        {
          "Text": "Hello,",
          "Confidence": 0.9921,
          "BoundingBox": { "X": 12, "Y": 34, "Width": 58, "Height": 20 }
        },
        {
          "Text": "OCR",
          "Confidence": 0.9812,
          "BoundingBox": { "X": 78, "Y": 34, "Width": 34, "Height": 20 }
        },
        {
          "Text": "World!",
          "Confidence": 0.9890,
          "BoundingBox": { "X": 118, "Y": 34, "Width": 62, "Height": 20 }
        }
      ]
    }
  ]
}
```

Bu JSON **girintili** olduğundan, günlüklerde okumak ya da sonraki hizmetlere teslim etmek kolaydır.

### Kenar Durumları ve İpuçları

| Durum | Ne Yapmalı |
|-----------|------------|
| **Görüntü bulanık** | `RecognizeImage` çağırmadan önce `ocrEngine.Config.Dpi` değerini artırın (örnek: `ocrEngine.Config.Dpi = 300`). |
| **İngilizce dışı dil** | `ocrEngine.Config.Language = OcrLanguage.German` (veya desteklenen herhangi bir dil) olarak ayarlayın. |
| **Büyük dosya topluluğu** | Bir dizin üzerinde döngü kurun, aynı `OcrEngine` örneğini yeniden kullanın; her JSON sonucunu benzersiz bir dosya adıyla kaydedin. |
| **Yalnızca yüksek güvenilirlikli metin** | Serileştirmeden önce `ocrResult.Lines` içinde `Confidence` ≥ 0.95 olanları filtreleyin. |

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda *tam* program yer alıyor, `Program.cs` dosyasına eklemeye hazır. Tüm adımları, hata yönetimini ve kodu açıklayıcı yorumları içerir.

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    public static void Main()
    {
        // 👉 Step 1: Initialize the OCR engine.
        var ocrEngine = new OcrEngine();

        // 👉 Step 2: Path to the PNG image you want to process.
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "text.png");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found at {imagePath}");
            return;
        }

        // 👉 Step 3: Perform OCR – this is where we **recognize png text**.
        var ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 👉 Step 4: Validate the result.
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("No recognizable text found. Try a clearer image or adjust DPI settings.");
            return;
        }

        // 👉 Step 5: Configure JsonSerializer to **write indented json**.
        var jsonOptions = new JsonSerializerOptions
        {
            WriteIndented = true // Pretty‑print the JSON.
        };

        // 👉 Step 6: Serialize the OCR result – this demonstrates **use jsonserializer c#**.
        string jsonOutput = JsonSerializer.Serialize(ocrResult, jsonOptions);

        // 👉 Step 7: Output to console (or write to a file).
        Console.WriteLine(jsonOutput);

        // Optional: Save to disk.
        string outputPath = Path.ChangeExtension(imagePath, ".json");
        File.WriteAllText(outputPath, jsonOutput);
        Console.WriteLine($"JSON saved to {outputPath}");
    }
}
```

Kodu çalıştırın, konsolu veya oluşturulan `.json` dosyasını inceleyin; çıkarılan metni güven puanlarıyla birlikte, düzenli bir şekilde **girintili** göreceksiniz.

## Sonuç

Artık **c# ocr tutorial** olarak **extract text image c#**, **recognize png text** ve `JsonSerializer` kullanarak **write indented json** nasıl yapılır gösteren sağlam bir örneğiniz var. Örnek eksiksiz, çalıştırılabilir ve gerçek dünya senaryoları için pratik ipuçları içeriyor.  

Sonraki adımlar? Aspose.OCR'ı başka bir motorla (ör. Tesseract) değiştirip `OcrResult` yapısının nasıl değiştiğini görün, ya da JSON'u OCR verilerini bir veritabanına kaydeden bir sonraki API'ye gönderin. Ayrıca **use jsonserializer c#** seçeneklerini, tarih formatlama veya enum işleme için özel dönüştürücüler gibi deneyebilirsiniz.

Kodlamaktan keyif alın ve OCR veri akışlarınız her zaman doğru olsun!  

---  

![c# ocr tutorial diyagramı](image.png "OCR akışını gösteren diyagram")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}