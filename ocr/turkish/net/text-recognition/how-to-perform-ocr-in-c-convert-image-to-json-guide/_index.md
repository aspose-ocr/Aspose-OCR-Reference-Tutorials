---
category: general
date: 2026-02-17
description: C#'ta OCR nasıl yapılır ve görüntüyü hızlı bir şekilde JSON'a dönüştürülür.
  Görüntülerden metin çıkarmak ve düzeni JSON olarak kaydetmek için bu C# OCR öğreticisini
  izleyin.
draft: false
keywords:
- how to perform OCR
- convert image to json
- c# ocr tutorial
- extract text image c#
- load image file c#
language: tr
og_description: C#'ta OCR nasıl yapılır? Bu rehber, bir resmi JSON'a dönüştürmeyi,
  C#'ta resimden metin çıkarmayı ve OCR için resim dosyasını yüklemeyi gösterir.
og_title: C#'ta OCR Nasıl Yapılır – Görüntüyü JSON'a Dönüştürme
tags:
- OCR
- C#
- Aspose
title: C#'ta OCR Nasıl Yapılır – Görüntüyü JSON'a Dönüştürme Rehberi
url: /tr/net/text-recognition/how-to-perform-ocr-in-c-convert-image-to-json-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta OCR Nasıl Yapılır – Görüntüyü JSON'a Dönüştürme Kılavuzu

C# kullanarak bir makbuz, fatura veya herhangi bir taranmış belgede **OCR nasıl yapılır** diye hiç merak ettiniz mi? Tek başınıza değilsiniz. Birçok geliştirici, metni *ve* düzeni koruyarak saatlerce özel ayrıştırıcılar yazmadan çıkarmaları gerektiğinde bir duvara çarpar.  

Bu öğreticide, **c# ocr tutorial** adlı tam bir örnek üzerinden tam olarak OCR nasıl yapılır, **görseli json'a dönüştürülür** ve sonucun daha sonraki analizler için nasıl kaydedilir, adım adım göstereceğiz. Sonunda, C#'ta bir görüntü dosyasını yükleyen, metni çıkaran ve koordinatlar, güven skorları ve ham metni içeren ayrıntılı bir JSON dosyası yazan, çalıştırmaya hazır bir konsol uygulamanız olacak.

## Önkoşullar — İhtiyacınız Olanlar

- .NET 6 SDK veya daha yenisi (kod .NET Core'da da çalışır)  
- Visual Studio 2022 veya tercih ettiğiniz herhangi bir editör  
- Bir Aspose OCR lisansı (ücretsiz deneme ile başlayabilirsiniz)  
- Örnek bir görüntü, örn. `receipt.png`, referans alabileceğiniz bir klasöre yerleştirilmiş  

Hepsi bu—`Aspose.OCR` dışındaki ekstra NuGet paketlerine gerek yok. Bu bileşenlere sahipseniz, hazırsınız.

## OCR Nasıl Yapılır ve JSON Çıktısı Alınır

Aspose ile **OCR nasıl yapılır** sorusunun temeli basittir: bir `OcrEngine` oluşturun, ona bir görüntü akışı verin, `Recognize` metodunu çağırın ve ardından `OcrResult`'ı JSON'a serileştirin. Şimdi adım adım inceleyelim.

### Adım 1: Aspose  OCR NuGet Paketini Yükleyin

Proje klasörünüzde terminali açın ve şu komutu çalıştırın:

```bash
dotnet add package Aspose.OCR
```

> **Pro ipucu:** En son kararlı sürüme kilitlemek için `--version` bayrağını kullanın (örnek: `23.9.0`). Bu, derlemenizin tekrarlanabilir olmasını sağlar.

### Adım 2: Konsol Proje Taslağını Oluşturun

Henüz bir projeniz yoksa, bir tane oluşturun:

```bash
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo
```

Artık **load image file c#** kodunu içerecek ve OCR sürecini başlatacak bir `Program.cs` dosyanız var.

### Adım 3: Tam OCR‑to‑JSON Kodunu Yazın

Aşağıda tam, çalıştırmaya hazır program yer alıyor. `Program.cs` dosyasına kopyalayıp yapıştırın. Her satır yorumlanmış, böylece her parçanın *neden* önemli olduğunu görebilirsiniz.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonOutput
{
    static void Main()
    {
        // ---------------------------------------------------------
        // 1️⃣  Initialize the OCR engine – this object holds
        //     language settings, recognition options, etc.
        // ---------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---------------------------------------------------------
        // 2️⃣  Load the image you want to analyze.
        //     This demonstrates **load image file c#** in a clean way.
        // ---------------------------------------------------------
        // Replace the path with the actual location of your receipt.png
        string imagePath = Path.Combine(
            Environment.CurrentDirectory, "receipt.png");
        ImageStream image = ImageStream.FromFile(imagePath);

        // ---------------------------------------------------------
        // 3️⃣  Perform the recognition.
        //     The engine returns an OcrResult containing text,
        //     confidence scores, and layout information.
        // ---------------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // ---------------------------------------------------------
        // 4️⃣  Convert the result to a detailed JSON string.
        //     This is the heart of **convert image to json**.
        // ---------------------------------------------------------
        string jsonResult = ocrResult.ToJson();

        // ---------------------------------------------------------
        // 5️⃣  Save the JSON to disk – you can later import this into
        //     databases, analytics pipelines, or UI components.
        // ---------------------------------------------------------
        string jsonPath = Path.Combine(
            Environment.CurrentDirectory, "receipt.json");
        File.WriteAllText(jsonPath, jsonResult);

        // ---------------------------------------------------------
        // 6️⃣  Let the user know we’re done.
        // ---------------------------------------------------------
        Console.WriteLine("JSON with layout saved to " + jsonPath);
    }
}
```

#### Kodun Ne Yaptığı

| Adım | Neden Önemli |
|------|--------------|
| **Initialize OcrEngine** | Varsayılan dili (İngilizce) ayarlar ve dahili modelleri hazırlar. |
| **Load image file** | `ImageStream.FromFile` kullanımı, görüntünün Aspose'un beklediği formatta okunmasını sağlar. |
| **Recognize** | Yoğun işlem—piksel analizi, karakter segmentasyonu ve sözlük taraması. |
| **ToJson** | Sınır kutuları, güven skorları ve ham metni içeren yapılandırılmış bir çıktı üretir. |
| **WriteAllText** | JSON'ı kalıcı hale getirir, böylece diğer hizmetlerle paylaşabilirsiniz. |
| **Console.WriteLine** | Anında geri bildirim verir—terminalden çalıştırırken kullanışlıdır. |

> **Dikkat:** Görüntünüz büyükse, hız ve bellek kullanımını artırmak için önce yeniden boyutlandırmayı düşünün. Aspose, `ImageStream` üzerinde çağırabileceğiniz `Resize` metodlarını sağlar.

### Adım 4: Uygulamayı Çalıştırın ve Çıktıyı Doğrulayın

Terminalden:

```bash
dotnet run
```

Şu çıktıyı görmelisiniz:

```
JSON with layout saved to C:\Path\To\OcrJsonDemo\receipt.json
```

Herhangi bir editörde `receipt.json` dosyasını açın; aşağıdakine benzer bir içerik bulacaksınız:

```json
{
  "Pages": [
    {
      "Blocks": [
        {
          "Text": "Total: $12.34",
          "Confidence": 0.98,
          "BoundingBox": { "X": 120, "Y": 340, "Width": 150, "Height": 30 }
        }
      ]
    }
  ]
}
```

Bu JSON, **extract text image c#** ve düzen meta verilerini yakalar, sonraki işleme için mükemmeldir.

## Görüntüyü JSON'a Dönüştürme – Temel Ötesi

Artık **OCR nasıl yapılır** bildiğinize göre, gerçek projelerde ihtiyaç duyabileceğiniz birkaç varyasyonu inceleyelim.

### Çoklu Sayfaları İşleme

Kaynağınız çok sayfalı bir PDF veya TIFF ise, her sayfa üzerinde basitçe döngü oluşturun:

```csharp
foreach (var pageStream in multiPageImageStreams)
{
    OcrResult result = ocrEngine.Recognize(pageStream);
    // Append each page's JSON to a master list
}
```

### Dil ve Doğruluk Özelleştirme

Aspose 40'tan fazla dili destekler. İspanyolcaya geçmek için:

```csharp
ocrEngine.Language = Language.Spanish;
```

`ocrEngine.Settings`'i ayarlayarak **auto‑rotate**, **gürültü kaldırma** veya **sözlük‑tabanlı düzeltme** gibi özellikleri etkinleştirebilir—bunun hepsi elde ettiğiniz JSON kalitesini artırır.

### JSON'ı Güzel‑Biçimlendirilmiş (Pretty‑Printed) Formatta Kaydetme

Okunabilirlik için girintili JSON tercih ediyorsanız:

```csharp
string prettyJson = ocrResult.ToJson(true); // true = formatted
File.WriteAllText(jsonPath, prettyJson);
```

## Load Image File C# – Yaygın Tuzaklar ve İpuçları

When you **load image file c#**, you might run into:

- **File not found** – Yolu mutlak olduğundan emin olun veya `Environment.CurrentDirectory` ile `Path.Combine` kullanın.  
- **Unsupported format** – Aspose PNG, JPEG, BMP, TIFF ve PDF'yi destekler. RAW formatları için önce dönüştürün.  
- **Large file memory pressure** – Yükleme sırasında küçültmek için `ImageStream.FromFile(path, maxSizeInKB)` kullanın.

Bu sorunları erken ele almak, OCR işlem hattında daha sonra ortaya çıkabilecek belirsiz istisnalardan sizi korur.

## Extract Text Image C# – Sonuçları Doğrulama

JSON'ı elde ettikten sonra sadece düz metni almak isteyebilirsiniz:

```csharp
var ocrResult = ocrEngine.Recognize(image);
string plainText = ocrResult.Text; // Simple string with line breaks
Console.WriteLine(plainText);
```

Bu kod parçacığı, **extract text image c#**'yi düzen detayları olmadan gösterir—hızlı aramalar veya günlükleme için kullanışlı.

![OCR iş akışı diyagramı – OCR nasıl yapılır, görüntüyü JSON'a dönüştürme ve metin görüntüsü çıkarma](/images/ocr-workflow.png "OCR iş akışı nasıl yapılır")

*Görsel alt metni: "OCR iş akışı diyagramı, görüntüyü JSON'a dönüştürme ve metin görüntüsü çıkarma"*  
*(Görsel bir yer tutucudur; yayınlarken gerçek bir diyagramla değiştirin.)*

## Sonuç

C#'ta **OCR nasıl yapılır** konusunu baştan sona ele aldık, **görseli JSON'a dönüştürme** yöntemini gösterdik ve **load image file c#** ve **extract text image c#** inceliklerini açıkladık. Tam kod örneği herhangi bir .NET projesine eklenmeye hazır ve JSON çıktısı ham metni ve sonraki analizler için kesin düzen verilerini sunar.

Sırada ne var? JSON'ı bir veritabanına beslemeyi, bir UI'de sınırlama kutularını görselleştirmeyi veya toplu işleme için birden fazla OCR çalıştırmasını zincirlemeyi deneyin. Ayrıca el yazısı tanıma veya barkod algılama gibi diğer Aspose özellikleriyle de deney yapabilirsiniz—her ikisi de aynı işlem hattına doğal olarak uyar.

Herhangi bir sorunla karşılaşırsanız, “Load Image File C#” bölümündeki sorun giderme ipuçlarına tekrar göz atın veya gelişmiş ayarlar için Aspose'un kapsamlı belgelerini inceleyin. Kodlamaktan keyif alın ve görüntüleri yapılandırılmış verilere dönüştürmenin tadını çıkarın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}