---
category: general
date: 2026-04-01
description: OCR doğruluğunu artırmak için görüntüyü ön işleme tabi tutun. Aspose.OCR
  kullanarak otomatik eğim düzeltme, gürültü giderme ve siyah‑beyaz dönüşümünü nasıl
  uygulayacağınızı öğrenin.
draft: false
keywords:
- preprocess image for OCR
- improve OCR accuracy
- black and white OCR
- Aspose OCR preprocessing
- image deskew C#
- OCR noise reduction
language: tr
og_description: OCR doğruluğunu artırmak için görüntüyü ön işleme tabi tutun. Bu adım
  adım kılavuz, C#'ta otomatik eğri düzeltme, gürültü giderme ve siyah‑beyaz dönüşümünü
  gösterir.
og_title: OCR için Görüntüyü Ön İşleme – Aspose.OCR ile Doğruluğu Artırın
tags:
- OCR
- C#
- Image Processing
title: OCR için Görüntüyü Ön İşleme – Aspose.OCR ile Doğruluğu Artırın
url: /tr/net/ocr-optimization/preprocess-image-for-ocr-boost-accuracy-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR için Görüntüyü Ön İşleme – Aspose.OCR ile Doğruluğu Artırın

OCR sonuçlarınızın, kaynak görüntü iyi görünmesine rağmen karışık bir karmaşa gibi görünmesinin nedenini hiç merak ettiniz mi? Muhtemelen kritik bir adımı kaçırıyorsunuz: **preprocess image for OCR**.  
Bu öğreticide, eğimli ve gürültülü bir resmi nasıl temizleyeceğinizi adım adım göstereceğiz, böylece motor bunu bir profesyonel gibi okuyabilir. Sonunda **improve OCR accuracy**'de belirgin bir artış görecek ve Aspose.OCR'un basit hale getirdiği **black and white OCR** tekniğine aşina olacaksınız.

## Öğrenecekleriniz

Aspose.OCR NuGet paketinin kurulumundan, görüntünüzü otomatik döndürme, gürültü giderme ve ikiliye çevirme işlemlerini yapan `PreprocessOptions` yapılandırmasına kadar her şeyi ele alacağız. Ayrıca aşırı döndürme veya düşük kontrastlı taramalar gibi uç durumları nasıl ele alacağınız konusunda pratik ipuçları alacaksınız, böylece ne olursa olsun tanıma kalitesini yüksek tutabilirsiniz. Harici belgelere gerek yok; tüm çözüm burada.

### Ön Koşullar

- .NET 6.0 veya daha yenisi (örnek .NET 6 ile derlenir, ancak daha eski sürümler de çalışır)
- C# ve Visual Studio (veya tercih ettiğiniz herhangi bir IDE) hakkında temel bilgi
- Eğik veya gürültülü bir görüntü dosyası (biz ona `skewed_noisy.jpg` diyeceğiz)

Bu maddeleri işaretlediyseniz, başlayalım.

## OCR için Görüntüyü Ön İşleme – Ön İşlemenin Önemi

Bir OCR motorunu seçici bir okuyucu gibi düşünün: sayfa eğik, lekeli ya da çok gri ise, kelimeler üzerinde takılır. Ön‑işleme üç yaygın sorunu çözer:

1. **Rotation** – Auto‑deskew sayfayı düzleştirir, böylece satırlar yatay olur.  
2. **Noise** – Denoising, aksi takdirde karakter gibi görünen rastgele pikselleri temizler.  
3. **Contrast** – Binarizing (siyah‑beyaz dönüşüm) motorun net bir ön‑arkaplan ayrımı yapmasını sağlar.

Birlikte, **improve OCR accuracy** hedefleyen herhangi bir iş akışının temelini oluşturur.

![preprocess image for OCR example](https://example.com/ocr-preprocess.png "preprocess image for OCR example")

*(Alt text: “OCR için görüntü ön işleme örneği, ikileştirme öncesi ve sonrası gösterimi”)*

## Adım 1: Aspose.OCR'ı Kurun

İlk olarak, kütüphaneyi edinin. Terminalinizi (veya Package Manager Console) açın ve şu komutu çalıştırın:

```bash
dotnet add package Aspose.OCR
```

Veya Visual Studio arayüzünü tercih ediyorsanız, **Dependencies → Manage NuGet Packages** üzerine sağ tıklayın, **Aspose.OCR**'ı arayın ve **Install**'a tıklayın. Paket, ön işleme için kullanılan `Filters` ad alanı da dahil olmak üzere ihtiyacınız olan her şeyi içerir.

## Adım 2: OCR Motorunu Oluşturun

Kütüphane yerinde olduğuna göre, bir `OcrEngine` örneği oluşturabiliriz. Bu nesne, tüm tanıma işlemlerinin giriş noktasıdır.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // Step 2: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // The rest of the steps follow...
    }
}
```

İlk olarak motoru neden oluşturuyoruz? Motor, küresel ayarları (dil, bölge vb.) tutar ve özellikle bir sonraki adımda yapılandıracağımız `PreprocessOptions`'ı içerir.

## Adım 3: Ön İşleme Seçeneklerini Yapılandırın

İşte sihrin gerçekleştiği yer. Üç bayrağı etkinleştireceğiz:

- `AutoDeskew` – Rotasyonu otomatik olarak algılar ve düzeltir.
- `DenoiseLevel = DenoiseLevel.Medium` – Gürültüyü temizleme ile ince detayları koruma arasında bir denge kurar.
- `Binarize` – Motoru klasik **black and white OCR** yaklaşımına zorlayan siyah‑beyaz bir çıktı üretir.

```csharp
// Step 3: Set up preprocessing to clean the image
PreprocessOptions preprocessOptions = new PreprocessOptions
{
    AutoDeskew = true,                     // Correct rotation automatically
    DenoiseLevel = DenoiseLevel.Medium,   // Reduce noise while preserving details
    Binarize = true                        // Convert to black‑and‑white for better recognition
};

// Attach options to the engine
ocrEngine.PreprocessOptions = preprocessOptions;
```

**Neden bu ayarlar?** Auto‑deskew, çoğu yaygın eğimi (yaklaşık ~15°'ye kadar) ele alır. Medium denoise tipik taranmış belgeler için uygundur; yoğun lekeli taramalar için `High`'a çıkarabilirsiniz, ancak küçük karakterlerin kaybolmasına dikkat edin. Binarization, **black and white OCR**'ın temel taşıdır—tanıyıcıyı şaşırtan ince gri geçişleri ortadan kaldırır.

## Adım 4: Gürültülü Bir Görüntüde Tanıma Çalıştırın

Motor hazır olduğunda, problemli görüntünüzün yolunu ona verin. `Recognize` metodu, çıkarılan metin ve güven puanlarını içeren bir `OcrResult` nesnesi döndürür.

```csharp
// Step 4: Recognize text from a skewed and noisy image
// Replace the path with your actual image location
var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/skewed_noisy.jpg");

// Output the raw text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

Her şey sorunsuz çalışırsa, konsolda temiz bir metin bloğu görmelisiniz. Motor ayrıca **improve OCR accuracy** için sayısal bir ölçüm gerektiğinde `ocrResult.Confidence` değerini sunar.

## Adım 5: Sonucu Doğrulayın ve Daha İyi Doğruluk İçin İnce Ayar Yapın

Çıktıyı görmek harika, ancak özellikle alışılmadık yazı tiplerinde birkaç hatalı okuma fark edebilirsiniz. İşte birkaç hızlı kontrol:

1. **Inspect Confidence** – 0.7'nin altındaki değerler genellikle sorunlu bir alanı gösterir. Bunları kaydedebilir ve daha yüksek bir `DenoiseLevel` ile yeniden işleyip işlemeyeceğinize karar verebilirsiniz.
2. **Adjust Binarization Threshold** – Aspose, `PreprocessOptions.BinarizationThreshold` aracılığıyla özel bir eşik değeri belirlemenize izin verir. Daha düşük sayılar daha fazla gri tutar, daha yüksek sayılar daha katı siyah‑beyaz uygular.
3. **Crop or Resize** – Görüntü çok büyükse, motorun önüne vermeden önce ~150 DPI'ye küçültün; bu işlem süresini hızlandırır ve aslında doğruluğu artırabilir.

```csharp
// Example: Increase denoise for a very dirty scan
ocrEngine.PreprocessOptions.DenoiseLevel = DenoiseLevel.High;

// Re‑run recognition
var refinedResult = ocrEngine.Recognize("YOUR_DIRECTORY/very_dirty.jpg");
Console.WriteLine(refinedResult.Text);
```

## Bonus: Daha İyi Sonuçlar İçin Siyah ve Beyaz OCR Kullanımı

Bazen geliştiricilerin “sadece gri tonlamayı kullan” dediğini duyarsınız—ancak **black and white OCR** yaklaşımı, özellikle kaynak materyalin eşit olmayan aydınlatması olduğunda, genellikle daha iyi performans gösterir. İkili bir görüntü zorlayarak, motorun karakter olarak algılayabileceği ince gölgeleri ortadan kaldırırsınız.

Daha fazla deneme yapmak isterseniz, ikili görüntüyü kendiniz oluşturup motorun içine besleyebilirsiniz:

```csharp
// Generate a binary bitmap manually (optional)
Bitmap binaryBitmap = ocrEngine.PreprocessOptions.ApplyFilters(
    Image.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg")
);

// Pass the bitmap directly
var bitmapResult = ocrEngine.Recognize(binaryBitmap);
Console.WriteLine(bitmapResult.Text);
```

## Tam Çalışan Örnek

Hepsini bir araya getirerek, yeni bir C# projesine kopyalayıp yapıştırabileceğiniz çalıştırmaya hazır bir konsol uygulaması burada:

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure preprocessing (auto‑deskew, denoise, binarize)
        PreprocessOptions preprocessOptions = new PreprocessOptions
        {
            AutoDeskew = true,
            DenoiseLevel = DenoiseLevel.Medium,
            Binarize = true
        };
        ocrEngine.PreprocessOptions = preprocessOptions;

        // 3️⃣ Recognize the image (replace with your file path)
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/skewed_noisy.jpg");

        // 4️⃣ Show the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);

        // 5️⃣ Optional: tweak settings if confidence is low
        if (ocrResult.Confidence < 0.7)
        {
            Console.WriteLine("\nLow confidence detected – increasing denoise level.");
            ocrEngine.PreprocessOptions.DenoiseLevel = DenoiseLevel.High;
            var retryResult = ocrEngine.Recognize("YOUR_DIRECTORY/skewed_noisy.jpg");
            Console.WriteLine("=== Refined Output ===");
            Console.WriteLine(retryResult.Text);
        }
    }
}
```

**Beklenen konsol çıktısı**

```
=== OCR Output ===
The quick brown fox jumps over the lazy dog.

=== Refined Output ===
The quick brown fox jumps over the lazy dog.
```

*Elbette gerçek metniniz farklı olacaktır, ancak aynı temiz formatlamayı fark edeceksiniz.*

## Sonuç

Aspose.OCR kullanarak **preprocess image for OCR**'ı nasıl yapacağınızı ve her adımın—auto‑deskew, denoise ve siyah‑beyaz dönüşüm—**improve OCR accuracy**'de neden kritik bir rol oynadığını gösterdik. Yukarıdaki kodu izleyerek, belgeler arasında dolaşmadan gürültülü ve eğimli taramalarda güvenilir sonuçlar elde edeceksiniz.

Sıradaki adım ne? Bu iş akışını dil‑spesifik ayarlarla (ör. `ocrEngine.Language = Language.English`) birleştirmeyi deneyin veya temizlenmiş bitmap'i sonraki bir NLP modeline besleyin. Ayrıca düşük kontrastlı makbuzlar veya el yazısı notlar için **black and white OCR** etkisini ince ayarlamak amacıyla `BinarizationThreshold` ile deneyler yapabilirsiniz.

Herhangi bir sorunla karşılaşırsanız yorum bırakmaktan çekinmeyin, ya da OCR'dan ekstra doğruluk elde etmek için kendi ipuçlarınızı paylaşın. Kodlamanın tadını çıkarın ve metniniz her zaman okunaklı olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}