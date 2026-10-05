---
category: general
date: 2026-01-15
description: Aspose OCR'i C#'ta kullanarak görüntüyü JSON'a dönüştürün. Görüntüden
  metni nasıl çıkaracağınızı, JSON sınırlama kutularını nasıl alacağınızı ve fiş görüntüsünü
  nasıl tanıyacağınızı öğrenin.
draft: false
keywords:
- convert image to json
- extract text from image
- aspose ocr c# example
- recognize receipt image
- json bounding boxes
language: tr
og_description: Aspose OCR kullanarak C#'de resmi JSON'a dönüştürün. Görüntüden metin
  çıkarmak, fiş görüntüsünü tanımak ve JSON sınırlama kutularını elde etmek için adım
  adım rehber.
og_title: Aspose OCR C# Rehberi ile Görüntüyü JSON'a Dönüştür
tags:
- Aspose OCR
- C#
- JSON
- Image Processing
title: Aspose OCR C# Kılavuzu ile Görüntüyü JSON'a Dönüştür
url: /tr/net/text-recognition/convert-image-to-json-with-aspose-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR C# Kılavuzu ile Görüntüyü JSON'a Dönüştürme

Hiç **görüntüyü JSON'a dönüştürmek** gerekti, ancak hem ham metni hem de kelime koordinatlarını sağlayabilecek bir kütüphanenin hangisi olduğunu bilmiyor muydunuz? Yalnız değilsiniz. Birçok geliştirici, özellikle makbuzlar gibi görüntü dosyalarından metin çıkarmaya çalışırken, aynı zamanda sonraki işlem adımları için makine‑okunur bir JSON yüküne ihtiyaç duyduklarında bu engelle karşılaşıyor.

Bu öğreticide, **Aspose OCR C# örneği** üzerinden görüntüden metin çıkarma, makbuz görüntüsünü tanıma ve her kelime için **JSON bounding boxes** üretme adımlarını göstereceğiz. Sonunda, herhangi bir API, veritabanı veya analiz boru hattına besleyebileceğiniz güzel biçimlendirilmiş bir JSON dizesi yazdıran, çalıştırmaya hazır bir konsol uygulamanız olacak.

> **Neler Öğreneceksiniz**  
> • Tam işlevsel bir C# projesi **görüntüyü JSON'a dönüştürür**  
> • Neden `IncludeBoundingBoxes`'ı etkinleştirdiğimize dair içgörü (`json bounding boxes` anahtarıdır)  
> • Farklı görüntü formatları ve dillerle başa çıkma ipuçları  

Hadi başlayalım.

---

## İhtiyacınız Olanlar

Before we dive into code, make sure you have the following prerequisites installed:

- **.NET 6.0 SDK** (or any later version) – kod .NET 6 hedefliyor ancak .NET Framework 4.7+ üzerinde de çalışıyor.  
- **Aspose.OCR for .NET** NuGet paketi – `dotnet add package Aspose.OCR` komutuyla ekleyebilirsiniz.  
- Projenizden referans alabileceğiniz bir klasöre yerleştirilmiş örnek makbuz görüntüsü (`receipt.jpg`).  
- Visual Studio 2022, VS Code veya tercih ettiğiniz herhangi bir IDE.

Başka bir dış hizmete ihtiyaç yok; her şey yerel olarak çalışır.

## Görüntüyü JSON'a Dönüştürme – Genel Bakış

Temel fikir basit: bir görüntüyü yükleyin, Aspose OCR'a İngilizce (veya desteklenen herhangi bir dil) tanımasını söyleyin, sınırlama kutularını eklemesini isteyin ve sonunda sonucu **JSON** formatında alın. Kütüphane tüm ağır işleri yapar—OCR, düzen analizi ve JSON serileştirme.

İşte akışın yüksek seviyeli bir diyagramı (küçük bir resim hayal edin):

```
[Image File] → Aspose OCR Engine → Recognition Options (JSON + Bounding Boxes) → JSON Output
```

Bu küçük diyagram, uygulayacağımız tüm boru hattını özetliyor.

## Adım 1: Projeyi Kurun ve Aspose OCR'ı Yükleyin

İlk olarak, yeni bir konsol projesi oluşturun ve Aspose OCR paketini ekleyin.

```bash
dotnet new console -n JsonOutputDemo
cd JsonOutputDemo
dotnet add package Aspose.OCR
```

> **Pro ipucu:** Visual Studio kullanıyorsanız, projeye sağ‑tıklayın → *Manage NuGet Packages* → **Aspose.OCR** aratın ve en son stabil sürümü (şu anda 23.12) yükleyin.

## Adım 2: Tanımak İstediğiniz Görüntüyü Yükleyin

Makbuz görüntüsünü okumak için `OcrImage.FromFile` metodunu kullanacağız. Yolun gerçek bir dosyaya işaret ettiğinden emin olun; aksi takdirde `FileNotFoundException` alırsınız.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // Step 2: Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

Görüntünüz `.csproj` dosyasının yanında ise, sadece `"receipt.jpg"` kullanabilirsiniz.

## Adım 3: JSON Sınırlama Kutuları İçin OCR Seçeneklerini Yapılandırın

Sihir, `OutputFormat = OutputFormat.Json` **ve** `IncludeBoundingBoxes = true` etkinleştirildiğinde gerçekleşir. İlki Aspose'a sonucu JSON olarak serileştirmesini söyler, ikincisi ise her kelime için `x`, `y`, `width` ve `height` ekler—tam da `json bounding boxes` için ihtiyacınız olan şey.

```csharp
        // Step 3: Configure OCR options
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };
```

Daha yüksek çözünürlük veya farklı bir dil gerekiyorsa `ocrOptions.Dpi` veya `ocrOptions.Language` ayarlarını da değiştirebilirsiniz.

## Adım 4: Tanıma İşlemini Gerçekleştirin – Görüntüden Metin Çıkarın

Şimdi `Recognize` metodunu çağırıyoruz. Bu metod, JSON dizesi, ham metin ve daha fazlasını içeren bir `OcrResult` nesnesi döndürür.

```csharp
        // Step 4: Perform recognition using English language and the configured options
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);
```

Başka dilleri işlemek istiyorsanız, `Language.English` yerine `Language.Spanish`, `Language.French` vb. kullanın. Aspose kutudan çıktığı gibi 30'dan fazla dili destekler.

## Adım 5: Sonucu Çıktılayın – JSON Yükünüz

Son olarak, JSON'ı konsola yazdırıyoruz. Gerçek bir uygulamada muhtemelen bir dosyaya yazdırır veya bir servise gönderirsiniz.

```csharp
        // Step 5: Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

Programı çalıştırdığınızda aşağıdaki snippet'e benzer bir JSON belgesi üretmelidir.

```json
{
  "Text": "Total $12.34\nDate 01/01/2024",
  "Words": [
    {
      "Text": "Total",
      "BoundingBox": { "X": 45, "Y": 112, "Width": 60, "Height": 20 }
    },
    {
      "Text": "$12.34",
      "BoundingBox": { "X": 110, "Y": 112, "Width": 70, "Height": 20 }
    },
    {
      "Text": "Date",
      "BoundingBox": { "X": 45, "Y": 140, "Width": 50, "Height": 20 }
    },
    {
      "Text": "01/01/2024",
      "BoundingBox": { "X": 100, "Y": 140, "Width": 120, "Height": 20 }
    }
  ]
}
```

Her kelimenin artık **JSON sınırlama kutusuna** sahip olduğuna dikkat edin—UI üzerine bindirme veya sonraki bir ayrıştırıcıya beslemek için mükemmel.

## Tam Çalışan Örnek

Aşağıda eksiksiz, kopyala‑yapıştır hazır program yer alıyor. Gizli kısımlar, dış çağrılar yok—sadece saf C#.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");

        // 3️⃣ Configure OCR options to get detailed JSON output with word positions
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };

        // 4️⃣ Perform recognition using English language and the configured options
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);

        // 5️⃣ Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

> **Dikkat Edilmesi Gerekenler:**  
> • **Dosya yolu hataları** – görüntünün konumunu iki kez kontrol edin.  
> • **Eksik NuGet paketi** – `Aspose.OCR` referansının olduğundan emin olun.  
> • **Desteklenmeyen görüntü formatları** – en iyi sonuç için JPEG, PNG, BMP veya TIFF kullanın.

## Yaygın Sorular ve Kenar Durumları

### **PDF sayfasını** JPEG yerine JSON'a dönüştürebilir miyim?

Evet. PDF sayfasını önce bir görüntüye dönüştürün (örneğin `Aspose.PDF` kullanarak), ardından bu görüntüyü aynı OCR boru hattına besleyin. JSON çıktısı aynı olacaktır çünkü OCR adımı yalnızca raster veriyi dikkate alır.

### Makbuz bulanıktaysa ne olur?

`ocrOptions` içinde DPI'yi artırın. Örneğin:

```csharp
ocrOptions.Dpi = 300; // higher DPI improves accuracy on low‑quality scans
```

Daha yüksek DPI bellek kullanımını artırabilir, bu yüzden kalite ve performans arasında denge kurun.

### Aynı makbuzda **birden fazla dil** (ör. İngilizce + İspanyolca) gerekiyor.

Dillerin bir dizisini geçirebilirsiniz:

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, new[] { Language.English, Language.Spanish }, ocrOptions);
```

Aspose, belirtilen sırada her dili tanımaya çalışacaktır.

### JSON'u bir dosyaya nasıl yazarım?

`Console.WriteLine` satırını şununla değiştirin:

```csharp
System.IO.File.WriteAllText("receipt.json", ocrResult.Json);
```

Artık diğer servislere gönderebileceğiniz kalıcı bir dosyanız var.

## Görsel Özet

![convert image to json example](convert-image-to-json.png "convert image to json example")

*Ekran görüntüsü, demoyu çalıştırdıktan sonra JSON yükünün konsol çıktısını gösterir.*

## Sonuç

Aspose OCR'ı C# ile kullanarak **görüntüyü JSON'a dönüştürme** yöntemini az önce gösterdik. `OutputFormat` ve `IncludeBoundingBoxes` yapılandırarak **görüntüden metin çıkarabilir**, **makbuz görüntüsünü tanıyabilir** ve her kelime için kesin **JSON sınırlama kutuları** elde edebilirsiniz. Tam, çalıştırılabilir kod yukarıdaki snippet'te yer alıyor, böylece hemen herhangi bir .NET projesine ekleyebilirsiniz.

Sırada ne var? JSON'u her kelimeyi vurgulayan bir ön‑uç görüntüleyiciye beslemeyi deneyin ya da verileri makbuzlardaki satır öğelerini sınıflandıran bir makine‑öğrenme modeline gönderin. Ayrıca diğer diller, daha yüksek DPI ayarları veya bir döngüde birden fazla görüntünün toplu işlenmesiyle de deney yapabilirsiniz.

Herhangi bir sorunla karşılaşırsanız, dosya yolları, DPI ve dil dizileriyle ilgili ipuçlarını hatırlayın. Bu demo için oluşturduğunuz GitHub deposunda yorum bırakmaktan veya bir issue açmaktan çekinmeyin. Kodlamanın tadını çıkarın ve resimleri yapılandırılmış JSON'a dönüştürmenin keyfini yaşayın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}