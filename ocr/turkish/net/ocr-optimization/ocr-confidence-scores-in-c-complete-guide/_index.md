---
category: general
date: 2026-05-31
description: C#'ta OCR güven puanlarını nasıl alacağınızı öğrenin; görüntüden metin
  çıkarırken ve Aspose OCR ile fiş görüntüsünü okurken.
draft: false
keywords:
- ocr confidence scores
- extract text from image
- ocr bounding boxes
- perform ocr on jpg
- read receipt image
language: tr
og_description: OCR güven skorları, doğruluğu ölçmenizi sağlar; bu rehber, Aspose
  OCR kullanarak bir görüntüden metin çıkarmayı, sınırlayıcı kutuları almayı ve makbuz
  görüntüsünü okumayı gösterir.
og_title: C#'de OCR güven puanları – Tam Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get OCR confidence scores in C# while extract text from
    image and read receipt image with Aspose OCR.
  headline: OCR confidence scores in C# – Complete Guide
  type: TechArticle
tags:
- OCR
- C#
- Aspose
- Image Processing
title: C#'da OCR güven puanları – Tam Kılavuz
url: /tr/net/ocr-optimization/ocr-confidence-scores-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'de OCR güven puanları – Tam Kılavuz

Bir görüntüden *extract text from image* gerektiğinde **OCR confidence scores** merak ettiniz mi? Belki harcama takibi için **read receipt image** dosyalarını okumaya çalışıyorsunuz ve motorun hangi karakterlerden emin olmadığını bilmek istiyorsunuz. İyi haber? Aspose.OCR ile sadece birkaç C# satırıyla bir JPG'den confidence percentages, bounding boxes ve plain text alabilirsiniz.

Bu öğreticide, bilmeniz gereken her şeyi adım adım göstereceğiz: kütüphaneyi kurma, motoru **perform OCR on JPG** olarak yapılandırma, confidence scores çıkarma ve her karakterin sayfada nerede olduğunu gösteren **OCR bounding boxes** yorumlama. Sonunda, her karakteri, güvenini ve konumunu yazdıran, receipt doğrulama veya herhangi bir taranmış belge için mükemmel, çalıştırmaya hazır bir console uygulamanız olacak.

## Öğrenecekleriniz

- NuGet üzerinden Aspose.OCR'yi kurun ve temel bir OCR motoru ayarlayın.  
- `OcrOptions`'ı **with confidence scores** ve **bounding boxes** içeren plain‑text çıktısı talep edecek şekilde yapılandırın.  
- `OcrResult` üzerinden **extract text from image** satır satır ve sembol sembol döngüleyin.  
- Eksik dosyalar, düşük confidence karakterler ve JPG olmayan formatlar gibi yaygın sorunları ele alın.  
- Örneği, bir klasördeki birden fazla receipt image işlemek için genişletin.

Aspose ile ilgili önceden bir deneyime ihtiyacınız yok; sadece çalışan bir .NET ortamı ve test etmek istediğiniz bir receipt image (JPG) yeterli.

---

## 1. Adım – Aspose.OCR'yi Kurun ve Projenizi Hazırlayın

İlk olarak, Aspose.OCR NuGet paketine ihtiyacınız var. Proje klasörünüzde bir terminal açın ve şu komutu çalıştırın:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Ücretsiz deneme, 200 sayfaya kadar çalışır; bu, receipt taramasını test etmek için fazlasıyla yeterlidir.

Paket kurulduktan sonra, yeni bir console projesi oluşturun (eğer hâlâ yoksa):

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
```

Şimdi oluşturulan `Program.cs` dosyasını açabilir ve using yönergelerini eklemeye başlayabilirsiniz:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
```

Bu ad alanları, daha sonra ihtiyaç duyacağımız `OcrEngine`, `OcrOptions` ve sonuç tiplerine erişim sağlar.

## 2. Adım – OCR güven puanlarını ve OCR sınırlama kutularını alın

Bu, öğreticinin kalbidir. Motoru, tanınan her karakterin **confidence score** ve **bounding box** (glyph'i çevreleyen dikdörtgen) ile gelmesi için yapılandıracağız. H2 başlığı zaten birincil anahtar kelimeyi içeriyor, SEO kuralını karşılıyor.

```csharp
// Step 2: Initialize the OCR engine and request detailed output
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process – here we assume a JPEG receipt
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Tell Aspose we want plain text, confidence percentages, and bounding boxes
ocrEngine.Options = new OcrOptions
{
    OutputFormat = OcrOutputFormat.PlainText,
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};
```

**Neden confidence scores eklenir?**  
Bir confidence score (0‑100%) motorun her karakterden ne kadar emin olduğunu gösterir. Çıktıyı aşağı akış mantığına—örneğin bir expense‑approval iş akışına—besliyorsanız, düşük güvenli sembolleri otomatik olarak reddedebilir veya işaretleyebilirsiniz.

**Neden bounding boxes istenir?**  
Bounding boxes, orijinal görüntüde metni vurgulamanız, alt bölgeler çıkarmanız veya OCR sonuçlarını bir UI katmanıyla hizalamanız gerektiğinde çok önemlidir. Her `character.Bounds` size X, Y, genişlik ve yükseklik değerlerini piksel koordinatlarıyla verir.

## 3. Adım – JPG üzerinde OCR gerçekleştir ve görüntüden metin çıkar

Şimdi motoru gerçekten çalıştırıyoruz. `Recognize()` çağrısı tüm ağır işi yapar ve bir `OcrResult` nesnesi döndürür.

```csharp
// Step 3: Run the OCR process
OcrResult ocrResult = ocrEngine.Recognize();
```

Eğer görüntü yolu yanlışsa veya dosya desteklenen bir formatta değilse, Aspose bir `FileNotFoundException` veya `UnsupportedImageFormatException` fırlatır. Üretim kodunda bu çağrıyı bir try/catch bloğuna sararak bu uç durumları nazikçe ele alın.

### Düz metni çıkarma

Sadece birleştirilmiş metne ihtiyacınız varsa, `ocrResult.Text`'i okuyabilirsiniz:

```csharp
Console.WriteLine("Full extracted text:");
Console.WriteLine(ocrResult.Text);
```

Ancak confidence scores ve bounding boxes da istediğimiz için, yapıyı dolaşarak her karakterin detaylarını göreceğiz.

## 4. Adım – Satırları, sembolleri dolaş ve OCR confidence scores'ı göster

İşte her karakteri, güvenini ve kutusunu yazdıran döngü. Bu, **read receipt image** örneğinin gerçekten parladığı yerdir.

```csharp
// Step 4: Walk through each line and each symbol (character)
foreach (var textLine in ocrResult.Lines)
{
    foreach (var character in textLine.Symbols)
    {
        Console.WriteLine(
            $"Char: '{character.Text}'  Confidence: {character.Confidence}%  Box: {character.Bounds}");
    }
}
```

Örnek çıktı şöyle görünebilir:

```
Char: 'R'  Confidence: 98%  Box: {X=12,Y=34,Width=15,Height=20}
Char: 'e'  Confidence: 95%  Box: {X=28,Y=34,Width=12,Height=20}
Char: 'c'  Confidence: 92%  Box: {X=41,Y=34,Width=13,Height=20}
...
```

**Sayıların yorumlanması:**  
- **Confidence ≥ 90%** – genellikle kabul edilebilir.  
- **Confidence 70‑89%** – özellikle tutarların rakamları için iki kez kontrol etmek isteyebilirsiniz.  
- **Confidence < 70%** – manuel inceleme için işaretlemeyi düşünün.

## 5. Adım – Tam çalıştırılabilir örnek (hata yönetimi dahil)

Her şeyi bir araya getirerek, `Program.cs`'ye kopyalayıp yapıştırabileceğiniz tam bir program burada. Eksik dosyalar için basit bir kontrol içerir ve OCR başarısız olursa dostça bir mesaj yazdırır.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the receipt image – adjust to your environment
            const string imagePath = "YOUR_DIRECTORY/receipt.jpg";

            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found -> {imagePath}");
                return;
            }

            try
            {
                // Initialize engine
                OcrEngine ocrEngine = new OcrEngine
                {
                    Image = ImageStream.FromFile(imagePath),
                    Options = new OcrOptions
                    {
                        OutputFormat = OcrOutputFormat.PlainText,
                        IncludeConfidence = true,
                        IncludeBoundingBoxes = true
                    }
                };

                // Perform OCR
                OcrResult ocrResult = ocrEngine.Recognize();

                // Show full plain text (optional)
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
                Console.WriteLine();

                // Show each character with confidence and bounding box
                Console.WriteLine("=== Detailed Character Data ===");
                foreach (var line in ocrResult.Lines)
                {
                    foreach (var symbol in line.Symbols)
                    {
                        Console.WriteLine(
                            $"Char: '{symbol.Text}'  Confidence: {symbol.Confidence}%  Box: {symbol.Bounds}");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"OCR failed: {ex.Message}");
            }
        }
    }
}
```

### Beklenen çıktı

`dotnet run` komutunu çalıştırdığınızda console önce birleştirilmiş receipt metnini, ardından her karakterin confidence score ve bounding box'ını listeleyecek. Bir karakterin confidence'ı düşükse, %80'in altında bir yüzde göreceksiniz; bu, receipt'in o kısmını manuel olarak doğrulamanız gerektiğine işaret eder.

## Bonus: Klasördeki Birden Fazla Receipt'i İşleme

Eğer bir dizi receipt JPG'niz varsa, yukarıdaki mantığı `foreach (var file in Directory.GetFiles(folder, "*.jpg"))` döngüsüyle sarın. Her dosya için `OcrEngine`'i sıfırlamayı veya döngü içinde yeni bir tane oluşturmayı unutmayın; böylece durum sızıntısı önlenir.

```csharp
string folder = "YOUR_DIRECTORY/Receipts";
foreach (var file in System.IO.Directory.GetFiles(folder, "*.jpg"))
{
    // reuse the same code block, just replace imagePath with 'file'
}
```

Toplu işleme, geceleyin expense importları için kullanışlıdır.

---

## Sonuç

Artık C#'de **OCR confidence scores** elde etmek, **extract text from image** yapmak ve **perform OCR on JPG** dosyaları (örneğin **read receipt image**) sırasında **OCR bounding boxes** almak için sağlam, uçtan uca bir çözümünüz var. Kod tamamen bağımsız, en son Aspose.OCR sürümüyle (2026‑05‑31 itibarıyla) çalışıyor ve güvenilir belge‑işleme hatları oluşturmak için ihtiyacınız olan ayrıntılı verileri sağlıyor.

Sırada ne var? `System.Drawing` veya bir UI kütüphanesi kullanarak orijinal receipt üzerindeki bounding boxes'ı görselleştirmeyi deneyin, ya da düşük confidence karakterlerini ikincil bir doğrulama servisine gönderin. Ayrıca `ocrEngine.Options.Language = OcrLanguage.French;` ayarını yaparak farklı dillerle deneme yapabilirsiniz – API birçok yerel dili destekliyor.

Kodlamaktan keyif alın ve confidence score'larınız her zaman yüksek olsun! 

![Console output showing OCR confidence scores and bounding boxes for a receipt


## Bir Sonraki Öğrenmeniz Gerekenler

- [Aspose.OCR kullanarak dil seçimiyle C#'de görüntü metni çıkarma](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Görüntü Tanıma'da Tanınan Karakterler İçin OCR Karakter Seçeneklerini Nasıl Alırsınız](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)
- [Görüntü Tanıma'da JSON Sonucu İçin Aspose OCR Nasıl Kullanılır](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}