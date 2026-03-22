---
category: general
date: 2026-03-21
description: 'c# ocr eğitimi: C#''ta OCR kullanarak bir PNG görüntüsünden Urdu metnini
  nasıl çıkaracağınızı öğrenin. Adım adım kod, dil kurulumu ve pratik ipuçları dahil.'
draft: false
keywords:
- c# ocr tutorial
- extract urdu text
- recognize text image
- how to extract urdu
- ocr from png file
language: tr
og_description: 'c# ocr tutorial: C#''ta OCR kullanarak bir PNG görüntüsünden Urdu
  metnini nasıl çıkaracağınızı öğrenin. Kod ve ipuçlarıyla tam rehber.'
og_title: c# OCR öğreticisi – PNG Görsellerinden Urdu Metni Çıkarma
tags:
- OCR
- C#
- Urdu
- Image Processing
title: c# OCR öğreticisi – PNG Görsellerinden Urdu Metni Çıkar
url: /tr/net/text-recognition/c-ocr-tutorial-extract-urdu-text-from-png-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – PNG Görsellerinden Urdu Metni Çıkarma

Hiç **c# ocr tutorial** ararken bir PNG dosyasından Urdu metnini gerçekten çıkarabilen bir şey bulamadınız mı? Yalnız değilsiniz. Birçok projede—fatura işleme, belge arşivleme ya da hızlı bir çeviri aracı—metin görüntüsü verisini tanımanız gerekir ve dil önemlidir.  

Bu rehberde, bir OCR motoru kullanarak PNG’den Urdu metnini çıkaran tam, çalıştırmaya hazır bir çözümü adım adım inceleyeceğiz. Her satırın neden var olduğunu, eksik dil paketleriyle nasıl başa çıkılacağını ve görüntü mükemmel olmadığında ne yapılacağını göreceksiniz. Sonunda, kodu diğer diller veya dosya türleri için uyarlamaya yeterince güvenli olacaksınız.

## Öğrenecekleriniz

- Bir C# OCR kütüphanesini (gizli sihir yok) nasıl kuracağınız  
- Bir PNG dosyasından **urdu metni çıkarma** adımları  
- Dilin Urdu olarak ayarlanmasının önemi ve motorun eksik verileri otomatik olarak nasıl indirdiği  
- Çıktıyı doğrulama ve yaygın sorunları giderme yolları  

Harici dokümantasyon linklerine ihtiyaç yok—gereken her şey burada.

## Önkoşullar (Başlamadan Önce Gerekenler)

| Requirement | Why It Matters |
|-------------|----------------|
| .NET 6.0+ (or .NET Core 3.1) | Modern APIs and async support |
| Visual Studio 2022 (or VS Code with C# extension) | IDE with IntelliSense makes the code clearer |
| An OCR library that exposes `OcrEngine` (e.g., **Microsoft.Windows.SDK.Contracts** or a third‑party NuGet) | Provides `Language.Urdu` and `Recognize` methods |
| A PNG image containing Urdu text (e.g., `urdu_invoice.png`) | The source for **recognize text image** operation |

Eğer henüz bir OCR paketi kurmadıysanız, Package Manager Console’da şu tek satırı çalıştırın:

```powershell
Install-Package Microsoft.Windows.SDK.Contracts
```

Bu, ileride kullanacağımız `OcrEngine` sınıfını projenize ekleyecek.

> **Pro tip:** SDK, ilk kullanımda dil verilerini otomatik olarak indirir, bu yüzden Urdu dil paketlerini manuel olarak indirmenize gerek yoktur.

## Adım 1: OCR Kütüphanesini Kurun ve Referans Ekleyin

Bir motor oluşturabilmek için proje OCR paketine referans vermelidir. Dosyanızın en üstüne aşağıdaki `using` yönergelerini ekleyin:

```csharp
using System;
using Windows.Media.Ocr;          // Core OCR classes
using Windows.Graphics.Imaging;   // For loading PNG files
using Windows.Storage;            // File handling helpers
```

Bu ad alanları `OcrEngine`, `Language` ve görüntü‑yükleme yardımcılarını bize sunar. Farklı bir kütüphane kullanıyorsanız, benzer ad alanlarını arayın.

## Adım 2: Bir OCR Motoru Örneği Oluşturun  

Şimdi motoru gerçekten başlatıyoruz. Motor, piksel desenlerini karakter olarak yorumlayacak beyin gibidir.

```csharp
// Step 2: Initialize the OCR engine
OcrEngine ocrEngine = OcrEngine.TryCreateFromLanguage(new Language("ur"));
if (ocrEngine == null)
{
    Console.WriteLine("Failed to create OCR engine for Urdu. Check your language pack.");
    return;
}
```

**Neden önemli:** `TryCreateFromLanguage`, dil verileri yoksa `null` döner; bu da daha sonra çökmeden önce hızlı bir şekilde hatayı yakalamamızı sağlar.

## Adım 3: PNG Görüntüyü Yükleyin  

OCR motoru `SoftwareBitmap` nesneleriyle çalışır, ham dosya yollarıyla değil. Aşağıdaki yardımcı, diskteki bir PNG’yi yükleyip gerekli formata dönüştürür.

```csharp
// Step 3: Load the PNG image into a SoftwareBitmap
async Task<SoftwareBitmap> LoadImageAsync(string path)
{
    StorageFile file = await StorageFile.GetFileFromPathAsync(path);
    using var stream = await file.OpenReadAsync();
    var decoder = await BitmapDecoder.CreateAsync(stream);
    // Convert to Gray8 for best OCR accuracy
    return await decoder.GetSoftwareBitmapAsync(BitmapPixelFormat.Gray8, BitmapAlphaMode.Ignore);
}
```

**Köşe durumu:** PNG renkliyse, gri tonlamaya (`Gray8`) dönüştürmek tanıma performansını artırır; özellikle Urdu gibi ince diakritiklere sahip yazı sistemlerinde faydalıdır.

## Adım 4: Görüntüden Metni Tanıyın  

İşte **c# ocr tutorial**’ın kalbi—motoru görüntüyü okumaya zorlamak.

```csharp
// Step 4: Perform OCR on the loaded bitmap
async Task<string> RecognizeUrduAsync(string imagePath)
{
    SoftwareBitmap bitmap = await LoadImageAsync(imagePath);
    OcrResult result = await ocrEngine.RecognizeAsync(bitmap);
    return result.Text;
}
```

`OcrResult.Text` özelliği ham Unicode dizesini içerir. Daha önce dili Urdu olarak ayarladığımız için motor doğru script kurallarını uygular.

## Adım 5: Çıkarılan Metni Çıktılayın ve Doğrulayın  

Son olarak sonucu konsola yazdırıyoruz. Gerçek bir uygulamada bunu bir veritabanına kaydedebilir ya da bir çeviri servisine gönderebilirsiniz.

```csharp
// Step 5: Run the OCR and display the result
static async Task Main(string[] args)
{
    string imageFile = @"C:\Images\urdu_invoice.png"; // adjust path as needed
    string extracted = await RecognizeUrduAsync(imageFile);
    Console.WriteLine("=== Extracted Urdu Text ===");
    Console.WriteLine(extracted);
}
```

**Beklenen:** Görüntü netse, aşağıdakine benzer bir çıktı alırsınız:

```
=== Extracted Urdu Text ===
بل نمبر: 12345
تاریخ: 21/03/2026
کل رقم: 5,000 روپے
```

Çıktı bozuk görünüyorsa, görüntü kalitesini (kontrast, gürültü) kontrol edin ve ön‑işleme (ör. ikilileştirme) yapmayı düşünün.

## PNG Dosyasından Urdu Metni Çıkarma – Yaygın Tuzaklar  

1. **Düşük kontrast** – Ön plan ve arka plan renkleri benzer olduğunda OCR zorlanır. Kodu çalıştırmadan önce kontrastı artırmak için bir görüntü düzenleme aracı kullanın.  
2. **Yanlış DPI** – 300 dpi veya daha yüksek tarama, motorun daha fazla detay almasını sağlar.  
3. **Eksik dil paketi** – `TryCreateFromLanguage` ilk çağrıldığında bir indirme tetiklenebilir; makinenizin internet erişimi olduğundan emin olun.  

Bu sorunları giderdiğinizde **recognize text image** başarısı büyük ölçüde artar.

## Recognize Text Image: Diğer Formatlara Genişletme  

Bu eğitim PNG üzerine odaklansa da aynı iş akışı JPEG, BMP veya TIFF için de geçerlidir—sadece dosya uzantısını değiştirin ve çözücünün desteklediğinden emin olun. Temel satır aynı kalır: `await ocrEngine.RecognizeAsync(bitmap);`.

## PNG Dosyasından OCR İpuçları – Performans ve Ölçeklendirme  

- **Toplu işleme:** Birden fazla görüntüyü bir listeye yükleyip `Task.WhenAll` ile tanıma işlemlerini paralelleştirin.  
- **Motoru önbellekleme:** Tek bir `OcrEngine` örneği oluşturup çağrılar arasında yeniden kullanın; motoru sürekli yeniden oluşturmak ek yük getirir.  
- **Bellek yönetimi:** Kullanım sonrası `SoftwareBitmap` nesnelerini (`bitmap.Dispose()`) serbest bırakın, böylece süreç hafif kalır.

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda derleyip çalıştırabileceğiniz tüm program yer alıyor. Tüm `using` ifadeleri, async yönetimi ve hata kontrolleri dahildir.

```csharp
// Full C# OCR tutorial – Extract Urdu text from a PNG file
using System;
using System.Threading.Tasks;
using Windows.Media.Ocr;
using Windows.Graphics.Imaging;
using Windows.Storage;

class Program
{
    // Initialize the OCR engine for Urdu
    private static OcrEngine _ocrEngine = OcrEngine.TryCreateFromLanguage(new Language("ur"));

    static async Task Main(string[] args)
    {
        if (_ocrEngine == null)
        {
            Console.WriteLine("Urdu language pack not available. Ensure internet connectivity for automatic download.");
            return;
        }

        string imagePath = @"C:\Images\urdu_invoice.png"; // <-- change to your image location
        string text = await RecognizeUrduAsync(imagePath);
        Console.WriteLine("=== Extracted Urdu Text ===");
        Console.WriteLine(text);
    }

    // Load PNG and convert to grayscale bitmap
    private static async Task<SoftwareBitmap> LoadImageAsync(string path)
    {
        StorageFile file = await StorageFile.GetFileFromPathAsync(path);
        using var stream = await file.OpenReadAsync();
        var decoder = await BitmapDecoder.CreateAsync(stream);
        return await decoder.GetSoftwareBitmapAsync(BitmapPixelFormat.Gray8, BitmapAlphaMode.Ignore);
    }

    // Perform OCR and return the recognized text
    private static async Task<string> RecognizeUrduAsync(string imagePath)
    {
        SoftwareBitmap bitmap = await LoadImageAsync(imagePath);
        OcrResult result = await _ocrEngine.RecognizeAsync(bitmap);
        return result.Text;
    }
}
```

**Beklenen çıktı:** Konsol, görüntüde bulunan tam Urdu karakterlerini sağ‑dan‑sola sıralı şekilde yazdırır.

## Sonuç  

Bir **c# ocr tutorial** tamamladınız; PNG’den **urdu metni çıkarma**, dili yapılandırma ve sonucu güvenli bir şekilde işleme adımlarını gösterdik. Kütüphaneyi kurma, motoru oluşturma, görüntüyü yükleme, metni tanıma ve çıktıyı alma adımları, herhangi bir script ya da dosya türü için yeniden kullanılabilir bir desen oluşturur.  

Şimdi **recognize text image**’ı çok sayfalı PDF’lerde (her sayfayı önce PNG’ye çevirerek) denemeyi ya da bir çeviri API’siyle çıkarılan Urdu’yu otomatik olarak İngilizce’ye çevirmeyi düşünebilirsiniz. Bu temel iş akışını kavradığınızda, olasılıklar sınırsızdır.

Keyifli kodlamalar, OCR sonuçlarınız kristal‑gibi olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}