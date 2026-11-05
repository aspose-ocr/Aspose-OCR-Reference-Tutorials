---
category: general
date: 2026-02-09
description: C#'ta OCR yaparak görüntüden metin çıkarmayı, PNG'den metin tanımayı
  ve JSON dosyası yazmayı hızlı bir şekilde öğrenin.
draft: false
keywords:
- how to perform OCR
- extract text from image
- recognize text from png
- write json file c#
language: tr
og_description: C#'ta OCR nasıl yapılır? Görüntüden metin çıkarmak, PNG'den metin
  tanımak ve C#'ta JSON dosyasını verimli bir şekilde yazmak için bu adım adım kılavuzu
  izleyin.
og_title: C#'ta OCR Nasıl Yapılır – Metni Çıkar ve JSON Yaz
tags:
- OCR
- C#
- Aspose
- JSON
title: C#'ta OCR Nasıl Yapılır – Metni Çıkar ve JSON Yaz
url: /tr/net/text-recognition/how-to-perform-ocr-in-c-extract-text-and-write-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta OCR Nasıl Yapılır – Tam Kılavuz

C#'ta OCR yapmak, **görüntüden metin çıkarma** dosyalarına ihtiyaç duyduğunuzda yaygın bir engeldir. Bu kılavuzda PNG'den metin tanımayı, ayrıntılı sonucu bir JSON dizesine dışa aktarmayı ve sonunda **write JSON file C#** tarzında kaydetmeyi adım adım göstereceğiz. Hiç taranmış bir formun önünde durup bu karalamaları aranabilir metne nasıl dönüştürebileceğinizi merak ettiniz mi? Yalnız değilsiniz; birçok geliştirici bu sorunu erken aşamalarda yaşar.

Aspose.OCR kütüphanesini kullanacağız çünkü kutudan çıkar çıkmaz sembol bazında güven puanı sağlar ve .NET 6+ projeleriyle sorunsuz çalışır. Bu öğreticinin sonunda, bir PNG yükleyen, her karakteri çıkaran ve bir veritabanına ya da bir AI modeline besleyebileceğiniz düzenli bir JSON dosyası kaydeden, çalıştırmaya hazır bir konsol uygulamanız olacak. “belgelere bak” gibi gizemli kısayollar yok—sadece bağımsız bir çözüm.

## Gereksinimler

- **.NET 6 SDK** (veya daha yeni) – yazım anındaki mevcut LTS sürümü.
- **Aspose.OCR for .NET** NuGet paketi – `Install-Package Aspose.OCR`.
- Tarama yapmak istediğiniz bir PNG görüntüsü (ör. `form.png`).  
- Bir IDE veya editör – Visual Studio, VS Code, Rider – rahat olduğunuz herhangi bir şey.

Hepsi bu. Bu parçalar elinizdeyse, hazırsınız.

![OCR Nasıl Yapılır örneği](ocr-example.png "C#'ta OCR Nasıl Yapılır")

*Görsel alt metni: C# konsol uygulamasının bir PNG işlediğini gösteren OCR nasıl yapılır illüstrasyonu.*

## Adım 1: Projeyi Kurun ve Bağımlılıkları Ekleyin

İlk olarak, yeni bir konsol projesi oluşturun ve Aspose OCR kütüphanesini ekleyin.

```csharp
// Create a new console app (run in terminal)
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo

// Add Aspose.OCR NuGet package
dotnet add package Aspose.OCR
```

> **Pro tip:** Hedef çerçeveyi açıkça kilitlemek istiyorsanız `--framework net6.0` bayrağını kullanın.

Bu adımın önemi: NuGet paketi, reliance edeceğimiz `OcrEngine`, `ImageStream` ve `JsonExporter` sınıflarını içerir. Onsuz, derleyici “OCR”un ne olduğunu bilemez.

## Adım 2: Çekirdek OCR Mantığını Yazın

`Program.cs` dosyasını açın (veya yeni bir dosya oluşturun) ve içeriğini aşağıdakilerle değiştirin. Her bölüm yorumlanmıştır, böylece neden orada olduğunu görebilirsiniz.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Export;
using System;

namespace OcrJsonDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Initialize the OCR engine – this prepares the
            //    internal models and allocates native resources.
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // 2️⃣ Load the image you want to process.
            //    Replace the path with your own PNG file.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/form.png";
            ImageStream image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // 3️⃣ Perform OCR recognition – the heavy lifting.
            //    The result includes text, per‑symbol confidence,
            //    and layout information.
            // -------------------------------------------------
            RecognitionResult ocrResult = ocrEngine.Recognize(image);

            // -------------------------------------------------
            // 4️⃣ Export the result to a JSON string.
            //    JsonExporter respects the confidence values.
            // -------------------------------------------------
            JsonExporter jsonExporter = new JsonExporter();
            string jsonContent = jsonExporter.ExportToString(ocrResult);

            // -------------------------------------------------
            // 5️⃣ Write the JSON to disk – this is how we
            //    **write JSON file C#** style.
            // -------------------------------------------------
            string jsonPath = @"YOUR_DIRECTORY/form.json";
            System.IO.File.WriteAllText(jsonPath, jsonContent);

            // -------------------------------------------------
            // 6️⃣ Let the user know we succeeded.
            // -------------------------------------------------
            Console.WriteLine($"JSON file saved successfully at {jsonPath}");
        }
    }
}
```

### Her Parçanın Neden Önemli Olduğu

- **OcrEngine**: İşlemin beyni gibi düşünün. Dil modellerini yükler ve çıkarım hattını kurar.
- **ImageStream.FromFile**: Herhangi bir PNG, JPEG, BMP vb. dosyayı işler. Dosya‑I/O inceliklerini soyutlar.
- **RecognitionResult**: Ham metni ve güven puanlarını tutar. Bu, sonraki doğrulama için ihtiyacınız olan ayrıntılı veriyi alacağınız yerdir.
- **JsonExporter**: Zengin `RecognitionResult`'ı temiz bir JSON yüküne dönüştürür, API'ler için mükemmeldir.
- **File.WriteAllText**: Ek bağımlılıklar olmadan **write JSON file C#** yapmanın basit .NET yoludur.

## Adım 3: Uygulamayı Çalıştırın ve Çıktıyı Doğrulayın

Programı derleyin ve çalıştırın:

```bash
dotnet run
```

Aşağıdaki gibi bir konsol mesajı görmelisiniz:

```
JSON file saved successfully at YOUR_DIRECTORY/form.json
```

`form.json` dosyasını açın – şöyle bir şey bulacaksınız:

```json
{
  "Text": "Sample Form\nName: John Doe\nDate: 2026-02-09",
  "Symbols": [
    { "Char": "S", "Confidence": 0.99, "X": 12, "Y": 8 },
    { "Char": "a", "Confidence": 0.98, "X": 22, "Y": 8 },
    // … more symbols …
  ]
}
```

**extract text from image** adımı başarılı oldu ve artık her karakterin makine‑okunur bir JSON temsiline sahipsiniz.

## Adım 4: Yaygın Kenar Durumlarını Ele Alın

### Eksik veya Bozuk Dosyalar

PNG yolu yanlışsa, `ImageStream.FromFile` bir `FileNotFoundException` fırlatır. Yükleme kodunu bir try‑catch bloğuna sarın:

```csharp
try
{
    ImageStream image = ImageStream.FromFile(imagePath);
}
catch (FileNotFoundException ex)
{
    Console.Error.WriteLine($"Could not find image: {ex.Message}");
    return;
}
```

### Düşük Güven Puanları

Bazen OCR, gürültülü taramalarda düşük güven puanı döndürür. Dışa aktarmadan önce sembolleri filtreleyebilirsiniz:

```csharp
ocrResult.Symbols.RemoveAll(s => s.Confidence < 0.6);
```

Bu, JSON'un yalnızca makul derecede güvenilir karakterleri içermesini sağlar—veriyi sonraki doğrulama hatlarına beslerken faydalıdır.

### Büyük Dosyalar ve Bellek

Çok megabaytlık bir PNG işlemek bellek kullanımını artırabilir. Görüntüyü parçalar halinde akış olarak işlemeyi veya UI'nin yanıt vermesini sağlamak için `OcrEngine.RecognizeAsync` (daha yeni Aspose sürümlerinde mevcut) kullanmayı düşünün.

## Adım 5: Çözümü Genişletin (İsteğe Bağlı)

- **Batch processing**: PNG dizinindeki dosyalar üzerinde döngü yapın ve her dosya için eşleşen bir JSON oluşturun.
- **Database storage**: JSON'u daha sonraki analizler için bir SQL `NVARCHAR(MAX)` sütununa ekleyin.
- **Language selection**: İngilizce dışı destek gerekiyorsa `ocrEngine.Language = OcrLanguage.Spanish;` ayarlayın.

Bu tüm uzantılar, oluşturduğumuz aynı **how to perform OCR** desenini izler—başlat, tanı, dışa aktar ve kalıcı hale getir.

## Sıkça Sorulan Sorular

**S: Bu JPG veya TIFF ile çalışır mı?**  
C: Kesinlikle. `ImageStream.FromFile` formatı otomatik algılar, bu yüzden PNG'yi desteklenen herhangi bir raster görüntüyle değiştirebilirsiniz.

**S: PDF'den metin çıkarmam gerekirse ne yapmalıyım?**  
C: Önce her PDF sayfasını bir görüntüye dönüştürün (ör. `Aspose.PDF` kullanarak) ve ardından PNG'yi burada açıklanan OCR akışına besleyin.

**S: OCR sonucunu JSON yerine XML olarak alabilir miyim?**  
C: Evet. Aspose.OCR ayrıca bir `XmlExporter` da sunar. `JsonExporter`'ı `XmlExporter` ile değiştirin ve dosya uzantısını ayarlayın.

## Sonuç

Başlangıçtan sona kadar C#'ta **how to perform OCR** sürecini gösterdik, **extract text from image**, **recognize text from PNG** ve **write JSON file C#** nasıl yapılacağını sorunsuz bir şekilde gösterdik. Tam, çalıştırılabilir örnek yukarıdaki kod parçacıklarında yer alıyor ve artık her adımın nedenini anlıyorsunuz—motoru başlatma, kenar durumlarını ele alma ve sonuçları kalıcı hale getirme.

Sonraki adımda, toplu OCR boru hatlarını keşfedebilir, JSON çıktısını Azure Cognitive Search ile entegre edebilir veya özel dil modelleriyle deney yapabilirsiniz. C#'ta OCR temellerini kavradıktan sonra sınır yok.

Herhangi bir sorunla karşılaştıysanız veya daha fazla uzantı için fikirleriniz varsa, aşağıya bir yorum bırakın. Kodlamaktan keyif alın ve o pikselli taramaları temiz, aranabilir verilere dönüştürmenin tadını çıkarın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}