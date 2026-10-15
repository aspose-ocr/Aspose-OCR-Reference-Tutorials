---
category: general
date: 2026-02-20
description: C#'ta makbuzu nasıl okuyacağınızı, görüntüden metin çıkararak ve JSON'a
  dönüştürerek öğrenin. Aspose OCR kullanarak adım adım kod.
draft: false
keywords:
- how to read receipt
- extract text from image
- convert image to json
- load image file c#
- OCR receipt C#
- Aspose OCR tutorial
language: tr
og_description: C#'ta bir resim dosyası yükleyerek, Aspose OCR ile metin çıkararak
  ve sonucu JSON'a dönüştürerek fişi nasıl okuyacağınızı keşfedin. Tam kod örneği.
og_title: C#'ta Makbuz Okuma – Metni Çıkar, JSON'a Dönüştür
tags:
- C#
- OCR
- Image Processing
- JSON
title: C# ile Makbuz Okuma – Görüntüden Metin Çıkarma Tam Rehberi
url: /tr/net/text-recognition/how-to-read-receipt-in-c-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile Makbuz Okuma – Tam Kılavuz

Programlı olarak **makbuz okuma** görsellerini hiç merak ettiniz mi? Belki bir harcama‑takip uygulaması geliştiriyorsunuz ve bir market makbuzunun fotoğrafından satır‑kalemlerini çekmeniz gerekiyor. Benim deneyimime göre en büyük sıkıntı, o bulanık JPEG'i gerçekten kullanabileceğiniz yapılandırılmış verilere dönüştürmek. İyi haber? Birkaç C# satırı ve Aspose OCR ile **görüntüden metin çıkarabilir**, ardından **görüntüyü JSON’a dönüştürebilirsiniz**, bu neredeyse sihirli bir şekilde.

Bu öğreticide, **C# ile bir görüntü dosyası yükleyen**, OCR çalıştıran ve ayrıntılı bir JSON yükü üreten hazır‑çalıştır çözümle ayrılacaksınız. Harici hizmetler yok, karmaşık REST çağrıları yok—sadece herhangi bir konsol veya ASP.NET projesine ekleyebileceğiniz saf .NET kodu. Sonunda her adımın neden önemli olduğunu, yaygın kenar durumlarını (ör. standart dışı makbuz boyutları) nasıl ele alacağınızı ve JSON çıktısının gerçekte nasıl göründüğünü anlayacaksınız.

## İhtiyacınız Olanlar

- **.NET 6.0 veya üzeri** – kod `System.Drawing.Common` kullanıyor ve bu Windows, Linux ve macOS'ta desteklenir.
- **Aspose.OCR for .NET** – ücretsiz deneme NuGet paketini (`Aspose.OCR`) alabilir veya bir lisansınız varsa lisanslı bir kopya kullanabilirsiniz.
- Bir **örnek makbuz görüntüsü** (`receipt.jpg`) uygulamanızın okuyabileceği bir yere yerleştirilmiş.
- Tercih ettiğiniz herhangi bir IDE (Visual Studio, Rider, VS Code).  

Hepsi bu. Ek yapılandırma yok, API anahtarı yok.

---

## Adım 1 – Görüntü Dosyasını Yükle C# (Eylemde Birincil Anahtar Kelime)

OCR motoru sihrini yapmadan önce resmi belleğe almanız gerekir. Bu, birçok geliştiricinin gözden kaçırdığı klasik “C# ile görüntü dosyasını yükle” adımıdır.

```csharp
using System.Drawing;          // Required for Image
using Aspose.OCR;
using Aspose.OCR.Models;

// Path to your receipt image – adjust as needed
string imagePath = @"C:\Receipts\receipt.jpg";

// Load the image into a System.Drawing.Image object
Image receiptImage = Image.FromFile(imagePath);
```

**Neden önemli:**  
`Image.FromFile` dosyayı *bir kez* okur ve bir tutamaç açık tutar, bu hızlı bir OCR geçişi için mükemmeldir. Döngüde birçok makbuz işliyorsanız, dosyanın kilitlenmesini önlemek için `Image.FromStream` kullanmayı düşünün.

> **Pro ipucu:** *FileNotFoundException* alırsanız, yolu iki kez kontrol edin ve görüntünün gerçekten orada olduğundan emin olun. Göreli yollar da çalışır (`"./receipt.jpg"`), ancak mutlak yollar üretim işleri için daha güvenlidir.

## Adım 2 – OCR Motorunu Oluştur ve Yapılandır

Aspose OCR, hazır bir `OcrEngine` ile birlikte gelir. Model eğitmenize gerek yok; kütüphane zaten basılı metni okuyabiliyor, bu da çoğu makbuzun kullandığı şeydir.

```csharp
// Instantiate the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Optional: tweak recognition settings if your receipts are low‑contrast
ocrEngine.Config.Language = OcrLanguage.English;
ocrEngine.Config.DetectOrientation = true;   // Handles rotated receipts
```

**Bu seçenekleri neden ayarlıyoruz:**  
`DetectOrientation` motoru, makbuz ters tarandıysa görüntüyü otomatik olarak döndürmesini söyler. Dili ayarlamak karakter kümesini daraltır, bu da doğruluğu artırabilir—özellikle sadece İngiliz alfanümerik veriye ihtiyacınız olduğunda.

## Adım 3 – Görüntüyü Tanı ve JSON’a Dönüştür

Şimdi eğlenceli kısım: **görüntüden metin çıkar** ve **görüntüyü JSON’a dönüştür** tek bir çağrıda.

```csharp
// Perform OCR and get the result as a JSON string
string jsonResult = ocrEngine.RecognizeToJson(receiptImage);
```

`RecognizeToJson` metodu aşağıdaki öğeleri içeren zengin bir JSON yapısı döndürür:

- `Text`: düz birleştirilmiş metin.
- `Lines`: koordinatlarla birlikte satır nesnelerinin dizisi.
- `Words`: her kelimeye ait güven puanları.
- `Regions`: algılanan metin bloklarının sınırlayıcı kutuları.

Bu JSON’u tipli erişim için bir C# nesnesine serileştirebilirsiniz, ancak birçok senaryoda ham JSON’u yazdırmak yeterlidir.

## Adım 4 – JSON’u Çıktıla (veya Sakla)

Çıktıyı görelim ve onunla ne yapacağımızı tartışalım.

```csharp
// Write the JSON to the console – perfect for quick debugging
Console.WriteLine(jsonResult);

// Bonus: Save the JSON to a file for later processing
File.WriteAllText("receipt_output.json", jsonResult);
```

### Örnek Çıktı

```json
{
  "Text":"Walmart\n123 Main St\nItem A  $2.99\nItem B  $5.49\nTotal   $8.48",
  "Lines":[
    {"Text":"Walmart","BoundingBox":{"X":10,"Y":15,"Width":200,"Height":30}},
    {"Text":"123 Main St","BoundingBox":{"X":10,"Y":50,"Width":180,"Height":25}},
    {"Text":"Item A  $2.99","BoundingBox":{"X":10,"Y":85,"Width":210,"Height":28}},
    {"Text":"Item B  $5.49","BoundingBox":{"X":10,"Y":120,"Width":210,"Height":28}},
    {"Text":"Total   $8.48","BoundingBox":{"X":10,"Y":155,"Width":210,"Height":30}}
  ],
  "Words":[
    {"Text":"Walmart","Confidence":0.99,"BoundingBox":{...}},
    …
  ]
}
```

**Sonra ne yapılmalı?**  
`Lines` dizisini ayrıştırarak `Total` tutarını çekebilir ya da JSON’u harcama girişlerini saklayan bir sonraki hizmete besleyebilirsiniz. Sonuç zaten JSON olduğundan, doğrudan herhangi bir NoSQL veritabanına, Azure Function’a veya Power Automate akışına bağlayabilirsiniz.

## Adım 5 – Yaygın Kenar Durumlarını Ele Alma

En iyi OCR motorları bile birkaç şeyde takılır. Aşağıda **makbuz okuma** görselleri öğrenirken karşılaşabileceğiniz senaryolar var.

| Situation | Fix / Recommendation |
|-----------|----------------------|
| **Düşük çözünürlüklü makbuz (≤ 150 dpi)** | İlk olarak `Bitmap` ve `Graphics` (`InterpolationMode.HighQualityBicubic`) kullanarak görüntüyü büyütün. |
| **Döndürülmüş veya eğik makbuz** | `DetectOrientation = true` tutun. Şiddetli eğim için, `Image.RotateFlip` veya OpenCV gibi üçüncü‑taraf bir kütüphane ile ön işleme yapın. |
| **Renkli arka plan (ör. masada bir makbuz)** | OCR öncesinde gri tonlamaya çevirin ve kontrastı artırın (`ImageAttributes`). |
| **Tek fotoğrafta birden fazla makbuz** | Her makbuz bölgesini manuel olarak kırpın veya `ocrEngine.Config.RecognizeMultipleRegions = true` kullanın. |
| **Büyük dosyalar OutOfMemory hatasına neden oluyor** | `using` ifadelerini kullanarak `Image` nesnelerini hemen serbest bırakın, ya da parçalar halinde işleyin. |

```csharp
// Example: simple grayscale conversion
using (Bitmap bmp = new Bitmap(receiptImage))
{
    for (int y = 0; y < bmp.Height; y++)
        for (int x = 0; x < bmp.Width; x++)
        {
            Color c = bmp.GetPixel(x, y);
            int gray = (int)(c.R * 0.3 + c.G * 0.59 + c.B * 0.11);
            bmp.SetPixel(x, y, Color.FromArgb(gray, gray, gray));
        }
    receiptImage = (Image)bmp.Clone();
}
```

## Adım 6 – Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda şu anda derleyebileceğiniz *tam* program var. Tüm adımları, doğru `using` yönergelerini ve nazik hata yönetimini içerir.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptReaderDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image file C#
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY\receipt.jpg";

            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found: {imagePath}");
                return;
            }

            Image receiptImage;
            try
            {
                receiptImage = Image.FromFile(imagePath);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"⚠️ Failed to load image: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Create and configure OCR engine
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine
            {
                Config =
                {
                    Language = OcrLanguage.English,
                    DetectOrientation = true
                }
            };

            // -------------------------------------------------
            // 3️⃣ Recognize and convert to JSON
            // -------------------------------------------------
            string jsonResult;
            try
            {
                jsonResult = ocrEngine.RecognizeToJson(receiptImage);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"🛑 OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 4️⃣ Output results
            // -------------------------------------------------
            Console.WriteLine("🗂️ OCR JSON Result:");
            Console.WriteLine(jsonResult);

            // Optionally persist the JSON
            string outputPath = Path.Combine(
                Path.GetDirectoryName(imagePath) ?? ".", "receipt_output.json");
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"✅ JSON saved to {outputPath}");
        }
    }
}
```

**Çalıştırın:**  
Proje klasöründen `dotnet run`. Her şey doğru ayarlandıysa, konsolda JSON’u yazdırdığını ve makbuz görüntüsünün yanına kaydedildiğini göreceksiniz.

## Sonuç

C# ile **makbuz okuma** görsellerini baştan sona nasıl yapacağınızı yeni kapsadık. Görüntüyü yükleyerek, Aspose OCR’yi yapılandırarak ve `RecognizeToJson` çağırarak, **görüntüden metin çıkarabilir** ve **görüntüyü JSON’a dönüştürebilirsiniz**, neredeyse hiç ek kod olmadan. Yaklaşım ölçeklenebilir—tek bir makbuz demosundan, geceleri yüzlerce makbuzu işleyen bir toplu işleyiciye kadar.

İleride keşfedebileceğiniz adımlar:

- **JSON’u ayrıştır** tarihleri, toplamları ve satır kalemlerini çekmek için (`System.Text.Json` veya `Newtonsoft.Json` kullanın).
- **Bir veritabanına entegre et** (SQL, Cosmos DB) harcama kayıtlarını otomatik olarak saklamak için.
- **Bir UI ekle** (WinForms, WPF veya Blazor) böylece kullanıcılar makbuzları sürükle‑bırak yapabilir.
- **Aspose OCR’yi** başka bir motorla değiştir (Tesseract, Microsoft Azure OCR) lisans endişesi varsa—sadece aynı “C# ile görüntü dosyasını yükle” desenini koruyun.

Deney yapmaktan, şeyleri kırmaktan çekinmeyin ve ardından bir yenileme için buraya geri dönün. Bir sorunla karşılaşırsanız, topluluk (ve Aspose forumları) sormak için harika yerlerdir. Mutlu kodlamalar, ve o kağıt makbuzları temiz, aranabilir verilere dönüştürmenin tadını çıkarın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}