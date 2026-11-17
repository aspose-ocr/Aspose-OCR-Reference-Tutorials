---
category: general
date: 2026-03-17
description: C#'ta OCR sonuçlarından JSON ayrıştırmayı öğrenin. Bu öğreticide metin
  çıkarma, OCR için görüntü yükleme, OCR tanıma çalıştırma ve OCR motorunu C#'ta verimli
  bir şekilde kullanma konuları ele alınmaktadır.
draft: false
keywords:
- how to parse json
- how to extract text
- load image for OCR
- run OCR recognition
- use OCR engine C#
language: tr
og_description: C#'ta OCR çıktısından JSON nasıl ayrıştırılır. Metni çıkarmak, OCR
  için resmi yüklemek, OCR tanımasını çalıştırmak ve OCR motorunu C#'ta kullanmak
  için rehberimizi izleyin.
og_title: C# OCR Motoru ile JSON Nasıl Ayrıştırılır – Tam Öğretici
tags:
- C#
- OCR
- JSON
- Image Processing
title: OCR Motoru C# ile JSON Nasıl Ayrıştırılır – Tam Adım Adım Kılavuz
url: /tr/net/text-recognition/how-to-parse-json-with-ocr-engine-c-complete-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Engine C# ile JSON Nasıl Ayrıştırılır – Tam Adım‑Adım Kılavuz

Bir OCR motorundan doğrudan gelen **how to parse json**'ı merak ettiniz mi? Yalnız değilsiniz. Çoğu geliştirici aynı sorunu yaşıyor—ham JSON alıp, güven puanları ya da gerçek metin gibi faydalı parçaları nasıl çıkaracağını belirlemek. Bu kılavuzda bir görüntüyü OCR için yüklemeyi, OCR tanımasını çalıştırmayı ve sonunda **how to parse json**'ı temiz ve sürdürülebilir bir şekilde nasıl yapacağımızı adım adım göstereceğiz.

Bu eğitim sonunda şunları yapabilecek olacaksınız:

* Sadece birkaç satır kodla OCR için bir görüntüyü yükleyebileceksiniz.  
* C# OCR motoru kullanarak OCR tanımasını çalıştırabileceksiniz.  
* **How to extract text** ve JSON yükünden diğer meta verileri çıkarabileceksiniz.  
* Yaygın kenar durumlarını (eksik alanlar, beklenmeyen formatlar) çökmeden ele alabileceksiniz.

Harici bir dokümantasyona gerek yok—gereken her şey burada.

## Önkoşullar

Başlamadan önce, şunların olduğundan emin olun:

* .NET 6.0 veya daha yeni bir sürüm (kod .NET Framework 4.7+ üzerinde de derlenir).  
* Kullandığınız OCR kütüphanesine bir referans (örnek, varsayımsal bir `OcrEngine` sınıfı kullanıyor).  
* `Newtonsoft.Json` NuGet paketi JSON işleme için (`Install-Package Newtonsoft.Json`).  
* Uygulamanızın okuyabileceği bir yerde bulunan bir görüntü dosyası (ör. `passport.png`).

> **Pro tip:** Eğer ticari bir OCR SDK'sı kullanıyorsanız, JSON çıktı formatının etkin olduğundan emin olun—çoğu satıcı bunu `ocrEngine.Config.OutputFormat` gibi bir yapılandırma özelliği aracılığıyla sunar.

## Adım 1 – OCR Motorunu Oluşturma ve Yapılandırma (Ana Anahtar Kelime Eylemde)

İlk yapmanız gereken OCR motorunu örneklemek ve ona JSON döndürmesini söylemektir. İşte **how to parse json** ifadesinin kodumuzda ilk kez göründüğü yer, çünkü motor bize daha sonra ayrıştıracağımız bir JSON dizesi verecek.

```csharp
using System;
using Newtonsoft.Json.Linq;   // For JSON parsing
// Assume OcrEngine, OutputFormat, and ImageStream live in the OCR SDK namespace
using OcrSdk;                  // <-- replace with the real namespace

// Step 1: Create an OCR engine instance and set JSON output
var ocrEngine = new OcrEngine();
ocrEngine.Config.OutputFormat = OutputFormat.Json;
```

**Neden önemli:** `OutputFormat`'ı `Json` olarak ayarlamak, yanıtın tanınan metni **ve** güven puanları gibi faydalı meta verileri içermesini sağlar. Bu adımı atlayarsanız sadece düz metin alırsınız ve **how to parse json** anlamsız bir hal alır.

## Adım 2 – OCR için Görüntüyü Yükleme

Şimdi analiz etmek istediğimiz resmi yüklüyoruz. Bu, ikincil anahtar kelime **load image for OCR**'un parladığı tam noktadır.

```csharp
// Step 2: Load the image you want to recognize
// Make sure the path points to a real file; otherwise an exception is thrown.
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY\passport.png");
```

> **Dosya yoksa ne olur?** Çağırmayı bir `try/catch` bloğuna sarın ve dostça bir mesaj gösterin—uygulamanız çökmez ve kullanıcılar neyin yanlış gittiğini bilir.

## Adım 3 – OCR Tanımasını Çalıştırma

Motor hazır ve görüntü yüklendiğinde, bir sonraki mantıklı adım tanıma sürecini çalıştırmaktır. Bu, ikincil anahtar kelime **run OCR recognition**'ı karşılar.

```csharp
// Step 3: Execute OCR and get the raw result object
var ocrResult = ocrEngine.Recognize();
```

`ocrResult.Text` özelliği artık bir JSON dizesi içeriyor. Konsola yazdırırsanız şöyle bir şey görürsünüz:

```json
{
  "OverallConfidence": 0.92,
  "Pages": [
    {
      "Text": "John Doe\nPassport No: 123456789",
      "Confidence": 0.95
    }
  ]
}
```

## Adım 4 – JSON'dan Metin (ve Diğer Alanlar) Nasıl Çıkarılır

İşte eğitimin kalbi: OCR yükünden **how to parse json** ve **how to extract text**. Esnekliği nedeniyle `Newtonsoft.Json.Linq.JObject` kullanacağız.

```csharp
// Step 4: Output the raw JSON (optional, helps debugging)
Console.WriteLine("Raw OCR JSON:");
Console.WriteLine(ocrResult.Text);
Console.WriteLine();

// Step 5: Parse the JSON into a JObject
JObject jsonObject = JObject.Parse(ocrResult.Text);

// Extract the overall confidence score
var overallConfidence = jsonObject["OverallConfidence"]?.Value<double>() ?? 0.0;
Console.WriteLine($"Overall confidence: {overallConfidence:P0}");

// Extract the text from the first page (how to extract text)
string pageText = jsonObject["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;
Console.WriteLine("Extracted text:");
Console.WriteLine(pageText);
```

**Neden `JObject` kullanmalı?** Tam bir C# model sınıfı tanımlamadan JSON ağacında güvenli bir şekilde gezinmenizi sağlar. Null‑koşullu (`?.`) operatörleri, OCR motoru bir alanı atladığında `NullReferenceException` hatasından korunmanıza yardımcı olur.

### Kenar Durumlarını Ele Alma

* **Eksik alanlar:** `?.Value<T>() ?? default` deseni mantıklı bir varsayılan değer döndürür.  
* **Birden fazla sayfa:** Birden fazla sayfa bekliyorsanız `jsonObject["Pages"]` üzerinde döngü yapın.  
* **Sayısal olmayan güven:** SDK bazen bir string döndürürse `double.TryParse` kullanın.

## Adım 5 – Hepsini Yeniden Kullanılabilir Bir Metoda Sarmak

Aynı tekrarlayan kodu kopyalayıp yapıştırmaktan kaçınmak için tüm akışı bir yardımcı metoda kapsülle. Bu aynı zamanda **use OCR engine C#**'ı temiz ve yeniden kullanılabilir bir şekilde gösterir.

```csharp
public static void RunOcrAndParseJson(string imagePath)
{
    // 1️⃣ Create engine & set JSON output
    var engine = new OcrEngine();
    engine.Config.OutputFormat = OutputFormat.Json;

    // 2️⃣ Load image (load image for OCR)
    engine.Image = ImageStream.FromFile(imagePath);

    // 3️⃣ Run OCR (run OCR recognition)
    var result = engine.Recognize();

    // 4️⃣ Show raw JSON (optional)
    Console.WriteLine("=== Raw JSON ===");
    Console.WriteLine(result.Text);
    Console.WriteLine();

    // 5️⃣ Parse JSON (how to parse json)
    JObject obj = JObject.Parse(result.Text);

    // 6️⃣ Extract useful data (how to extract text)
    double confidence = obj["OverallConfidence"]?.Value<double>() ?? 0.0;
    string text = obj["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;

    Console.WriteLine($"Overall confidence: {confidence:P0}");
    Console.WriteLine("Extracted text:");
    Console.WriteLine(text);
}
```

Artık `RunOcrAndParseJson(@"C:\Images\passport.png");` çağrısını `Main` içinde ya da uygulamanızın başka bir bölümünden yapabilirsiniz.

## Tam Çalışan Örnek

Aşağıda, yeni bir `.csproj` içine kopyalayıp yapıştırabileceğiniz, tam ve bağımsız bir konsol programı bulunuyor. Tartıştığımız tüm parçaları ve biraz hata yönetimini içerir.

```csharp
// File: Program.cs
using System;
using Newtonsoft.Json.Linq;
using OcrSdk;               // Replace with the actual namespace of your OCR library

class Program
{
    static void Main()
    {
        try
        {
            // Adjust the path to point at a real image on your machine
            string imagePath = @"YOUR_DIRECTORY\passport.png";

            RunOcrAndParseJson(imagePath);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Unexpected error: {ex.Message}");
        }
    }

    /// <summary>
    /// Demonstrates how to parse JSON returned by an OCR engine,
    /// and how to extract text, confidence, and other metadata.
    /// </summary>
    /// <param name="imagePath">Full path to the image file.</param>
    public static void RunOcrAndParseJson(string imagePath)
    {
        // 1️⃣ Initialize OCR engine (use OCR engine C#)
        var engine = new OcrEngine();
        engine.Config.OutputFormat = OutputFormat.Json;

        // 2️⃣ Load image for OCR
        engine.Image = ImageStream.FromFile(imagePath);

        // 3️⃣ Run OCR recognition
        var result = engine.Recognize();

        // 4️⃣ Print raw JSON (helps debugging)
        Console.WriteLine("=== Raw OCR JSON ===");
        Console.WriteLine(result.Text);
        Console.WriteLine();

        // 5️⃣ Parse JSON (how to parse json)
        JObject json = JObject.Parse(result.Text);

        // 6️⃣ Extract overall confidence
        double overallConf = json["OverallConfidence"]?.Value<double>() ?? 0.0;
        Console.WriteLine($"Overall confidence: {overallConf:P0}");

        // 7️⃣ Extract text from first page (how to extract text)
        string firstPageText = json["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(firstPageText);
    }
}
```

**Beklenen çıktı** (OCR başarılı olduğunu varsayarsak):

```
=== Raw OCR JSON ===
{
  "OverallConfidence": 0.92,
  "Pages": [
    {
      "Text": "John Doe\nPassport No: 123456789",
      "Confidence": 0.95
    }
  ]
}

Overall confidence: 92%
=== Extracted Text ===
John Doe
Passport No: 123456789
```

Görüntü okunamazsa, SDK bir istisna fırlatır ve bunu `Main` içinde yakalarız, çökmeden dostça bir hata mesajı yazdırırız.

## Sıkça Sorulan Sorular (SSS)

**S: OCR motoru bir sayfa dizisi döndürürse ne olur?**  
C: `json["Pages"]` üzerinde döngü yapın ve her `["Text"]` değerini birleştirin, ya da kullanım durumunuza göre ayrı ayrı işleyin.

**S: JSON'u tiplenmiş bir C# sınıfına serileştirebilir miyim?**  
C: Kesinlikle. JSON şemasına uyan bir sınıf yapısı tanımlayın ve `JsonConvert.DeserializeObject<YourRootClass>(result.Text)` kullanın. Bu, derleme‑zamanı güvenliği sağlar ancak modeli SDK'nın çıktısıyla senkronize tutmanız gerekir.

**S: Bu async OCR API'leriyle çalışır mı?**  
C: Evet. `engine.Recognize()` ifadesini `await engine.RecognizeAsync()` ile değiştirin ve `RunOcrAndParseJson` metodunu `async Task` yapın. JSON ayrıştırma kısmı aynı kalır.

**S: JSON'u daha sonra analiz için bir dosyaya nasıl kaydederim?**  
C: `result.Text` alındıktan sonra `File.WriteAllText(@"output.json", result.Text);` çağırın. Ardından `JObject.Parse(File.ReadAllText(...))` ile yeniden yükleyebilirsiniz.

## Sonraki

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}