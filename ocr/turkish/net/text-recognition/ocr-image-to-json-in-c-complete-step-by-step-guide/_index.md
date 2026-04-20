---
category: general
date: 2026-02-11
description: C#'ta bir OCR görüntüsünü JSON'a dönüştürün. Görüntüden metin çıkarmayı,
  C#'ta görüntü dosyasını okumayı, JSON çıktısını biçimlendirmeyi ve Aspose.OCR ile
  JSON'ı güzel bir şekilde yazdırmayı öğrenin.
draft: false
keywords:
- ocr image to json
- extract text from image
- read image file c#
- format json output
- pretty print json c#
language: tr
og_description: C#'ta bir OCR görüntüsünü JSON'a dönüştürün. Bu kılavuz, görüntüden
  metin çıkarmayı, C#'ta görüntü dosyasını okumayı, JSON çıktısını biçimlendirmeyi
  ve Aspose.OCR kullanarak C#'ta JSON'ı güzel bir şekilde yazdırmayı gösterir.
og_title: C#'ta OCR görüntüyü JSON'a dönüştürme – Tam Adım Adım Kılavuz
tags:
- OCR
- C#
- JSON
title: C#'ta OCR görüntüsünü JSON'a dönüştürme – Tam Adım Adım Rehber
url: /tr/net/text-recognition/ocr-image-to-json-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#’ta Görüntüyü JSON’a OCR – Tam Adım‑Adım Kılavuz

Her zaman **ocr image to json** yapmanız gerektiğinde, hangi kütüphaneyi seçeceğinizden veya güzel formatlanmış bir sonuç almanın nasıl olacağından emin olmadınız mı? Yalnız değilsiniz. Gerçek dünyadaki birçok uygulamada—fiş tarama, kimlik doğrulama veya basit belge arşivleme—bir görüntüden metin çıkarmak ve aşağı akış hizmetlerinin tüketebileceği temiz bir JSON yükü elde etmek istersiniz.

Bu öğreticide tüm süreci adım adım inceleyeceğiz: C#’ta bir görüntü dosyasını okumaktan, metni Aspose.OCR ile çıkarmaya, motoru yapılandırarak yapılandırılmış bir JSON çıktısı istemeye ve son olarak bu JSON’u insan tarafından okunabilir şekilde güzel bir şekilde yazdırmaya kadar. Sonunda, herhangi bir .NET projesine ekleyebileceğiniz, üretim‑hazır, bağımsız bir kod parçacığına sahip olacaksınız.  

Ayrıca yaygın tuzaklara (örneğin eksik dil paketleri) değinecek ve birkaç hızlı varyasyon göstereceğiz—ör. XML çıktısına geçiş veya çok sayfalı PDF’leri işleme. Harici bir dokümantasyona ihtiyaç yok; ihtiyacınız olan her şey burada.

## İhtiyacınız Olanlar

- **.NET 6+** (kod .NET Framework 4.7+ ile de çalışır)
- **Aspose.OCR for .NET** – NuGet üzerinden kurun (`Install-Package Aspose.OCR`)
- Referans alabileceğiniz bir örnek görüntü (ör. `receipt.png`)
- C# sözdizimine temel aşinalık (eğer “Hello World” yazdıysanız, hazırsınız)

> *Pro tip:* Bir CI sunucusunda çalışıyorsanız, `AutomaticResourceDownload = true` ayarlayın; böylece Aspose dil verilerini anında indirir—elle DLL yönetimine gerek kalmaz.

## Adım 1: C#’ta Görüntü Dosyasını Oku ve OCR Motorunu Oluştur  

İlk olarak görüntüyü diskteki konumundan yüklüyoruz. `System.Drawing.Image` kullanmak kodu kısa tutar ve PNG, JPEG, BMP ve hatta çok‑sayfalı TIFF’ler için çalışır (motor varsayılan olarak ilk sayfayı seçer).

```csharp
using System.Drawing;          // For Image
using Aspose.OCR;              // Core OCR classes
using Aspose.OCR.Models;       // Language and output enums
using System.Text.Json;        // JSON parsing & pretty‑print

// 1️⃣ Configure the OCR engine – this is where we tell Aspose what language we expect
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,          // extract text from image in English
    AutomaticResourceDownload = true,        // auto‑download language packs if missing
    OutputFormat = OcrOutputFormat.Json      // ask for JSON rather than plain text
};
```

**Neden önemli:**  
- `AutomaticResourceDownload`, İngilizce dil dosyası yerel olarak bulunmadığında çalışma zamanı çöküşlerini önler.  
- `OutputFormat`’u `Json` olarak ayarlamak, motorun ham OCR sonuçlarını yapılandırılmış bir nesneye dönüştürme işini zaten yapmasını sağlar—elle string ayrıştırmaya gerek kalmaz.

## Adım 2: OCR’ı Çalıştır ve JSON Çıktısını Al  

Şimdi yüklediğimiz bitmap’i motora veriyoruz. `Recognize` metodu, JSON dizesini tutan bir `Text` özelliği içeren bir `OcrResult` döndürür.

```csharp
// 2️⃣ Load the image you want to process
using (var receiptImage = Image.FromFile(@"C:\Images\receipt.png"))
{
    // 3️⃣ Perform OCR – this call blocks until the engine finishes
    var ocrResult = ocrEngine.Recognize(receiptImage);

    // 4️⃣ The OCR engine gave us JSON straight away
    string rawJson = ocrResult.Text;
    
    // Optional: write the raw JSON to a file for debugging
    System.IO.File.WriteAllText(@"C:\Temp\ocr_raw.json", rawJson);
}
```

**Köşe durumu:** Görüntü bozuksa veya yol hatalıysa, `Image.FromFile` bir `FileNotFoundException` fırlatır. Güvenilir olmayan giriş bekliyorsanız bloğu bir `try/catch` ile sarın.

## Adım 3: JSON’u Ayrıştır ve Formatla – JSON’u Güzel Yazdır C#  

OCR motorundan gelen ham JSON sıkıştırılmış ve göz yorar. `System.Text.Json` kullanarak bunu bir `JsonDocument` içine deserialize edebilir, ardından girinti ekleyerek yeniden serialize edebiliriz.

```csharp
// 5️⃣ Parse the JSON string into a DOM-like structure
using var jsonDoc = JsonDocument.Parse(rawJson);

// 6️⃣ Pretty‑print with indentation (2 spaces by default)
string prettyJson = JsonSerializer.Serialize(
    jsonDoc.RootElement,
    new JsonSerializerOptions { WriteIndented = true });

// 7️⃣ Output to console – you could also send this to an API or a file
Console.WriteLine(prettyJson);

// 8️⃣ Save the pretty JSON for later use
System.IO.File.WriteAllText(@"C:\Temp\ocr_pretty.json", prettyJson);
```

**Gördükleriniz:**  

```json
{
  "Lines": [
    {
      "Text": "Store Name",
      "BoundingBox": { "X": 12, "Y": 5, "Width": 150, "Height": 20 }
    },
    {
      "Text": "Total: $23.45",
      "BoundingBox": { "X": 12, "Y": 200, "Width": 100, "Height": 20 }
    }
  ],
  "Language": "English",
  "Confidence": 0.96
}
```

JSON artık satır‑satır metin, sınırlama kutuları, tespit edilen dil ve bir güven puanı içeriyor—alt akış analizlerine veya bir UI bileşenine beslemek için mükemmel.

## Adım 4: Bonus – Çıktı Formatını veya Dili Değiştirme  

Eğer **format json output**’u XML olarak almak ya da İspanyolca bir fişi OCRlamak isterseniz, sadece motor konfigürasyonunu değiştirin:

```csharp
ocrEngine.Language = OcrLanguage.Spanish;          // extract text from image in Spanish
ocrEngine.OutputFormat = OcrOutputFormat.Xml;     // ask for XML instead of JSON
```

Kodun geri kalanı aynı kalır; sadece ayrıştırma adımını değiştirirsiniz (XML için `XmlDocument` kullanın).

## Tam Çalışan Örnek  

Her şeyi bir araya getirerek, bir konsol uygulamasına kopyalayıp‑yapıştırabileceğiniz tek bir dosya:

```csharp
// ---------------------------------------------------------------
// ocr_image_to_json_demo.cs
// ---------------------------------------------------------------
using System;
using System.Drawing;
using System.Text.Json;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Configure OCR engine
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            AutomaticResourceDownload = true,
            OutputFormat = OcrOutputFormat.Json
        };

        // Path to your image – adjust as needed
        string imagePath = @"C:\Images\receipt.png";

        try
        {
            using (var receiptImage = Image.FromFile(imagePath))
            {
                var ocrResult = ocrEngine.Recognize(receiptImage);
                string rawJson = ocrResult.Text;

                // Parse & pretty‑print
                using var jsonDoc = JsonDocument.Parse(rawJson);
                string prettyJson = JsonSerializer.Serialize(
                    jsonDoc.RootElement,
                    new JsonSerializerOptions { WriteIndented = true });

                Console.WriteLine("=== Pretty‑Printed OCR JSON ===");
                Console.WriteLine(prettyJson);

                // Optional: write to file
                System.IO.File.WriteAllText(@"C:\Temp\ocr_pretty.json", prettyJson);
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Error processing image: {ex.Message}");
        }
    }
}
```

Bu programı çalıştırdığınızda, konsola güzel girintili bir JSON yükü yazdırır ve `C:\Temp\ocr_pretty.json` konumuna kaydeder. `try/catch` bloğu, görüntü okunamazsa bile sessiz bir çökme yerine net bir hata mesajı almanızı sağlar.

## Yaygın Sorular & Tuzaklar  

- **OCR boş metin döndürürse ne olur?**  
  Genellikle bu, görüntünün çok gürültülü olduğu veya dilin eşleşmediği anlamına gelir. Görüntü kontrastını artırmayı veya `Language`’i `AutoDetect` olarak değiştirmeyi deneyin.  

- **Bir döngü içinde birden fazla görüntüyü işleyebilir miyim?**  
  Kesinlikle. `using (var img = Image.FromFile(...))` bloğunu `foreach (var file in Directory.GetFiles(...))` döngüsü içine sarın ve her `prettyJson` değerini bir listeye toplayın ya da ayrı dosyalara yazın.  

- **JSON şeması stabil mi?**  
  Aspose, `Json` çıktı formatı için geriye dönük uyumluluğu garanti eder, ancak belirli bir API sürümüne hedefleniyorsanız yanıt içindeki `Version` özniteliğini her zaman kontrol edin.  

- **Aspose.OCR için bir lisansa ihtiyacım var mı?**  
  Ücretsiz değerlendirme anahtarı 100 sayfaya kadar çalışır. Üretim ortamı için bir lisans satın alın ve `License license = new License(); license.SetLicense("Aspose.OCR.lic");` kodu ile ayarlayın.

## Sonuç  

Artık C#’ta **ocr image to json** için **tam, bağımsız bir çözüm** elinizde. Görüntü dosyasını okuyarak, OCR motorunu yapılandırarak, JSON çıktısı isteyerek ve bunu güzel bir şekilde yazdırarak, metin çıkarımını herhangi bir .NET servisine string hack’leriyle uğraşmadan entegre edebilirsiniz.  

Bundan sonra **extract text from image** konusunu diğer dosya tipleri (PDF, çok‑sayfalı TIFF) için keşfedebilir, farklı dillerle deney yapabilir veya JSON’u analiz için bir NoSQL depoya yönlendirebilirsiniz. Sınır yok—sadece hataları nazikçe ele almayı ve ölçeklendikçe lisans durumunu göz önünde bulundurmayı unutmayın.

Kodlamaktan keyif alın, OCR boru hatlarınız her zaman doğru sonuç versin!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}