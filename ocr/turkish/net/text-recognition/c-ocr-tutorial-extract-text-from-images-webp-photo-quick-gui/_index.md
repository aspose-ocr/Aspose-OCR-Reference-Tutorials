---
category: general
date: 2026-03-17
description: c# OCR öğreticisi – görüntü dosyalarından metin nasıl çıkarılır, WebP
  fotoğraflarından metin nasıl okunur ve basit bir OcrEngine kullanarak görüntüyü
  metne nasıl dönüştürülür keşfedin.
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- read text from webp
- recognize text from photo
- convert image to text
language: tr
og_description: c# OCR öğreticisi, görüntü dosyalarından metin çıkarmayı, WebP fotoğraflarından
  metin okumayı ve birkaç satır kodla görüntüyü metne dönüştürmeyi gösterir.
og_title: c# OCR öğreticisi – Görüntülerden Dakikalar İçinde Metin Çıkarın
tags:
- C#
- OCR
- Image Processing
title: 'c# OCR öğreticisi: Görsellerden (WebP, Fotoğraf) Metin Çıkarma – Hızlı Rehber'
url: /tr/net/text-recognition/c-ocr-tutorial-extract-text-from-images-webp-photo-quick-gui/
---

for any missed bold or code. Keep bold formatting.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR öğretici – Görüntülerden Metin Çıkarma (WebP, Fotoğraf)

C#'ta **extract text from image** dosyalarından metin çıkarmak istediğiniz ama nereden başlayacağınızı bilmediğiniz oldu mu? Belki bir WebP ekran görüntünüz, bir makbuzun JPEG'i ya da taranmış bir PDF sayfanız var ve içindeki kelimeleri sadece istiyorsunuz. Bu **c# OCR tutorial** içinde fotoğraftan metin okuyan, WebP ve diğer modern formatları işleyen ve görüntüyü düz metne dönüştüren, birkaç satırda çalışan eksiksiz bir örnek üzerinden ilerleyeceğiz.

**Ne kazanacaksınız?** Herhangi bir metin resmini aranabilir dizelere dönüştürebilecek, bunları veritabanlarına aktarabilecek veya sonraki AI işlem hatlarına besleyebileceksiniz. Hiçbir sihir yok, sadece sağlam bir OCR motoru, birkaç .NET API'si ve her adımın “neden”ini açıklayan net açıklamalar.

## Gereksinimler

- **.NET 6 SDK** (veya daha yeni). Aşağıdaki kod .NET 6+ ile derlenir ve Windows, Linux veya macOS'ta çalışır.
- **Visual Studio 2022** veya tercih ettiğiniz herhangi bir editör (VS Code da gayet çalışır).
- **`Microsoft.Windows.SDK.Contracts`** NuGet paketi (`Windows.Media.Ocr` sağlar). Şu şekilde kurun:

```bash
dotnet add package Microsoft.Windows.SDK.Contracts
```

- İşlemek istediğiniz bir görüntü dosyası – bu öğreticide **WebP** fotoğrafı `photo.webp` adlı ve `YOUR_DIRECTORY` klasörüne yerleştirilmiş bir dosya kullanacağız.

> Pro ipucu: Windows dışı bir platformda iseniz, `OcrEngine`'i **Tesseract** gibi çapraz‑platform bir kütüphane ile değiştirebilirsiniz. Çevreleyen kod neredeyse aynı kalır.

## Adım 1: Bir C# OCR Öğretici Projesi Oluşturun

İlk olarak, yeni bir konsol uygulaması oluşturun. Bir terminal açın ve şu komutu çalıştırın:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Gerekli paketi ekleyin (yukarıda gösterildiği gibi) ve projeyi IDE'nizde açın. Bu iskelet, **c# OCR tutorial** için temiz bir başlangıç sağlar.

## Adım 2: Ad Alanlarını İçe Aktarın ve Görüntüyü Hazırlayın

Derleyicinin `OcrEngine`, `SoftwareBitmap` ve görüntü‑yükleme yardımcılarını nerede bulacağını bilmesi için birkaç `using` yönergesine ihtiyacımız var.

```csharp
using System;
using System.IO;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;
```

> **Bu ad alanları neden?**  
> `Windows.Media.Ocr`, tanıma işlemini gerçekleştiren `OcrEngine` sınıfını barındırır. `Windows.Graphics.Imaging`, görüntüyü (WebP dahil) motorun anlayabileceği bir `SoftwareBitmap`'e çözümlememizi sağlar. `System.IO` ve `Windows.Storage.Streams` yardımcıları dosya yüklemeyi sorunsuz hâle getirir.

Şimdi, görüntüyü yükleyin. Yerleşik çözücü WebP, HEIF, PNG, JPEG ve daha fazlasını işleyebilir, böylece ekstra eklentiler olmadan **read text from WebP** yapabilirsiniz.

```csharp
// Step 2: Load the image file into a SoftwareBitmap
string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

// Open the file as a random access stream
using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
{
    // Decode the image (auto-detects format)
    BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
    SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();
    
    // Optional: Convert to grayscale for better OCR accuracy
    SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);
    
    // Pass the bitmap to the next step
    await RecognizeTextAsync(grayBitmap);
}
```

> **Köşe durumu:** Görüntünüz zaten siyah‑beyaz ise dönüşüm adımını atlayabilirsiniz. Gri tonlamaya dönüştürme küçük bir performans kazancı sağlar ve genellikle gürültülü fotoğraflarda tanıma kalitesini artırır.

## Adım 3: OCR Motorunu Çalıştırın – Fotoğraftan Metin Tanıyın

İşte **c# OCR tutorial**'ın kalbi. `OcrEngine`'in bir örneğini oluşturur, bitmap'i ona verir ve tanınan metni alırız.

```csharp
static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
{
    // Step 3: Create the OCR engine instance – it automatically picks the best language
    OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

    if (ocrEngine == null)
    {
        Console.WriteLine("❌ No OCR engine available for the current language.");
        return;
    }

    // Perform recognition
    OcrResult ocrResult = await ocrEngine.RecognizeAsync(bitmap);

    // Step 4: Display the extracted text – this is the “convert image to text” part
    Console.WriteLine("📝 Recognized text:");
    Console.WriteLine(ocrResult.Text);
}
```

**Ne oluyor?**  
- `TryCreateFromUserProfileLanguages()` Windows kullanıcı profilinizin ayarlı olduğu dili(leri) seçer, genellikle İngilizce, İspanyolca vb. kapsar. Belirli bir dile ihtiyacınız varsa, `OcrEngine.TryCreateFromLanguage(new Language("fr-FR"))` kullanın.  
- `RecognizeAsync` ağır işi arka planda çalıştırır ve ham dizeyi, kelime sınırlama kutularını ve güven skorlarını içeren bir `OcrResult` döndürür.  
- Son olarak, `ocrResult.Text`'i yazdırırız, bu size **convert image to text** sonucunu verir ve başka bir yere yönlendirebilirsiniz.

## Adım 4: Tam, Çalıştırılabilir Örnek

Hepsini bir araya getirerek, `Program.cs` içine kopyalayıp yapıştırabileceğiniz bağımsız bir program burada. Derlenir, çalışır ve `photo.webp`'ten çıkarılan metni yazdırır.

```csharp
// Program.cs – Complete c# OCR tutorial example
using System;
using System.IO;
using System.Threading.Tasks;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;

class Program
{
    static async Task Main(string[] args)
    {
        // Replace with your actual directory and file name
        string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"❗ Image not found: {imagePath}");
            return;
        }

        // Load and optionally preprocess the image
        using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
        {
            BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
            SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();

            // Convert to grayscale – improves OCR accuracy on many photos
            SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);

            // Run OCR
            await RecognizeTextAsync(grayBitmap);
        }
    }

    static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
    {
        // Create OCR engine (auto‑detect language)
        OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

        if (ocrEngine == null)
        {
            Console.WriteLine("❌ Unable to create OCR engine. Ensure language packs are installed.");
            return;
        }

        // Perform recognition
        OcrResult result = await ocrEngine.RecognizeAsync(bitmap);

        // Output the extracted text
        Console.WriteLine("\n--- OCR Output ---");
        Console.WriteLine(result.Text);
        Console.WriteLine("--- End of Output ---\n");
    }
}
```

### Beklenen Çıktı

Eğer `photo.webp` “Hello, world! This is a test.” cümlesini içeriyorsa şöyle bir şey görürsünüz:

```
--- OCR Output ---
Hello, world!
This is a test.
--- End of Output ---
```

Tam satır sonları kaynak görüntünün düzenine bağlıdır, ancak **extract text from image** sonucu her zaman daha fazla işleyebileceğiniz düz bir dize olacaktır.

## Yaygın Sorular ve Köşe Durumları

### Bu diğer görüntü formatlarıyla çalışır mı?

Kesinlikle. Kullanılan çözücü (`BitmapDecoder`) JPEG, PNG, BMP, GIF, **WebP**, HEIF ve daha fazlasını otomatik algılar. Böylece kodu değiştirmeden **read text from WebP**, JPEG veya hatta TIFF'tan metin okuyabilirsiniz.

### OCR motoru düşük güven skoru döndürürse ne olur?

`ocrResult.Lines` ve her `OcrWord`'ün `ConfidenceScore`'unu inceleyebilirsiniz. Skor bir eşik değerinin (ör. 0.6) altında ise şunları düşünün:

- Görüntüyü ön‑işleme (kontrastı artırma, keskinleştirme, eğikliği düzeltme).
- Daha yüksek çözünürlüklü bir kaynak görüntü kullanma.
- Çok dilli destek için **Tesseract** gibi özel bir kütüphaneye geçiş.

### Aynı görüntüde birden fazla dili nasıl ele alabilirsiniz?

Her dil için ayrı `OcrEngine` örnekleri oluşturup sırasıyla çalıştırın veya karışık‑dil algılamayı destekleyen bir kütüphane kullanın. Yerleşik motor için bir `Language` nesnesi şu şekilde geçirilebilir:

```csharp
var spanishEngine = OcrEngine.TryCreateFromLanguage(new Language("es-ES"));
```

### Bunu Linux/macOS'ta çalıştırabilir miyim?

`Windows.Media.Ocr` API'si sadece Windows içindir. Windows dışı platformlarda OCR bölümünü **Tesseract** (`Tesseract.Net.SDK` aracılığıyla) ile değiştirin. Yükleme ve ön‑işleme kodu aynı kalır, bu yüzden bu **c# OCR tutorial**'ın geri kalanı hâlâ geçerlidir.

## Daha İyi Doğruluk İçin Pro İpuçları

- **Resize** büyük görüntüleri en uzun kenarında maksimum 2000 px olacak şekilde yeniden boyutlandırın – OCR motorları orta boyutlarda daha hızlı çalışır.
- **Denoise** fotoğraf grenliyse basit bir Gaussian bulanıklaştırma kullanın.
- **Deskew** bitmap'i metin tam yatay değilse; `SoftwareBitmap` `OcrEngine`'e geçmeden önce döndürülebilir.
- **Cache** `OcrEngine` örneğini bir toplu işlemde çok sayıda görüntü işliyorsanız; tekrar tekrar oluşturmak ek yük getirir.

## Keşfedilecek İlgili Konular

- **Convert image to text** çapraz‑platform projeler için **Tesseract** kullanarak.
- **Extract text from PDF** önce her sayfayı bir görüntüye render ederek.
- **Batch OCR**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}