---
category: general
date: 2026-03-02
description: Aspose OCR kullanarak görüntüden metin çıkarırken JSON kaydetmeyi öğrenin.
  JSON dosyası yazma kodu, bitmap görüntü yükleme ipuçları ve tam C# örneği içerir.
draft: false
keywords:
- how to save json
- extract text from image
- write json file
- how to extract text
- load bitmap image
language: tr
og_description: Aspose OCR ile görüntüden metin çıkarırken JSON kaydetmeyi keşfedin.
  Tam C# kodu, JSON dosyası yazma adımları ve pratik ipuçları.
og_title: C#'ta OCR'dan JSON Nasıl Kaydedilir – Tam Programlama Öğreticisi
tags:
- C#
- OCR
- Aspose
- JSON
title: C#'ta OCR'dan JSON Nasıl Kaydedilir – Tam Adım Adım Rehber
url: /tr/net/ocr-configuration/how-to-save-json-from-ocr-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta OCR'dan JSON Nasıl Kaydedilir – Tam Adım‑Adım Kılavuz

Hiç **JSON nasıl kaydedilir** sorusunu, az önce bir resimden çektiğiniz metni içeren bir dosya olarak düşündünüz mü? Tek başınıza değilsiniz. Birçok geliştirici, *görüntüden metin çıkarma* ihtiyacıyla karşılaştığında ve bu bilgiyi düzenli bir JSON dosyası olarak saklamak zorunda kaldığında bir çıkmaza giriyor. İyi haber? Doğru parçalar bir araya getirildiğinde çözüm oldukça basit.

Bu öğreticide gerçek bir senaryoyu adım adım inceleyeceğiz: Aspose.OCR kullanarak **görüntüden metin çıkarma**, ardından **JSON dosyası yazma** ve son olarak **JSON nasıl kaydedilir** konularını ele alacağız. Ayrıca **bitmap görüntü** nesnelerini doğru şekilde nasıl yüklersiniz gösterip, karşılaşabileceğiniz birkaç uç durumu da ele alacağız. Sonunda, resmi yüklemekten kullanıma hazır bir JSON belgesi üretmeye kadar her şeyi yapan bağımsız bir C# konsol uygulamanız olacak.

## Gereksinimler

- .NET 6.0 veya üzeri (kod .NET Core ve .NET Framework ile de çalışır)
- Aspose.OCR for .NET (ücretsiz deneme NuGet paketini alabilirsiniz)
- İngilizce metin içeren bir PNG veya JPG örnek resmi
- Visual Studio, VS Code veya herhangi bir C# uyumlu IDE

Ek bir kütüphane gerekmez—sadece bitmap işleme için standart `System.Drawing` isim alanı ve serileştirme için `System.Text.Json` yeterlidir.

---

## Adım 1 – Bitmap Görüntüyü Yükleme (“load bitmap image” bölümü)

Herhangi bir OCR işlemine başlamadan önce resmi bir `Bitmap` olarak belleğe almanız gerekir. Bunu, sayfalarını okumaya başlamadan önce bir kitabı açmak gibi düşünün.

```csharp
using System.Drawing;

// Replace the placeholder with the actual path to your image file
string imagePath = @"C:\Images\sample-page.png";

// Load the image – this is the “load bitmap image” step
Bitmap bitmapImage = new Bitmap(imagePath);
```

> **İpucu:** Görüntü büyükse, performansı artırmak için önce yeniden boyutlandırmayı düşünün. OCR motoru 2 MB altında olan görüntülerde daha hızlı çalışır.

---

## Adım 2 – Aspose OCR Motorunu Yapılandırma

Bitmap hazır olduğuna göre bir `OcrEngine` nesnesine ihtiyacımız var. Bu nesne **görüntüden metin çıkarma** işlemini bilir ve isteğe bağlı olarak sınırlayıcı kutular gibi geometrik verileri de sağlayabilir.

```csharp
using Aspose.OCR;

// Create the OCR engine with English language and enable bounding boxes
OcrEngine ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,
    ExportBoundingBoxes = true // adds geometry info to the result
};
```

`ExportBoundingBoxes` özelliğini neden etkinleştirirsiniz? UI’da kelimeleri vurgulamanız gerektiğinde bu koordinatlar altın değerindedir. İhtiyacınız yoksa bayrağı `false` yapabilir ve JSON biraz daha ince olur.

---

## Adım 3 – OCR İşlemini Gerçekleştir ve Yapılandırılmış Sonucu Al

Motor yapılandırıldıktan sonra gerçek **görüntüden metin çıkarma** işlemi gerçekleşir. `RecognizeToOcrResult` metodu, tanınan metni, güven skorlarını ve isteğe bağlı düzen verilerini içeren zengin bir nesne döndürür.

```csharp
// Run OCR – this is the core “how to extract text” call
var ocrResult = ocrEngine.RecognizeToOcrResult(bitmapImage);
```

`ocrResult` değişkeni artık ihtiyacınız olan her şeyi tutuyor. Hata ayıklayıcıda incelerseniz, `Page`, `Paragraph`, `Line` ve `Word` nesnelerinin bir hiyerarşisini, her birinin `Text` özelliğiyle birlikte göreceksiniz.

---

## Adım 4 – Sonucu Biçimlendirilmiş JSON Dizesine Serileştirme

İşte **JSON nasıl kaydedilir** sihrinin gerçek başlangıcı. `System.Text.Json` kullanacağız çünkü yerleşik, hızlı ve kutudan çıkar çıkmaz güzel bir biçimlendirme (pretty printing) sunuyor.

```csharp
using System.Text.Json;

// Serialize with indentation for readability
string jsonResult = JsonSerializer.Serialize(
    ocrResult,
    new JsonSerializerOptions { WriteIndented = true }
);
```

Farklı bir adlandırma kuralına (ör. camelCase) ihtiyacınız varsa, `options` nesnesine `PropertyNamingPolicy = JsonNamingPolicy.CamelCase` eklemeniz yeterli.

---

## Adım 5 – JSON'ı Disk'e Yazma (“write json file” adımı)

Son olarak **JSON dosyası yazma** işlemini gerçekleştiriyoruz. Bu, **C# ortamında JSON nasıl kaydedilir** sorusunun somut cevabı.

```csharp
using System.IO;

// Choose where you want the JSON output
string jsonPath = @"C:\Images\sample-page.json";

// Save the JSON string – this completes the “how to save json” workflow
File.WriteAllText(jsonPath, jsonResult);
```

Bu satır çalıştıktan sonra, orijinal resminizin yanına güzel bir şekilde girintilenmiş `sample-page.json` dosyasını bulacaksınız. Herhangi bir metin editörüyle açabilir ya da başka bir servise besleyebilirsiniz—OCR veriniz artık taşınabilir.

---

## Adım 6 – Çıktıyı Doğrulama (Ne Görmelisiniz?)

Programı çalıştırdığınızda konsola kısa bir onay mesajı basılmalıdır:

```csharp
Console.WriteLine("OCR result saved as JSON.");
```

Oluşturulan JSON dosyasını açtığınızda şu benzeri bir içerik göreceksiniz:

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Hello, world!",
          "Words": [
            { "Text": "Hello,", "Confidence": 0.99 },
            { "Text": "world!", "Confidence": 0.98 }
          ]
        }
      ]
    }
  ]
}
```

`ExportBoundingBoxes` bayrağı `true` ise, her kelime ayrıca `Rectangle` koordinatlarını da içerecektir. Bu, sonraki UI çalışmalarında oldukça işe yarar.

---

## Yaygın Sorular & Uç Durumlar

### Görüntü yolu geçersiz olduğunda ne olur?

Bitmap yüklemeyi bir `try/catch` bloğuna sarın ve net bir hata mesajı gösterin:

```csharp
try
{
    Bitmap bitmapImage = new Bitmap(imagePath);
}
catch (FileNotFoundException)
{
    Console.Error.WriteLine($"Image not found: {imagePath}");
    return;
}
```

### İngilizce dışındaki diller nasıl işlenir?

Sadece `Language` özelliğini değiştirin:

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

Aspose 50'den fazla dili destekler; kaynak materyalinize uygun olanı seçin.

### `Bitmap` nesnelerini dispose etmek gerekir mi?

Evet. `Bitmap` `IDisposable` uygular, bu yüzden yerel kaynakları hızlıca serbest bırakmak için `using` ifadesi içinde kullanın.

```csharp
using (Bitmap bitmapImage = new Bitmap(imagePath))
{
    // OCR code here
}
```

### Girintisiz, sıkıştırılmış bir JSON istiyorum, ne yapmalıyım?

`JsonSerializerOptions`'ı şu şekilde değiştirin:

```csharp
new JsonSerializerOptions { WriteIndented = false }
```

Bu, dosya boyutunu azaltır—bant genişliği sınırlı senaryolar için faydalıdır.

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda, yukarıda tartışılan tüm adımları, hata yönetimini ve en iyi uygulama ipuçlarını içeren tam program yer alıyor. `Program.cs` olarak kaydedin ve komut satırından ya da IDE'nizden çalıştırın.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1 – Load the bitmap image (load bitmap image)
        // -------------------------------------------------
        string imagePath = @"C:\Images\page.png";
        string jsonPath  = @"C:\Images\page.json";

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"Error: Image file not found at {imagePath}");
            return;
        }

        using Bitmap bitmapImage = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2 – Configure the OCR engine
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            ExportBoundingBoxes = true // optional, adds geometry info
        };

        // -------------------------------------------------
        // Step 3 – Perform OCR (how to extract text)
        // -------------------------------------------------
        var ocrResult = ocrEngine.RecognizeToOcrResult(bitmapImage);

        // -------------------------------------------------
        // Step 4 – Serialize to JSON (how to save json)
        // -------------------------------------------------
        string jsonResult = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true }
        );

        // -------------------------------------------------
        // Step 5 – Write JSON file (write json file)
        // -------------------------------------------------
        try
        {
            File.WriteAllText(jsonPath, jsonResult);
            Console.WriteLine($"OCR result saved as JSON at {jsonPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Failed to write JSON file: {ex.Message}");
        }
    }
}
```

**Ne yapıyor:**  
1. Görüntünün varlığını kontrol eder.  
2. `using` bloğu ile güvenli bir şekilde yükler.  
3. OCR çalıştırarak **görüntüden metin çıkarma** yapar.  
4. Sonucu güzel bir girintili JSON dizesine serileştirir.  
5. Bu dizeyi diske kaydederek temel soru **JSON nasıl kaydedilir**'e yanıt verir.

`dotnet run` komutunu (veya Visual Studio’da F5 tuşunu) çalıştırın; dosya yazıldıktan sonra onay mesajını göreceksiniz.

---

## Sonuç

Artık OCR‑tabanlı metin çıkarımından elde edilen **JSON nasıl kaydedilir** sorusuna tam, üretim‑hazır bir tarifiniz var. Bitmap görüntüyü yüklemekten temiz bir JSON dosyası yazmaya kadar her adım, kodun “neden”ini açıklayarak anlatıldı; böylece çözümü kendi projelerinize kolayca uyarlayabilirsiniz.

Bir sonraki adım için merak edebileceğiniz konular:

- **PDF'lerden metin çıkarma**, her sayfayı önce görüntüye dönüştürerek.  
- Sınırlayıcı kutu verilerini bir WPF veya WinForms UI’da kelimeleri vurgulamak için kullanma.  
- JSON'ı dosyaya yazmak yerine doğrudan bir web API'ye akıtma (ör. `HttpClient` kullanarak).

Deneyin, seçenekleri ayarlayın ve OCR verisini inşa ettiğiniz uygulamaya güç katın. Sorularınız mı var? Yorum bırakın, iyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}