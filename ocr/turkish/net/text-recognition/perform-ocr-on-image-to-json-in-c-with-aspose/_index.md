---
category: general
date: 2026-04-08
description: Aspose OCR kullanarak bir görüntüde OCR nasıl yapılır ve C# ile JSON
  dosyası nasıl yazılır öğrenin. Bu Aspose OCR C# öğreticisi, güven değerleriyle birlikte
  OCR görüntüsünün JSON’a dönüştürülmesini gösterir.
draft: false
keywords:
- perform OCR on image
- write JSON file C#
- OCR image to JSON
- Aspose OCR C# tutorial
language: tr
og_description: Görüntü üzerinde OCR gerçekleştirip sonuçları C#’ta bir JSON dosyasına
  aktarın. Bu öğretici, güven puanları dahil olmak üzere tam Aspose OCR C# iş akışını
  kapsar.
og_title: C#'ta Görüntüden JSON'a OCR Yapın – Aspose OCR Rehberi
tags:
- Aspose
- OCR
- C#
- JSON
title: Aspose ile C#'ta Görüntüden JSON'a OCR Yapın
url: /tr/net/text-recognition/perform-ocr-on-image-to-json-in-c-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile Aspose Kullanarak Görüntüyü JSON'a OCR Yapma

Hiç **görüntü dosyaları üzerinde OCR** yapmak istediğinizde sonuçları yapılandırılmış bir formata nasıl aktaracağınızı merak ettiniz mi? Yalnız değilsiniz—geliştiriciler sık sık “Taranmış bir resmi kullanılabilir verilere nasıl dönüştürebilirim?” sorusunu sorar. İyi haber şu ki Aspose.OCR bu işi çocuk oyuncağı haline getiriyor ve **write JSON file C#**‑style olarak güven puanlarını da içeren bir JSON dosyası oluşturabiliyorsunuz.

Bu rehberde, bir resmi yüklemekten tanınan metni JSON olarak dışa aktarmaya kadar her şeyi kapsayan eksiksiz bir **aspose OCR C# tutorial** üzerinden geçeceğiz. Sonunda **perform OCR on image** yapan, çıktıyı JSON’a (güven değerleri dahil) dönüştüren ve tek bir satır kodla kaydeden çalıştırılabilir bir konsol uygulamanız olacak. Gizli adımlar, harici betikler yok—sadece saf C#.

## Prerequisites

İlerlemeye başlamadan önce şunların yüklü olduğundan emin olun:

- .NET 6.0 SDK veya daha yeni bir sürüm (kod .NET Core ve .NET Framework ile de çalışır)
- Visual Studio 2022 (ya da tercih ettiğiniz başka bir editör)
- Geçerli bir **Aspose.OCR for .NET** lisansı veya ücretsiz geçici bir lisans (deneme sürümü test için yeterli)
- İşlemek istediğiniz bir görüntü dosyası (`input.png`) (herhangi bir yaygın format—PNG, JPG, BMP—olabilir)

Hepsi bu kadar. Eğer bunlardan birini eksikse şimdi temin edin; öğreticinin geri kalanı bu bileşenlerin zaten kurulu olduğunu varsayar.

## Step 1: Install the Aspose.OCR NuGet Package

İlk iş olarak kütüphaneyi projenize ekleyin. Proje klasöründe bir terminal açın ve şu komutu çalıştırın:

```bash
dotnet add package Aspose.OCR
```

Bu, en son sürümü (Nisan 2026 itibarıyla 23.12) indirir ve gerekli DLL’leri `bin` klasörüne ekler. Ek bir yapılandırma gerekmez.

## Step 2: Initialize the OCR Engine (Perform OCR on Image)

Şimdi bir `OcrEngine` örneği oluşturup hangi dili kullanacağını belirtiyoruz. İngilizce (`"en"`) en yaygın dil, ancak `"fr"`, `"de"` ya da desteklenen başka bir dil ile değiştirebilirsiniz.

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Path to your input image – change as needed
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        // Path where the JSON will be saved
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // Step 2: Initialize the OCR engine – this is where we **perform OCR on image**
        var ocrEngine = new OcrEngine
        {
            Language = "en"               // Set language; you can use ISO‑639‑1 codes
        };

        // Optional: tweak recognition options (speed vs. accuracy)
        // ocrEngine.RecognitionMode = RecognitionMode.LargeText; // Uncomment for large blocks
```

**Burada neden başlatıyoruz:** `OcrEngine`, tanıma süreci için gereken tüm yapılandırmayı tutar. Dili önceden ayarlamak, motorun doğru karakter setini kullanmasını sağlar ve doğruluğu büyük ölçüde artırır.

## Step 3: Recognize the Image and Capture Confidence

Motor hazır olduğunda görüntü dosyasını ona veriyoruz. `RecognizeImage` metodu, çıkarılan metni ve her kelime için bir güven puanı içeren bir `OcrResult` nesnesi döndürür.

```csharp
        // Step 3: Perform OCR on the image file
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        // Verify that the result is not null
        if (ocrResult == null)
        {
            Console.WriteLine("OCR failed – check the file path and format.");
            return;
        }

        // For debugging: print the plain text to the console
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
```

**Arka planda neler oluyor?** Aspose, her piksel bloğunu analiz eden, dil modeline karşı eşleştiren ve her kelime için (0‑100) bir güven değeri ekleyen sinir ağı tabanlı bir tanıyıcı çalıştırır.

## Step 4: Convert the Result to JSON (OCR Image to JSON)

Aspose dönüşümü zahmetsiz hâle getirir. `includeConfidence: true` parametresini geçirerek aşağıdaki gibi bir JSON yükü elde ederiz:

```json
{
  "Text": "Hello world",
  "Words": [
    { "Value": "Hello", "Confidence": 97.3 },
    { "Value": "world", "Confidence": 95.8 }
  ]
}
```

JSON dizesini üreten kod ise şu şekildedir:

```csharp
        // Step 4: Convert OCR result to JSON, including confidence values
        string jsonResult = ocrResult.ToJson(includeConfidence: true);
```

**Güven değerini neden ekliyoruz?** Veriyi sonraki süreçlere (ör. doğrulama, UI vurgulama) beslemeyi planlıyorsanız, hangi kelimelerin şüpheli olduğunu bilmek, kullanıcıdan onay istemeniz gerekip gerekmediğine karar vermenizi sağlar.

## Step 5: Write the JSON File C#‑Style

Şimdi **write JSON file C#** işlemini gerçekleştiriyoruz. `File.WriteAllText` metodu atomiktir ve platformlar arası çalışır; bu da konsol uygulamaları için mükemmeldir.

```csharp
        // Step 5: Save the JSON output to a file
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

İşte tüm iş akışı—beş kısa adımda **perform OCR on image**, çıktıyı JSON’a dönüştürme ve kalıcı hale getirme.

## Full Working Example

Aşağıda `Program.cs` dosyasına kopyalayıp yapıştırabileceğiniz tam program yer alıyor. `input.png` dosyasının derlenmiş ikiliyle aynı klasörde olduğundan emin olun ya da yolları buna göre ayarlayın.

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------------
        // 1️⃣ Set up file locations (feel free to change paths)
        // -------------------------------------------------------
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // -------------------------------------------------------
        // 2️⃣ Initialize the OCR engine – this is where we **perform OCR on image**
        // -------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Language = "en" // English – replace with "fr", "es", etc. as needed
        };

        // -------------------------------------------------------
        // 3️⃣ Recognize the image and obtain confidence values
        // -------------------------------------------------------
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        if (ocrResult == null)
        {
            Console.WriteLine("❌ OCR failed – verify the image path and format.");
            return;
        }

        // Show plain text (optional)
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine();

        // -------------------------------------------------------
        // 4️⃣ Convert the result to JSON – **OCR image to JSON**
        // -------------------------------------------------------
        string jsonResult = ocrResult.ToJson(includeConfidence: true);

        // -------------------------------------------------------
        // 5️⃣ Write the JSON file – **write JSON file C#** style
        // -------------------------------------------------------
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

### Expected Output

Programı çalıştırdığınızda (`dotnet run`) aşağıdakine benzer bir çıktı göreceksiniz:

```
=== Extracted Text ===
Hello world

✅ JSON with confidence saved to: C:\YourProject\output.json
```

Ve `output.json` dosyası, daha önce gösterilen yapılandırılmış JSON’ı, her kelime için güven yüzdeleriyle birlikte içerecek.

## Pro Tips & Edge Cases

- **Dosya eksikliği yönetimi:** Dinamik yollar bekliyorsanız `RecognizeImage` çağrısını `FileNotFoundException` için bir `try/catch` bloğuna sarın.
- **Farklı diller:** Fransızca için `ocrEngine.Language = "fr"` ayarlayın ya da `ocrEngine.LoadLanguage("custom.lang")` ile özel bir dil paketi yükleyin.
- **Büyük belgeler:** Çok sayfalı PDF’ler için önce her sayfayı bir görüntüye dönüştürün (ör. `Aspose.PDF` kullanarak) ve OCR adımlarını döngü içinde uygulayın.
- **Performans ayarı:** Hızlı sonuçlar yeterliyse `RecognitionMode.Fast`’a geçin—doğruluk bir miktar düşer ama hız artar.
- **JSON biçimlendirme:** Güzel biçimlendirilmiş JSON ister misiniz? Aspose JSON dizesini deserialize ettikten sonra `JsonConvert.SerializeObject` (Newtonsoft) ile `Formatting.Indented` kullanın.

## Frequently Asked Questions

**S: Bu .NET Framework ile çalışır mı?**  
C: Kesinlikle. Aynı NuGet paketi .NET Standard 2.0 hedefli, bu yüzden .NET Framework 4.6.1 ve üzeri sürümlerden referans alabilirsiniz.

**S: Bütün belge için bir güven değeri istiyorum, kelime bazında değil.**  
C: `OcrResult` ayrıca `OverallConfidence` özelliğini sunar. Bunu JSON’a manuel olarak ekleyebilirsiniz:

```csharp
var customObj = new
{
    Text = ocrResult.Text,
    OverallConfidence = ocrResult.OverallConfidence,
    Words = ocrResult.Words
};
string json = JsonConvert.SerializeObject(customObj, Formatting.Indented);
```

**S: JSON’u doğrudan bir web API’ye akıtabilir miyim?**  
C: Evet. `File.WriteAllText` yerine bir `HttpClient` POST’u kullanarak `jsonResult`’ı gönderin.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}